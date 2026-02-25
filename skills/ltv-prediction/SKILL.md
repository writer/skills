---
name: ltv-prediction
description: >
  Predicts customer lifetime value using cohort analysis, RFM-based heuristics, and probabilistic
  modeling approaches for CPG and retail e-commerce brands. Use when a user needs to forecast
  customer value, set acquisition cost thresholds, inform retention investment, or evaluate
  segment profitability. Triggers on requests for LTV calculation, CLV prediction, customer
  value modeling, payback period analysis, or acquisition ROI forecasting.

metadata:
  display_name: "Ltv Prediction"
  short_description: "Predict customer lifetime value for retail and CPG brands"
  default_prompt: "Review my customer lifetime value for retail and and highlight top risks and next actions"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# LTV Prediction

## Overview

This skill calculates and predicts Customer Lifetime Value (LTV/CLV) using multiple complementary methodologies — from simple historical averages to probabilistic BG/NBD and Gamma-Gamma models. It produces segment-level and cohort-level LTV estimates with confidence intervals, enabling data-driven decisions on customer acquisition budgets, retention investment, and marketing resource allocation.

## When to Use

- Setting customer acquisition cost (CAC) ceilings by channel or segment
- Evaluating the ROI of retention and loyalty programs
- Forecasting revenue from existing customer cohorts
- Prioritizing customer segments by predicted future value
- Building business cases for marketing investment
- Assessing LTV:CAC ratios to evaluate unit economics health
- Informing subscription pricing and discount strategy

## Required Inputs

| Input | Required | Description |
|---|---|---|
| Transaction History | Yes | Customer-level: order date, order value, order count per customer |
| Customer Base Size | Yes | Total unique customers with at least one purchase |
| Analysis Period | Yes | Historical window (minimum 12 months; 24+ months preferred) |
| Prediction Horizon | Yes | Forward-looking period (12, 24, or 36 months) |
| Gross Margin | Recommended | Average gross margin % to calculate profit-based LTV |
| Acquisition Costs | Recommended | CAC by channel/segment for LTV:CAC ratio analysis |
| Discount Rate | No | Cost of capital for NPV-adjusted LTV (default: 10% annually) |
| Cohort Definitions | No | Monthly or quarterly acquisition cohorts for cohort analysis |
| Segment Labels | No | Pre-defined segments for segment-level LTV comparison |

## Methodology

### Step 1 — Historical LTV Calculation

Calculate observed LTV for baseline benchmarking:

**Simple Historical LTV**:
```
LTV(historical) = Average Revenue Per Customer over analysis period

LTV(historical) = Total Revenue ÷ Total Unique Customers
```

**Decomposed LTV Formula**:
```
LTV = AOV × Purchase Frequency × Customer Lifespan

Where:
  AOV = Total Revenue ÷ Total Orders
  Purchase Frequency = Total Orders ÷ Total Unique Customers
  Customer Lifespan = 1 ÷ Churn Rate (in years)
```

**Margin-Adjusted LTV**:
```
LTV(profit) = AOV × Gross Margin % × Purchase Frequency × Customer Lifespan
```

**NPV-Adjusted LTV** (accounts for time value of money):
```
LTV(npv) = Σ (Monthly Revenue × Gross Margin) ÷ (1 + d)^t
  for t = 1 to T months
  where d = monthly discount rate
```

### Step 2 — Cohort-Based LTV Analysis

Build a cohort retention and value matrix:

```
Cohort (Acquisition Month) → Track over months 1, 2, 3, ..., 12+

Metrics per cohort-month:
  - Retention Rate: % of cohort active in month N
  - Cumulative Revenue Per Customer: total spend through month N
  - Marginal Revenue: incremental revenue in month N
```

**Cohort LTV Curve Construction**:
1. Group customers by acquisition month (or quarter)
2. For each cohort, calculate cumulative revenue per customer at each time point
3. Plot LTV curves — earlier cohorts provide longer time series for extrapolation
4. Identify patterns: linear growth (subscription), logarithmic decay (one-time purchase heavy), or step-function (seasonal repurchase)

