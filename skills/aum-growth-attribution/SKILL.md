---
name: aum-growth-attribution
description: Attribute AUM growth to its component drivers — market performance, net new assets, client acquisition, attrition, and fee impact. Use when analyzing practice growth, preparing management reporting, evaluating advisor productivity, forecasting AUM trajectory, benchmarking organic growth rates, or presenting business development results to leadership.

metadata:
  display_name: "Aum Growth Attribution"
  short_description: "Break down AUM growth by market, flows, and attrition"
  default_prompt: "Analyze my aum growth attribution and recommend clear next actions"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# AUM Growth Attribution

## Overview

Decompose Assets Under Management (AUM) growth into its fundamental drivers to provide transparency into practice health and growth quality. This skill separates market-driven growth (beta) from organic growth (net new assets), further breaking organic growth into client acquisition, existing client contributions, distributions/withdrawals, and client attrition. Attribution enables leadership to distinguish sustainable growth from market-dependent growth and evaluate advisor and team productivity.

## When to Use

- Monthly/quarterly management reporting on practice growth
- Advisor performance evaluation and compensation planning
- Business development strategy assessment and planning
- Forecasting AUM and revenue under various market scenarios
- Benchmarking organic growth rates against industry standards
- Analyzing the sustainability and quality of growth
- Board/stakeholder reporting on wealth management business unit performance

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| AUM snapshots | Beginning and ending AUM for the period | Account-level data |
| Cash flows | All contributions, withdrawals, distributions, fees | Transaction data |
| New accounts | Accounts opened during the period with funding amounts | Account records |
| Closed accounts | Accounts closed/transferred with terminal values | Account records |
| Market returns | Benchmark returns for asset classes held | Market data |
| Fee schedule | Advisory fees charged during the period | Billing data |
| Advisor assignment | Account-to-advisor mapping | CRM data |

## Methodology

### Step 1 — AUM Bridge Construction

Build the period AUM bridge from beginning to ending balance:

```
Beginning AUM
+ Market appreciation/depreciation
+ New client assets (new relationships)
+ Existing client contributions (additional deposits)
- Client withdrawals and distributions
- Client attrition (lost relationships)
- Advisory fees deducted
+ Other adjustments (account transfers, reclassifications)
= Ending AUM
```

Each component must be precisely calculated so the bridge reconciles exactly to the actual ending AUM (no unexplained residual).

### Step 2 — Market Return Attribution

Isolate the market-driven component of AUM change:

- **Method**: Calculate the time-weighted return (TWR) of the aggregate portfolio, then apply to beginning AUM
- **Market appreciation** = Beginning AUM × Portfolio TWR for the period
- **Asset class decomposition**: Break market return into contributions from each asset class:

| Asset Class | Weight (Avg) | Asset Class Return | Contribution to Return |
|-------------|-------------|-------------------|----------------------|
| US Equity | XX% | X.X% | X.XX% |
| Int'l Equity | XX% | X.X% | X.XX% |
| Fixed Income | XX% | X.X% | X.XX% |
| Alternatives | XX% | X.X% | X.XX% |
| Cash | XX% | X.X% | X.XX% |
| **Total** | **100%** | | **X.XX%** |

- **Brinson attribution**: If applicable, decompose into allocation effect (asset class weighting vs. benchmark) and selection effect (security/manager selection within asset class)
- **Dollar impact**: Market-driven AUM change in dollar terms

### Step 3 — Organic Growth Decomposition

Calculate net new assets (NNA) — the key organic growth metric:

**New client assets:**
- Count of new relationships established
- Total initial funding from new clients
- Average new client size
- Source analysis: Referrals, COI introductions, marketing, organic inquiries
- Cost of acquisition (if available): Marketing spend / new client count

**Existing client net flows:**
- Additional contributions from existing clients (new money)
- Systematic investment plan contributions
- Retirement account rollovers into existing relationships
- One-time events (inheritance deposits, business sale proceeds)
- Scheduled withdrawals and distributions (retirement income, RMDs)
- Ad hoc withdrawals (home purchase, education, emergency)

