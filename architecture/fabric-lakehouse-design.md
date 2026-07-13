# Microsoft Fabric Lakehouse Design: Enterprise AI Foundation

**Author:** Jennifer Kelleman
**Platform:** Microsoft Fabric (OneLake + Lakehouse)

---

## Design Intent

This document captures the key architectural decisions behind an enterprise-scale Microsoft Fabric Lakehouse deployment designed to support both traditional analytics and AI/ML workloads. It's written to serve two audiences simultaneously: the data engineers who will implement it, and the executives who need to understand why these decisions were made.

That dual-audience requirement isn't an accident. In enterprise AI programs, architecture decisions that can't be explained to a CIO or CDO in plain language tend to get revisited — often at the worst possible moment.

---

## The OneLake Principle

Everything in this design flows from one foundational choice: **OneLake as the single source of truth.**

Microsoft Fabric's OneLake is the organizational data lake built into the platform. Unlike a traditional data lake that lives in Azure Data Lake Storage Gen2 and must be explicitly connected to downstream services, OneLake is the native storage layer for every Fabric workload — Lakehouses, Warehouses, Eventhouse, and the semantic model layer all read from and write to OneLake automatically.

### What This Means in Practice

| Traditional Multi-System Stack | Fabric OneLake Architecture |
|---|---|
| Separate storage for each tool (ADF, Synapse, Power BI datasets) | One storage layer shared by all workloads |
| Multiple copies of data with independent governance | One copy of data, governed once |
| Lineage across systems is manual or tooled | Native end-to-end lineage built in |
| Separate security models per service | Unified security model across all workloads |
| Data movement costs (egress, compute) at every integration | No egress within tenant; compute-only costs |

For an AI program, the OneLake advantage is especially significant: every model, notebook, and semantic model query is reading from the same governed, lineage-tracked data. There is no "model trained on data that doesn't match what's in the dashboard" problem — because there is only one copy of the data.

---

## Workspace Architecture

### Workspace Strategy: Domain-Aligned, Not Project-Aligned

A common mistake in Fabric deployments is creating workspaces per project. This creates governance sprawl, makes cross-domain analytics difficult, and produces lineage graphs that don't reflect actual data flows.

This design uses **domain-aligned workspaces** — one workspace per major data domain (Finance, Customer, Operations, Product, HR) — with a shared **Platform Services** workspace for common infrastructure.

```
┌─────────────────────────────────────────────────────────┐
│                    OneLake (Tenant)                      │
├───────────┬───────────┬───────────┬─────────┬───────────┤
│ Finance   │ Customer  │Operations │ Product │    HR     │
│ Workspace │ Workspace │ Workspace │Workspace│ Workspace │
├───────────┴───────────┴───────────┴─────────┴───────────┤
│              Platform Services Workspace                 │
│   (Shared Pipelines · Governance · Semantic Models)     │
└─────────────────────────────────────────────────────────┘
```

### Why This Matters for AI

When an AI application needs to join customer data with finance data, it can do so in one query — because both domains live in OneLake under a single security model. There is no "data access request" delay, no ad-hoc ETL to build, no copy to make. The AI application can read directly from certified Gold tables in each domain workspace.

---

## Lakehouse Item Design

Each domain workspace contains a **Lakehouse item** with three zones corresponding to the medallion architecture:

```
[Domain] Lakehouse
│
├── Files/          ← Raw file landing zone (CSV, JSON, Parquet, etc.)
│
├── Tables/
│   ├── bronze_*    ← Raw ingested delta tables (schema-as-source)
│   ├── silver_*    ← Cleaned, conformed, documented tables
│   └── gold_*      ← Curated business-domain views, AI-ready
│
└── Notebooks/      ← Transformation and quality notebooks (linked)
```

### Delta Lake as the Standard Format

All tables in the Lakehouse use **Delta Lake** format. Delta Lake provides:
- **ACID transactions** — reliable reads even during active writes
- **Time travel** — query the state of any table at any historical point
- **Schema enforcement** — rejects writes that violate the table schema
- **Optimize and V-Order** — Fabric automatically applies V-Order optimization, which significantly improves read performance for Power BI and ML workloads

