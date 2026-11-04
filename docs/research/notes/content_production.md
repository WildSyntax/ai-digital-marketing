# Content-production Agent Skills (SKILL.md): documents, images, video, design, diagrams, carousels, landing pages (as of 5 Nov 2026)

Method: I pulled repo metadata (stars, `pushed_at`, SPDX licence) from the GitHub REST API (`gh api repos/<owner>/<repo>`) on 2026-11-05. I read LICENSE / LICENSE.txt / README / SKILL.md files directly from the repos. Stars and dates are as of that day. "pushed" is the last push to any branch. For anthropics/skills, remotion-dev/skills, tfriedel and the other repos where I listed commits, it matched the last commit. A "licence=none" result means GitHub found no recognisable root licence file.

## 1. Candidate list with repo, owner, stars, last activity, licence

### Takeaway
The strongest skills that can legally be copied are Anthropic's Apache-2.0 design and web skills (canvas-design, algorithmic-art, brand-guidelines, frontend-design, web-artifacts-builder, theme-factory, slack-gif-creator) and appautomaton/document-SKILLs (MIT office suite with tests). Also in that group: kajisho5/ffmpeg-skill (MIT), OpenAI's Apache-2.0 pdf and imagegen skills, Canva's and Replicate's Apache-2.0 vendor skills, and several MIT diagram and carousel skills. Some high-profile repos have restrictive or missing licences: Anthropic's docx/pptx/xlsx/pdf, Remotion's skills, fal.ai's skills, Vercel's (README says MIT, no LICENSE file), and coleam00's Excalidraw skill.

### Cited Findings

