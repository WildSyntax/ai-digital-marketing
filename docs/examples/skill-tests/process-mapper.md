# process-mapper test
Prompt: "Map our client onboarding process."
Date: 2026-11-05
Result: PASS WITH ISSUES

Test setup: the skill was loaded by reading `.claude/skills/process-mapper/SKILL.md`, because the Skill tool returned `Unknown skill` in this session. The input JSON is at
`/private/tmp/claude-501/-Users-himanshu25--claude-spares-spare-97jvgk/c9aef6d1-9353-4a3b-9c65-8ef1b46a10b1/scratchpad/tests/northwind_client_onboarding.json`.

The skill's five forcing questions (SKILL.md lines 104-126) were answered by the tester for Northwind:
1. Measured or estimated? Estimates. The owner's averages are used as P50s, and the P90s are tester estimates. All are labelled as estimates.
2. As-is or to-be? As-is.
3. Handoffs and their waits? Owner to client after kickoff (intake form, about 5 days, often late). Owner to client after the draft (review, 3 days). Client to owner after each.
4. Batch size? 1 client at a time, with about 3 clients onboarding at once (WIP = 3).
5. Rework rate? 30% of clients need a second review round (a half-day revision plus another 3-day review).

Modelling choices: time is in business minutes (1 working day = 480 min). "Signed proposal" is the trigger, not a stage. The scripts have no field for how likely a stage is, so the 30% loop is entered as expected values (P50 = 30% of the loop) and the full loop is the P90.

Commands run (from `.claude/skills/process-mapper/`), all exit 0 with no errors:
```
python3 scripts/process_documenter.py  --input <scratch>/northwind_client_onboarding.json
python3 scripts/bottleneck_detector.py --input <scratch>/northwind_client_onboarding.json --profile services
python3 scripts/cycle_time_analyzer.py --input <scratch>/northwind_client_onboarding.json --profile services
```

---

## Process map: Northwind client onboarding (as-is)

Trigger: proposal signed. End: first content batch delivered. Figures are estimates, not measured.

### Swim lanes (script output, stage names cut to 32 characters by the script)

```
+----------------------+------------------------------------------------------------------------+
| OWNER                | STAGES (in process order)                                              |
+----------------------+------------------------------------------------------------------------+
| Owner                | #1 [W] Wait for kickoff call slot (p50=960m) -> #2 [V] Kickoff call    |
|                      | (p50=60m) -> #4 [V] Draft brand profile (p50=480m) -> #6 [R] Revise    |
|                      | brand profile (30% of cli (p50=72m) -> #8 [V] Produce first content    |
|                      | batch (p50=1440m)                                                      |
+----------------------+------------------------------------------------------------------------+
| Client               | #3 [W] Client completes brand intake fo (p50=2400m) -> #5 [W] Client   |
|                      | reviews brand profile (p50=1440m) -> #7 [R] Second client review (30%  |
|                      | of cli (p50=432m)                                                      |
+----------------------+------------------------------------------------------------------------+
```
Legend: `[V]` value-add, `[W]` wait, `[R]` rework

### Steps in order, with handoffs

| # | Stage | Owner | Type | P50 | P90 (est.) | Handoff |
|---|---|---|---|---|---|---|
| 1 | Wait for kickoff call slot | Owner | wait | 2 days | 4 days | |
| 2 | Kickoff call | Owner | value-add | 1 h | 1.5 h | Owner to client |
| 3 | Client completes brand intake form | Client | wait | 5 days | 10 days | Client to owner |
| 4 | Draft brand profile | Owner | value-add | 1 day | 1.5 days | Owner to client |
| 5 | Client reviews brand profile | Client | wait | 3 days | 5 days | 70%: to step 8. 30%: to step 6 |
| 6 | Revise brand profile (30% of clients) | Owner | rework | 0.15 day expected | 0.5 day | Owner to client |
| 7 | Second client review (30% of clients) | Client | rework | 0.9 day expected | 3 days | Client to owner |
| 8 | Produce first content batch | Owner | value-add | 3 days | 4 days | End |

Four handoffs on the main path, plus two more for the 30% who need a second round.

### Cycle time (services profile)

