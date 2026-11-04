# x-thread-builder test
Prompt: "Turn my blog draft content/drafts/blog/2026-11-04-which-products-are-losing-money.md into an X thread, goal: bookmarks."
Date: 2026-11-05
Result: PASS WITH ISSUES

## How the test ran

- `Skill` tool returned `Unknown skill: x-thread-builder` (the folder was added after this session started, so it is not registered). The tester followed `.claude/skills/x-thread-builder/SKILL.md` by reading it directly.
- Inputs answered by the tester: audience = founders and marketing leads at 2-20 person e-commerce stores (brand/profile.md); goal = bookmarks (owner); standard account, no `(1/N)` numbering; no link in the thread (the blog is still a draft, so there is no public URL yet).
- Formula picked: **X7 Listicle-Thread Promise**. X10 How-I Teardown was rejected because Northwind has no real first-person result to cite (the blog's jacket/beanie store is a sample), and the skill forbids inventing one.
- Every number is taken from the blog draft (sample store table, Practical Ecommerce USPS example, one-hour first pass, under 100 products).

## Approval card

Formula: X7 Listicle-Thread Promise | Goal: bookmarks | Tweets: 9 | Em dashes: 0 | Hashtags: 0 | Emoji: 0

| # | Chars | Role |
|---|---|---|
| 1 | 248 | hook: promise (7 steps, one hour) + open loop (step 5) |
| 2 | 257 | strongest payoff: the worked example |
| 3 | 273 | definition: what goes in and out |
| 4 | 248 | steps 1-2 |
| 5 | 265 | step 3 + USPS data point |
| 6 | 276 | steps 4-5, closes the step-5 loop |
| 7 | 265 | steps 6-7 |
| 8 | 260 | what to do with the bottom products |
| 9 | 124 | closer: quotable line + one ask (bookmark) |

## Thread

One product brought in 60% more revenue than another and earned less than a quarter of its contribution.

7 steps to find which of your products are losing money, in one spreadsheet, in about an hour. Step 5 is where the revenue leader gets caught.

---

The sample store sells two things.

Jacket: $60, 200 sold, $12,000 revenue. $4 left per unit after variable costs, $800 in total.
Beanie: $25, 300 sold, $7,500 revenue. $11 left per unit, $3,300 in total.

A revenue report would tell you to push the jacket.

---

What you are measuring: contribution margin is the price minus every cost that grows with each order.

In: landed product cost, packaging, shipping, payment and platform fees, returns, ad spend.
Out: rent, salaries, software. They stay the same when you sell one more unit.

---

1. Export last month's orders, one row per product per order: units, price, discounts, refunds.

2. Add landed cost per unit from supplier invoices. Landed means freight and duties included. Leave them out and every product looks better than it is.

---

3. Add shipping and packaging per order. If an order holds several products, split shipping by each product's share of the order value.

Small changes add up. Practical Ecommerce showed an 8% USPS rate rise taking contribution on a $100 order from $25.00 to $24.44.

---

4. Add payment and platform fees at the rates on your statement, usually a percentage plus a fixed fee.

5. Add ad spend per product. If campaigns aren't split by product, divide spend by each product's revenue share.

This is where the jacket got caught: $16 of ads per sale.

---

6. Subtract all costs from net revenue to get contribution per product, then divide by units sold.

7. Sort by total contribution in dollars, largest first.

The bottom of that list is your work for the month. Under 100 products, the first pass takes about an hour.

---

For each product at the bottom you have four options: raise the price, cut its costs, cut its ad spend, or stop selling it.

Start with the one losing the most dollars in total. Before you drop anything, check whether its orders usually include other products.

---

Revenue shows what sells. Contribution shows what pays for the business.

Bookmark this for the next time you plan ad spend.

Suggested reply to tweet 9 once the blog is live: the post URL (links stay out of tweet 1).

## Checks

**brand/profile.md banned phrases** ("game-changer", "unlock", "in today's fast-paced world", "delve", "leverage"): none found (grep). Tone: no hype, no exclamation marks, no emojis. Audience fit: small e-commerce teams, spreadsheet only.

**references/thread-structure.md per-tweet scrub**
- [x] Every tweet under 280 chars (max 276).
- [x] At most one em dash per tweet (0 used); no en/double dashes.
- [x] No AI-vocab cluster; no reveal bridge, no "It's not X, it's Y", no sincerity opener.
- [x] Each tweet stands alone (tweet 2 names "the sample store"; step tweets carry their own numbers).
- [x] Concrete detail in every body tweet.

**references/algorithm-heuristics.md pre-publish checklist**
- [x] Tweet 1 stops the scroll alone, with a number (60%, 7 steps, one hour).
- [x] Odd-precision number with a referent ($25.00 to $24.44, $16 of ads per sale).
- [x] No external link in tweet 1; 0 hashtags; 0 emoji.
- [x] Tweet 1 opens a loop (step 5) that tweet 6 closes.
- [x] One ask in the close (bookmark), one primary goal.

**SKILL.md hard rules**: tweet 1 has a promise and open loop; front-loaded value (worked example at position 2); 9 tweets, within 5-9; no padding; no punch tweets inserted.

Note: the brand profile has no X call to action, so the closer uses the skill's own bookmark ask.

## Issues found (see final report for fixes)

1. SKILL.md step 9 says the workspace `publish` skill schedules approved content via Metricool. The workspace has no X channel (CLAUDE.md channels: blog, linkedin, instagram, youtube; publish handles only those), and docs/skill-library.md says X threads are "posted by you".
2. `references/hook-formulas.md` X9 skeleton ends "Here is what actually happened." and X3 uses "Here is the part nobody tweets". Both are reveal bridges that thread-structure.md's scrub forbids.
3. `references/hook-formulas.md` X7 skeleton's "Most people get {number} of them wrong" asks for a claim nobody can back up, which clashes with SKILL.md's "Never invent the specifics". The test used a sourced loop ("step 5") instead.
4. `references/voice-rules.md` density rule treats one "leverage"/"unlock"/"delve" per tweet as fine; brand/profile.md bans them outright.
