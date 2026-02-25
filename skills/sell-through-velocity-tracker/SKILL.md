---
name: Sell-Through Velocity Tracker
description: Track product sell-through velocity against category benchmarks, seasonal expectations, and lifecycle targets, identifying fast and slow movers with actionable recommendations for markdown, promotion, or reorder acceleration.

metadata:
  display_name: "Sell Through Velocity Tracker"
  short_description: "Track product sell-through velocity against benchmarks"
  default_prompt: "Review my sell through velocity and highlight top risks and next actions"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Sell-Through Velocity Tracker

## Overview

This skill monitors sell-through velocity—the rate at which inventory converts to sales—across the product portfolio, comparing actual performance against category benchmarks, seasonal curves, and lifecycle targets. It identifies products selling faster or slower than expected, quantifies the financial impact of velocity deviations, and recommends actions including markdown timing, promotional intervention, reorder acceleration, or assortment rationalization. Sell-through is a leading indicator of inventory health, and early detection of velocity problems prevents both stockouts on winners and margin erosion on losers.

## When to Use

- During weekly merchandising reviews to track in-season product performance
- Within the first 2-4 weeks of a new product launch to assess early velocity signals
- During seasonal transitions to identify products that need markdown acceleration
- When evaluating promotional effectiveness (pre vs. during vs. post promotion velocity)
- During open-to-buy planning to allocate future purchase budget based on velocity trends
- For end-of-life inventory management to determine disposition timing

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `sales_data` | Daily or weekly unit sales by SKU-location | Structured array |
| `inventory_data` | Beginning on-hand inventory, receipts, and current on-hand | Structured array |
| `plan_targets` | Planned sell-through rates by week/month by category | Structured object |
| `seasonal_curves` | Expected demand shape by week-of-season for each category | Normalized array |
| `product_lifecycle` | Launch date, planned life, lifecycle stage (intro, growth, maturity, decline) | Structured object |
| `pricing_data` | Original price, current price, planned markdowns | Structured object |
| `category_benchmarks` | Industry sell-through benchmarks by category and channel | Structured object |
| `promotional_calendar` | Promotion dates, type, and expected lift | Structured object |

## Methodology

### Step 1: Sell-Through Rate Calculation

Compute sell-through at multiple time horizons:

```
Sell_Through_Rate = Units_Sold / (Beginning_Inventory + Receipts) × 100
```

Time-based variants:
```
Weekly_Sell_Through = Units_Sold_This_Week / BOW_Inventory × 100
Cumulative_Sell_Through = Total_Units_Sold_Since_Receipt / Total_Units_Received × 100
Sell_Through_Velocity = Units_Sold_per_Day  [absolute rate]
Days_to_Sell_Through = Remaining_Inventory / Average_Daily_Sales  [projected clearance timeline]
```

### Step 2: Velocity Benchmarking

Compare actual velocity against multiple benchmarks:

```
Velocity_Index = Actual_Sell_Through / Planned_Sell_Through × 100
```

| Velocity Index | Classification | Interpretation |
|---------------|---------------|----------------|
| > 130 | Outperforming | Selling faster than plan — monitor for stockout risk |
| 110-130 | Strong | On track, consider increasing future buy |
| 90-110 | On Plan | Within acceptable range |
| 70-89 | Underperforming | Below plan — investigate cause, prepare intervention |
| < 70 | Critical | Significantly behind — markdown or cancellation required |

Category-specific benchmarks (cumulative sell-through by end of lifecycle):

| Category | Target Sell-Through | Good | At Risk |
|----------|-------------------|------|---------|
| Fashion apparel | 60-70% at full price | >55% | <40% |
| Basic apparel | 80-90% at full price | >75% | <60% |
| Consumer electronics | 85-95% | >80% | <70% |
| Seasonal (holiday/summer) | 70-80% by season end | >65% | <50% |
| Grocery / CPG | 95-99% (perishable target) | >93% | <90% |

### Step 3: Seasonal Curve Alignment

Compare actual sell-through progression against the expected seasonal demand curve:

