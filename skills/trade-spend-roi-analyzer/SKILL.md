---
name: trade-spend-roi-analyzer
description: Analyze and explain trade spend impact, ROI, and effectiveness across CPG promotional programs and retailer investments. Use when evaluating trade promotion ROI, optimizing trade budgets, analyzing promotional lift, or preparing trade spend reviews for finance and sales leadership.

metadata:
  display_name: "Trade Spend Roi Analyzer"
  short_description: "Analyze CPG trade spend ROI and promotional effectiveness"
  default_prompt: "Analyze my trade spend roi and recommend clear next actions"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Trade Spend ROI Analyzer

## Overview

Provide rigorous analysis of trade spend effectiveness across promotional programs, retailer investments, and trade term structures. This skill decomposes trade spend into its component drivers, calculates true incremental ROI, identifies waste and optimization opportunities, and translates findings into actionable recommendations for finance and sales audiences.

## When to Use

- Quarterly or annual trade spend effectiveness reviews
- Promotional post-event analysis (PEA)
- Trade budget planning and allocation
- Trade spend optimization initiatives
- CFO/Finance deep-dives on commercial investment returns
- Evaluating trade spend vs. brand investment trade-offs

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Trade spend detail | Spend by type (OI, scan, MDF, slotting, display, BOGO) | $ by event/retailer/brand |
| Baseline sales | Non-promoted baseline velocity by SKU/retailer | Units per store per week |
| Promoted sales | Actual sales during promotional periods | Units per store per week |
| Revenue and COGS | Net revenue and COGS by SKU | $ per unit |
| Event calendar | Promotional events with dates, mechanics, depth | Event log |
| Retailer/channel detail | Which retailer, channel, region | Categorization |
| Volume decomposition | If available: base, incremental, pantry loading, cannibalization | Units breakdown |

## Methodology

### Step 1: Trade Spend Taxonomy

Classify all trade spend into standardized buckets:

| Category | Type | Examples | Visibility |
|----------|------|----------|-----------|
| Performance-based | Variable | Scan allowances, volume rebates, BOGO funding | Tied to sell-through |
| Fixed/Structural | Fixed | Slotting fees, annual MDF, JBP commitments | Not tied to performance |
| Display/Merch | Semi-variable | Display allowances, endcap fees, shipper programs | Conditional on execution |
| Price Reduction | Variable | TPR funding, coupon reimbursement | Direct to consumer |
| Other | Variable | Freight allowances, new item fees, data fees | Administrative |

Compute trade spend rate: `Trade Spend % = Total Trade Spend / Gross Revenue`

Benchmark: Average CPG trade spend is 20-25% of gross revenue. Flag deviations >3pp from benchmark.

### Step 2: Incremental Volume Isolation

Separate promoted volume into components:

```
Total Promoted Volume
├── Base Volume (would have sold without promotion)
├── Incremental Volume
│   ├── Category Expansion (net new consumption)
│   ├── Brand Switching (taken from competitors)
│   ├── Channel Shifting (moved from other retailers)
│   └── Pantry Loading (pull-forward from future periods)
└── Post-Promo Dip (negative volume in weeks following promo)
```

True incremental = Category Expansion + Brand Switching only. Channel shifting and pantry loading are value-destructive at the portfolio level.

**Calculation method (if decomposition not provided):**
```
Incremental Units = Promoted Units − (Baseline Units × Promo Weeks)
Post-Promo Dip = Avg Units (2 weeks post-promo) − Baseline Units
Adjusted Incremental = Incremental Units + Post-Promo Dip (negative)
```

### Step 3: ROI Calculation Framework

Calculate three levels of ROI:

**Level 1 — Gross ROI (simplistic):**
```
Gross ROI = Incremental Revenue / Trade Spend
```

**Level 2 — Net ROI (margin-adjusted):**
```
Incremental Profit = Incremental Units × (ASP − COGS)
Net ROI = Incremental Profit / Trade Spend
Breakeven: Net ROI = 1.0x
Healthy: Net ROI > 1.5x
```

**Level 3 — True Economic ROI (comprehensive):**
```
True Incremental Profit = Adjusted Incremental Units × Contribution Margin
                        − Cannibalization Loss (own portfolio)
                        − Post-Promo Dip Loss
                        − Execution Cost (in-store, broker, creative)
True ROI = True Incremental Profit / Total Promotion Investment
```

### Step 4: Promotional Effectiveness Scoring

Score each promotion/event on a standardized framework:

| Metric | Weight | Scoring |
|--------|--------|---------|
| Lift % (promoted vs baseline) | 25% | 1=<20%; 3=20-80%; 5=>80% |
| True ROI (Level 3) | 30% | 1=<0.5x; 3=0.5-1.5x; 5=>1.5x |
| Duration efficiency (lift per promo day) | 15% | Relative ranking within portfolio |
| Post-promo dip severity | 15% | 1=>30% dip; 3=10-30%; 5=<10% |
| Execution compliance | 15% | % of stores executing correctly |

