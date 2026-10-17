# Rubric: how to assign 🟢 🟡 🔴 ⚪

The point of the rubric is that two separate runs over the same ticket produce the same traffic light, and that every status can be explained in one sentence with a reference to the ticket text.

## General rules

1. **You grade the description, not the ticket.** The status reflects whether the author showed the value, not whether the value actually exists.
2. **Every status comes with evidence from the text.** Quote or paraphrase the specific spot: "the description says '…' → 🟡, because the effect is named but not measured." No evidence, no traffic light.
3. **Don't fill in the blanks for the author.** If you can see where value could be, but the ticket doesn't say it, the status stays 🔴/🟡, and your guess goes into a question for the author and into the draft rewrite.
4. **Find the strongest first, then the missing.** Work out which value type the ticket makes the strongest case for. That determines what is grey and what is red.
5. **One piece of evidence, one type.** Assign each fact from the ticket to the type it fits best, and don't smear it across neighbouring types. "~60 support complaints" is Efficiency value (support load) *or* Customer value (user pain); pick one based on what the ticket is about. "Needed before initiative X launches" is criterion 6, not Future value. A second type gets a status only if there is a **separate fact** for it ("15 tickets a week" → Efficiency; "customers recalculate by hand" → Customer — these are two different facts, so two statuses are legitimate). Indirect echoes of the same fact stay ⚪. Otherwise a well-written ticket with one strong value looks "yellower" in the table than a weak one, and that punishes completeness, which must not happen.

## The four statuses

### 🟢 Green: named and backed up
All three elements are present, at least qualitatively:
- **for whom** — a specific stakeholder or segment (not "users" in general, but "teams on the Pro plan", "the support team", "developers who touch module X");
- **what the effect is** — what changes after the increment ships;
- **how we'll know** — a metric, a number, a deadline, a signal. Qualitative is enough ("tickets about this scenario stop coming in", "deploy without a manual step"); a number is optional but raises confidence.

The "hypothesis" marker: if the value is backed up but not confirmed by a real stakeholder (no data, no requests, no interviews, only the team's reasoning), the status stays 🟢, but you write "(hypothesis)" in the evidence and add the question "how will we verify this". Confirmed value is simply 🟢.

### 🟡 Yellow: mentioned, not backed up
The value type can be guessed, but at least two of the three elements are missing. Typical markers: "will improve", "will speed up", "more convenient", "important", "requested for a long time", "tech debt", "optimisation", "needed for the strategy" — without who, what exactly, and how we'll measure it.

Also 🟡 when the value follows from the epic/parent but isn't restated in the ticket itself: the link exists, but a reader of the ticket has to follow a link to find it.

### 🔴 Red: should be there, isn't
Assigned **only in two cases**:
- **Criteria 1–5:** none of the five types is shown even at 🟡 level. Then 🔴 goes to *one* criterion, the one expected for this ticket type (see the table below), and the rest get ⚪.
- **Criterion 6:** no link to strategy at all — not in the hierarchy, not in a document, not in the text.

### ⚪ Grey: not applicable
The criterion doesn't apply to this ticket and its absence is not a flaw. Grey goes to every untouched criterion as soon as at least one of 1–5 gets 🟡 or 🟢.

## What is expected by ticket type

Determine the type from the Jira field (Issue Type, labels) or from the content. The table says which criterion gets 🔴 if none is shown, and which are ⚪ by default.

| Ticket type | Expected value (candidate for 🔴) | ⚪ by default |
|---|---|---|
| Product feature, Story | Customer or Commercial (pick by content) | — (all five are possible) |
| Bug, stability | Customer (if visible to the user) or Efficiency (if it loads support/the team). **Special rule:** a reproducible defect with steps already implies user pain, so a bug with no impact description gets 🟡 on Customer, not 🔴 — the verdict is "Needs work", not "Anomaly". 🔴 on values for a bug only when it's unclear what is broken at all. | Commercial, Market |
| Tech debt, refactoring | Future | Commercial, Market, Customer |
| Platform, infrastructure, DevOps | Efficiency or Future | Commercial, Market, Customer |
| Research, spike, R&D | Future | Commercial, Market, Customer |
| Integration, localisation, new platform | Market or Commercial | — |
| Compliance, security | Future (see the compliance caveat in value-types.md) | Commercial, Market |

Criterion 6 is expected for every type, no exceptions.

## Criterion 6 in detail

| What you found | Status |
|---|---|
| The hierarchy reaches an initiative/goal **and** the ticket or epic has an impact estimate | 🟢 |
| Explicit reference to a goal/initiative/OKR/MBO/job family in the text + impact estimate | 🟢 |
| The hierarchy reaches an initiative, but there is no impact estimate anywhere | 🟡 |
| A goal/initiative/job family is mentioned in the text without explaining what will change | 🟡 |
| Semantic match with a period goal or an initiative from the digest, but the author didn't write it | 🟡 with the question "is this for goal X? — then say so" |
| Link to a quarterly goal without numbers ("Q4 goal: speed up onboarding") + an explanation of how the ticket affects it | 🟢 — the goal doesn't need numbers, a cause-and-effect link is what's needed |
| There is an epic, but it's just a grouping, not a goal | 🔴 (a folder epic doesn't count as a link) |
| Nothing | 🔴 |
| No strategy document in context and nothing in the text | 🔴 + the note "strategy check was not performed" |
| No document, but the text names the initiative and estimates the impact | 🟢 — a missing document doesn't lower the status |