**A. Anthropic official: anthropics/skills** (https://github.com/anthropics/skills)
- 187,360 stars. Last commit 2026-10-28 ("Update mcp-builder skill: teach v2 of the MCP TypeScript SDK (#2087)"). No root SPDX licence; licences are per skill in LICENSE.txt. Skills present: academy-guide, algorithmic-art, brand-guidelines, canvas-design, claude-api, discernment-nudge, doc-coauthoring, docx, frontend-design, internal-comms, mcp-builder, pdf, pptx, skill-creator, slack-gif-creator, theme-factory, web-artifacts-builder, webapp-testing, xlsx — [GitHub API / repo tree](https://github.com/anthropics/skills/tree/main/skills)
- Apache-2.0 (LICENSE.txt is the Apache License 2.0 text): canvas-design, algorithmic-art, brand-guidelines, frontend-design, web-artifacts-builder, theme-factory, slack-gif-creator — [canvas-design/LICENSE.txt](https://github.com/anthropics/skills/blob/main/skills/canvas-design/LICENSE.txt), [brand-guidelines/LICENSE.txt](https://github.com/anthropics/skills/blob/main/skills/brand-guidelines/LICENSE.txt), [web-artifacts-builder/LICENSE.txt](https://github.com/anthropics/skills/blob/main/skills/web-artifacts-builder/LICENSE.txt)
- **Proprietary / source-available: docx, pptx, xlsx, pdf.** Each LICENSE.txt starts "© 2025 Anthropic, PBC. All rights reserved." It says use "is governed by your agreement with Anthropic regarding use of Anthropic's services" (Consumer or Commercial Terms). It then lists ADDITIONAL RESTRICTIONS under which users may not: "Extract these materials from the Services or retain copies of these materials outside the Services"; "Reproduce or copy these materials, except for temporary copies created automatically during authorized use of the Services"; "Create derivative works based on these materials"; "Distribute, sublicense, or transfer these materials to any third party"; "Reverse engineer, decompile, or disassemble these materials." It closes: "The receipt, viewing, or possession of these materials does not convey or imply any license or right beyond those expressly granted above." — [docx/LICENSE.txt](https://github.com/anthropics/skills/blob/main/skills/docx/LICENSE.txt) (identical in [pptx](https://github.com/anthropics/skills/blob/main/skills/pptx/LICENSE.txt), [xlsx](https://github.com/anthropics/skills/blob/main/skills/xlsx/LICENSE.txt), [pdf](https://github.com/anthropics/skills/blob/main/skills/pdf/LICENSE.txt))
- The README confirms the split: "Many skills in this repo are open source (Apache 2.0)… the document creation & editing skills… docx, pdf, pptx, and xlsx… are source-available, not open source, but we wanted to share these with developers as a reference" — [anthropics/skills README](https://github.com/anthropics/skills/blob/main/README.md)

**B. Office/PDF alternatives you can copy**
- **appautomaton/document-SKILLs**: MIT (LICENSE: "Copyright (c) 2026 appautomaton"). 181 stars, pushed 2026-10-15. Skills: docx, pptx, xlsx, pdf. Installs as a Claude Code plugin (`/plugin marketplace add appautomaton/document-SKILLs`). Has a `tests/` suite (test_docx.py, test_pptx.py, test_xlsx.py, test_pdf.py, test_ooxml.py). Supports tracked changes and comments in docx — [repo](https://github.com/appautomaton/document-SKILLs), [README](https://github.com/appautomaton/document-SKILLs/blob/main/README.md)
- **openai/skills: `pdf` (curated) and `imagegen` (system)**, per-skill Apache-2.0 LICENSE.txt. Repo has 28,519 stars, pushed 2026-10-28, and no root licence. I found no docx/pptx/spreadsheet skills in the current tree — [openai/skills](https://github.com/openai/skills), [pdf/LICENSE.txt](https://github.com/openai/skills/blob/main/skills/.curated/pdf/LICENSE.txt)
- **genspark-ai/genoffice**: Apache-2.0, 11,720 stars, pushed 2026-11-04. An open-source AI Office suite (Docs, Sheets, Slides, PDF, HTML editors) with a `genoffice` CLI and an agent skill for Claude Code, Codex and Cursor. It is a full app, not a light skill, and can route models "through the Genspark proxy" — [repo](https://github.com/genspark-ai/genoffice)
- **zarazhangrui/frontend-slides**: MIT, 31,877 stars, pushed 2026-06-23. Builds HTML slide decks using the agent's frontend skills — [repo](https://github.com/zarazhangrui/frontend-slides)
- **chuspeeism/dashi-ppt-skill**: AGPL-3.0, 10,363 stars, pushed 2026-09-12. Browser-editable presentations exportable to HTML, PDF and PPTX — [repo](https://github.com/chuspeeism/dashi-ppt-skill)
- **Gabberflast/academic-pptx-skill**: MIT, 1,447 stars, pushed 2026-07-14 — [repo](https://github.com/Gabberflast/academic-pptx-skill)
- **tfriedel/claude-office-skills**: 848 stars, last commit 2026-04-01, **no licence**. Its README says "Most scripts and workflows in this repository come directly from Claude… included here verbatim" and points users to the official repo instead. **Do not use.** It is effectively a copy of Anthropic's proprietary skills — [README](https://github.com/tfriedel/claude-office-skills/blob/main/README.md)
- **CodeStrate/Document_Skills_Agent**: 0 stars, no root licence. Weak lead — [repo](https://github.com/CodeStrate/Document_Skills_Agent)

**C. Video**
- **remotion-dev/skills**: 6,342 stars, last commit 2026-11-02, version 4.0.540. **No LICENSE file in the skills repo.** Its package.json says the source is the `remotion-dev/remotion` monorepo (`packages/skills`). Structure: a router skill `remotion-best-practices` with sub-references (remotion-create, remotion-captions, remotion-maps, remotion-interactivity, remotion-docs, remotion-license, and more) — [repo](https://github.com/remotion-dev/skills), [SKILL.md](https://github.com/remotion-dev/skills/blob/main/skills/remotion-best-practices/SKILL.md)
- The Remotion monorepo (70,704 stars) is under the **"Remotion License"**, not OSI. Free for "an individual", "a for-profit organization with up to 3 employees", non-profits, and evaluation. "A company license is required for for-profit organizations of a certain size". "It is not allowed to copy or modify Remotion code for the purpose of selling… relicensing, or sublicensing your own derivate" — [remotion LICENSE.md](https://github.com/remotion-dev/remotion/blob/main/LICENSE.md)
- **kajisho5/ffmpeg-skill**: MIT, 4,518 stars, pushed 2026-10-31. "No cloud · No API keys · Python standard library". Install with `npx ffmpeg-skill` (flags `--cursor`, `--codex`, `--all`), and `npx ffmpeg-skill doctor` checks the setup. Optional local transcription via `pip install faster-whisper`. Sibling repos: media-analysis-skill, transcription-skill, subtitle-skill, thumbnail-skill. Reproducible demos via `python3 demos/build.py` — [repo/README](https://github.com/kajisho5/ffmpeg-skill)
- **affaan-m/ECC (everything-claude-code)**: MIT, 297,098 stars, pushed 2026-11-02. Includes a video-editing skill covering an FFmpeg + Remotion pipeline. The Remotion parts carry Remotion's licence terms — [repo](https://github.com/affaan-m/everything-claude-code), [skill listing](https://skills.browseract.com/skills/affaan-m-everything-claude-code-video-editing)
- **bangtutorial/bang-motion**: MIT, 1,064 stars, pushed 2026-09-15. Browser motion graphics (openers, promos, kinetic type) as a single `index.html` — [repo](https://github.com/bangtutorial/bang-motion)
- **MomoFadaly/video-edit**: Apache-2.0 but only 1 star. Low adoption — [repo](https://github.com/MomoFadaly/video-edit)

**D. Image generation and editing**
- **openai/skills `imagegen`**: Apache-2.0. Uses the built-in `image_gen` tool by default (Codex-specific). The fallback CLI `scripts/image_gen.py` "Requires `OPENAI_API_KEY`" — [SKILL.md](https://github.com/openai/skills/blob/main/skills/.system/imagegen/SKILL.md)
- **fal-ai-community/skills**: 260 stars, last commit 2026-05-13 (repo pushed 2026-10-23), **no licence file**. Skills: genmedia, model-routing, fal-models-catalog, fal-prompting, fal-recipes, character-design, cinematography, commercial, marketing, storytelling, ugc, fal-workflow, fan-cam, fal-gamedev, fal-redesign, fal-regenerate-3d, genmedia-workflow. All execution goes through the `genmedia` CLI and needs `FAL_KEY`. The `marketing` skill covers "Campaign matrices, launch kits, paid social variants, landing-page visuals, banners" — [README](https://github.com/fal-ai-community/skills/blob/main/README.md)
- **replicate/skills**: Apache-2.0, 146 stars, pushed 2026-06-04. Skills: find-models, compare-models, run-models, prompt-images, prompt-videos, build-models, publish-models. Ships `.mcp.json` pointing to the remote MCP `https://mcp.replicate.com/sse`; needs a Replicate account and token — [repo](https://github.com/replicate/skills)
- **kingbootoshi/nano-banana-2-skill**: MIT, 416 stars, pushed 2026-10-31. Gemini image CLI (default Gemini 3.1 Flash Image Preview, `pro` = Gemini 3 Pro Image Preview), 512px–4K, cost tracking. Green-screen transparency uses FFmpeg `colorkey` + `despill` and ImageMagick. Needs `GEMINI_API_KEY` stored in `~/.nano-banana/.env` — [README](https://github.com/kingbootoshi/nano-banana-2-skill)
- **kkoppenhaver/cc-nano-banana**: MIT, 382 stars, pushed 2026-05-20. Goes through Gemini CLI's nanobanana extension — [repo](https://github.com/kkoppenhaver/cc-nano-banana)
- **google-gemini/gemini-skills**: Apache-2.0, 4,389 stars, pushed 2026-11-03. Skills are API/SDK developer skills (gemini-api-cli, gemini-api-dev, gemini-live-api-dev, gemini-omni-flash-api), not content-production skills — [repo](https://github.com/google-gemini/gemini-skills)
- **YouMind-OpenLab/ai-image-prompts-skill**: MIT, 1,362 stars, pushed 2026-11-04. A prompt library (10,000+ prompts), no generation — [repo](https://github.com/YouMind-OpenLab/ai-image-prompts-skill)
- **smixs/visual-skills**: CC-BY-4.0, 628 stars. Prompt syntax for Seedance, Kling, Veo, Nano Banana, GPT Image — [repo](https://github.com/smixs/visual-skills)
- **huggingface/skills**: Apache-2.0, 11,267 stars. Mostly ML/training/Spaces skills, not content production — [repo](https://github.com/huggingface/skills)

**E. Visual design, brand enforcement, vendor skills**
- Anthropic `canvas-design` (posters/art to PNG/PDF, bundled `canvas-fonts`), `algorithmic-art` (p5.js templates), `theme-factory` (themes + theme-showcase.pdf), `brand-guidelines` (encodes Anthropic's own brand; a template to swap in your brand), `frontend-design`. All Apache-2.0 — [anthropics/skills](https://github.com/anthropics/skills/tree/main/skills)
- **canva-sdks/canva-skills**: Apache-2.0, 149 stars, pushed 2026-10-23. Active skills: brand-check, bulk-create, cli, edit-design, get-design-feedback, implement-feedback, resize-for-social-media. Inactive: branded-presentation, generate-deck, design-translation, presentation-time-fitting, classroom-helper. Needs the Canva Connector/MCP and a Canva account — [repo tree](https://github.com/canva-sdks/canva-skills)
- **Figma**: Figma's skills (figma-use, figma-generate-design, figma-generate-library, figma-implement-design, figma-create-new-file, figma-code-connect-components…) appear in openai/skills `.curated/` with per-skill LICENSE files. Figma's own guide repo figma/mcp-server-guide has 2,149 stars, pushed 2026-11-03, no SPDX licence — [openai/skills tree](https://github.com/openai/skills/tree/main/skills/.curated), [figma/mcp-server-guide](https://github.com/figma/mcp-server-guide)
- **vercel-labs/agent-skills**: 33,540 stars, pushed 2026-10-28. README "License: MIT", but GitHub detects no LICENSE file. Includes `web-design-guidelines` (UI/accessibility audit) and react/composition skills — [repo](https://github.com/vercel-labs/agent-skills)

**F. Diagrams**
- **tt-a1i/archify**: Apache-2.0, 93,407 stars, pushed 2026-11-03. Interactive diagrams from ideas or codebases; installs via `npx skills add`; README says "No telemetry" — [repo](https://github.com/tt-a1i/archify)
- **yctimlin/mcp_excalidraw**: MIT, 2,611 stars, pushed 2026-10-30. MCP server + agent skill + CLI (`npx -y mcp-excalidraw-server …`, `install-skill`, offline `render`). Node ≥20, "no API keys or accounts"; optional `share` uploads an encrypted scene to excalidraw — [README](https://github.com/yctimlin/mcp_excalidraw)
- **coleam00/excalidraw-diagram-skill**: 5,185 stars, pushed 2026-03-01, **no licence file**. Has references (json-schema, element templates, color palette) and a Python renderer `render_excalidraw.py` — [repo](https://github.com/coleam00/excalidraw-diagram-skill)
- **axtonliu/axton-obsidian-visual-skills**: MIT, 3,678 stars. Canvas, Excalidraw and Mermaid for Obsidian — [repo](https://github.com/axtonliu/axton-obsidian-visual-skills)
- **WH-2099/mermaid-skill**: MIT, 299 stars, pushed 2026-08-11 — [repo](https://github.com/WH-2099/mermaid-skill)
- **ythx-101/live-panel-skill**: MIT, 840 stars. Animated architecture diagrams to MP4 or web — [repo](https://github.com/ythx-101/live-panel-skill)
- **softaworks/agent-toolkit**: MIT, 2,626 stars, pushed 2026-03-05. Includes an excalidraw plugin skill — [repo](https://github.com/softaworks/agent-toolkit)

**G. Carousels and thumbnails**
- **op7418/guizang-social-card-skill**: AGPL-3.0, 7,974 stars, pushed 2026-10-30. Xiaohongshu carousels and WeChat covers; 28 layouts, 10 themes; single-file HTML output — [repo](https://github.com/op7418/guizang-social-card-skill)
- **itchernetski/threads-carousel-claude-skill**: MIT, 120 stars. Text posts to carousel images for Threads, Instagram, LinkedIn, TikTok — [repo](https://github.com/itchernetski/threads-carousel-claude-skill)
- **helloianneo/ian-xhs-carousel**: MIT, 299 stars. 1080×1440, 20 masters — [repo](https://github.com/helloianneo/ian-xhs-carousel)
- **sergebulaev/instagram-skills** (MIT, 743 stars) and **sergebulaev/youtube-skills** (MIT, 88 stars), both pushed 2026-11-04. Publish via the Publora service — [instagram-skills](https://github.com/sergebulaev/instagram-skills), [youtube-skills](https://github.com/sergebulaev/youtube-skills)
- **Jakeschincariol/youtube-agent-skill**: MIT, 4,540 stars, pushed 2026-09-16. Eleven skills, including title and thumbnail "linted as one pairing" — [repo](https://github.com/Jakeschincariol/youtube-agent-skill)
- **AgriciDaniel/claude-youtube**: MIT, 661 stars. Includes thumbnails — [repo](https://github.com/AgriciDaniel/claude-youtube)
- kajisho5 also publishes a `thumbnail-skill` sibling to ffmpeg-skill (named in the ffmpeg-skill README; I did not check its metadata) — [ffmpeg-skill README](https://github.com/kajisho5/ffmpeg-skill)

**H. Awesome lists / directories (for discovery, not install)**
- ComposioHQ/awesome-claude-skills: 78,732 stars, pushed 2026-09-18, no licence — [repo](https://github.com/ComposioHQ/awesome-claude-skills)
- VoltAgent/awesome-agent-skills: MIT, 36,841 stars, pushed 2026-11-02, "1000+ agent skills" (VoltAgent/awesome-claude-skills redirects here) — [repo](https://github.com/VoltAgent/awesome-agent-skills)
- travisvn/awesome-claude-skills: 15,704 stars, pushed 2026-04-28, no licence — [repo](https://github.com/travisvn/awesome-claude-skills)

### Inferences
- Shortlist of about 15 for a marketing content stack: anthropics canvas-design, brand-guidelines, frontend-design, web-artifacts-builder, theme-factory; appautomaton/document-SKILLs; openai pdf and imagegen; kajisho5/ffmpeg-skill; remotion-dev/skills (if the org qualifies or buys a licence); kingbootoshi/nano-banana-2-skill; replicate/skills; canva-sdks/canva-skills; yctimlin/mcp_excalidraw or tt-a1i/archify; itchernetski/threads-carousel (MIT) or op7418/guizang (AGPL); Jakeschincariol/youtube-agent-skill; zarazhangrui/frontend-slides.
- The Anthropic doc skills are already available to Claude.ai / Claude Code users as built-in "anthropic-skills" through the Services. You can use them there, but you cannot vendor them into your own repo or redistribute them.
- Copyleft (AGPL-3.0: guizang, dashi-ppt) is fine for internal use. It matters if the skill is modified and offered to others over a network.

### Gaps
- I could not verify that appautomaton/document-SKILLs is clean-room. Its README and LICENSE do not mention Anthropic, but a third-party search summary said it was "based on Anthropic's official skills" (I could not confirm this in the repo text). Diff it against Anthropic's scripts (e.g. ooxml/validate, recalc) before relying on the MIT grant.
- Remotion skills repo licence is unstated. I infer the Remotion License applies through the monorepo source, but the skills repo has no LICENSE file.
- I did not open skillsmp.com. Some star counts look very high (archify at 93k, ECC at 297k), and API values may include star-farming; adoption signals beyond stars were not checked.
- Did not verify licences of Figma skill LICENSE.TXT contents in openai/skills (only presence).

## 2. Script and dependency requirements

### Takeaway
The office skills need Node (docx / pptxgenjs), Python (openpyxl, pandas, markitdown, pypdf, pdfplumber, reportlab), LibreOffice and Poppler. The video skills need ffmpeg and/or Node + Remotion. The image skills all need a paid API key (OPENAI_API_KEY, GEMINI_API_KEY, FAL_KEY, Replicate token) or a vendor account (Canva, Figma).

### Cited Findings
- Anthropic docx: "`docx` (npm, preinstalled…) · `pandoc` · LibreOffice (`soffice`) · `pdftoppm` (Poppler)". Edits work by unzipping and editing `word/document.xml` — [docx/SKILL.md](https://github.com/anthropics/skills/blob/main/skills/docx/SKILL.md)
- Anthropic pptx: "`pptxgenjs` (npm) · `markitdown[pptx]`, `Pillow`, `defusedxml`, `lxml` (pip) · LibreOffice · `pdftoppm`". Icons use react-icons, react, react-dom and sharp; `scripts/thumbnail.py` builds template grids — [pptx/SKILL.md](https://github.com/anthropics/skills/blob/main/skills/pptx/SKILL.md)
- Anthropic xlsx: "`openpyxl`, `pandas`, `markitdown` (pip) · LibreOffice". A mandatory `scripts/recalc.py` step recalculates formulas. Avoid XLOOKUP/FILTER/UNIQUE etc. because LibreOffice can't evaluate them — [xlsx/SKILL.md](https://github.com/anthropics/skills/blob/main/skills/xlsx/SKILL.md)
- Anthropic pdf: pypdf, pdfplumber, reportlab, pdftotext (poppler-utils), qpdf; plus forms.md and reference.md — [pdf/SKILL.md](https://github.com/anthropics/skills/blob/main/skills/pdf/SKILL.md)
- web-artifacts-builder: "React 18 + TypeScript + Vite + Parcel… Tailwind CSS… shadcn/ui"; scripts install parcel and html-inline and bundle to a single HTML file — [SKILL.md](https://github.com/anthropics/skills/blob/main/skills/web-artifacts-builder/SKILL.md)
- slack-gif-creator: `pip install pillow imageio numpy` — [SKILL.md](https://github.com/anthropics/skills/blob/main/skills/slack-gif-creator/SKILL.md)
- appautomaton: "Python scripts use uv + PEP 723 inline metadata — no virtual environments or pip install"; Node packages for docx and pptx only; macOS `brew bundle` via Brewfile — [README](https://github.com/appautomaton/document-SKILLs/blob/main/README.md)
- ffmpeg-skill: needs ffmpeg + python3 only; faster-whisper optional — [README](https://github.com/kajisho5/ffmpeg-skill)
- Remotion: Node/React project (`remotion`, `@remotion/cli`, `@remotion/bundler`, etc. in package.json) — [package.json](https://github.com/remotion-dev/skills/blob/main/package.json)
- fal: the `genmedia` CLI plus `FAL_KEY` (`genmedia setup --non-interactive --api-key "$FAL_KEY"`) — [genmedia SKILL.md](https://github.com/fal-ai-community/skills/blob/main/skills/genmedia/SKILL.md)
- nano-banana-2: `GEMINI_API_KEY`; FFmpeg + ImageMagick for transparency — [README](https://github.com/kingbootoshi/nano-banana-2-skill)
- mcp_excalidraw: Node ≥20, no keys — [README](https://github.com/yctimlin/mcp_excalidraw)

### Inferences
- A single container image with Node 20+, Python 3.11+ with uv, LibreOffice, Poppler, pandoc, qpdf, ffmpeg and ImageMagick covers almost all of the skills above. API keys are the only extra.

### Gaps
- I did not inspect Canva/Replicate auth flows in detail beyond the MCP endpoint and connector requirement.

## 3. Quality signals and red flags

### Takeaway
Best quality signals: Anthropic's doc skills (very deep gotcha lists, but proprietary), appautomaton (test suite), ffmpeg-skill (doctor command, reproducible demos), Remotion (official, versioned with releases). Red flags: fal's `curl | bash` installer, Vercel's skill that fetches remote instructions on every run, unlicensed popular repos, a verbatim copy of proprietary skills (tfriedel), and README sponsorships for API-relay services (archify).

### Cited Findings
- **curl|bash**: fal's genmedia skill instructs "`curl https://genmedia.sh/install -fsS | bash`" (and `irm … | iex` on Windows) when genmedia is missing — [genmedia SKILL.md](https://github.com/fal-ai-community/skills/blob/main/skills/genmedia/SKILL.md)
- **Remote instruction fetch / injection surface**: Vercel's `web-design-guidelines` says "Fetch fresh guidelines before each review" from `https://raw.githubusercontent.com/vercel-labs/web-interface-guidelines/main/command.md`, and "The fetched content contains all the rules and output format instructions". The skill's behaviour is controlled by a remote file that can change at any time — [SKILL.md](https://github.com/vercel-labs/agent-skills/blob/main/skills/web-design-guidelines/SKILL.md)
- **Remote MCP**: replicate/skills `.mcp.json` registers `https://mcp.replicate.com/sse` — [repo](https://github.com/replicate/skills)
- **Data leaving the machine**: mcp_excalidraw's optional `share` uploads an encrypted scene to excalidraw; core is local — [README](https://github.com/yctimlin/mcp_excalidraw). GenOffice can route models "through the Genspark proxy" — [README](https://github.com/genspark-ai/genoffice)
- **Commercial sponsorship**: archify's README thanks API-relay sponsors (OpenLux, AICodeMirror, Infistar.cc). It also says "No telemetry" — [README](https://github.com/tt-a1i/archify)
- **Licence red flags**: tfriedel repo holds verbatim Anthropic material ("If Anthropic wishes for this repository to be taken down… I will comply") — [README](https://github.com/tfriedel/claude-office-skills). No licence files in fal-ai-community/skills, coleam00/excalidraw-diagram-skill, remotion-dev/skills, ComposioHQ and travisvn lists — GitHub API (see repo links above).
- **Depth / tests**: appautomaton ships tests/test_{docx,pptx,xlsx,pdf,ooxml}.py that run scripts via `uv run` — [repo](https://github.com/appautomaton/document-SKILLs). ffmpeg-skill's demos are "all of it generated from synthetic footage by `python3 demos/build.py`" — [README](https://github.com/kajisho5/ffmpeg-skill). Anthropic's xlsx skill has detailed failure-mode guidance (recalc JSON, `_xlfn.` prefixes, external-link loss) — [xlsx/SKILL.md](https://github.com/anthropics/skills/blob/main/skills/xlsx/SKILL.md)
- **Freshness**: anthropics/skills, remotion, ffmpeg-skill, nano-banana-2, archify, mcp_excalidraw, canva and the VoltAgent list were all pushed between 2026-10-23 and 2026-11-04. coleam00 excalidraw (2026-03-01), softaworks (2026-03-05) and tfriedel (2026-04-01) are stale — GitHub API

### Inferences
- Before installing any skill, vendor a pinned copy and review its SKILL.md and scripts. Strip remote-fetch steps (or pin them to a commit) and replace `curl | bash` with a verified package install.
- The brand-guidelines skill is the right template for brand enforcement: fork the Apache-2.0 version and replace Anthropic's colours and fonts with the client's. Canva's `brand-check` adds enforcement on the Canva side for teams on Canva.

### Gaps
- I did not run the skills or scan the scripts for hidden network calls or telemetry, apart from the README/SKILL.md grep for curl, telemetry, analytics and posthog. I found no telemetry claims in the repos I checked.
- I found no reliable independent quality benchmark comparing these skills.
