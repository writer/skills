---
name: price-elasticity-estimator
description: >
  Estimates price elasticity of demand for retail/CPG products using historical sales and pricing data to
  quantify the expected volume impact of price changes. Use when the user wants to understand price sensitivity,
  model price change scenarios, optimize pricing, or evaluate the revenue/margin trade-off of price adjustments.
  Triggers on requests about price elasticity, price sensitivity, demand curves, pricing optimization, or
  price-volume trade-offs.

metadata:
  display_name: "Price Elasticity Estimator"
  short_description: "Estimate price elasticity and volume impact of changes"
  default_prompt: "Optimize my price elasticity estimator and suggest the best next steps"
  version: "1.0.0"
  tags:
    - commerce-intelligence
    - price-elasticity-estimator
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Price Elasticity Estimator

## Overview

Price Elasticity Estimator quantifies the relationship between price changes and demand response for CPG and retail products. It computes own-price elasticity coefficients, models cross-price effects, and simulates the revenue and margin impact of proposed price changes. This enables data-driven pricing decisions that balance volume, revenue, and margin objectives.

Price elasticity is the single most important input to pricing strategy. A product with elasticity of −2.0 will lose 10% of volume for every 5% price increase; knowing this allows precise trade-off analysis. In CPG, typical own-price elasticities range from −1.5 to −3.5, varying significantly by category, brand equity, competitive set, and channel.

## When to Use

- Evaluating the impact of a proposed price increase or decrease
- Annual pricing review or cost-driven price adjustment planning
- Competitive response analysis — "if competitor drops price by 10%, what happens to our volume?"
- Promotion depth optimization — determining optimal temporary price reduction
- Private label pricing strategy relative to national brands
- Building pricing architecture (good/better/best tiering)
- User provides historical price and volume data and asks about price sensitivity

## Required Inputs

| Input | Required | Description |
|---|---|---|
| Historical price & volume data | Yes | Weekly or monthly price points and corresponding unit sales; minimum 52 weeks, ideally 104+ weeks |
| SKU/product attributes | Yes | Brand, size, segment, price tier classification |
| Promotion flags | Recommended | Indicator of when prices reflect temporary promotions vs. EDLP |
| Competitor pricing | Recommended | Price points for key competitive SKUs over the same period |
| Distribution data | Recommended | Store count or %ACV to normalize volume (units/store/week) |
| Cost data | Optional | COGS or landed cost per unit for margin analysis |
| Seasonality indicators | Optional | Season or holiday flags to control for demand fluctuations |

## Methodology

### Step 1: Data Preparation

1. **Normalize volume**: Convert raw units to units per store per week (or per thousand site visits for e-commerce) to remove distribution effects
2. **Identify price variation**: Catalog all price points observed; flag regular price vs. promoted price
3. **Remove outliers**: Exclude weeks with stockouts, extreme events (pandemic, recalls), or data errors
4. **Create log transformations**: ln(Price) and ln(Volume) for log-log regression (constant elasticity model)
5. **Construct control variables**: seasonality dummies, trend variable, holiday flags, competitor price indices

### Step 2: Elasticity Estimation

Apply the log-log demand model:

```
ln(Q_it) = α + β₁·ln(P_it) + β₂·ln(P_competitor_t) + β₃·Promo_it + β₄·Season_t + β₅·Trend_t + ε_it
```

Where:
- **β₁** = Own-price elasticity (expected: negative, typically −1.5 to −3.5)
- **β₂** = Cross-price elasticity (expected: positive for substitutes)
- **β₃** = Promotion lift coefficient
- **Q_it** = Units per point of distribution for product i in period t
- **P_it** = Price of product i in period t

**Estimation methods** (in order of preference):
1. **OLS with controls**: Adequate when price variation is exogenous (e.g., cost-driven changes)
2. **Two-stage least squares (2SLS/IV)**: Use commodity cost indices as instruments when price is endogenous
3. **Difference-in-differences**: When a price change occurs at a specific date, compare treated vs. control stores/products
4. **Bayesian hierarchical model**: For estimating elasticities across many SKUs with limited data per SKU

