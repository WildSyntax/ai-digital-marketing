# yt-title-optimizer test
Prompt: "Give me YouTube title options for a video version of that blog post." (content/drafts/blog/2026-11-04-which-products-are-losing-money.md)
Date: 2026-11-05
Result: PASS WITH ISSUES

## How the test ran

- `Skill` tool returned `Unknown skill: yt-title-optimizer` (added after this session started, so not registered). The tester followed `.claude/skills/yt-title-optimizer/SKILL.md` by reading it directly.
- Inputs answered by the tester: long-form video (not a Short); payoff = the one-hour spreadsheet method plus the jacket/beanie worked example; viewer = small e-commerce founders and marketing leads; search phrase = "which products are losing money" (the blog's keyword).
- Job: mostly **search-first** (it is a how-to), with browse variants for Test & Compare.
- Formulas shortlisted: search-first how-to, Y1 Curiosity-Gap, Y2 Number, Y4 Mistake. Y3 How-I was skipped because Northwind has no real first-person result to quote (the store in the blog is a sample). Y4 is included but flagged: the skill's own corpus note says loss-aversion titles were absent among business/marketing over-performers.

## Approval card

| # | Title | Chars | Formula | Goal | Thumbnail carries (no repeated words) |
|---|---|---|---|---|---|
| 1 | Which Products Are Losing Money? Find Out in One Hour | 53 | search-first how-to | ctr (search) | spreadsheet with one row highlighted red at the bottom, text "$4 vs $11" |
| 2 | Why a $60 Jacket Earns Less Than a $25 Beanie | 45 | Y1 Curiosity-Gap | ctr (browse) | jacket and beanie side by side, a down arrow on the jacket, text "Revenue lies" |
| 3 | Your Best Seller Might Be Losing You Money | 42 | Y1 Curiosity-Gap | ctr (browse) | a "No.1" product tag with a red minus figure, no text beyond "-$" |
| 4 | 7 Costs Your Revenue Report Hides From You | 42 | Y2 Number | ctr | receipt-style list with 7 lines, the last one (ad spend) circled |
| 5 | Stop Ranking Products by Revenue: Find the Money Losers | 55 | Y4 Mistake | ctr | sorted spreadsheet with the revenue column crossed out |

**Lead the Test & Compare with #2** (concrete numbers, an honest gap the first 30 seconds can close by showing the sample table). Run #1 alongside it as the search-first control.

Opening-hook pairing (from the skill's pairing table): #2 and #3 with Y7 Restate-and-Raise ("A $60 jacket brought in 60% more revenue than a $25 beanie and kept $4 a sale against $11. By the end of this you'll have the spreadsheet that shows this for your own store.").

Honesty check: every claim is in the blog. #2 and the hook refer to the blog's sample store, so the video must say "sample store" on screen. #3 says "might", matching the blog's "can lose money on every sale".

## Checks

**brand/profile.md banned phrases**: none in any title (grep). No hype words, no exclamation marks, no emoji, no ALL CAPS.

**references/title-checklist.md**
- [x] All under 100 chars; all inside 40-60.
- [x] Click-deciding words before the colon (#5) / first.
- [x] Promise, not a label; curiosity plus a concrete noun in each.
- [x] Specific number where the claim allows (#1 one hour, #2 $60/$25, #4 7).
- [ ] "How I" over "How to": not applied, no real first-person result (see above).
- [x] The first 30 seconds can keep each promise.
- [x] Thumbnail words never repeat title words; split noted per variant.
- [x] 0 em dashes, 0 emoji, no AI vocabulary, no reveal bridge, keyword once (#1 only).
- [x] 5 variants across 4 shapes, each tagged, one flagged to lead.

## Issues found (see final report for fixes)

1. `references/hook-formulas.md` Y1 skeleton is "{Surprising result or claim}. Here is what nobody tells you." That is the exact reveal bridge SKILL.md step 5 and title-checklist.md tell you to strip. Y5 ("Here is what changed.") has the same problem.
2. SKILL.md says "Y1-Y6" (lines 29, 41, and Resources line 100) while its own table includes Y11; hook-formulas.md is titled "10 YouTube Hook Formulas" but holds 11.
3. SKILL.md has no "never invent the specifics" paragraph (x-thread-builder and ig-carousel-planner do), yet the Y3 reference pushes odd-precision money figures like "$24,937/mo".
4. `references/voice-rules.md` density rule conflicts with brand/profile.md banned words, as in the other two skills.
