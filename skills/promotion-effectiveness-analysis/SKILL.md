---
name: promotion-effectiveness-analysis
description: >
  Evaluates the return on investment and effectiveness of trade promotions, temporary price reductions, and
  marketing events for CPG and retail products. Use when the user wants to assess whether promotions are
  profitable, compare promotion types, optimize promotion calendars, or reduce inefficient promotional spending.
  Triggers on requests about promo effectiveness, promo ROI, trade promotion analysis, promotion lift,
  promotional efficiency, or deal evaluation.

metadata:
  display_name: "Promotion Effectiveness Analysis"
  short_description: "Evaluate trade promotion ROI, lift, and spending efficiency"
  default_prompt: "Analyze my promotion effectiveness and recommend clear next actions"
  version: "1.0.0"
  tags:
    - commerce-intelligence
    - promotion-effectiveness-analysis
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Promotion Effectiveness Analysis

## Overview

Promotion Effectiveness Analysis provides a rigorous framework for evaluating whether trade promotions and temporary price reductions generate profitable incremental volume or simply subsidize sales that would have occurred anyway. In CPG, trade promotion spending represents 15–25% of gross revenue—the second-largest line item after COGS—yet industry studies consistently find that 50–70% of promotions fail to break even.

This skill decomposes promotional volume into its true components (incremental vs. cannibalization vs. pantry loading vs. pull-forward), computes ROI using multiple methodologies, and provides actionable recommendations for optimizing the promotion calendar.

## When to Use

- Post-promotion analysis: evaluating a completed promotion's effectiveness
- Promotion planning: forecasting expected lift and ROI for a proposed promotion
- Annual trade fund optimization: reallocating promotion budgets across brands, categories, or tactics
- Comparing promotion tactics: TPR vs. BOGO vs. display vs. digital coupon vs. bundle
- Evaluating promotional dependency: determining if a brand is over-promoted
- Retailer-supplier joint business planning requiring promotion performance evidence

## Required Inputs

| Input | Required | Description |
|---|---|---|
| Promoted item sales data | Yes | Weekly units and revenue during promotion and surrounding non-promo periods (min 8 weeks pre/post) |
| Promotion details | Yes | Type (TPR, BOGO, display, coupon), start/end dates, promoted price, regular price, funding source |
| Baseline sales estimate | Yes/Derived | Non-promoted sales level; can be calculated from pre/post-promo data or provided |
| Trade spend/cost | Recommended | Promotion funding amount (scan-backs, billbacks, off-invoice, ad costs) |
| Margin data | Recommended | Regular and promoted margin per unit; cost of goods |
| Category sales data | Recommended | Total category volume during promo to assess share shift vs. category expansion |
| Competitive promo data | Optional | Whether competitors were also promoting during the same period |
| Consumer panel data | Optional | Household-level data to assess buyer dynamics (new vs. existing, pantry loading) |

## Methodology

### Step 1: Baseline Estimation

Establish the counterfactual—what would have sold without the promotion:

**Method A: Pre/Post Average**
```
Baseline = Average of (4-week pre-promo sales + 4-week post-promo sales) / 2
```
Adjust for trend and seasonality. Simple but effective for isolated promotions.

**Method B: Matched Control**
Use non-promoted stores/SKUs as a control group to estimate baseline during the promo period. More rigorous; handles concurrent market shifts.

**Method C: Statistical Model**
Fit a time-series model (e.g., structural time series, Prophet) to pre-promo data; forecast the promo period as baseline. Best for complex, overlapping promotions.

**Post-Promotion Dip Adjustment**: Measure the dip below baseline in weeks 1–4 after promotion ends. This "pull-forward" volume must be subtracted from incremental lift:
```
Adjusted Incremental = Promo Lift − Post-Promo Dip
```

### Step 2: Volume Decomposition

Decompose total promotion-period volume into components:

```
Total Promo Volume = Baseline Volume + Incremental Volume
```

Further decompose Incremental Volume:

```
Incremental = Category Expansion + Share Shift + Pantry Loading + Pull-Forward
```

