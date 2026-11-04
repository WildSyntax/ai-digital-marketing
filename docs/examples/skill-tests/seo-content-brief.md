# seo-content-brief test
Prompt: "Write a content brief for a blog post targeting 'contribution margin e-commerce'."
Date: 2026-11-05
Result: PASS WITH ISSUES

Test notes (not part of the brief):
- Mode: new page. No site URL or sitemap exists (`site_domain: example.com` is a sample), so business context came from `brand/profile.md` and the existing draft `content/drafts/blog/2026-11-04-which-products-are-losing-money.md` (read only). Internal links are therefore partly unverified.
- SERP: one web search on 2026-11-05 plus fetches of five ranking pages. Glossary/definition pages (thoughtmetric.io, finaloop.com, golocad.com) were left out as non-competitors for a guide.
- No keyword-data connector was connected, so search volume and difficulty are marked "not measured". Nothing was asked of the owner; no values were invented.
- Brand name in the title uses the sample value "Northwind Analytics" (profile still holds "Example:" values, as expected).
- Issues found are listed at the end of this file.

---

## Content Brief: contribution margin e-commerce

**Keyword data:** search volume not measured, keyword difficulty not measured (no keyword-data connector connected; paste exports from your keyword tool to replace these).

### Search Intent
Informational, with light commercial research behind it. The searcher wants a definition, the formula and a sense of what a good number is; most ranking pages are long-form guides (1,000 to 3,000 words) with a worked example, a cost table and an FAQ, written by analytics vendors and agencies. Audience for this piece: founders and marketing leads at e-commerce stores with 2 to 20 staff who know revenue and gross margin but have not split costs per order. Detected page type: Blog Post (pillar guide on the "Pricing and margin decisions" content pillar).

### Competitor Analysis
Scores are editorial judgement out of 40 (Depth, Formatting, SEO, UX, each out of 10). Word counts are estimates from page fetches on 2026-11-05.

| # | URL | Key H2 Sections | Est. Words | Score | Main Gap |
|---|-----|-----------------|------------|-------|----------|
| 1 | https://www.sarasanalytics.com/blog/ecommerce-contribution-margin | How to calculate; why gross margin isn't enough; CM vs ROAS; what is good; strategies; challenges; FAQ | ~3,000 | 27/40 | Written for $20M+ Shopify brands; heavy product pitch; benchmarks borrowed from other vendors |
| 2 | https://swankyagency.com/understanding-contribution-margin-ecommerce/ | What it is; why it matters; pivot points; factors; 7 strategies | ~2,200 | 27/40 | No table, no FAQ, no per-product view; examples mostly hypothetical |
| 3 | https://www.kickbite.io/en/blog/contribution-margin | What it measures; full variable cost stack; CM after marketing; getting the number right; FAQ | ~1,400 | 27/40 | Strong cost table but cost ranges are unsourced; per-order only, no per-product ranking |
| 4 | https://www.alexanderjarvis.com/what-is-contribution-margin-in-ecommerce/ | Fundamentals; calculating; variables; bundling; pricing; supply chain; CAC vs CM; marketplace vs DTC; FAQ | ~2,500 | 24/40 | No author or date; most benchmarks (35-65%) unsourced; broad and shallow |
| 5 | https://dema.ai/blog/contribution-margin-1-2-and-3-the-key-components-of-e-commerce-profitability | Net sales; CM1; CM2; CM3; how to improve CM3 | ~950 | 21/40 | Clear CM1/CM2/CM3 framing but no tables, no benchmarks, no FAQ |

Competitor average: ~2,000 words.

### Content Gaps and Opportunities
Ordered by priority (impact x advantage / effort).

- **Topic gap: per-product ranking.** Every ranking page calculates margin per order or for the whole store. None shows how to rank individual products by total contribution, which is where a small store finds its losers. Northwind already has this method in the "which products are losing money" draft; summarise it and link to it.
- **Topic gap: allocating ad spend when campaigns are not split by product.** Competitors say "subtract marketing" and stop. Small stores run mixed campaigns. Give the revenue-share allocation rule and one worked line.
- **Quality gap: benchmarks for small stores.** Published ranges (20% after marketing, 35-65% before) come from vendors and from brands well above the target audience's size. Present them with their source and size caveat, and show how to set your own target from fixed costs instead.
- **Depth gap: CM1, CM2, CM3 in one table.** Only one competitor uses the levels, and without a table. A single table showing which costs drop out at each level answers the definitional query fast.
- **Depth gap: break-even ROAS from contribution margin.** One competitor mentions it in passing. A two-line formula (break-even ROAS = 1 / CM2 ratio) with a worked number links margin to ad decisions, which the audience cares about.
- **Quality gap: authorship and dates.** Two of five pages have no visible author or date. A named author, a "Last updated" line and dated sources are an easy edge.

### Winning Outline

