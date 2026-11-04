# AI Digital Marketing Workspace

Run your brand's blog, LinkedIn, Instagram, and YouTube content from Claude Code. No app
code: skills, connectors, and Markdown.

## Setup (10 minutes)

1. Open this folder in Claude Code.
2. Edit `brand/profile.md` and `brand/keywords.md`; replace every "Example:" value, and fill
   the front-matter fields `site_domain`, `timezone`, `canva_template`, `seo_threshold`.
3. Drop a few of your own posts into `brand/examples/`.
4. Run `/mcp` and connect Metricool (publishing), Canva (Instagram images), vidIQ (YouTube
   research). See `docs/connectors.md` for optional ones. Scheduled routines (such as the
   Monday ideas run) are set up separately; see `docs/connectors.md`.

5. Install the marketing skills library (optional, recommended):

```bash
claude plugin marketplace add coreyhaines31/marketingskills
```

```bash
claude plugin install marketing-skills@marketingskills
```

## Daily use

| Say | Result |
|---|---|
| `topic ideas for <theme>` | ideas in `content/ideas/` |
| `write a blog on <topic>` | SEO-scored draft in `content/drafts/blog/` |
| `linkedin post about <topic>` | draft in `content/drafts/linkedin/` |
| `instagram post about <topic>` | caption, hashtags, image |
| `youtube video about <topic>` | title, description, script |
| `approve <file>` / `approve <file> for <datetime>` | moves to `content/approved/`, optionally with a schedule time |
| `repurpose <approved blog>` | three social drafts |
| `publish <file>` / `publish all approved` | schedules via Metricool, moves to `content/published/`; blog publishes locally until a host connector is added |
| `weekly review` | report in `reports/weekly/` |
| `/copywriting`, `/seo-audit`, `/ai-seo`, `/social`, ... | library skills from marketingskills; see CLAUDE.md "Marketing skills library" |

Nothing is published without you saying `approve` and then `publish`.

## Layout

- `brand/`: your profile, keywords, and example posts
- `content/`: the live queue (ideas, drafts, approved, published)
- `reports/`: SEO reports and weekly reviews
- `docs/examples/`: dry-run sample outputs for the placeholder Northwind brand; not part of
  the live queue, safe to delete

See `CLAUDE.md` for the rules and `docs/superpowers/specs/` for the design.
