# Five types of value + strategy

A digest of the "Five Types of Value" model (Christiaan Verwijs, The Liberators, 2021) and the Increment concept from the Scrum Guide, adapted for checking tickets. This is not a retelling of the article but a working reference: how to recognise each type in a ticket's text and what is usually missing.

## The underlying ideas everything rests on

**Value is a transaction with a stakeholder.** Something becomes valuable only when it is delivered to a real stakeholder and confirmed by them. Until then, any value is a hypothesis. A real stakeholder is someone who uses the product or pays for its development, not someone who relays other people's needs (a colleague from marketing is most likely not a stakeholder; a customer whose employees sit in the product every day is).

**Value = business value, with the long term in mind.** The team and the product must still exist tomorrow. So the Product Goal is a filter: something useful to someone that doesn't lead to the Product Goal is not valuable enough to spend time on instead of more valuable things.

**Each type is a question.** All the key questions start with "Given the Product Goal, how does this item…". If the question is easy to answer, value of that type exists. If it's hard, either it's a different type, or there is no value and the item has no business being in the backlog.

**An item with no value type demands an exceptionally strong justification.** This is the skill's main argument: if a ticket doesn't fit any type, the author has to explain why it is in the backlog.

**Increment.** An increment is a concrete, verified, usable step toward the Product Goal that meets the Definition of Done. Value is shown through an increment, not through a report of work done. So a good ticket describes not only "what we'll do" but also "what changes for the stakeholder once it's done" - and that is exactly what gets checked.

---

## 1. Commercial value (Commercial Value)

**Key question:** how will this increase our revenue or profit?

**What it is:** items that bring in money directly. The mental test: is this a line on the customer's invoice? A new paid feature, a paid add-on, a new plan, a new product in the store, content people pay for.

**How to recognise it in a ticket:** mentions of revenue, ARPU, conversion to paid, upsell, a new plan, a contract, a deal, monetisation; a reference to a commercial proposal or a deal condition.

**🟢 looks like:** "Customer X signs a contract worth N on the condition of SSO support; the feature is in the deal scope." "Paid export option: per the survey, 12% of active teams are willing to pay +$5/month."
**🟡 looks like:** "This will help sales." "Customers asked for it, we could monetise it."
**Typical mistake:** confusing it with Customer value - nobody pays for the feature directly, but it retains. If the money isn't directly visible, it's more likely type 4.

## 2. Efficiency value (Efficiency Value)

**Key question:** how will this save us money or time?

**What it is:** items that lower the cost of production, support, operations, delivery. They simplify, automate, remove or smooth out other work. The same value for stakeholders at lower cost. Including the indirect kind: stability that offloads support; shorter rollout time on the customer's side.

**How to recognise it:** "fewer servers", "automate", "cut the time of X from … to …", "offload support", "remove a manual step", "reduce the number of incidents".

**🟢 looks like:** "Deploy currently takes 40 minutes and needs a manual check; after, 5 minutes with no human involved. ~6 team hours a week." "Outages of this service generate ~30 support tickets a week."
**🟡 looks like:** "Will speed up development." "Optimisation." "Will remove unnecessary work."
**Typical mistake:** writing what we'll do but not what we'll save. "Move the build to X" is an action; the value is what gets faster/cheaper and by how much.

## 3. Market value (Market Value)

**Key question:** how will this attract more users or customers?

**What it is:** awareness, entering new markets and segments, differentiation from competitors. Marketing activities, but engineering ones too: porting to another platform, localisation, features "for a new segment", integrations that open up an ecosystem.

**How to recognise it:** "new segment", "market entry", "competitors already have it", "requirement for a marketplace listing", "support for platform Y", "localisation".

**🟢 looks like:** "Without the Z integration we don't make the shortlist with customers in segment S (3 lost tenders in six months)." "The Android version opens up a segment that generates 40% of inbound requests and currently walks away."
**🟡 looks like:** "The market needs this." "Competitors have it."
**Typical mistake:** confusing it with Customer value. Market is about *new* customers, Customer is about *retaining existing* ones.

## 4. Customer value (Customer Value)

**Key question:** how will this raise the likelihood that the customer keeps using the product?

