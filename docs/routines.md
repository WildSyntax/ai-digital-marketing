# Scheduled routines (cloud)

Two Claude Code cloud routines run against this repository. They were defined on 2026-11-04 but
creation returned `github_token_missing` from this session even after GitHub was connected on
claude.ai, so create them from https://claude.ai/code/routines (or ask Claude Code in a fresh,
freshly signed-in session to "create the two routines in docs/routines.md").

Common settings: environment `Default` (anthropic_cloud), model `claude-sonnet-5-5`,
repository `https://github.com/WildSyntax/ai-digital-marketing`. Times are UTC; the owner is
in Asia/Calcutta (UTC+5:30).

## 1. marketing-topic-ideas

- Cron: `30 3 * * 1` (Monday 09:00 Asia/Calcutta)
- Tools: Bash, Read, Write, Edit, Glob, Grep, WebSearch, WebFetch
- Prompt:

> You are running the weekly topic-ideas routine for the AI digital marketing workspace in this repository. First read CLAUDE.md, brand/profile.md, brand/keywords.md, and .claude/skills/topic-ideas/SKILL.md. Then follow the topic-ideas skill for all keyword clusters (no theme filter): research with WebSearch, generate 5-10 new blog ideas, deduplicate against every existing file under content/ (ignore docs/examples/), and write one idea file per idea into content/ideas/ using the skill's template with today's date. Commit the new files with the message format `content(ideas): add <n> ideas <YYYY-MM-DD>` ending with the line `Co-Authored-By: Claude Code Routine <noreply@anthropic.com>`. Create and push a branch named ideas/<YYYY-MM-DD> and open a pull request against main titled `Topic ideas <YYYY-MM-DD>` whose body lists each idea's title, keyword, and pillar. Rules: never create, move, or edit anything under content/approved/ or content/published/; never run the publish skill; never modify CLAUDE.md, the skills, or brand/. If brand/profile.md still contains only `Example:` placeholder values, proceed anyway but say so in the PR body. If web search is unavailable, write ideas from the keyword clusters alone and note that in each file's Sources section and in the PR body.

## 2. marketing-weekly-review

- Cron: `30 10 * * 5` (Friday 16:00 Asia/Calcutta)
- Tools: Bash, Read, Write, Edit, Glob, Grep
- Prompt:

> You are running the Friday weekly-review routine for the AI digital marketing workspace in this repository. First read CLAUDE.md in full, especially the section titled `Weekly review procedure`, and brand/profile.md for `seo_threshold`. Then follow that procedure exactly: read the front matter of every Markdown file under content/ (ignore docs/examples/) and write reports/weekly/<YYYY-MM-DD>.md with today's date containing every item the procedure lists: counts per channel per stage (ideas, drafts, approved, published); every draft with path, title, created date, and seo_score for blogs; every approved item with scheduled_for; items published in the last 7 days (by published_at) with published_url; blog drafts with seo_score below the threshold; ideas older than 30 days with a keep-or-drop suggestion. Write `none` for any empty section. End the report with a short `What to do next` list (items awaiting approval, approved items not yet scheduled or published, stale ideas). Commit it with the message `docs: weekly review <YYYY-MM-DD>` ending with the line `Co-Authored-By: Claude Code Routine <noreply@anthropic.com>`. Create and push a branch named review/<YYYY-MM-DD> and open a pull request against main titled `Weekly review <YYYY-MM-DD>` whose body is the report's counts table and the What-to-do-next list. Rules: this routine only reads content/ and writes the one report file; never create, move, or edit anything under content/; never run the publish skill; never modify CLAUDE.md, the skills, or brand/.

Routines never approve or publish. Merge their PRs to accept the ideas or the report.
