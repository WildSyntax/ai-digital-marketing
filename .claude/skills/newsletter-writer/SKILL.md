---
name: newsletter-writer
description: >-
  Plans and drafts newsletter issues for a publication on Substack, beehiiv, Kit or a LinkedIn
  newsletter: the niche, the edition structure (subject, hook, one core idea, personal aside, one
  CTA, P.S.), the 70-20-10 value mix, the web-archive version, and the loop between newsletter
  issues and social posts. Use when the owner asks to "write a newsletter issue," "draft this
  week's edition," "start or grow a newsletter," "Substack vs beehiiv," or "turn this issue into
  social posts (or vice versa)." Uses the INBOX framework. Reads brand/profile.md first. Returns
  text only: the owner sends the issue from their own newsletter platform, and social posts derived
  from it go through the workspace drafting skills. Lifecycle, onboarding, welcome, drip and other
  automated email sequences belong to marketing-skills:emails, not this skill. Metrics come from the
  newsletter platform and GA4, never fabricated; consent and unsubscribe are required.
license: MIT
metadata:
  version: 1.0.0
  source: "social-media-skills/skills@f28cef2b7067ec64e79c9d85421c022c06659e03"
  path: "skills/email-and-newsletter"
  modified: "yes"
---

# newsletter-writer

