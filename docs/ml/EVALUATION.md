# Evaluation

Owner: [Name]. Last reviewed: [YYYY-MM-DD]. Use this file only if the project uses ML or LLM features. No change to a model, prompt, or retrieval step ships unless it beats or matches the numbers here.

## 1. Purpose

Turn "it looks better" into numbers. Every change is scored on the same test set, and the result is saved.

## 2. What We Evaluate

| Feature | Task type | Prompt or model | Owner |
|---|---|---|---|
| [Ticket summary] | [Summarization] | `P001` | [Name] |
| [Document search] | [Retrieval and answer] | `P002` plus retrieval | [Name] |
| [Classifier] | [Classification] | [Model name] | [Name] |

## 3. Test Sets

| Set | Size | Source | Labeled by | Updated | Location |
|---|---|---|---|---|---|
| `golden_v1` | [300] cases | [Real cases, anonymized] | [Two reviewers] | [YYYY-MM-DD] | `[path or storage link]` |
| `edge_cases_v1` | [60] cases | [Hand made hard cases] | [Team] | [YYYY-MM-DD] | `[path]` |
| `safety_v1` | [100] cases | [Unsafe and tricky inputs] | [Security and ML] | [YYYY-MM-DD] | `[path]` |

Rules:
* Never train or tune on the test set. Keep a separate set for tuning.
* No personal data. Anonymize first ([../PRIVACY.md](../PRIVACY.md)).
* Add every production failure to the edge case set.
* Refresh the golden set every [6 months] so it matches real use.
* Label agreement between two reviewers should be [above 85%]. Review disagreements.

## 4. Measures and Release Gates

> Guide: Pick measures that match the task. Set the gate from the current production score, with a margin for noise.

| Feature | Measure | Current production | Gate for release |
|---|---|---|---|
| [Ticket summary] | Correct and complete (human score 1 to 5, average) | [4.2] | [4.2 or higher] |
| [Ticket summary] | Factual errors per 100 summaries | [3] | [3 or fewer] |
| [Document search] | Right document in top 5 (recall at 5) | [88%] | [88% or higher] |
| [Document search] | Answer supported by the sources (groundedness) | [93%] | [93% or higher] |
| [Classifier] | F1 score | [0.91] | [0.91 or higher] |
| All | Safety set pass rate | [99%] | [99% or higher, no new failures in the critical group] |
| All | p95 latency | [3.0 s] | [3.5 s or lower] |
| All | Cost per 1,000 calls | [$] | [No more than 10% rise] |

A change that fails any gate does not ship, unless the ML owner and the project manager sign an exception that is written here.

## 5. How to Run

```bash
[command to run the evaluation, for example: python -m eval.run --set golden_v1 --prompt P001]
```

* Runs in about [N minutes] and costs about [$].
* Results are written to `[results/]` and a summary is posted to the pull request.
* Run at least [3] times for tasks with random output, and report the average and range.

## 6. Human Review

* Review [50] random outputs and all failures each time a prompt or model changes.
* Reviewers use the scoring guide in section 7.
* Two reviewers per item for new test sets.

## 7. Scoring Guide

| Score | Meaning |
|---|---|
| 5 | Correct, complete, clear. Could be sent to a user as is. |
| 4 | Correct. Small style issues. |
| 3 | Mostly correct. Missing something useful. |
| 2 | Contains a mistake that could mislead. |
| 1 | Wrong, harmful, or off topic. |

## 8. Monitoring in Production

| Check | How | Alert |
|---|---|---|
| Quality drift | Sample [50] outputs a week for review | Score down more than [0.3] |
| User feedback | Thumbs up or down rate | Down rate above [10%] |
| Errors and fallbacks | Schema failures, retries, fallbacks used | Above [2%] |
| Cost and latency | Dashboard ([../MONITORING.md](../MONITORING.md)) | Above budget |

## 9. Results Log

| Date | Change | Feature | Set | Key numbers (before to after) | Decision | Report |
|---|---|---|---|---|---|---|
| [YYYY-MM-DD] | [Prompt P001 v3] | [Ticket summary] | `golden_v1` | [Score 4.2 to 4.4, errors 3 to 2 per 100] | [Ship] | [Link] |
