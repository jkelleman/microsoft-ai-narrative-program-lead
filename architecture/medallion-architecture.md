# Medallion Architecture on Microsoft Fabric

The medallion pattern separates data ingestion, refinement, and business use into three layers. It gives teams a shared way to discuss quality and ownership; it does not replace source-system controls, access reviews, or use-case approval.

## Data flow

```text
Source systems
     |
     v
Bronze: ingested data with source and load metadata
     |
     v
Silver: standardized data with documented validation results
     |
     v
Gold: curated datasets designed for agreed business needs
     |
     v
Reports, analytics, and separately reviewed applications
```

In Microsoft Fabric, these layers can be implemented with Lakehouse tables, files, notebooks, pipelines, or other suitable Fabric items. The choice depends on the source, workload, governance requirements, and operating model.

## Bronze: retain what arrived

Bronze holds data close to its source form so teams can trace what was received and investigate later transformations.

Design considerations:

- Record source, ingestion time, and pipeline run or batch identifiers where available.
- Choose append, upsert, or snapshot behavior based on source semantics and retention requirements.
- Document schema changes and failed or partial loads.
- Restrict access according to the sensitivity of the source data; raw data is not inherently safe to expose.

Bronze acceptance criteria should cover successful ingestion, traceability, and an agreed response to incomplete or invalid loads.

## Silver: standardize and validate

Silver applies documented rules so data is more consistent and usable across teams.

Typical work includes:

- Normalize types, formats, and codes where business owners agree on the definitions.
- Check required fields, valid values, key integrity, and duplicates.
- Preserve relevant source lineage and record validation results.
- Quarantine or flag records that fail important rules instead of silently dropping them.
- Track exceptions, rule owners, and remediation decisions.

Quality thresholds should reflect the intended use and be approved by data owners. Validation can identify data patterns, but it does not establish that sensitive data has been properly de-identified or that a dataset is appropriate for a particular model.

## Gold: publish for a defined purpose

Gold contains curated datasets shaped around agreed business questions, reports, or applications. A Gold table should have a named owner, clear definitions, refresh expectations, and access rules.

Before publishing a dataset, document:

- Intended users and permitted purposes.
- Business definitions and transformation logic.
- Known gaps, exclusions, and freshness limits.
- Quality checks and ownership for exceptions.
- Whether additional security, privacy, or regulatory review is required.

Gold is not automatically approved for AI use. Each proposed use needs its own assessment of data relevance, permissions, privacy, safety, and operational requirements.

## Operating controls across layers

| Control | Questions to resolve |
|---|---|
| Ownership | Who owns the source, transformation rules, and published data product? |
| Access | Which roles need access at each layer, and how is access reviewed? |
| Lineage | Can a consumer trace a published value back to its source and transformations? |
| Quality | Which rules apply, who approves thresholds, and how are failures handled? |
| Retention | How long is each copy retained, and how are deletion requirements handled? |
| Change management | How are schema, logic, and semantic-definition changes tested and communicated? |
| Cost and operations | What are the refresh schedule, capacity needs, monitoring, and support model? |

These controls should be implemented using the organization's approved Fabric and data-governance capabilities. Their availability and behavior depend on tenant configuration and platform features.

## Promotion between layers

Promotion should be an explicit, observable step rather than an automatic assumption that data is ready:

1. Define the expected schema, owner, and checks for the destination layer.
2. Run transformations and record rule results, exceptions, and source lineage.
3. Stop or flag promotion when agreed critical checks fail.
4. Review exceptions with the responsible data owner.
5. Publish only after required approvals and operational checks are complete.

The notebooks in this repository provide examples of profiling and readiness assessments. Adapt their rules to the data domain, and review their outputs before using them to make delivery or production decisions.
