# CIO Briefing Template: AI Data Modernization — Phase 3 Complete

**Template Version:** 1.0  
**Author:** Jennifer Kelleman  
**Use:** Customize for each CIO engagement. Replace `[COMPANY]`, `[DATE]`, and bracketed values with specifics.

---

## Pre-Briefing Setup

**Duration:** 30 minutes (25 min briefing + 5 min Q&A / Ask)
**Format:** In-person or video; single Power BI dashboard pinned to screen
**Attendees:** CIO + 1–2 direct reports (CDO or VP Data if separate)
**Materials to bring:**
- This briefing doc (speaker notes only — not a slide deck)
- Power BI dashboard: "AI Readiness Overview — [COMPANY]"
- 1-page executive summary for distribution after the meeting

---

## The Anchor (2 minutes)

> "When we kicked off this program, you told me that [COMPANY]'s strategic priority was [STATED CIO PRIORITY — e.g., 'reducing operational costs through automation' or 'improving customer retention through better personalization'].
>
> Every decision we've made in this program has been made with that priority in mind. Today I want to show you where we are — and I think you'll see that we've built something that makes that priority achievable, not just aspirational."

**Speaker notes:**
- Make eye contact when you say the stated priority. It signals that you remembered, and that this program is in service of *their* agenda, not yours.
- Pause before "Today I want to show you." Let the Anchor land.

---

## The Situation (5 minutes)

*[Reference the Power BI dashboard — do not show slides during this section]*

> "Here's where we are. [Pull up the AI Readiness Overview dashboard.]
>
> When we started Phase 1, [X months] ago, the estate average quality score was [BASELINE SCORE, e.g., 52%]. Today it's [CURRENT SCORE, e.g., 78%]. That's the difference between data you can't trust and data you can act on.
>
> [Walk through the domain scorecard — one sentence per domain:]
>
> - Customer: [SCORE] — AI Ready. The Customer 360 Gold table has [RECORD COUNT] records and passes all five readiness criteria.
> - Finance: [SCORE] — AI Conditional. One governance gap we're closing by [DATE].
> - Operations: [SCORE] — AI Development. We know exactly what needs to happen here and it's planned.
> - [Continue for each domain]
>
> The short version: [N] of [TOTAL] domains are AI-ready today. [N] are within one quarter of readiness. [N] require significant remediation."

**Speaker notes:**
- The dashboard does the heavy lifting. Your job is to narrate it, not explain it.
- Speak to *change over time* — the journey from baseline to current is the evidence of progress.
- Don't over-explain domains that are in good shape. Spend time on the ones that need attention, because those are where the CIO's instinct will go.

---

## The Insight (8 minutes)

*Choose 2–3 insights from the list below based on what's most relevant for this engagement. Replace placeholder values with actual findings.*

### Insight Option A: The Hidden Data Risk

> "One of the most important things this program surfaced — and I say 'surfaced' deliberately, because this was already in your data estate, we just made it visible — is that [FINDING, e.g., 'your customer ID is not consistent across the CRM and the billing system'].
>
> That sounds like a data problem. It is. But it's also an AI problem: if we built a churn prediction model on top of inconsistent customer IDs, we'd be training the model on fragmented customer histories. The model would give you confident predictions based on incomplete signals.
>
> We found this in Phase 1 and we've resolved it in Phase 2. That fix is what moved the Customer domain from [BEFORE SCORE] to [AFTER SCORE]."

### Insight Option B: The Governance Unlock

> "The governance work we did in Phase 2 is what unlocks the AI investment in Phase 4. Here's why.
>
> When an AI application is grounded on data, it inherits whatever governance model governs that data. If the data has no sensitivity classification, the AI application has no way to know which outputs might contain regulated information.
>
> Every Gold table in this estate now has Purview sensitivity labels. That means when we connect an AI application to this data — whether it's a Microsoft Copilot experience or a custom model — it automatically inherits the data governance policies you've already invested in building.
>
> You don't have to solve governance for AI separately. You already solved it."

### Insight Option C: The Readiness Gap

> "I want to be honest with you about the [DOMAIN] domain, because I think the gap we found there is relevant to your [AI USE CASE] ambition.
>
> [DOMAIN] is currently scoring [SCORE] — AI Development tier. The primary driver is [ROOT CAUSE, e.g., 'inconsistent product categorization across catalog versions'].
>
> That categorization issue matters because [AI USE CASE] requires the model to understand product context. Without consistent categorization, the model can't distinguish between [EXAMPLE A] and [EXAMPLE B].
>
> We have a 6-week remediation plan. I want to walk you through it before we close, because it requires a decision from you."

---

## The Ask (3 minutes)

*Select the appropriate ask for this briefing:*

### Ask Type: Decision

> "Here's what I need from you today.
>
> We're at the gate for Phase 4 — the first production AI applications on this estate. Based on the AI readiness scorecard, the [CUSTOMER/FINANCE] domain is ready to support [SPECIFIC AI USE CASE].
>
> The decision in front of you: do we proceed to Phase 4, with the [CUSTOMER] domain as the launch domain, targeting [SPECIFIC OUTCOME] by [DATE]?
>
> I'd like your answer before we leave this room, because the Phase 4 kick-off requires [DEPENDENCY] to begin."

### Ask Type: Resource

> "To hit the Phase 3 timeline I committed to in our last briefing, I need two things from you:
>
> First, I need [RESOURCE — e.g., 'sign-off on the Fabric Premium P2 capacity upgrade']. Without it, the semantic model refresh SLAs will not be met for Phase 4.
>
> Second, I need [RESOURCE — e.g., 'the data governance council to prioritize the Operations domain access review by end of month']. We've been waiting on that review for six weeks and it's now on the critical path.
>
> Can you unblock both of these today?"

### Ask Type: Endorsement

> "I'd like to ask you to take the AI Readiness Scorecard to the board — or share it with the [EXECUTIVE/COMMITTEE] — as part of the data strategy update.
>
> Here's why: the board approved this program as a strategic initiative. They should see that the investment is producing a measurable asset — a governed, AI-ready data estate — not just completed milestones.
>
> I can have a 1-page version of the scorecard ready for you by [DATE]. Would you be willing to include it in the next board update?"

---

## Closing the Briefing

After the Ask, pause and wait for a response. Do not fill the silence.

If the response is yes, confirm it explicitly:

> "Perfect. I'll follow up with [specific action] by [specific date]. Thank you for the time today."

If the response is unclear or deferred:

> "I understand. What would it take to get to a decision by [DATE]? I want to make sure we're not creating schedule risk in Phase 4."

---

## Post-Briefing Actions

- [ ] Send 1-page executive summary within 24 hours
- [ ] Capture the confirmed Ask outcome in the program log
- [ ] Update the briefing arc: note what commitments were made for next briefing reference
- [ ] Share Power BI dashboard link if requested

---

*This template is part of Jennifer Kelleman's executive briefing portfolio.*
*[AIwithjen.com](https://aiwithjen.com)*
