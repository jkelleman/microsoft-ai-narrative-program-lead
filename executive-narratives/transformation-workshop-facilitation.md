# Transformation Workshop: Agentic AI Readiness for Enterprise Leadership

**Author:** Jennifer Kelleman
**Format:** Half-day executive workshop facilitation guide (3.5 hours)
**Purpose:** Align a leadership team on agentic AI strategy, surface organizational readiness gaps, and leave with a prioritized commitment to action
**Audience:** C-suite + VP-level leaders (6–12 participants); works for both AI-native and AI-early-stage organizations

---

## Why This Workshop Exists

Most executive AI conversations happen in briefing format: a presenter, an audience, and a one-directional flow of information. Briefings are the right tool for program updates and investment requests. They are the wrong tool for alignment.

Alignment requires the leadership team to arrive at shared conclusions through structured discussion — not to receive a presentation and nod.

This workshop is designed for the moment when:
- The organization has made an AI commitment but leadership hasn't aligned on what that means operationally
- There is disagreement (stated or unstated) about which AI use cases to prioritize
- The data engineering and technical teams have outrun executive understanding of what's now possible
- A new executive sponsor needs to be brought into an existing AI program quickly

The output is not a slide deck. It is a prioritized decision: where does this organization focus its agentic AI investment first, and who owns that commitment.

---

## Workshop Overview

| Block | Duration | Purpose |
|---|---|---|
| **0. Welcome & Framing** | 15 min | Establish norms, define terms, set the output expectation |
| **1. Current State Honest Assessment** | 45 min | Surface what's actually true about the organization's AI readiness |
| **2. The Agentic AI Opportunity Map** | 50 min | Identify and prioritize agentic AI use cases specific to this organization |
| *(Break)* | 15 min | |
| **3. Readiness Gap Analysis** | 40 min | Diagnose what's blocking the top use cases — data, talent, governance, culture |
| **4. Commitment and Next Step Design** | 35 min | Translate insight into specific, time-bounded commitments |
| **5. Closing — The 30-Day Plan** | 15 min | Each leader leaves with one action they own |

---

## Pre-Workshop Preparation

### Facilitator Preparation (1–2 weeks before)

**Gather the following inputs before the workshop:**
- Current AI Readiness Scorecard results by domain (if available; if not, use the readiness self-assessment in Block 1)
- Any existing AI use case inventory or backlog
- Data engineering team's assessment of which use cases have sufficient data foundation
- One-page briefing on what "agentic AI" means in operational terms — distribute 48 hours before the workshop, not the morning of

**Stakeholder pre-interviews (recommended for groups > 8):**
Conduct 20-minute conversations with 3–4 participants before the workshop. Ask:
1. "What does success look like for our AI program in 18 months, from your perspective?"
2. "What's the one thing that's most likely to slow us down?"
3. "Which part of your organization would benefit most from AI that can act autonomously — not just assist?"

Pre-interviews serve two purposes: they surface divergence before the room is full, and they give each participant a sense that their perspective has already been heard.

**Room setup:**
- Round table or U-shape — not theater seating
- Whiteboards or large Post-it surfaces for Blocks 2 and 3
- No laptops unless needed for reference (phones face-down)
- One printed one-pager per participant: "What Is Agentic AI?" (see appendix)

---

## Block 0: Welcome and Framing (15 minutes)

**Facilitator script:**

> "Welcome. Before we get into the substance of today, I want to be clear about what we're here to do — and what we're not.
>
> We are not here to watch a presentation about AI. We are here to make decisions together.
>
> Specifically, by the end of this session, I want us to leave with three things:
> 1. A shared understanding of where this organization actually is on AI readiness — not the optimistic version, the accurate one
> 2. A prioritized list of two or three agentic AI use cases that we agree are worth investing in
> 3. A specific commitment from each person in this room for what they will do in the next 30 days to move those use cases forward
>
> I am going to ask you to be honest in ways that may be uncomfortable. I am going to ask you to disagree with each other productively. And I am going to ask you to make decisions in this room rather than deferring them to another meeting.
>
> One ground rule: when we're in a discussion exercise, the title on your business card is irrelevant. The best idea wins, regardless of rank."