**Folder epic** is an epic whose name describes a *category of work or a period*, not a *result for a stakeholder*: "Tech debt", "Bugs", "Misc", "Q4 2026", "Improvements", "Backlog", "Support", "Small stuff". The team's additional list is in `config.md`. An epic named after a result ("Onboarding 2.0", "Enterprise SSO", "Reduce Business churn") is not a folder but a candidate initiative; if it is itself linked to a goal, it's 🟢/🟡 by the rules above.

## Edge-case examples

### Product, good
> **Quick project switching in the header.** Customers on the Team plan (≈ 400 accounts) work in 4–6 projects on average and switch via the settings menu — 3 clicks. This is the 2nd most frequent support topic in Q3 (112 tickets). Expected: tickets on the topic < 20/quarter, DAU growth among multi-project teams. "Team retention" initiative, KR2.

- Customer: 🟢 — for whom (Team, multi-project), effect (3 clicks → 1), how we'll know (tickets, DAU), confirmed by support data.
- Strategy: 🟢 — initiative and KR named, impact estimated.
- The rest: ⚪.
- Verdict: ✅ OK. Under "what's good", note that the ticket is exemplary.

### Product, weak
> **Add dark theme.** Users are asking for it. Will improve UX.

- Customer: 🟡 — "asking for it" and "will improve UX" without who, how many, what will change.
- Strategy: 🔴 — no hierarchy, no mention.
- The rest: ⚪ (there is a 🟡 → no reds on 1–5).
- Verdict: 🛠 Needs work. Questions: who is asking and how often; which initiative; how we'll know it worked.

### Tech debt, weak: don't scold, but hold the bar
> **Refactor OrderService.** The code is outdated, lots of duplication, needs cleaning up.

- Future: 🟡 — value is implied (a hedge), but it isn't shown what exactly hurts and what will change.
- Efficiency: ⚪ (not claimed).
- Commercial, Market, Customer: ⚪ by default for tech debt.
- Strategy: 🔴.
- Verdict: 🛠 Needs work. Questions: what is expensive right now because of this code (time per change, incidents)? What is planned in this module under the initiatives? A draft rewrite along the lines of "any change takes N days; in Q1, initiative X needs … here".

Note: not a single red on values. Red only on strategy — that is the company requirement.

### Platform, good
> **Move the build to cacheable layers.** A full build currently takes 40 min, ~25 runs a day per team → ~15 h of machine time and waiting per day. Expected 5–7 min. Needed by the start of the "Marketplace" initiative (Q1), where the plan is 3 teams on one monorepo.

- Efficiency: 🟢 — for whom (the team), effect (40 → 5–7 min), how we'll know (build time), estimate in hours.
- Future: 🟡 — preparation for Q1 is mentioned, without an estimate of what happens without it.
- Strategy: 🟢 — initiative named, impact explained (3 teams on a monorepo).
- Verdict: ✅ OK.

### Bug
> **Formulas are lost on XLSX export.** Reproduces on all reports. Support gets ~15 tickets a week, customers recalculate by hand.

- Customer: 🟢 — "customers recalculate by hand" is user-visible pain.
- Efficiency: 🟢 — a separate fact: 15 tickets/week for support.
- (For comparison: the same bug with only reproduction steps and without these two facts is 🟡 on Customer, the rest ⚪, verdict "Needs work".)
- Strategy: 🔴 (if there is no hierarchy) or 🟡 (if the epic is an initiative). We ask for bugs too, but gently: "which initiative or job family does this get in the way of most?".

### Compliance
> **Enable the audit log as required by ISO 27001.**

- Future: 🟡 — the requirement is named, but it isn't said what we're protecting (certification → which customer/segment? risk → which one?).
- Strategy: 🔴, or 🟡 if certification is an initiative.
- Question for the author: is this a deal condition (Commercial)? A segment requirement (Market)? Protection against an incident (Future)?

### Ticket with no value at all
> **Build the settings page as in the mockup.** Link to Figma.

- Customer: 🔴 (expected for a feature, no type is shown even at 🟡).
- The rest of 1–5: ⚪.
- Strategy: 🔴.
- Verdict: ⚠️ Anomaly. One main question: "What changes for the user when this page appears, and which initiative does it belong to?"

## Self-check before output

- Is there a 🔴 on criteria 1–5 while at least one 🟡 exists? → error, replace with ⚪.
- More than one 🔴 among 1–5? → error, keep one, the one expected for the type.
- Does every non-grey status have evidence from the text? → if not, add it.
- Did a technical ticket get 🔴 on Customer/Commercial/Market? → error.
- Does the verdict match the table in SKILL.md? → check.
