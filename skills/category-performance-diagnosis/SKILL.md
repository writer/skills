---
name: category-performance-diagnosis
description: >
  Performs deep diagnostic analysis on a retail or e-commerce product category to identify root causes of
  performance changes—growth, decline, or stagnation. Use when the user asks why a category is underperforming,
  wants to decompose category growth drivers, or needs a structured performance review. Triggers on requests
  mentioning category review, category deep-dive, performance diagnosis, growth decomposition, or category health.

metadata:
  display_name: "Category Performance Diagnosis"
  short_description: "Diagnose retail category performance drivers and changes"
  default_prompt: "Analyze my category performance diagnosis and recommend clear next actions"
  version: "1.0.0"
  tags:
    - commerce-intelligence
    - category-performance-diagnosis
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Category Performance Diagnosis

## Overview

Category Performance Diagnosis provides a structured, root-cause-driven analysis of why a product category is performing the way it is. Rather than simply reporting metrics, this skill decomposes performance into its component drivers—traffic, conversion, basket, price, mix, distribution—and isolates the factors most responsible for observed changes. The output is an actionable diagnostic narrative with prioritized levers for improvement.

This methodology mirrors how leading CPG companies (P&G, Unilever, PepsiCo) conduct category reviews with retail partners, combining the rigor of a consulting-style decomposition with the specificity of CPG domain expertise.

## When to Use

- Quarterly or annual category business review preparation
- A category shows unexpected decline or acceleration and the user asks "why"
- Cross-category portfolio prioritization requiring standardized health assessments
- Retailer-supplier joint business planning sessions
- Post-event analysis (e.g., after a major promotion, competitor launch, or assortment reset)
- User provides category sales data and asks for a performance diagnosis

## Required Inputs

| Input | Required | Description |
|---|---|---|
| Category sales data | Yes | Revenue, units, transactions — minimum 52 weeks, ideally 104 weeks for YoY |
| Time granularity | Yes | Weekly or monthly data; weekly preferred for decomposition |
| Product hierarchy | Yes | Category > subcategory > brand > SKU with attributes |
| Traffic/visit data | Recommended | Store visits, site sessions, category page views |
| Basket/transaction data | Recommended | Items per basket, basket size, attach rates |
| Pricing data | Recommended | Regular and promoted prices, price indices |
| Distribution data | Recommended | Store count, %ACV, online availability rate |
| Market/syndicated data | Optional | Nielsen/Circana total market data for share context |
| Competitor data | Optional | Competitor pricing, promotions, launches |

## Methodology

### Step 1: Establish the Performance Fact Base

Calculate core category KPIs for current period vs. year-ago and vs. plan/budget:

| Metric | Current | YoY Change | vs. Plan |
|---|---|---|---|
| Revenue | — | — | — |
| Units | — | — | — |
| Transactions | — | — | — |
| Average Selling Price (ASP) | — | — | — |
| Units per Transaction (UPT) | — | — | — |
| Revenue per Transaction (RPT) | — | — | — |
| Gross Margin % | — | — | — |
| Gross Margin $ | — | — | — |

### Step 2: Revenue Growth Decomposition

Decompose total revenue change into additive components using the standard retail growth bridge:

```
ΔRevenue = ΔTraffic Effect + ΔConversion Effect + ΔBasket Effect + ΔPrice/Mix Effect
```

**Traffic Effect**: Change in total visits/sessions × prior-period conversion × prior-period RPT
**Conversion Effect**: Prior traffic × change in conversion × prior-period RPT
**Basket Effect**: Prior traffic × current conversion × change in items/basket × prior ASP
**Price/Mix Effect**: Prior traffic × current conversion × current items/basket × change in ASP

For each component, express as:
- Absolute dollar contribution to the total change
- Percentage of total change explained
- Trend direction (improving, stable, deteriorating)

### Step 3: Price/Mix Disaggregation

Further decompose the Price/Mix effect:

```
ΔPrice/Mix = Pure Price Effect + Trade-Up/Down Mix Effect + Size Mix Effect + Channel Mix Effect
```

- **Pure Price Effect**: Same-SKU price changes (regular price increases, cost-driven)
- **Trade-Up/Down Mix**: Shift in revenue share between premium, mid, and value tiers
- **Size Mix**: Shift between single-serve, standard, and bulk sizes
- **Channel Mix**: Shift between online, in-store, marketplace (different ASP profiles)

### Step 4: Subcategory and Brand Waterfall

Identify which subcategories and brands are driving the overall category trend:

1. Rank subcategories by absolute contribution to category ΔRevenue
2. For the top 3 growth and top 3 decline contributors, repeat the growth decomposition (Step 2)
3. Identify share-shifting dynamics: which brands are gaining at whose expense
4. Calculate **Growth Contribution Index**: (Brand's contribution to category growth / Brand's revenue share). Values > 1.0 indicate disproportionate growth contribution.

### Step 5: Identify Root Cause Hypotheses

Map decomposition findings to root causes using this diagnostic framework:

| Observed Signal | Likely Root Causes | Diagnostic Action |
|---|---|---|
| Traffic declining, conversion stable | Category relevance issue, reduced marketing, seasonal shift | Check media spend, category search volume trends |
| Traffic stable, conversion declining | Assortment issues, price competitiveness, UX friction | Analyze search-to-cart rate, price index vs. competition |
| Conversion up, basket declining | Promo-driven traffic (cherry-picking), stock issues | Check promo depth/frequency, OOS rates |
| ASP declining, units flat | Trade-down, promo depth increase, channel mix shift | Analyze tier mix trends, promo analysis |
| ASP rising, units declining | Price resistance, elasticity threshold crossed | Run price elasticity check, competitive price audit |

