# AI Digital Marketing Workspace Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a no-code Claude Code workspace that drafts, SEO-checks, approves, and publishes blog, LinkedIn, Instagram, and YouTube content for one brand through skills and MCP connectors.

**Architecture:** Claude is the engine. `CLAUDE.md` is the operating manual, one `SKILL.md` per activity lives in `.claude/skills/`, `.mcp.json` declares remote MCP connectors (Metricool, Canva, vidIQ), and Markdown files under `content/` are the content store and the review queue (`ideas → drafts → approved → published`).

**Tech Stack:** Claude Code (skills, `.mcp.json`, built-in WebSearch/WebFetch), Git, Markdown with YAML front matter. No application code.

## Global Constraints

- No Python or other application code anywhere in the repo.
- Never create or move a file into `content/approved/` or `content/published/` unless the owner explicitly says "approve" or "publish" in chat.
- A content file's `status` front matter must always match its folder.
- The publish skill only reads from `content/approved/`.
- No secrets in the repo; connectors authenticate through Claude Code's `/mcp` flow.
- Blog approval requires `seo_score >= seo_threshold` (default 70) unless the owner says "approve anyway".
- Content filenames: `YYYY-MM-DD-<slug>.md`, slug lowercase, hyphen-separated, contains the primary keyword where possible.
- Commit after every task and every content change: `content(<channel>): <action> <slug>` for content, conventional `feat:`/`docs:` otherwise. Every commit message ends with `Co-Authored-By: Claude Fable 5.1 <noreply@anthropic.com>`.
- Spec: `docs/superpowers/specs/2026-11-04-ai-digital-marketing-workspace-design.md`.

---

## File map

| Path | Responsibility |
|---|---|
| `CLAUDE.md` | Operating manual: pipeline, rules, skill table, approval and weekly-review procedures, content format |
| `.mcp.json` | Connector declarations (Metricool, Canva, vidIQ) |
| `docs/connectors.md` | Optional connectors and how to enable them (Typefully, WordPress.com, Notion, Webflow, OpenSEO) |
| `.gitignore` | Ignore OS and editor junk |
| `brand/profile.md` | Brand voice, audience, pillars, banned phrases, CTAs, cadence, `seo_threshold` |
| `brand/keywords.md` | Keyword clusters |
| `brand/examples/README.md` | Where to drop sample posts in the owner's voice |
| `content/{ideas,drafts,approved,published}/...` | Content queue folders |
| `reports/seo/`, `reports/weekly/` | SEO reports and weekly reviews |
| `.claude/skills/seo-check/SKILL.md` | On-page SEO scoring |
| `.claude/skills/blog-post/SKILL.md` | Research, outline, draft, self-check |
| `.claude/skills/linkedin-post/SKILL.md` | LinkedIn draft |
| `.claude/skills/instagram-post/SKILL.md` | Instagram caption, hashtags, Canva brief/design |
| `.claude/skills/youtube-video/SKILL.md` | YouTube title, description, tags, script, thumbnail brief |
| `.claude/skills/repurpose/SKILL.md` | Approved blog → three social drafts |
| `.claude/skills/topic-ideas/SKILL.md` | Weekly topic suggestions |
| `.claude/skills/publish/SKILL.md` | Push approved items through connectors |

---

### Task 1: Workspace skeleton, brand files, CLAUDE.md

**Files:**
- Create: `.gitignore`, `CLAUDE.md`, `brand/profile.md`, `brand/keywords.md`, `brand/examples/README.md`
- Create: `content/ideas/.gitkeep`, `content/{drafts,approved,published}/{blog,linkedin,instagram,youtube}/.gitkeep`, `reports/seo/.gitkeep`, `reports/weekly/.gitkeep`

**Interfaces:**
- Produces: `brand/profile.md` fields read by every skill: `seo_threshold`, `tone`, `audience`, `pillars`, `banned_phrases`, `cta` per channel, `canva_template` name, `site_domain`. Front matter schema in `CLAUDE.md` used by every skill.

- [ ] **Step 1: Create folders**

```bash
mkdir -p brand/examples content/ideas reports/seo reports/weekly .claude/skills
for s in drafts approved published; do for c in blog linkedin instagram youtube; do mkdir -p content/$s/$c; touch content/$s/$c/.gitkeep; done; done
touch content/ideas/.gitkeep reports/seo/.gitkeep reports/weekly/.gitkeep
```

- [ ] **Step 2: Write `.gitignore`**

```
.DS_Store
Thumbs.db
*.swp
.idea/
.vscode/
```

- [ ] **Step 3: Write `brand/profile.md`** (owner replaces every `Example:` value)

```markdown
---
brand_name: "Example: Northwind Analytics"
site_domain: "example.com"
seo_threshold: 70
canva_template: ""          # name of a Canva brand template for Instagram posts, if any
timezone: "Asia/Kolkata"
---

# Brand profile

Every skill reads this file first. Replace each "Example:" value with your own.

## One-line description
Example: Northwind Analytics helps small e-commerce teams turn their store data into weekly decisions.

## Audience
Example: Founders and marketing leads at e-commerce businesses with 2–20 staff. Busy, practical, not data scientists.

## Tone
Three adjectives: Example: clear, confident, warm.
Example sentence in our voice: "You don't need a data team to know which products are quietly losing you money. You need one report, read once a week."

Avoid: hype, jargon, exclamation marks, emojis in blog posts (emojis allowed sparingly on Instagram).

## Content pillars
1. Example: Reading store data without a data team
2. Example: Pricing and margin decisions
3. Example: Marketing attribution for small budgets
4. Example: Tools and workflows we actually use

## Banned words and phrases
- "game-changer"
- "unlock"
- "in today's fast-paced world"
- "delve"
- "leverage" (as a verb)

## Default calls to action
- blog: "Example: Want this done for you? Book a free 20-minute data review at example.com/review."
- linkedin: "Example: If this was useful, follow for one practical data tip a week."
- instagram: "Example: Save this for your next planning session."
- youtube: "Example: Subscribe for one practical walkthrough every week."

## Posting cadence
- blog: 1 per week
- linkedin: 3 per week
- instagram: 2 per week
- youtube: 1 per two weeks

## Blog defaults
- Target length: 1200–2000 words
- Always include: a short intro that states the problem, H2 sections, a FAQ section when the topic has common questions, and the blog CTA at the end.
```

