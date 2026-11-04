---
name: tt-hook-scripter
description: "Script the first 1-3 second TikTok hook: the spoken line, the on-screen text, and the opening visual firing at once so the viewer cannot swipe. Picks a 2026 hook formula (cold-open result, pattern interrupt, number reveal, open-loop question, relatable call-out, story) by goal of completion, saves, comments, or shares. The single biggest retention lever on TikTok. Use to script a hook from a video idea. Not for riding a trending sound (use tt-trend-mapper)."
license: MIT
metadata:
  source: "sergebulaev/tiktok-skills@2016087d14889213ffcc38d269ec7ddd01333450"
  path: "skills/tt-hook-scripter"
  modified: "yes"
---

# TikTok Hook Scripter

> Vendored from [sergebulaev/tiktok-skills](https://github.com/sergebulaev/tiktok-skills/tree/2016087d14889213ffcc38d269ec7ddd01333450/skills/tt-hook-scripter) under MIT.
> Changes for this workspace: removed voice-profile step and hand-offs to bundle skills not vendored (tt-caption-writer, tt-humanizer, tt-content-planner); replaced Publora posting settings in the copied algorithm reference; copied shared references into references/; on approval returns text. Read brand/profile.md first. Return text; workspace skills own files under content/.

Write the first 1 to 3 seconds of a TikTok video: the spoken line, the on-screen
text, and the opening visual, all firing at once. This is the single biggest
lever on the whole platform. TikTok's ranker runs on completion rate, and a
viewer decides to stay or swipe before second three. If the hook does not win,
nothing downstream gets watched.

## When to use

- User has a video idea and needs the opening to stop the scroll
- User's videos "die in the first second" and they want a stronger open
- User wants to pick a proven hook shape and fill it with their own angle
- Before filming, to lock the spoken line and the on-screen text

## What this skill produces

For one video idea, a ready-to-film hook block:

- **Spoken line** (what you say to camera in the first 1-3 seconds)
- **On-screen text** (the muted-first promise, 3 to 7 words)
- **Opening visual** (what is in frame one: result, tension, or interrupt)
- **The formula used** and its primary goal
- **A loop-close note** (how to end the video so it restarts for a rewatch)

It does not write the caption or the full body script beat-by-beat unless
asked; it locks the open, which is where retention is won or lost.

## Formulas this skill uses

| Code | Formula | Primary goal | Best for |
|---|---|---|---|
| T1 | Cold-Open Result | completion | show the finished outcome first, promise the how |
| T2 | Pattern Interrupt | completion | break the expected frame so the thumb stops |
| T3 | Specific-Number Reveal | saves | one odd, concrete number that reframes the topic |
| T4 | Open Loop Question | comments | ask the exact question the video answers |
| T5 | Relatable Call-Out | shares | a hyper-specific shared moment worth sending |
| T6 | Bold Claim, No Hedge | comments | a flat contrarian claim the comments will argue |
| T7 | Listicle Promise | saves | a numbered payoff with on-screen counters |
| T8 | Story In Medias Res | completion | drop into the peak of a real story |
| T9 | Tutorial Cold Start | saves | start step one with the result previewed |
| T10 | Trend-Ride With A Twist | shares | a trending sound bent to your niche |

Full skeletons (three layers each) in `references/hook-formulas.md`.

### Pick by goal first

| Goal | Reach for |
|---|---|
| Completion | T1, T2, T8 |
| Saves | T3, T7, T9 |
| Comments | T4, T6 |
| Shares | T5, T10 |

## Steps

**Brand profile first (all drafts).** Read `brand/profile.md` and match its tone, audience, banned words and default calls to action throughout.

**Never invent the specifics.** The rules below ask for a concrete number, a date and a named entity, because that is what separates a real post from a generated one. Take them from what the user actually said in this conversation. **Do not invent a figure, a date, a client name or a result, and do not soften a vague claim into a plausible-looking number.** If the user has nothing concrete for a beat, ask them once, and if they still have nothing, drop the claim rather than decorate it. A published invented number is a retraction; a missing one is only a weaker post.

1. **Gather inputs.** The video idea, the niche/audience, the one promise the
   video delivers, and the goal (completion / saves / comments / shares).
2. **Pick the formula.** Use the goal table to shortlist, then suggest 2-3 that
   also fit the idea and let the user choose. For a trend ride (T10), run the
   sound-fit check in `tt-trend-mapper` first.
3. **Write all three layers.** Spoken line, on-screen text, opening visual. The
   spoken line and the on-screen text MUST differ (muted-first viewing). Respect
   the 2026 rules:
   - The result or the tension is in frame one. No greeting, no logo, no zoom.
   - One specific number where the claim allows it.
   - Say it the way a person talks; read it out loud.
   - No AI vocabulary cluster (one marker is a slip; three in the hook is a
     script). Em dashes: `..` for a breath in the spoken line, at most one on
     the on-screen card.
   - No sincerity opener ("not gonna lie", "real talk") and no "Here's what
     nobody tells you" reveal bridge; say the thing.
4. **Write the loop-close note.** How the last frame should land so a rewatch
   feels natural (a rewatch is almost a second view).
5. **Humanizer pass.** Run the spoken line through the rules in
   `references/voice-rules.md` to strip script tells before it ever reaches
   camera: AI vocab by density, stacked triads, reveal bridges, sincerity
   openers, written-not-spoken phrasing. Make it sayable; never insert a punch
   line for rhythm.
6. **Approval card.** Show: formula, the three layers, primary goal, the
   loop-close note, and an estimated hook duration.
7. **On approval.** Return the text. The owner films and posts the video. If the
   owner wants a caption, write it under the caption rules in
   `references/voice-rules.md`.

## Hard rules

Global voice rules: see `references/voice-rules.md`. Additional skill-specific
rules:

- The hook is the first 1-3 seconds of the **video**, not the caption. Never let
  the caption do the hook's job.
- The spoken line and the on-screen text are two different jobs. Do not repeat the
  same words in both.
- Frame one shows something (result, tension, interrupt). No dead air, no intro.
- One specific number in the hook beats any adjective.
- The hook opens the loop; it never answers itself.

## Anti-patterns (skill will refuse)

- "Hey guys" / "welcome back" / "in this video" openers.
- A logo animation or slow zoom before the words start.
- Reading the caption aloud as the hook.
- Promising a result the video never shows on screen.
- ALL CAPS spoken scripts (you cannot shout for 30 seconds).
- More than one em dash, or an AI vocabulary cluster, in the on-screen text.
- A staged punch line or "The result?" reveal inserted for rhythm.
- Five stacked calls to action.

## Resources

- `references/hook-formulas.md` - all 10 TikTok hook formulas (three layers each)
- `references/algorithm-heuristics.md` - why completion and the first second rule everything
- `references/voice-rules.md` - the canonical voice rules (spoken script, on-screen text, caption)
- `references/hook-anatomy.md` - the three-layer hook teardown and timing budget

## Related skills

- `tt-trend-mapper` - check sound fit before a trend-ride hook (T10)
