# Module 5 · Coverage Matrix · Automated Data Tagging

## Coverage Row

| Product | Hallucination Rate | Fairness | Latency | UX Trust | Robustness |
|---|---|---|---|---|---|
| Automated Data Tagging | ❌ Gap | ⚠️ Partial | ❌ Gap | ✅ Covered | ⚠️ Partial |

## What Runs Today

- A code-based check confirms every label comes from the approved list, but not that it’s the right label.
- A data analyst reviews 50 labels by hand each quarter, split by source.
- A check confirms the same kind of text always gets the same label.

## Accepted Gap

**Latency.** The audience is internal and indirect. The labels go to Ascend teams and models, not to customers, regulators or the market. A mislabel doesn’t immediately produce an external-facing decision or statement. Its effect passes through downstream models and people who apply their own judgment, so there’s a buffer between the error and any real-world consequence.

We’ll look again: On a fixed schedule, I’d revisit this alongside the quarterly label review, since that’s when there’s fresh evidence about error rates and it costs little to also ask whether the set of consumers has changed. A fuller reassessment once a year would confirm the downstream map is still accurate.

## Critical Gap

We’ve flagged Hallucination Rate as the most critical gap for Automated Data Tagging because it’s the one failure that every current check is blind to. A hallucinated label is one the text doesn’t actually support, such as tagging a filing as “guidance cut” when it contains no guidance at all. As long as that label comes from the approved list, it passes the code-based check, and if the tagger makes the same mistake on similar text every time, it passes the consistency check too. Both automated controls confirm that labels are well-formed and stable, not that they’re true.

## After the Pressure Test

“What is the hallucination rate today?” Right now I can’t answer that, which is the real problem.


# Lab 1, Ascend Analytics Coverage Matrix

> Repo file `ai-evals/05-scale/lab-1-coverage-matrix.md`. Feeds the **Coverage / scale** slide of the final pitch deck (Module 6).
>
> Fill this with the **Coverage Matrix Tool**, then **Copy markdown** and paste it over this file. The headings below mirror the tool's output exactly. **Force ≥2 ❌ gaps** — an all-green matrix isn't real.

**Product:** _…_

## Coverage row

| Product | Hallucination | Bias | Latency | Toxicity | Drift Monitoring |
|---|---|---|---|---|---|
| _…_ | _✅ / ⚠️ / ❌_ | _✅ / ⚠️ / ❌_ | _✅ / ⚠️ / ❌_ | _✅ / ⚠️ / ❌_ | _✅ / ⚠️ / ❌_ |

## Method + Ground Truth (two ✅/⚠️ cells)

### _Risk name 1_
- **Method:** _how you evaluate it_
- **Ground truth:** _what you grade against_

### _Risk name 2_
- **Method:** _how you evaluate it_
- **Ground truth:** _what you grade against_

## Strategic acceptance

**Accepted gap:** _which ❌ you're accepting_

> _Why it's an acceptable risk right now + the kill criterion / date that would change the call._

## Critical mitigation

- **Critical gap:** _the ❌ you cannot accept_
- **Why critical:** _…_
- **Mitigation plan:** _concrete plan with a date/owner — not "we'll add it later"._
