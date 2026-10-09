# Monitoring and Alerting

Owner: [Name]. Last reviewed: [YYYY-MM-DD]. Playbooks for each alert are in [RUNBOOK.md](RUNBOOK.md).

## 1. Goals

* Know about a problem before users tell us.
* Page a person only when a person must act.
* Show the health of the system on one screen.

## 2. Tools

| Purpose | Tool | Link | Owner |
|---|---|---|---|
| Metrics and dashboards | [Grafana | Datadog | CloudWatch] | [url] | [Team] |
| Logs | [ELK | Loki | Datadog] | [url] | [Team] |
| Error tracking | [Sentry] | [url] | [Team] |
| Uptime checks | [Pingdom | UptimeRobot] | [url] | [Team] |
| Tracing | [OpenTelemetry with Jaeger] | [url] | [Team] |
| Paging | [PagerDuty | Opsgenie] | [url] | [Team] |
| Status page | [Statuspage] | [url] | [Team] |

## 3. Service Level Objectives

| Measure | Target | Window | Error budget |
|---|---|---|---|
| Availability | 99.9% | 30 days | About 43 minutes of downtime |
| API p95 latency | Under 300 ms | 30 days | 5% of requests may be slower |
| API error rate (5xx) | Under 0.5% | 30 days | N/A |
| Background job delay | 95% start within [60 seconds] | 7 days | N/A |
| Data freshness | [Reports updated within 15 minutes] | 7 days | N/A |

When more than 50% of the error budget is used in the first half of a window, slow down new feature releases and spend time on reliability.

## 4. The Four Golden Signals

| Signal | What we measure | Where |
|---|---|---|
| Latency | Request time p50, p95, p99 per endpoint | [Dashboard] |
| Traffic | Requests per second, active users | [Dashboard] |
| Errors | 4xx and 5xx rates, failed jobs, exceptions | [Dashboard] |
| Saturation | CPU, memory, disk, connections, queue depth | [Dashboard] |

## 5. Dashboards

| Dashboard | Shows | Used by |
|---|---|---|
| Overview | Golden signals, deploy markers | Everyone, on call first stop |
| API detail | Per endpoint latency and errors | Developers |
| Database | Connections, slow queries, replica lag | Developers, database owner |
| Queue and workers | Depth, age, failures | Developers |
| Business | [Orders per hour, sign ups] | Product, support |
| Cost | Cloud spend by service | Platform |

## 6. Alerts

> Guide: Every page must have a playbook and need action now. Alerts that fire and need nothing are removed or turned into a ticket.

| Alert | Condition | Level | Goes to | Playbook |
|---|---|---|---|---|
| Service down | Health check fails 3 times in 3 minutes | Page (SEV1) | On call | [RUNBOOK.md](RUNBOOK.md) |
| High error rate | 5xx above 1% for 5 minutes | Page (SEV2) | On call | [RUNBOOK.md](RUNBOOK.md) |
| High latency | p95 above 500 ms for 10 minutes | Page (SEV2) | On call | [RUNBOOK.md](RUNBOOK.md) |
| Queue backlog | Oldest job older than 15 minutes | Page (SEV2) | On call | [RUNBOOK.md](RUNBOOK.md) |
| Disk or memory high | Above 85% for 15 minutes | Ticket | Team channel | [RUNBOOK.md](RUNBOOK.md) |
| Certificate expiry | Less than 21 days left | Ticket | Platform | [RUNBOOK.md](RUNBOOK.md) |
| Error budget use | More than 50% used in half the window | Notify | Lead developer | This file |

## 7. Logging Rules

* Write structured JSON logs.
* Required fields: `timestamp` (UTC), `level`, `service`, `environment`, `request_id`, `message`.
* Never log passwords, tokens, full card numbers, or personal data.
* Keep logs for [30 days] hot and [12 months] archived. See [PRIVACY.md](PRIVACY.md).
* Use levels with care: ERROR means someone should look.

## 8. Health Endpoints

| Endpoint | Meaning | Checks |
|---|---|---|
| `/health` | Process is running | Returns 200 quickly |
| `/ready` | Ready for traffic | Database and cache reachable |

## 9. Tracing and Request IDs

Every request gets a `request_id` and passes it to all services and logs. Users can quote it in support requests.

## 10. Review Rhythm

| When | What |
|---|---|
| Daily | On call checks the overview dashboard |
| Weekly | Review pages from the last week, remove noisy alerts |
| Monthly | Check SLO results and error budget |
| Quarterly | Test that alerts fire (fire drill), update this file |
