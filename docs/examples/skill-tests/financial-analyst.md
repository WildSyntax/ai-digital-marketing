# financial-analyst test
Prompt: "Here are last quarter's numbers vs budget; analyse the variance."
Date: 2026-11-05
Result: PASS WITH ISSUES

Test setup: the figures are made up for Northwind Analytics, Q3 2026 (Jul-Sep), 3 revenue lines and 7 cost lines with monthly actuals, in
`/private/tmp/claude-501/-Users-himanshu25--claude-spares-spare-97jvgk/c9aef6d1-9353-4a3b-9c65-8ef1b46a10b1/scratchpad/tests/northwind_q3_budget_variance.json`
(flat `line_items` shape, as read from `scripts/budget_variance_analyzer.py` and `assets/sample_financial_data.json` -> `budget_variance`).
The skill was loaded by reading `.claude/skills/financial-analyst/SKILL.md`, because the Skill tool returned `Unknown skill: financial-analyst` in this session.

Questions the skill should put to the owner, answered by the tester for Northwind:
- Currency: USD (the script can only print `$`).
- Materiality threshold: 10% or $2,000. The script's default of $50,000 is larger than any Northwind line, so it would only apply the 10% rule.
- Period: the script handles one period only, so the three months were added up into quarter totals. The monthly figures were used by hand below.

Commands run (from `.claude/skills/financial-analyst/`):
```
python3 scripts/budget_variance_analyzer.py <scratch>/northwind_q3_budget_variance.json                      # exit 0, defaults 10% / $50K
python3 scripts/budget_variance_analyzer.py <scratch>/northwind_q3_budget_variance.json --threshold-pct 10 --threshold-amt 2000   # exit 0
python3 scripts/ratio_calculator.py assets/sample_financial_data.json                                       # exit 0
```
No script errors.

---

**Not financial advice.** This is arithmetic on the figures you gave, with notes on what they mean. It is not accounting, tax or investment advice. Check anything with real money at stake with your accountant.

## Budget variance report: Northwind Analytics, Q3 2026

| Field | Value |
|---|---|
| Period | Q3 2026 (Jul-Sep), quarter totals |
| Materiality threshold | 10% or $2,000 (set for this business; script default is 10% or $50,000) |
| Assumed, not provided by you | Currency is USD. A line exactly on budget is shown as "on budget" here, though the script counts it as Unfavorable |

### Summary

Revenue came in $2.3K (2.2%) under budget and costs came in $1.8K (2.6%) over, so profit missed budget by $4.1K. Retainers did better than planned. Dashboard project revenue fell well short, and contract analyst costs rose. Compared with Q3 2025, revenue grew 20.7% and costs grew 20.8%, so profit grew in dollars but the margin held flat rather than improving.

| Metric | Actual | Budget | Variance | Variance % | Status |
|---|---|---|---|---|---|
| Total revenue | $99,700 | $102,000 | -$2,300 | -2.2% | Unfavorable |
| Total costs | $71,300 | $69,500 | +$1,800 | +2.6% | Unfavorable |
| Profit (revenue minus costs) | $28,400 | $32,500 | -$4,100 | -12.6% | Unfavorable |
| Profit margin | 28.5% | 31.9% | -3.4 pp | - | Unfavorable |

### Material variances (10% or $2,000)

| Line | Actual | Budget | Variance | % | Status | What the monthly figures show |
|---|---|---|---|---|---|---|
| Dashboard projects | $28,000 | $36,000 | -$8,000 | -22.2% | Unfavorable | Jul $12K, Aug $4K, Sep $12K. The shortfall is all in August. |
| Reporting retainers | $64,500 | $60,000 | +$4,500 | +7.5% | Favorable | Rose each month ($21.0K, $21.5K, $22.0K). |
| Contract analysts | $13,800 | $11,000 | +$2,800 | +25.4% | Unfavorable | Rising ($4.2K, $4.4K, $5.2K), with the jump in September. |
| Paid ads | $3,900 | $6,000 | -$2,100 | -35.0% | Favorable | Spend cut after July ($1.5K, $1.2K, $1.2K). |
| Data review workshops | $7,200 | $6,000 | +$1,200 | +20.0% | Favorable | Rising each month ($1.8K, $2.4K, $3.0K). |
| Software and data tools | $5,400 | $4,500 | +$900 | +20.0% | Unfavorable | Flat $1.8K a month against a $1.5K budget. |
| Accounting and legal | $1,500 | $1,200 | +$300 | +25.0% | Unfavorable | Flat $500 a month against $400. |
| Co-working and travel | $2,100 | $2,400 | -$300 | -12.5% | Favorable | Small. |