```
Curve_Alignment_Score = 1 - |Actual_Cumulative_%_Sold - Expected_Cumulative_%_Sold|
```

Detect timing misalignment:
- **Ahead of curve**: Selling faster than seasonal pattern — likely to sell out before season end
- **Behind curve**: Selling slower — late-season markdown pressure building
- **Phase shift**: Peak selling week occurred earlier or later than expected

```
Seasonal_Peak_Week_Actual vs. Seasonal_Peak_Week_Expected
Peak_Shift = Actual_Peak_Week - Expected_Peak_Week  [negative = early, positive = late]
```

### Step 4: Cohort & Lifecycle Analysis

Track sell-through by product cohort (launch week) to establish velocity norms:

```
Week_1_Sell_Through by cohort → establishes early velocity benchmark
Week_4_Sell_Through by cohort → validates initial signal
Week_8_Sell_Through by cohort → determines lifecycle trajectory
```

Early warning system:
- If Week 2 cumulative sell-through is <50% of Week 2 benchmark for the category: flag as slow mover
- If Week 2 cumulative sell-through is >150% of benchmark: flag as potential winner, expedite reorder

Lifecycle velocity expectations:
```
Introduction: Increasing velocity (awareness building)
Growth: Peak velocity (market adoption)
Maturity: Stable velocity (replacement demand)
Decline: Decreasing velocity (markdown/exit phase)
```

### Step 5: Financial Impact & Action Recommendations

Quantify the financial consequences of velocity deviations:

**For slow movers (below plan):**
```
Unsold_Inventory_Risk = Remaining_Units × Unit_Cost
Markdown_Exposure = Remaining_Units × (Original_Price - Expected_Clearance_Price)
Carrying_Cost_Exposure = Remaining_Units × Unit_Cost × Carrying_Rate × Expected_Weeks_to_Clear / 52
Opportunity_Cost = Shelf_Space_Occupied × (Avg_Category_GMROI - Actual_GMROI)
```

**For fast movers (above plan):**
```
Stockout_Risk_Revenue = Projected_Unmet_Demand × Selling_Price
Lost_Margin = Projected_Unmet_Demand × Unit_Margin
Reorder_Urgency = Days_to_Stockout < Supplier_Lead_Time  [boolean critical flag]
```

Action matrix:

| Velocity | Lifecycle Stage | Recommended Action |
|---------|----------------|-------------------|
| Fast | Introduction/Growth | Expedite reorder, increase forward buy, expand distribution |
| Fast | Maturity | Ensure steady replenishment, capture demand data for next season |
| Fast | Decline | Do not reorder, let inventory deplete naturally |
| Slow | Introduction | Increase marketing, adjust placement, extend trial period |
| Slow | Growth | Investigate: pricing, competition, content quality, visibility |
| Slow | Maturity | Initiate 10-20% markdown, bundle with fast movers |
| Slow | Decline | Aggressive markdown (30-50%), move to clearance channel |

## Output Specification

```yaml
sell_through_report:
  report_date: "2026-02-07"
  portfolio_summary:
    total_skus_tracked: 3200
    on_plan_pct: 64
    outperforming_pct: 12
    underperforming_pct: 18
    critical_pct: 6
    portfolio_sell_through_rate: 72.3
    plan_target: 75.0
  fast_movers:
    - sku_id: "SKU-JACKET-2201"
      velocity_index: 185
      cumulative_sell_through: 68
      weeks_in_market: 4
      days_to_stockout: 9
      remaining_units: 340
      action: "EXPEDITE REORDER — 2,000 units from supplier, air freight justified ($3,200 premium vs. $28,000 lost margin)"
      revenue_at_risk: 48000
  slow_movers:
    - sku_id: "SKU-SWEATER-1855"
      velocity_index: 42
      cumulative_sell_through: 18
      weeks_in_market: 8
      remaining_units: 4200
      inventory_value: 126000
      markdown_recommendation:
        timing: "Immediate"
        initial_markdown_pct: 25
        expected_velocity_lift: 2.5
        projected_sell_through_after_markdown: 55
        projected_margin_recovery: 73500
      root_cause_hypothesis: "3 competing styles launched by competitor at 15% lower price point"
  seasonal_alerts:
    - category: "Winter Outerwear"
      season_week: 14
      total_season_weeks: 18
      cumulative_sell_through: 52
      target_at_this_point: 70
      gap_pct: 18
      inventory_at_risk_value: 890000
      recommendation: "Category-wide 20% markdown event needed by Week 15 to clear before spring transition"
```