**H1:** Contribution Margin: E-Commerce Formula, Levels and a Worked Example
**URL Slug:** /contribution-margin-e-commerce
**Target Word Count:** ~1,800 words (competitor avg: ~2,000 words; brand default 1,200-2,000)

Keyword note: the primary phrase reads awkwardly in prose. Exact matches work where punctuation sits between the two halves (for example "contribution margin: e-commerce" or "contribution margin, e-commerce teams"), because punctuation and hyphens count as spaces when the phrase is checked. Aim for 5 to 6 natural exact uses; do not force more.

**Intro (no heading), ~120 words. FS target.**
Answer-first paragraph, 40-60 words: "Contribution margin is revenue minus every cost that grows with each order..." Then one line on why revenue and gross margin reports hide unprofitable products. Keyword: primary phrase once in the first 100 words, plus "Last updated" line above it.

**H2: What contribution margin means for an e-commerce store, ~200 words**
Definition box, then a short paragraph on what counts as variable (landed product cost, packaging, shipping, payment and platform fees, returns, ad spend) and what stays out (rent, salaries, software). Keyword: variation "contribution margin for an e-commerce store" in H2; body: primary phrase once.

**H2: The contribution margin formula, ~200 words. FS target.**
Formula in a code-style line: Contribution margin = net revenue - variable costs. Ratio version: contribution margin / net revenue x 100. One per-order example ($80 order). Keyword: secondary "contribution margin formula" in H2; body: "contribution margin ratio".

**H2: CM1, CM2 and CM3: three levels of contribution margin, ~250 words**
Table: level | costs subtracted | what it tells you. CM1 = net sales - landed product cost; CM2 = CM1 - fulfilment, payment fees, returns; CM3 = CM2 - marketing. Note which one to use for product decisions (CM3). Keyword: secondary "CM1 CM2 CM3" in H2; body: primary phrase once.

**H2: Contribution margin vs gross margin, ~150 words. FS target.**
Two-column comparison table; one sentence on why a product can show a healthy gross margin and still lose money per order. Keyword: secondary "contribution margin vs gross margin" in H2.

**H2: A worked example with two products, ~250 words**
Reuse the jacket and beanie numbers from the existing draft (jacket $60 x 200, $56 variable cost, $800 total; beanie $25 x 300, $14 variable cost, $3,300 total), so the series stays consistent. Table plus a paragraph. Add one line on splitting a mixed ad campaign by revenue share. Keyword: secondary "contribution margin per product"; body: no primary needed.

**H2: What is a good contribution margin for e-commerce, ~200 words. FS target.**
Give the vendor benchmark (about 20% after marketing, per Eightx) with its source, date and "brands above $5M revenue" caveat. Then show how to set your own floor: monthly fixed costs / contribution per order = orders needed to break even. Keyword: secondary "good contribution margin" in H2; body: primary phrase once.

**H2: Using contribution margin to set ad budgets, ~180 words**
Break-even ROAS = 1 / CM2 ratio, one worked number (CM2 of 40% gives break-even ROAS of 2.5). One paragraph on moving budget from low-contribution to high-contribution products. Keyword: secondary "break-even ROAS".

**H2: Common mistakes, ~150 words**
Numbered list: using purchase price instead of landed cost; leaving out returns; spreading fixed costs across products; judging on store-wide averages; using CM2 for ad decisions without subtracting ad spend.

**H2: FAQ, ~200 words (4-5 questions, 40-60 words each)**
- Is contribution margin the same as profit?
- Should shipping be included in contribution margin?
- How often should a small store calculate it?
- Can contribution margin be negative?
- Do I need software to track it?
Keyword: primary phrase once in one answer.

**H2: Get this done for you, ~60 words**
Blog CTA from the profile: "Want this done for you? Book a free 20-minute data review at example.com/review."

### Recommended Meta Tags

**Title**
Contribution Margin: E-Commerce Guide | Northwind Analytics
(59 characters)

**Meta Description**
Contribution margin e-commerce guide: the formula, CM1 to CM3, a two-product example and benchmarks for small stores. Check your own store in an hour.
(150 characters; meets both this skill's 130-150 rule and seo-check's 150-160 rule)

### Unique Angle and Information Gain
Ranking pages explain contribution margin per order for mid-size and large brands. This piece is the only one written for a 2-20 person store and carries the idea through to a decision: it ranks products by total contribution in dollars, shows exactly how to split a mixed ad campaign across products, and replaces borrowed vendor benchmarks with a break-even target the reader calculates from their own fixed costs. The same jacket-and-beanie numbers used in Northwind's blog and LinkedIn posts make the series consistent. To add real first-hand evidence, the owner should supply one anonymised result from a Northwind data review (for example, the share of a client's catalogue that had negative CM3 before the review); without it, the piece relies on worked examples and must say so.

