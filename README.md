# value-check

**Does your backlog show value — or just describe work?**

`value-check` is an [Agent Skill](https://agentskills.io) that reviews backlog items against six criteria — the five types of value from [The Liberators' model](https://medium.com/the-liberators/five-types-of-value-84807deab1d) (Commercial, Efficiency, Market, Customer, Future) plus a link to strategy / OKR / MBO / period goals — and returns a traffic light, coaching questions for the author, and a suggested wording. It works on product tickets, bugs, tech debt and platform work alike.

It is a coach, not an auditor: it checks whether the author *showed* the value, not whether the ticket is "really" valuable. That decision stays with people.

[Русская версия ниже ↓](#русская-версия)

```
| Ticket                              | Com | Eff | Mkt | Cust | Fut | Strat | Verdict      |
|-------------------------------------|-----|-----|-----|------|-----|-------|--------------|
| APP-420 Filter lost after reload    | ⚪  | ⚪  | ⚪  | 🟡   | ⚪  | 🔴    | 🛠 Needs work |
| PLT-88  Jenkins → GitHub Actions    | ⚪  | ⚪  | ⚪  | ⚪   | 🟡  | 🔴    | 🛠 Needs work |
| APP-402 Invite teammates in onboard | ⚪  | ⚪  | ⚪  | 🟢   | ⚪  | 🟢    | ✅ OK        |
| PLT-91  Split notification queue    | ⚪  | 🟢  | ⚪  | ⚪   | ⚪  | 🟢    | ✅ OK        |
```

🟢 named and justified · 🟡 mentioned, not justified · 🔴 should be there, isn't · ⚪ not applicable

## What it does

- **Single ticket** — what's good, six traffic lights with a justification quoted from the ticket, verdict, 1–4 questions for the author, a draft "Value" section, and an offer to post it as a Jira comment (only after an explicit yes).
- **Backlog slice** — a table for the top 5–20 items (anomalies first), a summary of what the team most often leaves out, one key question per anomaly.
- **Wording help** — the author answers a question in their own words; the skill turns it into 1–3 plain sentences using *only* what they said, marks gaps as `[clarify: …]`, and re-scores.
- **Tech and platform work** — scored on Efficiency and Future value; never penalised for lacking customer or commercial value. Strategy link is required for everyone.
- **Two strategy layers** — long-term strategy (initiatives, job families) and period goals (this quarter's OKR/MBO, numbers optional). Asked for once, kept as a digest, with a freshness check.
- **Feedback loop built in** — every run is logged; disagreements are recorded for the skill owner (the skill never changes its own rubric); `/value-check calibrate` compares the skill against a golden set rated independently by 2–3 people.

## Install

The skill is a plain folder: `skills/value-check/` (English) or `skills/value-check-ru/` (Russian). Pick one.

| Client | How |
|---|---|
| **Claude.ai / Claude desktop** | Download `value-check.skill` from [Releases](../../releases) → Settings → Capabilities → upload. Team/Enterprise owners can publish it org-wide from Admin settings. |
| **Claude Code** | `/plugin marketplace add LevaUfoDriver/Product_Value_Validator` then `/plugin install value-check` — or copy the folder into `.claude/skills/`. |
| **Codex, Cursor, Gemini CLI, Copilot, Goose, OpenCode …** | Copy the folder into your client's skills directory. Each client's location is listed at [agentskills.io/clients](https://agentskills.io/clients). |

Then say `/value-check`, "check this ticket for value", or paste a ticket and ask what's missing. On first run it tells you what it needs (strategy, period goals, tickets) and what it already has.

## Setup for a team

1. Copy `config.example.md` → `config.md` and fill in Jira project keys, custom fields, folder epics, where your strategy lives. `config.md` is git-ignored.
2. Drop a strategy export (Confluence page, markdown, anything) into `strategy/`; the skill makes a 1–2 page digest and reuses it. Add `strategy/goals-2026-Q4.md` for this quarter's goals.
3. Name a skill owner in `config.md` — the only person who edits the rubric and assembles the golden set.
4. After two sprints: `/value-check stats` (is the share of first-run ✅ growing?), review `log/disagreements.md`, run `/value-check calibrate`.

See `references/feedback-and-calibration.md` for the full loop.

## Why these six criteria

The Scrum framework exists to deliver value, but rarely defines it. Christiaan Verwijs' *Five Types of Value* gives each backlog item a question: *with the Product Goal in mind, how does this item increase revenue / save money now / attract users / keep customers / save us from future trouble?* If none can be answered, the item needs an exceptionally good reason to stay. We added a sixth — explicit link to a current goal — because value in general isn't the same as value *for us, now*.

## Credits

Model: [Five Types of Value](https://medium.com/the-liberators/five-types-of-value-84807deab1d) by Christiaan Verwijs, The Liberators. Increment: [Scrum.org](https://www.scrum.org/resources/what-is-an-increment).
Skill: Levon Goncharov ([@LevaUfoDriver](https://github.com/LevaUfoDriver)), built with Claude. MIT license.

---

# Русская версия

**Твой бэклог показывает ценность — или просто описывает работу?**

`value-check` — это [Agent Skill](https://agentskills.io), который проверяет задачи бэклога по шести критериям: пять типов ценности из [модели The Liberators](https://medium.com/the-liberators/five-types-of-value-84807deab1d) (коммерческая, эффективность, рыночная, клиентская, будущая) плюс связь со стратегией / OKR / MBO / целями квартала. На выходе — светофор, вопросы автору в коучинговом тоне и предложенная формулировка. Работает и для продуктовых задач, и для багов, техдолга и платформы.

Это коуч, а не аудитор: он проверяет, *показал* ли автор ценность, а не ценна ли задача «на самом деле». Это решение остаётся за людьми.

## Что умеет

- **Одна задача** — что хорошо, шесть светофоров с обоснованием из текста, вердикт, 1–4 вопроса автору, черновик раздела «Ценность», предложение добавить комментарий в Jira (только после явного «да»).
- **Срез бэклога** — таблица по топ 5–20 задач (аномалии сверху), сводка «чего команда чаще всего не описывает», по одному вопросу на аномалию.
- **Помощь в формулировках** — автор отвечает своими словами, скилл превращает это в 1–3 нормальных предложения *только из сказанного*, пропуски помечает `[уточнить: …]` и пересчитывает светофор.
- **Техзадачи и платформа** — оцениваются по эффективности и будущей ценности, без красных за отсутствие клиентской или коммерческой. Привязка к стратегии обязательна для всех.
- **Два слоя целей** — стратегия (инициативы, job family) и цели периода (OKR/MBO квартала, можно без цифр). Спрашивает один раз, хранит выжимку, следит за свежестью.
- **Встроенная обратная связь** — лог каждого прогона; несогласия записываются для владельца скилла (скилл сам рубрику не меняет); `/value-check calibrate` сравнивает скилл с золотым набором, размеченным 2–3 людьми независимо.

## Установка

Скилл — обычная папка: `skills/value-check-ru/` (русский) или `skills/value-check/` (английский).

| Клиент | Как |
|---|---|
| **Claude.ai / Claude desktop** | Скачать `value-check-ru.skill` из [Releases](../../releases) → Settings → Capabilities → загрузить. В Team/Enterprise владелец организации может опубликовать на всех из админки. |
| **Claude Code** | `/plugin marketplace add LevaUfoDriver/Product_Value_Validator`, затем `/plugin install value-check-ru` — или скопировать папку в `.claude/skills/`. |
| **Codex, Cursor, Gemini CLI, Copilot, Goose, OpenCode …** | Скопировать папку в директорию скиллов клиента; где она у каждого — на [agentskills.io/clients](https://agentskills.io/clients). |

Дальше: `/value-check`, «проверь задачу на ценность» или просто вставь задачу и спроси, чего не хватает. При первом запуске скилл сам скажет, что ему нужно на вход.

## Настройка под команду

1. `config.example.md` → `config.md`: проекты Jira, поля, эпики-папки, где лежит стратегия. `config.md` в git не попадает.
2. Экспорт стратегии (страница Confluence, markdown, что угодно) — в `strategy/`; скилл сделает выжимку на 1–2 страницы. Цели квартала — `strategy/goals-2026-Q4.md`.
3. В `config.md` назначить владельца скилла — единственного, кто правит рубрику и собирает золотой набор.
4. Через два спринта: `/value-check stats` (растёт ли доля ✅ с первого раза?), разбор `log/disagreements.md`, `/value-check calibrate`.

Подробно — `references/feedback-and-calibration.md`.

## Авторы

Модель: [Five Types of Value](https://medium.com/the-liberators/five-types-of-value-84807deab1d), Christiaan Verwijs, The Liberators. Инкремент: [Scrum.org](https://www.scrum.org/resources/what-is-an-increment).
Скилл: Левон Гончаров ([@LevaUfoDriver](https://github.com/LevaUfoDriver)), собран вместе с Claude. Лицензия MIT.
