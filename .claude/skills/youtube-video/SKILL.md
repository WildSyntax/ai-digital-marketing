---
name: youtube-video
description: Write a YouTube video package (title options, description, tags, full script, thumbnail brief) into content/drafts/youtube/. Use when the owner says "youtube video about <topic>" or "from <blog file>", or when repurpose calls it.
---

# YouTube video

Input: a topic, or a path to a blog file.
Output: `content/drafts/youtube/YYYY-MM-DD-<slug>.md`.

## Steps

1. Read `brand/profile.md` and any `brand/examples/youtube-*.md`.
2. If a blog path was given, read it; the script follows the blog's H2 structure. Set
   `source` and `keyword` from the blog.
3. Keyword research, only if the `vidiq` connector is connected: call
   `vidiq_keyword_research` with the keyword; pick the top 3 related terms by search volume
   and low competition as `secondary_keywords`. If not connected, derive 3 related terms
   yourself and note "vidIQ not connected" in the reply.
4. Write the file:

   ```markdown
   ---
   title: "<title option 1>"
   channel: youtube
   status: draft
   keyword: "<keyword>"
   secondary_keywords: [<3 terms>]
   seo_score: null
   created: YYYY-MM-DD
   scheduled_for: null
   published_url: null
   source: <blog path or null>
   video_file: null
   ---

   ## Title options
   1. <≤ 60 chars, keyword near the start>
   2. <≤ 60 chars, curiosity angle>
   3. <≤ 60 chars, number or outcome angle>

   ## Description
   <2 lines containing the keyword, visible above the fold>

   <3–5 line summary of what the viewer learns>

   Chapters:
   00:00 Intro
   <one line per script section; keep 00:00 placeholders for timing after recording>

   <YouTube CTA from profile>
   <if source is set: the blog link from the source blog's `published_url` when that is an http(s)
   URL, otherwise the literal line `TODO: add blog URL once published`>
   #<3 hashtags>

   ## Tags
   <10–15 comma-separated tags, keyword first>

   ## Script
   ### Hook (0:00–0:30)
   <state the problem and the promise; under 80 words>
   ### <Section per H2 or key point>
   <spoken, conversational, short sentences; "you" voice; 120–200 words per section>
   ### Close
   <recap in 3 lines, then CTA>

   ## Thumbnail brief
   Text: <≤ 4 words>
   Visual: <one sentence>
   Emotion/face: <one phrase>
   ```
   Script length target: 5–8 minutes spoken, about 750–1200 words.
5. Commit `content(youtube): draft <slug>`. Reply with the path, title option 1, and script
   word count.
