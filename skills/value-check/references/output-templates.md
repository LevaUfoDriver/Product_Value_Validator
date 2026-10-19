# Output templates

Always in the person's language. Tone: coach - first what's good, then questions. No longer than one screen per ticket.

## Legend (remind in the first report of a conversation, one line)

🟢 named and justified · 🟡 mentioned without justification · 🔴 should be there but isn't · ⚪ not applicable


## Input checklist (first contact in a conversation)

Shown when the skill is invoked without a ticket, or as a single block after the first report. Checkmarks reflect what has already been found in `config.md` and `strategy/`.

```
I check tickets for value against six criteria (five value types + link to goals). For an accurate answer I need:

1. **Strategy** - a Confluence link or a file (goals, initiatives, job families). ✅ have it: strategy-digest from 2026-10-05 / ❌ none - send it and I'll put a digest in strategy/
2. **Goals for the current quarter** - optional, numbers not required, but greatly improves the alignment check. ✅ goals-2026-Q4 / ❌ none
3. **Tickets** - in any form: a Jira link or key (PROJ-123), JQL, "top 10 of project PROJ", a sprint name - or just the ticket text. Through Jira I'll pull the type, epic, links and fields myself.

Send 1–2 if you have them, plus the tickets - I'll get started.
```

If everything is already in place (both checkmarks), shorten to one line: "Strategy and Q4 goals are in place - send the tickets: links, keys, JQL or text".

## Single ticket

```
## PROJ-123 - <summary>

**What's good**
- <specific, with a reference to the text; 1–3 points. If the ticket is exemplary, say so directly: "This is a good example of describing value - it can be shown as a model".>

| Criterion | | Justification |
|---|---|---|
| Commercial | ⚪ | - |
| Efficiency | 🟢 | in the description: "…" - for whom, the effect, how we'll know |
| Market | ⚪ | - |
| Customer | 🟡 | "more convenient for users" - doesn't say for whom or how we'll measure it |
| Future | ⚪ | - |
| Strategy | 🔴 | epic "Q4" is a grouping, not a goal; no mention of initiatives |

**Verdict: 🛠 Needs work** - <one phrase, why>

**Questions for the author**
1. <on the yellow/red ones, as questions, 1–4>
2. …

**Draft "Value" section** *(for the author to refine; numbers to be filled in)*
> <2–4 sentences: for whom, what changes, how we'll know, which initiative. Where there is no data - a dash or [clarify].>

Answer any of the questions in your own words, even a single phrase - I'll propose wording for the ticket.

I can add this as a comment on the ticket in Jira - add it?   ← only if there is a Jira integration

*Disagree with a traffic light? Write, for example, "strategy should be 🟡 because …" - I'll record it for the skill owner.*
```

If there is no Jira integration or the ticket was pasted as text, one line after the table: *Hierarchy and links in Jira not checked - assessed from the text.* If there is no strategy document: *No cross-check against the strategy document was performed.*

## Group of tickets

```
## Value check: <sprint / JQL / "top 10 of the backlog"> - <N tickets>

| Ticket | Com | Eff | Mkt | Cust | Fut | Strat | Verdict |
|---|---|---|---|---|---|---|---|
| PROJ-131 Build the settings page | 🔴 | ⚪ | ⚪ | ⚪ | ⚪ | 🔴 | ⚠️ Anomaly |
| PROJ-125 Dark theme | ⚪ | ⚪ | ⚪ | 🟡 | ⚪ | 🟡 | 🛠 Needs work |
| PROJ-128 Refactor OrderService | ⚪ | ⚪ | ⚪ | ⚪ | 🟡 | 🔴 | 🛠 Needs work |
| PROJ-120 Project switching | ⚪ | ⚪ | ⚪ | 🟢 | ⚪ | 🟢 | ✅ OK |

*Hierarchy and links in Jira not checked - assessed from the text.* ← if there is no Jira integration

**Summary:** ✅ 1 · 🛠 2 · ⚠️ 1
- Most often missing: link to strategy (3 of 4) and an estimate of the effect (2 of 4).
- Good examples for the team: PROJ-120.

**Briefly per ticket**

**PROJ-131** - Customer 🔴: only a link to a mockup; what changes for the user is not stated. Strategy 🔴: no epic, no initiatives in the text. *Question:* what changes for the user after release, and which initiative does this belong to?

**PROJ-125** - Customer 🟡: "users are asking" - who, how many, how we'll know - missing. Strategy 🟡: epic "Retention" - there is a link, the impact is not assessed. *Question:* how many requests and from which segment, and how does a dark theme move retention?

**PROJ-128** - Future 🟡: "the code is outdated" - what hurts now and what will change is not shown. Strategy 🔴: epic "Tech debt" is a folder. *Question:* what needs to be done in this module for the initiatives in the coming quarter, and what do changes cost right now?

**PROJ-120** - Customer 🟢: Team accounts, 3 clicks → 1, 112 tickets in Q3, a target metric. Strategy 🟢: "Team retention", KR2. A model example.

To go through any ticket in detail, give me the number.

*Disagree with any traffic light? Name the ticket, the criterion and what it should be - I'll record it for the skill owner.*
```

After the report (both single ticket and group), if needed: a line about storage on the first run ("Where should I put the check log for the team? …"), a reminder line about sync, a "Log rows" block if there's nowhere to write.

Row order: all ⚠️ first, then all 🛠, then all ✅. Within each group - in the order the tickets arrived (backlog rank, JQL order or order in the text). The "Briefly per ticket" block follows the same order as the table; 2–4 lines per ticket, only non-grey statuses, one question; no rewording drafts.

In the summary, count by status, not by reason: "no link to strategy for 3 of 5" is one number, and the reasons (folder epic, no epic, no mention) go in one phrase after it, if that's useful to the team. The summary is a signal to the team about a pattern, not an assessment of people. Phrase it as an observation ("in this sprint, technical tickets are almost never tied to initiatives"), not as a complaint.

## Jira comment (only after an explicit "yes")

Shorter than the report, without the table (it reads poorly in Jira), with a signature.

```
Value description check (value-check)

What's good: <1–2 points>

By the five-value-types model: <one or two 🟢/🟡 with a one-line justification>. Link to strategy: <status and why>.

Questions that will help strengthen the description:
1. …
2. …

Draft "Value" section: <2–3 sentences>

- This is an assessment of how well the description shows value, not an assessment of the ticket's priority or usefulness.
```

## Wording help (after the author's reply)

```
From what you said:

> **Value.** Support currently recalculates formulas by hand in exported XLSX files for customers - [clarify: how many requests per week]. After the fix, requests on this topic will stop.

Traffic light: efficiency 🟡 → with the number of requests it becomes 🟢. Strategy is still 🔴 - which initiative or job family does this belong to?

If it fits, say "ok", or correct it in your own words.
```

Rules: only from what the person said; gaps as `[clarify: …]`; one criterion at a time; after "ok" - a full recount of the traffic light, a new verdict, a new row in the log with "Run: 2".
