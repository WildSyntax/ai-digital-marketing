---
name: financial-analyst
description: "Analyses financial figures the owner provides: ratio analysis of financial statements, DCF valuation, budget-vs-actual variance and driver-based rolling forecasts. Use when the owner asks what the business is worth, why spend missed budget, how healthy the numbers look, or what next quarter could look like. Works only from figures the owner supplies and never invents numbers. Not financial advice."
license: MIT
metadata:
  source: "alirezarezvani/claude-skills@c85b17e1fb621ba760478baaacc4fcb9be225e74"
  path: "finance/skills/financial-analyst"
  modified: "yes"
---

# Financial Analyst Skill

> Vendored from [alirezarezvani/claude-skills](https://github.com/alirezarezvani/claude-skills/tree/c85b17e1fb621ba760478baaacc4fcb9be225e74/finance/skills/financial-analyst) under MIT. needs: python3 (standard library only, no packages).
> Changes for this workspace: added a "not financial advice" line and a never-invent-numbers rule; scripts must run on owner-supplied figures, with defaulted assumptions reported; removed the Buy/Hold/Sell recommendation from the DCF template; dropped the illustrative `assets/expected_output.json` test fixture; script paths made relative to this skill folder; budget variance analyzer: zero variance reads "On budget", amounts print unsigned and variances as -$2.3K/+$1.8K, new `--currency` option, materiality thresholds printed in the report header; ratio calculator: valuation multiples get a neutral above/within/below-reference-range reading instead of a good/bad grade, and the report states its ranges are generic. Read brand/profile.md first. Return text; workspace skills own files under content/.

**Not financial advice.** This skill does arithmetic on figures the owner provides and explains what the results mean. It is not investment, tax, legal or accounting advice and does not recommend buying, selling or holding any security. For decisions with real money at stake, the owner should check with a qualified accountant or adviser.

## Ground rules for this workspace

- **Never invent numbers.** Use only figures the owner gives you (pasted, or in a file they point to). If a figure a calculation needs is missing, ask for it or leave that ratio out and say so. Do not fill gaps with benchmark, "typical range" or sample values.
- `assets/sample_financial_data.json` is a demo with fictional figures (for "Acme Corp"). Use it only to show the input shape or to test that a script runs. Never present its results as the owner's numbers.
- **Defaults in the scripts.** `dcf_valuation.py` and `forecast_builder.py` silently fall back to built-in defaults when an assumption is missing (for example risk-free rate 4%, equity risk premium 6%, beta 1.0, terminal growth 2.5%, exit multiple 12x, gross margin 40%, opex 25% of revenue, collection rate 85%). Before running, check which assumption keys the owner has supplied. Ask for the missing ones, or list every default used in the output as "assumed, not provided by you".
- **Materiality threshold default.** `budget_variance_analyzer.py` flags a variance as material at 10% of budget or 50,000 (currency units), whichever is hit first; the report header prints the thresholds in use. 50,000 is large for a small business, so ask the owner for a threshold that fits their size and pass it with `--threshold-pct` / `--threshold-amt`.
- **Reference ranges in the ratio calculator.** `ratio_calculator.py` grades ratios against generic built-in reference ranges (the `BENCHMARKS` table in the script), not the owner's industry data; say so when quoting an assessment. Valuation multiples (P/E, P/B, P/S, EV/EBITDA, PEG) are only described as below/within/above that range, never as good or bad.
- Write the owner's figures to a JSON input file outside `content/` (for example a scratch or temp folder), run the script, and return the result as text. Scripts only print to stdout; they never write files.
- Present valuations and forecasts as ranges with their assumptions stated, never as a single certain figure.

## Overview

Production-ready financial analysis toolkit providing ratio analysis, DCF valuation, budget variance analysis, and rolling forecast construction. Designed for financial modeling, forecasting & budgeting, management reporting, business performance analysis, and investment analysis.

## 5-Phase Workflow

### Phase 1: Scoping
- Define analysis objectives and stakeholder requirements
- Identify data sources and time periods
- Establish materiality thresholds and accuracy targets
- Select appropriate analytical frameworks

### Phase 2: Data Analysis & Modeling
- Collect and validate financial data (income statement, balance sheet, cash flow)
- **Validate input data completeness** before running ratio calculations (check for missing fields, nulls, or implausible values)
- Calculate financial ratios across 5 categories (profitability, liquidity, leverage, efficiency, valuation)
- Build DCF models with WACC and terminal value calculations; **cross-check DCF outputs against sanity bounds** (e.g., implied multiples vs. comparables)
- Construct budget variance analyses with favorable/unfavorable classification
- Develop driver-based forecasts with scenario modeling

### Phase 3: Insight Generation
- Interpret ratio trends and benchmark against industry standards
- Identify material variances and root causes
- Assess valuation ranges through sensitivity analysis
- Evaluate forecast scenarios (base/bull/bear) for decision support

### Phase 4: Reporting
- Generate executive summaries with key findings
- Produce detailed variance reports by department and category
- Deliver DCF valuation reports with sensitivity tables
- Present rolling forecasts with trend analysis

### Phase 5: Follow-up
- Track forecast accuracy (target: +/-5% revenue, +/-3% expenses)
- Monitor report delivery timeliness (target: 100% on time)
- Update models with actuals as they become available
- Refine assumptions based on variance analysis

## Tools

### 1. Ratio Calculator (`scripts/ratio_calculator.py`)

Calculate and interpret financial ratios from financial statement data.

**Ratio Categories:**
- **Profitability:** ROE, ROA, Gross Margin, Operating Margin, Net Margin
- **Liquidity:** Current Ratio, Quick Ratio, Cash Ratio
- **Leverage:** Debt-to-Equity, Interest Coverage, DSCR
- **Efficiency:** Asset Turnover, Inventory Turnover, Receivables Turnover, DSO
- **Valuation:** P/E, P/B, P/S, EV/EBITDA, PEG Ratio

```bash
python3 scripts/ratio_calculator.py assets/sample_financial_data.json
python3 scripts/ratio_calculator.py assets/sample_financial_data.json --format json
python3 scripts/ratio_calculator.py assets/sample_financial_data.json --category profitability
```

### 2. DCF Valuation (`scripts/dcf_valuation.py`)

Discounted Cash Flow enterprise and equity valuation with sensitivity analysis.

**Features:**
- WACC calculation via CAPM
- Revenue and free cash flow projections (5-year default)
- Terminal value via perpetuity growth and exit multiple methods
- Enterprise value and equity value derivation
- Two-way sensitivity analysis (discount rate vs growth rate)

```bash
python3 scripts/dcf_valuation.py assets/sample_financial_data.json
python3 scripts/dcf_valuation.py assets/sample_financial_data.json --format json
python3 scripts/dcf_valuation.py assets/sample_financial_data.json --projection-years 7
```

### 3. Budget Variance Analyzer (`scripts/budget_variance_analyzer.py`)

Analyze actual vs budget vs prior year performance with materiality filtering.

**Features:**
- Dollar and percentage variance calculation
- Materiality threshold filtering (default: 10% or $50K)
- Favorable/unfavorable classification with revenue/expense logic
- Department and category breakdown
- Executive summary generation

```bash
python3 scripts/budget_variance_analyzer.py assets/sample_financial_data.json
python3 scripts/budget_variance_analyzer.py assets/sample_financial_data.json --format json
python3 scripts/budget_variance_analyzer.py assets/sample_financial_data.json --threshold-pct 5 --threshold-amt 25000
python3 scripts/budget_variance_analyzer.py assets/sample_financial_data.json --currency "£"
```

The analyzer handles one period per run: it reads only each line's `actual`, `budget` and `prior_year`. For several months, either run it once per month or sum the months into one period first, and say in the output which was done.

### 4. Forecast Builder (`scripts/forecast_builder.py`)

Driver-based revenue forecasting with rolling cash flow projection and scenario modeling.

**Features:**
- Driver-based revenue forecast model
- 13-week rolling cash flow projection
- Scenario modeling (base/bull/bear cases)
- Trend analysis using simple linear regression (standard library)

```bash
python3 scripts/forecast_builder.py assets/sample_financial_data.json
python3 scripts/forecast_builder.py assets/sample_financial_data.json --format json
python3 scripts/forecast_builder.py assets/sample_financial_data.json --scenarios base,bull,bear
```

## Knowledge Bases

| Reference | Purpose |
|-----------|---------|
| `references/financial-ratios-guide.md` | Ratio formulas, interpretation, industry benchmarks |
| `references/valuation-methodology.md` | DCF methodology, WACC, terminal value, comps |
| `references/forecasting-best-practices.md` | Driver-based forecasting, rolling forecasts, accuracy |
| `references/industry-adaptations.md` | Sector-specific metrics and considerations (SaaS, Retail, Manufacturing, Financial Services, Healthcare) |

## Templates

| Template | Purpose |
|----------|---------|
| `assets/variance_report_template.md` | Budget variance report template |
| `assets/dcf_analysis_template.md` | DCF valuation analysis template |
| `assets/forecast_report_template.md` | Revenue forecast report template |

## Key Metrics & Targets

| Metric | Target |
|--------|--------|
| Forecast accuracy (revenue) | +/-5% |
| Forecast accuracy (expenses) | +/-3% |
| Report delivery | 100% on time |
| Model documentation | Complete for all assumptions |
| Variance explanation | 100% of material variances |

## Input Data Format

All scripts accept JSON input files in either of two shapes:

1. **Flat** — the tool's expected keys at the top level (e.g., `income_statement` / `balance_sheet` for the ratio calculator, `historical` / `assumptions` for DCF, `line_items` for variance, `historical_periods` / `drivers` / `assumptions` / `cash_flow_inputs` for forecasting).
2. **Nested (bundled)** — inputs for all four tools in one file, nested under per-tool keys: `ratio_analysis`, `dcf_valuation`, `budget_variance`, `forecast`. See `assets/sample_financial_data.json` for the complete bundled schema; every quick-start command above runs directly against it.

Each script auto-detects the shape (flat keys win if present) and exits non-zero with a clear error if neither shape yields usable data.

Run the commands from this skill's folder (`.claude/skills/financial-analyst/`). Swap `assets/sample_financial_data.json` for the path to the owner's own input file; the sample is only for checking the input shape.

## Dependencies

**None** beyond `python3` - all scripts use the Python standard library only (`math`, `statistics`, `json`, `argparse`, `datetime`). No numpy, pandas, or scipy required.
