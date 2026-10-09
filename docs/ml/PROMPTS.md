# Prompts

Owner: [Name]. Last reviewed: [YYYY-MM-DD]. Use this file only if the project calls a large language model. A prompt is code: it is versioned, reviewed, and tested. A change to a prompt follows the same pull request process as any other change ([../../CONTRIBUTING.md](../../CONTRIBUTING.md)).

## 1. Rules

1. Every prompt used in production is listed here with an ID and a version.
2. Prompts live in `[src/prompts/]` as files, not as strings inside code. This file explains them. The files are the source of truth.
3. A prompt change needs: a reason, an evaluation run ([EVALUATION.md](EVALUATION.md)), and 1 approval from the ML owner.
4. Never put secrets, keys, or personal data inside a prompt.
5. Changing the model also counts as a prompt change. Re run evaluation.
6. Keep old versions so you can roll back.

## 2. Prompt Index

| ID | Name | Purpose | File | Model | Current version | Owner |
|---|---|---|---|---|---|---|
| `P001` | [summarize_ticket] | [Summarize a support ticket in 3 lines] | `[src/prompts/summarize_ticket.txt]` | [model name] | [v3] | [Name] |
| `P002` | [Name] | [Purpose] | `[path]` | [model] | [v1] | [Name] |

## 3. Prompt Record

> Guide: Copy this block for each prompt.

### `P001` [Name]

* **Purpose:** [What task, for which feature]
* **Input:** [Fields passed in, max size, where it comes from]
* **Output:** [Format, for example JSON with keys `summary` and `priority`]
* **Model and settings:** [model, temperature N, max tokens N, timeout N seconds]
* **Where called:** [`src/...` function name]
* **Safety rules inside the prompt:** [What the model must refuse or avoid]
* **Known failure cases:** [List]
* **Cost per call (estimate):** [tokens in and out, and price]
* **Latency target:** [p95 under N seconds]

**Prompt text (current):** see `[file path]`.

## 4. Version History

| Prompt | Version | Date | Change | Why | Evaluation result | Author |
|---|---|---|---|---|---|---|
| `P001` | v3 | [YYYY-MM-DD] | [Added rule to keep names unchanged] | [Names were being altered in 4% of cases] | [Accuracy 91% to 95%] | [Name] |
| `P001` | v2 | [YYYY-MM-DD] | [Text] | [Text] | [Text] | [Name] |

## 5. Handling Model Output

* Validate output against a schema. If it fails, retry up to [2] times, then use the fallback.
* Fallback: [Return a clear error | use a simple rule based result | ask the user].
* Never run model output as code or as a database query.
* Treat all user supplied text inside a prompt as untrusted (prompt injection risk). Keep instructions and user text separate and tell the model which is which.
* Log the prompt ID, version, token counts, and latency. Log full text only when [rule], and never personal data ([../PRIVACY.md](../PRIVACY.md)).

## 6. Cost and Limits

| Item | Value |
|---|---|
| Monthly budget | [$] |
| Alert at | [80%] of budget |
| Rate limit from provider | [N requests per minute] |
| Our limit per user | [N requests per hour] |

## 7. Review

Every quarter, and whenever the provider announces a model change or retirement, check each prompt against the evaluation set.