- [ ] **Step 4: Write `brand/keywords.md`**

```markdown
# Keyword clusters

Replace with your own. Each cluster has a head keyword and related long-tail phrases.
topic-ideas and blog-post pick from here.

## Cluster: Example: e-commerce analytics
- head: "e-commerce analytics"
- long-tail: "e-commerce analytics for small business", "how to read shopify analytics", "e-commerce kpis to track weekly"

## Cluster: Example: product margin
- head: "product margin analysis"
- long-tail: "how to calculate product margin", "which products are losing money", "contribution margin e-commerce"

## Cluster: Example: marketing attribution
- head: "marketing attribution small business"
- long-tail: "last click vs first click attribution", "attribution without a data team", "utm tracking basics"
```

- [ ] **Step 5: Write `brand/examples/README.md`**

```markdown
# Voice examples

Drop 3–5 posts or articles you have written and like into this folder as `.md` files,
one per file. Skills read them to match your voice. Name them by channel, e.g.
`linkedin-1.md`, `blog-1.md`.
```

- [ ] **Step 6: Write `CLAUDE.md`**

```markdown
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
5. If a connector is not connected or a call fails: name the connector, leave the file where
   it is, stop. Never retry a publish call (it could double-post).
6. Never write secrets into this repo. Connectors authenticate via `/mcp`.
7. Commit after each content change: `content(<channel>): <action> <slug>`.
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
2. If `channel: blog`: require `seo_score >= seo_threshold`. Otherwise refuse, print the
   "Fixes" list from `reports/seo/<filename>.md`, and stop, unless the owner said
   "approve anyway".
3. Set `status: approved`. If the owner gave a time, set `scheduled_for` as ISO 8601 with the
   profile timezone offset (e.g. `2026-11-10T09:00:00+05:30`).
4. `git mv` the file to `content/approved/<channel>/`, commit `content(<channel>): approve <slug>`.
5. Reply with the new path and, for blogs, offer to run repurpose.

## Weekly review procedure

Write `reports/weekly/YYYY-MM-DD.md` containing:
- counts of files per channel in ideas, drafts, approved, published
- every draft: path, title, created date, seo_score if blog
- every approved item: path, scheduled_for
- items published in the last 7 days with `published_url`
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
source: null
---
```

Body sections per channel are defined in each skill. Channel-specific extras (meta
description, hashtags, image brief, tags, thumbnail brief) are `##` sections in the body.
```

- [ ] **Step 7: Verify**

Run: `find . -path ./.git -prune -o -type f -print | sort`
Expected: the 5 brand/root files plus 15 `.gitkeep` files (1 ideas + 12 channel folders + 2 reports), and the spec and plan.

Run: `grep -c "seo_threshold" brand/profile.md CLAUDE.md`
Expected: `brand/profile.md:1` and `CLAUDE.md:3` or more (non-zero both).

- [ ] **Step 8: Commit**

```bash
git add -A
git commit -m "feat: workspace skeleton, brand profile, operating manual

Co-Authored-By: Claude Fable 5.1 <noreply@anthropic.com>"
```

---

### Task 2: Connector configuration

**Files:**
- Create: `.mcp.json`, `docs/connectors.md`

**Interfaces:**
- Produces: MCP server names `metricool`, `canva`, `vidiq`. Skills refer to tools as `metricool: createScheduledPost`, `metricool: getBestTimeToPostByNetwork`, `metricool: getBrandSettings`, `canva: search-designs`, `canva: get-design`, `vidiq: vidiq_keyword_research`.

- [ ] **Step 1: Write `.mcp.json`**

```json
{
  "mcpServers": {
    "metricool": {
      "type": "http",
      "url": "https://ai.metricool.com/mcp"
    },
    "canva": {
      "type": "http",
      "url": "https://mcp.canva.com/mcp"
    },
    "vidiq": {
      "type": "http",
      "url": "https://mcp.vidiq.com/mcp"
    }
  }
}
```

- [ ] **Step 2: Write `docs/connectors.md`**

```markdown
# Connectors

Declared in `.mcp.json`. Connect each one by running `/mcp` in Claude Code inside this folder
and completing the sign-in. Nothing is stored in the repo.

## Active in v1

| Server | Used by | Purpose |
|---|---|---|
| metricool | publish | Schedule posts to LinkedIn, Instagram, YouTube; best time to post; analytics |
| canva | instagram-post | Find a brand template, create the post image, export |
| vidiq | youtube-video, topic-ideas | YouTube keyword research, trending topics |

## Optional (add to `.mcp.json` when wanted)

| Server | URL | When |
|---|---|---|
| typefully | https://mcp.typefully.com/mcp | If you prefer Typefully's drafting flow for LinkedIn/X over Metricool |
| wordpress | https://public-api.wordpress.com/wpcom/v2/mcp/v1 | Blog host is WordPress.com |
| notion | https://mcp.notion.com/mcp | Blog host is Notion |
| webflow | https://mcp.webflow.com/mcp | Blog host is Webflow |
| openseo | https://app.openseo.so/mcp | Live site audits and rank tracking |

Snippet to add one:

```json
"wordpress": { "type": "http", "url": "https://public-api.wordpress.com/wpcom/v2/mcp/v1" }
```

