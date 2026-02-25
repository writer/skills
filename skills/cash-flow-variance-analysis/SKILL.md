---
name: cash-flow-variance-analysis
description: Explain cash flow variance drivers including actual vs. forecast deviations, timing differences, behavioral assumption accuracy, and liquidity impact attribution. Use when analyzing cash flow forecast accuracy, explaining treasury cash position variances, or improving cash flow prediction models for ALCO reporting.

metadata:
  display_name: "Cash Flow Variance Analysis"
  short_description: "Explain cash flow variance drivers including actual vs."
  default_prompt: "Analyze my cash flow variance and recommend clear next actions"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Cash Flow Variance Analysis

## Overview

Systematically decomposes the variance between forecast and actual cash flows to identify root causes—timing shifts, volume deviations, behavioral assumption errors, market-driven changes, and operational factors. Enables treasury to improve forecast accuracy, refine behavioral models, enhance liquidity planning, and provide transparent variance explanations to ALCO and regulators.

## When to Use

- Explaining material variance between forecast and actual daily/weekly/monthly cash positions
- Analyzing the accuracy of liquidity forecasting models
- Identifying systemic biases in cash flow projection assumptions
- Improving behavioral models for deposit flows, loan prepayments, and drawdowns
- Reporting cash position variance to ALCO with actionable root-cause analysis
- Calibrating contingency funding plan assumptions based on observed flows

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Forecast cash flows | Projected inflows and outflows by category and time bucket | Time-bucketed table |
| Actual cash flows | Realized inflows and outflows by category and time bucket | Time-bucketed table |
| Behavioral assumptions | Deposit run-off, prepayment, drawdown, and rollover rates used in forecast | Parameter table |
| Business plan data | Planned originations, maturities, and balance sheet movements | Plan vs. actual |
| Market data | Rate changes, spread movements affecting cash flows | Market observations |
| Operational events | Unplanned events (large withdrawals, settlement failures, system issues) | Event log |
| Historical variance | Prior period variance data for trend and bias analysis | Time series |

## Methodology

### Step 1 — Establish the Variance Framework

Organize the variance analysis into a structured taxonomy:

**Primary variance categories:**
- **Volume variance**: Actual balance changes differ from forecast (larger/smaller flows)
- **Timing variance**: Correct amounts but different timing (early/late settlement, delayed maturities)
- **Rate/price variance**: Market rate changes affecting cash flow amounts (floating-rate coupons, FX)
- **Behavioral variance**: Actual customer behavior differs from modeled assumptions
- **Operational variance**: Unplanned events, system issues, counterparty actions
- **Model variance**: Structural deficiencies in the forecasting methodology

Total Variance = Volume + Timing + Rate + Behavioral + Operational + Model

### Step 2 — Compute Gross and Net Variances

For each cash flow category (asset inflows, liability outflows, off-balance-sheet, operations):

- **Gross variance** = |Actual − Forecast| (absolute magnitude, captures total forecasting error)
- **Net variance** = Actual − Forecast (directional, captures bias)
- **Variance ratio** = Net Variance / Forecast (relative magnitude for comparability)

Analyze at multiple aggregation levels:
- Individual cash flow line items (e.g., residential mortgage prepayments)
- Category subtotals (e.g., total loan portfolio cash flows)
- Grand total net cash position variance

Flag any line item where |variance ratio| > 10% as material for root-cause investigation.

### Step 3 — Decompose by Variance Type

For each material variance, attribute to specific drivers:

**Volume variance analysis:**
- Planned originations vs. actual: Were new loans/deposits higher or lower than plan?
- Unplanned maturities or terminations: Early repayments, deposit closures, contract cancellations
- Pipeline conversion: Committed facilities that drew down vs. remained undrawn
- Quantify: (Actual Volume − Forecast Volume) × Forecast Rate = Volume Variance

**Timing variance analysis:**
- Settlement date shifts: Payments or receipts arriving earlier or later than contractual date
- End-of-period cutoff effects: Transactions straddling the reporting boundary
- Seasonal patterns not captured in the forecast
- Quantify by netting across adjacent time buckets (pure timing variance nets to zero over longer horizons)

**Behavioral variance analysis:**
- Deposit run-off: Actual withdrawal rates vs. modeled decay functions
- Loan prepayments: Actual CPR vs. projected prepayment speeds
- Facility drawdowns: Actual utilization vs. modeled drawdown rates
- Rollover rates: Actual renewal rates on maturing deposits/wholesale funding vs. assumed
- Quantify: (Actual Behavioral Rate − Modeled Rate) × Relevant Balance = Behavioral Variance

**Rate/price variance analysis:**
- Floating-rate coupon resets at different rates than forecast
- FX rate changes affecting foreign-currency cash flows
- Spread changes affecting market-based funding costs

### Step 4 — Assess Forecast Bias

Analyze systematic forecast errors over a rolling 6-12 month window:

- **Mean forecast error (MFE)**: Average of (Actual − Forecast); non-zero indicates persistent bias
  - Positive MFE: Systematic under-forecasting of net cash inflows (conservative bias)
  - Negative MFE: Systematic over-forecasting (optimistic bias)
- **Mean absolute forecast error (MAFE)**: Average of |Actual − Forecast|; measures accuracy irrespective of direction
- **Forecast accuracy ratio**: 1 − (MAFE / Average Actual); higher is better, target >90%
- **Bias by category**: Identify which cash flow categories have the largest systematic bias
- **Directional accuracy**: Percentage of periods where the forecast correctly predicted the direction of net flows

### Step 5 — Assess Liquidity Impact

Translate cash flow variances into liquidity risk implications:

