# Ship-or-Hold Memo · Ascend IQ

> **Decision:** HOLD

## The Answer

Hold Ascend IQ until hallucination scoring is live on client traffic with a defined alert threshold and response owner, because data fabrication is our only P0 risk, nothing we run today would catch a made-up competitor price before a client acts on it, and overconfident answers would make that error look like fact.

## The Arguments

### 1. Brand risk: we can’t detect fabricated data before clients see it. Hallucination is marked ❌ for the tagging pipeline that feeds Ascend IQ. The only check that judges correctness is a hand review of 50 labels a quarter. At a true error rate of 2%, there’s about a 36% chance that sample contains no errors at all, so a clean review tells us almost nothing.

Evidence: [The number that proves it]

### 2. Legal and liability risk: wrong answers would look like facts. Overconfident Tone has zero checks running today, even though our row marked it ✅ Covered. A fabricated competitor price stated with full confidence is the kind of error a client acts on and then holds us responsible for.

Evidence: [The number that proves it]

### 3. Cost of holding: the fix is affordable and quick to put in place. Online scoring for both risks costs $150K a quarter, within the $200K cap. With cheaper checks on the other three failure modes, the total is $163.75K, leaving $36K for alerting and incident response. Holding is a short delay to fund a plan we can already pay for, not an open-ended stop.

Evidence: [The number that proves it]

## Next Step · Decision Needed

$163,750 per quarter for evals on Ascend IQ. That’s $150,000 for online scoring of Hallucination ($85,000) and Overconfident Tone ($65,000), plus $13,750 for weekly audits on Context Specificity ($7,000) and Data Bias ($5,500) and a code-based latency check ($1,250). This is within the $200,000 cap.
One accountable owner for the online eval alerts. This person sets the score thresholds, receives alerts, and has authority to pull an answer type from the product when the score is breached. Without this, the online evals only record problems; they don’t stop them.
A ship gate. We go live once both online evals have run for two weeks on pre-launch traffic and hallucination stays below the agreed threshold. I’d propose 1% of answers.

# Ship/Hold Memo · Ascend IQ

> Repo file `ai-evals/06-culture/lab-1-ship-hold-memo.md`. A Pyramid-Principle executive memo: the recommendation comes **first**.
>
> Fill this with the **Ship/Hold Memo Builder**, then **Copy markdown** and paste it over this file. The headings below mirror the tool's output exactly.

> **Decision:** 🚀 SHIP _(or 🛑 HOLD)_

**To:** _[CPO] · cc Eng Lead · Trust & Safety_
**From:** _[Your Name] · AI Evals Cohort · [Date]_

## The Answer

_First sentence = the recommendation and the business reason. Do not bury it._

## The Arguments

### 1. _Argument pillar title_

_…_

### 2. _Argument pillar title_

_…_

### 3. _Argument pillar title_

_…_

## Evidence · Trust Metrics

```
- Metric: result (Gate: bar) PASS/FAIL · Source
- … cite exact numbers from M2–M5 (hallucination rate vs gate, factual grounding %, bias coverage %, p95 latency)
```

## Business Risk

_Quantified SHIP-path vs HOLD-path risk (revenue, churn, competitive window)._

## Next Step · Decision Needed

_A specific decision request with a deadline — e.g. "Approve the Hold rollback by Friday to keep the Q3 launch window."_

## Reflection

_What defining "good enough" forced you to confront._
