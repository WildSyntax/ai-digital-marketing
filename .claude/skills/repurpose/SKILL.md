---
name: repurpose
description: Turn an approved blog post into LinkedIn, Instagram, and YouTube drafts, each with source set to the blog. Use when the owner says "repurpose <blog file>".
---

# Repurpose

Input: a path in `content/approved/blog/` or `content/published/blog/`.
Output: one new draft in each of `content/drafts/linkedin/`, `content/drafts/instagram/`,
`content/drafts/youtube/`.

## Requires

- Library: `marketing-skills@marketingskills` plugin. Check or install it with the
  setup-workspace skill (owner says "setup"). Calls: `marketing-skills:social` (through linkedin-post, instagram-post, youtube-video).
- Connectors: same as those skills.

If the library is not installed, skip every step marked **Library**, carry on, and add
"marketing-skills library not installed; say `setup` to fix" to the reply. Library skills
return text only: this skill writes the file, keeps its front matter and section layout, and
rejects any library suggestion that uses a banned phrase from `brand/profile.md`.

## Steps

1. Confirm the path is under `content/approved/blog/` or `content/published/blog/`. If it is
   still in drafts, reply "Approve the blog first (`approve <path>`), then repurpose." and stop.
2. Read the blog once. Note its keyword, H2 list, strongest statistic, and strongest practical
   tip.
   **Library:** use `marketing-skills:social` repurposing guidance to pick a different angle
   per channel, so the three drafts do not repeat the same line.
3. Run the linkedin-post skill with the blog path. Use the strongest practical tip as the
   angle.
4. Run the instagram-post skill with the blog path. Use the H2 list as the image list, or the
   strongest statistic as the headline.
5. Run the youtube-video skill with the blog path.
6. Each skill commits its own file. Reply with the three paths and one line per draft saying
   its angle.
