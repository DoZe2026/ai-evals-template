# Module 5 · Eval Budget · Ascend IQ

**Quarterly budget cap:** $200,000
**Online eval spend:** $0 (0 of at most 3 online evals)

## Budget

| Failure | Trust metric | Risk | Level | Cost |
| --- | --- | :---: | :---: | ---: |
| Data Fabrication | Hallucination Rate | P0 | Periodic audit | $8,500 |
| Context Specificity | Robustness | P1 | Code-based check | $3,500 |
| Overconfident Tone | UX Trust | P1 | Code-based check | $3,250 |
| Data Bias | Fairness | P2 | Code-based check | $2,750 |
| Slow Answers | Latency | P3 | Code-based check | $1,250 |

## Downgrades

### Periodic audit · Data Fabrication (Hallucination Rate · P0)
- **Cheaper check:** Periodic audit, a weekly sample review ($8,500/Q, 10% of the online eval cost).
- **Why it’s enough:** For Automated Data Tagging, fabrication means a label the text doesn’t support, like “guidance cut” on a filing with no guidance. That error is serious but recoverable. Labels are stored, used internally, and can be corrected and backfilled before they cause external harm. So the goal is to catch errors quickly, not to block every one in real time, and scoring live traffic buys protection this product doesn’t need.

A weekly audit shrinks the detection window from a quarter to a week and, for the first time, produces an actual hallucination rate. To make that rate meaningful, sample enough labels each week, roughly 50 to 100, stratified by source, and judge each one on whether the text supports it, not just whether it looks plausible. Track the rate per source, and if it crosses a set threshold such as 2%, pause, investigate and relabel affected data.

### Code-based check · Context Specificity (Robustness · P1)
- **Cheaper check:** A code-based check ($3,500/Q, 5% of the online eval cost), backed by one extra question in the weekly hallucination audit you’re already running.
- **Why it’s enough:** For Automated Data Tagging, this failure means a label that’s true but not specific enough, like tagging a filing as “earnings” when it should be “guidance cut,” or labeling a document’s general topic when the taxonomy asks about one aspect of it. Unlike hallucination, this is mostly systematic. It comes from how the tagger handles certain kinds of text, so it changes when the tagger, prompt or taxonomy changes, not randomly from day to day. A check on release catches it at the point where it’s likely to appear.

The check has two parts. First, build a golden set of a few hundred texts with known specific labels, covering each source and the label pairs most easily confused, and run it on every release, blocking the release if specificity drops. Second, add a rule that tracks the share of broad or catch-all labels per source and alerts if it rises. A sudden shift toward generic labels is a cheap, reliable signal of this failure.

### Code-based check · Overconfident Tone (UX Trust · P1)
- **Cheaper check:** A code-based check ($3,250/Q, 5% of the online eval cost), using data from the weekly audit you’re already running.
- **Why it’s enough:** A tagger has no tone, so for Automated Data Tagging this failure means giving ambiguous text a definite label with no sign of doubt. Downstream models then treat a guess about a vague piece of commentary the same as a clear-cut label on a filing. The fix is a confidence signal the models can use, and checking it is a mechanical, cheap job.

The check has three parts. First, a rule check confirms that every label carries a confidence score, or that the tagger can return “uncertain” and send the item for review. If neither exists today, adding one is a product change you need to make before any eval can measure this. Second, on each release, run the golden set from the specificity check and test calibration: labels marked 90% confident should be right about 90% of the time. Block the release if calibration drifts beyond a set margin. Third, use the weekly audit sample to track whether wrong labels tend to carry high confidence. That’s the clearest sign of overconfidence, and you get it from data you’re already collecting.

### Code-based check · Data Bias (Fairness · P2)
- **Cheaper check:** A code-based check ($2,750/Q, 5% of the online eval cost), splitting results you’re already collecting by region.
- **Why it’s enough:** For Automated Data Tagging, this failure means label quality is uneven across regions. APAC commentary and filings, which often come in different formats, from translated text or with different reporting conventions, might get more wrong, generic or low-confidence labels than US material. Downstream models would then be less reliable on APAC data without anyone noticing. This is a structural gap tied to the tagger and the source mix, so a release check fits it, and it’s P2 because the errors are internal and recoverable.

The check has two parts. First, make sure the golden set has enough APAC examples, at least as many per label as US, and report accuracy, specificity and calibration by region on each release. Block the release if the gap between regions exceeds a set margin. Second, a rule check compares the label mix by region and alerts if one region gets a much higher share of broad, catch-all or “uncertain” labels.

### Code-based check · Slow Answers (Latency · P3)
- **Cheaper check:** A code-based check ($1,250/Q, 5% of the online eval cost), or nothing at all, since you’ve accepted this gap.
- **Why it’s enough:** For Automated Data Tagging, no one is waiting 10 seconds for an answer. Tagging runs in batches, and the only real latency risk is labels arriving too late, leaving downstream models working with stale data. That’s P3, internal and quickly visible, so scoring live traffic would cost $25,000/Q to watch for a problem that barely exists.

If you run the check, make it measure what matters here: label freshness. A rule check records the time from a document arriving to its label being available, per source, and alerts if it exceeds what downstream teams need, for example if filings aren’t tagged by the next model run. Ask the consuming teams for that threshold rather than guessing it. This is cheap, fully automated, and gives you evidence for the quarterly revisit you committed to.



# Lab 2, Ascend IQ Budget Crisis

> Repo file `ai-evals/05-scale/lab-2-budget-crisis.md`. Allocate Level 1/2/3 coverage across the 5 failure modes under the **$200K/quarter cap** with **max 3 at Level 3**.
>
> Fill this with the **Budget Crisis Tool**, then **Copy markdown** and paste it over this file. The headings below mirror the tool's output exactly.

**Quarterly budget cap:** $200,000
**Total Level 3 spend:** _$… (… of max 3 L3 slots used)_

## Portfolio decision grid

| Failure | Trust metric | Risk | Level | Cost |
|---|---|---|---|---|
| Data Fabrication | Hallucination Rate | P0 | _L1 / L2 / L3_ | _$…_ |
| Context Specificity | UX Trust | P1 | _L1 / L2 / L3_ | _$…_ |
| Source Attribution Failure | Robustness | P1 | _L1 / L2 / L3_ | _$…_ |
| Data Bias | Fairness | P2 | _L1 / L2 / L3_ | _$…_ |
| Cost Overruns | Latency | P3 | _L1 / L2 / L3_ | _$…_ |

_Reference L3 costs: Hallucination $85K · Context $70K · Attribution $65K · Bias $55K · Latency $25K. L2 ≈ 10% of L3, L1 ≈ 5% of L3._

## Fallback methods (non-Level 3 items)

### L_n_ · _Failure name_ (_metric_ · _risk_)
- **Method:** _the cheaper fallback you'll run instead of L3_
- **Why this fallback is defensible:** _the story you could defend in a customer incident review — especially if you downgraded a P0/P1._
