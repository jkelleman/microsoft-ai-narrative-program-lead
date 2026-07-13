# Program Charter: Agentic AI Data Engineering

**Program Name:** Agentic AI Data Engineering Program
**Platform:** Microsoft Fabric + Azure AI Foundry
**Charter Version:** 1.0
**Author:** Jennifer Kelleman
**Prerequisite:** Enterprise AI Data Modernization Program — or equivalent governed data estate on a unified lakehouse platform

---

## Executive Summary

This program represents the next chapter of enterprise AI: moving from a governed, AI-ready data estate to a production agentic AI capability embedded in the data engineering workflow itself.

The preceding data modernization program answered the foundational question: *Is our data trustworthy enough to act on?* This program answers the next one: *What happens when AI acts on it — autonomously, at scale, in production?*

Agentic AI in data engineering is not a futuristic concept. It is a current production capability at organizations that have invested in the data foundation that makes it safe. This program designs, deploys, and operationalizes that capability — with the same combination of technical rigor and executive narrative discipline that made the data modernization program succeed.

The business case is concrete: organizations that automate data pipeline intelligence free data engineering capacity for higher-value work, reduce the incident surface that reaches analysts and AI applications, and build a compounding capability that improves with every new data domain added to the estate.

---

## Strategic Context

### What Changed With the Data Modernization Program

The completed data modernization program delivered three capabilities that are prerequisites for agentic AI:

**1. A unified, governed data estate on OneLake**
Every priority data domain exists in a single storage layer with one security model and one lineage graph. Agentic AI can operate across the estate without cross-system integration complexity.

**2. Quality baselines and measurement infrastructure**
The data quality assessment notebooks and AI readiness scorecard produce objective, real-time measurements of data estate health. Agents need this measurement infrastructure to understand what "normal" looks like and to detect when something has changed.

**3. Enforced governance**
Microsoft Purview sensitivity labels enforced at the platform level mean agents can query and act on the estate within defined access boundaries — without requiring a human to review every data access decision.

None of this existed before the data modernization program. The agentic AI layer is only safe to deploy because the foundation is in place.

### What Agentic AI Changes in Data Engineering

Traditional data engineering workflow:

> Source system → Pipeline → Bronze → Silver → Gold → Analyst / AI application
> *(Human monitors each stage; human investigates anomalies; human decides when to escalate; human approves remediation)*

Agentic data engineering workflow:

> Source system → Pipeline → Bronze → Silver → Gold → Analyst / AI application
> *(Agent monitors each stage continuously; agent detects anomalies before they propagate; agent diagnoses and — within defined boundaries — self-heals; human receives escalations with diagnosis already prepared)*

The human role shifts from monitor-and-responder to boundary-setter and escalation handler. This is not a reduction in the importance of the data engineering team — it is a shift in what they spend their expertise on. Less pipeline maintenance, more pipeline architecture. Less incident response, more capability building.

### The Compounding Effect

Each domain brought into the agent's operating environment increases the agent's diagnostic capability. An agent that has monitored the Customer domain for six months has pattern knowledge — what normal looks like, what change signatures precede incidents, which source system behaviors predict downstream quality issues — that cannot be replicated by a new team member reviewing dashboards.

This compounding knowledge is a durable organizational asset. It doesn't leave when an engineer leaves.

---

## Program Objectives

### Primary Objective

Deploy production agentic AI agents across the data engineering workflow — monitoring, diagnosing, and where appropriate autonomously remediating data quality and pipeline integrity issues — with measurable reduction in incident impact and engineering maintenance overhead.

### Secondary Objectives

1. **Establish a multi-agent orchestration architecture** on Microsoft Fabric + Azure AI Foundry that supports the addition of new agents and new domains without architectural rework
2. **Deploy an executive insight agent** that enables CDO, VP Data, and program leads to query data estate health in natural language, grounded in live semantic models
3. **Develop a responsible agentic AI governance model** that defines automation boundaries, escalation policies, audit logging standards, and human override mechanisms
4. **Build data engineering agentic AI skills** — creating a team capable of designing, deploying, and operating AI agents as a core competency
5. **Demonstrate repeatability** — document agent deployment patterns so each new agent is faster to build than the last

---

## Agent Catalog: Program Scope

### Agent 1: Pipeline Monitoring Agent
**What it does:** Continuously monitors Bronze and Silver layer data quality metrics. Detects completeness degradation, freshness violations, conformance failures, and schema drift. Diagnoses root causes using historical pattern matching and source system change logs.

**Automation boundary:** Within the approved boundary, triggers pre-approved remediation workflows (pipeline re-runs, schema mapping updates, null handling logic). Outside the boundary, escalates with a complete diagnostic report.

**Data it needs:** Bronze and Silver Delta tables; pipeline run logs; source system change notification feeds; historical quality metric time series

**Business outcome:** Reduction in quality incidents reaching the analyst and AI application layer; reduction in on-call burden for data engineering team

**Microsoft Fabric components:** Fabric notebooks (Spark + Python), Fabric Eventstream for real-time monitoring, Azure AI Foundry agent framework, Fabric Data Activator for alert and action triggers