After adding a blog host, update the `blog` branch of `.claude/skills/publish/SKILL.md`.
```

- [ ] **Step 3: Verify JSON parses**

Run: `python3 -I -c "import json,sys; d=json.load(open('.mcp.json')); print(sorted(d['mcpServers']))"`
Expected: `['canva', 'metricool', 'vidiq']`

- [ ] **Step 4: Commit**

```bash
git add .mcp.json docs/connectors.md
git commit -m "feat: declare Metricool, Canva, vidIQ connectors

Co-Authored-By: Claude Fable 5.1 <noreply@anthropic.com>"
```

---

### Task 3: seo-check skill

**Files:**
- Create: `.claude/skills/seo-check/SKILL.md`
- Test fixture: `content/drafts/blog/2026-11-04-sample-ecommerce-analytics.md` (temporary, deleted at end of task)

**Interfaces:**
- Consumes: `brand/profile.md` `seo_threshold`; blog draft body sections `## Meta description`, `## Suggested internal links`, `## Image brief`, `## Sources`.
- Produces: `reports/seo/<filename>.md` with a `## Fixes` list; sets `seo_score` (integer 0–100) in the draft's front matter.

- [ ] **Step 1: Write `.claude/skills/seo-check/SKILL.md`**

```markdown
---
name: seo-check
description: Score a blog draft 0-100 for on-page SEO (keyword placement and density, title and meta length, heading structure, readability, links, alt text) and write a fix list. Use when the owner says "seo check <file>" or when blog-post finishes a draft.
---

# SEO check

Input: path to a Markdown file in `content/drafts/blog/` or `content/approved/blog/`.
Output: `reports/seo/<filename>.md` and `seo_score` set in the file's front matter.
This skill never moves files.

## Steps

1. Read `brand/profile.md`; note `seo_threshold` and `site_domain`.
2. Read the file. Parse front matter. If `keyword` is empty, stop and ask the owner for the
   primary keyword.
3. Extract:
   - title: front matter `title`
   - slug: filename without the date prefix and `.md`
   - H1: the first line starting with `# `
   - meta: text under `## Meta description`
   - body: everything from H1 to the first of `## Meta description`, `## Suggested internal
     links`, `## Image brief`, `## Sources` (exclude those sections from word counts)
   - headings: all `##`/`###` lines in body
   - links: Markdown links in body; internal = host equals `site_domain` or path starts with
     `/`; external = any other host. Also count entries under `## Suggested internal links`
     as internal.
   - images: `![alt](url)` in body plus the alt text line under `## Image brief`
4. Score each check. Keyword matching is case-insensitive and ignores punctuation.

   | # | Check | Points |
   |---|---|---|
   | 1 | keyword in title | 10 |
   | 2 | keyword in H1 | 5 |
   | 3 | keyword in first 100 words of body | 10 |
   | 4 | keyword in meta description | 5 |
   | 5 | keyword (hyphenated) in slug | 5 |
   | 6 | keyword density 0.5–2.0% of body words (5 pts if 0.3–0.5 or 2.0–3.0) | 10 |
   | 7 | exactly one H1 | 5 |
   | 8 | at least 3 H2s and no H3 before the first H2 | 5 |
   | 9 | title length 50–60 chars (3 pts if 40–70) | 5 |
   | 10 | meta length 150–160 chars (3 pts if 120–170) | 5 |
   | 11 | body word count ≥ 1200 (5 pts if ≥ 800) | 10 |
   | 12 | readability: average sentence ≤ 20 words AND no paragraph > 150 words (5 pts if only one holds) | 10 |
   | 13 | ≥ 2 internal links (including suggested) | 5 |
   | 14 | ≥ 2 external links to sources in body | 5 |
   | 15 | every image has non-empty alt text, and `## Image brief` includes an alt text line | 5 |

   Total 100. Density = occurrences of the exact keyword phrase ÷ body words × 100.
5. Write `reports/seo/<filename>.md`:

   ```markdown
   # SEO report: <title>
   File: <path>  Keyword: <keyword>  Score: <score>/100  Threshold: <seo_threshold>  Result: PASS|FAIL
   Checked: YYYY-MM-DD

   | # | Check | Points | Earned | Note |
   |---|---|---|---|---|
   (one row per check; Note gives the measured value, e.g. "title is 44 chars")

   ## Fixes
   (ordered by points lost, most first; each one concrete, e.g. "Add 'e-commerce analytics'
   to the title; current: '...'")
   ```
6. Set `seo_score: <score>` in the draft's front matter (replace the existing line).
7. Reply in chat: score, PASS/FAIL against threshold, and the top 3 fixes.
```

- [ ] **Step 2: Create a fixture draft that should score below threshold**

Write `content/drafts/blog/2026-11-04-sample-ecommerce-analytics.md`:

```markdown
---
title: "Analytics tips"
channel: blog
status: draft
keyword: "e-commerce analytics"
secondary_keywords: []
seo_score: null
created: 2026-11-04
scheduled_for: null
published_url: null
source: null
---

# Analytics tips for stores

Running a store is hard. Numbers help. Here are some tips.

## Look at the numbers

Open your dashboard every week. Write down what changed. Numbers tell a story if you look at them long enough and you have time to do that which most people do not because they are busy running the store and talking to customers and dealing with suppliers.

