---
name: process-mapper
description: "Maps an existing business process: its steps, the owner of each step, the handoffs between owners, and where work waits or loops back (bottlenecks, wait time, rework). Use when the owner wants to see how a process really runs, find out why it is slow, or locate where handoffs drop work. Produces a swim-lane map, cycle-time figures and a ranked bottleneck list; it does not write SOPs. Its output can feed the workspace `process-doc` skill, which writes the SOP, RACI or runbook."
license: MIT
metadata:
  source: "alirezarezvani/claude-skills@c85b17e1fb621ba760478baaacc4fcb9be225e74"
  path: "business-operations/skills/process-mapper"
  modified: "yes"
  version: 2.8.0
  author: claude-code-skills
  tags: [bizops, process, bpmn, bottleneck, cycle-time, lean, six-sigma, value-stream]
---

# process-mapper

> Vendored from [alirezarezvani/claude-skills](https://github.com/alirezarezvani/claude-skills/tree/c85b17e1fb621ba760478baaacc4fcb9be225e74/business-operations/skills/process-mapper) under MIT. needs: python3 (standard library only, no packages).
> Changes for this workspace: description narrowed to mapping a process (steps, owners, handoffs, bottlenecks), with a hand-off to `process-doc` for SOPs; references to sibling skills and the `/cs-grill-bizops` command in the source repo made optional; quick-example path fixed; added a never-invent-durations rule and a no-writes-under-content/ rule; swim-lane stage names no longer cut at 32 characters; cycle-time verdict now carries a caution when wait share exceeds the profile's wait limit; throughput also shown per day and per week (`--hours-per-day`, `--days-per-week`); VA% bands documented per `--profile` and script order made consistent; noted that rework loops must be entered as expected-value durations. Read brand/profile.md first. Return text; workspace skills own files under content/.

BPMN-style business process mapping, bottleneck detection, and cycle-time analysis for internal-operations leaders.

## Purpose

Internal-operations work suffers from three recurring failure modes:

1. **Implicit process** — the steps exist only in tribal knowledge, so handoffs drop and onboarding takes weeks.
2. **Invisible waiting** — most of the elapsed time on any business process is queue / wait / approval time, not actual work; teams optimize the wrong stage.
3. **Local optimization** — Goldratt's Theory of Constraints is ignored; resources are added to non-constraint stages, gaining nothing.

This skill produces a process map, identifies where work waits, and points the constraint out by name with deterministic logic — not LLM intuition.

## When to use

- Mapping a business process (procurement intake, vendor onboarding, employee onboarding, incident handoff, expense reimbursement, customer onboarding, claims adjudication).
- An existing process is "too slow" but nobody can name the bottleneck.
- Cycle time is being measured but value-add ratio is not — so the team can't tell whether the process is healthy or waste-heavy.
- Cross-functional handoffs are dropping work and root cause is unclear.

## Workflow

Five-step deterministic flow. Work only from step names, owners and durations the owner gives you. If durations are unknown, ask for rough P50 / P90 estimates and label them as estimates; never invent them. Write the input JSON outside `content/` (for example a scratch or temp folder) and print results to stdout. Do not pass `--output` with a path under `content/`.

1. **Intake.** Capture the process as a JSON file with one entry per stage: `name`, `owner`, `type` (`value-add` | `wait` | `rework`), `duration_minutes_p50`, `duration_minutes_p90`. Use `assets/process_template.md` and its JSON skeleton.
2. **Map stages.** Run `process_documenter.py` to produce an ASCII swim-lane diagram + a normalized JSON artifact. The swim-lane separates lanes by owner so cross-functional handoffs become visible.
3. **Measure cycle time.** Run `cycle_time_analyzer.py` with the appropriate `--profile` (saas / services / manufacturing / healthcare) to compute total P50, total P90, value-add ratio (VA%), and a Little's-Law throughput estimate. The HEALTHY / TYPICAL / WASTE-HEAVY bands depend on `--profile`; see the table under Scripts.
4. **Detect bottlenecks.** Run `bottleneck_detector.py` with the same `--profile`. Output is a ranked list with severity (CRITICAL / HIGH / MEDIUM), root-cause hypothesis, and one recommended action per finding.
5. **Recommend.** Pair the bottleneck list with the cycle-time verdict; recommend a single constraint-focused intervention per Goldratt's "subordinate everything to the constraint" rule. Don't recommend optimization of a non-constraint stage.
6. **Hand off (optional).** Return the map, figures and findings as text. If the owner wants the process written up as an SOP, RACI or runbook, pass this output to the workspace `process-doc` skill.

## Scripts

**`scripts/process_documenter.py`** — Reads a process JSON, validates it, and emits a text-based BPMN-style swim-lane diagram in Markdown (lanes by owner, stages annotated with type + duration). Also outputs a normalized JSON artifact for downstream tools. Stdlib only. `--sample` prints a 6-stage procurement-intake example.

**`scripts/bottleneck_detector.py`** — Applies three deterministic detection rules: (a) stage P50 > 2× mean of value-add stages, (b) wait-state % > 40% of total cycle, (c) rework % > 15%. Thresholds adjust by `--profile` because SaaS, services, manufacturing, and healthcare have different "normal" wait ratios. Output is a ranked list with severity, hypothesis, action.

**`scripts/cycle_time_analyzer.py`** — Computes total P50 and P90 cycle time, value-add ratio (VA%), wait %, rework %, and a Little's-Law throughput estimate (WIP / cycle time) per hour, day and week. Per-day and per-week figures default to 24-hour days and 7-day weeks; if durations are business minutes, pass `--hours-per-day 8 --days-per-week 5`. Verdict bands depend on `--profile` (default `saas`); TYPICAL is where most non-manufacturing processes land. If wait share is above the profile's wait limit (the same limit `bottleneck_detector.py` uses), the verdict adds a caution such as "HEALTHY flow, but waiting is 66% of lead time".

| `--profile` | HEALTHY (VA%) | TYPICAL (VA%) | WASTE-HEAVY (VA%) | Wait limit |
|-------------|---------------|---------------|-------------------|------------|
| saas (default) | ≥ 25% | 10–25% | < 10% | 40% |
| services | ≥ 20% | 8–20% | < 8% | 50% |
| manufacturing | ≥ 35% | 15–35% | < 15% | 30% |
| healthcare | ≥ 20% | 8–20% | < 8% | 55% |

## Quick example

```bash
# Run from this skill's folder: .claude/skills/process-mapper/
# Renders a BPMN-style swim-lane diagram for the built-in 6-stage procurement-intake demo (fictional data)
python3 scripts/process_documenter.py --sample

# On the owner's process (input JSON written outside content/)
python3 scripts/process_documenter.py  --input /path/to/process.json
python3 scripts/cycle_time_analyzer.py --input /path/to/process.json --profile services
python3 scripts/bottleneck_detector.py --input /path/to/process.json --profile services
```

Note the flag names: in `process_documenter.py`, `--format` picks markdown/json and `--output` is a file path. In the other two scripts, `--output` picks markdown/json and nothing is written to disk.

## References

- `references/lean_six_sigma_canon.md` — TIMWOOD wastes, value-stream mapping, Theory of Constraints, Kanban WIP, Little's Law. Cites Womack & Jones, Rother & Shook, Goldratt, Ohno, Liker, Pyzdek, Anderson.
- `references/bpmn_essentials.md` — Pools, lanes, gateways, events, message flows, common notation mistakes. Cites the OMG BPMN 2.0 spec, Silver, Allweyer, Freund/Rücker, OASIS, ISO/IEC 19510:2013.
- `references/bottleneck_anti_patterns.md` — Seven specific anti-patterns drawn from Goldratt, Kim et al., Spear, DORA, Deming, and process-mining research.

## Assumptions

1. The user can provide stage-level cycle-time data (even rough P50 / P90 estimates). If they cannot, the first step is to instrument the process — not to map it.
2. "Process" here means a repeatable business workflow with discrete stages, not a one-off project.
3. The user has authority to act on bottlenecks (or can route findings to someone who does). Without that, the output is academic.
4. Stage `type` is honest: a "value-add" stage labeled as such by the user really does change the work product from the customer's perspective. Mis-labelling waiting as value-add is the most common data-quality failure.

## Limitations

- The scripts model a straight sequence with no branch probabilities: rework loops must be entered as expected-value durations (for example, a 2-day revision that 30% of clients need is entered as 0.3 × 2 days).

## Anti-patterns

- **Mapping every process at once.** Pick one. Goldratt: the constraint is a single point.
- **Optimizing the non-constraint.** If stage 4 is the bottleneck, speeding up stage 2 just builds inventory in front of stage 4. Subordinate everything to the constraint.
- **Mistaking total cycle time for processing time.** They are almost never the same; VA% reveals the gap.
- **Adding people to a wait-bound process.** Wait time is not solved by more headcount; it's solved by removing the handoff or batch.
- **Treating rework as a separate problem.** Rework loops belong in the process map. Hiding them understates true cycle time.

## Distinct from

- **`process-doc` (this workspace)** — writes SOPs, RACI matrices and runbooks. Process-mapper maps and measures the process; process-doc documents it. Map first, then hand the result to process-doc if a written procedure is needed.
- **Sales, marketing or customer-funnel work** — process-mapper is *internal* operations, not external funnel conversion.
- **System reliability (SLOs, uptime)** — process-mapper measures *business-process* cycle time, not system uptime.
- **Ticket tracking** — process-mapper is process *design*, not ticket *tracking*.

(The source repo pairs this skill with sibling skills that are not vendored here, such as business-growth, slo-architect, c-level-advisor and project-management skills. They are optional and not required.)

## Forcing-question library

Before invoking the tools, walk the owner through these questions **one at a time, with a recommended answer + canon citation**. Never bundled.

1. **"Do you have measured cycle times for the top-3 longest stages, or only estimates?"**
   Recommended: insist on measured data.
   Canon: Goldratt 1984 (*The Goal*) — optimizing estimated bottlenecks reliably attacks the wrong constraint.

2. **"Are you mapping the *current* process (as-is) or the *intended* process (to-be)?"**
   Recommended: map as-is first. To-be after bottleneck is identified.
   Canon: Rother & Shook 1999 (*Learning to See*) — value-stream mapping starts with the current state, always.

3. **"Where do handoffs occur between teams, and how long does each handoff wait?"**
   Recommended: log every handoff with median wait time.
   Canon: Reinertsen 2009 (*Principles of Product Development Flow*) — wait time at handoffs is the largest invisible cost.

4. **"What's your batch size at each stage?"**
   Recommended: drive batch size toward 1 wherever possible.
   Canon: Anderson 2010 (*Kanban*) — batch size correlates 1:1 with cycle time variance.

5. **"What's the rework rate per stage?"**
   Recommended: surface it explicitly; rework loops belong in the map.
   Canon: Pyzdek (*Six Sigma Handbook*) — hidden rework drives 30-50% of total cycle time in service processes.

Walk depth-first. Don't open question 4 before 1-3 are answered. If the owner has no measured data, accept estimates and label them as such. After all 5 are answered, invoke `process_documenter.py` → `cycle_time_analyzer.py` → `bottleneck_detector.py` in sequence (the same order as the Workflow).
