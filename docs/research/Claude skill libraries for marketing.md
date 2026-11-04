# Vendor permissive skills, skip the star-farmed ones

The best skills to copy into this marketingskills-based workspace in November 2026 come from a small set of permissively licensed sources. Anthropic's two official repos, `anthropics/skills` and `anthropics/knowledge-work-plugins`, supply the Apache-2.0 design, brand, internal-comms, performance-report, sales, support, ops and legal-basics skills. Sergey Bulaev's MIT per-platform bundles fill YouTube, X, Threads, Instagram and TikTok depth. `social-media-skills/skills` (MIT, test-first evals) covers community, newsletter, podcast and voice. AgriciDaniel/claude-seo and rampstackco (both MIT) cover SEO briefs, clustering and brand voice. For business work, `phuryn/pm-skills`, `alirezarezvani/claude-skills` and `evolsb/claude-legal-skill` (all MIT) fill research, finance calculators, project management and contract review. Most gaps can be filled without a paid key; the "insights" and analytics-pulling skills are the exception, because nearly all of them need Apify, ScrapeCreators, your own Google OAuth or a hosted vendor MCP. Licensing knocks out several famous names: Anthropic's own docx/pptx/xlsx/pdf skills are proprietary, and Remotion, fal.ai, Vercel, coleam00's Excalidraw skill, ComposioHQ's list and several high-star marketing repos have restrictive or missing licences. One popular YouTube skill, Jakeschincariol/youtube-agent-skill, shows a star pattern consistent with manipulation. The ecosystem matters here: 2026 audits found 26–37% of public skills vulnerable and a few percent outright malicious. So the right method is to vendor a reviewed, commit-pinned snapshot of each skill, never to run an installer.

## Marketing gaps: platform depth is easy, newsletters and podcasts are thin

