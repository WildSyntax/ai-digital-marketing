---
name: community-management
description: >-
  Use to build a genuine community — turning an audience into people who interact with each
  other, not just with the brand. Run when the user asks how to build community, foster
  belonging/loyalty, create superfans, start a group/Discord channel, get members talking to each
  other, or move beyond chasing followers/virality. Reads brand/profile.md first. Community
  outperforms virality, measured by
  relationship depth/retention, not follower count. Covers the audience-to-community distinction
  (member-to-member interaction), choosing the space (in-feed -> semi-owned -> owned
  groups/Discord), recurring rituals, building belonging, and nurturing superfans into advocates.
  KPIs read natively, never fabricated. Advisory: The `publish` skill schedules the content but does NOT
  run Discord/Slack or show analytics — the human runs the community, the agent drafts. Never
  fake community; get consent before spotlighting.
license: MIT
metadata:
  version: 1.0.0
  source: "social-media-skills/skills@f28cef2b7067ec64e79c9d85421c022c06659e03"
  path: "skills/community-management"
  modified: "yes"
---

# Community Management

> Vendored from [social-media-skills/skills](https://github.com/social-media-skills/skills/tree/f28cef2b7067ec64e79c9d85421c022c06659e03/skills/community-management) under MIT.
> Changes for this workspace: WoopSocial scheduling replaced by the workspace `publish` skill (Metricool, approved content only); context path set to brand/profile.md; note on source-repo sibling skills that are not installed. Read brand/profile.md first. Return text; workspace skills own files under content/.

**Workspace notes.** Ritual, prompt and spotlight posts are drafted as text and handed to the
matching workspace skill (`linkedin-post`, `instagram-post`, `youtube-video`), which writes the
draft file; the `publish` skill schedules them through Metricool only after the owner approves
them. Return the text. The owner posts it, or the workspace `publish` skill schedules approved
content via Metricool. Other skills named in backticks below (`reply-and-comment-writer`,
`engagement-routine`, `crisis-and-moderation`, `content-pillars`, `profile-optimization`,
`audience-research`, `social-strategy`, `brand-profile`) come from the source repo and are not
installed here: cover that step inline, or use `marketing-skills:community-marketing` /
`marketing-skills:social` when the library plugin is installed.

Turn an **audience into a community** — the strategy layer of the engagement cluster. The tactical
skills handle the brand talking *to* people (`reply-and-comment-writer` = craft, `engagement-routine` =
cadence, `crisis-and-moderation` = when it goes wrong). This skill builds the space where members talk
*to each other.*

The 2026 shift is **broadcasting → belonging**: community **outperforms virality**, it's
**algorithm-proof** (closed spaces aren't suppressed by feed changes), and it's measured by
**relationship depth, not follower count.** A real community is a moat; an audience is rented.

## Step 0 — Read the context

Load `brand/profile.md` (and `.claude/product-marketing.md` if present): who these people are, what they
care about, and where they already gather. Ask the owner for anything the profile does not cover.

## Step 1 — Diagnose: audience or community?

**The marker is member-to-member.** Diagnostic: is your comment section all *brand replies*, or are
**members talking to each other**? The goal is a **self-sustaining** space where members help each
other. Then define the **purpose** — the clear reason this community exists (no purpose → it plateaus).
See `references/audience-to-community.md`.

## Step 2 — Choose the space (by audience + purpose, not hype)

Pick along the spectrum — **in-feed comment culture → semi-owned (broadcast channels/DMs) → owned
(groups/Discord/Substack/newsletter)** — by **where the audience already is** and **whether there's a
clear promise to join.** Don't launch a Discord because a competitor did. **Max out in-feed first**;
graduate the engaged into an owned space you can **commit to** (it needs moderation from day one →
`crisis-and-moderation`). See `references/where-community-lives.md`.

## Step 3 — Build belonging with rituals

Run the **seven moves** (initiate conversations, exclusive spaces, shared identity/inside language,
respond personally, feature members, surprise-and-delight, **facilitate member-to-member connections**)
on a backbone of **recurring rituals** (weekly thread, AMA, challenge, member spotlight, resource drop)
— **consistency over scattered activity.** Schedule the ritual content via the workspace `publish` skill. See
`references/building-belonging.md`.

## Step 4 — Nurture superfans

Find the devoted core, **nurture them** (recognition, access, status/roles, collaboration), and
**elevate them into advocates** (lurker → regular → advocate). A small core beats broad reach. See
`references/superfans-and-honest-scope.md`.

## Measure community, not vanity

**Active members, returning members/retention, member-to-member interaction, response time, advocacy** —
**not follower count.** Read **natively** (The `publish` skill has no analytics); **never fabricate a number.**
Community is a **long game** — judged over months.

## Honest scope (always)

- **The `publish` skill schedules the approved community content** (rituals, prompts, spotlights,
  announcements) — that's its real role. It does **not** run Discord/Slack/groups, manage a
  broadcast channel or inbox, identify superfans from data, or show analytics. **The human runs the
  space in-platform; the agent advises + drafts/schedules.**
- **No fake community** — no bought members, pods, or astroturfing (fake, detected, trust-destroying).
- **Consent & privacy** — get permission before spotlighting a member; don't expose member data.
- **Sustainable** — don't open a space you can't keep tending (boundaries → `engagement-routine`).

## Quality bar — self-check

- Did I diagnose **audience vs community** (member-to-member marker) and define a **purpose**?
- Did I choose the space by **audience + purpose, not hype**, and max out in-feed before an owned space?
- Did I design **recurring rituals** + belonging moves that get **members connecting with each other**?
- Did I plan to **nurture superfans into advocates**, and measure by **community signals (not vanity,
  not fabricated)**?
- Did I keep it **advisory + genuine** (The `publish` skill schedules content; human runs the space; no fake
  community; consent)?

## Edge cases & pushback

- **"Big following = community?"** → no; the marker is member-to-member, self-sustaining interaction.
- **"Competitor has a Discord, should we?"** → purpose gate + where the audience is; commitment/moderation.
- **"How do I measure it?"** → community signals read natively; no vanity, no fabricated numbers.
- **"Buy members / run a pod to look active"** → refuse; genuine belonging only; consent for spotlights.
- **"Run our Discord / find my top members via the `publish` skill"** → the `publish` skill schedules content, doesn't run
  spaces/inbox or show analytics; human runs it, agent drafts.

## Related

- `reply-and-comment-writer` — the personal replies that build belonging; `engagement-routine` — the cadence + boundaries.
- `crisis-and-moderation` — protecting/moderating the community; `content-pillars` — a "community" pillar.
- the workspace `publish` skill — schedule the ritual/spotlight content; `profile-optimization` — the community's front door.
- `audience-research`, `social-strategy`, `brand-profile` — who the community is for and why.

## References

- `references/audience-to-community.md` — the core distinction, why it matters, purpose, and community KPIs.
- `references/where-community-lives.md` — the in-feed → semi-owned → owned spectrum and choosing by audience + purpose.
- `references/building-belonging.md` — the seven moves, the rituals engine, UGC/live, and how the `publish` skill helps.
- `references/superfans-and-honest-scope.md` — finding/nurturing/elevating superfans, and the genuine-only honest scope.