### Step 3: Elasticity Segmentation

Group products by elasticity profile:

| Elasticity Range | Classification | Typical Products | Pricing Implication |
|---|---|---|---|
| 0 to −1.0 | Inelastic | Staples, baby formula, pet food, addictive categories | Price increases recover margin with limited volume loss |
| −1.0 to −2.0 | Moderate | Most center-store CPG, branded household products | Careful trade-off analysis needed; brand equity matters |
| −2.0 to −3.0 | Elastic | Commoditized categories, snacks, beverages, private label | Price increases risk significant volume loss |
| < −3.0 | Highly Elastic | Price-comparison categories, undifferentiated products | Compete on value; price increases very risky |

### Step 4: Scenario Simulation

For each proposed price change, compute expected outcomes:

```
% ΔVolume = Elasticity × % ΔPrice
New Volume = Current Volume × (1 + % ΔVolume)
New Revenue = New Volume × New Price
ΔRevenue = New Revenue − Current Revenue
ΔMargin = (New Price − Cost) × New Volume − (Current Price − Cost) × Current Volume
```

**Optimal price** (margin-maximizing):
```
P* = Cost × (ε / (1 + ε))
```
Where ε is own-price elasticity (negative value). This formula yields the theoretical margin-maximizing price assuming constant elasticity.

**Revenue-maximizing price**:
```
P_rev* = P_current / (1 + 1/ε)
```

### Step 5: Cross-Price and Cannibalization Effects

For products within a portfolio, estimate cross-price elasticities to understand:

- **Substitution effects**: If Brand A raises price, how much volume shifts to Brand B
- **Category expansion/contraction**: Does the price change grow or shrink total category volume
- **Private label cross-elasticity**: Measure PL volume response to national brand price changes (typically 0.1–0.5)

```
Cross-Elasticity_AB = % ΔVolume_B / % ΔPrice_A
```
Positive values indicate substitutes; negative values indicate complements.

### Step 6: Confidence and Sensitivity Analysis

Report confidence intervals around elasticity estimates and simulate across the range:

- **95% confidence interval** for the elasticity coefficient
- **Optimistic scenario**: Use lower-bound elasticity (less elastic)
- **Base scenario**: Use point estimate
- **Pessimistic scenario**: Use upper-bound elasticity (more elastic)
- **Break-even price change**: The price increase at which margin gain equals zero

## Output Specification

### 1. Elasticity Summary Table

| Product/SKU | Own-Price Elasticity | 95% CI | Classification | R² | Data Quality |
|---|---|---|---|---|---|
| — | — | [−X, −Y] | Inelastic/Moderate/Elastic | — | Good/Fair/Poor |

### 2. Scenario Impact Analysis

| Scenario | Price Change | Volume Impact | Revenue Impact | Margin Impact | Break-Even Volume Loss |
|---|---|---|---|---|---|
| +5% price increase | +$X.XX | −Y.Y% | +/−$Z | +/−$Z | −W.W% |
| +10% price increase | — | — | — | — | — |
| −10% price decrease | — | — | — | — | — |

### 3. Price Optimization Recommendation

Recommended price point, expected volume, revenue, and margin at that point vs. current.

### 4. Cross-Price Effects Matrix

Matrix showing how price changes in Product A affect volumes of Products B, C, D.

### 5. Sensitivity Tornado Chart

Ranked list of variables that most influence the revenue/margin outcome, with ranges.

## Analysis Framework

### Key Metrics