### Step 6: Prioritize Improvement Levers

For each root cause identified, define an improvement lever and size the opportunity:

```
Lever Impact = Current Gap × Recovery Rate × Confidence Factor
```

Where:
- **Current Gap**: Measured shortfall vs. benchmark, prior period, or plan
- **Recovery Rate**: Realistic % of gap that can be recovered (typically 30–60%)
- **Confidence Factor**: 0.5–1.0 based on data quality and certainty of root cause

## Output Specification

### 1. Category Health Scorecard

One-page summary with traffic-light indicators (green/yellow/red) for:
- Revenue trend, Unit trend, Margin trend
- Traffic, Conversion, Basket size
- Price competitiveness, Assortment coverage
- Overall Category Health Rating (A/B/C/D)

### 2. Growth Decomposition Bridge

Waterfall chart (or table) showing additive contribution of each growth driver to total ΔRevenue.

### 3. Root Cause Narrative

Structured narrative (3–5 paragraphs) explaining: What happened → Why it happened → What matters most → What to do about it.

### 4. Subcategory/Brand Contribution Matrix

Table showing each subcategory's contribution to category growth with Growth Contribution Index.

### 5. Prioritized Action Plan

| Priority | Lever | Root Cause | Expected Impact | Timeline | Owner |
|---|---|---|---|---|---|
| 1 | — | — | — | — | — |

## Analysis Framework

### Key Performance Indicators

- **Revenue Growth Rate**: Current vs. YoY, vs. market, vs. plan
- **Volume/Price Decomposition**: % of growth from volume vs. price
- **Category Development Index (CDI)**: Category performance in a market vs. national average (index 100)
- **Brand Development Index (BDI)**: Brand performance in a market vs. national average
- **Share of Wallet**: Category spend as % of total department or basket
- **Promotion Intensity**: % of volume sold on promotion (healthy range: 25–40% for CPG)
- **Everyday Margin Rate**: Gross margin excluding promotional markdowns
- **Inventory Turns**: Annual COGS / average inventory (benchmark varies by category: 8–15 for center store, 20–50 for perishables)

### Diagnostic Benchmarks

- Healthy category grows at ≥ market rate ± 1pp
- Conversion rate decline > 2pp warrants urgent investigation
- If > 50% of growth comes from price, sustainability is at risk
- Promo-driven volume exceeding 45% of total signals promotional dependency
- Top brand gaining > 3pp share in 12 months signals competitive disruption

## Examples

**Input**: "Our Beverages category did $48M last year, down 3.2% vs. prior year. We have weekly POS data for 52 weeks, 280 SKUs across carbonated, water, juice, energy, and tea subcategories. Help me understand what's driving the decline."

**Output**:
1. **Health Scorecard**: Overall grade C — Revenue declining, units declining faster (−5.1%), ASP up +2.0% masking volume weakness. Traffic yellow, conversion red.
2. **Growth Bridge**: Traffic (−$0.4M) + Conversion (−$1.1M) + Basket (−$0.3M) + Price/Mix (+$0.2M) = −$1.6M total decline
3. **Root Cause**: Conversion is the primary drag. Deep dive reveals: (a) Carbonated soft drinks lost 12% of units due to out-of-stocks on the #2 and #3 brands during a supplier disruption (Q2); (b) Juice subcategory declined $0.6M as consumers shifted to flavored water, which is under-assorted (only 8 SKUs vs. 22 at key competitor); (c) Energy subcategory grew +14% but doesn't offset core declines.
4. **Action Plan**: P1 — Fix CSD supply chain ($0.8M recovery). P2 — Expand flavored water assortment by 10 SKUs ($0.5M). P3 — Increase energy shelf space to match growth trajectory ($0.3M).

## Guidelines

- Always decompose before diagnosing — resist jumping to conclusions from headline numbers
- Present the "so what" after every data point; diagnosis without interpretation is not useful
- Distinguish between cyclical effects (weather, seasonality) and structural shifts (consumer behavior change)
- Compare category performance to total market growth, not just prior period — a category growing 2% in a market growing 6% is underperforming
- Account for calendar shifts (Easter timing, extra/fewer selling days) in YoY comparisons
- If promotional volume is high, separate base volume trends from promoted volume trends
- Flag data quality issues explicitly rather than drawing conclusions from unreliable inputs
- Consider external macro factors: inflation, consumer confidence, demographic shifts
- The diagnosis should tell a story, not just present numbers — lead with the narrative

## Validation Checklist

- [ ] Growth bridge components sum to total ΔRevenue (within rounding tolerance)
- [ ] Both volume and value decompositions are presented
- [ ] Year-over-year and vs.-plan comparisons are included
- [ ] At least 3 subcategories are analyzed in detail
- [ ] Root causes are supported by data, not assumptions
- [ ] External/market context is referenced (market growth rate, share trends)
- [ ] Recommendations are sized with estimated revenue impact
- [ ] Promotional vs. base volume trends are separated
- [ ] Seasonal and calendar effects are accounted for
- [ ] The narrative answers "What happened? Why? What now?"
