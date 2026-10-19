# Team settings

This file is filled in by the team. Anything left blank is skipped by the skill, which then works with the defaults (see SKILL.md). The skill's core (`references/`) does not need to be touched.

## Jira

- **Projects:** `<project keys, comma-separated, e.g. PLT, APP>`
- **Hierarchy field up to the initiative:** `<Parent / Epic Link / custom field, e.g. "Initiative" (customfield_10042)>`
- **Field with the goal / OKR / MBO on the ticket (if any):** `<name or customfield_...>`
- **Job family field (if any):** `<name or customfield_...>`
- **Issue types considered technical:** `Technical, Tech Debt, Platform, Infrastructure, Chore` ← adjust to your scheme
- **Folder epics that do not count as a link to a goal:** by default "Tech debt", "Bugs", "Misc", "Improvements", "Support", "Small stuff", period names. Add your own: `<…>`
- **Hierarchy: known epic-to-goal links** (for cases where it isn't visible in Jira; the skill appends here on your "yes" after disagreements):
  - `<epic> → <goal / MBO / initiative>` e.g.: "Tech debt Q4" → MBO-3 "Reduce delivery time"
- **Default JQL for "top of the backlog":** `project in (<...>) AND status = Backlog ORDER BY rank ASC` (the skill takes the first 10)

## Strategy and goal sources

The skill searches in this order and asks the person only if it finds nothing. If the team has no strategy document, write `none` here and the skill won't ask: `<…>`

1. **Confluence (via the Confluence integration (MCP/connector)):**
   - Strategy: `<page ID or URL>`
   - Goals / OKR / MBO: `<ID or URL>`
   - Job families: `<ID or URL>`
   - Goals for the current period (quarter/month), if kept separately: `<ID or URL>` - optional, numbers not required; greatly improves the alignment check
2. **Local digest:** `strategy/strategy-digest.md` - created by the skill on first load (or placed by the team by hand). Update when the quarter/goals change.
3. **Period goals locally:** `strategy/goals-<period>.md` (e.g. `goals-2026-Q4.md`) - fresh until the end of the period. Update every quarter.
4. **Internal goals site:** `<URL>` - no integration yet; export the needed pages to `strategy/` by hand (markdown or txt).

## Job families

A short list, one line each, so the skill can match tickets. If the list lives in Confluence, keep the link above and don't duplicate it here.

- `<Job family 1>` - `<who this is and their main job>`
- `<Job family 2>` - …

## Log and feedback

- **Log storage:** `<empty - the skill will ask on the first run>`
  Options: a link to a Confluence page · a path to an `.md` in Obsidian · a file in a repository · a Notion page · `local` (don't send). Any place where markdown can be appended.
- **Sync frequency:** `1 day` - the skill reminds you to send the log if more time has passed
- **Strategy digest freshness:** `14 days` - after that the skill suggests updating (doesn't force it). If your strategy changes less often, `30 days` is fine too; more than that is not advisable.
- **Skill owner** (the only one who changes the rubric and assembles the golden set): `<name>`
- **Golden set raters:** `<A - role>`, `<B - role>`, `<C - role>` (2–3 people, rate independently via `/value-check rate`, each in their own file in `calibration/ratings/`)
- **Target golden set size:** `20 tickets`

## Behavior

- **Wording help:** `on` - after the questions, the skill offers to turn the author's reply into wording for the ticket. `off` - questions and a draft with gaps only. Can be switched off in a conversation with the phrase "no help".

- **Report language:** `auto` (the person's language) or pin one: `english` / `русский`
- **Tickets per batch in group mode:** 10 by default, no more than 20
- **Jira comments:** only after explicit confirmation (fixed)
