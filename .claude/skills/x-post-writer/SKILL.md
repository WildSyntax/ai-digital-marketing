---
name: x-post-writer
description: "Draft a single tweet or short micro-thread for X (Twitter) using a 2026 X hook formula (one-liner contrarian, data-point, build-in-public, mini-list, relatable cold-open), picked by goal (replies, reposts, likes, bookmarks). Respects the 280-char limit (25,000 on Premium) and runs the humanizer pass. Use to write a tweet from notes. Not for long threads (use x-thread-builder)."
license: MIT
metadata:
  source: "sergebulaev/x-skills@f52d7c64258de02a990eceee4378cef2c87c5600"
  path: "skills/x-post-writer"
  modified: "yes"
---

# X Post Writer

> Vendored from [sergebulaev/x-skills](https://github.com/sergebulaev/x-skills/tree/f52d7c64258de02a990eceee4378cef2c87c5600/skills/x-post-writer) under MIT.
> Changes for this workspace: removed Publora publishing, Pixfaro illustration, voice-profile/story-bank steps and links to bundle skills not vendored (x-humanizer, x-hook-extractor); copied shared references into references/; on approval returns text. Read brand/profile.md first. Return text; workspace skills own files under content/.

Ship a single tweet, or a tight 2-3 tweet micro-thread, using hook shapes that
actually travel on X in 2026. Single-tweet formulas land a complete punch in
the first line, because X has no "see more" fold.

## When to use

- User says "write me a tweet about X"
- User has a topic or a rough one-liner and wants a sharper hook
- User wants to pick a proven single-tweet shape and fill in their voice

## Formulas this skill uses (single-tweet shapes)

| Code | Formula | Primary goal | Best for |
|---|---|---|---|
| X1 | One-Liner Contrarian | reposts | a sharp, defensible against-the-grain take |
| X2 | Data-Point Hook | bookmarks | one odd-precision number that reframes a thing |
| X3 | Build-in-Public Confession | replies | a real metric from your own work, ugly ones included |
| X4 | Quote-Tweet Dunk-with-Value | reposts | adding a layer to someone else's take (quote tweet) |
| X5 | Mini-List Tweet | bookmarks | a scannable list that fits in one tweet |
| X6 | Relatable Cold-Open | likes | a specific shared moment, no setup |
| X11 | Third-Person Case-Study Flex | reposts | someone else's absurd, specific result as anyone-could-copy bait |

Full skeletons in `references/hook-formulas.md`. For long-form tweetstorms
(X7-X10), use `x-thread-builder`. X11 was validated as the top-recurring winning
shape in a ~450-tweet corpus (July 2026); prefer it over a first-person "How I"
when the result you are citing is someone else's.

### Pick by goal first

| Goal | Reach for |
|---|---|
| Replies | X3, X1 |
| Reposts | X1, X4, X11 |
| Likes | X6 |
| Bookmarks | X2, X5, X11 |

## Steps

**Brand profile first (all drafts).** Read `brand/profile.md` and match its tone, audience, banned words and default calls to action throughout.

**Never invent the specifics.** Take every concrete detail (numbers, dates, named projects, positions) from `brand/profile.md` or from what the user supplied in this conversation. **Never invent a figure, a date or a client name.** If nothing fits, ask the user. A draft with a plausible invented number is worse than a draft with none: one is vague, the other is a retraction.

1. **Gather inputs.** Topic, angle, any rough draft, target audience (builders /
   founders / a niche), and the goal (replies / reposts / likes / bookmarks).
2. **Pick the container.** If the idea is one claim, one number, or one moment,
   it is a single tweet. If it is a scannable one-line-per-item list, still a
   single tweet (X5). If items need teaching or the idea has a build, hand off
   to `x-thread-builder`.
3. **Pick the formula.** Use the goal table to shortlist, then suggest 2-3 that
   also fit the topic and let the user choose.
4. **Draft the tweet.** Fill the skeleton in the user's voice. Respect the 2026
   X rules:
   - First line carries the whole load (no fold).
   - Under 280 chars on a standard account (emoji count as 2 chars). Confirm the
     user's tier; only go long if they are on Premium and the length earns it.
   - One idea per tweet. Line breaks as beats.
   - 0-1 hashtag at the end, 0-1 emoji, none on a serious take.
   - No external link in the tweet (offer to put it in a reply).
5. **Humanizer pass.** Scrub 2026 AI vocab by density, cap em dashes (at
   most one per tweet, never swap one for a period), break stacked triads,
   generic openers and reveal bridges. Leave a single tweet's rhythm alone
   (uniform rhythm wins on short posts; never insert a fragment for punch).
   Add an odd-precision number with a named referent or a named entity where
   the claim allows it. Canonical rules: `references/voice-rules.md` and
   `references/single-tweet-checklist.md`.
6. **Approval card.** Show: formula used, full draft, char count (note if emoji
   push it over 280), suggested posting window, primary goal.
7. **On approval.** Return the text. The owner posts it, or the workspace
   `publish` skill schedules approved content via Metricool.

## Hard rules

Global voice rules: see `references/voice-rules.md`. Additional skill-specific
rules:

- The first line must stop the scroll on its own. Rewrite any opener that needs
  line 2 to make sense.
- Keep a standard-account tweet inside 280 chars. If it does not fit, tighten it
  or escalate to a thread, never ship a truncated thought.
- One specific number where the claim allows it. 2.4x beats "way better".
- Do not hard-sell the user's product. One natural mention max.

## Anti-patterns (skill will refuse)

- ALL CAPS first line for intensity. Carry intensity with word choice.
- Em dashes above the cap (more than one in a tweet), or an em dash swapped for a period.
- "Here's what / here's how" or "Stop X, start Y" as the opener; "The result?" as a reveal.
- Announced candor ("Let me be honest", "not gonna lie") with no dated fact behind it.
- "Unpopular opinion:" on a take that is actually popular.
- Padding a one-line idea with filler to look substantial.
- Rule-of-three lists without specifics.
- "leverage", "fundamentally", "game-changer", "deep dive".
- External link in the tweet body.
- Engagement bait ("RT if you agree", "reply YES").

## Resources

- `references/hook-formulas.md` - all 11 X formula skeletons (X1-X6 and X11 are single-tweet)
- `references/algorithm-heuristics.md` - 2026 X ranking rules (signals, timing, limits)
- `references/voice-rules.md` - the canonical voice rules
- `references/single-tweet-checklist.md` - the per-tweet scrub and fit list

## Related skills

- `x-thread-builder` - when the idea needs more than a tweet