**Define agentic AI (2 minutes):**

> "I want to make sure we're all working with the same definition before we start.
>
> Agentic AI is AI that can pursue a goal autonomously — planning the steps required, executing them, and adapting when something unexpected happens, all without requiring human input at each step.
>
> It's different from the AI most of us use today, which is assistive — it helps a human do a task faster. Agentic AI *does* the task, with a human supervising the outcome rather than directing every step.
>
> The practical implication: agentic AI requires data it can trust implicitly, because there's no human in the loop to catch a mistake before it compounds. That's why the data foundation work matters for this conversation."

---

## Block 1: Current State Honest Assessment (45 minutes)

**Purpose:** Replace organizational mythology about AI readiness with an accurate, shared picture.

### Activity 1A: The Readiness Self-Assessment (20 minutes)

Distribute the readiness assessment card (one per participant). Ask everyone to complete it independently before discussing.

**Agentic AI Readiness Self-Assessment**

*Score each dimension 1–5: 1 = Not true, 3 = Partially true, 5 = Fully true*

| Dimension | Score |
|---|---|
| Our most important data is in one governed location, accessible to AI applications without manual extraction | |
| We can answer "how fresh is this data?" for any dataset AI would use, in real time | |
| We know which data contains sensitive information and have enforced controls — not just documented policies | |
| Our data engineering team has time to build new capabilities, not just maintain existing pipelines | |
| Executives receive AI-relevant insights without requiring a data engineer to pull a report | |
| We have deployed at least one AI application in production that is used by the business daily | |
| We have a clear owner for data quality in each business domain | |
| Our data engineering team understands what agentic AI requires of a data foundation | |
| We have a governance model for AI that addresses autonomy, escalation, and human override | |
| If an AI agent made an incorrect decision autonomously, we would know within 24 hours | |

*Score interpretation: 40–50 = Ready to scale agentic AI; 25–39 = Foundation in place, targeted gaps; 10–24 = Pre-conditions for agentic AI not yet met*

After individual completion, go around the room and ask for each participant's total score. Write them on the whiteboard without attribution. Look for:
- Range of scores (divergence > 15 points is significant and worth naming)
- Which dimensions have the most variation (these are the productive disagreements)
- Any dimension where everyone scored 1–2 (these are universal gaps)

**Debrief question:** "What surprised you about your own score, or about the range in the room?"

### Activity 1B: The Three Honest Statements (25 minutes)

Divide into pairs or triads. Each group completes three sentences:

1. **"The thing that is most holding us back from agentic AI that we don't talk about enough is..."**
2. **"The part of our data foundation we are most confident about is..."**
3. **"If an AI agent had access to our data today and tried to act on it autonomously, the biggest risk would be..."**

Groups report back (5 minutes per group). Facilitator captures themes on the whiteboard without judgment.

**What to listen for:**
- Repeated themes across groups = confirmed organizational gaps
- Contradictions between groups = potential misalignment to surface
- Anything about the data engineering team's capacity = critical input for use case prioritization

---

## Block 2: The Agentic AI Opportunity Map (50 minutes)

**Purpose:** Generate, pressure-test, and prioritize agentic AI use cases specific to this organization.

### Activity 2A: Use Case Generation (15 minutes)

Working individually (silent brainstorm, 8 minutes), each participant generates three agentic AI use cases for their function. Frame the prompt as:

> *"Describe a task or process in your domain where an AI agent — one that can plan, act, and adapt without requiring human input at every step — would create significant business value. Be specific about what the agent would do, what data it needs, and what the business outcome would be."*

Post all use cases on the whiteboard. Cluster similar ones. Give the full group 7 minutes to read everything silently.

### Activity 2B: Pressure-Testing (20 minutes)

Select the 6–8 use cases that generated the most interest. For each one, evaluate against four criteria using quick show-of-hands voting:

