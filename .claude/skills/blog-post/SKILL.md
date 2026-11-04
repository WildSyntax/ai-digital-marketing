---
name: blog-post
description: Research, outline, and write an SEO-ready blog post draft into content/drafts/blog/, then score it with seo-check and revise once. Use when the owner says "write a blog on <topic or keyword>" or names a file in content/ideas/.
---

# Blog post

Input: a topic, a keyword, or a path in `content/ideas/`.
Output: `content/drafts/blog/YYYY-MM-DD-<slug>.md` with `seo_score` set, plus its SEO report.

## Steps

1. Read `brand/profile.md`, `brand/keywords.md`, and every file in `brand/examples/`.
2. Decide the primary keyword:
   - idea file: use its `keyword`
   - owner gave a keyword: use it
   - owner gave only a topic: pick the closest long-tail phrase from `brand/keywords.md`, or
     derive a 2–4 word phrase; state the choice in the reply.
   Pick 2–3 `secondary_keywords` from the same cluster.
3. Research (skip gracefully if search is unavailable; note "research unavailable" in the
   report's Sources section):
   - WebSearch the keyword and `<keyword> questions`.
   - WebFetch the top 3–5 result pages. For each note: title, H2 headings, one gap they leave.
   - Collect at least 3 facts or statistics with source URLs for citation.
4. Outline: H1 containing the keyword; 4–7 H2 sections; add `## FAQ` with 3–5 questions when
   the research shows common questions; final section is the CTA from the profile.
5. Draft in the brand voice, 1200–2000 words (or the idea file's target). Rules:
   - keyword in the first 100 words, naturally
   - paragraphs of at most 4 sentences; sentences average under 20 words
   - cite each fact inline with a Markdown link to its source
   - no banned phrases; no exclamation marks
   - one `# ` H1 only; H2 before any H3
6. Write the file with front matter (`channel: blog`, `status: draft`, `created: today`,
   `source: <idea path or null>`; when the input was an idea file, also carry its `pillar` into
   the front matter) and these sections after the body:

   ```markdown
   ## Meta description
   <150–160 characters, contains the keyword, ends with a reason to click>

   ## Suggested internal links
   - <anchor text> → /<path on site_domain> (why)
   - <anchor text> → /<path> (why)

   ## Image brief
   Hero: <one sentence visual idea>
   Alt text: <descriptive alt text containing the keyword>

   ## Sources
   - <title> — <url>
   ```
7. Run the seo-check skill on the new file.
8. If the score is below `seo_threshold`: apply the top fixes from the report, then run
   seo-check once more. Do not loop further; report the remaining fixes.
9. If the input was an idea file, `git rm` it (the draft's `source` records its path).
10. Commit: `content(blog): draft <slug>`.
11. Reply: path, keyword, score and PASS/FAIL, remaining fixes, and "say `approve <path>`
    when ready".