**Net new assets calculation:**
NNA = New client assets + Existing client contributions - Existing client withdrawals

**Organic growth rate:**
Organic Growth Rate = NNA / Beginning AUM × 100

Industry benchmark for organic growth rate: 3%–5% annually is considered healthy for established practices; 5%+ is strong growth.

### Step 4 — Attrition Analysis

Quantify and analyze client losses:

- **Accounts lost**: Number of relationships terminated or transferred away
- **AUM lost**: Dollar value of assets departing
- **Attrition rate**: Lost AUM / Beginning AUM (annualized)
- **Gross vs. net**: Gross attrition (total departures) vs. net attrition (departures minus new)

**Attrition driver analysis:**

| Reason | Accounts | AUM Lost ($M) | % of Attrition |
|--------|----------|--------------|----------------|
| Moved to competitor | X | $X | XX% |
| Deceased | X | $X | XX% |
| Divorce/relationship split | X | $X | XX% |
| Dissatisfaction | X | $X | XX% |
| Fee sensitivity | X | $X | XX% |
| Advisor departure | X | $X | XX% |
| Account consolidation | X | $X | XX% |
| Other/unknown | X | $X | XX% |

**Controllable vs. uncontrollable attrition**: Separate attrition into controllable (dissatisfaction, fees, competitor — actionable) and uncontrollable (death, relocation, life events — expected baseline).

Industry benchmark: Annual attrition rate of 3%–5% is typical; >7% warrants investigation.

### Step 5 — Revenue Impact Analysis

Connect AUM changes to revenue:

- **Fee revenue bridge**: Map AUM changes to fee revenue impact
  - Market-driven AUM change × average fee rate = Market-driven revenue change
  - NNA × average fee rate × partial-year factor = Organic revenue change
  - Attrition AUM × average fee rate × partial-year factor = Revenue loss
- **Fee rate analysis**: Average fee rate trend (blending effect of new clients vs. departures)
- **Revenue per advisor**: AUM per advisor × average fee rate
- **Breakeven analysis**: NNA required to offset fee compression (if fee rates declining)

### Step 6 — Advisor-Level Attribution

Break down AUM growth by individual advisor or team:

| Advisor | Beg AUM ($M) | Market ($M) | New Clients ($M) | Net Flows ($M) | Attrition ($M) | End AUM ($M) | Organic Rate |
|---------|-------------|------------|-----------------|----------------|---------------|-------------|-------------|
| [Name] | $XX | $X.X | $X.X | $X.X | ($X.X) | $XX | X.X% |
| [Name] | $XX | $X.X | $X.X | $X.X | ($X.X) | $XX | X.X% |
| **Total** | **$XXX** | **$XX** | **$XX** | **$XX** | **($XX)** | **$XXX** | **X.X%** |

- **Productivity metrics**: New clients per advisor, NNA per advisor, revenue per advisor
- **Ranking**: Rank advisors by organic growth rate for compensation and recognition purposes
- **Trend**: Quarter-over-quarter and year-over-year growth rate trends per advisor
- **Pipeline analysis**: Weighted pipeline of prospective new clients and expected funding

### Step 7 — Forecasting and Scenario Analysis

Project AUM and revenue forward under scenarios:

**Base case:**
- Market return assumption: [X%] (based on CMAs or historical average)
- Organic growth assumption: [X%] (based on trailing 12-month trend)
- Attrition assumption: [X%] (based on trailing 12-month rate)
- Fee rate assumption: [X bps] (current blended rate)
- Projected ending AUM: $[X]
- Projected revenue: $[X]

**Bull case:** Market +[X%], organic growth +[X%], attrition -[X pp]
**Bear case:** Market -[X%], organic growth -[X pp], attrition +[X pp]

Revenue sensitivity: Show how each 1% change in market return, organic growth, or attrition affects annual revenue.

## Output Specification

