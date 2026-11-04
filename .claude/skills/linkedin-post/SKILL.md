---
name: linkedin-post
description: Write a LinkedIn post draft into content/drafts/linkedin/ from a topic or from a blog post. Use when the owner says "linkedin post about <topic>" or "linkedin post from <blog file>", or when repurpose calls it.
---

# LinkedIn post

Input: a topic, or a path to a blog file (drafts, approved, or published).
Output: `content/drafts/linkedin/YYYY-MM-DD-<slug>.md`.

## Steps

1. Read `brand/profile.md` and any `brand/examples/linkedin-*.md`.
2. If a blog path was given, read it and pick the single most useful insight or list from it.
   Set `source` to that path and `keyword` to the blog's keyword.
3. Write the post:
   - line 1: a hook under 12 words that states a problem, a surprising number, or a
     contrarian claim; no "I'm excited to share"
   - 150–300 words, one idea per line, blank line between lines
   - a concrete example or number in the middle
   - end with the LinkedIn CTA from the profile, then 3–5 hashtags on the last line
   - no links in the body
4. Write the file:

   ```markdown
   ---
   title: "<hook line>"
   channel: linkedin
   status: draft
   keyword: "<keyword or empty>"
   secondary_keywords: []
   seo_score: null
   created: YYYY-MM-DD
   scheduled_for: null
   published_url: null
   source: <blog path or null>
   ---

   <post body exactly as it should be posted>

   ## First comment
   <link to the blog if source is set, else one sentence, or "none">
   ```
5. If the owner asked for variants, add `## Variants` with two alternative hooks plus first
   paragraphs.
6. Commit `content(linkedin): draft <slug>`. Reply with the path and the hook line.
