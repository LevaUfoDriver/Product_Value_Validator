# Feedback, log and calibration

The skill answers two different "does it work" questions, and collects data for both:

1. **Accuracy** — do people agree with the traffic light. Measured against the golden set (`calibration/golden-set.md`), command `/value-check calibrate`.
2. **Effect** — does the team's behavior change. Measured as the share of tickets rated "✅ OK" on the first run, by week/sprint, from the log (`log/value-check-log.md`), command `/value-check stats`.

The skill **never changes the rubric on its own**. It only records disagreements and counts discrepancies; edits to `references/rubric.md` are made by a human after reviewing what has accumulated.

---

## 1. Run log

After every check (single ticket or group), append one row per ticket to `log/value-check-log.md` — a markdown table, one row = one run of one ticket:

```
| Date | Who | Ticket | Type | Com | Eff | Mkt | Cust | Fut | Strat | Verdict | Source | Run | Synced |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 2026-10-05 | ivan | APP-402 | Story | ⚪ | ⚪ | ⚪ | 🟢 | ⚪ | 🟢 | ✅ | jira | 1 | — |
```

- **Who** — the name or login of whoever ran it (ask once per conversation if you don't know; if they don't want to say — "—").
- **Type** — Issue Type from Jira or your own classification (Story / Bug / Tech / Platform / Spike / Compliance).
- **Source** — `jira` (via the integration) or `text` (pasted).
- **Run** — which run of this ticket this is (1 — the first). The share of ✅ at Run=1 is the main effect metric: it shows whether people have started writing tickets with value *right away*.
- **Synced** — "—" until the row has been sent to storage; after `/value-check sync` — the date it was sent.

If the file doesn't exist, create it with the table header. If there's nowhere to write the file (no file system access), print the log rows at the end of the report in a collapsed "Log rows" block and ask the person to save them; don't lose data silently.

## 2. Disagreement — one-line feedback

At the end of every report, one line:

> Disagree with a traffic light or verdict? Write, for example: "PLT-88 strategy should be 🟡 — our epic 'Tech debt Q4' is tied to MBO-3". I'll record it; the skill owner will fix the rubric.

When the person objects:
1. Clarify, if unclear, **which criterion** and **what the status should be**. Don't argue or try to persuade — you may explain in one phrase why you rated it that way (with a reference to the rubric rule), but the record is made regardless.
2. Append to `log/disagreements.md`:

```
| Date | Who | Ticket | Criterion | Skill | Human | Reason (human's words) | Rubric rule applied | Status |
|---|---|---|---|---|---|---|---|---|
| 2026-10-05 | ivan | PLT-88 | Strat | 🔴 | 🟡 | epic "Tech debt Q4" is tied to MBO-3 | "a folder epic does not count as a link" | open |
```

3. If the disagreement points to **a fact you didn't know** (as in the example — the epic really is tied to a goal), that's not a rubric error but a lack of context. Suggest: "If your tech-debt epics are tied to MBOs, add that to `config.md` → hierarchy, and I'll take it into account". Still make the record in disagreements — the owner will see that context was missing.
4. If the same rule is challenged twice in one conversation, say so directly: "This is the second disagreement with rule X today; the skill owner should take a look at it".

Status "open" → "accepted" (rubric changed) / "rejected" (with a reason) / "context" (fixed in config) is set by the owner during review.

## 3. Storage — set up once

The log and disagreements accumulate locally and are sent to shared storage every so often with the `/value-check sync` command. Where the storage is lives in `config.md` → "Log storage". If the field is empty, **on the first run in a conversation** ask once, after the report:

> Where should I put the check log for the team? Give me a link to a page/file where I can append markdown: a Confluence page, an Obsidian note (path to the .md in the vault), a file in a repository, a Notion page — whatever your team uses. You can say "nowhere for now" — then the log stays local and I won't ask again in this conversation.

Record the answer in `config.md`. Record "nowhere for now" as well (`local`) so as not to ask again.

### How to write to different storages

General principle: storage is **any place where you can append markdown**. Determine the type from the link and pick the method:

| Storage | How to recognize | How to write |
|---|---|---|
| Confluence | `*.atlassian.net/wiki/…` | Confluence integration (MCP/connector): read the page, add rows to the table (or create a child page "value-check log YYYY-MM" if the page has grown > 200 rows), save |
| Obsidian / local markdown | path to an `.md` or a folder | File on disk: via the agent's file access. Append rows to the table at the end of the file. Don't touch the frontmatter or the text above the table |
| Git repository | path inside the repo or a GitHub URL | Append to the file, propose a commit with the message `value-check: sync YYYY-MM-DD` |
| Notion | `notion.so/…` | Notion integration, if available: add rows to the database/table |
| Jira issue | ticket key | A comment with a table of the new rows |
| Something else | — | Ask how to write there; if there's no way, print the markdown for the person to paste themselves |

If there's no integration or access, don't fail: print the new rows in the chat as a block and say where to paste them. Mark them in the local log as "Synced: manually YYYY-MM-DD".

### `/value-check sync`

1. Collect the rows from `log/value-check-log.md` and `log/disagreements.md` with "Synced: —".
2. Append them to storage by the rules above. Disagreements go to a separate table/section "Disagreements".
3. Set the sync date in the local files.
4. Report in one line: "Sent N log rows and M disagreements to <storage>".

Remind about sync yourself at the frequency from `config.md` (default — once a day): if there are unsent rows and the last sync is older than that period, add one line at the end of the report: "N rows in the log have not been sent to storage — send them?". Take the last send date from the "Synced" column (last non-empty value). "Yes" — send and don't ask again until the end of the conversation; "no" — also don't ask again until the end of the conversation.

