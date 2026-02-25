---
name: competitive-price-monitoring
description: >
  Systematically tracks, compares, and analyzes competitor pricing across products, channels, and time periods
  to identify competitive positioning gaps, pricing threats, and opportunities. Use when the user wants to
  benchmark prices against competitors, monitor price changes, assess price image, or detect competitive
  pricing moves. Triggers on requests about competitor pricing, price benchmarking, price index, price image,
  competitive intelligence, or price monitoring.

metadata:
  display_name: "Competitive Price Monitoring"
  short_description: "Monitor competitor pricing gaps, threats, and moves"
  default_prompt: "Review my competitive price and highlight top risks and next actions"
  version: "1.0.0"
  tags:
    - commerce-intelligence
    - competitive-price-monitoring
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Competitive Price Monitoring

## Overview

Competitive Price Monitoring provides a structured framework for tracking and analyzing competitor prices to inform pricing strategy, protect price image, and identify threats and opportunities. This skill goes beyond simple price comparison to deliver strategic intelligence: trend analysis, price positioning maps, competitive response patterns, and actionable recommendations.

In CPG retail, price perception drives 20–40% of store-choice decisions. A retailer whose price index drifts 3–5% above key competitors risks losing traffic and basket share. Conversely, unnecessarily low prices leave margin on the table. This skill enables precision price positioning.

## When to Use

- Regular (weekly/monthly) competitive price benchmarking
- Before or after own price changes to assess competitive context
- When market share shifts suggest competitive pricing pressure
- Retailer negotiation prep requiring competitive price data
- E-commerce dynamic pricing response strategy
- Private label pricing calibration vs. national brand and competitor PL
- User asks to compare prices against specific competitors

## Required Inputs

| Input | Required | Description |
|---|---|---|
| Own product prices | Yes | Current regular and promoted prices by SKU |
| Competitor prices | Yes | Matched competitor prices (scraped, syndicated, or manually collected) |
| Product matching | Yes | UPC-level or attribute-level matching between own and competitor items |
| Time series | Recommended | Price history for trend analysis (minimum 12 weeks, ideally 52) |
| Category hierarchy | Recommended | Category, subcategory, segment for rolled-up analysis |
| Sales volume data | Optional | To weight price indices by revenue importance |
| Cost data | Optional | To assess margin implications of competitive pricing |

## Methodology

### Step 1: Product Matching and Basket Construction

1. **Exact match**: Match identical UPCs/GTINs across retailers
2. **Equivalent match**: Match products by brand + size + variant where UPCs differ (e.g., retailer-specific packaging)
3. **Attribute match**: For private label, match by category + size + key attributes (organic, etc.)
4. **Construct Key Value Item (KVI) basket**: Identify the 100–300 most price-sensitive items that disproportionately shape consumer price perception. KVIs typically represent 10–15% of SKUs but drive 40–60% of price image.

**KVI Identification Criteria**:
- High purchase frequency (top 20% of basket penetration)
- High price awareness (items consumers price-check: milk, eggs, bananas, diapers, cola)
- High cross-shop rate (items bought at multiple retailers)
- Category traffic drivers

### Step 2: Price Index Calculation

Compute price indices at multiple levels:

**Item-Level Price Index**:
```
Price Index_item = (Own Price / Competitor Price) × 100
```
- Index 100 = price parity
- Index < 100 = cheaper than competitor
- Index > 100 = more expensive than competitor

**Category-Level Price Index** (revenue-weighted):
```
Category PI = Σ(Price Index_item × Item Revenue Weight) / Σ(Revenue Weights)
```

**Overall Price Index** (basket-level):
```
Basket PI = Σ(Own Price_i × Quantity_i) / Σ(Competitor Price_i × Quantity_i) × 100
```

**KVI Price Index**: Same as basket PI but limited to KVI items only — this is the most actionable metric for price image.

### Step 3: Price Position Mapping

Create a price-position matrix:

| | Competitor Cheaper | Price Parity (±2%) | Own Cheaper |
|---|---|---|---|
| **KVI Items** | CRITICAL — fix immediately | Maintain | Evaluate margin opportunity |
| **Secondary Items** | Monitor trend | Acceptable | Possible price increase |
| **Long Tail** | Low priority | Low priority | Increase price if margin-negative |

### Step 4: Competitive Price Movement Detection

Track price changes over time to detect competitive strategies:

1. **Change frequency**: How often does each competitor adjust prices? (Weekly, monthly, seasonal)
2. **Change magnitude**: Average size of price moves (benchmark: 2–5% in CPG)
3. **Directional trend**: Net price movement direction over trailing 12 weeks
4. **Promotional patterns**: Promo depth, frequency, and duration by competitor
5. **Leader-follower dynamics**: Which competitor moves first; how quickly do others follow

**Price Velocity Score**:
```
PVS = (# Price Changes in Period / # Items Monitored) × (Avg % Change Magnitude)
```
High PVS indicates an actively managing/aggressive competitor.

### Step 5: Price Gap Analysis

For each category, compute the price gap distribution:

```
Price Gap = Own Price − Competitor Price (in $ and %)
```

Analyze the distribution:
- **Mean gap**: Overall positioning
- **Median gap**: Central tendency (less sensitive to outliers)
- **Gap dispersion (std dev)**: Consistency of positioning
- **Skewness**: Are gaps systematically positive (more expensive) or negative (cheaper)?
- **% of items within ±3% parity**: Measure of overall alignment