## Meta description
Tips.
```

- [ ] **Step 3: Run the skill on the fixture**

Follow `SKILL.md` steps on the fixture (in-session, or `claude -p "seo check content/drafts/blog/2026-11-04-sample-ecommerce-analytics.md"` from the folder).
Expected: `reports/seo/2026-11-04-sample-ecommerce-analytics.md` exists, score between 10 and 35, Result FAIL, Fixes list includes title keyword, meta length, word count, H2 count, links. Front matter now has `seo_score: <n>`.

Run: `grep "^seo_score:" content/drafts/blog/2026-11-04-sample-ecommerce-analytics.md`
Expected: `seo_score: <integer>`

- [ ] **Step 4: Remove the fixture and its report**

```bash
rm content/drafts/blog/2026-11-04-sample-ecommerce-analytics.md reports/seo/2026-11-04-sample-ecommerce-analytics.md
```

- [ ] **Step 5: Commit**

```bash
git add .claude/skills/seo-check/SKILL.md
git commit -m "feat: seo-check skill

Co-Authored-By: Claude Fable 5.1 <noreply@anthropic.com>"
```

---

### Task 4: blog-post skill

**Files:**
- Create: `.claude/skills/blog-post/SKILL.md`

**Interfaces:**
- Consumes: seo-check (Task 3), `brand/profile.md`, `brand/keywords.md`, `brand/examples/*.md`, optional idea file from `content/ideas/`.
- Produces: `content/drafts/blog/YYYY-MM-DD-<slug>.md` with sections `# <Title>`, body, `## Meta description`, `## Suggested internal links`, `## Image brief`, `## Sources`; `seo_score` set.

- [ ] **Step 1: Write `.claude/skills/blog-post/SKILL.md`**

```markdown
---
name: blog-post
description: Research, outline, and write an SEO-ready blog post draft into content/drafts/blog/, then score it with seo-check and revise once. Use when the owner says "write a blog on <topic or keyword>" or names a file in content/ideas/.
---

# Blog post

Input: a topic, a keyword, or a path in `content/ideas/`.
Output: `content/drafts/blog/YYYY-MM-DD-<slug>.md` with `seo_score` set, plus its SEO report.

## Steps

1. Read `brand/profile.md`, `brand/keywords.md`, and every file in `brand/examples/`.
2. Decide the primary keyword:
   - idea file: use its `keyword`
   - owner gave a keyword: use it
   - owner gave only a topic: pick the closest long-tail phrase from `brand/keywords.md`, or
     derive a 2–4 word phrase; state the choice in the reply.
   Pick 2–3 `secondary_keywords` from the same cluster.
3. Research (skip gracefully if search is unavailable; note "research unavailable" in the
   report's Sources section):
   - WebSearch the keyword and `<keyword> questions`.
   - WebFetch the top 3–5 result pages. For each note: title, H2 headings, one gap they leave.
   - Collect at least 3 facts or statistics with source URLs for citation.
4. Outline: H1 containing the keyword; 4–7 H2 sections; add `## FAQ` with 3–5 questions when
   the research shows common questions; final section is the CTA from the profile.
5. Draft in the brand voice, 1200–2000 words (or the idea file's target). Rules:
   - keyword in the first 100 words, naturally
   - paragraphs of at most 4 sentences; sentences average under 20 words
   - cite each fact inline with a Markdown link to its source
   - no banned phrases; no exclamation marks
   - one `# ` H1 only; H2 before any H3
6. Write the file with front matter (`channel: blog`, `status: draft`, `created: today`,
   `source: <idea path or null>`) and these sections after the body:

   ```markdown
   ## Meta description
   <150–160 characters, contains the keyword, ends with a reason to click>

   ## Suggested internal links
   - <anchor text> → /<path on site_domain> (why)
   - <anchor text> → /<path> (why)

   ## Image brief
   Hero: <one sentence visual idea>
   Alt text: <descriptive alt text containing the keyword>

   ## Sources
   - <title> — <url>
   ```
7. Run the seo-check skill on the new file.
8. If the score is below `seo_threshold`: apply the top fixes from the report, then run
   seo-check once more. Do not loop further; report the remaining fixes.
9. If the input was an idea file, `git rm` it (the draft's `source` records its path).
10. Commit: `content(blog): draft <slug>`.
11. Reply: path, keyword, score and PASS/FAIL, remaining fixes, and "say `approve <path>`
    when ready".
```

- [ ] **Step 2: Dry run on a sample topic**

Run: in-session, "write a blog on e-commerce kpis to track weekly" (or `claude -p` with that text from the folder).
Expected:
- `content/drafts/blog/2026-11-04-e-commerce-kpis-to-track-weekly.md` exists with all six body sections.
- `reports/seo/2026-11-04-e-commerce-kpis-to-track-weekly.md` exists.
- `grep "^seo_score:" <draft>` shows an integer ≥ 70.
- `grep -ci "game-changer\|delve\|unlock" <draft>` prints 0.
- Commit `content(blog): draft e-commerce-kpis-to-track-weekly` exists.

Keep this draft: Tasks 8 and 10 use it.

- [ ] **Step 3: Commit the skill**

```bash
git add .claude/skills/blog-post/SKILL.md
git commit -m "feat: blog-post skill

Co-Authored-By: Claude Fable 5.1 <noreply@anthropic.com>"
```

---

### Task 5: linkedin-post skill

**Files:**
- Create: `.claude/skills/linkedin-post/SKILL.md`

**Interfaces:**
- Consumes: `brand/profile.md`; optional source blog path.
- Produces: `content/drafts/linkedin/YYYY-MM-DD-<slug>.md` with body text, `## First comment`, optional `## Variants`.

- [ ] **Step 1: Write `.claude/skills/linkedin-post/SKILL.md`**

```markdown
---
name: linkedin-post
description: Write a LinkedIn post draft into content/drafts/linkedin/ from a topic or from a blog post. Use when the owner says "linkedin post about <topic>" or "linkedin post from <blog file>", or when repurpose calls it.
---

# LinkedIn post

Input: a topic, or a path to a blog file (drafts, approved, or published).
Output: `content/drafts/linkedin/YYYY-MM-DD-<slug>.md`.

## Steps

1. Read `brand/profile.md` and any `brand/examples/linkedin-*.md`.
2. If a blog path was given, read it and pick the single most useful insight or list from it.
   Set `source` to that path and `keyword` to the blog's keyword.
3. Write the post:
   - line 1: a hook under 12 words that states a problem, a surprising number, or a
     contrarian claim; no "I'm excited to share"
   - 150–300 words, one idea per line, blank line between lines
   - a concrete example or number in the middle
   - end with the LinkedIn CTA from the profile, then 3–5 hashtags on the last line
   - no links in the body
4. Write the file:

   ```markdown
   ---
   title: "<hook line>"
   channel: linkedin
   status: draft
   keyword: "<keyword or empty>"
   secondary_keywords: []
   seo_score: null
   created: YYYY-MM-DD
   scheduled_for: null
   published_url: null
   source: <blog path or null>
   ---

   <post body exactly as it should be posted>

   ## First comment
   <link to the blog if source is set, else one sentence, or "none">
   ```
5. If the owner asked for variants, add `## Variants` with two alternative hooks plus first
   paragraphs.
6. Commit `content(linkedin): draft <slug>`. Reply with the path and the hook line.
```

- [ ] **Step 2: Dry run**

Run: in-session, "linkedin post about why weekly kpi reviews beat daily dashboards".
Expected: file in `content/drafts/linkedin/`, body 150–300 words (`wc -w` on the body section between the front matter and `## First comment` is 150–300), last body line starts with `#`, no `http` in the body section, `## First comment` present.

- [ ] **Step 3: Commit**

```bash
git add .claude/skills/linkedin-post/SKILL.md
git commit -m "feat: linkedin-post skill

Co-Authored-By: Claude Fable 5.1 <noreply@anthropic.com>"
```

---

### Task 6: instagram-post skill

**Files:**
- Create: `.claude/skills/instagram-post/SKILL.md`

**Interfaces:**
- Consumes: `brand/profile.md` (`canva_template`), Canva connector tools `search-designs`, `get-design`; optional source blog path.
- Produces: `content/drafts/instagram/YYYY-MM-DD-<slug>.md` with `## Caption`, `## Hashtags`, `## Image brief`, and front matter extra `canva_design_url` when a design was created.

- [ ] **Step 1: Write `.claude/skills/instagram-post/SKILL.md`**

```markdown
---
name: instagram-post
description: Write an Instagram caption, hashtags, and an image brief into content/drafts/instagram/, and create the image in Canva when connected. Use when the owner says "instagram post about <topic>" or "from <blog file>", or when repurpose calls it.
---

# Instagram post

Input: a topic, or a path to a blog file.
Output: `content/drafts/instagram/YYYY-MM-DD-<slug>.md`.

## Steps

1. Read `brand/profile.md` (tone, CTA, `canva_template`) and any `brand/examples/instagram-*.md`.
2. If a blog path was given, read it and choose one takeaway that fits a single image or a
   3–5 point list. Set `source` and `keyword` from the blog.
3. Write the file:

   ```markdown
   ---
   title: "<headline on the image>"
   channel: instagram
   status: draft
   keyword: "<keyword or empty>"
   secondary_keywords: []
   seo_score: null
   created: YYYY-MM-DD
   scheduled_for: null
   published_url: null
   source: <blog path or null>
   canva_design_url: null
   ---

   ## Caption
   <first line is the hook, under 10 words; then 3–6 short lines; blank lines between;
   ends with the Instagram CTA; total under 2200 characters; at most 3 emojis>

   ## Hashtags
   <10–20 hashtags, mix of broad (100k+ posts) and niche, one line, lowercase>

   ## Image brief
   Format: 1080x1350 portrait (or 1080x1080 if a square template is named)
   Headline overlay: <at most 8 words>
   Visual: <one sentence>
   Alt text: <descriptive alt text>
   ```
4. Canva, only if the `canva` connector is connected (its tools appear in the session):
   - If `canva_template` is set: `search-designs` for that name, `get-design`, and create the
     post from it with the headline overlay; export as PNG; put the design URL in
     `canva_design_url`.
   - If not set: `search-designs` for "instagram post" in the owner's designs; if nothing
     fits, leave `canva_design_url: null` and say "no template found; image brief only".
   If Canva is not connected: leave `canva_design_url: null` and say
   "Canva not connected; image brief only. Connect via /mcp to create the image."
5. Commit `content(instagram): draft <slug>`. Reply with the path, the headline, and whether
   an image was created.
```

- [ ] **Step 2: Dry run**

Run: in-session, "instagram post about 5 kpis every store owner should check on monday".
Expected: file in `content/drafts/instagram/` with the three `##` sections; `## Hashtags` line has 10–20 tokens starting with `#`; the caption section is under 2200 characters; reply states Canva status.

- [ ] **Step 3: Commit**

```bash
git add .claude/skills/instagram-post/SKILL.md
git commit -m "feat: instagram-post skill

Co-Authored-By: Claude Fable 5.1 <noreply@anthropic.com>"
```

---

### Task 7: youtube-video skill

**Files:**
- Create: `.claude/skills/youtube-video/SKILL.md`

**Interfaces:**
- Consumes: `brand/profile.md`; vidIQ tool `vidiq_keyword_research`; optional source blog path.
- Produces: `content/drafts/youtube/YYYY-MM-DD-<slug>.md` with `## Title options`, `## Description`, `## Tags`, `## Script`, `## Thumbnail brief`.

- [ ] **Step 1: Write `.claude/skills/youtube-video/SKILL.md`**

```markdown
---
name: youtube-video
description: Write a YouTube video package (title options, description, tags, full script, thumbnail brief) into content/drafts/youtube/. Use when the owner says "youtube video about <topic>" or "from <blog file>", or when repurpose calls it.
---

# YouTube video

Input: a topic, or a path to a blog file.
Output: `content/drafts/youtube/YYYY-MM-DD-<slug>.md`.

## Steps

1. Read `brand/profile.md` and any `brand/examples/youtube-*.md`.
2. If a blog path was given, read it; the script follows the blog's H2 structure. Set
   `source` and `keyword` from the blog.
3. Keyword research, only if the `vidiq` connector is connected: call
   `vidiq_keyword_research` with the keyword; pick the top 3 related terms by search volume
   and low competition as `secondary_keywords`. If not connected, derive 3 related terms
   yourself and note "vidIQ not connected".
4. Write the file:

   ```markdown
   ---
   title: "<title option 1>"
   channel: youtube
   status: draft
   keyword: "<keyword>"
   secondary_keywords: [<3 terms>]
   seo_score: null
   created: YYYY-MM-DD
   scheduled_for: null
   published_url: null
   source: <blog path or null>
   video_file: null
   ---

   ## Title options
   1. <≤ 60 chars, keyword near the start>
   2. <≤ 60 chars, curiosity angle>
   3. <≤ 60 chars, number or outcome angle>

   ## Description
   <2 lines containing the keyword, visible above the fold>

   <3–5 line summary of what the viewer learns>

   Chapters:
   00:00 Intro
   <one line per script section; keep 00:00 placeholders for timing after recording>

   <YouTube CTA from profile>
   <link to blog if source set>
   #<3 hashtags>

   ## Tags
   <10–15 comma-separated tags, keyword first>

   ## Script
   ### Hook (0:00–0:30)
   <state the problem and the promise; under 80 words>
   ### <Section per H2 or key point>
   <spoken, conversational, short sentences; "you" voice; 120–200 words per section>
   ### Close
   <recap in 3 lines, then CTA>

   ## Thumbnail brief
   Text: <≤ 4 words>
   Visual: <one sentence>
   Emotion/face: <one phrase>
   ```
   Script length target: 5–8 minutes spoken, about 750–1200 words.
5. Commit `content(youtube): draft <slug>`. Reply with the path, title option 1, and script
   word count.
```

- [ ] **Step 2: Dry run**

Run: in-session, "youtube video about reading shopify analytics in 10 minutes a week".
Expected: file in `content/drafts/youtube/` with the five `##` sections, three title lines each ≤ 60 characters (`awk` check on the lines under `## Title options`), script section 750–1200 words, reply states vidIQ status.

- [ ] **Step 3: Commit**

```bash
git add .claude/skills/youtube-video/SKILL.md
git commit -m "feat: youtube-video skill

Co-Authored-By: Claude Fable 5.1 <noreply@anthropic.com>"
```

---

### Task 8: repurpose skill

**Files:**
- Create: `.claude/skills/repurpose/SKILL.md`

**Interfaces:**
- Consumes: linkedin-post, instagram-post, youtube-video skills with a blog path as input.
- Produces: three draft files, each with `source` set to the blog path.

- [ ] **Step 1: Write `.claude/skills/repurpose/SKILL.md`**

```markdown
---
name: repurpose
description: Turn an approved blog post into LinkedIn, Instagram, and YouTube drafts, each with source set to the blog. Use when the owner says "repurpose <blog file>".
---

# Repurpose

Input: a path in `content/approved/blog/` or `content/published/blog/`.
Output: one new draft in each of `content/drafts/linkedin/`, `content/drafts/instagram/`,
`content/drafts/youtube/`.

## Steps

1. Confirm the path is under `content/approved/blog/` or `content/published/blog/`. If it is
   still in drafts, reply "Approve the blog first (`approve <path>`), then repurpose." and stop.
2. Read the blog once. Note its keyword, H2 list, strongest statistic, and strongest practical
   tip.
3. Run the linkedin-post skill with the blog path. Use the strongest practical tip as the
   angle.
4. Run the instagram-post skill with the blog path. Use the H2 list as the image list, or the
   strongest statistic as the headline.
5. Run the youtube-video skill with the blog path.
6. Each skill commits its own file. Reply with the three paths and one line per draft saying
   its angle.
```

- [ ] **Step 2: Dry run (uses the blog from Task 4)**

First the owner-approval step must be done explicitly: the executor says, in chat, "approve content/drafts/blog/2026-11-04-e-commerce-kpis-to-track-weekly.md" and follows the approval procedure in `CLAUDE.md`.
Expected: file now at `content/approved/blog/...` with `status: approved`; commit `content(blog): approve e-commerce-kpis-to-track-weekly`.

Then run: "repurpose content/approved/blog/2026-11-04-e-commerce-kpis-to-track-weekly.md".
Expected: three new files in the three social draft folders; each has `source: content/approved/blog/2026-11-04-e-commerce-kpis-to-track-weekly.md` (`grep -l "^source: content/approved/blog" content/drafts/*/*.md` lists 3 files); three commits.

Also run the refusal path: "repurpose content/drafts/linkedin/<any file>".
Expected: reply says approve first; no files created.

- [ ] **Step 3: Commit**

```bash
git add .claude/skills/repurpose/SKILL.md
git commit -m "feat: repurpose skill

