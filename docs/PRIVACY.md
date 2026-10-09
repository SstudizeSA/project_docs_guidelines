# Privacy and Data Policy

Owner: [Security lead or data protection contact]. Last reviewed: [YYYY-MM-DD]. This is an engineering reference, not legal advice. Have your legal team review it against the laws that apply to you, for example GDPR, India's DPDP Act, or CCPA.

## 1. Purpose

Say exactly what personal data this project holds, why, for how long, and who can see it, so that developers make safe choices and the company can answer questions from users and regulators.

## 2. Data Inventory

| Data item | Category | Where stored | Why we need it | Legal basis | Kept for | Who can access |
|---|---|---|---|---|---|---|
| [Email address] | Contact | `[table.column]` | Sign in, notices | [Contract] | Account life plus [N days] | [App, support] |
| [Name] | Contact | `[table.column]` | Show in the app | [Contract] | Account life plus [N days] | [App, support] |
| [IP address] | Technical | Logs | Security, debugging | [Legitimate interest] | [30 days] | [Platform, security] |
| [Payment data] | Financial | Held by [provider], not by us | Take payments | [Contract] | Per provider | N/A |
| [Uploaded files] | User content | [Bucket] | Core feature | [Contract] | Until the user deletes them | [Owner, support on request] |

> Guide: List every field that can identify a person, alone or with others. If you are not sure, list it.

## 3. Data Classes and Handling

| Class | Examples | Storage rule | Logging rule | Sharing rule |
|---|---|---|---|---|
| Public | Marketing text | Any | Allowed | Allowed |
| Internal | Metrics, design docs | Company systems | Allowed | Staff only |
| Personal | Name, email, phone | Encrypted at rest | Mask or leave out | Need to know only |
| Sensitive | Government ID, health, payment, passwords | Encrypted, tightest access | Never logged | Approval from security lead |

## 4. Rules for Developers

* Collect the least data needed. Do not add a field "just in case".
* Encrypt in transit (HTTPS or TLS 1.2 or higher) and at rest.
* Never put personal data in logs, error messages, URLs, test data, or screenshots.
* Use fake or anonymized data outside production.
* Hash passwords with a slow, salted method ([bcrypt | argon2]). Never store them in plain text.
* Check access on the server for every request.
* Mask personal data in admin screens unless the person needs to see it.

## 5. User Rights and How We Handle Them

| Request | What it means | How we do it | Deadline |
|---|---|---|---|
| Access | Send the user their data | [Export tool or script] | [30 days] |
| Correction | Fix wrong data | [In app or support] | [30 days] |
| Deletion | Remove the user's data | [Delete job, steps, what is kept by law] | [30 days] |
| Export | Give data in a usable format | [JSON or CSV export] | [30 days] |
| Objection or limit use | Stop certain uses | [Process] | [30 days] |

Requests come to [email or form] and are handled by [role]. Each request is logged.

## 6. Retention and Deletion

| Data | Keep for | Then |
|---|---|---|
| Account data | While the account is active | Delete or anonymize within [N days] after closing |
| Logs | [30 days] hot, [12 months] archive | Delete |
| Backups | [30 days] | Expire automatically. Deleted data leaves backups on that schedule. |
| Support tickets | [24 months] | Delete or anonymize |

Automatic delete jobs are tested. Owner: [Name].

## 7. Third Parties That Receive Personal Data

| Vendor | Data shared | Purpose | Location | Agreement in place |
|---|---|---|---|---|
| [Cloud provider] | All app data | Hosting | [Region] | [Yes, DPA signed on date] |
| [Email provider] | Name, email | Send email | [Region] | [Yes] |
| [Analytics tool] | [Pseudonymous IDs] | Usage statistics | [Region] | [Yes] |

See also [THIRD_PARTY_LICENSES.md](THIRD_PARTY_LICENSES.md) for software licenses (a separate topic).

## 8. Breach Handling

1. Treat any suspected exposure of personal data as a SEV1 security incident ([INCIDENT_RESPONSE.md](INCIDENT_RESPONSE.md)).
2. The security lead and legal decide on notice to regulators and users. Many laws set a deadline, often 72 hours from when we know.
3. Keep a record of what happened, what data, how many people, and what we did.

## 9. Children's Data

[State whether the service accepts users under 18 (or the local age). If not, how this is enforced. If yes, the extra rules.]

## 10. If the Project Uses AI or ML

* Do not send personal data to outside model providers unless the contract allows it and the user was told. See [ml/PROMPTS.md](ml/PROMPTS.md).
* State whether user content is used for training. Default: no.
* Remove personal data from datasets used for evaluation ([ml/EVALUATION.md](ml/EVALUATION.md)).

## 11. Review

Every 6 months, and on every new feature that handles personal data. Add a privacy check to the pull request for such features. Contact for questions: [email].