marketingskills already covers the categories. Its `social` skill handles LinkedIn, X, Instagram, TikTok, Reels, Shorts and listening, and it also has `community-marketing`, `video`, `emails`, `analytics`, `attribution` and `seo-audit`. What the third-party libraries add is depth: per-platform hook formula libraries, profile optimisers, reply drafters, hashtag strategists and trend mappers. They also add a few genuinely new capabilities: GSC/GA4 report pulling, structured performance reports, brand-voice and identity systems, keyword clustering, content briefs and podcast production ([marketingskills](https://github.com/coreyhaines31/marketingskills)).

**Platform growth.** Sergey Bulaev's bundles are the cleanest fit. All are **MIT, last committed 2026-10-27**, with 8–9 skills each and a `references/` folder per skill: youtube-skills (88 stars), x-skills (169), threads-skills (58), instagram-skills (743) and tiktok-skills (109) ([youtube-skills](https://github.com/sergebulaev/youtube-skills); [x-skills](https://github.com/sergebulaev/x-skills); [threads-skills](https://github.com/sergebulaev/threads-skills); [instagram-skills](https://github.com/sergebulaev/instagram-skills); [tiktok-skills](https://github.com/sergebulaev/tiktok-skills)). They have **no evals**, and the READMEs funnel users to Publora and Pixfaro through UTM-tagged links. The writer skills are draft-only and approval-gated ("Every skill shows you a draft first and waits for your OK"). The `*-audience-insights` skills need `APIFY_TOKEN`, and the bundled `lib/` clients (`apify_client.py`, `publora_client.py`, `pixfaro_client.py`) call paid services ([x-skills README](https://github.com/sergebulaev/x-skills)). Copy only the writer and planner skills, and leave out `lib/` and anything that publishes. This workspace already has `instagram-post` and `youtube-video` skills, so the Bulaev skills work best as reference material that those skills call or quote. They should not replace them.

**Community, newsletter, podcast and voice.** `social-media-skills/skills` (**MIT, 246 stars, last commit 2026-10-15**) is the strongest broad library for these gaps. It has 106 skills and 106 eval files "written before the skill body (test-first)". The useful picks are `community-management`, `email-and-newsletter`, `podcast-and-audiograms`, `analytics-and-reporting`, `voice-builder` and `brand-profile`. A few skills reference `ELEVENLABS_API_KEY` or `TRAFFIC_TOKEN`, so read each file before copying ([social-media-skills](https://github.com/social-media-skills/skills)). For deeper newsletter and podcast coverage, the only real option is `ur-grue/autopunk-media-skills`. It is **MIT and has 1,074 eval files**, with dedicated `newsletter/*` skills (edition writer, subject lines, sponsorship rate card) and `podcast/*` skills (show notes, guest research, ad reads). But it has **just 43 stars**, its last commit was 2026-08-31, and its scripts were not scanned ([autopunk](https://github.com/ur-grue/autopunk-media-skills)). There is no dedicated Kit/ConvertKit skill. beehiiv's official advisor has **no licence** ([beehiiv](https://github.com/beehiiv/beehiiv-newsletter-advisor)).

**Brand voice and identity.** Three sources compete. rampstackco `brand-voice` (180 lines) and `brand-identity` (203 lines) are MIT and come from a 1,033-star repo with no evals ([rampstackco](https://github.com/rampstackco/claude-skills)). `fatihaydost/brand-identity-skill` is MIT, has 298 stars and **255 eval files**, and says "No telemetry; nothing is uploaded". It also ships 61 scripts that must be read before copying ([fatihaydost](https://github.com/fatihaydost/brand-identity-skill)). Anthropic's `brand-guidelines` is Apache-2.0. It encodes Anthropic's own brand and is meant as a template to swap your palette and type into ([anthropics/skills](https://github.com/anthropics/skills/tree/main/skills)). The two `brand-identity` skills share a name, so pick one.

**Analytics reporting and SEO briefs.** Anthropic's `marketing/skills/performance-report` (**392 lines, Apache-2.0**) is the best structured reporting skill ([knowledge-work-plugins](https://github.com/anthropics/knowledge-work-plugins)). From AgriciDaniel/claude-seo (**MIT, 26,589 stars, 79 test/eval files**), the picks are `seo-content-brief` (256 lines) and `seo-cluster`. `seo-google` (377 lines) pulls GSC and GA4 through your own Google OAuth, with OAuth safety tests. Its siblings `seo-audit`, `seo-schema`, `seo-geo` and `seo-programmatic` duplicate marketingskills, so skip them ([claude-seo](https://github.com/AgriciDaniel/claude-seo)). For deep analytics method, `clamp-sh/analytics-skills` covers traffic-change diagnosis, anomaly detection and experiment reading. It is MIT, but it has 9 stars and assumes an analytics MCP ([clamp-sh](https://github.com/clamp-sh/analytics-skills)).

| Skill(s) | Repo / licence | Stars / last activity | Dependencies | Overlap with marketingskills | Quality signals / red flags |
|---|---|---|---|---|---|
| yt-, x-, threads-, ig-, tt- writer and planner skills | sergebulaev/* — MIT | 58–743 / 2026-10-27 | None for writers; Apify, Publora and Pixfaro for insights and publishing | Deepens `social`, `video` | Deep references, no evals; UTM vendor funnels |
| community-management, email-and-newsletter, podcast-and-audiograms, voice-builder, analytics-and-reporting | social-media-skills/skills — MIT | 246 / 2026-10-15 | Mostly prompt-only; scattered ElevenLabs refs | Partial: `community-marketing`, `emails`, `analytics` | Test-first evals; low stars |
| newsletter/*, podcast/* | ur-grue/autopunk-media-skills — MIT | 43 / 2026-08-31 | Not scanned | Partial: `emails` | 1,074 evals; very low adoption |
| performance-report, brand-review | anthropics/knowledge-work-plugins — Apache-2.0 | 34,707 / 2026-11-04 | Plugin `.mcp.json` lists HubSpot, Amplitude and others; works on pasted data | Partial: `analytics` | Official; keep NOTICE/attribution |
| seo-content-brief, seo-cluster, seo-google | AgriciDaniel/claude-seo — MIT | 26,589 / 2026-10-22 | `seo-google`: own Google OAuth; optional paid extensions | Siblings collide in function with `seo-audit`, `schema`, `ai-seo`, `programmatic-seo` | Tests and 129 references; scripts not scanned |
| brand-voice, brand-identity, content-brief-authoring | rampstackco/claude-skills — MIT | 1,033 / 2026-10-19 | None | None direct | No evals; very broad repo (321 SKILL.md incl. dist copies) |
| brand-identity | fatihaydost/brand-identity-skill — MIT | 298 / 2026-11-01 | 61 local scripts | None | 255 evals; no telemetry claim |
| engagement-inbox-manager, crisis-response-planner, voice-dossier-builder | aaron-he-zhu/aaron-marketing-skills — Apache-2.0 | 3,068 / 2026-11-04 | Not scanned | Many other folders overlap | 374 eval files ([repo](https://github.com/aaron-he-zhu/aaron-marketing-skills)) |

## Content production: Anthropic's Apache-2.0 skills lead, its office skills are off-limits

`anthropics/skills` (about 187k stars, last commit 2026-10-28) has no root licence. Licences are set per skill. **canvas-design, algorithmic-art, brand-guidelines, frontend-design, web-artifacts-builder, theme-factory and slack-gif-creator each ship an Apache-2.0 LICENSE.txt** and can be vendored ([canvas-design LICENSE](https://github.com/anthropics/skills/blob/main/skills/canvas-design/LICENSE.txt); [brand-guidelines LICENSE](https://github.com/anthropics/skills/blob/main/skills/brand-guidelines/LICENSE.txt)). The **docx, pptx, xlsx and pdf skills are "© 2025 Anthropic, PBC. All rights reserved."** Their terms forbid copying, derivative works and distribution outside Anthropic's services ([docx LICENSE](https://github.com/anthropics/skills/blob/main/skills/docx/LICENSE.txt)). That is not a practical loss, because this environment already exposes them as built-in `anthropic-skills:docx/pptx/xlsx/pdf`. Use those in place and do not vendor them. `doc-coauthoring` has no LICENSE.txt at all, so treat it as unlicensed and use the built-in copy instead ([doc-coauthoring](https://github.com/anthropics/skills/tree/main/skills/doc-coauthoring)).

For office files you control, `appautomaton/document-SKILLs` is the copyable alternative. It is MIT, has 181 stars, was pushed 2026-10-15, and ships a `tests/` suite covering docx, pptx, xlsx, pdf and ooxml ([repo](https://github.com/appautomaton/document-SKILLs)). Its clean-room status is **unverified**. One third-party summary called it "based on Anthropic's official skills", so diff its scripts against Anthropic's before trusting the MIT grant. OpenAI's `pdf` skill is Apache-2.0 ([openai/skills](https://github.com/openai/skills)). For slides, `zarazhangrui/frontend-slides` builds HTML decks; it is MIT, has 31,877 stars and was last pushed 2026-06-23 ([repo](https://github.com/zarazhangrui/frontend-slides)).

For video, **`kajisho5/ffmpeg-skill` is the standout**. It is MIT with 4,518 stars and was pushed 2026-10-31. The README promises "No cloud · No API keys · Python standard library", and the repo includes reproducible demos and a `doctor` check ([repo](https://github.com/kajisho5/ffmpeg-skill)). Copy its files directly; do not run `npx ffmpeg-skill`. Remotion's skills are official and current, but the skills repo has **no LICENSE file**, and the monorepo's Remotion License requires a paid company licence above a size threshold ([Remotion LICENSE](https://github.com/remotion-dev/remotion/blob/main/LICENSE.md)).

For diagrams, the MIT options are `WH-2099/mermaid-skill` (299 stars) ([repo](https://github.com/WH-2099/mermaid-skill)), `axtonliu/axton-obsidian-visual-skills` (3,678 stars) ([repo](https://github.com/axtonliu/axton-obsidian-visual-skills)) and `yctimlin/mcp_excalidraw`. mcp_excalidraw has 2,611 stars, needs no keys, and is an MCP server plus skill rather than a pure skill ([README](https://github.com/yctimlin/mcp_excalidraw)). For carousels, the MIT option is `itchernetski/threads-carousel-claude-skill` (120 stars) ([repo](https://github.com/itchernetski/threads-carousel-claude-skill)). The higher-star `op7418/guizang-social-card-skill` is AGPL-3.0 ([repo](https://github.com/op7418/guizang-social-card-skill)).

Every image-generation skill needs a paid key or a vendor account:

| Skill | Licence | Requires |
|---|---|---|
| OpenAI `imagegen` | Apache-2.0 | `OPENAI_API_KEY` ([SKILL.md](https://github.com/openai/skills/blob/main/skills/.system/imagegen/SKILL.md)) |
| `kingbootoshi/nano-banana-2-skill` | MIT | `GEMINI_API_KEY` ([README](https://github.com/kingbootoshi/nano-banana-2-skill)) |
| `replicate/skills` | Apache-2.0 | Remote MCP at `mcp.replicate.com` ([repo](https://github.com/replicate/skills)) |
| `canva-sdks/canva-skills` | Apache-2.0 | Canva connector ([repo](https://github.com/canva-sdks/canva-skills)) |

The Canva skills are the most relevant to this workspace, because it already uses Canva for Instagram. Their `brand-check` and `resize-for-social-media` skills fit that existing pipeline directly.

| Skill(s) | Repo / licence | Stars / last activity | Dependencies | Overlap | Quality / red flags |
|---|---|---|---|---|---|
| brand-guidelines, canvas-design, theme-factory, frontend-design, web-artifacts-builder, algorithmic-art, slack-gif-creator | anthropics/skills — Apache-2.0 per skill | ~187k / 2026-10-28 | Python (Pillow, imageio); web-artifacts-builder needs Node, Vite, Parcel | `image` (light) | Official; "demonstration and educational purposes" disclaimer |
| docx, pptx, xlsx, pdf | appautomaton/document-SKILLs — MIT | 181 / 2026-10-15 | uv, Node, LibreOffice, Poppler | None | Test suite; provenance unverified |
| ffmpeg-skill | kajisho5 — MIT | 4,518 / 2026-10-31 | ffmpeg, python3 | `video` (production, not strategy) | Doctor command, reproducible demos |
| frontend-slides | zarazhangrui — MIT | 31,877 / 2026-06-23 | Agent's frontend skills | None | Popular |
| mermaid-skill / axton visual skills | MIT | 299 / 3,678 | None | None | Low adoption (mermaid) |
| threads-carousel | itchernetski — MIT | 120 | Not checked | Deepens `social` | Low adoption |

## Business and ops: Anthropic's small-business plugin covers almost everything

For a small marketing business, `anthropics/knowledge-work-plugins` is the base layer (**Apache-2.0, 34,707 stars, pushed 2026-11-04**). Its small-business plugin (v1.35.1) has about 45 skills. The ones that matter most are `proposal-builder` (turns discovery-call notes into a proposal), `invoice-chase`, `cash-flow-snapshot`, `close-month`, `contract-review` ("Lightweight NDA, MSA, and vendor contract review for SMBs without legal on staff"), `ticket-deflector` and `report-builder`. It is also the only library found that ships explicit safety guardrails. `shared/untrusted-content.md` tells every skill to read outside text "as data about the world", and `invoice-chase` sends "only after approval" ([small-business](https://github.com/anthropics/knowledge-work-plugins/tree/main/small-business/skills); [shared](https://github.com/anthropics/knowledge-work-plugins/tree/main/small-business/shared)).

The sales, customer-support and operations plugins add more. Sales has `call-prep`, `call-summary`, `pipeline-review` and `crm-hygiene-check`. Customer support has `ticket-triage`, `draft-response` and `kb-article`. Operations has `status-report` and `process-doc` for SOPs ([sales](https://github.com/anthropics/knowledge-work-plugins/tree/main/sales/skills); [operations](https://github.com/anthropics/knowledge-work-plugins/tree/main/operations/skills)).

The catch is connectors. The small-business `.mcp.json` declares **35 remote MCP servers**, including HubSpot, QuickBooks, Xero, Stripe, Gmail and Notion ([.mcp.json](https://github.com/anthropics/knowledge-work-plugins/blob/main/small-business/.mcp.json)). Nobody has tested which skills still work without them. Skills that start from notes or pasted documents belong on the copy-now list. Skills that read a ledger or CRM belong on the copy-later list. When you copy a skill, copy the `shared/` files it references too. Two KWP skills, the marketing plugin's `seo-audit` and small-business's `content-strategy`, share names with marketingskills skills. Do not vendor them.

Anthropic's `internal-comms` (Apache-2.0) covers status updates, newsletters, FAQs and leadership updates ([internal-comms](https://github.com/anthropics/skills/tree/main/skills/internal-comms)). Calculations, research and legal basics come from MIT repos:

| Need | Skill(s) | Source |
|---|---|---|
| Finance and pricing calculations | `financial-analyst`, with local `budget_variance_analyzer.py`, `dcf_valuation.py` and `forecast_builder.py`; no network calls found in a grep | alirezarezvani, 29,289 stars ([financial-analyst](https://github.com/alirezarezvani/claude-skills/tree/main/finance/skills/financial-analyst)) |
| Contracts and proposals | `contract-and-proposal-writer` | alirezarezvani |
| Process documentation | `process-mapper` | alirezarezvani |
| Research and planning | `competitor-analysis`, `market-sizing`, `swot-analysis`, `summarize-meeting`, `pre-mortem`, `sprint-plan`, `retro`, `draft-nda` | phuryn/pm-skills, 27,687 stars, markdown-only ([repo](https://github.com/phuryn/pm-skills)) |
| Contract review | a single CUAD-grounded skill (41 risk categories) that outputs redlines | evolsb/claude-legal-skill, 495 stars ([repo](https://github.com/evolsb/claude-legal-skill)) |
| Startup financial modelling | `startup-financial-modeling`, `kpi-dashboard-design`, `data-storytelling` | wshobson/agents, 42,192 stars ([repo](https://github.com/wshobson/agents)) |

Watch three details when copying these. alirezarezvani's `marketing-skill/` folder mirrors marketingskills names (`page-cro`, `copy-editing`, `pricing-strategy`), and its docs show a `curl | bash` installer, so take only the business folders ([docs](https://github.com/alirezarezvani/claude-skills/blob/main/docs/plugins/index.md)). evolsb ships its skill as lowercase `skill.md`, so rename it to `SKILL.md` and record that as a modification. For heavy modelling, `anthropics/financial-services` (Apache-2.0) is available, but it targets investment banking and is overkill for this workspace ([repo](https://github.com/anthropics/financial-services)).

| Skill(s) | Repo / licence | Stars / last activity | Dependencies | Overlap | Quality / red flags |
|---|---|---|---|---|---|
| proposal-builder, contract-review, ticket-deflector, report-builder | KWP small-business — Apache-2.0 | 34,707 / 2026-11-04 (folder 2026-09-15) | Optional MCPs; `shared/` guardrail files | Its marketing skills overlap; `content-strategy` collides by name | Approval-gated; untrusted-content policy |
| call-prep, call-summary, pipeline-review | KWP sales — Apache-2.0 | same | HubSpot, Gong and similar MCPs | `draft-outreach` duplicates `cold-email`, `prospecting` | Official |
| ticket-triage, draft-response, kb-article; status-report, process-doc | KWP customer-support, operations — Apache-2.0 | same | Intercom, Notion and similar MCPs (optional) | None | Official |
| internal-comms | anthropics/skills — Apache-2.0 | ~187k / 2026-10-28 | None | None | Official |
| financial-analyst, contract-and-proposal-writer, process-mapper | alirezarezvani — MIT | 29,289 / 2026-11-03 | Local Python | `pricing-strategist` duplicates `pricing` | Uneven depth across 410 skills; curl\|bash in docs |
| competitor-analysis, market-sizing, swot, pre-mortem, summarize-meeting, sprint-plan, retro, draft-nda | phuryn/pm-skills — MIT | 27,687 / 2026-10-29 | None | `competitor-analysis` overlaps `competitors`; `pricing-strategy` overlaps `pricing` | Markdown-only |
| contract review | evolsb/claude-legal-skill — MIT | 495 / 2026-07-23 | None | None | CUAD-grounded; file named `skill.md` |
| startup-financial-modeling, kpi-dashboard-design | wshobson/agents — MIT | 42,192 / 2026-11-02 | None | None | Broad repo |

## Licences, look-alike repos and installers knock out famous names

Missing or restrictive licences cause most exclusions. Treat no licence as all rights reserved. Repos with **no licence or NOASSERTION** include:

- irinabuht12-oss/marketing-skills, with 6,810 stars ([repo](https://github.com/irinabuht12-oss/marketing-skills))
- beehiiv's advisor
- borghei/Claude-Skills, stevenflanagan1/social-ai-team and cofoundy/brand-skills ([borghei](https://github.com/borghei/Claude-Skills))
- coleam00's Excalidraw skill, with 5,185 stars ([repo](https://github.com/coleam00/excalidraw-diagram-skill))
- fal-ai-community/skills ([README](https://github.com/fal-ai-community/skills/blob/main/README.md))
- ComposioHQ/awesome-claude-skills ([repo](https://github.com/ComposioHQ/awesome-claude-skills))
- 199-biotechnologies' deep-research skill, whose README claims MIT but which ships no LICENSE file ([repo](https://github.com/199-biotechnologies/claude-deep-research-skill))
- vercel-labs/agent-skills, whose README also claims MIT without a LICENSE file ([repo](https://github.com/vercel-labs/agent-skills))

Other repos carry **non-commercial or no-derivatives** terms: deanpeters/Product-Manager-Skills is CC BY-NC-SA ([repo](https://github.com/deanpeters/Product-Manager-Skills)), and lawve-ai's root licence is CC BY-NC-ND ([repo](https://github.com/lawve-ai/awesome-legal-skills)). `tfriedel/claude-office-skills` copies Anthropic's proprietary skills "verbatim" ([README](https://github.com/tfriedel/claude-office-skills/blob/main/README.md)). AGPL-3.0 skills such as guizang and dashi-ppt fall outside the permitted licence list for this repo.

Security flags are rarer but sharper. **Jakeschincariol/youtube-agent-skill has 4,540 stars, yet the same author's x-agent-skill has 71.** At least four empty look-alike repos created in September and October 2026 each carry stars; one is described as "Install this skill, then...". That pattern points to star or SEO manipulation, or a lure campaign. The original code looked benign, but its SKILL.md files are thin (58 lines for `yt-script`), and Bulaev's bundles cover the same ground better ([GitHub search](https://github.com/search?q=youtube-agent-skill&type=repositories)). The archify (93k) and ECC (297k) star counts may also be inflated; nobody checked adoption beyond stars ([archify](https://github.com/tt-a1i/archify)).

Some skills run code or instructions from outside the repo:

- fal's genmedia skill tells the agent to run `curl https://genmedia.sh/install -fsS | bash` ([SKILL.md](https://github.com/fal-ai-community/skills/blob/main/skills/genmedia/SKILL.md)).
- claude-office-skills shows `curl | bash` against a third-party domain, molt.bot ([README](https://github.com/claude-office-skills/skills)).
- Vercel's `web-design-guidelines` fetches its rules from a remote URL on every run, so its behaviour can change after you review it ([SKILL.md](https://github.com/vercel-labs/agent-skills/blob/main/skills/web-design-guidelines/SKILL.md)). Snyk calls this a known route for skills to "turn malicious after review" ([Snyk](https://snyk.io/blog/toxicskills-malicious-ai-agent-skills-clawhub/)).

The broader numbers justify the caution. Liu et al. found **26.1% of 31,132 skills vulnerable**, and skills that bundle scripts were **2.12× more likely** to be vulnerable ([arXiv 2601.10338](https://arxiv.org/abs/2601.10338)). Snyk confirmed **76 malicious payloads** among 3,984 skills ([Snyk](https://snyk.io/blog/toxicskills-malicious-ai-agent-skills-clawhub/)). Koi found **341 malicious ClawHub skills** delivering Atomic Stealer through fake prerequisites ([Koi Security](https://koi.ai/blog/clawhavoc-341-malicious-clawedbot-skills-found-by-the-bot-they-were-targeting)).

Name collisions have a specific mechanism. Plugin skills are namespaced (`/marketing-skills:social`), so a vendored project skill never shadows them. If both are present, both load ([Claude Code skills docs](https://code.claude.com/docs/en/skills)). The real risk is two near-identical descriptions confusing automatic skill selection. Precedence is personal over project, so a teammate's `~/.claude/skills` copy silently wins over the repo's. Distinct names avoid both problems. Names must also avoid "claude" and "anthropic" ([best practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices)).

## Ranked "copy now" shortlist

The criteria for this list: MIT or Apache-2.0, no paid key, and no name clash with a marketingskills skill or a workspace skill (`topic-ideas`, `blog-post`, `seo-check`, `linkedin-post`, `instagram-post`, `youtube-video`, `repurpose`, `publish`, `setup-workspace`). Every item still has to pass the checklist below. Items whose repo scripts have not been scanned yet are marked ⚠.

| Rank | Skill(s) | Source @ licence | Fills | Note |
|---|---|---|---|---|
| 1 | `brand-guidelines` (rebrand to your palette and type), `theme-factory`, `canvas-design` | anthropics/skills, Apache-2.0 | Brand guidelines, design, posters/PDF | Mark modified files; carry LICENSE.txt |
| 2 | `performance-report`, `brand-review` | KWP marketing, Apache-2.0 | Analytics reporting, brand QA | Works on pasted data; drop `.mcp.json` |
| 3 | `internal-comms` | anthropics/skills, Apache-2.0 | Business writing | — |
| 4 | `proposal-builder`, `contract-review` (+ the `shared/` files they reference), `status-report`, `process-doc`, `draft-response`, `kb-article` | KWP small-business, operations, customer-support, Apache-2.0 | Sales, legal basics, PM, support | Rename `contract-review` if you also take evolsb |
| 5 | Bulaev writer skills: `yt-hook-scripter`, `yt-title-optimizer`, `yt-description-writer`, `x-thread-builder`, `x-post-writer`, `threads-post-writer`, `ig-carousel-planner`, `ig-caption-writer`, `ig-hashtag-strategist`, `tt-hook-scripter`, `tt-trend-mapper` | sergebulaev/*, MIT | YouTube, X, Threads, IG, TikTok growth | Exclude `lib/`, `*-audience-insights` and publishing; strip UTM links |
| 6 | `community-management`, `email-and-newsletter`, `podcast-and-audiograms`, `voice-builder` | social-media-skills/skills, MIT | Community, newsletter, podcast, voice | Remove ElevenLabs steps if present; keep evals |
| 7 | `seo-content-brief`, `seo-cluster` ⚠ | AgriciDaniel/claude-seo, MIT | SEO briefs, clustering | Feeds the workspace `seo-check`; does not replace it |
| 8 | `ffmpeg-skill` | kajisho5, MIT | Video editing | Copy files; skip the `npx` installer |
| 9 | `brand-voice` (rampstackco) **or** `brand-identity` (fatihaydost ⚠, read all 61 scripts) | MIT | Brand voice and identity | Pick one `brand-identity` to avoid a self-collision |
| 10 | `competitor-analysis`→rename, `market-sizing`, `swot-analysis`, `summarize-meeting`, `pre-mortem`, `retro`, `sprint-plan`, `draft-nda` | phuryn/pm-skills, MIT | Research, PM, legal basics | Skip `pricing-strategy` (overlaps `pricing`) |
| 11 | `financial-analyst`, `contract-and-proposal-writer`, `process-mapper` ⚠ | alirezarezvani, MIT | Finance, business writing | Business folders only; local Python |
| 12 | contract-review skill | evolsb/claude-legal-skill, MIT | Legal basics | Rename `skill.md` to `SKILL.md`; name it `contract-redline` |
| 13 | `frontend-slides`; `mermaid-skill`; `threads-carousel` ⚠ | zarazhangrui, WH-2099, itchernetski, MIT | Slides, diagrams, carousels | Smaller authors; read every file |
| 14 | `newsletter/*`, `podcast/*` picks ⚠ | ur-grue/autopunk-media-skills, MIT | Deeper newsletter and podcast work | 43 stars; only if #6 falls short |

## "Copy later": needs a key, OAuth or a connector

Copy these only once the account or connector is in place, and connect them through `/mcp`, never through secrets in the repo, as workspace rule 6 requires.

| Skill(s) | Licence | Blocker |
|---|---|---|
| claude-seo `seo-google` | MIT | Your own Google OAuth for GSC and GA4 (free, but it is a credential) |
| canva-sdks `brand-check`, `resize-for-social-media` | Apache-2.0 | Canva connector (fits the existing Instagram pipeline) |
| KWP `invoice-chase`, `cash-flow-snapshot`, `close-month`, `call-prep`, `pipeline-review`, `crm-hygiene-check`, `ticket-triage` | Apache-2.0 | Ledger, CRM and helpdesk MCPs |
| KWP brand-voice partner skills (`discover-brand`, `guideline-generation`, `brand-voice-enforcement`) | Apache-2.0 | Notion, Box, M365 and Figma MCPs ([brand-voice](https://github.com/anthropics/knowledge-work-plugins/tree/main/partner-built/brand-voice)) |
| Bulaev `*-audience-insights` | MIT | Paid `APIFY_TOKEN` |
| ScrapeCreators social-research skills (`outlier-post-finder`, `comment-mining`) | MIT | Paid `SCRAPECREATORS_API_KEY` ([repo](https://github.com/ScrapeCreators/social-media-research-skills)) |
| clamp-sh analytics skills | MIT | An analytics MCP; 9 stars |
| OpenAI `imagegen`, nano-banana-2, replicate/skills | Apache-2.0 / MIT | `OPENAI_API_KEY`, `GEMINI_API_KEY`, Replicate token |
| seranking/seo-skills, Ryze open-seo-mcp-skills, Dataslayer | MIT | Paid SE Ranking key; Ryze's hosted MCP sees your GSC, GA4 and ads data; Dataslayer's paid MCP ([Ryze](https://github.com/Ryze-AI-Adgent/open-seo-mcp-skills)) |
| yctimlin/mcp_excalidraw | MIT | An MCP server, not a skill; core runs locally |
| appautomaton/document-SKILLs | MIT | No key, but copy only after a provenance diff against Anthropic's scripts; the built-in `anthropic-skills` already cover this |
| Arin117Kaushik/substack-skills | MIT | `substack-publisher` uses the full-account `substack.sid` cookie ([repo](https://github.com/Arin117Kaushik/substack-skills)) |

## "Do not copy"

| Item | Reason |
|---|---|
| anthropics/skills `docx`, `pptx`, `xlsx`, `pdf` | Proprietary; copying and derivatives forbidden. Use the built-ins |
| anthropics/skills `doc-coauthoring` | No licence file; use the built-in |
| tfriedel/claude-office-skills | Verbatim copy of proprietary skills, no licence |
| Jakeschincariol/youtube-agent-skill and look-alike repos | Star-pattern manipulation or lure signs; thin skills; Bulaev covers the same ground |
| irinabuht12-oss/marketing-skills, beehiiv advisor, borghei, stevenflanagan1, cofoundy, coleam00 excalidraw, ComposioHQ list and skills, 199-bio deep research | No licence or NOASSERTION (all rights reserved) |
| deanpeters/Product-Manager-Skills, lawve-ai root | Non-commercial or no-derivatives terms |
| remotion-dev/skills | No LICENSE file; Remotion License needs a paid licence above a company-size threshold |
| fal-ai-community/skills | No licence, plus a `curl \| bash` prerequisite |
| vercel-labs/agent-skills `web-design-guidelines` | No LICENSE file; fetches remote instructions on every run |
| claude-office-skills/skills | `curl \| bash` from a third-party domain; stale since January 2026; duplicates better sources |
| guizang social cards, dashi-ppt | AGPL-3.0, outside the allowed licence list |
| genspark-ai/genoffice | A full app, not a skill; can route models through the Genspark proxy |
| alirezarezvani `marketing-skill/*`, KWP marketing `seo-audit`, KWP small-business `content-strategy`, claude-seo `seo-audit`/`seo-schema`/`seo-geo`/`seo-programmatic` | Duplicate or collide with marketingskills |

## Vendoring and vetting checklist

These steps follow the Apache-2.0 §4 conditions ([Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0)), Anthropic's plugin security guidance ([Plugin security](https://code.claude.com/docs/en/plugins/security.md)), the OWASP Agentic Skills Top 10 ([OWASP](https://owasp.github.io/www-project-agentic-skills-top-10/ast01)) and Snyk's findings, adapted to this repo's rules.

| # | Step |
|---|---|
| 1 | **Licence gate.** Open the actual LICENSE or LICENSE.txt in the skill folder and the repo root; GitHub's detection is not enough. Allow only MIT, Apache-2.0, BSD, CC0 or CC-BY. No licence means do not copy. |
| 2 | **Fetch by git at a commit, never by installer.** `git clone`, then `git checkout <sha>`, then copy the folder. No `curl \| bash`, no `npx skills add -y`, no `install.sh`, no `npx <pkg>`. Never clone a look-alike repo name. |
| 3 | **Read every file**: SKILL.md, `references/`, `scripts/`, `assets/`, and for plugins `.mcp.json`, `hooks/hooks.json` and `bin/`. Reject prerequisites that download binaries, password-protected archives, base64 or Unicode-obfuscated strings, runtime URL fetches of instructions, reads of `.env`, keys or memory files, and "disable safeguards" text. |
| 4 | **Strip what you won't use**: `lib/` API clients, `.mcp.json`, UTM and sign-up links, publishing steps. Workspace rules apply: no skill may create or move files under `content/approved` or `content/published`. |
| 5 | **Check frontmatter.** `name` must match the folder, be lowercase and hyphenated, be at most 64 characters, and avoid "claude" and "anthropic". `description` must be at most 1,024 characters. Body under 500 lines. Review any `allowed-tools`, `hooks` or `` !`cmd` `` lines. Add `disable-model-invocation: true` to anything with side effects. Run `skills-ref validate` ([spec](https://agentskills.io/specification)). |
| 6 | **Rename to avoid collisions** with marketingskills and workspace skills (for example `contract-redline`, `podcast-show-notes`). A rename is a modification, so record it. |
| 7 | **Attribution.** Keep LICENSE.txt in each skill folder. Reproduce any upstream NOTICE text in the repo NOTICE. Add `license:` and `metadata: {source: "<owner/repo>@<sha>", path: "<upstream path>"}` to frontmatter. Mark changed files as modified, which Apache-2.0 requires. |
| 8 | **Record in `THIRD_PARTY_NOTICES.md` (or `vendor.lock`)**: upstream URL, commit SHA, licence, date and local changes, one row per skill. |
| 9 | **Scan as a second opinion**, for example `uvx mcp-scan@latest --skills`. Scanners miss things, so this does not replace step 3. |
| 10 | **Run in containment.** Set `"disableSkillShellExecution": true` unless a skill needs it. Run scripts only with `python -I` and only after reading them. Keep secrets out of the repo and authenticate connectors via `/mcp`. |
| 11 | **Update deliberately.** Re-vendor at a new SHA, then review the diff. Never auto-update. |
| 12 | **Docs in the same commit.** Update `README.md` and `docs/skill-library.md`, then push to `origin main`, as workspace rule 9 requires. |

## Conclusion

The research turns "which library is best" into "which files are safe to own". No single library beats marketingskills on its own turf. The value comes from assembling about 40 narrowly chosen skills from five or six reputable sources, with Anthropic's Apache-2.0 material as the trust anchor and MIT specialists for platform depth. Two figures should shape the policy: script-bundling skills are twice as likely to be vulnerable, and star counts can be farmed. Together they make prompt-only, eval-backed skills the default choice and make every bundled script an explicit review decision.

Several points remain open. Nobody has run these skills' evals or compared output quality. Nobody has tested whether the KWP skills degrade gracefully without connectors. The scripts in claude-seo, alirezarezvani, rampstackco, aaron-he-zhu and autopunk have not been scanned. appautomaton's provenance is unconfirmed. Treat the shortlist as a well-founded starting order, not a verdict, and let the checklist do the final filtering.