Co-Authored-By: Claude Fable 5.1 <noreply@anthropic.com>"
```

---

### Task 9: topic-ideas skill

**Files:**
- Create: `.claude/skills/topic-ideas/SKILL.md`

**Interfaces:**
- Consumes: `brand/keywords.md`, `brand/profile.md` pillars, existing files in all `content/` folders, WebSearch, optional vidIQ.
- Produces: `content/ideas/YYYY-MM-DD-<slug>.md` files with `status: idea`, `channel: blog`, `keyword`, and a body of angle, why now, outline, sources.

- [ ] **Step 1: Write `.claude/skills/topic-ideas/SKILL.md`**

```markdown
---
name: topic-ideas
description: Suggest 5-10 new blog topic ideas from the brand's keyword clusters and current web trends, deduplicated against existing content, written to content/ideas/. Use when the owner says "ideas" or "topic ideas for <theme>", and in the Monday routine.
---

# Topic ideas

Input: optional theme or cluster name.
Output: 5–10 files in `content/ideas/`.

## Steps

1. Read `brand/profile.md` (pillars) and `brand/keywords.md`. If a theme was given, use only
   the matching cluster(s); otherwise use all.
2. List existing titles and keywords from every `.md` under `content/` (all stages) so you
   can avoid repeats.