```
## AUM Growth Attribution Report — [Period]

### AUM Bridge
| Component | Amount ($M) | % of Change |
|-----------|-----------|------------|
| Beginning AUM | $XXX.X | |
| Market appreciation | $XX.X | XX% |
| New client assets | $X.X | XX% |
| Existing client contributions | $X.X | XX% |
| Withdrawals/distributions | ($X.X) | XX% |
| Client attrition | ($X.X) | XX% |
| Fees deducted | ($X.X) | XX% |
| **Ending AUM** | **$XXX.X** | |

### Key Metrics
| Metric | Current Period | Prior Period | YoY | Benchmark |
|--------|---------------|-------------|-----|-----------|
| Total growth rate | X.X% | X.X% | +/-X.X% | — |
| Organic growth rate | X.X% | X.X% | +/-X.X% | 3–5% |
| Attrition rate | X.X% | X.X% | +/-X.X% | <5% |
| New clients | XX | XX | +/-XX | — |
| Avg new client size | $XXX K | $XXX K | +/-X% | — |
| Revenue impact | $X.X M | $X.X M | +/-X% | — |

### Advisor Leaderboard
[Advisor-level attribution table]

### Growth Quality Assessment
- Market-dependent growth: XX% of total
- Organic growth: XX% of total
- Growth sustainability rating: [Strong / Moderate / Weak]

### Forecast
[Scenario table with base, bull, and bear projections]
```

## Analysis Framework

Apply the **GRAIN** framework:

- **G**rowth decomposition — Separate market from organic growth precisely
- **R**etention analysis — Quantify and categorize attrition drivers
- **A**dvisor attribution — Assign growth components to individual producers
- **I**ncome impact — Connect AUM changes to revenue effects
- **N**ext period forecast — Project forward under multiple scenarios

## Examples

**Example 1 — Strong Organic Growth Quarter**

Q3 results: Beginning AUM $850M, ending AUM $912M (+$62M, +7.3%). Attribution: Market +$38M (4.5%), new clients +$18M (5 new relationships, avg $3.6M), existing client contributions +$8M, withdrawals -$6M, attrition -$4M (1 relationship lost to competitor), fees -$2M. Organic growth rate: 2.4% for the quarter (9.6% annualized), well above the 3–5% industry benchmark. Growth quality: Strong — organic growth represents 35% of total growth, indicating sustainable practice expansion not purely dependent on market returns.

**Example 2 — Market-Masked Attrition Problem**

YTD results: AUM grew 11% from $1.2B to $1.33B. Surface-level: appears healthy. Attribution: Market +$168M (+14%), new clients +$22M, contributions +$15M, withdrawals -$18M, attrition -$42M (8 relationships lost), fees -$15M. Organic growth rate: -1.9% (net outflows of $23M). Attrition rate: 3.5% (elevated). Diagnosis: Strong market returns masked a net-negative organic growth problem. Without the 14% market tailwind, the practice would have shrunk. Three of 8 lost clients cited fee dissatisfaction. Recommendation: Conduct fee competitiveness analysis, implement client retention program, investigate advisor service quality for clients at risk.

## Guidelines

- Reconcile the AUM bridge exactly to actual ending AUM — no unexplained residuals
- Use time-weighted returns (TWR) for market attribution; money-weighted for client-specific analysis
- Annualize growth rates for comparability across periods of different lengths
- Separate controllable from uncontrollable attrition for actionable insights
- Track organic growth rate as the primary health metric, not total AUM growth
- Benchmark organic growth against industry standards (Cerulli, FA Insight, InvestmentNews benchmarks)
- Include pipeline data in advisor-level reporting to provide leading indicator context
- Present growth quality metrics (organic as % of total) alongside absolute growth

## Validation Checklist

- [ ] AUM bridge reconciles exactly (beginning + components = ending, no residual)
- [ ] Market return calculated using time-weighted methodology
- [ ] New client assets distinguished from existing client contributions
- [ ] Attrition tracked by reason with controllable/uncontrollable classification
- [ ] Fee revenue impact calculated for each AUM component
- [ ] Advisor-level attribution sums to practice total
- [ ] Organic growth rate annualized for cross-period comparability
- [ ] Forecasting assumptions documented and internally consistent
- [ ] Industry benchmarks cited for organic growth and attrition rates
- [ ] Growth quality assessment distinguishes sustainable from market-dependent growth
