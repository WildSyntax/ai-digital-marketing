---
name: seo-check
description: Score a blog draft 0-100 for on-page SEO (keyword placement and density, title and meta length, heading structure, readability, links, alt text) and write a fix list. Use when the owner says "seo check <file>" or when blog-post finishes a draft.
---

# SEO check

Input: path to a Markdown file in `content/drafts/blog/` or `content/approved/blog/`.
Output: `reports/seo/<filename>.md` and `seo_score` set in the file's front matter.
This skill never moves files.

## Steps

1. Read `brand/profile.md`; note `seo_threshold` and `site_domain`.
2. Read the file. Parse front matter. If `keyword` is empty, stop and ask the owner for the
   primary keyword.
3. Extract:
   - title: front matter `title`
   - slug: filename without the date prefix and `.md`
   - H1: the first line starting with `# `
   - meta: text under `## Meta description`
   - body: everything from H1 to the first of `## Meta description`, `## Suggested internal
     links`, `## Image brief`, `## Sources` (exclude those sections from word counts)
   - headings: all `##`/`###` lines in body
   - links: Markdown links in body; internal = host equals `site_domain` or path starts with
     `/`; external = any other host. Also count entries under `## Suggested internal links`
     as internal.
   - images: `![alt](url)` in body plus the alt text line under `## Image brief`
4. Score each check. Keyword matching is case-insensitive and ignores punctuation.

   | # | Check | Points |
   |---|---|---|
   | 1 | keyword in title | 10 |
   | 2 | keyword in H1 | 5 |
   | 3 | keyword in first 100 words of body | 10 |
   | 4 | keyword in meta description | 5 |
   | 5 | keyword (hyphenated) in slug | 5 |
   | 6 | keyword density 0.5–2.0% of body words (5 pts if 0.3–0.5 or 2.0–3.0) | 10 |
   | 7 | exactly one H1 | 5 |
   | 8 | at least 3 H2s and no H3 before the first H2 | 5 |
   | 9 | title length 50–60 chars (3 pts if 40–70) | 5 |
   | 10 | meta length 150–160 chars (3 pts if 120–170) | 5 |
   | 11 | body word count ≥ 1200 (5 pts if ≥ 800) | 10 |
   | 12 | readability: average sentence ≤ 20 words AND no paragraph > 150 words (5 pts if only one holds) | 10 |
   | 13 | ≥ 2 internal links (including suggested) | 5 |
   | 14 | ≥ 2 external links to sources in body | 5 |
   | 15 | every image has non-empty alt text, and `## Image brief` includes an alt text line | 5 |

   Total 100. Density = occurrences of the exact keyword phrase ÷ body words × 100.
5. Write `reports/seo/<filename>.md`:

   ```markdown
   # SEO report: <title>
   File: <path>  Keyword: <keyword>  Score: <score>/100  Threshold: <seo_threshold>  Result: PASS|FAIL
   Checked: YYYY-MM-DD

   | # | Check | Points | Earned | Note |
   |---|---|---|---|---|
   (one row per check; Note gives the measured value, e.g. "title is 44 chars")

   ## Fixes
   (ordered by points lost, most first; each one concrete, e.g. "Add 'e-commerce analytics'
   to the title; current: '...'")
   ```
6. Set `seo_score: <score>` in the draft's front matter (replace the existing line).
7. Reply in chat: score, PASS/FAIL against threshold, and the top 3 fixes.