### E-E-A-T Requirements
- Named author with a short bio stating hands-on experience running store data reviews (owner to supply; the current draft uses an Organization author only).
- "Last updated" date at the top, matching `dateModified` in the schema.
- Every benchmark linked to its source with the source type (vendor) and date, and the revenue-size caveat stated next to it.
- Worked examples labelled as sample numbers, not client data.
- One anonymised client result if the owner can provide it, clearly marked.
- Finance-adjacent topic: avoid advice phrased as accounting or tax guidance; say "check with your accountant" where fixed-cost treatment is discussed.

### Internal Linking Opportunities
Page role: hub for the "Pricing and margin decisions" pillar, linking out to spoke posts.
- "find which products are losing money" -> /blog/which-products-are-losing-money (the current draft; confirm the final slug at publish)
- "book a free data review" -> /review (CTA destination from the profile)
- "weekly e-commerce KPIs" -> /blog/e-commerce-kpis-to-track-weekly (referenced by the existing draft; not verified to exist, no sitemap available)
- Future spokes to create and link: "break-even ROAS calculator", "how to calculate landed cost" (suggested, not existing)

Sources:
- [Saras Analytics: eCommerce Contribution Margin](https://www.sarasanalytics.com/blog/ecommerce-contribution-margin)
- [Swanky: Understanding Contribution Margin in Ecommerce](https://swankyagency.com/understanding-contribution-margin-ecommerce/)
- [Kickbite: Contribution Margin in Ecommerce](https://www.kickbite.io/en/blog/contribution-margin)
- [Alexander Jarvis: Contribution Margin in Ecommerce](https://www.alexanderjarvis.com/what-is-contribution-margin-in-ecommerce/)
- [Dema: Contribution margin 1, 2 and 3](https://dema.ai/blog/contribution-margin-1-2-and-3-the-key-components-of-e-commerce-profitability)
- [Eightx: Average contribution margin by vertical](https://eightx.co/blog/average-contribution-margin-by-vertical) (cited via the existing draft)

Next step: say "write a blog on contribution margin e-commerce" and blog-post will draft from this brief; seo-check then scores it.

---

## Issues found in the skill

1. **Loaded skill text differs from the file on disk.** The Skill tool returned the upstream text (with "DataForSEO Integration (Optional)" and "Ahrefs Integration (Optional)" sections and "Fetch the target URL or homepage" as a hard step), while `.claude/skills/seo-content-brief/SKILL.md` on disk has the workspace version (lines 24-33 workspace note, lines 249-256 "Keyword Data (Optional)"). The session appears to have cached the skill before the 00:21 edit. Fix: restart the session (or reload skills) after editing skills; consider noting this in `docs/skill-library.md`. I followed the on-disk version.
2. **Meta length conflicts with seo-check.** SKILL.md lines 156-158 require 130-150 characters; seo-check check 10 gives full points only at 150-160. SKILL.md line 32-33 says seo-check wins, but a writer following the brief gets 3 of 5 points for anything under 150. Fix: change line 157 to "150-160 characters (seo-check's range)".
3. **Keyword density conflicts with seo-check.** SKILL.md lines 117-120 and `references/keyword-density.md` say there is no density target; seo-check check 6 scores 0.5-2.0% exact-phrase density for 10 points. For an awkward phrase like this one, ~8 forced uses in 1,800 words are needed for full points. Fix: add a line under "Keyword Placement" saying "seo-check scores exact-phrase density 0.5-2.0%; for awkward phrases accept partial points rather than forcing repetition", or relax seo-check for multi-word keywords.
4. **Alt-text rule contradicts itself.** `references/page-type-templates.md` line 38 lists "one image alt text" as a required placement for blog posts; SKILL.md line 129 and `references/keyword-density.md` line 31 say alt text is not required. Fix: remove ", one image alt text" from page-type-templates.md line 38.
5. **FAQPage advice contradicts blog-post.** `references/page-type-templates.md` line 37 says "Do not add FAQPage"; `blog-post/SKILL.md` lines 73-74 add `FAQPage` when a post has an FAQ (and the existing draft does). Not harmful, since the brief does not output schema, but confusing. Fix: change line 37 to "Article (BlogPosting); blog-post adds FAQPage for the visible FAQ".
6. **No guidance for the no-sitemap case in this workspace.** `site_domain` is `example.com`, so the "fetch the sitemap" path never works; the brief cannot verify internal link targets (e.g. `/blog/e-commerce-kpis-to-track-weekly` is referenced by the existing draft but no such content exists under `content/`). Fix: in SKILL.md line 57-58, add "treat files under `content/published/` as the sitemap, and mark any other link target as unverified".
7. **No cannibalisation check.** The existing draft already targets "contribution margin" as a secondary keyword. The skill has no step to check existing `content/` keywords for overlap. Fix: add to step 2 "grep `keyword:` and `secondary_keywords:` under `content/` and state how the new page differs".

End to end: the skill produced a complete brief in the required structure with real SERP research, honest "not measured" labels, and brand-consistent content. No banned phrases in the output.