## Analysis Framework

### GMROI Integration

Connect sell-through velocity to return on inventory investment:

```
GMROI = Gross_Margin_$ / Average_Inventory_Cost
     = (Sell_Through_Rate × Gross_Margin_%) / (1 - Sell_Through_Rate / 2) × (365 / Avg_Days_in_Stock)
```

A SKU with high sell-through and healthy margins = high GMROI (keep/grow). A SKU with low sell-through regardless of margin = low GMROI (fix/exit).

### Velocity Decay Analysis

Track velocity trend over time using exponential smoothing:

```
Smoothed_Velocity_t = α × Actual_Velocity_t + (1-α) × Smoothed_Velocity_(t-1)
Velocity_Trend = Smoothed_Velocity_t - Smoothed_Velocity_(t-4)  [4-week trend]
```

Accelerating decay (velocity dropping faster) = urgent action needed. Stabilizing velocity after markdown = markdown was effective but watch for further decay.

## Examples

**Example 1 — Fast Mover Stockout Prevention**
> "Winter Jacket SKU-2201 launched 4 weeks ago with velocity index of 185 (85% above plan). Cumulative sell-through is 68% with only 340 units remaining. At current velocity, stockout in 9 days. Supplier lead time is 21 days (ocean). Recommendation: Place 2,000-unit reorder via air freight. Air premium is $3,200; projected lost margin from stockout is $28,000 over the remaining 6 weeks of the winter season. ROI on air freight: 775%. Action: Approved expedite."

**Example 2 — Slow Mover Markdown Optimization**
> "Sweater SKU-1855 has velocity index of 42 after 8 weeks in market. Cumulative sell-through is 18% vs. 55% benchmark. 4,200 units remain valued at $126,000. Root cause analysis: 3 competing styles from brand X launched at 15% lower price. Without intervention, projected end-of-season sell-through is 30%, generating $45,000 in markdown losses. Recommended: immediate 25% markdown projected to lift velocity 2.5×, improving end-of-season sell-through to 55% and recovering $73,500 in margin vs. delayed clearance scenario."

## Guidelines

1. Calculate sell-through using receipt-based denominators (BOH + receipts), not current inventory
2. Track velocity daily for new launches in first 4 weeks — early signal is critical for reorder decisions
3. Normalize velocity for out-of-stock days — a product with 50% in-stock rate has understated velocity
4. Compare sell-through within like groups (same category, same price tier, same season) for meaningful benchmarks
5. For fashion/seasonal products, the sell-through clock starts at season start, not receipt date
6. Factor in planned markdowns when projecting forward sell-through — full-price velocity differs from markdown velocity
7. Use GMROI, not sell-through alone, to make keep/markdown/exit decisions — a slow seller with very high margins may be worth keeping
8. Track cannibalization — a new SKU's velocity may come at the expense of existing SKU velocity
9. Integrate velocity data with open-to-buy decisions — shift future budget from slow categories to fast ones

## Validation Checklist

- [ ] Sales data excludes returns (net sales, not gross)
- [ ] Beginning inventory is accurate (reconciled with physical counts or WMS)
- [ ] Receipts include all inventory additions (POs, transfers in, return-to-stock)
- [ ] Seasonal curves are updated for current year trends, not just prior year replication
- [ ] Benchmarks are category-appropriate (don't compare fashion apparel to basic replenishment)
- [ ] Velocity index calculations handle zero-inventory periods (exclude from denominator)
- [ ] Markdown recommendations account for markdown budget and approval workflows
- [ ] Fast-mover reorder recommendations confirm supplier capacity and lead time feasibility
- [ ] Financial projections use current margin rates, including any cost changes
- [ ] Lifecycle stage assignments are current and accurate for each SKU