| Criterion | Question |
|---|---|
| **Data foundation** | Does the data this agent needs already exist in a governed, trustworthy state? |
| **Business value** | Is the business outcome this agent produces significant enough to justify the investment? |
| **Autonomy appropriateness** | Is it appropriate for this action to be taken autonomously, with human oversight rather than approval? |
| **Organizational readiness** | Does the team that would own this agent have the capacity and skills to run it? |

Use cases that score high on all four are "launch candidates." Use cases that score high on value but low on data foundation reveal the next data engineering priority.

### Activity 2C: Prioritization (15 minutes)

Each participant has three votes. Dot-vote on the use cases. The top two or three by vote count become the workshop's candidate priorities.

**Facilitator note:** If the top vote-getters are all from the same function, name it:
> "I notice that [Function]'s use cases are dominating the top of the list. Before we lock this in, I want to make sure we're comfortable that this represents an organizational priority, not just the loudest voice in the room. Does anyone want to advocate for something that didn't make the top tier?"

---

## Break (15 minutes)

---

## Block 3: Readiness Gap Analysis (40 minutes)

**Purpose:** For each priority use case, diagnose the specific gaps between current state and launch-ready, and assign ownership.

### Activity 3A: Gap Mapping (25 minutes)

For each of the top two or three use cases selected in Block 2, work as a full group through the gap map:

**Gap Map Template (whiteboard or large paper)**

```
Use Case: [NAME]

What the agent needs to work:
  Data: ___________________________________________
  Governance: _____________________________________
  Infrastructure: _________________________________
  Skills / talent: ________________________________

Current state of each:
  Data: [Ready / Partial / Not started]
  Governance: [Ready / Partial / Not started]
  Infrastructure: [Ready / Partial / Not started]
  Skills / talent: [Ready / Partial / Not started]

What would need to happen to close each gap:
  Data: ___________________________________________
  Governance: _____________________________________
  Infrastructure: _________________________________
  Skills / talent: ________________________________

Who owns each gap:
  Data: ___________________________________________
  Governance: _____________________________________
  Infrastructure: _________________________________
  Skills / talent: ________________________________
```

### Activity 3B: The Blocking Question (15 minutes)

For each use case, ask the group one question:

> "If we committed today to launching this agent in production by [DATE 6 months out], what is the single most likely reason we would fail to hit that date?"

Capture the answers. These are the organizational blockers that leadership needs to actively manage — not the technical problems, which the engineering team will solve.

Common blockers at this stage:
- Data engineering capacity is consumed by maintenance, leaving no room for new builds
- Governance policy for autonomous AI action has not been defined
- Executive sponsor accountability is unclear
- Business unit ownership of AI outputs is unresolved

Name each blocker explicitly and assign it a preliminary owner before moving to Block 4.

---

## Block 4: Commitment and Next Step Design (35 minutes)

**Purpose:** Translate the workshop's insights into specific, time-bounded commitments.

### Activity 4A: The Decision Log (15 minutes)

Ask the group to ratify three things explicitly:

**Decision 1: Priority use case(s)**
> "Are we in agreement that [USE CASE 1] and [USE CASE 2] are the organization's top agentic AI priorities for the next two quarters?"

Get explicit verbal agreement from each senior leader. If there's disagreement, surface it now: "I'm hearing some hesitation — can we name what's unresolved?"

**Decision 2: Data foundation investment**
> "Based on the gap mapping, [DATA DOMAIN] is the blocking dependency for [USE CASE 1]. Are we committing to prioritize that data engineering work, with [DATA ENGINEERING LEAD / CDO] as the accountable owner?"

**Decision 3: Governance model**
> "Agentic AI requires a governance model that defines when an agent can act autonomously and when it must escalate. We do not have that model today. Are we committing to develop it, with [OWNER] responsible and a target completion of [DATE]?"

### Activity 4B: The 30-Day Commitment (20 minutes)

Each person in the room — including the CEO or most senior leader present — completes a commitment card:

