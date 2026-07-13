# Multi-Stakeholder Communication Plan: Agentic AI Data Engineering Program

**Author:** Jennifer Kelleman
**Purpose:** Define what each stakeholder group needs to hear, how often, in what format, and from whom — across the full program lifecycle
**Applies to:** Both the data modernization program and the agentic AI program that follows it

---

## Why a Communication Plan Is a Program Management Discipline

Executive AI programs fail in two ways. The first is technical failure — the data isn't ready, the architecture is wrong, the team can't execute. The second is narrative failure — the right people don't have the right information at the right time to keep the program funded, staffed, and prioritized.

The second failure is more common.

A multi-stakeholder communication plan is not a distribution list or a meeting calendar. It is a deliberate answer to four questions for every stakeholder group:

1. **What do they care about?** (Not what we want them to care about — what they actually care about)
2. **What do they need to know?** (The minimum information required to keep the program moving)
3. **What action do we need from them?** (Every communication should either maintain alignment or drive a decision)
4. **What format works for them?** (A CDO and a board member need different things, even if the underlying facts are the same)

This document answers all four questions for every stakeholder group this program touches.

---

## The Stakeholder Map

| Stakeholder Group | Role in Program | Communication Need | Risk if Underserved |
|---|---|---|---|
| **Board / CEO** | Strategic investor and mandate-giver | Investment thesis, competitive position, evidence of value | Program defunded or deprioritized when competing priorities emerge |
| **CIO** | Platform owner and technology risk manager | Architecture decisions, cost management, security posture | Platform choices made without program input; capacity blocked |
| **CDO / VP Data** | Data governance authority and business translator | Governance quality, team capability, cross-functional adoption | Governance gaps emerge; AI applications built on unvetted data |
| **Data Engineering Lead** | Technical program execution | Clear direction, unblocked dependencies, recognition of progress | Team burnout; scope creep from other demands; talent attrition |
| **Business Unit Leaders** | AI use case owners and demand generators | Use case roadmap, timeline to value, what they need to do | Unrealistic expectations; premature AI application requests; misalignment on priorities |
| **Data Engineering Team** | Builders of the foundation and agents | Technical context, program arc, connection between their work and business outcomes | Disengagement; "data plumbing" identity instead of strategic contributor |
| **Analysts / Data Consumers** | Downstream beneficiaries of the data estate | What's changing, when, and how to use it | Shadow data work; resistance to new semantic models; workarounds that undermine governance |

---

## Stakeholder Communication Profiles

### 1. Board / CEO

**What they care about:**
Competitive position, return on investment, organizational capability, risk management. They approved the budget — they need evidence that the investment is producing a strategic asset, not just completing a technology project.

**What they need to know:**
- Whether the program is on track to produce what was promised
- What the competitive implications are of the current pace
- What's now possible that wasn't possible before
- What decision or endorsement they need to provide

**What they do NOT need:**
Technical detail of any kind. Pipeline architecture, data quality metrics, Azure AI Foundry configuration. None of it. Their information should be 100% expressed in business outcomes.

**Format:** Executive one-pager + verbal briefing (in-person or 15-minute video). One-pager distributed before or immediately after the meeting.

**Frequency:** Quarterly, minimum. Monthly during critical phases (program launch, major milestone, significant risk).

**Owner:** Program Lead

**Key messages by phase:**

| Phase | Key Message |
|---|---|
| Data Modernization — Launch | "This investment is the prerequisite for every AI application we want to build. Without it, AI pilots will keep failing in production." |
| Data Modernization — Progress | "We now have a measurable picture of our data estate for the first time. [N] domains are AI-ready. Here's the evidence." |
| Data Modernization — Completion | "The data foundation is built. We are ready to launch AI in production on [N] domains. What's the first use case we prioritize?" |
| Agentic AI — Launch | "We are moving from AI that assists to AI that acts. The infrastructure to do this safely is already built. Here's what we're deploying first." |
| Agentic AI — In production | "Our agents have [OUTCOME]. The data engineering team is spending [X]% less time on maintenance and [Y]% more on building new capabilities." |

---

### 2. CIO

**What they care about:**
Platform risk (is this the right architectural bet?), vendor consolidation (are we reducing or increasing complexity?), total cost of ownership (are we getting value from the Fabric investment?), security posture (does agentic AI introduce new attack surface?).