---

### Agent 2: Data Integration Agent
**What it does:** Monitors source system schemas for changes (new columns, renamed fields, changed data types, deprecated tables). When a schema change is detected, proposes updated pipeline mapping logic and — for low-risk changes within the automation boundary — deploys the update automatically. For high-risk changes, prepares a complete impact assessment.

**Automation boundary:** Additive schema changes (new nullable columns) within the boundary. Breaking changes (column renames, type changes, table deprecation) always escalate.

**Data it needs:** Source system schema registry; current Data Factory pipeline configurations; column lineage graph in Purview; historical schema change log

**Business outcome:** Elimination of silent schema-break incidents where pipelines continue running but produce incorrect output; reduction in time-to-response for schema changes from days to hours

**Microsoft Fabric components:** Data Factory pipeline metadata API; Microsoft Purview schema scanning; Azure AI Foundry agent for impact analysis; Fabric notebooks for mapping update generation

---

### Agent 3: Semantic Model Freshness Agent
**What it does:** Monitors Power BI semantic model usage patterns and refresh SLA compliance. Detects when models are running stale relative to their business use (e.g., a model used heavily at 8am is refreshing at 9am). Proposes and — within the boundary — adjusts refresh schedules. Alerts when refresh failures have business impact.

**Automation boundary:** Refresh schedule adjustments within pre-approved windows. Refresh failures in business-critical models always escalate with impact assessment.

**Data it needs:** Power BI semantic model refresh logs; model usage telemetry; business domain priority register; analyst working hours patterns

**Business outcome:** Elimination of analysts starting their day with stale models; reduction in manual refresh schedule management overhead

**Microsoft Fabric components:** Fabric REST APIs for semantic model management; Power BI activity log; Azure AI Foundry agent for schedule optimization; Fabric notebooks for usage pattern analysis

---

### Agent 4: Executive Insight Agent
**What it does:** Responds to natural language queries from program leads, CDO, and VP Data about data estate health, AI readiness by domain, pipeline performance trends, and agent activity. Grounded in live Gold layer semantic models and agent activity logs. Does not take action — retrieves, synthesizes, and surfaces.

**Scope of queries it handles:**
- "Which domains are closest to AI readiness and what's blocking them?"
- "How many pipeline incidents did the monitoring agent catch this week that would have reached analysts?"
- "What's changed in the Finance domain quality score in the last 30 days and why?"
- "Which semantic models are most at risk of freshness violations this week?"

**Data it needs:** AI readiness scorecard (live); domain quality metric time series; agent activity logs; pipeline run history; Power BI usage telemetry

**Business outcome:** Program leads spend time on decisions, not on pulling reports. Executive briefing prep time reduced. CDO and VP Data have always-current data estate situational awareness.

**Microsoft Fabric components:** Azure AI Foundry agent with RAG architecture; Gold layer semantic models as the knowledge base; Fabric Copilot integration for the chat interface

---

### Agent 5: AI Readiness Monitoring Agent *(Phase 2)*
**What it does:** Continuously monitors AI readiness scores across all data domains. Detects when a domain crosses the readiness threshold (triggering an unlock notification) or drops below it (triggering a regression alert). Surfaces the specific factors driving each change and maps them to active AI applications that depend on the domain.

**Data it needs:** AI readiness scorecard time series; Gold table quality metrics; AI application dependency registry

**Business outcome:** AI application owners receive proactive notification of data readiness changes before those changes affect application performance; data engineering team receives early warning when a domain is drifting toward a quality problem

---

## Architecture Overview

```
[Source Systems]
      │
      ▼
[Data Factory Pipelines] ◄──── Schema change detected by Data Integration Agent
      │
      ▼
[Bronze Layer — OneLake]
      │                    ◄──── Pipeline Monitoring Agent (continuous quality scan)
      ▼
[Silver Layer — OneLake]
      │                    ◄──── Pipeline Monitoring Agent (conformance + freshness)
      ▼
[Gold Layer — OneLake]
      │
      ├──► [Power BI Semantic Models] ◄── Semantic Model Freshness Agent
      │
      ├──► [AI Applications] ◄── AI Readiness Monitoring Agent
      │
      └──► [Executive Insight Agent] ◄── Natural language queries from leadership


[Azure AI Foundry]
      │
      ├──► Agent orchestration layer (all agents above)
      ├──► Multi-agent coordination framework
      └──► Audit logging and human override interface


[Microsoft Purview]
      │
      └──► Governance policy enforcement (agents operate within Purview-defined boundaries)
```

---

## Program Phases

### Phase 1 — Agent Infrastructure (Weeks 1–6)
**Goal:** Stand up the agentic AI infrastructure and deploy the first production agent.

Key deliverables:
- Azure AI Foundry workspace provisioned and integrated with Fabric tenant
- Multi-agent orchestration framework deployed (one-agent baseline)
- Governance model v1: automation boundaries, escalation policy, audit log schema, human override interface
- **Pipeline Monitoring Agent** deployed to production for Customer and Finance domains
- Data engineering team agentic AI skills baseline assessment and training plan

