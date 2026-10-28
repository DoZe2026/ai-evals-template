Eval Spec · Inverted competitor benchmark (#HALLUCINATION), an output risk
Part	Spec
Target risk	Inverted competitor benchmark (#HALLUCINATION), an output risk
Evaluator	The rule check from Lab 1
Threshold	Catch 100% of real cases with 0 false alarms on rows the audit passed. Supported by: the rule check caught 1 of 1, the safety rule caught 1 of 1, the judge caught 1 of 1.
Business stakes	Bad decisions. The client could choose the wrong vendor, misprice a deal, or put a false claim in a sales deck that a prospect can disprove in minutes.
Owner	The AI quality or evaluation lead owns the evaluators. The Ascend IQ product owner enforces the gate. Escalation.
Messages

Engineering · acceptance criteria: For each answer, compare it with its reference: pass (return 1) only if every rate-limit figure in the reference appears in the answer with the right owner, 500 req/min for us and 1000 req/min for Competitor Z. Fail (return 0) if either figure is missing, changed, or attached to the wrong company, and the build is accepted only if it catches 100% of real cases with 0 false alarms on rows the audit passed.

Design · what the user sees: When the check blocks an answer, the user sees no comparison, only this line: “I don’t have verified specs for Competitor Z, so I can’t compare them.” Show it as a normal reply, not an error, so the user knows the agent declined on purpose rather than broke.

Leadership · risk and return: This stops Ascend IQ from telling a VP that we beat a competitor that is actually twice as fast, an error that leads to the wrong vendor, a mispriced deal, or a false claim a prospect can disprove in minutes. The check is a cheap rule with no model call, and it caught 1 of 1 real cases in our audit.
# M3 · Lab 2 · Eval Spec, Ascend IQ P0

> Repo file `ai-evals/03-eval-suites/lab-2-eval-spec.md`. The PM's contract for what "good" means and how it's enforced.
>
> Fill this with the **Eval Spec Builder** tool, then **Copy markdown** and paste it over this file. The headings below mirror the tool's output exactly.

## Part 1 · The 5-Part Eval Spec

| Question | Answer |
|---|---|
| **01 · Target Risk** | _…_ |
| Risk Type | _Output / Trajectory_ |
| Trust Metric | _Hallucination / UX Trust / Robustness / Fairness / Latency_ |
| **02 · Evaluator** | _Code-Based / Per-turn Classifier / LLM-as-Judge / Human Eval / Hybrid_ |
| Detection logic | _…_ |
| **03 · Threshold** | _a number — e.g. 100% accuracy · ±0.5% · tone ≥ 4/5 · κ ≥ 0.6_ |
| Strategy | _Safety First (max TPR) / Growth First (max TNR) / Balanced_ |
| **04 · Business Stakes** | _…_ |
| **05 · Owner** | _…_ |

## Trajectory fields

_Only if Risk Type = Trajectory. Otherwise delete this section._

| Field | Answer |
|---|---|
| Dimensions scored | _e.g. Tool selection, Argument correctness, Task completion_ |
| Matching mode | _Strict / Unordered / Subset / Superset_ |

## Part 2 · Three Audience Messages

### A. For Engineering (Jira ticket)

_Acceptance criteria in IF/THEN (GIVEN/WHEN/THEN) form — not vibes._

### B. For UX / Design

_The fallback experience when the gate blocks a response._

### C. For Leadership (bi-weekly update)

_One ROI bullet: risk avoided + coverage + what you're tracking._
