# Security Policy

## 1. Supported Versions

Only these versions receive security fixes.

| Version | Supported | Notes |
|---|---|---|
| [2.x] | Yes | Current release line |
| [1.x] | Fixes for critical issues only until [date] | Plan to upgrade |
| [Below 1.0] | No | End of life |

## 2. How to Report a Vulnerability

**Do not open a public issue, pull request, or chat message for a security problem.**

Use one of these private routes:
1. GitHub: Security tab, then "Report a vulnerability" (private advisory). [Enable this in repo settings.]
2. Email: [security@yourcompany.com]. Encrypt with our key if you can: [PGP key link or fingerprint].

**Please include:**
* What the problem is and where it is (URL, endpoint, file, or version)
* Steps to reproduce
* What an attacker could do (impact)
* Proof of concept, logs, or screenshots, if you have them
* Your name or handle if you want credit

## 3. What You Can Expect From Us

| Step | Our promise |
|---|---|
| Acknowledge your report | Within 48 hours |
| Confirm if it is valid | Within 5 business days |
| Share a fix plan and timeline | Within 7 days of acknowledging |
| Fix and release | Based on severity (table below) |
| Tell you when it is fixed | At release |
| Public disclosure | After the fix is available, usually within 90 days of your report |

## 4. Fix Targets by Severity

| Severity | Example | Target time to fix |
|---|---|---|
| Critical | Remote code execution, full data leak | 7 days |
| High | Auth bypass, access to another user's data | 14 days |
| Medium | Limited data exposure, needs user action | 30 days |
| Low | Minor issue with small impact | Next planned release |

## 5. Scope

**In scope:**
* [Production application and API: https://example.com]
* [Source code in this repository]
* [Official Docker images and build scripts]

**Out of scope:**
* Social engineering or phishing of our staff
* Physical attacks
* Denial of service by sending huge traffic
* Reports from automated scanners with no proof of impact
* Issues in third party services we use (report those to the vendor)
* Missing best practice headers with no real impact

## 6. Safe Harbor

If you act in good faith, follow this policy, avoid harming users, and do not read, change, or keep data that is not yours, we will not take legal action against you.

## 7. Rules for Contributors

* Never commit secrets, keys, tokens, or passwords. Use environment variables ([docs/ENVIRONMENT.md](docs/ENVIRONMENT.md)).
* Secret scanning and dependency scanning run in CI. Fix findings before merge.
* Update vulnerable dependencies within the target times in section 4.
* Treat all user input as unsafe. Validate on the server.
* Auth, payments, and data access code needs 2 approvals.
* If you find a leaked secret, rotate it first, then tell [security contact].

## 8. Security Contacts

| Role | Name | Contact |
|---|---|---|
| Security lead | [Name] | [email] |
| Backup | [Name] | [email] |
