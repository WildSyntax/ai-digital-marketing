---
name: topic-ideas
description: Suggest 5-10 new blog topic ideas from the brand's keyword clusters and current web trends, deduplicated against existing content, written to content/ideas/. Use when the owner says "ideas" or "topic ideas for <theme>", and in the Monday routine.
---

# Topic ideas

Input: optional theme or cluster name.
Output: 5–10 files in `content/ideas/`.

## Requires

- Library: `marketing-skills@marketingskills` plugin. Check or install it with the
  setup-workspace skill (owner says "setup"). Calls: `marketing-skills:content-strategy`.
- Connectors: `vidiq` (optional); WebSearch.

If the library is not installed, skip every step marked **Library**, carry on, and add
"marketing-skills library not installed; say `setup` to fix" to the reply. Library skills
return text only: this skill writes the file, keeps its front matter and section layout, and
rejects any library suggestion that uses a banned phrase from `brand/profile.md`.

## Steps

1. Read `brand/profile.md` (pillars) and `brand/keywords.md`. If a theme was given, use only
   the matching cluster(s); otherwise use all.
2. List existing titles and keywords from every `.md` under `content/` (all stages) so you
   can avoid repeats.
3. For each cluster: WebSearch `<head keyword>`, `<head keyword> 2026`, and
   `<head keyword> questions`. From the results note recurring questions, new developments,
   and angles competitors cover thinly. If the `vidiq` connector is connected, also call
   `vidiq_keyword_research` on the head keyword and note high-volume, low-competition terms.
4. **Library:** use `marketing-skills:content-strategy` to sort the research into
   searchable vs shareable topics and hub/spoke clusters, and prefer ideas that fill a gap in
   a pillar's cluster.
   Generate 5–10 ideas total, spread across pillars. Drop any whose keyword or title closely
   matches an existing item (same keyword, or title sharing 4+ significant words).
5. Write each idea as `content/ideas/YYYY-MM-DD-<slug>.md`:

   ```markdown
   ---
   title: "<working title with keyword>"
   channel: blog
   status: idea
   keyword: "<long-tail keyword>"
   secondary_keywords: [<2–3>]
   seo_score: null
   created: YYYY-MM-DD
   scheduled_for: null
   published_url: null
   source: null
   pillar: "<pillar name>"
   ---

   ## Angle
   <two sentences: the specific take and who it is for>

   ## Why now
   <one sentence citing a trend, question, or gap, with a source URL>

   ## Outline
   - <H2>
   - <H2>
   - <H2>
   - <H2>

   ## Sources
   - <url>
   ```
6. Commit `content(ideas): add <n> ideas YYYY-MM-DD`.
7. Reply with a numbered list: title, keyword, pillar; and "say `write <path>` to draft one".
