# CIO Briefing: Data Modernization and AI Readiness

**Audience:** CIO and relevant technology, data, and business leaders
**Duration:** 45 minutes
**Purpose:** Review the current state, agree on priorities, and make a clear decision about next steps.

Replace bracketed prompts with current, verified information. If a measure is not available, say so and identify how it will be established rather than estimating a result.

## Before the meeting

- Confirm the business priority this work is intended to support.
- Agree on the data domains and systems in scope.
- Prepare a short baseline with sources, dates, and known limitations.
- Identify the decision or support needed from leadership.
- Bring a follow-up plan with owners and dates.

## Briefing agenda

### 1. Why this matters now — 10 minutes

Describe the business need in terms the organization already uses: [priority, customer need, operating challenge, or risk].

Summarize what is known about the current data estate:

- Priority systems and domains: [list]
- Known issues with quality, access, ownership, or duplication: [evidence]
- Business effect of those issues: [verified example or impact]

Keep the distinction clear between confirmed findings and assumptions that still need investigation.

### 2. The proposed foundation — 15 minutes

Explain how the proposed Microsoft Fabric and OneLake design fits the organization's needs. Cover:

- Which data sources and workloads are in scope.
- How access, sensitivity, lineage, and retention will be handled.
- Where data is copied, referenced, transformed, and stored.
- What the design does not solve on its own, including data ownership and source quality.

Use the Fabric lakehouse design document for architecture details. Avoid presenting a shared storage platform as a replacement for workload-specific governance or review.

### 3. Delivery plan and evidence — 15 minutes

Walk through the proposed Bronze, Silver, and Gold stages:

- **Bronze:** retain ingested source data with useful lineage and audit information.
- **Silver:** standardize and validate data against documented rules.
- **Gold:** publish domain-oriented datasets for agreed reporting or application needs.

For each stage, identify the owner, acceptance criteria, dependencies, and evidence that will be reported. The readiness scorecard can help surface gaps; it is not, by itself, an approval for model use or production release.

### 4. Decision and next steps — 5 minutes

State the request plainly:

> **Decision requested:** [specific decision]
> **Recommended option:** [option and rationale]
> **Needed by:** [date]
> **If deferred:** [impact on scope, cost, or schedule]

Close by confirming the decision, owner, and next checkpoint. If more information is needed, agree on what evidence is missing and when it will be available.

## Common questions

| Question | Suggested response |
|---|---|
| Why not connect an AI service directly to the current systems? | That may be appropriate for a limited use case, but first assess data quality, access controls, sensitivity, and retrieval needs. A direct connection does not resolve gaps in those areas. |
| Does Fabric mean we can stop maintaining existing platforms? | Not necessarily. The design should identify which workloads can move, which remain, and how transition costs and dependencies will be managed. |
| How will we know whether the program is working? | Set a baseline and track agreed measures such as quality-rule results, time to prepare data, domain coverage, access-review completion, and delivery milestones. Report actual results with their sources and limitations. |
| Does a high readiness score mean a dataset can be used with AI? | No. The score is a screening aid. Use-case owners, data owners, security, privacy, and legal reviewers still need to assess the intended use and applicable controls. |

## Follow-up record

- Decision and date: [record]
- Open questions and evidence needed: [record]
- Action, owner, and due date: [record]
- Next review: [date]
