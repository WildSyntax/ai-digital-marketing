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

Snippet to add one (paste inside the `mcpServers` object):

```json
"wordpress": { "type": "http", "url": "https://public-api.wordpress.com/wpcom/v2/mcp/v1" }
```

After adding a blog host, update the `blog` branch of `.claude/skills/publish/SKILL.md`.

## Scheduled routines

Full config and prompts: `docs/routines.md`.

Recurring runs (for example the Monday topic-ideas run) are set up separately from this
repo, in Claude Code's scheduled-task settings. Routines never approve or publish.

## Skill library: coreyhaines31/marketingskills

Chosen over the alternatives on usage: ~58k GitHub stars and 8.5k forks, MIT, 53 skills,
updated within the last week; next-best collections have 100–3k stars. Pure prose skills,
no API keys, no paid dependencies for the core skills.

Per machine:

```
claude plugin marketplace add coreyhaines31/marketingskills
claude plugin install marketing-skills@marketingskills
```

To enable it for everyone who opens this folder, create `.claude/settings.json` with:

```json
{
  "extraKnownMarketplaces": {
    "marketingskills": { "source": { "source": "github", "repo": "coreyhaines31/marketingskills" } }
  },
  "enabledPlugins": { "marketing-skills@marketingskills": true }
}
```

Claude Code asks for confirmation before installing a plugin declared by a project. The skill
map (which library skill to use at which pipeline step) is in CLAUDE.md.