| Component | Definition | Measurement | Typical % of Lift |
|---|---|---|---|
| **Category Expansion** | New consumption occasions created by the promotion | Category volume increase during promo | 10–25% |
| **Share Shift** | Volume taken from competitors | Own share gain × category volume | 20–40% |
| **Pantry Loading** | Consumers stock up, reducing future purchases | Post-promo volume dip analysis | 15–30% |
| **Pull-Forward** | Sales moved from future periods to current | Time-shift analysis of purchase occasions | 10–20% |
| **Subsidized Baseline** | Volume that would have occurred anyway at full price | Baseline estimate during promo | Not incremental — this is waste |

### Step 3: Promotion ROI Calculation

**Volume Lift %**:
```
Lift % = (Actual Promo Volume − Baseline Volume) / Baseline Volume × 100
```

**Incremental Revenue**:
```
Incremental Revenue = Incremental Units × Promoted Price
```

**Promotion Cost**:
```
Total Promo Cost = Trade Spend + (Regular Margin − Promo Margin) × Baseline Volume
```
The second term captures the margin given away on sales that would have happened at full price.

**Promotion ROI**:
```
ROI = (Incremental Margin − Promo Cost) / Promo Cost × 100
```

Where Incremental Margin = Incremental Units × Promoted Margin per Unit

**Breakeven Lift**: The minimum lift required for the promotion to generate positive ROI:
```
Breakeven Lift % = (Regular Price − Promo Price) / (Promo Price − COGS) × Baseline Units × 100 / Baseline Units
```

Simplified:
```
Breakeven Lift % = Discount % / (Promo Margin % − Discount %)
```

### Step 4: Efficiency Metrics

Calculate efficiency ratios to compare across promotion types:

**Cost per Incremental Unit**:
```
CPIU = Total Promo Cost / Incremental Units
```

**Promoted Revenue per $1 Trade Spend**:
```
Revenue Efficiency = Incremental Revenue / Trade Spend
```
Benchmark: $3–$8 of incremental revenue per $1 of trade spend for effective promotions.

**Incremental Margin Return on Investment (iMROI)**:
```
iMROI = Incremental Margin $ / Total Promo Cost
```
Target: iMROI > 1.0 (every dollar spent generates more than $1 in incremental margin).

### Step 5: Promotion Tactic Comparison

Compare across promotion types using a standardized framework:

| Promotion Type | Avg Lift % | Avg ROI | Avg Duration | Best For |
|---|---|---|---|---|
| TPR (shelf price reduction) | 20–60% | Variable | 1–2 weeks | Volume driving, price image |
| Display only | 15–30% | High (low cost) | 1–2 weeks | Impulse, awareness |
| Feature (ad/flyer) | 25–50% | Medium | 1 week | Traffic driving |
| Feature + Display | 50–150% | Medium-High | 1 week | Maximum lift events |
| BOGO / Multibuy | 80–200% | Low (deep discount) | 1–2 weeks | Trial, pantry loading |
| Digital coupon | 10–25% | High (targeted) | 2–4 weeks | Targeted, measurable |
| Bundle/cross-promo | 15–40% | Medium-High | 2–4 weeks | Basket building |

### Step 6: Promotional Calendar Optimization

Based on historical effectiveness data, recommend an optimized promotion calendar:

1. **Frequency optimization**: Calculate optimal weeks on promo per year (benchmark: 12–18 weeks for center-store CPG)
2. **Depth optimization**: Find the price point on the promotion response curve that maximizes iMROI
3. **Timing optimization**: Align promotions with high-traffic periods and avoid competitor overlap
4. **Tactic mix**: Shift spend toward highest-ROI tactics
5. **Cannibalization management**: Space promotions to minimize inter-brand cannibalization

## Output Specification

### 1. Promotion Scorecard

| Metric | Result | Benchmark | Rating |
|---|---|---|---|
| Volume Lift % | — | 30–50% | Green/Yellow/Red |
| Incremental Units | — | — | — |
| Promotion ROI | — | > 0% | — |
| iMROI | — | > 1.0 | — |
| Cost per Incremental Unit | — | < $X | — |
| Post-Promo Dip | — | < 10% of lift | — |

### 2. Volume Decomposition Waterfall

Visual/tabular breakdown: Baseline → + Category Expansion → + Share Shift → − Pantry Loading → − Pull-Forward → = True Incremental

### 3. Tactic Comparison Matrix

Comparison across promotion types with lift, ROI, cost efficiency, and strategic rating.

### 4. Calendar Recommendations

Proposed promotion calendar for next period with recommended timing, depth, and tactic for each event.