### Step 6: Strategic Recommendations

Classify items into pricing action buckets:

| Action | Criteria | Typical Volume |
|---|---|---|
| **Price Decrease** | KVI items > 5% above competitor, high elasticity | 5–10% of items |
| **Price Increase** | Items > 10% below competitor, low elasticity, no strategic role | 5–15% of items |
| **Maintain** | Within ±3% of competitor, appropriate positioning | 60–70% of items |
| **Investigate** | Large gaps with unclear strategic rationale | 10–15% of items |
| **Promotional Response** | Competitor running deep promos in key categories | Variable |

## Output Specification

### 1. Executive Price Index Summary

| Metric | vs. Competitor A | vs. Competitor B | vs. Competitor C |
|---|---|---|---|
| Overall Price Index | — | — | — |
| KVI Price Index | — | — | — |
| Private Label PI | — | — | — |
| Promo Price Index | — | — | — |

### 2. Category-Level Price Index Table

Table showing price index by category for each competitor, color-coded (green < 98, yellow 98–102, red > 102).

### 3. Price Movement Alert Report

Items with significant competitive price changes in the monitoring period, ranked by strategic importance.

### 4. Price Position Map

Scatter plot (or table) with own price on Y-axis, competitor price on X-axis, sized by revenue. Items above the diagonal are more expensive; below are cheaper.

### 5. Action Item List

Specific SKU-level pricing recommendations with expected revenue/margin impact.

## Analysis Framework

### Key Metrics

- **Price Index (PI)**: Core positioning metric (target varies by retailer strategy: EDLP aims for 97–100 vs. market)
- **KVI Price Index**: Most important for price image; should be at or below target PI
- **Price Image Score**: Consumer-perceived pricing derived from KVI PI (correlated r=0.7+ with KVI PI)
- **Gap Closure Rate**: % of identified gaps actioned within one review cycle
- **Price Change Velocity**: Frequency and magnitude of competitive price changes
- **Promo Price Index**: Average promoted price vs. competitor promoted price
- **Everyday Price Index**: Regular (non-promoted) price comparison
- **Private Label Price Ratio**: PL price / national brand price (benchmark: 20–35% discount)

### Strategic Pricing Benchmarks

| Retailer Strategy | Target PI vs. Market | KVI PI Target | Promo Intensity |
|---|---|---|---|
| EDLP (Walmart model) | 95–98 | 93–96 | Low (< 15% of volume) |
| Hi-Lo (traditional grocery) | 100–105 regular | 95–100 promo | High (30–45% of volume) |
| Premium (Whole Foods model) | 110–125 | 105–115 | Low-Medium |
| Value/Discount (Aldi model) | 80–90 | 80–85 | Very Low |

## Examples

**Input**: "Compare our pricing in the Dairy category against Kroger and Walmart. We have 180 matched items with weekly price data for the last 26 weeks."

**Output**:
1. **Overall Dairy PI**: vs. Walmart 104.2 (4.2% more expensive), vs. Kroger 99.1 (at parity)
2. **KVI PI (top 30 items)**: vs. Walmart 106.8 (critical — we are 6.8% above Walmart on the most price-sensitive dairy items), vs. Kroger 100.3 (parity)
3. **Biggest gaps vs. Walmart**: Gallon milk (+$0.42, PI 112), Large eggs (+$0.35, PI 109), Butter 1lb (+$0.28, PI 107) — all KVIs
4. **Trend**: Walmart reduced dairy prices on 14 items in the last 4 weeks (PVS rising), likely a price investment play. Our gap has widened from PI 102 to 104 in 6 weeks.
5. **Recommendations**: (a) Invest in 12 KVI items to close gap to PI ≤ 100 vs. Walmart — estimated cost $180K/year in margin, but protects estimated $2.4M in at-risk dairy revenue. (b) Increase prices on 8 specialty dairy items where we are 15%+ below Kroger — margin recovery $95K/year.

## Guidelines

- Always weight price indices by revenue or volume; unweighted indices are misleading because they treat a $1 spice the same as a $5 milk
- Separate everyday and promotional price comparisons — a retailer can be expensive everyday but cheap on promo, creating a different price perception
- Match products carefully; incorrect matching invalidates the entire analysis. Verify matching logic with the user.
- KVI identification is critical — focus price investments on the items that consumers actually notice and compare
- Monitor trends, not just snapshots — a competitor that has made 10 consecutive weekly price decreases is signaling a strategy shift
- Consider channel context: online prices may differ from in-store; compare like-for-like
- Account for private label substitution effects; national brand price gaps matter less if the consumer's real alternative is the store brand
- Don't recommend matching every competitor on every item — that leads to a race to the bottom. Be surgical.
- Factor in basket economics: sometimes being 5% higher on commodity items is sustainable if the total basket value proposition is strong

## Validation Checklist

- [ ] Product matching is verified (exact UPC or validated equivalent match)
- [ ] Price indices are revenue-weighted (not simple averages)
- [ ] KVI basket is explicitly defined and KVI-specific PI is calculated
- [ ] Both regular and promotional prices are analyzed separately
- [ ] Time trends are included (not just a point-in-time snapshot)
- [ ] Price indices are calculated vs. at least 2 competitors
- [ ] Recommendations are prioritized by strategic impact (KVIs first)
- [ ] Margin impact of pricing actions is estimated
- [ ] Data recency is verified (stale competitive data misleads)
- [ ] Channel-specific considerations are noted (online vs. in-store)
