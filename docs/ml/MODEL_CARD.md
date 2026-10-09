# Model Card

Owner: [Name]. Last reviewed: [YYYY-MM-DD]. Use one card per model or per model backed feature. Use this file only if the project uses ML or LLM features. Update it with every model, prompt, or data change that affects behavior.

## 1. Summary

| Item | Value |
|---|---|
| Model name and version | [Name, version or checkpoint] |
| Type | [Hosted LLM | Fine tuned model | Classifier | Embedding model | Other] |
| Provider or source | [Company or open source project] |
| License and terms | [Link and summary. See [../THIRD_PARTY_LICENSES.md](../THIRD_PARTY_LICENSES.md)] |
| Used in | [Feature names] |
| Date put in production | [YYYY-MM-DD] |
| Owner | [Name] |
| Replaces | [Previous model, or none] |

## 2. Intended Use

* **Meant for:** [Tasks, users, and settings the model is approved for]
* **Not meant for:** [Tasks it must not be used for, such as medical, legal, or hiring decisions without a human check]
* **Human oversight:** [Who reviews outputs and when]

## 3. How It Is Used Here

* Inputs: [Type, size limits, languages]
* Outputs: [Format and how the app uses them]
* Settings: [Temperature, max tokens, other]
* Prompts: [See [PROMPTS.md](PROMPTS.md)]
* Retrieval or tools: [Data sources, tools the model can call, and limits on them]

## 4. Training or Tuning Data (if we train or tune)

| Item | Detail |
|---|---|
| Sources | [List] |
| Size | [N records] |
| Time range | [Dates] |
| Personal data | [None | Removed by method | Present, with basis] |
| Collection consent and license | [Text] |
| Known gaps | [Languages, groups, topics missing or rare] |

For hosted models we do not train, write: "Training data is described by the provider at [link]."

## 5. Performance

| Test set | Measure | Result | Date |
|---|---|---|---|
| `golden_v1` | [Average human score] | [4.4] | [YYYY-MM-DD] |
| `edge_cases_v1` | [Pass rate] | [78%] | [YYYY-MM-DD] |
| `safety_v1` | [Pass rate] | [99%] | [YYYY-MM-DD] |

Details and method: [EVALUATION.md](EVALUATION.md). Results by group or language (if relevant): [table or link].

## 6. Limits and Known Failure Cases

| Failure | When it happens | How often (from tests) | What we do about it |
|---|---|---|---|
| [Invents facts] | [Question not covered by sources] | [About 2 in 100] | [Require sources, show citations, fall back to "I do not know"] |
| [Weak on a language] | [Input in language X] | [Score 3.1 vs 4.4] | [Route to human] |
| [Long input cut off] | [Over N tokens] | [Always] | [Split input] |

## 7. Risks and Safeguards

| Risk | Safeguard |
|---|---|
| Wrong or made up answers | Source checks, schema validation, human review for [high impact cases] |
| Prompt injection from user or document text | Separate instructions from data, limit tools, never run output as code |
| Leak of personal or secret data | No personal data in prompts unless allowed, output filters, access limits ([../PRIVACY.md](../PRIVACY.md)) |
| Bias or unfair results | Test by group where it applies, review failures |
| Harmful content | Safety test set, provider filters, refusal rules |
| Provider outage or model retirement | Fallback model or non AI path. Check retirement dates every quarter. |
| Cost spike | Budget alerts and per user limits ([PROMPTS.md](PROMPTS.md)) |

## 8. Monitoring and Review

* Dashboards and alerts: [../MONITORING.md](../MONITORING.md), [EVALUATION.md](EVALUATION.md) section 8.
* Review the card: every 6 months and on every model change.
* Retirement plan: [How and when we replace this model].

## 9. Contact and Reporting

Report model problems to [Name or channel]. Security issues follow [../../SECURITY.md](../../SECURITY.md).

## 10. Change History

| Date | Change | Author |
|---|---|---|
| [YYYY-MM-DD] | [First version] | [Name] |
