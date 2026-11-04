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
