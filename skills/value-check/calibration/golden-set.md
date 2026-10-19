# Golden set for value-check calibration

**This file is assembled only by the skill owner** (`/value-check assemble` or by hand). Raters don't write here - each rates in their own file `ratings/<name>.md` via `/value-check rate`, **independently**, without looking at others' ratings and without running a normal check. The statuses are the same: 🟢 🟡 🔴 ⚪. The rules are in `references/rubric.md`. After assembly - `/value-check calibrate`.

Target size: 15–30 tickets, 2–3 raters. A good mix: half product tickets, a third technical/platform, a few bugs and one or two compliance/spike. Be sure to include tickets where there were disagreements with the skill (`log/disagreements.md`).

Raters: `<A - name/role>`, `<B - name/role>`, `<C - name/role>`

---

## Entry format

```
### <KEY> · <type> · epic: <name or "none">
<ticket text as in Jira - summary and description, unabridged>

| Rater | Com | Eff | Mkt | Cust | Fut | Strat | Verdict | Comment |
|---|---|---|---|---|---|---|---|---|
| A | ⚪ | ⚪ | ⚪ | 🟢 | ⚪ | 🟢 | ✅ | |
| B | … |
| C | … |
```

Comment - only if the status isn't obvious: one phrase, why. It's these comments that later turn into rubric examples.

---

## Rating examples (test tickets, one rater's ratings - replace with your own)

### APP-402 · Story · epic: Onboarding 2.0
**Invite colleagues at step 2 of onboarding.** New admins on the Business plan don't invite anyone in the first week in 70% of cases (Amplitude data, September), and accounts without a second user churn 3 times more often. We're adding an "Invite your team" step with import from Google Workspace. Goal: share of accounts with 2+ users on day 7 - from 30% to 50%. Initiative "Business activation", KR1.

| Rater | Com | Eff | Mkt | Cust | Fut | Strat | Verdict | Comment |
|---|---|---|---|---|---|---|---|---|
| example | ⚪ | ⚪ | ⚪ | 🟢 | ⚪ | 🟢 | ✅ | model example |

### PLT-88 · Technical · epic: Tech debt Q4
**Move from Jenkins to GitHub Actions.** Jenkins is outdated, plugins aren't updated, we want a modern CI. Migrate all pipelines.

| Rater | Com | Eff | Mkt | Cust | Fut | Strat | Verdict | Comment |
|---|---|---|---|---|---|---|---|---|
| example | ⚪ | ⚪ | ⚪ | ⚪ | 🟡 | 🔴 | 🛠 | period-based epic - a folder |

### PLT-91 · Platform · epic: none
**Move the notification queue into a separate service.** Notifications currently go through the shared worker together with reports, and when reports are built at month end, pushes are delayed by 20–40 minutes - 4 P2 incidents and ~60 support complaints over the last 3 months. A separate service with its own queue. Expected: delay < 1 min under any load. Needed before the launch of "Realtime alerts" (a Q1 initiative), which makes no sense without this.

| Rater | Com | Eff | Mkt | Cust | Fut | Strat | Verdict | Comment |
|---|---|---|---|---|---|---|---|---|
| example | ⚪ | 🟢 | ⚪ | ⚪ | ⚪ | 🟢 | ✅ | put the 60 complaints under efficiency, didn't duplicate them under customer |

### APP-417 · Story · epic: none
**PDF export with the customer's logo.** A few customers have asked. Add a logo setting in the profile and insert it into the PDF.

| Rater | Com | Eff | Mkt | Cust | Fut | Strat | Verdict | Comment |
|---|---|---|---|---|---|---|---|---|
| example | ⚪ | ⚪ | ⚪ | 🟡 | ⚪ | 🔴 | 🛠 | |

### APP-420 · Bug · epic: Bugs
**Table filter is not saved after reload.** Steps: apply a filter, F5 - the filter is reset. Expected: the filter is kept.

| Rater | Com | Eff | Mkt | Cust | Fut | Strat | Verdict | Comment |
|---|---|---|---|---|---|---|---|---|
| example | ⚪ | ⚪ | ⚪ | 🟡 | ⚪ | 🔴 | 🛠 | a bug with steps = 🟡, not 🔴 |

---

## Your tickets

<!-- add below, in the format above -->