For a team that wants no reminders at all: the log can be sent automatically on a schedule — a daily task that runs `/value-check sync`. Set it up with your agent's tooling (scheduled task, cron, CI). The skill does not create the schedule itself.

---

## 4. Golden set and calibration

The golden set is 15–30 real tickets, rated **independently by 2–3 people** (for example, CPO, CTO, architect) against the same six criteria. File: `calibration/golden-set.md`; the format is in the template there.

Why independently: discrepancies between people show where **the rubric itself is vague** — that needs fixing in the rubric, not in the skill. Discrepancies between the skill and the human consensus show where **the skill is wrong**.

### Who may change what

| File | Who writes | How |
|---|---|---|
| `calibration/ratings/<name>.md` | each rater — only their own | `/value-check rate` or by hand |
| `calibration/golden-set.md` | only the owner (the "Skill owner" field in `config.md`) | `/value-check assemble` or by hand |
| `references/rubric.md` | only the owner | by hand, based on calibrate results and the disagreement review |
| `calibration/runs/` | the skill | `/value-check calibrate` |

The skill never writes to `golden-set.md` on its own and does not run `assemble` for anyone who hasn't identified themselves as the owner. This is not protection against a malicious actor (the files are accessible to anyone who has the skill), but protection against accidental edits: if the ratings need to change, go through the owner, with a note on why.

### `/value-check rate` — rater mode

The goal is for the rater to be comfortable while the ratings stay independent.

1. Ask the rater's name (once per conversation), open or create `calibration/ratings/<name>.md` with a table in the same format as in golden-set.
2. The person pastes a ticket (text or key — via the integration pull the text, but **not the hierarchy and not the epic links**: the rater should see the same thing the skill will see during calibration — the text plus the epic name).
3. **Don't rate the ticket yourself and don't hint at anything about its value.** Even if asked "what do you think?" — reply that you'll show it after the set is assembled, otherwise the calibration is meaningless.
4. Go through the six criteria one at a time. For each — one reminder line from the rubric (the key question and what distinguishes 🟢 from 🟡) and four options. Then the verdict and an optional comment "why, if it's not obvious".
5. Record the row. If the ticket is already in this rater's file, ask whether to overwrite.
6. Offer the next ticket. At the end, say how many tickets this rater has rated and how many are expected in the set in total (from `config.md`).

If the rater prefers working in the file, that's fine too: the format is the same, the skill will assemble it later.

### `/value-check assemble` — the owner assembles the set

1. Ask the name, check it against "Skill owner" in `config.md`. If it doesn't match, refuse: "Only <owner> can assemble the golden set. Your ratings are saved in `ratings/<name>.md`".
2. Read all `ratings/*.md`. Show a summary: how many tickets, how many have ≥ 2 raters, which tickets have only one (don't include those in the set — ask whether to wait).
3. Assemble `golden-set.md`: the ticket text once, with all raters' rows under it. Overwrite the existing set after confirmation; save the previous version as `golden-set.<date>.md`.
4. Offer to run `calibrate` right away.

### `/value-check calibrate`

1. Read `calibration/golden-set.md`. If there are fewer than two raters or fewer than 10 tickets, say the set is small, and count anyway.
2. For each ticket, compute the **human consensus** per criterion: the status the majority gave; on a tie (2 raters, different statuses) — "disputed".
3. Run each ticket through the rubric **as a normal run** — without peeking at the human ratings (rate from the ticket text, then compare).
4. Count and print:

```
## value-check calibration — <date>, <N tickets>, <K raters>

**Agreement between people** (where the rubric is vague)
| Criterion | Full agreement | Disputed | Example of a disputed one |
|---|---|---|---|
| Com | 90% | 10% | APP-417 — 🟡 vs ⚪: whether "customers have asked" counts as a hint at commercial |
| … |

**Skill vs human consensus** (where the skill is wrong)
| Criterion | Exact | Off by one step (🟢↔🟡, 🟡↔🔴) | Miss (🟢↔🔴, status↔⚪) |
|---|---|---|---|
| Strat | 70% | 25% | 5% |
| … |
| Verdict | 80% | — | 20% |

**Systematic biases** — if a criterion has ≥ 3 discrepancies in the same direction:
- Strategy: the skill is stricter than people (4 times 🔴 where people gave 🟡). All four are epics of the form "Tech debt Qn". People consider them linked. → Either add to config.md, or soften the "folder epic" rule.

**Discrepancies by ticket** — a table: ticket, criterion, people, skill, the rule the skill applied.

**What I would change in the rubric** — 1–3 specific proposals with wording. These are proposals to the owner, not edits.
```

5. Save the report to `calibration/runs/YYYY-MM-DD.md` to see the trend between rubric edits.

### How to read the result

- Agreement between people < 70% on a criterion → the wording of that criterion in the rubric is vague. Fix the rubric and the examples, not the skill.
- Skill "exact + off by one step" ≥ 85% and "miss" ≤ 5% → the rubric works; the traffic light can be trusted at refinement.
- A systematic bias in one direction → almost always it's one rule in the rubric; find it and fix the wording or the example.
- Discrepancies in the verdict matter more than discrepancies in individual criteria: the verdict is what the team sees in the table.

### When to run

- After every edit to `rubric.md` or `value-types.md`.
- Once a month — together with the review of `disagreements.md`: open disagreements the owner marks "accepted" turn into a rubric edit → calibrate → compare with the previous run.
- The golden set is topped up from disagreements: a ticket people argued with the skill about is the best candidate for the set.
