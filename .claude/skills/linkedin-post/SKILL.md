---
name: linkedin-post
description: Write a LinkedIn post draft into content/drafts/linkedin/ from a topic or from a blog post. Use when the owner says "linkedin post about <topic>" or "linkedin post from <blog file>", or when repurpose calls it.
---

# LinkedIn post

Input: a topic, or a path to a blog file (drafts, approved, or published).
Output: `content/drafts/linkedin/YYYY-MM-DD-<slug>.md`.

## Requires

- Library: `marketing-skills@marketingskills` plugin. Check or install it with the
  setup-workspace skill (owner says "setup"). Calls: `marketing-skills:social`, `marketing-skills:copy-editing`.
- Connectors: none.

If the library is not installed, skip every step marked **Library**, carry on, and add
"marketing-skills library not installed; say `setup` to fix" to the reply. Library skills
return text only: this skill writes the file, keeps its front matter and section layout, and
rejects any library suggestion that uses a banned phrase from `brand/profile.md`.

## Steps

1. Read `brand/profile.md` and any `brand/examples/linkedin-*.md`.
2. If a blog path was given, read it and pick the single most useful insight or list from it.
   Set `source` to that path and `keyword` to the blog's keyword.
3. Write the post:
   - line 1: a hook under 12 words that states a problem, a surprising number, or a
     contrarian claim; no "I'm excited to share"
   - 150–300 words in short paragraphs of 1–3 sentences, blank line between paragraphs;
     never one sentence per line for the whole post; no em dashes
   - a concrete example or number in the middle
   - end with the LinkedIn CTA from the profile, then 3–5 hashtags on the last line
   - no links in the body
   - **Library:** use `marketing-skills:social` LinkedIn guidance for the hook and line
     rhythm (no broetry, no "it's not X, it's Y" reveals), then run
     `marketing-skills:copy-editing` on the body. The rules above win over library advice.
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
   <if source is set: the blog link, taken from the source blog's `published_url` when that is an
   http(s) URL, otherwise the literal line `TODO: add blog URL once published`; if source is not set:
   one sentence, or "none">
   ```
5. If the owner asked for variants, add `## Variants` after `## First comment`, with two alternative hooks plus first
   paragraphs (**Library:** generate them with `marketing-skills:social`).
6. Commit `content(linkedin): draft <slug>`. Reply with the path and the hook line.
