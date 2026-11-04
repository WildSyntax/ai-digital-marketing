---
name: status-report
description: Generate a status report with KPIs, risks, and action items. Use when writing a weekly or monthly update for leadership, summarizing project health with green/yellow/red status, surfacing risks and decisions that need stakeholder attention, or turning a pile of project tracker activity into a readable narrative.
argument-hint: "[weekly | monthly | quarterly] [project or team]"
license: Apache-2.0
metadata:
  source: "anthropics/knowledge-work-plugins@d900840716eb262e1feb17c6f4406c9ce0e06bcf"
  path: "operations/skills/status-report"
  modified: "yes"
---

# /status-report

> Vendored from [anthropics/knowledge-work-plugins](https://github.com/anthropics/knowledge-work-plugins/tree/d900840716eb262e1feb17c6f4406c9ce0e06bcf/operations/skills/status-report) under Apache-2.0.
> Changes for this workspace: CONNECTORS.md copied into references/; risk-assessment skill reference replaced (not vendored); "post to a channel" replaced with returning text. Read brand/profile.md first. Return text; workspace skills own files under content/.

> If you see unfamiliar placeholders or need to check which tools are connected, see [CONNECTORS.md](references/CONNECTORS.md). If no such connector is connected, ask the owner to paste the data.

Generate a polished status report for leadership or stakeholders. Rate each risk by likelihood and impact (high, medium, low) to set its severity.

## Usage

```
/status-report $ARGUMENTS
```

## Output

```markdown
## Status Report: [Project/Team] — [Period]
**Author:** [Name] | **Date:** [Date]

### Executive Summary
[3-4 sentence overview — what's on track, what needs attention, key wins]

### Overall Status: 🟢 On Track / 🟡 At Risk / 🔴 Off Track

### Key Metrics
| Metric | Target | Actual | Trend | Status |
|--------|--------|--------|-------|--------|
| [KPI] | [Target] | [Actual] | [up/down/flat] | 🟢/🟡/🔴 |

### Accomplishments This Period
- [Win 1]
- [Win 2]

### In Progress
| Item | Owner | Status | ETA | Notes |
|------|-------|--------|-----|-------|
| [Item] | [Person] | [Status] | [Date] | [Context] |

### Risks and Issues
| Risk/Issue | Impact | Mitigation | Owner |
|------------|--------|------------|-------|
| [Risk] | [Impact] | [What we're doing] | [Who] |

### Decisions Needed
| Decision | Context | Deadline | Recommended Action |
|----------|---------|----------|--------------------|
| [Decision] | [Why it matters] | [When] | [What I recommend] |

### Next Period Priorities
1. [Priority 1]
2. [Priority 2]
3. [Priority 3]
```

## If Connectors Available

If **~~project tracker** is connected:
- Pull project status, completed items, and upcoming milestones automatically
- Identify at-risk items and overdue tasks

If **~~chat** is connected:
- Scan recent team discussions for decisions and blockers to include
- Never post the report. Return the text. The owner posts it, or the workspace `publish` skill schedules approved content via Metricool.

If **~~calendar** is connected:
- Reference key meetings and decisions from the reporting period

## Tips

1. **Lead with the headline** — Busy leaders read the first 3 lines. Make them count.
2. **Be honest about risks** — Surfacing issues early builds trust. Surprises erode it.
3. **Make decisions easy** — For each decision needed, provide context and a recommendation.