---

### Phase 2 — Agent Expansion (Weeks 7–14)
**Goal:** Extend the monitoring agent coverage and deploy the integration and insight agents.

Key deliverables:
- Pipeline Monitoring Agent expanded to all AI-ready domains
- **Data Integration Agent** deployed — schema monitoring for top 5 source systems
- **Executive Insight Agent** deployed — CDO and VP Data onboarded
- Governance model v2: lessons from Phase 1 automation boundary decisions incorporated
- Executive briefing: "Agents in production — what they've taught us about our data estate"

---

### Phase 3 — Semantic Layer and AI Readiness Monitoring (Weeks 15–22)
**Goal:** Close the loop between agentic monitoring and business-facing data consumption.

Key deliverables:
- **Semantic Model Freshness Agent** deployed
- **AI Readiness Monitoring Agent** deployed — all AI-ready domains in scope
- Agent knowledge base expanded with 6 months of operational pattern data
- Agent deployment playbook documented — standard architecture and deployment checklist for new agents
- Executive briefing: "The compounding advantage — what 6 months of agentic operations has produced"

---

## Success Metrics

| Metric | Baseline | Target | Measurement Method |
|---|---|---|---|
| Pipeline quality incidents reaching analysts | [CURRENT #/month] | ≥ 50% reduction | Incident log comparison |
| Time to detect quality degradation | [CURRENT hours] | < 30 minutes | Agent alert timestamps |
| Data engineering time on pipeline maintenance | [CURRENT %] | ≥ 30% reduction | Team time tracking |
| Schema change incidents (silent breaks) | [CURRENT #/quarter] | 0 in scope systems | Data Integration Agent log |
| Executive insight queries fulfilled without analyst involvement | 0 | ≥ 15/week | Insight Agent usage log |
| Semantic model freshness SLA compliance | [CURRENT %] | ≥ 99% | Power BI refresh log |
| Agent automation boundary compliance | N/A | 100% (no unauthorized actions) | Audit log |

---

## Governance Model: Responsible Agentic AI

Agentic AI in production requires a governance model that is more specific than general AI policy. This section defines the operating principles.

### The Automation Boundary

Every agent in this program operates within a defined automation boundary. Actions inside the boundary are executed without human approval. Actions outside the boundary are escalated with a complete diagnostic report.

**Boundary definition process:**
1. Data engineering lead and governance council jointly define the boundary for each agent before deployment
2. Boundary is documented in the agent's configuration and logged in the governance registry
3. Boundary reviews occur quarterly or after any escalation event that reveals a gap

**Current boundary examples:**
- Pipeline re-run for a freshness violation: **inside boundary** (low risk, reversible, self-contained)
- Schema mapping update for a new nullable column: **inside boundary** (additive, documented, reversible)
- Schema mapping update for a renamed column: **outside boundary** (breaking change, requires human review)
- Any action affecting a Gold table certified for AI application use: **outside boundary** (downstream AI impact)
- Any action affecting data with PII sensitivity classification: **outside boundary** (governance escalation required)

### Audit Logging

Every agent action — including automated actions within the boundary — is logged with:
- Timestamp
- Agent identity
- Action taken
- Data affected (table, domain, sensitivity classification)
- Confidence score of the diagnosis
- Human override option and expiry

Audit logs are retained for 24 months and available to the governance council, data engineering lead, and CDO on demand.

### Human Override

Every automated action has a defined override window — a period during which a data engineering team member can cancel or reverse the action before it is finalized. Override notifications are sent in real time to the on-call engineer.

---

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Agent acts on stale diagnostic data and makes a wrong remediation decision | Medium | High | Real-time quality checks before every automated action; override window on all automations |
| Automation boundary is set too conservatively — agents escalate everything and add no value | Medium | Medium | Boundary calibration review at 4 weeks; escalation rate is a key Phase 1 metric |
| Automation boundary is set too aggressively — agents take actions they shouldn't | Low | High | Governance council review of all boundary settings before deployment; audit log monitoring |
| Data engineering team resists agent oversight of their pipelines | Medium | Medium | Team involvement in boundary setting; agents framed as capacity amplifiers, not monitors |
| Azure AI Foundry / Fabric integration performance limitations | Low | Medium | Performance testing in staging before production deployment; SLA agreements with Fabric capacity |
| Agent knowledge base becomes stale as the data estate evolves | Medium | Medium | Scheduled knowledge base refresh; AI readiness monitoring agent flags changes |

---

## About This Charter

This charter reflects the logical next step for organizations that have completed a data modernization program on Microsoft Fabric and are ready to deploy agentic AI on the foundation they've built. The agent catalog, architecture, and governance model represent a practical, production-ready approach — not a theoretical framework.

The most important principle underlying this program: **agentic AI is only as trustworthy as the data it operates on.** That's not a constraint — it's the reason the data modernization program was the right first investment.

*Jennifer Kelleman | [AIwithjen.com](https://aiwithjen.com) | [LinkedIn: jenniferkelleman](https://www.linkedin.com/in/jenniferkelleman)*
