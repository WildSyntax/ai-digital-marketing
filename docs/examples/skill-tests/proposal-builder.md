# proposal-builder test
Prompt: "Write a proposal for Acme Outdoor: monthly content package (4 blogs, 12 LinkedIn posts, 8 Instagram posts), 3 months, $2,500 a month, 50% deposit."
Date: 2026-11-05
Result: PASS WITH ISSUES

Test notes (tester, not skill output):
- The Skill tool returned `Unknown skill: proposal-builder` (the session's skill list was built before the folder was added at 00:21). The tester followed `.claude/skills/proposal-builder/SKILL.md` by hand.
- Step 1 question ("where should the material come from?"): no connectors connected, so the only choice was paste; the tester answered "the brief in the prompt is all there is".
- Voice: `brand/profile.md` holds only "Example:" values and no samples were pasted, so `references/voice-profile.md` says to ask for three emails. Tester answered "decline, use the brand profile tone" (clear, confident, warm; no hype, no exclamation marks).
- Apollo research offer: skipped silently (Apollo not connected), as the skill says.
- No send, e-signature, invoice, payment link or task creation was attempted. Output is text only.

---

## Proposal: Acme Outdoor, 3-month content package

**USD 7,500** (USD 2,500 a month x 3 months) · Priced at the figure you gave. No ledger, rate card or past proposal is connected or uploaded, so there were no comparables to check it against.

Based on: your stated price of USD 2,500 a month. That works out to about USD 104 per piece across 24 pieces a month. I have not split it into per-channel lines, because that would mean inventing a blog rate and a social rate. Give me your per-piece rates if you want the investment table broken out.

### Open assumptions

- **What "50% deposit" means.** I read it as 50% of the 3-month total (USD 3,750 on signing), with the rest split over months 2 and 3. If you meant 50% of the first month (USD 1,250), the deposit is USD 2,500 smaller and you carry more risk in month 1.
- **Blog length.** Not given. I left it as a blank. A 2,000-word post costs roughly twice what an 800-word one does to write. If you fill this in after you price it, you lose money.
- **Revisions.** Not given. I put two rounds per piece and marked it for you to confirm. With no limit, the 12 LinkedIn posts alone could eat a week.
- **Images.** I assumed Acme supplies the photos and we do simple branded graphics only. If they expect original photography or stock licences, that is extra cost the price does not cover.
- **Publishing.** I assumed we deliver ready-to-post files and Acme publishes. If they want us to schedule and post, add a line.

### Worth knowing before you send

- **Fit with your positioning.** Your brand profile describes Northwind as a store-data and decisions business. A pure content package for an outdoor retailer is a different service. Make sure you want to be known for it, and that the work can carry your data angle (for example, blogs built on their sales data).
- **Volume against price.** 24 pieces a month at about USD 104 each is thin margin for blog posts, especially with research and SEO. Most of the risk sits in the 4 blogs.
- **Three months is short for SEO.** Blog results usually show up after month 3. Acme may judge the work just before it starts paying off. Say this in your cover note, or offer a 6-month option.
- **Terms are defaults, not yours.** Net 15, 30-day validity and two revision rounds are conservative defaults, because I had no past proposals to copy your usual terms from. Change them to what you normally use.

---

**Northwind Analytics**
example.com

**Proposal for:** Acme Outdoor, attention: ______________ (contact name and email)
**Proposal number:** NW-2026-____
**Date:** 5 November 2026
**Valid until:** 5 December 2026

### What you asked for

You want a steady flow of content across your blog, LinkedIn and Instagram, without having to write it yourselves. You asked for a fixed monthly package over three months, so you can see how it performs before committing longer.

### What we'll do

Each month, for three months:

| Deliverable | Quantity per month | Total over 3 months |
|---|---:|---:|
| Blog posts, up to ______ words each, with SEO title, meta description and one internal link suggestion | 4 | 12 |
| LinkedIn posts, written for your company page | 12 | 36 |
| Instagram posts: caption, hashtags and one simple branded graphic each | 8 | 24 |

How each month runs:

1. In the first week we agree the month's topics with you in one 30-minute call.
2. We deliver drafts in two batches, mid-month and end of month.
3. You get two rounds of revisions per piece, returned within 5 business days of your feedback.
4. Approved pieces are delivered as ready-to-post files (Markdown or Google Doc for blogs, text and image files for social).

### What's not included

- Publishing, scheduling or posting the content on your channels
- Original photography, video, or paid stock image licences
- Paid ads, boosted posts or ad management
- Replying to comments or messages, and community management
- Website changes, page design or technical SEO work
- More than two revision rounds per piece, or rewriting a piece after its topic changes
- Content beyond the monthly quantities above. Unused pieces do not roll over to the next month

### This price assumes

- Acme Outdoor supplies product photos and brand assets (logo, colours, fonts) before work starts. If you need us to source images, we will quote it separately.
- One person at Acme gives consolidated feedback on each batch.
- Feedback arrives within 5 business days. If it takes longer, the delivery dates move by the same amount.
- Blog posts are up to the word count stated above. Longer pieces are quoted separately.

### Investment

| Item | Amount |
|---|---:|
| Monthly content package (4 blogs, 12 LinkedIn posts, 8 Instagram posts) | USD 2,500 / month |
| Term | 3 months |
| **Total** | **USD 7,500** |

### Timeline

- Start: the first Monday after we receive the signed proposal and the deposit (target ______________).
- Month 1 topic call in week 1; first batch of drafts by the middle of month 1.
- The schedule depends on receiving your brand assets and topic sign-off on time.

### Terms

- **Deposit:** 50% of the total, USD 3,750, due on signing. Work starts when it is received.
- **Balance:** USD 1,250 due at the start of month 2 and USD 2,500 due at the start of month 3, each payable within 15 days of invoice.
- **Changes:** any change to scope or quantities is agreed in writing before work on it starts.
- **Ownership:** you own the final delivered content once it has been paid for in full.
- **Validity:** this proposal is valid for 30 days from the date above.

### Next step

Sign below and pay the deposit, and we will book the month 1 topic call within 3 business days.

### Signatures

For Acme Outdoor: ____________________  Name: ______________  Date: __________

For Northwind Analytics: ______________  Name: ______________  Date: __________

---

Ready for you: a USD 7,500 proposal to Acme Outdoor (contact still blank), with the USD 3,750 deposit due on signing. Nothing has been sent, invoiced or put on a board. You send it and collect the signature yourself. Fill in the blog word count and the contact, then: do you want to send it as it is, or change the terms first? When Acme sends back their own contract, say "review this contract" (`contract-review`).

---

## Judgement (tester)

- Worked end to end with no connectors: text out, nothing sent, invoiced, charged or put on a task board. The internal read (assumptions, risks) stayed above the customer text, and the price was not padded with invented per-channel rates; unknowns (blog length, contact) were left as blanks as the skill requires.
- Issue: `references/voice-profile.md` lines 9-21 list 11 skills that do not exist in this workspace (`outreach-composer`, `speed-to-lead`, `invoice-chase`, `inbox-manager`, ...). Fix: replace the table with "Used by proposal-builder in this workspace".
- Issue: `references/untrusted-content.md` lines 30, 38-40 and 83-88 name skills that do not exist here (`ticket-deflector`, `inbox-manager`, `ap-processor`, `build-connector`, ...). Fix: drop the skill names and keep the rules.
- Issue: `references/proposal_structure.md` line 120 says "store it so later runs match" with no location. Fix: say "save it where the owner names (for example `docs/templates/`), never under `content/`", matching SKILL.md Step 3.
- Minor: with a placeholder brand profile the skill tells you to ask for three emails before writing; for a test that is one extra round trip. Expected behaviour, not a defect.