Composite Score = Weighted average (1-5 scale)

### Step 5: Portfolio-Level Optimization

Analyze trade spend allocation efficiency:

**Spend Curve Analysis**: Plot incremental revenue per trade dollar across all events. Rank from most to least efficient. Identify the "efficiency frontier" — the optimal allocation that maximizes total incremental revenue for a given budget.

**Reallocation Opportunity:**
```
Bottom quartile events (lowest ROI): $X spend generating $Y incremental revenue
If reallocated to top quartile mechanics: Estimated additional $Z incremental revenue
Net improvement: $Z − $Y = Optimization opportunity
```

### Step 6: Waterfall Decomposition

Present trade spend impact as a P&L waterfall:

```
Gross Revenue                    $XXX
  − Trade Spend (total)          ($XX)
    − Performance-based          ($X)
    − Fixed/Structural           ($X)
    − Display/Merch              ($X)
    − Price Reduction            ($X)
  = Net Revenue                  $XX
  − COGS                        ($XX)
  = Gross Profit                 $XX
  Trade Spend as % of Gross:     XX.X%
  Incremental Revenue per $1:    $X.XX
```

## Output Specification

```markdown
# Trade Spend ROI Analysis — [Period] [Scope]

## Executive Summary
[Key finding: overall ROI, top/bottom performers, optimization opportunity size]

## Trade Spend Overview
| Metric | Current Period | Prior Period | YoY Change |
|--------|---------------|-------------|------------|
| Total Trade Spend | $XM | $XM | +X% |
| Trade Rate (% of Gross) | XX.X% | XX.X% | +/-Xbps |
| Overall Net ROI | X.Xx | X.Xx | +/-X.Xx |

## P&L Waterfall Impact
[Visual waterfall: Gross Revenue → Trade Spend components → Net Revenue]

## Event-Level Performance
| Event/Program | Spend | Lift % | Net ROI | Score | Recommendation |
|--------------|-------|--------|---------|-------|----------------|
| [Best event] | $XK | XX% | X.Xx | 4.5 | Scale |
| [Worst event] | $XK | XX% | X.Xx | 1.2 | Eliminate |

## Optimization Recommendations
1. [Reallocation opportunity with $ impact]
2. [Mechanic change recommendation with expected ROI improvement]
3. [Structural term renegotiation opportunity]

## Retailer-Level Analysis
[Trade ROI by retailer with benchmarks]

## Appendix: Methodology Notes
[Baseline methodology, data sources, key assumptions]
```

## Analysis Framework

**Contribution Margin Bridge for Trade Spend:**
```
Baseline Contribution Margin          $X.XX per unit
+ Incremental volume contribution     $X.XX
− Trade spend cost                    ($X.XX)
− Cannibalization                     ($X.XX)
− Post-promo dip                      ($X.XX)
= Net Promotional Contribution        $X.XX per unit
```

## Example

**Input**: "BOGO promotion at Target: 2-week event, $150K spend. Baseline 50 units/store/week across 1,900 stores. Promoted volume was 180 units/store/week. Post-promo dip was 35 units/store/week for 1 week. ASP $4.99, COGS $2.10."

**Analysis output**:
> "The Target BOGO generated a 260% lift (180 vs 50 baseline units/store/week), producing 494K incremental units over 2 weeks. However, the post-promo dip of 28.5K units (35 vs 50 baseline × 1,900 stores × 1 week) reduces adjusted incremental to 465.5K units. At $4.99 ASP and $2.10 COGS, the BOGO effectively sells at $2.50 (50% discount), generating $0.40/unit margin vs $2.89 at full price. **Net ROI = 0.62x** — below the 1.0x breakeven threshold. Recommendation: Convert to a $1-off TPR (yielding $1.89/unit margin) at reduced depth. Modeling suggests a TPR at $3.99 would generate ~60% lift with 1.8x Net ROI, improving total promotional profit by $95K."

## Guidelines

- Always calculate Level 3 (True Economic) ROI — Level 1 overstates performance
- Include post-promo dip in every analysis — omitting it inflates incrementality by 10-25%
- Benchmark trade rates by channel: Grocery 22-28%, Club 8-12%, DTC 3-8%
- Separate fixed/structural trade costs from performance-based in all ROI calculations
- Flag any promotion with Net ROI <1.0x as value-destructive
- Recommend reallocation, not just elimination — budget neutrality is realistic

## Validation Checklist

- [ ] Trade spend classified into standardized taxonomy
- [ ] Baseline volume methodology documented
- [ ] Incremental volume decomposed (expansion, switching, loading, dip)
- [ ] Three levels of ROI calculated (Gross, Net, True Economic)
- [ ] Event-level scoring applied with composite scores
- [ ] Portfolio optimization analysis with reallocation quantified
- [ ] P&L waterfall shows trade spend impact on margins
- [ ] Recommendations are actionable with quantified expected impact
- [ ] All data sources and assumptions documented
