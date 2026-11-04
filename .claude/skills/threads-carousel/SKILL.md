---
name: threads-carousel
user_invocable: true
description: >
  Converts an existing text post into a slide-by-slide carousel or presentation plan for Threads, Instagram, LinkedIn, TikTok, Stories or YouTube.
  Picks one of 6 format presets (1080x1350, 1080x1080, 1080x1920, 1920x1080), assigns each slide one of 12 typed layouts (hook, body, list, stats, quote, checklist, process, comparison, cta, image, emoji, number) with badge and highlighted keyword, and suggests a style (font x surface x accent x purpose, background).
  Returns the plan as text; it does not render images. Not for writing Threads text posts (use threads-post-writer) or Instagram carousel formulas and captions (use ig-carousel-planner).
  Triggers: threads carousel, linkedin carousel, tiktok carousel, carousel from a post, slides from a post.
license: MIT
metadata:
  source: "itchernetski/threads-carousel-claude-skill@cc775b668088ba348022bc2296ff41f130f1f7ef"
  path: "SKILL.md"
  modified: "yes"
---

# Threads Carousel Generator

> Vendored from [itchernetski/threads-carousel-claude-skill](https://github.com/itchernetski/threads-carousel-claude-skill/tree/cc775b668088ba348022bc2296ff41f130f1f7ef) under MIT.
> Changes for this workspace: planning only. Removed the Next.js/bun render template (template/, needs package installs and a dev server), the generate/export step, image copying, toolbar and future-work notes; output is a slide plan returned as text. Differs from `ig-carousel-planner` (Instagram-only formulas plus caption) and `threads-post-writer` (text posts): this turns an existing post into typed slides for any platform format. Read brand/profile.md first. Return text; workspace skills own files under content/.

Converts a text post into a plan for a set of visual carousel slides for Threads, Instagram, LinkedIn, TikTok, Stories, YouTube, or a standalone presentation deck. Composable design system with three independent style axes (font × color × purpose) and 12 slide types. The plan can be rendered by the owner in any design tool, or by the workspace `canvas-design` skill; for brand colours and fonts use the workspace `brand-guidelines` skill.

## Invocation

```
/threads-carousel <post text>
/threads-carousel path/to/post.md
```

## Format presets (choose target platform)

| Preset | Size | Platforms |
|---|---|---|
| `threads-4x5` *(default)* | 1080×1350 | Threads, Instagram feed (portrait) |
| `instagram-square` | 1080×1080 | Instagram, Facebook, LinkedIn feed |
| `linkedin-square` | 1080×1080 | LinkedIn document post (PDF) |
| `tiktok-9x16` | 1080×1920 | TikTok Photo Mode, Reels, Shorts |
| `story-9x16` | 1080×1920 | Instagram Stories, Threads Stories |
| `wide-16x9` | 1920×1080 | Presentations, YouTube, desktop decks |

## Slide types (12)

| Type | Purpose | Required fields |
|---|---|---|
| `hook` | Opening slide — the catchiest line | `text` |
| `body` | Title + paragraph | `title`, `text` |
| `body` (points) | Pros/cons list with ✓/✗ SVG icons | `title`, `points[]` (instead of `text`) |
| `list` | Numbered items (ordered list) | `title`, `items[]` |
| `stats` | Big numbers with labels | `title`, `stats[]` |
| `quote` | Large pulled quote | `text`, `author` |
| `checklist` | Checkmark bullets | `title`, `items[]` |
| `process` | Numbered steps with connector line | `title`, `steps[]` |
| `comparison` | Two-column VS / before-after | `leftLabel`, `leftItems[]`, `rightLabel`, `rightItems[]` |
| `cta` | Final call to action | `text`, `handle` |
| `image` | Title + screenshot/photo + optional caption | `imageSrc`, optional `title`, `imageCaption` |
| `emoji` | Giant emoji illustration + title + text | `emoji`, optional `title`, `text` |
| `number` | Huge hero number/string + title + text | `bigNumber`, optional `title`, `text` |

`points` shape: `Array<{ type: "plus" | "minus"; text: string }>` — green ✓ for plus, muted ✗ for minus. Adaptive sizing (44–62px) based on item count and longest line.

All types also support optional:
- `badge` — small outlined tag above title (e.g. `"01"`, `"TIP"`)
- `highlight` — a word or phrase within `text`/`title` that will be colored in the preset's highlight color (yellow for dark themes)
- `highlightStyle: "italic-box"` — renders the highlighted word in Playfair italic on a colored rectangle (instead of plain color)

### Images in slides

For `image` slides, reference the image the owner names (a local file path or a description of the shot needed). Do not copy or move image files; list them in the plan so the owner can supply them.

## Background decorations (8 types)

Suggest one in the plan. Default: `glow`.

| Type | What it is |
|---|---|
| `none` | Solid background |
| `blobs` | Organic colored shapes |
| `grid` | Dotted grid pattern |
| `lines` | Diagonal line pattern |
| `paper` | Ruled notebook lines + left margin (use with `paper`/`light`/`white` colors for a literary feel) |
| `noise` | SVG grain overlay (overlay blend) |
| `bignumber` | Giant slide index as watermark (01, 02…) |
| `glow` *(default)* | Soft radial gradient in alternating corners |

## Style system (3 independent axes)

The final style is composed from three independent axes (plus a background):

**Font axis** (`DEFAULT_FONT`), 5 typefaces:

| Id | Font | Feel |
|---|---|---|
| `minimal` *(default)* | Unbounded (body + hook) | Geometric display, bold, distinctive |
| `editorial` | Playfair Display | Classic serif, literary |
| `clean` | Inter | Neutral sans-serif, most standard |
| `mono` | JetBrains Mono | Monospace, tech/dev feel |
| `condensed` | Oswald | Narrow + tall, editorial poster |

**Surface axis** (`DEFAULT_SURFACE`) — bg + text neutrals, 8 options:

| Id | Bg | Text | Feel |
|---|---|---|---|
| `dark` *(default)* | `#0A0A0A` | white | default bold |
| `white` | pure `#FFFFFF` | near-black | sharp clinical, Apple-style |
| `light` | cool zinc `#F4F4F5` | near-black | neutral cool grey, Vercel-style |
| `paper` | cream `#ECE2C8` | warm brown | notebook / literary warm |
| `gradient` | purple→pink→amber | white | bright gradient |
| `pastel` | lilac `#EDE9FE` | indigo | soft |
| `neon` | dark gradient | light cyan | tech dark |
| `ember` | black→red radial | near-white | dramatic |

**Accent axis** (`DEFAULT_ACCENT`) — pop color for highlighted words, 8 options:

| Id | Hex | Matches surfaces |
|---|---|---|
| `yellow` *(default)* | `#FACC15` | dark, ember |
| `red` | `#DC2626` | pure red — white, light, paper |
| `teal` | `#14B8A6` | versatile — dark, white, light, paper |
| `coral` | `#FB7185` | pink-family — paper, light, white |
| `orange` | `#F97316` | pumpkin — paper, light, dark |
| `violet` | `#A78BFA` | dark, neon, ember |
| `lime` | `#D9F056` | ember, dark |
| `blue` | `#3B82F6` | white, light, paper, dark |
| `fuchsia` | `#C026D3` | pastel, white, dark |
| `pink` | `#EC4899` | pastel, dark, light |
| `amber` | `#F59E0B` | gradient, dark, paper |

Any surface, accent, font and purpose can be combined. Pick surface for neutral base, accent for pop color — independently.

**Reference combos** (inspired by design refs):
- `dark + teal` — noir / minimalist tech
- `paper + orange` — literary warm
- `ember + lime` — dramatic announcement
- `white + coral` — sharp editorial
- `light + teal` — calm informational

**Purpose axis** (`DEFAULT_PURPOSE`):

| Id | Title | Body | Divider |
|---|---|---|---|
| `carousel` *(default)* | 44px, weight 800, UPPERCASE | weight 600, `textColor`, line-height 1.2 | visible (96×4px accent) |
| `presentation` | 72px, weight 700, sentence case | weight 400, `textSecondary`, line-height 1.45 | hidden |

Pick `purpose: "presentation"` + `format: "wide-16x9"` for a desktop / YouTube presentation deck. For a full animated HTML deck, use the workspace `frontend-slides` skill instead.

---

## Workflow

### Step 1 — Get the text

- If passed inline — use it.
- If a file path (`.md`, `.txt`) — read it.
- If text is long (>500 chars) — confirm it's complete before planning.

### Step 2 — Clarify parameters (optional, can assume defaults)

Ask once, combined:

1. **Number of slides** (3–10, default 6)
2. **Format** (see table above, default `threads-4x5`; use `wide-16x9` for a presentation deck)
3. **Purpose** (`carousel` or `presentation`, default `carousel`)
4. **Font** (`minimal` / `editorial` / `clean`, default `minimal`)
5. **Color** (8 palettes, default `dark`)
6. **Handle** for CTA slide (take it from `brand/profile.md` if listed, otherwise ask)

If the slides should carry the brand's look, take font and colours from `brand/profile.md` (via `brand-guidelines`) instead of the presets below.

Shortcut: if user says "presentation" / "презентация" / "slide deck" → default to `purpose: presentation`, `format: wide-16x9`, `font: clean`, `color: white`.

If user says "your call" — apply defaults, do not block.

### Step 3 — Plan the slide breakdown

Show the user a preview list before generation:

```
Slide 1 (hook): "Headline..."  [highlight: "word"]
Slide 2 (body): badge 01 — "Title" / "Text..."
Slide 3 (list): badge 02 — "iOS stack" / 3 items
Slide 4 (stats): badge 03 — "Growth" / 3 stats
Slide 5 (quote): "Quote..." — Author
Slide 6 (cta): "Final message" @username
```

### Rules for splitting text into slides

1. **Hook** = single most intriguing line from the post. 1–3 short lines. Works as a standalone thumbnail.
2. **Body slides** = one idea each. Max 40 words. Max 5 lines. Never join two ideas with "and".
3. **Mix slide types** for visual variety: prefer `list` for enumerations, `stats` for numbers, `quote` for direct speech, `comparison` for VS/before-after. Don't make every slide a `body`.
4. **CTA** = conclusion + follow handle. Centered, short.

### Step 4 — Return the plan

Return the plan as text, ready for the owner to render or hand to a design tool:

1. **Settings:** format preset (and pixel size), purpose, font, surface, accent, background.
2. **Slides:** for each slide, its number, type, badge, title, text (or items / stats / steps / points / comparison columns), highlight word and highlight style, and any image needed.
3. **Copy check:** every slide follows the splitting rules and `brand/profile.md` (voice, banned phrases).

Optionally add the same plan as a TypeScript `SLIDES` array in the shape below, for owners who render with the upstream template themselves:

```ts
export const SLIDES = [
  { type: "hook", text: "Line one\nline two", highlight: "two" },
  { type: "body", badge: "01", title: "Title", text: "Body text...", highlight: "key" },
  { type: "body", badge: "02", title: "Pros & Cons", points: [
    { type: "plus",  text: "One click to register" },
    { type: "minus", text: "Requires provider setup" },
  ]},
  { type: "list", badge: "03", title: "Steps", items: ["First", "Second", "Third"] },
  { type: "stats", title: "Numbers", stats: [
    { value: "10×", label: "Faster" },
    { value: "50%", label: "Smaller" },
  ]},
  { type: "quote", text: "Big idea\nin few words", author: "Someone", role: "2026" },
  { type: "cta", text: "Last word", handle: "@username" },
];
```

Do not save files under `content/`. When the owner wants the carousel as a draft post, hand the plan to the matching workspace skill (`instagram-post`, `linkedin-post`, ...), which writes the file. The owner posts it, or the workspace `publish` skill schedules approved content via Metricool.

---

## Design system

Canonical look (`font: minimal`, `color: dark`, `purpose: carousel`):

- **Display typeface:** Unbounded (Google Fonts), for hooks
- **Body typeface:** Space Grotesk (minimal) / Playfair (editorial) / Inter (clean)
- **Palette (dark):** `#0A0A0A` bg, `#FFFFFF` text, `#FACC15` highlight
- **Layout:** 80px padding, left-aligned, slide counter bottom-center
- **Title discipline:** carousel purpose — title → a 96×4px accent divider → body, with ≥64px breathing room above body. Presentation purpose — no divider, sentence case, 72px.
- **Hook size:** 104–140px, adaptive by character/line count
- **Body text size:** 48–88px, adaptive
- **Text balance:** `textWrap: "balance"` on hook + title (no orphan words)

### Typography table (carousel purpose)

The `presentation` purpose overrides titles to 72px / 700 / sentence case and body to 400 / `textSecondary` / line-height 1.45.

| Element | Size | Weight | Font source |
|---|---|---|---|
| Hook | 104–140px | 800 | display (hook) font |
| Title | 44px | 800 uppercase | body font |
| Body | 48–88px | 600 | body font |
| Points (pros/cons) | 44–62px | 600 | body font |
| Badge | 26px | 800 uppercase | body font |
| Stats value | 140–170px | 900 | body font |
| Stats label | 32px | 500 uppercase | body font |
| Quote | 62px | 600 | body font |
| List item | 46px | 600 | body font (numbers 48px) |
| Checklist item | 44px | 600 | body font |
| Process step title | 36px | 700 | body font |
| Handle | 36px | 500 | body font |

## Common mistakes

| Mistake | Fix |
|---|---|
| Too much text on a slide | Max 40 words, max 5 lines |
| Two ideas on one slide | Split into two slides |
| All slides are `body` type | Mix in `list`, `stats`, `quote`, `checklist` for visual variety |
| No hook on first slide | Slide 1 must be the catchiest line |
| No CTA on last slide | Slide N must end with a handle or call to action |
| Highlight word too long | Keep highlight to 1–2 words, not whole phrase |
| Badge has too many characters | Max 2–4 characters (`01`, `TIP`, `NEW`) |