For AI workloads specifically, Delta time travel is a governance advantage: every model training run can be associated with a specific table version, making results reproducible and auditable.

---

## Security Architecture

### Three-Layer Security Model

**Layer 1: Fabric Workspace Roles**
Controls who can access the workspace itself. Roles: Admin, Member, Contributor, Viewer.
- Data Engineers: Contributor
- Data Analysts: Viewer
- Platform Admins: Admin

**Layer 2: Lakehouse Item Permissions**
Controls which items within a workspace are accessible. Read-all, ReadData, and Build permissions can be granted independently.
- Analysts in adjacent domains get ReadData on Gold tables only
- AI/ML users get ReadData on Silver and Gold tables
- No direct access to Bronze tables outside the owning domain team

**Layer 3: Column-Level Security via Semantic Models**
Sensitive fields (PII, financial data) are never exposed in raw form. Access to these columns flows through the semantic model layer, where Row Level Security (RLS) and Object Level Security (OLS) are enforced.

This means an AI application grounded on a semantic model inherits all data security policies automatically — a critical governance assurance for enterprise AI deployment.

---

## Compute Architecture

### Fabric Capacity and CU Management

Microsoft Fabric is billed by Capacity Units (CUs). The design principle is:

> **Right-size for peak, govern for baseline**

Fabric capacities can be paused and resumed. For non-production workloads (dev, test), capacities should be scheduled to pause during off-hours. For production workloads, capacities should run continuously with CU monitoring alerts at 80% utilization.

### Spark Cluster Configuration

For notebook and pipeline workloads, the following Spark configuration is used as a baseline:

```json
{
  "node_size": "Medium",
  "min_executors": 1,
  "max_executors": 5,
  "autoscale": true,
  "runtime_version": "1.3",
  "spark_properties": {
    "spark.sql.extensions": "io.delta.sql.DeltaSparkSessionExtension",
    "spark.sql.catalog.spark_catalog": "org.apache.spark.sql.delta.catalog.DeltaCatalog",
    "spark.databricks.delta.optimizeWrite.enabled": "true",
    "spark.databricks.delta.autoCompact.enabled": "true"
  }
}
```

V-Order (Fabric's proprietary optimization) is enabled by default on all Fabric Spark runtimes and does not require configuration.

---

## Lineage and Governance

### Native Lineage in Fabric

Microsoft Fabric tracks lineage automatically across all items in the tenant. From a single data source, you can see:

```
Source (SQL Server) → Pipeline → Bronze Table → Notebook → Silver Table 
  → Semantic Model → Power BI Report
  → ML Experiment → AI Application
```

This lineage is accessible in the Fabric Portal under **Data Lineage View** — no additional tooling required.

### Microsoft Purview Integration

For enterprise governance requirements (data cataloging, sensitivity classification, policy enforcement), the design integrates Microsoft Purview:

- **Sensitivity labels** from Purview propagate automatically to Fabric items
- **Purview Data Map** ingests Fabric lineage for org-wide catalog visibility
- **Data Use Governance** policies control which AI models can access which Purview-classified data

This integration is the governance story for executive audiences: "Every piece of data in our AI applications is classified, tracked, and governed by the same policies that cover our regulatory data estate."

---

## Design Decisions Log

| Decision | Rationale | Alternative Considered |
|---|---|---|
| Domain-aligned workspaces over project workspaces | Long-term governance and cross-domain analytics | Project-aligned: rejected due to governance sprawl |
| Delta Lake for all tables | ACID, time travel, schema enforcement | Parquet-only: rejected due to lack of ACID |
| Semantic model as AI grounding layer | Inherits all security policies automatically | Direct Gold table access: rejected for PII risk |
| Purview integration from Day 1 | Governance retrofit is 10x harder than Day 1 design | Add governance later: rejected, high retrofit risk |
| V-Order enabled by default | Power BI and ML read performance improvement at no additional cost | Disabled: no reason to disable |

---

*This architecture document is part of Jennifer Kelleman's program portfolio. It reflects real design decisions from enterprise Microsoft Fabric deployments.*
*[AIwithjen.com](https://aiwithjen.com)*
