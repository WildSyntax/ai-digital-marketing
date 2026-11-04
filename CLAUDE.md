# AI Digital Marketing Workspace

This folder runs digital marketing for one brand. There is no application code. Skills in
`.claude/skills/` define each activity, connectors in `.mcp.json` do publishing and research,
and Markdown files under `content/` are the content store and the review queue.

Read `brand/profile.md` before writing anything. Design: `docs/superpowers/specs/2026-11-04-ai-digital-marketing-workspace-design.md`.

## Pipeline

`content/ideas` → `content/drafts/<channel>` → `content/approved/<channel>` → `content/published/<channel>`

## Rules (always apply)

1. Never create or move a file into `content/approved/` or `content/published/` unless the
   owner explicitly says "approve" or "publish" in this chat. Scheduled routines never approve
   or publish.
2. `status` in front matter must match the folder. Move the file and update `status` in the
   same step, using `git mv`.
3. Blog drafts need a `seo_score` before approval. If it is below `seo_threshold` in
   `brand/profile.md`, refuse approval and show the fix list from `reports/seo/`, unless the
   owner says "approve anyway".
4. The publish skill only reads from `content/approved/`.
5. If a connector needed for publishing or a connector write is not connected or a call
   fails: name the connector, leave the file where it is, stop. Never retry a publish call
   (it could double-post). Drafting skills that define a no-connector path (instagram-post,
   youtube-video, topic-ideas) continue without the connector and say so.
6. Never write secrets into this repo. Connectors authenticate via `/mcp`.
7. Commit after each content change: `content(<channel>): <action> <slug>` (topic-ideas is the
   exception: `content(ideas): add <n> ideas <date>`).
8. Never use phrases listed under "Banned words and phrases" in `brand/profile.md`.

## Skills

| Owner says | Skill | Writes to |
|---|---|---|
| "ideas", "topic ideas for <theme>" | topic-ideas | `content/ideas/` |
| "write a blog on <topic or keyword>", "write <idea file>" | blog-post | `content/drafts/blog/` + `reports/seo/` |
| "seo check <file>" | seo-check | `reports/seo/`, updates `seo_score` |
| "linkedin post about <topic>" / "from <blog file>" | linkedin-post | `content/drafts/linkedin/` |
| "instagram post about <topic>" / "from <blog file>" | instagram-post | `content/drafts/instagram/` |
| "youtube video about <topic>" / "from <blog file>" | youtube-video | `content/drafts/youtube/` |
| "repurpose <approved blog file>" | repurpose | the three social draft folders |
| "approve <file> [for <datetime>]" | approval procedure (below) | `content/approved/<channel>/` |
| "publish <file>", "publish all approved" | publish | `content/published/<channel>/` |
| "weekly review" | weekly review procedure (below) | `reports/weekly/` |

## Approval procedure

1. Confirm the file is in `content/drafts/<channel>/`. If not, say where it is and stop.
2. If the body contains `<...>` or `TODO:` placeholders, refuse approval and list them.
3. If `channel: blog`: first re-run seo-check (edits since the last score make it stale), then
   require `seo_score >= seo_threshold`. Otherwise refuse, print the "Fixes" list from
   `reports/seo/<filename>.md`, and stop, unless the owner said "approve anyway".
4. Set `status: approved`. If the owner gave a time, set `scheduled_for` as ISO 8601 with the
   profile timezone offset (e.g. `2026-11-10T09:00:00+05:30`).
5. `git mv` the file to `content/approved/<channel>/`. For a blog, also run
   `grep -l "^source: <old path>" -r content/` and update each referencing file's `source` to
   the new path in the same commit. Commit `content(<channel>): approve <slug>`.
6. Reply with the new path and, for blogs, offer to run repurpose.

## Weekly review procedure

Write `reports/weekly/YYYY-MM-DD.md` containing:
- counts of files per channel in ideas, drafts, approved, published
- every draft: path, title, created date, seo_score if blog
- every approved item: path, scheduled_for
- items whose `published_at` is within the last 7 days, with `published_url`
- blog drafts with `seo_score < seo_threshold`
- ideas older than 30 days (suggest keep or drop)
Commit `docs: weekly review YYYY-MM-DD`.

## Content file format

Filename `YYYY-MM-DD-<slug>.md`. Front matter:

```yaml
---
title: ""
channel: blog | linkedin | instagram | youtube
status: idea | draft | approved | published
keyword: ""
secondary_keywords: []
seo_score: null
created: YYYY-MM-DD
scheduled_for: null
published_url: null
published_at: null
publish_attempted: null
source: null
---
```

`source` is the source blog's path at repurpose time and may go stale when the blog moves;
approval and publish of a blog update every referencing file (see above).

Channel extras, when present: `canva_design_url` and `image_url` (instagram; `image_url` is the
public http(s) URL of the exported PNG that publish uses), `video_file` (youtube), `pillar`
(ideas, carried into blog drafts), `publish_attempted` (ISO datetime set just before a publish
call), `published_at` (ISO datetime set on success).

Body sections per channel are defined in each skill. Channel-specific extras (meta
description, hashtags, image brief, tags, thumbnail brief) are `##` sections in the body.
