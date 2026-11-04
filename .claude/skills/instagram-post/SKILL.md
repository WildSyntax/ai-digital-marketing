---
name: instagram-post
description: Write an Instagram caption, hashtags, and an image brief into content/drafts/instagram/, and create the image in Canva when connected. Use when the owner says "instagram post about <topic>" or "from <blog file>", or when repurpose calls it.
---

# Instagram post

Input: a topic, or a path to a blog file.
Output: `content/drafts/instagram/YYYY-MM-DD-<slug>.md`.

## Steps

1. Read `brand/profile.md` (tone, CTA, `canva_template`) and any `brand/examples/instagram-*.md`.
2. If a blog path was given, read it and choose one takeaway that fits a single image or a
   3–5 point list. Set `source` and `keyword` from the blog.
3. Write the file:

   ```markdown
   ---
   title: "<headline on the image>"
   channel: instagram
   status: draft
   keyword: "<keyword or empty>"
   secondary_keywords: []
   seo_score: null
   created: YYYY-MM-DD
   scheduled_for: null
   published_url: null
   source: <blog path or null>
   canva_design_url: null
   ---

   ## Caption
   <first line is the hook, under 10 words; then 3–6 short lines (a bulleted or numbered list counts as one line; a line is at most ~15 words); blank lines between;
   ends with the Instagram CTA; total under 2200 characters; at most 3 emojis>

   ## Hashtags
   <10–20 hashtags, mix of broad (100k+ posts) and niche, one line, lowercase>

   ## Image brief
   Format: 1080x1350 portrait (or 1080x1080 if a square template is named)
   Headline overlay: <at most 8 words>
   Visual: <one sentence>
   Alt text: <descriptive alt text>
   ```
4. Canva, only if the `canva` connector is connected (its tools appear in the session):
   - If `canva_template` is non-empty: `search-designs` for that name, `get-design`, and create the
     post from it with the headline overlay; export as PNG; put the design URL in
     `canva_design_url`.
   - If `canva_template` is empty: `search-designs` for "instagram post" in the owner's designs; if nothing
     fits, leave `canva_design_url: null` and say "no template found; image brief only".
   If Canva is connected but a call fails: name the connector, leave the file in place, and stop.
   If Canva is not connected: leave `canva_design_url: null` and say
   "Canva not connected; image brief only. Connect via /mcp to create the image."
5. Commit `content(instagram): draft <slug>`. Reply with the path, the headline, and whether
   an image was created.