**Extrapolation Methods**:
- **Log-linear fit**: LTV(t) = a × ln(t) + b — works well for decelerating growth
- **Shifted geometric**: LTV(t) = a × (1 - r^t) / (1 - r) — models retention decay
- Use the most mature cohorts to parameterize the model; apply to newer cohorts

### Step 3 — RFM-Based LTV Scoring

Map RFM segments to LTV tiers using historical performance:

| RFM Segment | Avg Historical LTV | Predicted LTV Multiplier | Confidence |
|---|---|---|---|
| Champions (555) | $XXX | 1.2×–1.5× historical | High |
| Loyal (X45+) | $XXX | 1.0×–1.2× historical | High |
| Potential Loyalists (5X2–3) | $XX | 1.5×–2.5× historical | Medium |
| Recent (511) | $XX | 0.8×–3.0× historical | Low (wide range) |
| At Risk (1–2, 4–5, 4–5) | $XXX | 0.3×–0.5× historical | Medium |
| Hibernating (111–112) | $X | 0.0×–0.2× historical | High (near zero) |

Use RFM-LTV mapping for quick segment-level estimates when full modeling infrastructure is unavailable.

### Step 4 — Probabilistic Modeling (BG/NBD + Gamma-Gamma)

For advanced prediction, apply the **Buy-Till-You-Die** framework:

**BG/NBD Model** (predicts future transaction count):
- Inputs: frequency (repeat purchases), recency (time of last purchase), T (customer age)
- Outputs: P(alive) — probability customer is still active; E(X) — expected transactions in future period
- Assumptions: Purchases follow a Poisson process; dropout follows a beta-geometric distribution

**Gamma-Gamma Model** (predicts future transaction value):
- Inputs: frequency, average transaction value, population-level value distribution
- Outputs: E(M) — expected average transaction value for each customer
- Assumption: Transaction values are gamma-distributed and independent of frequency

**Combined LTV Prediction**:
```
Predicted LTV = E(X | BG/NBD) × E(M | Gamma-Gamma) × Gross Margin %

  Discounted:
  Predicted LTV(npv) = Σ [E(transactions in period t) × E(M) × margin] ÷ (1 + d)^t
```

**Model Validation**:
- Train on first 70% of time period; validate against held-out 30%
- Metric: Mean Absolute Error (MAE) between predicted and actual customer-level spend
- Acceptable MAE: <25% of average LTV for CPG/retail
- Also validate P(alive) calibration: predicted alive probabilities should match observed reactivation rates

### Step 5 — LTV:CAC Ratio Analysis

Calculate unit economics health by channel and segment:

```
LTV:CAC Ratio = Predicted LTV ÷ Customer Acquisition Cost

Interpretation:
  < 1.0  → Unprofitable; losing money on acquisition
  1.0–2.0 → Marginal; requires high retention to break even
  2.0–3.0 → Healthy; typical target for DTC CPG brands
  3.0–5.0 → Strong; room to increase acquisition spend
  > 5.0  → Potentially under-investing in growth
```

**Payback Period**:
```
Payback Period = CAC ÷ (Monthly Revenue Per Customer × Gross Margin %)

CPG Benchmarks:
  Subscription CPG: 3–6 months payback
  Non-subscription DTC: 6–12 months payback
  Marketplace-dependent: 2–4 months payback (lower CAC, lower LTV)
```

### Step 6 — Sensitivity Analysis & Scenarios

Model LTV under different retention and AOV assumptions:

| Scenario | Retention Rate | AOV | Frequency | Predicted 24mo LTV |
|---|---|---|---|---|
| Base Case | Current | Current | Current | $XXX |
| Retention +10% | +10pp | Current | Current | $XXX (+XX%) |
| AOV +15% | Current | +15% | Current | $XXX (+XX%) |
| Frequency +1 order | Current | Current | +1/year | $XXX (+XX%) |
| Combined Upside | +10pp | +10% | +0.5/year | $XXX (+XX%) |
| Downside | -10pp | -5% | Current | $XXX (-XX%) |

Identify which lever (retention, AOV, frequency) has the greatest LTV impact — this prioritizes marketing strategy.

