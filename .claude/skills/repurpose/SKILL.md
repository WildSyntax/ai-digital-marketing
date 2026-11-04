---
name: repurpose
description: Turn an approved blog post into LinkedIn, Instagram, and YouTube drafts, each with source set to the blog. Use when the owner says "repurpose <blog file>".
---

# Repurpose

Input: a path in `content/approved/blog/` or `content/published/blog/`.
Output: one new draft in each of `content/drafts/linkedin/`, `content/drafts/instagram/`,
`content/drafts/youtube/`.

## Steps

1. Confirm the path is under `content/approved/blog/` or `content/published/blog/`. If it is
   still in drafts, reply "Approve the blog first (`approve <path>`), then repurpose." and stop.
2. Read the blog once. Note its keyword, H2 list, strongest statistic, and strongest practical
   tip.
3. Run the linkedin-post skill with the blog path. Use the strongest practical tip as the
   angle.
4. Run the instagram-post skill with the blog path. Use the H2 list as the image list, or the
   strongest statistic as the headline.
5. Run the youtube-video skill with the blog path.
6. Each skill commits its own file. Reply with the three paths and one line per draft saying
   its angle.
