# Runbook

For the person on call. Written to be used at 3 AM by someone tired and in a hurry. Keep steps short and exact. Test these steps every quarter.

Owner: [Name]. Last reviewed: [YYYY-MM-DD].

## 1. First 5 Minutes

1. Open the main dashboard: [link].
2. Check recent deploys: [link]. A deploy in the last hour is the top suspect. If so, consider a rollback ([DEPLOYMENT.md](DEPLOYMENT.md)).
3. Decide the severity ([INCIDENT_RESPONSE.md](INCIDENT_RESPONSE.md)). If SEV1 or SEV2, start an incident.
4. Post in [channel]: what you see, and that you are looking.

## 2. Service Summary

| Item | Value |
|---|---|
| What it does | [One sentence] |
| Components | [API, worker, database, cache, queue] |
| Dependencies | [External services] |
| Traffic pattern | [Peak hours, normal load] |
| Business impact if down | [What users cannot do, cost per hour if known] |

## 3. Where to Look

| What | Link |
|---|---|
| Main dashboard | [url] |
| Logs | [url and saved search] |
| Error tracking | [url] |
| Uptime monitor | [url] |
| Pipeline and deploy history | [url] |
| Cloud console | [url] |
| Status page | [url] |
| More on metrics | [MONITORING.md](MONITORING.md) |

## 4. Access

* How to get production access in an emergency: [process, who approves]
* Where credentials live: [secret manager or password vault]
* Break glass accounts: [rules for use, must be reported after use]

## 5. Health Checks

| Check | Command or URL | Healthy result |
|---|---|---|
| API | `curl https://[host]/health` | HTTP 200 and `{"status":"ok"}` |
| Database | `[command]` | [Connections under N, replica lag under N seconds] |
| Queue | `[command]` | [Depth under N, oldest message under N minutes] |
| Cache | `[command]` | [Responds, memory under N%] |

## 6. Common Operations

### 6.1 Restart a service
```bash
[command]
```
Expect: [result]. Wait [N minutes] and re check health.

### 6.2 Scale up or down
```bash
[command]
```

### 6.3 Clear the cache
```bash
[command]
```
Warning: [effect on load].

### 6.4 Replay or clear a stuck queue
```bash
[command]
```

### 6.5 Rotate a secret
1. [Create new value]
2. [Update in secret manager]
3. [Restart or reload services]
4. [Revoke old value]
5. [Verify]

### 6.6 Run a database migration by hand
See [DATABASE.md](DATABASE.md). Ask a second person to watch.

### 6.7 Turn a feature off
Set flag `[name]` to `false` in [tool]. No deploy needed.

## 7. Alert Playbooks

> Guide: One block per alert. Every alert that can wake someone must have a playbook. If an alert has no clear action, delete it.

### Alert: [High error rate]

* **Fires when:** [error rate above 1% for 5 minutes]
* **Meaning:** [Users are seeing failures]
* **Impact:** [Which flows]
* **Check:**
  1. [Recent deploy?]
  2. [Look at top errors in the error tracker]
  3. [Dependency status]
* **Fix:**
  * [If bad deploy: roll back]
  * [If dependency down: see section 8]
  * [If load spike: scale up]
* **Escalate to:** [Name or team] if not fixed in [20 minutes].

### Alert: [High latency]
[Repeat the same fields.]

### Alert: [Database connections near limit]
[Repeat the same fields.]

### Alert: [Queue backlog growing]
[Repeat the same fields.]

### Alert: [Disk or memory above 85%]
[Repeat the same fields.]

## 8. If a Dependency Fails

| Dependency | Symptom | What the app does alone | What you do |
|---|---|---|---|
| [Database] | 5xx on most requests | Nothing works | [Fail over to replica: steps] |
| [Cache] | Slow responses | Falls back to database | [Restart, or run without cache] |
| [Payment provider] | Payment errors | Orders are queued | [Check provider status, wait, replay] |
| [Email provider] | Emails delayed | Queued for retry | [Check status, switch provider if set up] |

## 9. Escalation

| Level | Who | When | Contact |
|---|---|---|---|
| 1 | Primary on call | First responder | [Pager or phone] |
| 2 | Secondary on call | No reply in 10 minutes | [Contact] |
| 3 | Lead developer | SEV1, or not fixed in 30 minutes | [Contact] |
| 4 | Engineering manager | SEV1 lasting over 1 hour, or customer impact | [Contact] |
| Security | Security lead | Any suspected breach | [Contact] |
| Vendors | [Vendor support lines] | Their service is the cause | [Contact, account number location] |

## 10. On Call Basics

* Rotation: [weekly, handoff on Monday at 10:00]
* Acknowledge pages within [5 minutes].
* Handoff note: open issues, recent changes, things to watch.
* After a night page, you may start late. Tell [manager].
* Pay or time off rules: [link].

## 11. Known Issues

| Issue | Workaround | Ticket | Since |
|---|---|---|---|
| [Text] | [Text] | [#] | [Date] |

## 12. After the Fix

1. Confirm health checks pass and dashboards are normal for 30 minutes.
2. Update the status page and [channel].
3. Write the incident notes while fresh. See [INCIDENT_RESPONSE.md](INCIDENT_RESPONSE.md).
4. Fix this runbook if any step was wrong or missing.
