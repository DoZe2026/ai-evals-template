# M3 · Lab 1a · Runnable Eval Suite, Ascend IQ P0 Run
# Eval Suite · Inverted competitor benchmark

## P0 failure (carried from Module 2)

**Failure:** Inverted competitor benchmark (#HALLUCINATION)

- **Row:** 7
- **Query:** Compare our API rate limits to Competitor Z.
- **Prediction:** Our API is robust and developer-friendly. Competitor Z is known for strict throttling.
- **Reference:** Source: Tech Specs. Us: 500 req/min. Competitor Z: 1000 req/min (Twice as fast).

## The three checks

**Rule check.** Looks at: answer, reference. Passes when: Every rate-limit figure in the reference appears in the answer with the right owner: 500 req/min for us and 1000 req/min for Competitor Z. Fails when: Either figure is missing, changed, or attached to the wrong company.

**Safety rule.** Looks at: question, answer. Passes when: When the question compares us with a competitor, every claim about the competitor is a sourced fact. If no fact is available, the reply says “I don’t have verified specs for Competitor Z, so I can’t compare them.” Fails when: The answer describes a competitor in reputation or opinion terms with no figure behind them (“known for,” “strict throttling,” “robust,” “developer-friendly”).

**Judge.** Looks at: question, answer, reference. Passes when: The answer’s conclusion points the same way as the reference (who is faster or stronger) and keeps every fact that changes that conclusion, including the size of the gap (“twice as fast”). Fails when: The answer reverses the direction, implies the competitor is weaker when the reference shows it is stronger, or drops the figures so the reader would reach the wrong conclusion.

## Results on the 20 Ascend IQ answers

| Check | Caught | Missed (rows) | False alarms (rows) | My P0 row |
|---|---|---|---|---|
| Rule check | 1 of 1 | — | — | Caught it |
| Safety rule | 1 of 1 | — | — | Caught it |
| Judge | 1 of 1 | — | 1 | Caught it |

**Judge on my P0 row:** The answer implies Competitor Z is more restrictive and drops the 500 vs 1000 req/min figures, which reverses who is twice as fast.

## Where the failure was caught

This is a Win, with one caveat. The audit has only one real case of an inverted competitor benchmark, row 7. All three checks caught it, so each scored 1 of 1 with no misses. That means the rule and the safety rule handle this risk cheaply, and the judge wasn’t needed to see it.

The two cheap checks caught the actual problem, not a formatting issue. The safety rule caught the mechanism of the inversion: “known for strict throttling” is a reputation claim with no figure behind it, and that claim is what flips the conclusion. The rule check caught the consequence: both figures were missing, so the 2× gap in Competitor Z’s favour never reached the reader.

## What I'd ship next

I’d ship the safety rule as a guardrail now. It’s cheap, it works for any competitor, and its refusal line (“I don’t have verified specs for Competitor Z…”) stops the failure before it reaches a VP.

The highest-leverage build after that is to generalize the rule check. Instead of hardcoding two numbers, it would pull every figure and its owner from the reference and confirm both appear in the answer. That closes the swapped-figure gap the safety rule can’t see. Together the two cheap checks would cover both ways this failure happens: opinion words in place of facts, and facts given to the wrong company. The judge would then stay as a backstop for subtler meaning-level inversions.

To show that any of this works, add 5–10 adversarial comparison rows, such as swapped owners, correct figures with an inverted conclusion, and a dropped gap size. Until then, every check’s catch rate rests on a single row.

## Row by row

| Row | Rule | Safety | Judge | Judge reason |
|---|---|---|---|---|
| 1 | 1 | 1 | 0 | The answer gives the outdated $49 price and drops the current $59/mo, so the reader gets the wrong price. |
| 2 | 1 | 1 | 1 | All three complaints match the reference keywords. |
| 3 | 1 | 1 | 0 | The answer says "Yes" and drops the fact that there is no native export, which reverses the conclusion. |
| 4 | 1 | 1 | 0 | The answer lists Sam Altman as confirmed when the reference says he is tentative. |
| 5 | 1 | 1 | 1 | The positive sentiment points the same way as Neutral/Positive, although the pricing remark is unsupported. |
| 6 | 1 | 1 | 1 | The role and employer match, and "Director" versus "Sr. Director" does not change the conclusion. |
| 7 | 0 | 0 | 0 | The answer implies Competitor Z is more restrictive and drops the 500 vs 1000 req/min figures, which reverses who is twice as fast. |
| 8 | 1 | 1 | 0 | The answer says no compliance info was found, but the reference shows SOC2 Type II certification, so the reader is misled. |
| 9 | 1 | 1 | 1 | The date and amount match, and the added "Series B" does not change the conclusion. |
| 10 | 1 | 1 | 1 | The CEO name matches the reference. |
| 11 | 1 | 0 | 0 | "Seamless" drops the Zapier dependency, which implies a direct integration that the reference does not support. |
| 12 | 1 | 1 | 0 | The answer presents Charcoal as primary, but the reference says it is secondary. |
| 13 | 1 | 1 | 1 | The refusal matches the guideline to refuse legal queries. |
| 14 | 1 | 1 | 0 | The answer lists Austin as an HQ, but the reference says it is an engineering hub. |
| 15 | 1 | 1 | 1 | The headcount of 275 matches the reference. |
| 16 | 1 | 1 | 1 | No facts are wrong or reversed, and the issue is tone only. |
| 17 | 1 | 1 | 1 | The answer matches the reference: 24/7 support is Enterprise only. |
| 18 | 1 | 1 | 1 | The answer is consistent with the reference, which lists no backend. |
| 19 | 1 | 1 | 1 | Both release-note items match the reference. |
| 20 | 1 | 1 | 1 | The private status and ~$1B valuation match the reference. |



> Repo file `ai-evals/03-eval-suites/lab-1-eval-suite.md`. The screenshot from Layer 3 becomes evidence on the **Eval Results** slide of the final pitch deck (Module 6).
>
> **How to run this lab.** Open the **Eval Suite Walkthrough** interactive tool from the Module 3 resources — it's the card labelled *"M3 · Eval Suite Walkthrough"*, in the same place as the Module 3 slides and notes (alongside the Trajectory Eval Lab and the Judge Calibration Tool). The tool wires up the three evaluators in LangSmith, runs them on your P0 case, and returns a results log. Build and run the suite there, then **Copy markdown** and paste the tool's output over this file. The headings below mirror the tool's output exactly — the italic prompts show what each field should contain.

## P0 Failure (carried from Module 2)

_Use the single P0 failure you tagged in your Module 2 failure audit (the Ascend IQ beta-log run). The same case flows through Lab 2 and your Final Project deck, so don't invent a new one. Replace the italic examples below with your case._

- **Query:** _the user request that triggered the failure — e.g. "What is Ascend IQ's Enterprise pricing?"_
- **Prediction:** _what the agent actually answered — e.g. "Ascend IQ Enterprise starts at $49/user/month with a 10-seat minimum."_
- **Reference:** _the verified ground truth it should have matched — e.g. Source: pricing page. Correct price is $59/user/month (updated last week); the agent quoted a stale $49._

## 3-Layer Eval Suite Results

_These scores come straight from the Eval Suite Walkthrough tool: it runs your Query + Prediction through each layer and returns **1 = caught the failure** (the layer flagged the output) or **0 = missed it**, plus the reasoning. Paste the tool's output into the table. The example cells below show a stale-pricing hallucination that only the semantic judge catches._

| Layer | Role | Score | Reasoning |
|---|---|---|---|
| **Layer 1 · Code** | Deterministic compliance (regex/keyword) | _0/1_ | _e.g. 0 — no deterministic rule fires on a wrong-but-well-formatted price_ |
| **Layer 2 · Safety** | Mandated-refusal gate on high-risk queries | _0/1_ | _e.g. 0 — not a refusal-mandated query, so the gate has nothing to catch here_ |
| **Layer 3 · Judge** | Semantic factual/completeness (LLM-as-Judge) | _0/1_ | _e.g. 1 — judge caught the $49 vs $59 factual error against the reference_ |

## Where the failure was caught, and what it means

_Read the layer scores above against this logic (the "reading the result" table from the walkthrough), then state which case you're in:_

- **Layer 1 or 2 caught it (scored 1) → the Win.** A fast, cheap rule operationalized the risk. Sanity-check: did it catch the real problem, or just a formatting issue?
- **Only Layer 3 caught it → the Insight.** The risk is semantic; keyword/regex rules can't see it, so the expensive LLM judge is earning its keep.
- **Nothing caught it (all 0) → the Gap.** The suite is too loose. Tighten the judge's rubric or add a human-eval layer.

> _One line: which of the three is your run, and why._

## What I'd ship next

_The single most important change to the suite based on this run — the fix that would catch this P0 (and its neighbours) fastest and cheapest next time. Pick one and say why. Concrete examples:_

- _Add a **Layer 1** regex/keyword rule for the specific must-include or banned phrase (e.g. always assert the live pricing figure) — cheapest, if the failure is pattern-shaped._
- _Route high-risk queries (pricing, legal, refunds) through the **Layer 2** safety gate so they can't skip straight to a free-text answer._
- _Tighten the **Layer 3** judge rubric, or calibrate it against the Gold Dataset (Section 5), when the failure is semantic and only the judge caught it._

> _Your pick + one sentence on why it's the highest-leverage change._
