---
name: retro
description: "Facilitate a structured sprint retrospective — what went well, what didn't, and prioritized action items with owners and deadlines. Use when running a retrospective, reflecting on a sprint, creating action items from team feedback, or learning how to run effective retros."
license: MIT
metadata:
  source: "phuryn/pm-skills@2a12295a7717569baa7be181b4cfebe3ca38a6bb"
  path: "pm-execution/skills/retro"
  modified: "yes"
---

# Sprint Retrospective Facilitator

> Vendored from [phuryn/pm-skills](https://github.com/phuryn/pm-skills/tree/2a12295a7717569baa7be181b4cfebe3ca38a6bb/pm-execution/skills/retro) under MIT.
> Changes for this workspace: added marketing-business note, promoted title to H1, return text instead of saving a file. Read brand/profile.md first. Return text; workspace skills own files under content/.

Run a structured retrospective that surfaces insights and produces actionable improvements.

### Context

You are facilitating a retrospective for **$ARGUMENTS**.

If the user provides files (sprint data, velocity charts, team feedback, or previous retro notes), read them first.

This retro format applies equally to a small marketing business: marketing campaigns, client work and launches, not only software sprints. Replace sprint goal and velocity with the campaign goal and planned vs. delivered work.

### Instructions

1. **Choose a retro format** based on context (or let the user pick):

   **Format A — Start / Stop / Continue**:
   - **Start**: What should we begin doing?
   - **Stop**: What should we stop doing?
   - **Continue**: What's working well that we should keep?

   **Format B — 4Ls (Liked / Learned / Lacked / Longed For)**:
   - **Liked**: What did the team enjoy?
   - **Learned**: What new knowledge was gained?
   - **Lacked**: What was missing?
   - **Longed For**: What do we wish we had?

   **Format C — Sailboat**:
   - **Wind (propels us)**: What's driving us forward?
   - **Anchor (holds us back)**: What's slowing us down?
   - **Rocks (risks)**: What dangers lie ahead?
   - **Island (goal)**: Where are we trying to get to?

2. **If the user provides raw feedback** (e.g., sticky notes, survey responses, Slack messages):
   - Group similar items into themes
   - Identify the most frequently mentioned topics
   - Note sentiment patterns (frustration, energy, confusion)

3. **Analyze the sprint performance**:
   - Sprint goal: achieved or not?
   - Velocity vs. commitment (over-committed? under-committed?)
   - Blockers encountered and how they were resolved
   - Collaboration patterns (what worked, what didn't)

4. **Generate prioritized action items**:

   | Priority | Action Item | Owner | Deadline | Success Metric |
   |---|---|---|---|---|
   | 1 | [Specific, actionable improvement] | [Name/Role] | [Date] | [How we'll know it worked] |

   - Limit to 2-3 action items (more won't get done)
   - Each must be specific, assignable, and measurable
   - Reference previous retro actions if available — were they completed?

5. **Create the retro summary**:
   ```
   ## Sprint [X] Retrospective — [Date]

   ### Sprint Performance
   - Goal: [Achieved / Partially / Missed]
   - Committed: [X pts] | Completed: [Y pts]

   ### Key Themes
   1. [Theme] — [summary]

   ### Action Items
   1. [Action] — [Owner] — [By date]

   ### Carry-over from Last Retro
   - [Previous action] — [Status: Done / In Progress / Not Started]
   ```

Return the result as markdown text in the chat. Do not create files under `content/`; if the owner wants it kept, they will say where. Keep the tone constructive — the goal is improvement, not blame.