**What it is:** product "stickiness". Convenience, clarity, fewer errors, a better fit for the user's task. Features nobody pays for separately, but which are requested often and which retain.

**How to recognise it:** "users complain", "frequent request", "reduce errors/failures in the scenario", "NPS", "churn", "retention", "simplify scenario X".

**🟢 looks like:** "The report-building scenario is the 2nd most common reason for support tickets (quarterly data); the goal is to halve tickets about it." "5 of 8 customers in interviews named this as their top irritant."
**🟡 looks like:** "Will improve UX." "Users will find it more convenient." "Requested for a long time."
**Typical mistake:** backing it up with the team's opinion instead of a signal from stakeholders. "We think it's more convenient" is a hypothesis; not bad, but you need to say how we'll verify it.

## 5. Future value (Future Value)

**Key question:** how will this save money or time **in the future** / what problems will it prevent?

**What it is:** work that doesn't deliver clear value right away, but without which there will be big problems or costs later. Research, R&D, training, technology alternatives. Reducing tech debt: missing tests, outdated documentation, "spaghetti" nobody dares touch. Security and hardening (they prevent damage from incidents). These are hedges against future trouble, and some of them are worth keeping even if they bring no value now.

**How to recognise it:** "tech debt", "refactoring", "investigate", "spike", "upgrade the version", "outdated dependency", "risk", "security", "preparation for …".

**🟢 looks like:** "Library X goes end-of-life in March; after that we patch any vulnerabilities ourselves. Migrate by end of quarter." "Any change in the module takes 3+ days because of coupling; in Q1, initiative Z needs two features added there."
**🟡 looks like:** "The code is bad, needs a rewrite." "Tech debt." "Upgrade because it's old."
**Important caveat from the article:** there should be few such items in the backlog. If, in a group of tickets, Future value is the only type for most of them, that's a signal for the summary (not a reproach to any specific ticket).

### Compliance is not a separate type

Regulatory compliance, certification, protocols are not value in themselves but a means. Dig into *why* it is valuable: the customer pays for compliance → Commercial; needed so the customer doesn't leave → Customer/Market; security and protection from damage → Future. If it's simply a quality rule, its place is in the Definition of Done, not in a separate ticket. When checking a compliance ticket, ask the author "which of the values does this secure", and don't assign red just because the text says "regulator requirement" - that's yellow with a question.

---

## 6. Strategy link (added by the team)

**Key question:** which goal, initiative, OKR / MBO or job family is the ticket linked to, and how has its impact on that goal been estimated?

**Why:** the five types answer "why is this valuable at all". The sixth answers "why is this valuable *to us now*". A ticket with excellent Customer value that doesn't lead to any current goal is a candidate for "not now". This follows directly from the idea of the Product Goal as a filter.

**Two layers:** strategy (a year or more: initiatives, directions, job family) and period goals (a quarter: current OKR/MBO, which may have no numbers). A link to either counts; a link to a quarterly goal is more common and more natural for backlog tickets. In the evidence, name the level: "Q4 goal '…'", "initiative '…'", "job family …".

**Where to look (cascade):**
1. The Jira hierarchy: ticket → epic → initiative/goal. If the chain reaches a goal, that's a strong signal.
2. Period goals (`strategy/goals-<period>.md`): does the ticket match a quarterly goal.
3. The strategy document / digest (`strategy/strategy-digest.md`): does the ticket semantically match an initiative or a job family.
4. The ticket text: an explicit mention of a goal/initiative/OKR/job family.

**🟢:** an explicit link (a reference to an initiative or a goal, a named job family) **and** an impact estimate - a number, a deadline, a share, or at least a clear cause-and-effect link ("closes about a third of the KR 'onboarding time < 1 day'").
**🟡:** a link exists, but it's indirect or has no estimate ("belongs to the 'Enterprise' initiative", "for the Analyst job family" - without explaining what will change).
**🔴:** no hierarchy, no mention, no semantic match with the strategy.

**For technical tickets** the link usually sounds like "enables initiative Y" or "without this, Z is impossible by the deadline". That's enough for 🟡; with an estimate (deadlines, risk, money) it's 🟢. The link requirement for technical tickets is the same as for product ones.

**If there is no strategy document in context**, grade by the hierarchy and the text, and note in the report that the check against the document was not performed.