| Metric | Value |
|---|---|
| Total P50 | 7,284 min = about 15 working days (3 weeks) |
| Total P90 | 13,530 min = about 28 working days (5.5 weeks) |
| Value-add time | 4.1 days (27.2%) |
| Waiting time | 10 days (65.9%) |
| Rework time (expected) | 1.05 days (6.9%) |
| Throughput (Little's Law, WIP 3) | 0.025 clients per working hour = about 1 client every 5 working days |
| Script verdict | HEALTHY (VA% above the 20% services band) |

The HEALTHY verdict depends on counting the whole 1-day draft and 3-day content batch as value-add time. If those days are partly waiting in the queue too, VA% falls quickly. Two-thirds of the elapsed time is spent waiting.

### Bottlenecks (ranked by script)

1. **[MEDIUM] Waiting dominates (R2).** Wait stages are 66% of P50, above the 50% services threshold. That is 10 of about 15 days.
2. **[MEDIUM] Slow stage: client completes brand intake form (R1).** 5 days P50, 3.6 times the average value-add step, and the widest P50-to-P90 spread (5 to 10 days). The owner says it is often late.

### Recommendation (one constraint)

The constraint is **step 3, the brand intake form**. It is the longest single wait, it is the least predictable, and nothing downstream can start until it is back. Following the skill's rule, change only this step first. Fill the intake form together during the kickoff call, with the call booked for 90 minutes instead of 60. If that removes most of the 5-day wait, onboarding drops from about 3 weeks to about 2 at P50 and saves about 5 working days at P90.

Do not speed up the content batch or the drafting yet. Faster owner work does not help while the client queue is the long pole. Look at the kickoff scheduling wait (2 days) and the 30% second-review rate after step 3 is fixed. A better intake answer set may also cut the second-round rate.

To turn this into an SOP or checklist, hand this map to the `process-doc` skill.

---

## Tester's judgement

The skill worked end to end. All three scripts ran without errors on the owner-supplied steps, and the result named one constraint, as the skill intends. The never-invent-durations rule (line 40) was useful: it led to the P90s being labelled as estimates.

Issues:
1. **Stage names cut off in the swim lane.** `scripts/process_documenter.py` line 152 uses `s['name'][:32]`, which produces "Client completes brand intake fo" and "Revise brand profile (30% of cli". Fix: wrap long names instead of truncating them, or raise the limit to about 60 since the table wraps anyway.
2. **No way to enter a probability for a rework loop.** The schema in `assets/process_template.md` and the docstring at the top of `scripts/process_documenter.py` (lines 11-25) has no `probability` / `loop_to` field, so "30% need a second round" had to be faked as expected-value P50s. The swim lane draws it as a straight line, not a loop. Fix: add an optional `probability` (0-1) per stage, and have `cycle_time_analyzer.py` (lines 57-61) and `bottleneck_detector.py` (lines 89-93) weight P50 by it. Until then, add a note to SKILL.md step 1 (line 42) explaining how to enter partial rework.
3. **Handoffs not shown.** The SKILL.md description and line 43 promise that cross-functional handoffs "become visible", but the swim lane lists each owner's stages in a row with no arrows between lanes, so the owner-to-client handoffs are hard to see. The handoff column above was added by hand. Fix: in `render_markdown` (process_documenter.py around lines 114-160), list each owner change ("#2 Owner -> #3 Client") under the lanes.
4. **The thresholds in SKILL.md do not match the scripts.** SKILL.md lines 44 and 55 say "VA% > 25% = HEALTHY, 10-25% = TYPICAL", but `cycle_time_analyzer.py` lines 24-29 use 20% / 8% for `services`. This matters here: at 27.2% Northwind is HEALTHY on either band, but a 22% process would be HEALTHY to the script and TYPICAL by the docs. Fix: state in SKILL.md that the bands depend on the profile, and list them.
5. **The order of the scripts is inconsistent.** Workflow steps 2-4 (lines 43-45) run documenter, then cycle-time, then bottleneck. Line 126 says documenter, then bottleneck, then cycle-time. Harmless, but pick one.
6. **A HEALTHY verdict alongside a wait-time finding is confusing.** The cycle-time verdict says HEALTHY while the detector flags 66% waiting. Fix: in `cycle_time_analyzer.py`, add a caution to the verdict when the wait ratio is above the profile's `wait_share_max`, or explain in SKILL.md step 5 (line 46) how to read the two together.
7. **Throughput in items per hour is awkward for multi-week processes.** It came out as 0.025/hour. Fix: also print items per day or per week (`cycle_time_analyzer.py` line 146).
8. **Skill not registered in this session.** The Skill tool returned `Unknown skill: process-mapper`. This is probably a stale session skill list. Check it in a fresh session.

No banned phrases in the output.