### 5. Trade Spend Reallocation

Current vs. recommended allocation of trade funds across brands/categories/tactics with expected ROI improvement.

## Analysis Framework

### Key Metrics

- **Volume Lift %**: (Promo Volume − Baseline) / Baseline (benchmark: 30–100% depending on tactic)
- **Promotion ROI %**: (Incremental Profit − Promo Cost) / Promo Cost (target: > 0%, top quartile > 25%)
- **iMROI**: Incremental margin per dollar of trade spend (target: > 1.0)
- **Subsidized Volume %**: Baseline volume during promo / total promo volume (lower is better; > 60% indicates waste)
- **Promotional Dependency**: % of annual volume sold on deal (healthy: 25–40% for CPG; > 50% is problematic)
- **Promo Frequency**: Weeks on promotion per year (benchmark: 12–20 for CPG)
- **Average Discount Depth**: Promoted price / regular price (typical: 15–30% off)
- **Halo Effect**: Sales lift in adjacent non-promoted products during the promotion

### Profitability Benchmarks

- Promotions with < 20% lift rarely break even after accounting for baseline subsidy
- Feature + display combinations typically deliver 2–3× the lift of price cut alone at similar cost
- Post-promo dip exceeding 30% of lift indicates heavy pantry loading — consider depth reduction
- Promotions deeper than 35% off exhibit diminishing returns and attract cherry-pickers

## Examples

**Input**: "Evaluate the effectiveness of our Q4 BOGO promotion on Brand X Pasta Sauce (24oz). The promo ran for 2 weeks in 1,800 stores. Regular price $3.99, promoted at 2/$3.99 (effectively 50% off second unit). Trade spend was $180K. Here are 16 weeks of weekly sales data (4 pre, 2 during, 10 post)."

**Output**:
1. **Lift**: +142% volume lift during promo period (baseline: 18K units/week → actual: 43.5K units/week)
2. **Decomposition**: Of 51K incremental units, 31% was category expansion, 28% share shift (from competitor sauce brands), 26% pantry loading (dip visible weeks 1–4 post), 15% pull-forward
3. **ROI**: Total promo cost $247K (trade spend $180K + baseline margin subsidy $67K). Incremental margin: $122K. ROI: −50.6%. **The promotion destroyed value.**
4. **Diagnosis**: BOGO was too deep. The 50% effective discount required a 280% lift to break even; we achieved 142%. Pantry loading was excessive — consumers stocked up for 5–6 weeks.
5. **Recommendation**: Switch to 25% off TPR ($2.99) with feature + display support. Expected lift: 65–80%. Expected ROI: +12–22%. Reduce promo depth, increase promo frequency from 2× to 4× per year with shallower cuts.

## Guidelines

- Always calculate baseline rigorously — the most common source of misleading promotion analysis is an inaccurate baseline
- Account for post-promotion dip; failing to do so overstates effectiveness by 15–30% on average
- Separate retailer-funded promotions from manufacturer-funded to compute the correct ROI for each party
- Use category-level analysis alongside item-level to distinguish share shift from category growth
- Beware of "promotional addiction": when base volume erodes because consumers learn to wait for deals
- Consider the long-term brand equity impact of deep or frequent promotions (hard to quantify but real)
- Don't evaluate promotions in isolation — assess the full promotional calendar and competitive context
- Different metrics matter to different stakeholders: retailers care about category $ growth; manufacturers care about brand profit
- For BOGO/multibuy, calculate the effective per-unit price; a "buy 2 get 1 free" is a 33% discount
- Always compare actual lift against breakeven lift — many promotions with impressive lift still lose money

## Validation Checklist

- [ ] Baseline methodology is explicitly stated and appropriate for the context
- [ ] Post-promotion dip is measured and netted from incremental calculation
- [ ] Volume decomposition includes all components (expansion, share, pantry, pull-forward)
- [ ] ROI includes both trade spend and baseline margin subsidy in cost
- [ ] Breakeven lift is calculated and compared to actual lift
- [ ] Tactic-level comparison uses consistent methodology
- [ ] Promotional dependency is assessed (% volume on deal)
- [ ] Category-level impact is analyzed alongside item-level
- [ ] Recommendations include specific tactic, depth, timing, and expected ROI
- [ ] Long-term effects (brand equity, base erosion) are acknowledged
