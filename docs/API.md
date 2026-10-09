# API Reference

Owner: [Name]. Machine readable spec: [openapi.yaml or live docs URL]. If this file and the spec disagree, the spec wins and this file must be fixed.

## 1. Overview

* Style: [REST over HTTPS, JSON]
* Current version: [v1]
* Audience: [Web app, mobile app, partner systems]

## 2. Base URLs

| Environment | URL |
|---|---|
| Local | http://localhost:[8000]/api/v1 |
| Staging | https://staging.[example.com]/api/v1 |
| Production | https://api.[example.com]/v1 |

## 3. Authentication

* Method: [Bearer token (JWT) | API key | OAuth 2.0]
* How to get a token: [endpoint and steps]
* How to send it: `Authorization: Bearer [token]`
* Token lifetime: [60 minutes]. Refresh: [endpoint].
* Permissions: [roles and what each can do. Link to a table below.]

| Role | Can do |
|---|---|
| [admin] | [Everything] |
| [member] | [Read and write own data] |
| [viewer] | [Read only] |

## 4. Conventions

| Topic | Rule |
|---|---|
| Format | JSON, UTF 8. Header: `Content-Type: application/json` |
| Field names | [snake_case] |
| Dates | ISO 8601 in UTC, for example `2026-10-09T11:38:00Z` |
| IDs | [UUID strings] |
| Money | Integer in the smallest unit (cents), plus currency code |
| Null vs missing | [Describe rule] |
| Request ID | Every response has `X-Request-ID`. Include it in bug reports. |

## 5. Versioning and Deprecation

* Version is in the URL path (`/v1`).
* Adding fields or endpoints is not a breaking change. Removing or renaming is.
* Breaking changes get a new version. The old version stays for at least [6 months].
* Deprecated endpoints return a `Deprecation` header and are listed in [../CHANGELOG.md](../CHANGELOG.md).

## 6. Response Format

Success:

```json
{
  "data": { },
  "meta": { "request_id": "[id]" }
}
```

List with paging:

```json
{
  "data": [ ],
  "meta": { "page": 1, "page_size": 50, "total": 1234 }
}
```

## 7. Errors

```json
{
  "error": {
    "code": "[validation_error]",
    "message": "[Human readable text]",
    "details": [ { "field": "[email]", "issue": "[invalid format]" } ],
    "request_id": "[id]"
  }
}
```

| HTTP status | Meaning | Example code |
|---|---|---|
| 400 | Bad request | `bad_request` |
| 401 | Not signed in | `unauthenticated` |
| 403 | Not allowed | `forbidden` |
| 404 | Not found | `not_found` |
| 409 | Conflict | `conflict` |
| 422 | Validation failed | `validation_error` |
| 429 | Too many requests | `rate_limited` |
| 500 | Server error | `internal_error` |
| 503 | Service unavailable | `unavailable` |

## 8. Paging, Filtering, Sorting

* Paging: `page` and `page_size` (default [50], maximum [200]) | or cursor based: `cursor` and `limit`.
* Filtering: `?status=active&created_after=2026-01-01`
* Sorting: `?sort=created_at` (ascending), `?sort=-created_at` (descending)

## 9. Rate Limits

| Client type | Limit | Window |
|---|---|---|
| Anonymous | [N] requests | per minute |
| Signed in user | [N] requests | per minute |
| Partner key | [N] requests | per minute |

Headers returned: `X-RateLimit-Limit`, `X-RateLimit-Remaining`, `Retry-After` (on 429).

## 10. Idempotency

For `POST` requests that create money or orders, send `Idempotency-Key: [unique string]`. Repeating the same key within [24 hours] returns the first result and does not repeat the action.

## 11. Endpoint Reference

> Guide: Copy the block below for every endpoint. Keep endpoints grouped by resource. Put a real, working example in each block.

### 11.1 [Resource name]

#### `[METHOD] [/path/{id}]` [Short title]

* Purpose: [one sentence]
* Auth: [required role or "public"]
* Rate limit: [default or special]

**Path and query parameters**

| Name | In | Type | Required | Description |
|---|---|---|---|---|
| `[id]` | path | string | Yes | [text] |

**Request body**

```json
{ "[field]": "[value]" }
```

| Field | Type | Required | Rules |
|---|---|---|---|
| `[field]` | string | Yes | [1 to 100 characters] |

**Success response** `[200]`

```json
{ "data": { } }
```

**Errors:** `[400, 401, 403, 404, 422]`

**Example**

```bash
curl -X [METHOD] "https://api.[example.com]/v1/[path]" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{ "[field]": "[value]" }'
```

### 11.2 [Next resource]

[Repeat.]

## 12. Webhooks (if used)

| Event | When sent | Payload link |
|---|---|---|
| `[order.created]` | [After an order is saved] | [section or file] |

* Signature: [header name and method to verify]
* Retries: [N tries over N hours]
* Your endpoint must reply within [5 seconds] with a 2xx status.

## 13. Tools and Clients

* OpenAPI file: [path or URL]
* Postman or Insomnia collection: [path or URL]
* SDKs: [list or "none"]

## 14. Change History

See [../CHANGELOG.md](../CHANGELOG.md) for API changes by version.
