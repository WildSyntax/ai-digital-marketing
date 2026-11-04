---
name: x-thread-builder
description: "Build a long-form X (Twitter) thread (tweetstorm) using a 2026 thread formula (listicle-thread, story thread, curiosity-gap opener, how-I teardown), picked by goal (bookmarks, likes, reposts, replies). Structures tweet 1 as a promise plus open loop, paces one beat per tweet, and closes for the repost. Returns the thread hand-split with --- separators. Not for single tweets (use x-post-writer)."
license: MIT
metadata:
  source: "sergebulaev/x-skills@f52d7c64258de02a990eceee4378cef2c87c5600"
  path: "skills/x-thread-builder"
  modified: "yes"
---

# X Thread Builder

> Vendored from [sergebulaev/x-skills](https://github.com/sergebulaev/x-skills/tree/f52d7c64258de02a990eceee4378cef2c87c5600/skills/x-thread-builder) under MIT.
> Changes for this workspace: removed Publora publishing and auto-split section, voice-profile/story-bank steps and links to bundle skills not vendored (x-humanizer, x-hook-extractor, x-content-planner); copied shared references into references/; on approval returns text. Read brand/profile.md first. Return text; workspace skills own files under content/.

Build tweetstorms that get read all the way down. On X, tweet 1 is the entire
funnel: it has to promise a payoff and open a loop, or no one taps "Show this
thread." Everything after only matters if tweet 1 earns the tap.

## When to use

- User says "turn this into a thread" or "write me a thread about X"
- The idea is a list where each item needs teaching, a story with a build, a
  surprising result with a mechanism, or a repeatable process
- User has a single tweet that is trying to do too much and should be a thread

## Formulas this skill uses (thread shapes)

| Code | Formula | Primary goal | Best for |
|---|---|---|---|
| X7 | Listicle-Thread Promise | bookmarks | numbered teaching thread, one item per tweet |
| X8 | Story Thread | likes, reposts | a real narrative with a build and a turn |
| X9 | Curiosity-Gap Opener | replies, bookmarks | a surprising result, mechanism withheld |
| X10 | How-I Teardown | bookmarks | a repeatable process you ran yourself |

Full skeletons in `references/hook-formulas.md`. For single tweets
(X1-X6), use `x-post-writer`.

### Pick by goal first

| Goal | Reach for |
|---|---|
| Bookmarks | X7, X10, X9 |
| Likes | X8 |
| Reposts | X8 |
| Replies | X9 |

## Thread format

Hand-split the thread with a `---` separator on its own line between tweets, so
the user sees exactly how the thread will land before approving. Add `(1/N)`
numbering in the text only if the user wants it (it counts toward 280 chars).

## Steps

**Brand profile first (all drafts).** Read `brand/profile.md` and match its tone, audience, banned words and default calls to action throughout.

**Never invent the specifics.** Take every concrete detail (numbers, dates, named projects, positions) from `brand/profile.md` or from what the user supplied in this conversation. **Never invent a figure, a date or a client name.** If nothing fits, ask the user. A draft with a plausible invented number is worse than a draft with none: one is vague, the other is a retraction.

1. **Gather inputs.** Topic, the raw material (notes, a transcript, a result),
   target audience, and the goal (bookmarks / likes / reposts / replies).
2. **Pick the formula** from the goal table, confirm it fits the material.
3. **Write tweet 1.** This is 80% of the work:
   - Promise a specific payoff (a number, a named result, a clear list count).
   - Open a loop the reader has to resolve ("most people get 3 of them wrong",
     "I did not expect why").
   - Keep it under 280 chars on a standard account. It must stop the scroll
     alone.
4. **Pace the body.** One beat or one item per tweet. Front-load the strongest
   item or beat at position 1-2; tap-through decays with depth. Target 5-9
   tweets for teaching/list threads; longer only for a strong story.
5. **Make each tweet stand alone.** A reader landing mid-thread from a quote
   tweet should still get something.
6. **Write the closer.** The last tweet earns the repost and the follow. End on
   the most quotable line, then one clear ask (bookmark, follow, or "reply with
   yours"), not both.
7. **Humanizer pass** on every tweet. Scrub 2026 AI vocab by density, cap em
   dashes (at most one per tweet, never swap one for a period), break stacked
   triads and reveal bridges. Let tweet length vary only as the material
   varies: never insert a 3-word punch tweet for rhythm, never alternate
   long/short, and touch rhythm only if the whole thread reads machine-flat.
   Canonical rules: `references/voice-rules.md` and the per-tweet scrub in
   `references/thread-structure.md`.
8. **Approval card.** Show the thread tweet-by-tweet with per-tweet char counts,
   total tweet count, the formula, and the goal. Confirm any `---` breaks.
9. **On approval.** Return the text (with the `---` breaks). The owner posts it,
   or the workspace `publish` skill schedules approved content via Metricool.

## Hard rules

Global voice rules: see `references/voice-rules.md`. Additional skill-specific
rules:

- Tweet 1 must contain a real promise and an open loop. A bare "A thread:" label
  is not a hook.
- Keep each tweet under 280 chars on a standard account (emoji = 2 chars).
- Front-load value. Never bury the best item at the end of a teaching thread.
- No external link in tweet 1. Put links in a later tweet or a reply.
- Natural rhythm, not manufactured variance. A long thread where every tweet
  is the same length and none carries a real clause reads machine-flat; fix
  that one thing. Never pad or chop tweets to create variance, and never
  insert a punch tweet: the inserted punch is the humanizer fingerprint.
- Only ship a Story Thread (X8) built on a true story. Readers punish
  manufactured stakes.

## Anti-patterns (skill will refuse)

- Tweet 1 that closes its own loop (no reason to expand).
- Over-promising in tweet 1 and under-delivering in the body.
- Vague how-to steps ("be consistent", "add value") in an X10 teardown.
- Padding to hit a round number of tweets.
- Em dashes above the cap (more than one in a tweet), AI vocab clusters, ALL CAPS openers.
- "The result?" reveals, "No X. No Y. Just Z." staccato stacks, one-word tweets for drama.
- Announced candor ("Let me be honest", "not gonna lie") with no dated fact behind it.
- Engagement-bait closers ("RT if this helped").

## Resources

- `references/hook-formulas.md` - X7-X10 thread skeletons with worked shapes
- `references/algorithm-heuristics.md` - thread length, tap-through decay, signals
- `references/voice-rules.md` - the canonical voice rules
- `references/thread-structure.md` - per-position pacing and the closer playbook

## Related skills

- `x-post-writer` - when the idea is really just one tweet
