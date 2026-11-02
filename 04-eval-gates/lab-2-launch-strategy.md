# Module 4 · Launch Strategy · Ascend IQ Copilot

## 4.0 Release Criteria

| Gate | Failure | Metric | Threshold | Dataset | Method | Runs at |
|---|---|---|---|---|---|---|
| Hard | Inverted competitor benchmark (#HALLUCINATION): the agent swaps or misstates rate-limit figures, claiming we beat Competitor Z when they’re actually twice as fast. | Share of comparison answers where every rate-limit figure from the reference appears with the right owner: 500 req/min for us and 1000 req/min for Competitor Z. | 100% of real cases caught, with 0 false alarms on rows the audit passed. | Ascend IQ golden set | Code-based check | Staging |
| Soft | Row 5 · Hallucination: lists an unconfirmed speaker as confirmed | Share of speaker-list answers that name someone as “confirmed” who isn’t marked confirmed on the agenda (such as Sam Altman, who is only invited). | 0% | Ascend IQ golden set | Code-based check | Staging |
| Advisory | Row 17 · Tone: slang detected | Share of drafted emails that use slang or break the brand voice (confident, professional, expert). | 0% | Ascend IQ golden set | LLM judge | Pull Request |

## CI Gate Request for Engineering

- **Hard gate · Inverted competitor benchmark (#HALLUCINATION): the agent swaps or misstates rate-limit figures, claiming we beat Competitor Z when they’re actually twice as fast..** Check: the code-based check, run on the Ascend IQ golden set at Staging. Measures: Share of comparison answers where every rate-limit figure from the reference appears with the right owner: 500 req/min for us and 1000 req/min for Competitor Z.. Passes when: 100% of real cases caught, with 0 false alarms on rows the audit passed.. On a fail: block the merge.
- **Soft gate · Row 5 · Hallucination: lists an unconfirmed speaker as confirmed.** Check: the code-based check, run on the Ascend IQ golden set at Staging. Measures: Share of speaker-list answers that name someone as “confirmed” who isn’t marked confirmed on the agenda (such as Sam Altman, who is only invited).. Passes when: 0%. On a fail: pause the release until the PM signs off on an override.
- **Advisory gate · Row 17 · Tone: slang detected.** Check: the LLM judge, run on the Ascend IQ golden set at Pull Request. Measures: Share of drafted emails that use slang or break the brand voice (confident, professional, expert).. Passes when: 0%. On a fail: post a warning, and don't block.

## Mitigation Plan · Soft Gate

If the soft gate fails on launch day because speaker-list answers name an unconfirmed speaker as confirmed (like Sam Altman, who is only invited), I’d connect the speaker-list feature to a live run of the agenda rule check. If the failure rate goes above 0%, the feature switches itself off. That lets us ship the rest of Ascend IQ on schedule while the check runs on real traffic and collects new failure cases for the golden set.

# Module 4 · Launch Strategy · Section 4.0 Release Criteria

> Repo file `ai-evals/04-eval-gates/lab-2-launch-strategy.md`. Your PRD's release-criteria section: the numeric thresholds, the CI gate policy, and the mitigation lever for the Soft gate.
>
> Fill this with the **Launch Strategy Builder** tool, then **Copy markdown** and paste it over this file. The headings below mirror the tool's output exactly.

## 4.0 Release Criteria

| Severity | Metric | Threshold | Dataset | Method |
|---|---|---|---|---|
| Hard | _…_ | _e.g. = 0%_ | `Ascend_IQ_Logs` | _…_ |
| Soft | _…_ | _e.g. < 2%_ | `Ascend_IQ_Logs` | _[Example Spec]_ |
| Advisory | _…_ | _e.g. tone ≥ 4/5_ | `Ascend_IQ_Logs` | _[Example Spec]_ |

## 4.1 CI Gate Policy

> _Which per-dimension regression blocks the merge vs warns, referencing a regression golden set ≥ 30. Policy is per-dimension — never one blended "quality" number. Use deterministic fixtures/replay, not live model calls._

## 4.2 Mitigation Plan · Soft Gate

**Selected Lever:** _Staged Rollout / Feature Flagging / Beta Labeling / Delay Launch_

> _One sentence: how this lever contains the Soft-gate risk while you ship._
