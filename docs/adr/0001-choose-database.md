# ADR 0001: Choose the Primary Database

> Guide: This is a sample record that shows the level of detail to aim for. Fill it in with your real decision, or replace it. Copy [0000-template.md](0000-template.md) for new decisions. Number records in order and never reuse a number.

* **Status:** [Proposed | Accepted | Rejected | Superseded by ADR NNNN]
* **Date:** [YYYY-MM-DD]
* **Deciders:** [Names and roles]
* **Consulted:** [People who gave input]
* **Informed:** [People told after the decision]

## 1. Context

[What problem forces a decision now? Include facts and numbers.]

Example: We need a primary data store for [orders and users]. We expect [N] records in 12 months, [N] writes per second at peak, and strict consistency for payments. The team has [N years] of experience with [technologies].

## 2. Decision Drivers

* [Consistency needs: transactions across tables]
* [Query needs: joins, reports, full text search]
* [Scale: size and traffic in 12 months]
* [Team skills]
* [Cost per month]
* [Managed service available in our cloud]
* [Licence and vendor risk]

## 3. Options Considered

| Option | Good | Bad | Estimated cost per month |
|---|---|---|---|
| [PostgreSQL] | [Strong transactions, rich queries, wide skills] | [Needs tuning at very large scale] | [$] |
| [MongoDB] | [Flexible documents, easy scaling] | [Weaker joins, more care for consistency] | [$] |
| [MySQL] | [Mature, simple] | [Fewer advanced features] | [$] |
| [Other] | [Text] | [Text] | [$] |

## 4. Decision

We will use **[option]** because [two or three reasons that tie back to the drivers].

## 5. Consequences

**Good**
* [Result 1]
* [Result 2]

**Bad or costly**
* [Result 1, and how we reduce it]

**Risks**
* [Risk and what we watch for]

**Follow up work**
* [ ] [Task, owner, ticket]

## 6. How We Will Know It Was Right

[Measures and a review date. Example: p95 query time under 50 ms and no data loss incidents after 6 months. Review on [date].]

## 7. Links

* Related decisions: [ADR numbers]
* Design notes or benchmarks: [links]
* Affected docs: [../DATABASE.md](../DATABASE.md), [../ARCHITECTURE.md](../ARCHITECTURE.md)
