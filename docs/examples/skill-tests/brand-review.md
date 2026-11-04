# brand-review test
Prompt: "Review content/drafts/linkedin/2026-11-04-best-seller-losing-money.md against our brand."
Date: 2026-11-05
Result: PASS WITH ISSUES

Test notes (not part of the review):
- `Skill` tool call `brand-review` failed with "Unknown skill: brand-review": the skill is not in this session's skill list (the folder and SKILL.md exist on disk, edited 00:20 on 2026-11-05). I followed `.claude/skills/brand-review/SKILL.md` read from disk.
- Brand guide: `brand/profile.md` (the skill's workspace default). It holds sample "Example:" values for Northwind Analytics, as expected. No other style guide exists, so no question was asked.
- The skill's closing question ("Would you like me to revise...") was answered on the owner's behalf with "No revision now; keep the review only", so the draft was not edited.
- Source file read only; nothing under `content/` was changed.

---

### Summary
- **Overall assessment:** Strong alignment. The post is clear, confident and warm, uses the profile's LinkedIn CTA word for word, sits squarely on the "Pricing and margin decisions" pillar, and contains no banned words, no exclamation marks and no emojis.
- **Strengths:** It opens on a specific, relatable problem and proves it with one small worked example the reader can copy. The numbers match the source blog draft exactly (jacket $800, beanie $3,300).
- **Most important improvements:** Make the cost wording consistent (per unit vs per order), qualify the "in an hour" promise the way the blog does, and make sure the spreadsheet promised in the first comment exists before this goes live.

### Detailed Findings

| Issue | Location | Severity | Suggestion |
|-------|----------|----------|------------|
| Promise of an asset that does not exist yet. The first comment offers "the spreadsheet layout I use"; there is no template in the workspace, and "ask in the comments" reads as engagement bait, which cuts against the calm, no-hype tone. | `## First comment`, line 33 | Medium | Only keep it once a template exists. Otherwise link the blog post (after it is published) or drop the offer. See revision 3. |
| Unit and order mixed up. "$56 of product cost, shipping, payment fees and ads per order" and "$14 per order all in" are per-unit figures in the blog's table (variable cost per unit). A reader checking the maths may trip on this. | Lines 18, 20 | Medium | Say "per jacket" / "per beanie" or "per unit". See revisions 1 and 2. |
| Time claim stated without its condition. "You can check your own store in an hour" — the blog limits this to stores with under 100 products. | Line 24 | Medium | Add the condition: "If you sell fewer than 100 products, you can check your store in about an hour." |
| Cost list shorter than the method. The how-to lists product cost, shipping, payment fees and ad spend, but omits packaging, platform fees and returns, which the blog counts. A reader following the post gets a flattering number. | Line 24 | Low | "Subtract every cost that comes with an order: product, packaging, shipping, fees, returns and ads." |
| Sample numbers not labelled as samples. "Take two products" implies a hypothetical, but a reader could take the figures as client data. | Line 18 | Low | "Take two products from a sample store." |
| Comma style inconsistent. Lines 18 and 24 use no serial comma ("payment fees and ads"); line 26 uses one ("cut ad spend, or stop selling"). The profile sets no rule; pick one. | Lines 18, 24, 26 | Low | Drop the serial comma on line 26 to match the rest and the blog draft. |
| Generalisation without support. "Most small stores rank products by revenue." | Line 16 | Low | Soften to "Many small stores..." or keep, as it is framed as the problem statement, not a statistic. |
| Platform hashtag. `#shopify` names a third-party brand that the post never mentions, and the profile's audience is not Shopify-only. | Line 30 | Low | Replace with `#contributionmargin` or `#ecommercetips`. |
| Missing pillar hook. The post could also reinforce pillar 1 ("Reading store data without a data team"), which the blog states and the post implies. | Line 24 | Low | Add "No data team needed: a spreadsheet and three exports." |

Not an issue: voice, banned words (none of the five entries in the profile's banned list appear), exclamation marks (none), emojis (none), jargon (only "contribution margin", defined on first use), CTA (matches the profile's LinkedIn default exactly).

### Revised Sections

**1. Line 18**
Before: "Take two products. A $60 jacket sells 200 a month, so $12,000 in revenue. After $56 of product cost, shipping, payment fees and ads per order, it leaves $4 a unit. That is $800 a month."
After: "Take two products from a sample store. A $60 jacket sells 200 a month, so $12,000 in revenue. Each jacket costs $56 once you add product cost, shipping, payment fees and ads. It leaves $4 a unit, or $800 a month."

**2. Line 20**
Before: "A $25 beanie sells 300 a month, so $7,500 in revenue. It costs $14 per order all in and needs very little ad spend."
After: "A $25 beanie sells 300 a month, so $7,500 in revenue. Each one costs $14 all in, because it needs very little ad spend."

**3. First comment, line 33**
Before: "Want the spreadsheet layout I use for this? Ask in the comments and I will share it."
After (once the blog is published): "The full step-by-step method, with the cost list and a worked table, is on our blog: <link to published blog post>."
After (if a template exists): "The spreadsheet layout I use is here: <template link>."

**4. Line 24**
Before: "You can check your own store in an hour. Export last month's orders by product. Subtract product cost, shipping, payment fees and ad spend per order. Then sort by total contribution in dollars."
After: "If you sell fewer than 100 products, you can check your store in about an hour. Export last month's orders by product. Subtract every cost that comes with an order: product, packaging, shipping, fees, returns and ads. Then sort by total contribution in dollars."

### Legal/Compliance Flags
- **Financial example:** the figures are illustrative. Label them as a sample store (revision 1) so they are not read as a client result or a promised outcome.
- **Third-party mark:** `#shopify` uses a trademark as a hashtag; low risk, but unnecessary (see findings).
- No superlatives, competitor comparisons, testimonials, guarantees or copied text found.

### After review
"Would you like me to revise the full content with these suggestions applied, fix only the high-severity issues, review more content, or help document your brand voice?" (Answered for the test: no revision now.)

---

## Issues found in the skill

1. **Skill not loadable in this session.** `Skill(brand-review)` returned "Unknown skill: brand-review" although `.claude/skills/brand-review/SKILL.md` exists. Likely the session's skill list was built before the skill was added. Fix: restart the session after adding vendored skills; the README/skill-library could say so.
2. **Profile has no style rules for the "Style Guide Compliance" step.** SKILL.md lines 63-67 (Style Guide Compliance) and the "Grammar and Mechanics" table expect rules such as serial comma, heading case, number format; `brand/profile.md` has none, so these checks fall back to internal consistency. Fix: add a short "Style rules" section to the profile template (serial comma, sentence-case headings, numerals, currency) or have the skill say "profile sets no style rules; checked for consistency only".
3. **Generic tone tables can conflict with the profile.** The "Tone by Channel" table (Sales collateral example "reduce reporting time by 40%") and "Tone by Situation" ("Product launch: Excited") pull toward hype, which the profile's Avoid list bans. Fix: add one line under "Tone Adaptation Across Channels": "In this workspace, brand/profile.md's Avoid list overrides these examples."
4. **Unresolved placeholder reference.** SKILL.md line 29 mentions "~~knowledge base reference"; fine via `references/CONNECTORS.md`, but no knowledge-base connector is in `.mcp.json`. No action needed beyond the existing "ask the owner to paste" fallback.
5. **Workspace pipeline check missing (not brand, but useful).** The reviewed draft's front matter lacks `published_at` and `publish_attempted` that CLAUDE.md's content file format lists (lines 9-11 of the draft stop at `published_url` / `source`). brand-review does not look at front matter, so this goes unnoticed; it is a linkedin-post template issue rather than a brand-review one. Fix in `linkedin-post/SKILL.md` front-matter template.

End to end: following the on-disk SKILL.md produced a complete review in the required format, using `brand/profile.md` as instructed, with specific before/after fixes and no false banned-word hits.
