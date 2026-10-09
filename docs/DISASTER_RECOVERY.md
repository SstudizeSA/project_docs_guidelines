# Disaster Recovery

Owner: [Name]. Last reviewed: [YYYY-MM-DD]. Last full restore test: [YYYY-MM-DD]. A backup that has never been restored is not a backup.

## 1. Scope

This plan covers loss of data, loss of a region or data center, loss of a key vendor, and loss of access to our accounts. Small outages are handled with [RUNBOOK.md](RUNBOOK.md).

## 2. Recovery Targets

| System | RPO (most data we can lose) | RTO (most downtime we accept) | Tier |
|---|---|---|---|
| Production database | [15 minutes] | [1 hour] | 1 |
| API and web app | [N/A, stateless] | [1 hour] | 1 |
| File storage | [24 hours] | [4 hours] | 2 |
| Reports and analytics | [24 hours] | [24 hours] | 3 |
| Internal tools | [24 hours] | [48 hours] | 3 |

> Guide: Targets come from the business. Ask the project manager what a lost hour costs, then set numbers that match the budget.

## 3. What Can Go Wrong

| Scenario | Likelihood | Impact | Plan section |
|---|---|---|---|
| Accidental data deletion or bad migration | Medium | High | 5 |
| Database corruption | Low | High | 5 |
| Region or data center outage | Low | High | 6 |
| Ransomware or account takeover | Low | Very high | 7 |
| Vendor shuts down or locks us out | Low | Medium | 8 |
| Key person unavailable | Medium | Medium | 9 |

## 4. Backups

| Data | Method | Schedule | Kept for | Stored where | Encrypted | Owner |
|---|---|---|---|---|---|---|
| Database full backup | [Managed snapshot] | Daily at [02:00 UTC] | 30 days | [Region B] | Yes | [Name] |
| Database change log (point in time) | [Continuous archive] | Continuous | 7 days | [Region B] | Yes | [Name] |
| Uploaded files | [Versioned bucket copy] | Continuous | 90 days | [Region B] | Yes | [Name] |
| Config and infrastructure code | Git | On every commit | Forever | [Host and mirror] | N/A | [Name] |
| Secrets | [Vault backup] | Daily | 30 days | [Location] | Yes | [Security lead] |

Rules: backups live in a different account or region than the source. At least one copy cannot be deleted by normal staff (immutable or separate access).

## 5. Restore the Database

1. Declare an incident ([INCIDENT_RESPONSE.md](INCIDENT_RESPONSE.md)). Stop writes if data is being damaged.
2. Pick the restore point: [latest snapshot | point in time just before the bad event].
3. Restore to a **new** instance. Do not overwrite the damaged one.
4. Check row counts and sample records against expectations.
5. Point the app to the new instance: `[command or config change]`.
6. Run the smoke test ([TESTING.md](TESTING.md)).
7. Open writes again. Watch dashboards for 1 hour.
8. Keep the damaged instance for investigation until the security or database lead says to remove it.

Expected time for a database of [N GB]: [N minutes]. Measured in the last test: [N minutes].

## 6. Region or Data Center Outage

1. Confirm the outage with the provider status page.
2. Decide: wait or fail over. Rule: fail over if the provider estimate is longer than [RTO minus 20 minutes].
3. Steps to fail over: [Bring up infrastructure from `infra/` code in region B, restore latest database backup, change DNS, check certificates].
4. DNS change takes up to [N minutes] to spread. Set a low TTL ([300 seconds]) ahead of time.
5. Plan the return to the main region after it is healthy. Do it in a planned window.

## 7. Ransomware or Account Takeover

1. Tell the security lead at once. Treat as a SEV1.
2. Cut off the attacker: disable affected accounts, rotate all keys and tokens, revoke sessions.
3. Do not pay or contact attackers. Legal and management decide.
4. Rebuild from clean code and restore data from backups made before the break in.
5. Legal and privacy notices: see [PRIVACY.md](PRIVACY.md). Some laws require notice within [72 hours].

## 8. Vendor Loss

| Vendor | What we use it for | Exit plan | Data export method |
|---|---|---|---|
| [Cloud provider] | [Hosting] | [Move to other provider using infra code in N weeks] | [Method] |
| [Payment provider] | [Payments] | [Backup provider integration] | [Method] |
| [Email provider] | [Email] | [Alternate provider, config ready] | [Method] |

## 9. People and Access

* At least 2 people can run each recovery step. Names: [list].
* Emergency access (break glass) steps: [text].
* Contact list with phone numbers is stored [location outside the main systems].

## 10. Testing the Plan

| Test | How often | Last done | Result |
|---|---|---|---|
| Restore database backup to a new instance | Every quarter | [YYYY-MM-DD] | [Time taken, pass or fail] |
| Restore a deleted file | Every quarter | [YYYY-MM-DD] | [Result] |
| Full fail over exercise | Every year | [YYYY-MM-DD] | [Result] |
| Read through this document | Every 6 months | [YYYY-MM-DD] | [Changes made] |

Every test ends with a short report and fixes to this document.

## 11. Contact List

| Role | Name | Phone | Backup |
|---|---|---|---|
| Incident commander | [Name] | [Number] | [Name] |
| Database owner | [Name] | [Number] | [Name] |
| Platform lead | [Name] | [Number] | [Name] |
| Security lead | [Name] | [Number] | [Name] |
| Executive sponsor | [Name] | [Number] | [Name] |
| Cloud provider support | N/A | [Number and account ID location] | N/A |
