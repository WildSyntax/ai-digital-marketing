# ig-carousel-planner test
Prompt: "Plan an Instagram carousel from that same blog draft." (content/drafts/blog/2026-11-04-which-products-are-losing-money.md)
Date: 2026-11-05
Result: PASS WITH ISSUES

## How the test ran

- `Skill` tool returned `Unknown skill: ig-carousel-planner` (added after this session started, so not registered). The tester followed `.claude/skills/ig-carousel-planner/SKILL.md` by reading it directly.
- Inputs answered by the tester: goal = **saves** (the owner gave none; the brand's Instagram CTA is "Save this for your next planning session"); audience from brand/profile.md.
- Step 2 asks the owner to choose between 2-3 formulas. Offered: IG5 Listicle, IG6 Before/After, IG8 Steal-This Framework. Tester chose **IG5 Listicle Carousel**: the blog's cost table is a ready numbered list. IG6 needs a real before/after result (only a sample store exists). IG8 is first-person ("the framework I use") with no named framework in the source.
- Every figure comes from the blog draft. The jacket/beanie store is labelled "sample" on the slide, as in the blog.

## Approval card

Formula: IG5 Listicle Carousel | Primary goal: saves | Slides: 9 (hook + 7 items + payoff) | Frame: 4:5 portrait

| Slide | On-image text | Words |
|---|---|---|
| 1 (hook) | **7 costs your revenue report hides.** / #1 is how a best seller loses money. | 13 |
| 2 | **1. Ad spend per product** / Sample store: a $60 jacket needed $16 of ads per sale. It kept $4. | 19 |
| 3 | **2. Shipping to the customer** / Several products in one order? Split shipping by each one's share of the order value. | 19 |
| 4 | **3. Landed product cost** / Freight and duties included. Take it from supplier invoices. | 13 |
| 5 | **4. Returns and refunds** / Pull them from your store's refunds report. | 11 |
| 6 | **5. Payment processing fees** / Usually a percentage plus a fixed fee. Use the rates on your statement. | 15 |
| 7 | **6. Marketplace and platform fees** / From your marketplace statements. | 8 |
| 8 | **7. Packaging** / Box, filler, tape. It is on the supplier invoice. | 10 |
| 9 (payoff) | **Price minus all 7 = contribution per unit.** / Sort products by total contribution. Start with the one at the bottom. / Save this for your next planning session. | 25 |

Note on slide 1: it runs 13 words against the 6-12 guide in `references/slide-architecture.md`; set line 2 smaller as the loop line. Note on slide 8: "Box, filler, tape" is a generic illustration of packaging, not a claim from the blog; cut it if the owner prefers source-only wording.

### Caption (661 chars; first line 102 chars, inside the 125-char fold)

```
A product can bring in 60% more revenue than another and earn less than a quarter of its contribution.

Revenue reports count the money that comes in. They skip what each order costs to fulfil, and these 7 costs are the gap.

Subtract them from the price and you get contribution margin: what each sale adds toward rent, salaries and profit. In a sample store, a $60 jacket kept $4 per sale once $16 of ads per sale came out. A $25 beanie kept $11.

Sort your products by total contribution and start with the one at the bottom.

Save this for your next planning session.
.
#contributionmargin #ecommerceprofit #shopifyseller #ecommercetips #smallbusinessowner
```

Hashtag set (sized by judgment; post counts cannot be checked from here, confirm in the app's search): niche `#contributionmargin`, `#ecommerceprofit`, `#shopifyseller`; mid `#ecommercetips`; broad `#smallbusinessowner`.

Media reminder: the owner supplies 9 images (all images, no video), 4:5, in the slide order above, in brand colours #1F3A5F / #E8EEF4 with #F2A541 for the item numbers, Poppins headings.

## Checks

**brand/profile.md banned phrases**: none in slides or caption (grep for game-changer, unlock, fast-paced, delve, leverage). No exclamation marks, 0 emoji, Instagram CTA used verbatim.

**SKILL.md hard rules / anti-patterns**
- [x] Slide 1 is a promise with an open loop (#1), not a bare title.
- [x] Strongest point (ad spend, the jacket example) on slide 2.
- [x] One point per slide; longest value slide is 19 words.
- [x] 2-10 slides (9), not padded: 7 real cost lines from the blog table.
- [x] Payoff slide is a self-contained recap with one ask.
- [x] Em dashes: 0. No "The result?" reveals, no staccato stacks.

**references/algorithm-heuristics.md pre-publish checklist**
- [x] First 125 chars of the caption stop the scroll alone.
- [x] Odd-precision number with a referent ($16 of ads per sale, $4 vs $11).
- [x] 5 sized hashtags at the end.
- [x] 0-3 emoji (0).
- [x] One primary goal (saves); close is a specific save ask.
- [ ] Media within limits: depends on the owner's design.

## Issues found (see final report for fixes)

1. Hand-off is broken: SKILL.md says the plan feeds `instagram-post` and `publish` "schedules approved content", but both handle a single `image_url` only; there is no carousel field or multi-image publish path.
2. `references/hook-formulas.md` IG1 skeleton ("Here is the exact thing I changed.") is a reveal bridge the voice rules forbid elsewhere.
3. `references/voice-rules.md` density rule allows one "unlock"/"delve"/"leverage" per paragraph; brand/profile.md bans them outright.