- **Intraday impact**: Did the variance cause intraday overdrafts or require unexpected repo borrowing?
- **Buffer impact**: How did the variance affect the HQLA buffer or LCR calculation?
- **Limit impact**: Did the variance cause a breach of internal liquidity limits or early-warning triggers?
- **Cost impact**: Quantify the cost of unexpected borrowing or opportunity cost of excess liquidity
- **Stress calibration**: Should contingency funding plan assumptions be recalibrated based on observed variance?

### Step 6 — Identify Actionable Improvements

Based on the root-cause analysis, recommend specific improvements:

**Model improvements:**
- Recalibrate behavioral parameters (update deposit decay functions, prepayment models, drawdown rates)
- Incorporate new variables (e.g., digital channel deposit behavior, macroeconomic indicators)
- Adjust confidence intervals on forecasts to reflect observed variance

**Process improvements:**
- Enhance communication with business lines for large transaction visibility
- Implement T+1 rolling forecast updates for high-variance categories
- Add conditional forecast branches for known upcoming events (rate decisions, large maturities)

**Reporting improvements:**
- Add variance dashboards with trend visualization
- Implement traffic-light early-warning for forecast deviation
- Report forecast accuracy KPIs alongside cash flow data

### Step 7 — Compile the Variance Report

Structure the final output:
1. **Headline variance**: Net cash position variance with materiality assessment
2. **Variance waterfall**: Decomposition into volume, timing, rate, behavioral, operational, model
3. **Top 5 line-item variances**: Material items with root-cause explanation
4. **Forecast accuracy metrics**: MFE, MAFE, accuracy ratio, directional accuracy
5. **Liquidity impact**: Any limit breaches, cost impacts, or stress calibration implications
6. **Trend analysis**: Is forecast accuracy improving or deteriorating over time?
7. **Action items**: Specific model, process, or reporting improvements with owners

## Output Specification

```markdown
# Cash Flow Variance Analysis — [Period]

## Headline
Net cash position was $[X]M [above/below] forecast, a variance of [Y]%.

## Variance Waterfall
| Category | Variance ($M) | % of Total | Direction |
|----------|--------------|------------|-----------|
| Volume | | | |
| Timing | | | |
| Rate/Price | | | |
| Behavioral | | | |
| Operational | | | |
| Model | | | |
| **Total** | | **100%** | |

## Top 5 Material Variances
| Rank | Line Item | Forecast ($M) | Actual ($M) | Variance ($M) | Root Cause |
|------|-----------|---------------|-------------|---------------|------------|

## Forecast Accuracy Metrics
| Metric | Current Period | 6-Month Avg | Trend | Target |
|--------|---------------|-------------|-------|--------|
| Mean Forecast Error | | | | ±2% |
| Mean Absolute Error | | | | <5% |
| Accuracy Ratio | | | | >90% |
| Directional Accuracy | | | | >85% |

## Liquidity Impact Assessment
[Impact on LCR, limits, borrowing costs]

## Bias Analysis
[Systematic patterns identified with recommended calibration adjustments]

## Action Items
| # | Action | Category | Owner | Deadline |
|---|--------|----------|-------|----------|
```

## Analysis Framework

Apply the **Forecast-Observe-Analyze-Improve (FOAI) cycle**:
1. **Forecast**: Generate projections using behavioral models and business plan inputs
2. **Observe**: Capture actual cash flows at equivalent granularity to forecasts
3. **Analyze**: Decompose variance into the six variance categories with root-cause attribution
4. **Improve**: Update models, refine assumptions, enhance processes based on findings

Each FOAI cycle iteration should demonstrably improve forecast accuracy metrics.

## Examples

**Example — Behavioral Variance Narrative:**
"The $340M net cash outflow variance was primarily driven by behavioral variance in the retail deposit portfolio (-$280M). Actual demand deposit outflows exceeded the modeled 3% monthly decay rate, with observed outflows at 4.7%, reflecting increased competitive pressure from online banks offering 80bps above our posted rate. The prepayment model also underestimated residential mortgage prepayments by $95M as refinancing activity spiked following the 50bps rate cut. Recommendation: recalibrate the deposit decay function to incorporate competitive rate differential as an explanatory variable."

**Example — Timing Variance Narrative:**
"Total gross variance of $620M reduces to a net variance of only $45M after netting timing effects across adjacent weeks. A $380M corporate loan repayment expected in Week 2 settled in Week 3, and a $195M institutional deposit inflow forecast for Week 3 arrived in Week 2. These timing shifts, while netting out over the month, caused a $380M intraday liquidity shortfall on Day 8 requiring a $400M overnight repo at a cost of $52K. Recommendation: implement T+1 large-transaction settlement tracking for flows exceeding $100M."

## Guidelines

- Always distinguish between gross and net variance (gross measures accuracy, net measures bias)
- Decompose into all six variance categories; do not lump residual into 'other'
- Report forecast accuracy metrics over rolling windows, not single periods
- Quantify the cost of forecast errors (borrowing cost, opportunity cost, limit breach)
- Separate timing variance from true volume variance by netting across adjacent periods
- Update behavioral parameters quarterly based on observed variance analysis
- Flag persistent biases (>3 consecutive periods in same direction) for immediate model recalibration

## Validation Checklist

- [ ] Forecast and actual data are at equivalent granularity and categorization
- [ ] Variance waterfall components sum to total net variance
- [ ] Material variances (>10% variance ratio) have root-cause attribution
- [ ] Timing variances verified to net to approximately zero over longer horizons
- [ ] Behavioral variance traced to specific model parameter deviations
- [ ] Forecast accuracy metrics computed over minimum 6-month rolling window
- [ ] Liquidity impact assessed for buffer, limit, and cost implications
- [ ] Bias analysis covers directional persistence and magnitude trends
- [ ] Action items are specific with owners and deadlines
- [ ] FOAI cycle iteration documented with expected accuracy improvement