Not material: Salaries ($42,000, exactly on budget), Content and design freelancers (+$200, +8.3%).

### Category view

| Category | Variance | % |
|---|---|---|
| Recurring revenue | +$4,500 | +7.5% |
| Project revenue | -$6,800 | -16.2% |
| Delivery costs (contract analysts) | +$2,800 | +25.4% |
| Technology | +$900 | +20.0% |
| Sales and marketing | -$1,900 | -22.6% |
| Personnel | $0 | 0.0% |
| G&A | $0 | 0.0% |

### What to look at

These are questions for you. The figures show where the gap is but not why, and this report does not guess the causes.

1. **August dashboard projects ($8K short).** Did a project slip into Q4, or was one lost? If it slipped, Q4 revenue should show it.
2. **Contract analysts (+$2.8K, rising each month).** Is this extra retainer work (retainers were $4.5K over budget), or project overrun? If it is retainer work, the retainer price may not cover the hours.
3. **Software (+$900).** The overspend is a steady $300 a month, which looks like a recurring subscription the budget missed. Worth updating the Q4 budget to match.
4. **Paid ads ($2.1K under).** This is favorable on cost. Check whether workshop and project leads held up after the cut before treating it as a saving.

Net effect: the business is growing about 21% year on year, but project revenue fell short and delivery costs rose, so profit margin missed budget by 3.4 points.

---

## Ratio calculator smoke test (bundled demo data only)

`python3 scripts/ratio_calculator.py assets/sample_financial_data.json` ran with exit 0 and printed all 5 categories (profitability, liquidity, leverage, efficiency, valuation). The data is the fictional "Acme Corp" demo, so the ratios are not Northwind's and are not reported as such. Problem found: valuation ratios are graded on a "higher is better" scale (see issue 4).

## Tester's judgement

The skill worked end to end. The variance script read the made-up file without errors, and the ratio script ran on the sample. SKILL.md has a clear "Not financial advice" line (line 16) and a never-invent-numbers rule (line 20). It discloses the DCF and forecast defaults and requires them to be listed (line 22).

Issues:
1. **Zero variance counted as Unfavorable.** `scripts/budget_variance_analyzer.py` lines 81-85: `classify_favorability` returns "Unfavorable" when the variance is 0. Salaries exactly on budget appear as "Team: Fav 0 / Unfav 1", and the summary's Unfavorable count is 6 when it should be 5. Fix: return "On budget" when `variance_amount == 0`, and count it separately.
2. **Money formatting.** Same script, `fmt_money` lines 294-300: plain actual and budget amounts get a "+" (`Actual +$99.7K vs Budget +$102.0K`), and negatives print as `$-2.3K`. Fix: use one formatter for amounts with no sign and one for variances that prints `-$2.3K` / `+$1.8K`. Currency is hard-coded to `$`. Add a `--currency` flag or a `currency` key in the input.
3. **Variance threshold default is not covered by the defaults rule.** SKILL.md line 22 lists the DCF and forecast defaults only. The variance default of 10% or $50,000 (SKILL.md line 107, script lines 384-395) is not mentioned, and for a business this size it switches off the dollar rule without saying so. Fix: add to line 22: "budget_variance_analyzer.py defaults to 10% or $50,000 materiality; ask the owner for a threshold that suits their size, and state the one used."
4. **Valuation ratios graded the wrong way.** `scripts/ratio_calculator.py` lines 336-344 apply "higher is better" to every ratio not specially handled. On the sample, P/E 81.8, P/B 20.5 and EV/EBITDA 45.7 are labelled "Excellent - significantly above peers". A high multiple means expensive, not excellent, and this verdict sits badly with the "does not recommend buying, selling or holding" line (SKILL.md line 16). The built-in `BENCHMARKS` (line 48) are generic and are not disclosed to the owner. Fix: for valuation ratios, print a neutral label ("above the built-in reference range") or none. Add to the SKILL.md ground rules that the ratio assessments compare against built-in generic ranges, which must be stated as such.
5. **Single period only.** The variance script compares one actual to one budget per line. A 3-month budget-vs-actual has to be added up first, and the month-by-month trend is lost (the August project gap above was found by hand). Fix: say so in SKILL.md "Budget Variance Analyzer" (around line 100), or accept an optional `monthly` array per line.
6. **Skill not registered in this session.** The Skill tool returned `Unknown skill: financial-analyst`, as it did for `process-mapper` and `summarize-meeting`, although `.claude/skills/<name>/SKILL.md` exists. This is probably a stale session skill list rather than a fault in the skill. Check it in a fresh session.

No banned phrases in the output.
