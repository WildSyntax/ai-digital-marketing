# AI Digital Marketing Workspace — Design

Date: 2026-11-04
Status: approved by owner

## Purpose

A Claude Code workspace that runs digital marketing for one brand (the owner's own business).
Claude is the engine. There is no custom application code: skills define each marketing
activity, MCP connectors do the outside work (publishing, visuals, research), and Markdown
files on disk are the content store and review queue.

Channels covered: blog (with on-page SEO checks), LinkedIn, Instagram, YouTube.

## Decisions already made

| Question | Decision |
|---|---|
| Audience | Owner's own brand/business (single brand, single voice) |
| First priority | Blog + SEO fully detailed; all other channel skills scaffolded as solid first versions |
| Publishing mode | Draft, then explicit human approval, then publish. Never auto-publish. |
| Implementation | No Python or other code. Claude Code skills + MCP connectors + Markdown. |
| AI model | Claude (the Claude Code session itself) |
| Blog host | Not decided. Posts land in a local folder until a host is chosen. |
| Interface | Chat with Claude Code in this folder. No dashboard. |
| Topic source | Owner gives topics or keywords; a weekly routine also suggests topics. |
| SEO scope (v1) | On-page essentials, computed by Claude from the draft. No paid SEO API. |
| Research | Light web research before drafting, using Claude Code's built-in web search and fetch. |
| Brand profile | Placeholder values; owner fills in later. |
| Scheduled runs | Yes: Monday topic ideas, Friday content review. Requires the repo on GitHub. |

## Architecture

```
owner (chat)  ──►  Claude Code in ai-digital-marketing/
                      │
                      ├── CLAUDE.md            operating manual and rules
                      ├── .claude/skills/*     one skill per activity
                      ├── brand/               voice, keywords, examples
                      ├── content/             ideas → drafts → approved → published
                      ├── reports/             SEO scores, weekly summaries
                      └── .mcp.json            connectors
                                │
            ┌───────────────────┼─────────────────────┐
         Metricool            Canva                 vidIQ
   (LinkedIn, Instagram,  (Instagram visuals)  (YouTube research)
    YouTube publish,
    best time, analytics)
```

Built-in Claude Code web search and fetch handle research; no search connector is needed.

### Connectors

| Need | Connector | Status in v1 |
|---|---|---|
| Publish and schedule LinkedIn, Instagram, YouTube | Metricool (`https://ai.metricool.com/mcp`) | Configured, owner connects |
| LinkedIn text drafts (alternative) | Typefully (`https://mcp.typefully.com/mcp`) | Listed, commented out |
| Instagram visuals | Canva (`https://mcp.canva.com/mcp`) | Configured, owner connects |
| YouTube research | vidIQ (`https://mcp.vidiq.com/mcp`) | Configured, owner connects |
| Blog publishing | WordPress.com, Notion, or Webflow | Commented out until host is chosen |
| Live SEO audit | OpenSEO (`https://app.openseo.so/mcp`) | Commented out; optional later |

All connectors are remote HTTP MCP servers declared in `.mcp.json`. Authentication is done by
the owner through Claude Code's `/mcp` flow; no keys are stored in the repo.

## Folder layout

```
ai-digital-marketing/
  CLAUDE.md
  .mcp.json
  .claude/skills/
    topic-ideas/SKILL.md
    blog-post/SKILL.md
    seo-check/SKILL.md
    linkedin-post/SKILL.md
    instagram-post/SKILL.md
    youtube-video/SKILL.md
    repurpose/SKILL.md
    publish/SKILL.md
  brand/
    profile.md
    keywords.md
    examples/README.md
  content/
    ideas/
    drafts/{blog,linkedin,instagram,youtube}/
    approved/{blog,linkedin,instagram,youtube}/
    published/{blog,linkedin,instagram,youtube}/
  reports/
    seo/
    weekly/
  docs/superpowers/specs/
```

Empty directories carry a `.gitkeep`.

## Content item format

Every content item is one Markdown file. Filename: `YYYY-MM-DD-<slug>.md`. Front matter:

```yaml
---
title: ""
channel: blog | linkedin | instagram | youtube
status: idea | draft | approved | published
keyword: ""              # primary target keyword
secondary_keywords: []
seo_score: null          # 0-100, set by seo-check (blog only)
created: YYYY-MM-DD
scheduled_for: null      # ISO datetime, set at approval if scheduling
published_url: null      # set by publish
source: null             # path of the blog post this was repurposed from, if any
---
```

The body is the content itself. Channel-specific extras (meta description, hashtags, image
brief, video tags, thumbnail brief) live in clearly headed sections inside the body.

The `status` field and the folder must agree. Skills move files between folders and update
`status` in the same step.

## Skills

Each skill is a `SKILL.md` with frontmatter `name` and `description` and a step-by-step
procedure. All skills read `brand/profile.md` first.

| Skill | Input | Output | Notes |
|---|---|---|---|
| topic-ideas | optional theme | 5–10 idea files in `content/ideas/` | Uses web search on `brand/keywords.md` clusters; dedupes against existing ideas and published. |
| blog-post | topic or keyword, or an idea file | draft in `content/drafts/blog/` plus SEO report | Research (top results for the keyword) → outline → draft (1200–2000 words unless told otherwise) → runs seo-check → revises once if score below threshold. |
| seo-check | path to a blog draft | `seo_score` in front matter plus `reports/seo/<file>.md` | Checks: keyword in title, H1, first 100 words, URL slug, meta description; keyword density 0.5–2%; one H1, logical H2/H3; title 50–60 chars; meta 150–160 chars; readability (short paragraphs, sentence length); word count; at least 2 internal and 2 external links suggested; image alt text present. Produces a score 0–100 and a fix list. |
| linkedin-post | topic, or a blog path | draft in `content/drafts/linkedin/` | Hook in first line, 150–300 words, 3–5 hashtags, no links in body (link in first comment noted). Offers 3 variants on request. |
| instagram-post | topic, or a blog path | draft in `content/drafts/instagram/` | Caption, up to 20 hashtags, and a Canva image brief (format, text overlay, visual idea). If Canva is connected, creates the design and records its URL. |
| youtube-video | topic, or a blog path | draft in `content/drafts/youtube/` | Title (≤60 chars), description with timestamps placeholder, tags, full script with hook/body/CTA, thumbnail brief. Uses vidIQ keyword research when connected. |
| repurpose | path of an approved blog | one draft per social channel | Calls the three channel skills with `source` set. |
| publish | path in `content/approved/` | file moved to `published/`, `published_url` set | Refuses any path outside `approved/`. Routes by `channel`: linkedin/instagram/youtube → Metricool `createScheduledPost` (uses `scheduled_for`, or best time via `getBestTimeToPostByNetwork`); blog → local `published/blog/` only until a host connector is enabled. If the connector is not connected, reports which one and stops. |

## Workflow

1. Ideas: owner adds to `content/ideas/` or runs topic-ideas.
2. Draft: owner asks for a piece. The skill writes to `drafts/<channel>/`. Blog drafts get an
   SEO score automatically.
3. Review: owner reads the draft and asks for edits in chat.
4. Approve: owner says "approve <file>". Claude checks SEO threshold (blog), sets
   `status: approved`, optionally `scheduled_for`, and moves the file to `approved/<channel>/`.
5. Publish: owner says "publish <file>" (or "publish everything approved"). The publish skill
   pushes through the connector, sets `published_url`, moves to `published/<channel>/`.
6. Repurpose: after a blog is approved, owner can run repurpose to seed social drafts.

Approval is always an explicit instruction from the owner in chat. No skill may move a file
into `approved/` or `published/` on its own.

## Scheduled runs

Two cloud routines, created with Claude Code's scheduler after the repo is on GitHub:

- Monday 09:00 local: run topic-ideas, commit new idea files, open a PR or push to a branch.
- Friday 16:00 local: write `reports/weekly/YYYY-MM-DD.md` listing drafts, approved,
  published, blog drafts with `seo_score` below threshold, and ideas older than 30 days.

Routines never approve or publish.

## Brand profile

`brand/profile.md` holds placeholders the owner fills in: brand name, one-line description,
audience, tone (three adjectives plus an example sentence), content pillars (3–5),
banned words/phrases, CTA defaults per channel, posting cadence per channel, and
`seo_threshold` (default 70).

## Error handling

- Connector not connected or call fails: skill names the connector, leaves the file where it
  is, and stops. No retries that could double-post.
- SEO score below `seo_threshold`: approve is refused with the fix list, unless the owner says
  "approve anyway".
- Publish called on a file outside `approved/`: refused with the reason.
- Research fetch fails: skill proceeds from the model alone and notes it in the draft's report.

## Testing (dry runs)

- Blog: one sample topic through research → draft → seo-check → approve → local publish.
  Verify front matter, folder moves, SEO report file.
- Repurpose: the sample blog into three social drafts; verify `source` and channel formats.
- Publish refusal: attempt to publish a file in `drafts/`; verify refusal.
- Connector publishes: after the owner connects Metricool, one real LinkedIn post the owner
  approves.

## Out of scope for v1

Paid keyword data, live site crawling, image generation beyond Canva templates, video
rendering, analytics dashboards, multi-brand support.
