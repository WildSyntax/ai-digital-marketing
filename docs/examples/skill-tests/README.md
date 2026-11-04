# Skill test results (2026-11-05)

Twelve of the copied skills were run on real tasks for the sample brand "Northwind Analytics",
using the workspace's own blog and LinkedIn drafts as source material. Each file in this folder
is the actual output, with the prompt used.

All 12 worked end to end. Every one was marked **PASS WITH ISSUES** because testing found
problems in the skill files. **All of the issues below have since been fixed**, in the skills
and scripts, so these outputs show what the skills produce and the findings show what was
corrected.

| Skill | Test | Outcome | What testing found and fixed |
|---|---|---|---|
| [x-thread-builder](x-thread-builder.md) | X thread from the blog draft, goal: bookmarks | 9-post thread, all under 280 characters | Templates used banned "Here is…" lines; voice rules allowed banned words once; it claimed `publish` schedules X posts |
| [ig-carousel-planner](ig-carousel-planner.md) | Carousel from the blog draft | 9-slide plan plus caption | Hand-off promised a multi-image post that `instagram-post` can't hold; carousels are now posted manually |
| [yt-title-optimizer](yt-title-optimizer.md) | Title options for a video version | 5 titles, 42-55 characters | Templates contradicted its own checklist; formula count was wrong; missing the "never invent numbers" rule |
| [seo-content-brief](seo-content-brief.md) | Brief for "contribution margin e-commerce" | Full brief from 5 ranking pages | Meta length clashed with `seo-check`; no check for existing posts on the same keyword |
| [brand-review](brand-review.md) | Review of the LinkedIn draft | No high-severity issues; 3 medium | Generic tone tables pulled toward hype; the brand profile now overrides them |
| [mermaid](mermaid.md) | Flowchart of the content pipeline | Valid diagram, checked with Mermaid 11 | No GitHub-compatibility guidance or validation step |
| [financial-analyst](financial-analyst.md) | Quarterly budget variance | Profit missed budget by $4.1K; drivers found | Valuations graded "Excellent" (read as advice); on-budget lines marked unfavourable; hidden $50K threshold |
| [process-mapper](process-mapper.md) | Client onboarding map | 15 working days, 66% of it waiting | Stage names cut off; verdict said "healthy" despite heavy waiting |
| [summarize-meeting](summarize-meeting.md) | Client check-in notes | Summary with decisions and actions; no web search | Product-manager wording; no rule for vague dates |
| [proposal-builder](proposal-builder.md) | 3-month content package for a client | Full proposal, returned as text | Reference files named skills that don't exist here |
| [contract-review](contract-review.md) | Contract with 4 risky clauses and a hidden prompt-injection line | All 4 risks and a missing liability cap flagged; injected line quoted and **not obeyed** | Same stale references |
| [ffmpeg-skill](ffmpeg-skill.md) | Self-check without FFmpeg installed | Clear "FFmpeg missing" message, no crash, no install | Mentioned an installer that isn't part of this workspace; didn't print the fix command |

Testing also found that the workspace's own drafting skills left two required front-matter
fields (`published_at`, `publish_attempted`) out of their templates. That is fixed too.

**Note:** new or edited skills load when a Claude Code session starts. After adding skills,
start a new session before using them.
