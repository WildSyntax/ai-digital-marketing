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

## Counting rules

These settle every ambiguity above; apply them exactly.

- **Keyword empty:** `keyword` that is null, empty, or whitespace-only counts as empty (step 2).
- **Keyword matching (checks 1-4, 6):** lowercase both keyword and text, replace every run of
  non-alphanumeric characters (hyphens and punctuation included) with one space, trim, then look
  for the keyword as a whole-word phrase. Hyphens become spaces, they are not deleted, so
  `e-commerce analytics` matches "E-commerce analytics" and "e commerce analytics" but not
  "ecommerce analytics". Variants (plurals, spellings, synonyms, `secondary_keywords`) never count.
- **Slug (check 5):** lowercase the keyword, replace each run of non-alphanumeric characters
  with `-`, and require that exact string as a substring of the slug. `e-commerce-analytics`
  is not found in `ecommerce-analytics`.
- **Title and meta text:** title is measured after YAML unquoting. Meta is the text under
  `## Meta description`, trimmed, with multiple lines joined by single spaces. Lengths are
  characters of that text.
- **Body words (checks 3, 6, 11):** use prose only. Remove headings (all `#` lines), the
  Markdown syntax characters, link URLs (keep link text), image syntax, list markers and table
  separator rows. List items and table cell text count as words. A word is a
  whitespace-separated token. Check 11, density and the sentence average all use this count.
- **First 100 words (check 3):** the first 100 words of body prose, counted from the first
  word after the H1 line. Headings are not in the range, so a keyword in the H1 does not
  satisfy check 3.
- **Density (check 6):** use the unrounded value. Bands are inclusive on the higher-scoring
  side: 0.5% and 2.0% earn full points; 0.3% to below 0.5% and above 2.0% to 3.0% earn 5.
- **Readability (check 12):** sentences are prose paragraphs only (headings, list items, table
  rows and block quotes excluded), split on `.`, `!` or `?` followed by whitespace or end of
  text. Average = prose words in those paragraphs ÷ sentence count. A paragraph is a block of
  prose text separated by blank lines; its length is its word count.
- **Headings (check 8):** count only `##` lines inside the body. The excluded sections from
  step 3 (`## Meta description`, `## Suggested internal links`, `## Image brief`,
  `## Sources`) are not H2s. Exactly `## ` and `### ` prefixes define H2 and H3.
- **Links (checks 13, 14):** deduplicate by URL (ignoring a trailing `/` and `www.`, so
  `www.example.com` equals `example.com` for `site_domain`). A URL appearing in both the body
  and `## Suggested internal links` counts once. Ignore `#anchor`-only and `mailto:` links.
  Internal = host equals `site_domain` or relative path starting with `/`. Check 14 counts any
  external http(s) link in the body (it need not be listed under `## Sources`).
- **Images (check 15):** inline images are `![alt](url)` in the body. Zero inline images
  passes the first clause. The second clause always applies: `## Image brief` must contain a
  line starting `Alt text:` with non-empty text after it. The Alt text line is not itself an
  image. Both clauses are required for the 5 points.
- **Score and result:** earned points are summed as integers. PASS if score >= `seo_threshold`,
  otherwise FAIL; if the profile lacks `seo_threshold`, use 70.
- **Fixes:** list only checks that lost points, ordered by points lost (most first), ties by
  check number. If the score is 100, write "No fixes needed".
- **Front matter:** if `seo_score` is absent, add `seo_score: <score>` on a new line after
  `keyword`.

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