### Step 7 — Segment-Level LTV Summary

Produce a summary table:

```
Segment       | Customers | Avg LTV(12mo) | Avg LTV(24mo) | LTV:CAC | Payback | Priority
Champions     | X,XXX     | $XXX          | $XXX          | X.X     | X mo    | Retain
Loyal         | X,XXX     | $XXX          | $XXX          | X.X     | X mo    | Grow
Pot. Loyalists| X,XXX     | $XX           | $XXX          | X.X     | X mo    | Convert
New           | X,XXX     | $XX           | $XX–$XXX      | X.X     | X mo    | Nurture
At Risk       | X,XXX     | $XXX          | $XX           | N/A     | N/A     | Win-back
```

## Output Specification

1. **LTV Summary Metrics**: Overall average LTV (historical, 12mo predicted, 24mo predicted)
2. **Cohort LTV Curves**: Cumulative revenue per customer by cohort with trend extrapolation
3. **Segment-Level LTV Table**: Per-segment LTV with confidence intervals
4. **LTV:CAC Analysis**: Ratio by channel and segment with payback period
5. **Sensitivity Analysis**: Impact of retention, AOV, and frequency changes on LTV
6. **Key Lever Identification**: Which growth lever has the highest LTV impact
7. **Methodology Notes**: Model used, assumptions, validation metrics, and limitations

## Examples

**Input**: "Calculate LTV for our DTC coffee subscription brand. 30,000 customers, 24 months of data, $35 AOV, 65% gross margin. We spend $40 CAC on Meta and $25 on Google."

**Output**: Historical 12-month LTV of $142; predicted 24-month LTV of $198 (BG/NBD + Gamma-Gamma). LTV:CAC of 3.5× for Meta, 5.7× for Google — recommend shifting 15% of Meta budget to Google. Cohort analysis shows LTV curves plateau at month 18 for non-subscribers vs. continuous growth for subscribers. Key lever: converting one-time buyers to subscription (+$85 incremental LTV). Sensitivity: +10pp retention increases 24mo LTV by 28%.

**Input**: "We need LTV estimates per customer segment for our beauty e-commerce brand to set acquisition budgets for next year."

**Output**: Segment-level 12-month predicted LTV ranging from $28 (one-time discount buyers) to $340 (VIP multi-category buyers). Recommendation: set Meta CPA cap at $45 for VIP-likely audiences (LTV:CAC 7.5×) and $15 for deal-seeker audiences (LTV:CAC 1.9×). Cohort analysis shows Q4-acquired customers have 20% lower LTV due to promotion-driven acquisition.

## Guidelines

- Always calculate both revenue-based and profit-based (margin-adjusted) LTV
- Minimum 12 months of data required; flag low-confidence predictions for businesses <12 months old
- Exclude outlier transactions (>99th percentile order value) to prevent skewed averages
- For subscription businesses, separate subscriber vs. non-subscriber LTV — they have fundamentally different curves
- Discount-heavy acquisition cohorts typically show 15–30% lower LTV; flag this in analysis
- NPV discounting is critical for long prediction horizons (>12 months)
- Always present confidence intervals, not point estimates, for predicted LTV
- BG/NBD assumes non-contractual settings (customer can leave silently); use different models for subscription/contractual
- Validate model predictions against holdout data before using for budget decisions
- Seasonal CPG categories (sunscreen, cold remedies) need seasonality-adjusted frequency estimates

## Validation Checklist

- [ ] Historical LTV calculated using at least two methods (simple and decomposed)
- [ ] Cohort analysis includes at least 4 cohorts with sufficient maturity
- [ ] LTV predictions include confidence intervals or scenario ranges
- [ ] LTV:CAC ratios calculated per acquisition channel
- [ ] Payback period estimated and compared against cash flow constraints
- [ ] Sensitivity analysis identifies the highest-impact growth lever
- [ ] Model validation metrics reported (MAE, calibration of P(alive))
- [ ] Segment-level LTV differences are large enough to justify differentiated strategy
- [ ] Assumptions and limitations are transparently documented
