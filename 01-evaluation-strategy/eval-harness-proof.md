# First LLM-as-a-Judge Eval, Module 1

## Version A, Concise, system prompt used

You are an executive briefing assistant.
Summarize in exactly 3 bullet points under 60 words. No preamble, no extra text.

## Version B, Narrative, system prompt used

You are a PR communications assistant.
Write a 100-word narrative summary highlighting wins first, then risks and next steps. Keep a positive tone. No bullets.

## Eval setup, dataset name + judge model/family

- Dataset: `Module1Output`, 2 rows (`exec_bullets`, `pr_narrative`), each with system_prompt, input email, and output.
- Starter dataset: 20 synthetic rows (10 good / 10 bad) for calibrating the judge.
- Generator: Claude Opus 5.5 (Anthropic family).
- Judge: [YOUR JUDGE MODEL] ([FAMILY], chosen to avoid self-preference bias).
- Metric: Conciseness, binary (1 = concise and faithful, 0 = not), returned as JSON with a one-sentence reason.

## Cold-start, the prompt you used to seed a starter dataset

Generate 20 example rows for evaluating email-summary quality.
Each row: an input email + a candidate summary + a first-pass label ("good" or "bad") + a one-line reason.
Make roughly half concise/faithful ("good") and half verbose or inaccurate ("bad").
Return it as a markdown table.

## Your definition of good vs bad (golden-set criteria), the graded part, write your own

_…_#	Input email	Candidate summary	Label	Reason
1	Server maintenance this Saturday 2–4 AM; checkout will be unavailable during the window. Please notify the support team.	Checkout down Saturday 2–4 AM for maintenance; notify support.	good	Captures timing, impact, and action concisely.
2	Q3 revenue was $4.2M, up 8% QoQ; churn steady at 3%. Board deck due Oct 20.	Q3 revenue hit $4.8M, up 8%; churn steady; deck due Oct 20.	bad	Revenue figure is wrong ($4.8M vs. $4.2M).
3	The office will be closed Nov 11 for the holiday. Remote work is optional that day.	Office closed Nov 11; remote work optional.	good	Complete and faithful in minimal words.
4	Engineering hiring freeze through Q1; open reqs paused; existing offers will be honored.	This email, which was sent to the team, discusses hiring and explains that there will be a freeze on engineering hiring lasting through the first quarter, meaning open requisitions are paused, though it’s worth noting that offers already extended will still be honored.	bad	Accurate but padded with filler; longer than the source.
5	Vendor contract renewal: price rises 12%; legal review needed by Oct 30; procurement is exploring alternatives.	Vendor renewal up 12%; legal review due Oct 30; procurement weighing alternatives.	good	All three points preserved accurately.
6	Mobile app v3.2 release slipped to Oct 28 due to a payment bug; QA is retesting.	App v3.2 releases Oct 28 as planned.	bad	Misrepresents a delay as on-schedule and omits the bug.
7	Customer satisfaction rose from 78 to 84 after the new onboarding flow. Expanding to enterprise tier next month.	CSAT up 78→84 from new onboarding; enterprise rollout next month.	good	Keeps numbers, cause, and next step.
8	Security training is mandatory; complete by Oct 31. Non-completion will lock account access.	Security training optional this month.	bad	Reverses “mandatory” and drops deadline and consequence.
9	Budget for two contractors approved; they start Nov 3; manager to finalize the SOW.	Two contractors approved to start Nov 3; manager finalizing SOW.	good	Faithful and concise.
10	Website traffic down 10% after a search algorithm update; SEO audit scheduled next week.	Traffic down 10%, likely due to weak content and poor leadership; SEO audit next week.	bad	Invents causes not in the source.
11	Sales kickoff moved from Jan 15 to Jan 22; venue unchanged; please update travel bookings.	Sales kickoff now Jan 22, same venue; update travel.	good	Captures change, constant, and action.
12	Data warehouse migration 70% complete; finance reports may lag one day during the Nov 5 cutover.	Migration 70% done.	bad	Omits the business-impacting cutover delay.
13	Q4 OKR drafts due Friday; use the new template in the shared drive.	Q4 OKR drafts due Friday using the new shared-drive template.	good	Deadline and instruction both kept.
14	Support ticket backlog fell from 1,200 to 450; response time now under 4 hours.	Backlog rose to 1,200; response time under 4 hours.	bad	Reverses the trend and misstates the current backlog.
15	Partner webinar registrations hit 600, exceeding the 400 goal; recording will be shared.	Webinar registrations reached 600 vs. 400 goal; recording to be shared.	good	Accurate and brief.
16	Expense policy update: meal limit raised to $60/day; receipts required over $25; effective Nov 1.	Hi team! Great news, everyone: the expense policy has been updated! To summarize the key points, the meal limit has now been raised to $60 per day, and receipts are going to be required for anything over $25. This all takes effect starting November 1. Thanks!	bad	Facts correct but verbose, with preamble and sign-off.
17	Two of five pilot customers renewed; the remaining three decide by month-end.	2 of 5 pilot customers renewed; other 3 decide by month-end.	good	Faithful with no loss of detail.
18	Laptop refresh: new devices ship Nov 10; return old devices within two weeks of receipt.	New laptops ship Nov 10; keep old devices as backups.	bad	Contradicts the return instruction.
19	Brand guidelines v2 published; old logo files retire Dec 1.	Brand guidelines v2 live; old logo files retire Dec 1.	good	Concise and complete.
20	API outage of 45 minutes on Tuesday; root cause was a config error; postmortem Thursday.	45-minute API outage caused by a cyberattack; postmortem Thursday.	bad	Fabricates the root cause.

## Screenshots, links or repo paths (optional if you followed the demo)

_…_
