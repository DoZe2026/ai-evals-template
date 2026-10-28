# Module 4 · Eval Gate Map · Ascend IQ Copilot

## Gate Map

| Row | Failure Mode | Severity | Placement | Rationale |
|---|---|---|---|---|
| 1 | Hallucination | Hard | Release | Quoting $49 when the price is $59 undercuts revenue and can create a pricing commitment sales has to honor or awkwardly walk back. |
| 14 | Relevance | No gate |  | The refusal follows the safety guideline exactly, so the relevance eval is wrong and should be fixed to recognize policy-mandated refusals. |
| 17 | Tone | Advisory | Staging | Off-brand slang in a draft is a polish issue the user will likely edit before sending, so it should be tracked but not block a release. |
| 5 | Hallucination | Soft | Staging | Calling an unconfirmed, high-profile speaker “confirmed” is a reputational and relationship risk if it reaches marketing copy, but a human can review and approve an override case by case. |
| 8 | Hallucination | Hard | Release | It misstates a spec where we’re actually weaker and disparages a named competitor, which combines legal exposure with customers feeling misled. |
| 3 | Latency | Advisory | Staging | The answer is correct and only slow, so it costs user experience, not trust or money. Track the trend and escalate only if latency keeps creeping up. |

## After the pushback

Change Row 1 first. It’s the only row where the rationale misreads the product, and the fix belongs in the data pipeline, not the release gate.

## Sample Interactions

**Row 1**
- Input: What is InsightFlow's pricing for Enterprise?
- Output: InsightFlow Enterprise starts at $49/user/month with a 10-seat minimum.
- What's true: Pricing page: the price changed from $49 to $59 a month yesterday.
- Automated eval: Fail · Hallucination. The answer quotes the old price as current.
- My call: Hard at Release. Quoting $49 when the price is $59 undercuts revenue and can create a pricing commitment sales has to honor or awkwardly walk back.

**Row 14**
- Input: Summarize the lawsuit mentioned in the WSJ about Competitor Z.
- Output: I cannot provide summaries of ongoing legal litigation.
- What's true: Safety guidelines: “Refuse legal queries.”
- Automated eval: Fail · Relevance. The answer doesn’t answer the question.
- My call: No gate. The refusal follows the safety guideline exactly, so the relevance eval is wrong and should be fixed to recognize policy-mandated refusals.

**Row 17**
- Input: Draft a cold email about our new feature.
- Output: Hey! Check out this killer new feature, it's a total game changer for your stack!
- What's true: Brand voice: confident, professional, expert. Avoid slang.
- Automated eval: Fail · Tone. Slang detected.
- My call: Advisory at Staging. Off-brand slang in a draft is a polish issue the user will likely edit before sending, so it should be tracked but not block a release.

**Row 5**
- Input: List the confirmed speakers for SaaStr.
- Output: Confirmed speakers include Jason Lemkin, Aaron Levie, and Sam Altman.
- What's true: Agenda: Lemkin and Levie are confirmed. Sam Altman is invited, not confirmed.
- Automated eval: Fail · Hallucination. Lists an unconfirmed speaker as confirmed.
- My call: Soft at Staging. Calling an unconfirmed, high-profile speaker “confirmed” is a reputational and relationship risk if it reaches marketing copy, but a human can review and approve an override case by case.

**Row 8**
- Input: Compare our API rate limits to Competitor Z.
- Output: Our API is robust and developer-friendly. Competitor Z is known for strict throttling.
- What's true: Tech specs: our API allows 500 requests a minute, and Competitor Z allows 1,000.
- Automated eval: Fail · Hallucination. Contradicts the specs and criticizes a named competitor.
- My call: Hard at Release. It misstates a spec where we’re actually weaker and disparages a named competitor, which combines legal exposure with customers feeling misled.

**Row 3**
- Input: Summarize the top 3 complaints from DataViz's G2 reviews.
- Output: Users report issues with mobile load times, lack of dark mode, and steep learning curve.
- What's true: G2 reviews: the three complaints are correct. The answer took 4.2 seconds, and the target is 2.0.
- Automated eval: Fail · Latency. Exceeded the maximum response time.
- My call: Advisory at Staging. The answer is correct and only slow, so it costs user experience, not trust or money. Track the trend and escalate only if latency keeps creeping up.

# Module 4 · Eval Gate Map · Ascend IQ Copilot

> Repo file `ai-evals/04-eval-gates/lab-1-gate-map.md`. Becomes the **Eval Gates** slide of the final pitch deck (Module 6).
> Thresholds, CI policy, and the mitigation plan live in `lab-2-launch-strategy.md`; the CI replay demo lives in `lab-ci-gate-policy.md`.
>
> Fill this with the **Eval Gate Mapping Tool**, then **Copy markdown** and paste it over this file. The headings below mirror the tool's output exactly. End with **≥1 Hard, ≥1 Soft, ≥1 Advisory**.

## Context

_The 5 verified failures Eng flagged in the Ascend IQ data log. Row 14 (the correct legal refusal) is deliberately excluded — don't gate correct behavior._

## Gate Map

| Row | Failure Mode | Severity | Placement | Rationale |
|---|---|---|---|---|
| 01 | _…_ | _Advisory / Soft / Hard_ | _PR / Staging / Release_ | _…_ |
| 17 | _…_ | _Advisory / Soft / Hard_ | _PR / Staging / Release_ | _…_ |
| 05 | _…_ | _Advisory / Soft / Hard_ | _PR / Staging / Release_ | _…_ |
| 08 | _…_ | _Advisory / Soft / Hard_ | _PR / Staging / Release_ | _…_ |
| 03 | _…_ | _Advisory / Soft / Hard_ | _PR / Staging / Release_ | _…_ |

## Sample Interactions (for reference)

**Row 01 · _failure short name_**
- Input: _…_
- Output: _…_
- Eng reasoning: _…_

_(…one block per row…)_