- **Own-Price Elasticity**: % change in quantity / % change in price
- **Arc Elasticity**: For discrete price changes: ((Q2−Q1)/(Q2+Q1)) / ((P2−P1)/(P2+P1))
- **Revenue Elasticity**: Own-price elasticity + 1 (if > 0, revenue increases with price increase)
- **Margin Elasticity**: Captures margin impact factoring in cost; more relevant than revenue elasticity for profitability
- **Price Gap Ratio**: Brand price / competitive set average price (healthy: 1.0–1.3 for premium brands)
- **Promotional Elasticity**: Separate elasticity during promoted periods (typically 1.5–3× everyday elasticity)
- **Break-Even Volume Loss**: The maximum % volume decline that still yields positive margin impact: `%ΔVolume_max = -%ΔPrice / (CM% + %ΔPrice)` where CM% = contribution margin %

### Industry Benchmarks

| Category | Typical Own-Price Elasticity |
|---|---|
| Baby care / diapers | −1.0 to −1.5 |
| Household cleaners | −1.5 to −2.0 |
| Carbonated soft drinks | −2.0 to −2.8 |
| Salty snacks | −1.8 to −2.5 |
| Paper products | −1.5 to −2.2 |
| Fresh produce | −0.5 to −1.5 |
| Private label (avg) | −2.5 to −3.5 |

## Examples

**Input**: "We want to take a 7% price increase on our top 5 laundry detergent SKUs (branded, liquid, mid-tier). We have 104 weeks of POS data with weekly price points and units across 2,400 stores. What will happen to volume, revenue, and margin?"

**Output**:
1. **Elasticity estimates**: SKU-level elasticities range from −1.6 to −2.1 (avg −1.85), consistent with household cleaners category benchmarks
2. **Scenario at +7%**: Expected volume decline of −13.0% (range: −11.2% to −14.7%). Revenue impact: +$2.1M (net positive because volume loss is partially offset by higher price). Margin impact: +$4.8M (strongly positive due to margin expansion on remaining volume).
3. **Break-even**: Volume can decline up to −18.4% before the price increase becomes margin-negative
4. **Cross-price effect**: Competitor liquid detergent gains an estimated +3.2% volume; private label gains +5.8% volume
5. **Recommendation**: Proceed with +7% increase; monitor competitive response and volume weekly for 8 weeks. If volume declines exceed 15%, consider partial rollback or promotional mitigation.

## Guidelines

- Minimum 52 weeks of data for reliable estimation; 104+ weeks strongly preferred for seasonality control
- Always separate regular-price elasticity from promotional elasticity — they differ substantially
- Never extrapolate elasticity estimates beyond the observed price range (e.g., don't assume a 30% increase will follow the same elasticity measured from 5% variations)
- Elasticity is not constant across the demand curve; acknowledge this limitation when using the constant-elasticity (log-log) model
- Control for competitor actions: if a competitor raised prices simultaneously, your observed elasticity will be biased toward inelastic
- Beware of reverse causality: managers often cut prices when volume is already declining, biasing elasticity toward inelastic. Use instrumental variables if possible.
- Private label elasticity is almost always higher (more elastic) than national brand; don't apply one estimate to both
- Consider reference price effects: consumers respond more negatively to price increases than positively to decreases (loss aversion)
- Report confidence intervals; a point estimate of −2.0 with a 95% CI of [−0.5, −3.5] is not actionable
- Validate elasticity estimates against industry benchmarks; if your estimate is dramatically different, investigate why

## Validation Checklist

- [ ] Data covers at least 52 weeks with sufficient price variation (minimum 3 distinct price points)
- [ ] Regular price and promotional price elasticities are estimated separately
- [ ] Model R² exceeds 0.50 for category-level and 0.30 for SKU-level (otherwise flag data quality)
- [ ] Competitor prices are controlled for in the model
- [ ] Seasonality and trend are controlled for
- [ ] Cross-price elasticities are estimated for key substitutes
- [ ] Scenario analysis includes optimistic, base, and pessimistic cases
- [ ] Break-even volume loss is calculated for each scenario
- [ ] Estimates are benchmarked against industry norms
- [ ] Confidence intervals are reported and actionability is assessed
