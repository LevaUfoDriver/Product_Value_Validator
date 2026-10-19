# value-check

**Does your backlog show value - or just describe work?**

`value-check` is an [Agent Skill](https://agentskills.io) that reviews backlog items against six criteria - the five types of value from [The Liberators' model](https://medium.com/the-liberators/five-types-of-value-84807deab1d) (Commercial, Efficiency, Market, Customer, Future) plus a link to strategy / OKR / MBO / period goals - and returns a traffic light, coaching questions for the author, and a suggested wording. It works on product tickets, bugs, tech debt and platform work alike.

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

- **Single ticket** - what's good, six traffic lights with a justification quoted from the ticket, verdict, 1–4 questions for the author, a draft "Value" section, and an offer to post it as a Jira comment (only after an explicit yes).
- **Backlog slice** - a table for the top 5–20 items (anomalies first), a summary of what the team most often leaves out, one key question per anomaly.
- **Wording help** - the author answers a question in their own words; the skill turns it into 1–3 plain sentences using *only* what they said, marks gaps as `[clarify: …]`, and re-scores.
- **Tech and platform work** - scored on Efficiency and Future value; never penalised for lacking customer or commercial value. Strategy link is required for everyone.
- **Two strategy layers** - long-term strategy (initiatives, job families) and period goals (this quarter's OKR/MBO, numbers optional). Asked for once, kept as a digest, with a freshness check.
- **Feedback loop built in** - every run is logged; disagreements are recorded for the skill owner (the skill never changes its own rubric); `/value-check calibrate` compares the skill against a golden set rated independently by 2–3 people.

## Install

The skill is a plain folder: `skills/value-check/` (English) or `skills/value-check-ru/` (Russian). Pick one.

| Client | How |
|---|---|
| **Claude.ai / Claude desktop** | Download `value-check.skill` from [Releases](../../releases) → Settings → Capabilities → upload. Team/Enterprise owners can publish it org-wide from Admin settings. |
| **Claude Code** | `/plugin marketplace add LevaUfoDriver/Product_Value_Validator` then `/plugin install value-check` - or copy the folder into `.claude/skills/`. |
| **Codex, Cursor, Gemini CLI, Copilot, Goose, OpenCode …** | Copy the folder into your client's skills directory. Each client's location is listed at [agentskills.io/clients](https://agentskills.io/clients). |

Then say `/value-check`, "check this ticket for value", or paste a ticket and ask what's missing. On first run it tells you what it needs (strategy, period goals, tickets) and what it already has.

## Setup for a team

1. Copy `config.example.md` → `config.md` and fill in Jira project keys, custom fields, folder epics, where your strategy lives. `config.md` is git-ignored.
2. Drop a strategy export (Confluence page, markdown, anything) into `strategy/`; the skill makes a 1–2 page digest and reuses it. Add `strategy/goals-2026-Q4.md` for this quarter's goals.
3. Name a skill owner in `config.md` - the only person who edits the rubric and assembles the golden set.
4. After two sprints: `/value-check stats` (is the share of first-run ✅ growing?), review `log/disagreements.md`, run `/value-check calibrate`.

See `references/feedback-and-calibration.md` for the full loop.

## Why these six criteria

The Scrum framework exists to deliver value, but rarely defines it. Christiaan Verwijs' *Five Types of Value* gives each backlog item a question: *with the Product Goal in mind, how does this item increase revenue / save money now / attract users / keep customers / save us from future trouble?* If none can be answered, the item needs an exceptionally good reason to stay. We added a sixth - explicit link to a current goal - because value in general isn't the same as value *for us, now*.

## Credits

Model: [Five Types of Value](https://medium.com/the-liberators/five-types-of-value-84807deab1d) by Christiaan Verwijs, The Liberators. Increment: [Scrum.org](https://www.scrum.org/resources/what-is-an-increment).
Skill: Levon Goncharov ([@LevaUfoDriver](https://github.com/LevaUfoDriver)), built with Claude. MIT license.

---

# Русская версия

**В задачах вашего бэклога есть ценность - или только список работ?**

`value-check` - это [Agent Skill](https://agentskills.io): папка с инструкцией, которую понимает Claude, Codex, Cursor и ещё несколько десятков агентов. Скилл читает задачу из Jira или просто вставленный текст и отвечает на один вопрос: видно ли из описания, зачем эта задача нужна. Кому станет лучше, что изменится, к какой цели компании это ведёт. Если не видно - задаёт автору вопросы и помогает написать.

Проверка идёт по шести критериям. Первые пять - типы ценности из статьи [Five Types of Value](https://medium.com/the-liberators/five-types-of-value-84807deab1d) Кристиана Вервейса (The Liberators): коммерческая, эффективность, рыночная, клиентская, будущая. Шестой - связь с целями: инициатива, OKR, MBO или цель квартала, к которой задача относится. Задача не обязана закрывать все шесть, обычно хватает одной-двух ценностей и связи с целью.

Важно, что это не ревизор. Скилл проверяет, *описал* ли автор ценность, а не решает, нужна ли задача на самом деле. Решение остаётся за людьми.

```
| Задача                                   | Ком | Эфф | Рын | Кли | Буд | Страт | Вердикт       |
|------------------------------------------|-----|-----|-----|-----|-----|-------|---------------|
| APP-420 Фильтр сбрасывается после F5     | ⚪  | ⚪  | ⚪  | 🟡  | ⚪  | 🔴    | 🛠 Доработать |
| PLT-88  Переезд с Jenkins на GH Actions  | ⚪  | ⚪  | ⚪  | ⚪  | 🟡  | 🔴    | 🛠 Доработать |
| APP-402 Пригласить коллег в онбординге   | ⚪  | ⚪  | ⚪  | 🟢  | ⚪  | 🟢    | ✅ Норм       |
| PLT-91  Вынести очередь уведомлений      | ⚪  | 🟢  | ⚪  | ⚪  | ⚪  | 🟢    | ✅ Норм       |
```

🟢 ценность описана и обоснована · 🟡 упомянута, но не обоснована · 🔴 должна быть, а её нет · ⚪ к этой задаче не относится

## Что он делает

**Проверяет одну задачу.** Сначала показывает, что уже хорошо в задаче. Потом - шесть светофоров, и под каждым цитата из задачи, по которой поставлен именно этот цвет. Дальше вердикт, несколько вопросов автору и черновик раздела «Ценность», где вместо недостающих данных стоит `[уточнить: …]`. Если подключена Jira, предложит добавить это комментарием к задаче - но только после явного «да».

**Проверяет кусок бэклога.** Можно дать 5–20 задач сразу: получится таблица как выше, проблемные сверху, и короткая сводка - чего команда не описывает чаще всего. Удобно открыть перед refinement.

**Помогает сформулировать.** Автору часто сложно написать про ценность, хотя он её понимает. Он может ответить на вопрос скилла как получится - скилл переведёт это в два-три нормальных предложения, ничего не добавляя от себя. Цифры, которых не было, останутся пропусками.

**Не топит технические задачи.** Рефакторинг, инфраструктуру и исследования оценивает только по эффективности и будущей ценности; за отсутствие коммерческой или клиентской ценности красный им не ставится. Но планка та же: «код плохой» - жёлтый, «любая правка здесь занимает три дня, а в Q1 сюда нужно добавить две фичи по инициативе X» - зелёный. Связь с целями обязательна для всех.

**Хранит стратегию и цели квартала отдельно.** Стратегия живёт годами, а задачи привязаны к целям на квартал, и они не всегда совпадают дословно. При первом запуске скилл просит документы один раз, делает короткую выжимку и сам предлагает обновить её, когда она устареет. Цифры в целях не обязательны.

**Умеет проверять сам себя.** Каждая проверка записывается в лог; `/value-check stats` показывает, растёт ли доля задач, которые проходят с первого раза. С ним можно спорить - возражение запишется для владельца скилла, сам он правила не меняет. А `/value-check calibrate` сравнивает его оценки с оценками двух-трёх людей на реальных задачах и показывает, где ошибается он, а где расплывчато само правило.

## Установка

Скилл - обычная папка: `skills/value-check-ru/` (русский) или `skills/value-check/` (английский). Выберите одну.

| Где | Как |
|---|---|
| **Claude.ai и Claude для компьютера** | Скачайте `value-check-ru.skill` из [Releases](../../releases) и загрузите в Settings → Capabilities. На планах Team и Enterprise владелец организации может включить скилл сразу всем из админки. |
| **Claude Code** | `/plugin marketplace add LevaUfoDriver/Product_Value_Validator`, затем `/plugin install value-check-ru`. Или скопируйте папку в `.claude/skills/`. |
| **Codex, Cursor, Gemini CLI, Copilot, Goose, OpenCode и другие** | Скопируйте папку в каталог скиллов вашего агента. Где он у каждого - на [agentskills.io/clients](https://agentskills.io/clients). |

Дальше напишите `/value-check` или просто «проверь задачу на ценность» и вставьте задачу. При первом запуске скилл сам скажет, что ему нужно: стратегию, цели квартала и задачи.

## Настройка под команду

1. Скопируйте `config.example.md` в `config.md` и заполните: ключи проектов Jira, нужные поля, какие эпики считать папками, где лежит стратегия. `config.md` в git не попадает.
2. Положите экспорт стратегии (страница Confluence, markdown, что угодно) в `strategy/` - скилл сделает из него выжимку на одну-две страницы. Цели квартала - отдельным файлом вроде `strategy/goals-2026-Q4.md`.
3. Назначьте в `config.md` владельца скилла. Это единственный человек, который правит правила и собирает золотой набор для калибровки.
4. Через два спринта посмотрите `/value-check stats`, разберите возражения в `log/disagreements.md` и запустите `/value-check calibrate`.

Подробнее про лог, возражения и калибровку - в `references/feedback-and-calibration.md`.

## Авторы

Модель пяти типов ценности - [Five Types of Value](https://medium.com/the-liberators/five-types-of-value-84807deab1d), Кристиан Вервейс, The Liberators. Понятие инкремента - [Scrum.org](https://www.scrum.org/resources/what-is-an-increment).
Автор скилла - Левон Гончаров ([@LevaUfoDriver](https://github.com/LevaUfoDriver)), сделано вместе с Claude. Лицензия MIT.