**What they need to know:**
- Architecture decisions and their rationale
- Fabric capacity utilization and cost management
- Security model for agent operations (what can agents access, what can't they)
- Integration points with existing enterprise architecture
- Team capability relative to platform requirements

**Format:** Technical briefing with data (Fabric capacity metrics, workspace consolidation, cost per workload). Architecture diagrams when relevant. Not a one-pager — a structured 30-minute conversation.

**Frequency:** Monthly during active phases; bi-monthly during steady state.

**Owner:** Program Lead + Data Engineering Lead (both in the room)

**Key messages by phase:**

| Phase | Key Message |
|---|---|
| Data Modernization | "OneLake is collapsing our multi-system data stack into one governed estate. We're reducing our integration debt while building the infrastructure that makes AI possible." |
| Agentic AI — Architecture | "Agents operate within Purview-enforced boundaries. Every action is audit-logged. The automation boundary is set by the governance council, not by the agent. There is a human override window on every automated action." |
| Agentic AI — In production | "The security model for agents is the same Purview model we built in Phase 2. Agents inherit sensitivity classification policies automatically — no new security framework required." |

---

### 3. CDO / VP Data

**What they care about:**
Data trust (is the data actually good?), governance maturity (are the policies being enforced, not just documented?), team credibility (is the data organization being seen as a strategic function?), cross-functional adoption (are business units actually using the new data estate?).

**What they need to know:**
- Data quality metrics by domain — with trend lines
- Governance coverage (sensitivity labels, lineage completeness, ownership documentation)
- AI readiness status and what's blocking each domain
- Agent activity and what the agents are surfacing about data estate health
- Adoption metrics for semantic models and Power BI certified reports

**Format:** Dashboard-first (Power BI AI Readiness Overview), supported by verbal context. The CDO should be able to get the current picture from the dashboard before the meeting and use the meeting time for insight and decision.

**Frequency:** Bi-weekly during active phases; monthly during steady state. The executive insight agent should provide always-current situational awareness between formal briefings.

**Owner:** Program Lead

**Key messages by phase:**

| Phase | Key Message |
|---|---|
| Data Modernization | "We now know exactly which data is trustworthy and which isn't — with scores, not opinions. The governance model is enforced at the platform level, not documented in a spreadsheet." |
| Agentic AI — Agents operational | "The pipeline monitoring agent is surfacing data quality patterns that manual monitoring was missing. Here's what it found this month that we wouldn't have caught otherwise." |

---

### 4. Data Engineering Lead

**What they care about:**
Clear direction (where are we going and why?), unblocked dependencies (what do they need from others to execute?), technical credibility of the program architecture (is the approach sound?), team capacity (is the program asking for the right things in the right sequence?), recognition (is the team's work visible to the business?).

**What they need to know:**
- Full program arc — all phases, with technical depth
- Priority sequencing and the reasoning behind it
- How their team's work connects to the executive narrative (what are the business stakes of the technical decisions?)
- Where the program is running behind and why
- What organizational blockers need to be escalated

**Format:** Working session — not a briefing. Collaborative agenda, whiteboard, technical detail welcomed. Weekly during active phases.

**Frequency:** Weekly during active phases; bi-weekly during steady state.

**Owner:** Program Lead (peer relationship, not hierarchical)

**Key messages (ongoing):**
- "The business cares about [OUTCOME]. The technical decision that makes that outcome possible is [DECISION]. That's why it's on the critical path."
- "Here's what I'm telling the CIO / CDO about this domain. Does the technical picture I'm representing match your assessment?"
- "What's blocking the team right now that I can unblock through executive channels?"

---

### 5. Business Unit Leaders

**What they care about:**
When will AI be available in their domain? What do they need to do to get there? What business outcomes can they expect? They are consumers of the AI-ready data estate, not builders of it — and they have competing priorities that will consistently crowd out AI program work unless the value is clear and the asks are specific.

**What they need to know:**
- Their domain's AI readiness status and timeline
- What is required from them to accelerate readiness (data ownership commitments, access policy decisions, business glossary input)
- What AI applications will be possible when their domain is ready
- What the agentic AI layer means for their analysts' day-to-day experience

**Format:** Targeted one-pager + 30-minute conversation. Domain-specific — a Finance BU leader does not need to know about the Customer domain's status. Keep it relevant to their world.

**Frequency:** At each phase gate that affects their domain. Not a recurring briefing — an event-driven conversation tied to a specific milestone or decision.

**Owner:** Program Lead, supported by CDO / VP Data for relationship context

**Key messages by phase:**

| Phase | Key Message |
|---|---|
| Domain onboarding | "We're bringing your domain into the program. Here's what we need from you to make it AI-ready, and here's what you'll be able to do when we're done." |
| AI readiness gate | "Your domain is AI-ready. Here's the evidence. You can now launch [SPECIFIC AI APPLICATION] from a trusted data foundation. What do you want to build first?" |
| Agentic AI | "The monitoring agent means your analysts will stop receiving stale or incomplete data without warning. Here's what that changes for your team's workflow." |

---

### 6. Data Engineering Team

**What they care about:**
Meaningful work (are they building something that matters?), technical growth (are they learning skills that will matter in the future?), recognition (is their work visible beyond the data team?), stability (will this program continue, or will it be cancelled mid-stream?).

**What they need to know:**
- The full program narrative — not just their sprint tasks, but why the program exists and what it's building toward
- How agentic AI changes their role (emphasis: it amplifies their capabilities, it doesn't replace them)
- What the executive briefings are saying about their work (show them the one-pagers; give them visibility into the business reaction to what they're building)
- Skill development opportunities — especially Azure AI Foundry agent development, multi-agent orchestration, and Fabric Copilot patterns

**Format:** Team all-hands (monthly, program narrative focus) + sprint ceremonies (technical, continuous). The monthly all-hands should include a 10-minute "business context" segment that connects the sprint's technical work to the executive narrative.

**Frequency:** Sprint ceremonies continuous; team all-hands monthly; individual career conversations quarterly.

**Owner:** Data Engineering Lead (primary); Program Lead contributes to monthly all-hands business context segment

**Key message (constant):**
> "The work you are doing is not pipeline plumbing. It is the infrastructure for every AI application this organization will build. The agentic AI layer you're designing is the capability that will define what 'data engineering' means at this company for the next five years. The executives who fund this program know your team's work is what makes it possible."

---

### 7. Analysts / Data Consumers

**What they care about:**
Will this change how I work? Will my reports break? Will the data I rely on be different? Can I trust the new models?

**What they need to know:**
- What is changing in their tools and data (specific models, reports, refresh schedules)
- When changes are happening and how to prepare
- Where to get help if something doesn't work as expected
- Why these changes are happening (context reduces resistance)

**Format:** Email announcement + short reference guide for each change. Not a program briefing — a practical "here's what's different and here's what you do" communication.

**Frequency:** At each milestone that affects their tools. Proactively, before the change — not reactively after analysts notice something is different.

**Owner:** CDO / VP Data team, with content provided by Data Engineering team

---

## The Communication Cascade

When a major program milestone occurs, communications flow in a specific sequence:

```
[Milestone achieved — e.g., Customer domain reaches AI-ready status]
          │
          ▼
1. Data Engineering Lead briefed (confirm technical facts, surface any caveats)
          │
          ▼
2. CDO / VP Data briefed (data quality and governance framing)
          │
          ▼
3. Relevant Business Unit Leader briefed (domain-specific impact, ask)
          │
          ▼
4. CIO briefed if architecture or platform implications exist
          │
          ▼
5. CEO / Board one-pager distributed (business outcome framing only)
          │
          ▼
6. Analyst / data consumer change communication (if tools are affected)
          │
          ▼
7. Data Engineering team recognition (share the business reaction to their work)
```

**Why sequence matters:**
Communications that arrive out of order create confusion. If a Business Unit Leader hears about their domain's AI readiness before the CDO does, the CDO loses credibility with their own stakeholder. If the CEO receives a one-pager before the CIO has been briefed, the CIO is in a conversation they're unprepared for.

The cascade takes 48–72 hours for a standard milestone. For major program decisions, allow a full week.

---

## Communication Anti-Patterns

These are the communication failures that consistently undermine enterprise AI programs:

| Anti-Pattern | How It Manifests | Fix |
|---|---|---|
| **The simultaneous blast** | The same email goes to board, CIO, analysts, and engineers at the same time | Use the cascade; each group needs a different message |
| **The technical leak** | A business leader hears about an architectural problem from a team member before from the program lead | Brief the program lead chain first; ensure technical issues are framed with context before they surface informally |
| **The radio silence** | No communication between major milestones — executives lose track of the program | Monthly one-pager to key stakeholders even when there's no milestone; the absence of news is itself a message |
| **The good news only** | Communications only surface successes; risks and problems are hidden | Trust is built by being honest about problems before they become crises; the briefing framework applies to bad news too |
| **The format mismatch** | Sending a 12-page technical report to a board member | Format to the audience; never send more detail than the stakeholder needs |
| **The missing ask** | Communications that end with "FYI" rather than a specific request | Every stakeholder communication should either maintain alignment (no ask needed) or drive a decision (specific ask required) |

---

## Communication Calendar Template

*Adapt to actual program timeline. This template assumes a 12-month program with monthly cycles.*

| Week | Communication | Audience | Owner |
|---|---|---|---|
| Week 1 of each month | AI Readiness dashboard refresh | CDO, VP Data (via Executive Insight Agent) | Automated |
| Week 2 of each month | Data Engineering Lead working session | Data Engineering Lead | Program Lead |
| Week 2 of each month | Data Engineering team all-hands (monthly) | Data Engineering team | Data Eng Lead + Program Lead |
| Week 3 of each month | CDO / VP Data briefing | CDO / VP Data | Program Lead |
| Week 4 of each month | CIO briefing (active phases) | CIO | Program Lead + Data Eng Lead |
| Phase gate | Business Unit Leader briefing (affected domain) | BU Leader | Program Lead + CDO |
| Quarterly | CEO / Board one-pager + briefing | CEO / Board | Program Lead |
| Quarterly | Analyst / data consumer change communication | Analysts | CDO team |
| At each agentic AI milestone | Agent deployment announcement | Data Engineering team (recognition) | Program Lead |

---

*This communication plan is part of Jennifer Kelleman's program leadership portfolio. It reflects principles applied across enterprise AI and data modernization programs — where the technical work and the human communication work are treated as equally essential to program success.*

*[AIwithjen.com](https://aiwithjen.com) | [LinkedIn: jenniferkelleman](https://www.linkedin.com/in/jenniferkelleman)*