> Vendored from [social-media-skills/skills](https://github.com/social-media-skills/skills/tree/f28cef2b7067ec64e79c9d85421c022c06659e03/skills/email-and-newsletter) under MIT.
> Changes for this workspace: renamed from email-and-newsletter and narrowed to newsletter issues (Substack/beehiiv/Kit); lifecycle and drip sequences routed to `marketing-skills:emails`; WoopSocial replaced by the workspace drafting skills and `publish` (Metricool); note on source-repo sibling skills that are not installed. Read brand/profile.md first. Return text; workspace skills own files under content/.

**Scope in this workspace.** This skill writes **newsletter issues** (one edition at a time, plus
the strategy around the publication). It does not design lifecycle email: welcome, onboarding,
nurture, re-engagement or other automated drip sequences go to **`marketing-skills:emails`**
(when the library plugin is installed). Where the references below mention a welcome sequence,
only plan what edition 2 and the first issues should deliver; hand the sequence itself to
`marketing-skills:emails`.

**Output.** Return the issue as text (subject options, preview text, body, P.S.). The owner
sends it from their newsletter platform. For social posts that promote or repurpose an issue,
hand the text to `linkedin-post`, `instagram-post` or `youtube-video`, which write the draft
files; once the owner approves them, the workspace `publish` skill schedules them via
Metricool. Never create or move files under `content/`.

**Not installed here.** Skills named in the sections below (`voice-builder` aside, which is
installed) come from the source repo: `link-in-bio-and-traffic`, `cross-platform-repurposing`,
`content-recycling`, `lead-magnets-and-funnels`, `social-selling-and-dm`, `content-pillars`,
`analytics-and-reporting`, `reels-script`, `ai-video`, `carousel-writer`, `caption-writer`,
`hook-writer`, `linkedin-post-writer`, `ai-search-optimization`, `social-seo`, `linkedin-growth`,
`goals-and-kpis`, `experimentation`. Cover those steps inline or use the nearest workspace skill
(`repurpose`, `linkedin-post`, `instagram-post`) or library skill (`marketing-skills:lead-magnets`,
`marketing-skills:ai-seo`, `marketing-skills:ab-testing`, `marketing-skills:analytics`).

The **owned channel** — the newsletter is the audience layer social can't take away, plus the
newsletter↔social loop. The agent strategizes + drafts; the **newsletter platform is external +
human-run**; social posts derived from an issue go through the workspace drafting skills and,
once approved, **the workspace `publish` skill (Metricool)**.

## The POV: own the audience, run two surfaces
Every platform *rents* you attention and can change the rules overnight; a newsletter is the one audience
layer you **own** — opt-in, deliverable, measurable, the **highest-ROI channel** and the thing that makes
everything else compound. "Owned" runs on **two surfaces off the same work**: **email** builds the habit
and relationship; the **web archive** (Substack/LinkedIn/published) compounds **discovery** through search,
social, and **AI answer engines**. Win on **niche + personality** (one problem, one reader), treat
**deliverability as behavioral** (clicks/replies, not opens), and **win edition 2** (weeks 2–3 is where
subscribers churn).

## Read these first
1. **`brand/profile.md`** — positioning, audience, Tone, banned words, pillars.
2. **voice-builder** output, if the owner has pasted it into the Tone section — the personality that is the moat.
3. **Content pillars** in `brand/profile.md` — the one problem/topic the newsletter owns.

## The framework: INBOX
(Depth: `references/the-inbox-framework.md`.)
- **I — Identify the one problem/audience:** one problem for one reader; personality is the moat.
- **N — Nurture an owned list:** capture from social — simple form + lead magnet; own your
  domain/list; make edition 2 high-value (automated welcome sequences → `marketing-skills:emails`).
- **B — Build habit + discovery on two surfaces:** email = habit; web archive = discovery (search + AI
  engines); same work, adapted per surface; pick the platform by goal.
- **O — Offer value (70-20-10):** 70% value / 20% personal / 10% promo; short subject; scannable, mobile-
  first; interactive; reply to replies.
- **X — eXpand via the social↔newsletter loop:** one issue → a week of social; best social → next issue;
  measure clicks/replies/signups from the newsletter platform (not opens).

## The reality (verify-quarterly)
Owned-audience ROI; email-habit + web-discovery (+ AI engines); behavioral deliverability (clicks/replies
> opens; SPF/DKIM/DMARC, list hygiene, cadence); niche + personality; capture + 70-20-10 + retention
(weeks 2–3); platforms (beehiiv/Substack/LinkedIn/Kit — own your domain/list); honest monetization; the
social↔newsletter loop: `references/newsletter-2026-reality.md`. Edition structure, repurposing engine,
platform cheat-sheet + worked examples: `references/editions-and-repurposing.md`.

## Honest scope (never violate)
- **This workspace does not send email** (no ESP/list/capture/open tracking). Sending happens in the
  owner's **newsletter platform**, set up by a human. The agent **strategizes + drafts** issues +
  social-promo text; social posts go through the workspace drafting skills and `publish`.
- **Metrics from the newsletter platform + GA4** (clicks/replies/signups, not opens-as-vanity); **never fabricate.**
- **Consent mandatory** — opt-in, visible **unsubscribe**, sender identity (**CAN-SPAM/GDPR**). **No
  bought lists / no-consent sends / misleading subjects / spam.** **Monetize honestly.**
  (Scope, distinctions + connections: `references/scope-and-connections.md`.)

## Distinct from its siblings (route correctly)
**newsletter-writer (this)** = newsletter issues + the newsletter↔social loop ·
**`marketing-skills:emails`** = lifecycle, welcome, onboarding and drip sequences ·
**`marketing-skills:cold-email`** = outbound · **`repurpose`** = an approved blog → social drafts ·
**`marketing-skills:lead-magnets`** = the magnet design.

## Where this connects
Reads first: **`brand/profile.md`**. Repurpose engine: **`linkedin-post`**, **`instagram-post`**,
**`youtube-video`** (they write the draft files). Discovery: **`marketing-skills:ai-seo`** for the web
archive. Publish (social side, approved items only): **the workspace `publish` skill (Metricool)**.
A/B subject lines: **`marketing-skills:ab-testing`**.

## Definition of done
A focused niche (one problem/one reader) in the brand voice; an issue with short, honest subject
options, scannable and interactive, at 70-20-10; edition 2 planned as the highest-value send (any
automated welcome sequence handed to `marketing-skills:emails`); the web-archive version adapted for
search and AI engines; the social↔newsletter loop running both ways through the workspace drafting
skills; metrics taken from the newsletter platform + GA4 (clicks/replies/signups, not opens, nothing
fabricated) with consent + unsubscribe; the send stays with the owner's newsletter platform.