3. For each cluster: WebSearch `<head keyword>`, `<head keyword> 2026`, and
   `<head keyword> questions`. From the results note recurring questions, new developments,
   and angles competitors cover thinly. If the `vidiq` connector is connected, also call
   `vidiq_keyword_research` on the head keyword and note high-volume, low-competition terms.
4. Generate 5–10 ideas total, spread across pillars. Drop any whose keyword or title closely
   matches an existing item (same keyword, or title sharing 4+ significant words).
5. Write each idea as `content/ideas/YYYY-MM-DD-<slug>.md`:

   ```markdown
   ---
   title: "<working title with keyword>"
   channel: blog
   status: idea
   keyword: "<long-tail keyword>"
   secondary_keywords: [<2–3>]
   seo_score: null
   created: YYYY-MM-DD
   scheduled_for: null
   published_url: null
   source: null
   pillar: "<pillar name>"
   ---

   ## Angle
   <two sentences: the specific take and who it is for>

   ## Why now
   <one sentence citing a trend, question, or gap, with a source URL>

   ## Outline
   - <H2>
   - <H2>
   - <H2>
   - <H2>

   ## Sources
   - <url>
   ```
6. Commit `content(ideas): add <n> ideas YYYY-MM-DD`.
7. Reply with a numbered list: title, keyword, pillar; and "say `write <path>` to draft one".
```

- [ ] **Step 2: Dry run**

Run: in-session, "topic ideas for product margin".
Expected: 5–10 new files in `content/ideas/` (`ls content/ideas/*.md | wc -l`), each with `status: idea` and a non-empty `keyword`; none duplicates the Task 4 blog keyword; one commit.

- [ ] **Step 3: Commit**

```bash
git add .claude/skills/topic-ideas/SKILL.md
git commit -m "feat: topic-ideas skill

Co-Authored-By: Claude Fable 5.1 <noreply@anthropic.com>"
```

---

### Task 10: publish skill

**Files:**
- Create: `.claude/skills/publish/SKILL.md`

**Interfaces:**
- Consumes: files in `content/approved/<channel>/`; Metricool tools `getBrandSettings`, `getBestTimeToPostByNetwork`, `createScheduledPost`; front matter `scheduled_for`, `canva_design_url`, `video_file`.
- Produces: file moved to `content/published/<channel>/` with `status: published`, `published_url` set (Metricool post id or URL, or local path for blog).

- [ ] **Step 1: Write `.claude/skills/publish/SKILL.md`**

```markdown
---
name: publish
description: Publish or schedule an approved content item through the right connector (Metricool for LinkedIn, Instagram, YouTube; local folder for blog until a host is connected) and move it to content/published/. Use when the owner says "publish <file>" or "publish all approved".
---

# Publish

Input: a path under `content/approved/`, or "all approved".
Output: file(s) moved to `content/published/<channel>/` with `published_url` set.

## Guard

If the path does not start with `content/approved/`, reply exactly:
"Refusing: <path> is not in content/approved/. Approve it first with `approve <path>`."
and stop. Do nothing else.

## Steps per file

1. Read the file; take `channel`, `scheduled_for`, `title`, body sections.
2. Route by channel.

   **linkedin / instagram / youtube (Metricool):**
   a. Check the `metricool` connector is connected by calling `getBrandSettings`. If the tool
      is unavailable or the call fails, reply "Metricool is not connected. Run /mcp, connect
      Metricool, then retry." and stop. Leave the file in place.
   b. Time: if `scheduled_for` is set, use it. Otherwise call `getBestTimeToPostByNetwork`
      for the network and use the next suggested slot after now; write it into
      `scheduled_for`.
   c. Build the post:
      - linkedin: text = the body between the front matter and `## First comment`.
        After scheduling, if `## First comment` is not "none", tell the owner to add it
        manually once the post is live (Metricool does not post first comments).
      - instagram: text = `## Caption` + blank line + `## Hashtags`; media = `canva_design_url`
        exported PNG. If `canva_design_url` is null, ask the owner for an image path or URL
        and stop until given.
      - youtube: title = title option 1, description = `## Description`, tags = `## Tags`;
        media = `video_file`. If `video_file` is null, ask the owner for the video file path
        or URL and stop until given.
   d. Call `createScheduledPost` once with network, text, media, and the datetime. Never
      retry. If it fails, report the error and stop; the file stays in approved.
   e. Set `published_url` to the post URL returned, or the scheduled post id if no URL.

   **blog:**
   a. If no blog host connector is declared in `.mcp.json` (no `wordpress`, `notion`, or
      `webflow` key): local publish. Set `published_url` to the new path under
      `content/published/blog/`. Tell the owner the post is ready to paste into their CMS.
   b. If a host connector is declared: this branch is not yet written. Reply "Blog host
      connector <name> is declared but publish is not implemented for it yet; see
      docs/connectors.md" and stop.
3. Set `status: published`. `git mv` the file to `content/published/<channel>/`.
4. Commit `content(<channel>): publish <slug>`.
5. Reply with the new path, the scheduled time, and `published_url`.

## "publish all approved"

Process every file under `content/approved/*/` in filename order, following the steps above.
Stop at the first failure and report which files were published and which were not.
```

