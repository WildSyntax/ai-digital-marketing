---
name: setup-workspace
description: Check and set up everything this marketing workspace depends on (the marketing-skills library plugin, its brand context file, the brand profile, connectors) and print a status checklist with the exact fix for each gap. Use when the owner says "setup", "check setup", "is everything installed", on a new machine, or when another skill reports "library not installed".
---

# Setup workspace

Input: none.
Output: a status checklist in chat, and `.claude/product-marketing.md` if it was missing.
This skill never installs plugins itself: the owner runs the install commands.

## Dependencies this workspace uses

| Dependency | What it is | Needed by |
|---|---|---|
| `marketingskills` marketplace | GitHub repo `coreyhaines31/marketingskills` (MIT) registered as a plugin source | the plugin below |
| `marketing-skills@marketingskills` plugin | 53 marketing skills, invoked as `marketing-skills:<name>` | every drafting skill (optional steps) |
| `.claude/product-marketing.md` | context file the library skills read first | every library skill |
| `brand/profile.md` | brand voice, CTAs, rules | every workspace skill |
| `metricool`, `canva`, `vidiq` connectors (`.mcp.json`) | publishing, images, YouTube research | publish, instagram-post, youtube-video, topic-ideas |
| Vendored skills (`.claude/skills/*` with `metadata.source`) | 29 open-source skills copied into this repo; listed in `THIRD_PARTY_NOTICES.md` | owner, directly |
| FFmpeg 6.1+ and Python 3.10+ (optional) | local video tools | `ffmpeg-skill` only |

Library skills this workspace calls (all must exist): `copywriting`, `copy-editing`,
`content-strategy`, `ai-seo`, `schema`, `social`, `image`, `video`, `marketing-council`.

## Steps

1. **Library plugin.** Read `~/.claude/plugins/installed_plugins.json` and look for the key
   `marketing-skills@marketingskills`; note its `version`. Also check whether skills named
   `marketing-skills:*` are available in this session.
   - Installed and loaded: OK.
   - Installed but not loaded in this session: tell the owner to start a new session.
   - Not installed: give the owner these two commands to run in a terminal, each in its own
     `bash` code block, and explain that Claude cannot install plugins for them:

     ```bash
     claude plugin marketplace add coreyhaines31/marketingskills
     ```
     ```bash
     claude plugin install marketing-skills@marketingskills
     ```
     If a command fails with a GitHub 401, prefix it with `env -u GITHUB_TOKEN`.
     Then: start a new session and run `setup` again.
2. **Required library skills.** If installed, list
   `<installPath>/skills/` and confirm each required skill above exists. Name any missing one
   and suggest `claude plugin update marketing-skills@marketingskills`.
3. **Brand context file.** If `.claude/product-marketing.md` does not exist, create it with
   exactly this content, then commit `chore: add product-marketing context pointer`:

   ```markdown
   # Product marketing context

   The source of truth for this brand is `brand/profile.md` (brand, audience, tone, pillars,
   banned phrases, CTAs) and `brand/keywords.md` (keyword clusters). Read both before doing
   any marketing task. Do not copy their content here; edit them instead.

   Workspace rules for library skills: never create, move, or rename files under `content/`;
   return text and let the workspace skill write the file. Never use a phrase listed under
   "Banned words and phrases" in `brand/profile.md`.
   ```
4. **Brand profile.** Read `brand/profile.md`. List every line that still contains
   `Example:` or `example.com`. If any remain, warn that drafts will use sample brand values
   until they are replaced, and suggest `marketing-skills:product-marketing` or
   `marketing-skills:content-strategy` to help fill them in.
5. **Connectors.** For each key in `.mcp.json`, say whether its tools are available in this
   session. For each missing one, say what stops working without it (publish needs
   `metricool`; instagram-post and youtube-video and topic-ideas continue without `canva` /
   `vidiq`) and "connect via /mcp".
6. **Vendored skills.** For every `.claude/skills/*/SKILL.md` whose front matter has
   `metadata.source`: confirm a `LICENSE.txt` sits next to it and the skill appears in
   `THIRD_PARTY_NOTICES.md`; name any that fail. Run `ffmpeg -version` and `python3 --version`:
   if FFmpeg is missing or older than 6.1, or Python is older than 3.10, mark `ffmpeg-skill` as
   WARN with "install FFmpeg (e.g. `brew install ffmpeg`) to use video editing". Do not install
   anything yourself.
7. **Git.** Run `git status --short` and `git remote -v`; report uncommitted files and the
   remote.
8. Reply with a checklist, one line per item: `OK`, `ACTION`, or `WARN`, plus the fix.
   End with the next thing to try, e.g. "topic ideas" or "write a blog on <topic>".
