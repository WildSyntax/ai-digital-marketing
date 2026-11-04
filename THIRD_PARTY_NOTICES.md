# Third-party notices

This workspace includes skills copied (vendored) from other open-source projects. Each copied
skill keeps its licence in its own folder as `LICENSE.txt`, records its source repository and
commit in its `SKILL.md` front matter (`metadata.source`), and lists what was changed for this
workspace in the "Vendored from" note under its title. Files marked `modified: "yes"` were
changed from the original, as Apache-2.0 section 4(b) requires.

The `marketing-skills` library is not copied: it is installed as a plugin and keeps its own licence.

| Source | Commit | Licence | Copyright | Skills |
|---|---|---|---|---|
| [anthropics/skills](https://github.com/anthropics/skills) | [`ca45fc4`](https://github.com/anthropics/skills/tree/ca45fc496a3436251f191354091d557da31c15b5) | Apache-2.0 | see LICENSE.txt | `brand-guidelines`, `canvas-design`, `theme-factory` |
| [anthropics/knowledge-work-plugins](https://github.com/anthropics/knowledge-work-plugins) | [`d900840`](https://github.com/anthropics/knowledge-work-plugins/tree/d900840716eb262e1feb17c6f4406c9ce0e06bcf) | Apache-2.0 | see LICENSE.txt | `brand-review`, `contract-review`, `draft-response`, `kb-article`, `performance-report`, `process-doc`, `proposal-builder`, `status-report` |
| [social-media-skills/skills](https://github.com/social-media-skills/skills) | [`f28cef2`](https://github.com/social-media-skills/skills/tree/f28cef2b7067ec64e79c9d85421c022c06659e03) | MIT | Copyright (c) 2026 Frank Heijdenrijk | `community-management`, `newsletter-writer`, `podcast-and-audiograms`, `voice-builder` |
| [kajisho5/ffmpeg-skill](https://github.com/kajisho5/ffmpeg-skill) | [`1ce2c18`](https://github.com/kajisho5/ffmpeg-skill/tree/1ce2c186bf1dba96132d87274eee46df4f537e0e) | MIT | Copyright (c) 2026 kajisho5 | `ffmpeg-skill` |
| [sergebulaev/instagram-skills](https://github.com/sergebulaev/instagram-skills) | [`550d3cf`](https://github.com/sergebulaev/instagram-skills/tree/550d3cf6cece08de75dae64235bd32136820920f) | MIT | Copyright (c) 2026 Sergey Bulaev | `ig-caption-writer`, `ig-carousel-planner`, `ig-hashtag-strategist` |
| [AgriciDaniel/claude-seo](https://github.com/AgriciDaniel/claude-seo) | [`6be93f4`](https://github.com/AgriciDaniel/claude-seo/tree/6be93f45064ffbadced572b5d5c95f55fd263af0) | MIT | Copyright (c) 2026 agricidaniel; `seo-content-brief` also (c) 2026 puneetindersingh | `seo-cluster`, `seo-content-brief` |
| [sergebulaev/threads-skills](https://github.com/sergebulaev/threads-skills) | [`37199b9`](https://github.com/sergebulaev/threads-skills/tree/37199b9fe705e175ad578421d338672e779b2a1c) | MIT | Copyright (c) 2026 Sergey Bulaev | `threads-post-writer` |
| [sergebulaev/tiktok-skills](https://github.com/sergebulaev/tiktok-skills) | [`2016087`](https://github.com/sergebulaev/tiktok-skills/tree/2016087d14889213ffcc38d269ec7ddd01333450) | MIT | Copyright (c) 2026 Sergey Bulaev | `tt-hook-scripter`, `tt-trend-mapper` |
| [sergebulaev/x-skills](https://github.com/sergebulaev/x-skills) | [`f52d7c6`](https://github.com/sergebulaev/x-skills/tree/f52d7c64258de02a990eceee4378cef2c87c5600) | MIT | Copyright (c) 2026 Sergey Bulaev | `x-post-writer`, `x-thread-builder` |
| [sergebulaev/youtube-skills](https://github.com/sergebulaev/youtube-skills) | [`73cd16a`](https://github.com/sergebulaev/youtube-skills/tree/73cd16a05b589d755bf2eef3e4ee9db9e2df5494) | MIT | Copyright (c) 2026 Sergey Bulaev | `yt-description-writer`, `yt-hook-scripter`, `yt-title-optimizer` |

## Fonts

`.claude/skills/canvas-design/canvas-fonts/` contains font files under the SIL Open Font License 1.1.
Each font has its licence next to it as `<Font>-OFL.txt`.

## Not included on purpose

- `waveform.py` and the audiogram template from kajisho5/ffmpeg-skill: the script can delete an existing
  file of the user's, so it was left out.
- Anthropic's docx, pptx, xlsx and pdf skills: their licence does not allow copying. They are
  available built in as `anthropic-skills:docx` and the others.
- Vendor publishing, image and analytics clients (Publora, Pixfaro, Apify, WoopSocial, DataForSEO),
  installers and MCP servers: removed so every copied skill works without paid keys.