- [ ] **Step 2: Refusal test**

Run: in-session, "publish content/drafts/linkedin/<the Task 5 file>".
Expected: reply is the exact refusal line; `git status` shows no changes.

- [ ] **Step 3: Local blog publish test (uses the approved blog from Task 8)**

Run: "publish content/approved/blog/2026-11-04-e-commerce-kpis-to-track-weekly.md".
Expected: file now at `content/published/blog/2026-11-04-e-commerce-kpis-to-track-weekly.md`, `status: published`, `published_url: content/published/blog/2026-11-04-e-commerce-kpis-to-track-weekly.md`; commit `content(blog): publish e-commerce-kpis-to-track-weekly`.

- [ ] **Step 4: Metricool not-connected test**

Approve the Task 5 LinkedIn draft ("approve <path>"), then "publish <approved path>".
Expected: reply says Metricool is not connected and names `/mcp`; file remains in `content/approved/linkedin/`.
(If the owner has already connected Metricool, skip this step and instead confirm with the owner before any real post.)

- [ ] **Step 5: Commit**

```bash
git add .claude/skills/publish/SKILL.md
git commit -m "feat: publish skill

Co-Authored-By: Claude Fable 5.1 <noreply@anthropic.com>"
```

---

### Task 11: README and weekly review dry run

