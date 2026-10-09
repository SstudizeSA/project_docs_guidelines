# Incident Response

Owner: [Name]. Last reviewed: [YYYY-MM-DD]. Practice this process in a drill every quarter.

## 1. Purpose

Restore service fast, tell people the truth, and learn from every serious incident without blaming anyone.

## 2. What Counts as an Incident

An incident is any event that harms users, data, or security, or that is likely to. When unsure, treat it as an incident and lower the level later.

## 3. Severity Levels

| Level | Definition | Example | Respond within | Who is paged | Update rhythm |
|---|---|---|---|---|---|
| SEV1 | Service down, data loss, or active security breach | Nobody can sign in. Customer data exposed. | 15 minutes | On call, lead developer, manager | Every 30 minutes |
| SEV2 | Major feature broken or serious slowdown, workaround is weak | Payments fail for 20% of users | 1 hour | On call, lead developer | Every 2 hours |
| SEV3 | Minor feature broken or small group affected | Report export fails for one customer | Next business day | Ticket to owning team | Daily |

Raise the level if the impact grows. Only the incident commander lowers it.

## 4. Roles

| Role | Job | Who |
|---|---|---|
| Incident commander (IC) | Runs the response, makes decisions, assigns work. Does not debug. | [First senior person who joins] |
| Operations lead | Investigates and fixes | [On call engineer] |
| Communications lead | Sends updates to staff, customers, and the status page | [Support or product lead] |
| Scribe | Writes the timeline as things happen | [Any available person] |
| Security lead | Joins for any security incident | [Name] |

On small teams one person may hold two roles, but never IC and Operations lead together in a SEV1.

## 5. Response Steps

1. **Detect.** An alert, a user report, or a team member notices a problem.
2. **Declare.** Post in [#incidents]: `Incident: [short description], severity [N], IC: [name]`. Open a ticket or incident page: [link].
3. **Assess.** What is broken, who is affected, how many, since when.
4. **Stabilize first.** Pick the fastest safe action: roll back, turn off a feature, scale up, fail over. Do not hunt for the root cause yet.
5. **Communicate.** Send updates on the rhythm in section 3, even if the update is "no change".
6. **Resolve.** Confirm health checks, dashboards, and a user flow test are normal for 30 minutes.
7. **Close.** Announce the end, record the end time, and schedule the review.
8. **Review.** Hold a postmortem (section 8).

## 6. Rules During an Incident

* One channel, one thread of truth: [#incidents]. Side talk goes elsewhere.
* Write what you do before you do it ("restarting API pods now").
* No risky changes without the IC's agreement.
* Keep the timeline in UTC with times.
* Do not guess in public. Share facts and next steps.
* If you are tired after 4 hours, hand over to someone fresh.

## 7. Communication Templates

**Internal update**
```text
[SEV N] [Short title] | Update [number] at [time]
Status: [Investigating | Fix in progress | Monitoring | Resolved]
Impact: [Who and what is affected, with numbers]
What we know: [facts]
What we are doing: [actions]
Next update: [time]
IC: [name]
```

**Customer or status page update**
```text
We are aware of [plain description of the problem]. Since [time], some users cannot [action].
We are working on a fix. Next update by [time].
```

**Resolved message**
```text
The issue with [description] is fixed as of [time]. [One line cause]. We are sorry for the trouble. We will share what we learned within [N] business days.
```

## 8. Postmortem

* Required for every SEV1 and SEV2. Optional for SEV3.
* Meeting within 5 business days. Written report published within 7 business days.
* **Blameless.** Ask "what let this happen?" not "who did this?".

**Template**

| Section | Content |
|---|---|
| Summary | 3 sentences: what happened, how long, how bad |
| Impact | Users affected, failed requests, money lost, data affected, minutes of downtime |
| Timeline (UTC) | Detected at, declared at, mitigated at, resolved at, plus key events |
| Root cause | The real reason, found by asking "why" up to 5 times |
| Trigger | What set it off (a deploy, traffic spike, expired certificate) |
| Detection | How we found out. Could we have found out sooner? |
| What went well | [List] |
| What went badly | [List] |
| Where we got lucky | [List] |
| Action items | Table below |

| Action | Type (prevent, detect, respond) | Owner | Ticket | Due date |
|---|---|---|---|---|
| [Text] | [Type] | [Name] | [#] | [Date] |

Action items are tracked until done. Review open items in [weekly meeting].

## 9. Security Incidents

* Tell the security lead at once.
* Keep evidence: do not delete logs or restart machines unless needed to stop harm.
* Limit who knows until the security lead says otherwise.
* Legal, privacy, and customer notice rules: [link to policy]. Some laws require notice within [72 hours].
* See [../SECURITY.md](../SECURITY.md).

## 10. Measures We Track

| Measure | Meaning | Target |
|---|---|---|
| MTTA | Time from alert to someone acknowledging | Under 5 minutes |
| MTTR | Time from start to resolved | SEV1 under 1 hour |
| Incidents per month by level | Trend | Falling |
| Repeat incidents | Same root cause twice | 0 |
| Action items closed on time | Follow through | 90% or more |

## 11. Drills

Every quarter run one practice incident (a "game day"): pick a scenario, run the process, and fix what breaks in this document.

## 12. Past Incidents

| Date | Level | Title | Report |
|---|---|---|---|
| [YYYY-MM-DD] | [SEV N] | [Title] | [Link] |
