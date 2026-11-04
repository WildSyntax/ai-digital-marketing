---
name: brand-guidelines
description: Applies this brand's colours, typography, logo rules and image style, read from the "Visual identity" section of brand/profile.md, to any artifact that should carry the brand's look and feel (slides, documents, social graphics, HTML pages, reports). Use it when brand colours, style guidelines, visual formatting or company design standards apply.
license: Apache-2.0
metadata:
  source: "anthropics/skills@ca45fc496a3436251f191354091d557da31c15b5"
  path: "skills/brand-guidelines"
  modified: "yes"
---

# Brand Styling

> Vendored from [anthropics/skills](https://github.com/anthropics/skills/tree/ca45fc496a3436251f191354091d557da31c15b5/skills/brand-guidelines) under Apache-2.0.
> Changes for this workspace: replaced the vendor's hard-coded brand colours and fonts with values read from the "Visual identity" section of brand/profile.md; added logo and image-style rules; removed vendor branding. Read brand/profile.md first. Return text; workspace skills own files under content/.

## Overview

To apply this brand's visual identity to an artifact, use this skill. The brand is defined in `brand/profile.md`; this skill holds the method, the profile holds the values.

**Keywords**: branding, corporate identity, visual identity, post-processing, styling, brand colors, typography, visual formatting, visual design

## Brand Guidelines

Read `brand/profile.md` first, then its `## Visual identity` section. Never use colours or fonts from anywhere else unless the owner asks.

If a value still starts with `Example:`, it has not been filled in. Tell the owner which values are placeholders, ask them for the real values (or confirm they want the placeholder values used for a draft), and do not present placeholder styling as final.

### Colors

Take these from the profile:

- **Primary**: main brand colour. Use for headings, key shapes and primary buttons.
- **Secondary**: supporting colour. Use for backgrounds, panels and secondary elements.
- **Accent**: highlight colour. Use sparingly for calls to action, highlights and data points that need attention.

Derive neutrals (text, light backgrounds, dividers) from a near-black and near-white that fit the palette, unless the profile lists them.

### Typography

- **Headings**: the heading font from the profile (with a common system fallback of the same style, such as Arial for sans-serif or Georgia for serif)
- **Body Text**: the body font from the profile (with a matching system fallback)
- **Note**: Fonts should be pre-installed in your environment for best results

### Logo usage

Follow the logo rules in the profile (placement, clear space, minimum size, which version on light or dark backgrounds). Never recolour, stretch or add effects to the logo. If no logo file is available, leave a clearly marked placeholder and say so.

### Image style

Follow the image style in the profile when choosing, describing or briefing images (photography vs illustration, mood, subjects to use or avoid).

## Features

### Smart Font Application

- Applies the heading font to headings (24pt and larger)
- Applies the body font to body text
- Automatically falls back to a system font of the same style if the brand fonts are unavailable
- Preserves readability across all systems

### Text Styling

- Headings (24pt+): heading font
- Body text: body font
- Smart color selection based on background, keeping enough contrast for readability
- Preserves text hierarchy and formatting

### Shape and Accent Colors

- Non-text shapes use the primary, secondary and accent colours
- Cycles through the brand colours, keeping the accent for emphasis
- Maintains visual interest while staying on-brand

## Technical Details

### Font Management

- Uses system-installed brand fonts when available
- Provides automatic fallback to common system fonts of the same style
- No font installation required - works with existing system fonts
- For best results, pre-install the brand fonts in your environment

### Color Application

- Uses the hex values from the profile, converted to RGB where a tool needs it, for precise brand matching
- For example, applied via python-pptx's RGBColor class for slides, or as CSS custom properties for HTML
- Maintains color fidelity across different systems

## Output

Apply the styling to the artifact the owner is working on and return it. Do not create, move or rename files under `content/`; the workspace skills (blog-post, linkedin-post, instagram-post, youtube-video, ...) own those files.