**Files:**
- Create: `README.md`
- Create: `reports/weekly/2026-11-04.md` (by running the procedure)

- [ ] **Step 1: Write `README.md`**

```markdown
# AI Digital Marketing Workspace

Run your brand's blog, LinkedIn, Instagram, and YouTube content from Claude Code. No app
code: skills, connectors, and Markdown.

## Setup (10 minutes)

1. Open this folder in Claude Code.
2. Edit `brand/profile.md` and `brand/keywords.md`; replace every "Example:" value.
3. Drop a few of your own posts into `brand/examples/`.
4. Run `/mcp` and connect Metricool (publishing), Canva (Instagram images), vidIQ (YouTube
   research). See `docs/connectors.md` for optional ones.

## Daily use

| Say | Result |
|---|---|
| `topic ideas for <theme>` | ideas in `content/ideas/` |
| `write a blog on <topic>` | SEO-scored draft in `content/drafts/blog/` |
| `linkedin post about <topic>` | draft in `content/drafts/linkedin/` |
| `instagram post about <topic>` | caption, hashtags, image |
| `youtube video about <topic>` | title, description, script |
| `approve <file>` | moves to `content/approved/` |
| `repurpose <approved blog>` | three social drafts |
| `publish <file>` / `publish all approved` | schedules via Metricool, moves to `content/published/` |
| `weekly review` | report in `reports/weekly/` |

Nothing is published without you saying `approve` and then `publish`.

## Layout

See `CLAUDE.md` for the rules and `docs/superpowers/specs/` for the design.
```

- [ ] **Step 2: Run the weekly review procedure**

Run: in-session, "weekly review".
Expected: `reports/weekly/2026-11-04.md` exists and lists: counts per stage per channel, the drafts from Tasks 5–8, the approved LinkedIn item, the published blog, no blog drafts below threshold, no stale ideas; commit `docs: weekly review 2026-11-04`.

- [ ] **Step 3: Commit**

```bash
git add README.md
git commit -m "docs: README

Co-Authored-By: Claude Fable 5.1 <noreply@anthropic.com>"
```

---

### Task 12: GitHub repo and scheduled routines (needs owner go-ahead)

**Files:**
- None in repo. Creates a GitHub repository and two cloud routines.

Pushing to GitHub is outward-facing: ask the owner before Step 1 and stop if they decline. Everything in Tasks 1–11 works without this task.

- [ ] **Step 1: Create a private GitHub repo and push**

```bash
gh repo create ai-digital-marketing --private --source . --push
```
Expected: `gh repo view --json url` prints the repo URL; `git remote -v` shows origin.

- [ ] **Step 2: Create the Monday ideas routine**

Use the `schedule` skill. Routine: name `marketing-topic-ideas`, cron `0 9 * * 1` in the profile timezone, prompt:
"Run the topic-ideas skill for all clusters. Commit the new idea files and push to a branch named ideas/YYYY-MM-DD, then open a pull request titled 'Topic ideas YYYY-MM-DD'. Do not approve or publish anything."

- [ ] **Step 3: Create the Friday review routine**

Routine: name `marketing-weekly-review`, cron `0 16 * * 5` in the profile timezone, prompt:
"Follow the weekly review procedure in CLAUDE.md. Commit reports/weekly/YYYY-MM-DD.md and push to a branch named review/YYYY-MM-DD, then open a pull request titled 'Weekly review YYYY-MM-DD'. Do not approve or publish anything."

- [ ] **Step 4: Verify**

Run: list scheduled routines via the `schedule` skill.
Expected: both routines listed with the crons above. Trigger `marketing-weekly-review` once manually; expected a PR with a `reports/weekly/` file.

- [ ] **Step 5: Record in docs**

Append to `docs/connectors.md`:

```markdown
## Scheduled routines

| Routine | Cron | Does |
|---|---|---|
| marketing-topic-ideas | Mon 09:00 | topic-ideas → PR `Topic ideas YYYY-MM-DD` |
| marketing-weekly-review | Fri 16:00 | weekly review → PR `Weekly review YYYY-MM-DD` |

Routines never approve or publish. Merge their PRs to accept the ideas or the report.
```

```bash
git add docs/connectors.md
git commit -m "docs: scheduled routines

Co-Authored-By: Claude Fable 5.1 <noreply@anthropic.com>"
git push
```