```
My name: ___________________________

The one thing I will do in the next 30 days to advance our agentic AI program is:

_______________________________________________

The specific, measurable outcome that will tell me I've done it is:

_______________________________________________

The date I will report back on this commitment is:

_______________________________________________
```

Cards are collected by the facilitator. A summary is distributed to all participants within 48 hours, along with a 30-day check-in calendar invitation.

**Why this matters:** Executive commitment that doesn't leave the room on paper has a half-life of about 72 hours. The commitment card creates accountability without requiring a full governance process.

---

## Block 5: Closing — The 30-Day Plan (15 minutes)

**Facilitator closing:**

> "Here's what we accomplished today.
>
> We built a shared, honest picture of where we are on agentic AI readiness — and we didn't pretend it was better than it is.
>
> We identified [N] use cases and selected the top [2–3] as our organizational priorities — not by committee, but by structured evaluation against the criteria that actually predict success.
>
> We mapped the gaps between where we are and where we need to be — and we named owners for each one.
>
> And every person in this room made a specific, time-bounded commitment that we are all holding each other to.
>
> The work of actually building these agents is going to be done by the data engineering and AI teams who weren't in this room today. Our job is to make sure they have clear direction, adequate resources, and executive air cover to move fast. What happened in this room is the foundation for all of that.
>
> I'll have a summary in your inboxes by [DATE]. The 30-day check-in is already on your calendars. The next decision we need to make together is [NEXT DECISION] — I'll schedule that for [TIMEFRAME] after we see the first 30-day progress."

---

## Post-Workshop Deliverables

**Within 48 hours:**
- [ ] Workshop summary: decisions made, commitments captured, gap map per use case
- [ ] 30-day commitment card summary distributed to all participants
- [ ] 30-day check-in calendar invitation sent

**Within 2 weeks:**
- [ ] Data engineering briefing: share workshop priorities with the technical team; get their assessment of feasibility and timeline
- [ ] Governance model kickoff: first working session with the owner committed in Block 4
- [ ] One-pager prepared for stakeholders who were not in the room

**Within 30 days:**
- [ ] First check-in meeting: each participant reports on their commitment
- [ ] Adjusted use case roadmap based on data engineering input
- [ ] Executive sponsor formally assigned to each priority use case

---

## Appendix: What Is Agentic AI? (Participant One-Pager)

**Distribute 48 hours before the workshop.**

---

### Agentic AI: What It Is and Why It Requires a Different Kind of Data Foundation

**What it is:**
Agentic AI is AI that can pursue a goal autonomously. You give it an objective — "monitor our transaction data pipelines and address quality degradation before it reaches analysts" — and it plans the steps, executes them, and adapts when something unexpected happens. Unlike assistive AI (which helps a human do a task), agentic AI *does* the task.

**What it's not:**
Agentic AI is not science fiction and it's not fully autonomous. Every agentic AI system operates within defined boundaries — actions it can take without human approval, and actions that require escalation. The boundaries are set by the organization, not by the AI.

**Where it's running today (in data engineering and operations):**
- Pipeline monitoring agents that detect data quality issues, diagnose root causes, and trigger remediation
- Data integration agents that identify new source system schemas and propose mapping updates
- Semantic model refresh agents that monitor usage patterns and optimize data freshness schedules
- Executive insight agents that respond to natural language queries about data estate health, grounded in live semantic models

**Why data foundation matters:**
An agentic AI system acts on data without a human reviewing each step. If the data is inconsistent, incomplete, or ungoverned, the agent will act on bad information — and without a human in the loop, the mistake compounds before it's caught. A governed, trustworthy data estate is not a nice-to-have for agentic AI. It's a prerequisite.

**What to bring to the workshop:**
Think about one process in your function where an AI agent — one that acts rather than assists — would change the economics of how your team operates. We'll start there.

---

*This facilitation guide is part of Jennifer Kelleman's executive engagement portfolio.*
*[AIwithjen.com](https://aiwithjen.com) | [LinkedIn: jenniferkelleman](https://www.linkedin.com/in/jenniferkelleman)*
