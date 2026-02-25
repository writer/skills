---
name: pricing-strategy-simulator
description: Simulate CPG pricing strategies including cost pass-through, promotional pricing, EDLP/Hi-Lo analysis, and price pack architecture optimization with elasticity modeling and competitive response scenarios. Use when evaluating price changes, building price pack architecture, analyzing price gaps, or modeling price elasticity impacts.

metadata:
  display_name: "Pricing Strategy Simulator"
  short_description: "Simulate CPG pricing scenarios with elasticity modeling"
  default_prompt: "Simulate my pricing strategy options and suggest the best next steps"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Pricing Strategy Simulator

## Overview

Model and simulate pricing strategies across the CPG value chain — from manufacturer list price through retailer shelf price to consumer response. This skill integrates price elasticity modeling, competitive price gap analysis, price pack architecture design, and channel pricing consistency to produce financially rigorous pricing recommendations with quantified risk ranges.

## When to Use

- Cost-increase pass-through strategy and sizing
- Promotional pricing depth optimization
- EDLP vs Hi-Lo strategy evaluation
- Price pack architecture (PPA) design or rationalization
- Competitive price gap analysis and response
- Private label price gap management
- Price harmonization across channels/retailers
- Revenue Growth Management (RGM) initiatives

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Current pricing | List price, net price, shelf price by SKU/retailer | Price table |
| Price elasticity | Own-price elasticity by SKU or brand (estimated or measured) | Coefficient (e.g., -1.8) |
| Cross-price elasticity | How competitor/substitute price changes affect your volume | Coefficient matrix |
| Cost structure | COGS breakdown, margin targets by SKU | $ per unit |
| Competitive pricing | Key competitor shelf prices and promotional patterns | Price table |
| Volume data | Current unit volume by SKU, retailer, channel | Units per period |
| Price pack architecture | Size, count, price points across portfolio | SKU matrix |
| Retailer margin requirements | Known or estimated retailer margin expectations | % or $ per unit |

## Methodology

### Step 1: Current Pricing Landscape Assessment

Map the complete pricing architecture:

```
Manufacturer List Price (MSLP)
  − Off-Invoice Allowance (OI)
  = Net Invoice Price
  − Scan/Performance Allowances
  = Net Net Price (Net Revenue to Manufacturer)

Retailer Cost (= Net Invoice Price)
  + Retailer Margin
  = Regular Shelf Price (RSP)
  − Promotional Discount
  = Promoted Price

Key Ratios:
  Trade Rate = (MSLP − Net Net) / MSLP
  Retailer Margin = (RSP − Net Invoice) / RSP
  Consumer Value = Price per Unit (oz, count, serving)
```

### Step 2: Elasticity-Based Volume Modeling

Model volume impact of price changes:

**Own-Price Elasticity Application:**
```
% Volume Change = Elasticity × % Price Change

Example: Elasticity = -1.8, Price increase = +5%
Volume impact = -1.8 × 5% = -9.0%

New Volume = Current Volume × (1 + Volume Change)
New Revenue = New Volume × New Price
Revenue impact = (New Revenue / Current Revenue) − 1
```

**Elasticity Confidence Ranges:**
Use a range rather than a point estimate:
- Optimistic elasticity: 70% of point estimate (less elastic)
- Base elasticity: Point estimate
- Pessimistic elasticity: 130% of point estimate (more elastic)

This produces a revenue impact range for risk assessment.

**Cross-Price Elasticity (Competitive Response):**
```
% Volume Change (Yours) = Cross-Elasticity × % Price Change (Competitor)

If competitor follows your increase: Net volume impact reduced
If competitor holds price: Full elasticity impact applies
If competitor reduces price: Amplified negative impact
```

### Step 3: Price Gap Analysis

Analyze competitive and private label price gaps:

**Price Gap Calculation:**
```
Absolute Gap = Your Price − Competitor Price
Relative Gap = (Your Price − Competitor Price) / Competitor Price × 100

Price Per Unit Gap (normalize by size):
Your $/oz vs Competitor $/oz → Gap in $/oz and %
```

**Critical Price Gap Thresholds (CPG industry benchmarks):**
| Gap Type | Danger Zone | Optimal Zone |
|----------|------------|-------------|
| vs. #1 Branded Competitor | >15% premium | 0-10% premium |
| vs. Private Label | >40% premium | 20-35% premium |
| vs. Value Tier | <10% premium | >25% premium |

Flag any SKU crossing into the danger zone.

### Step 4: Price Pack Architecture (PPA) Simulation

Evaluate the portfolio price ladder:

```
Good/Better/Best Framework:
  Good (entry):   [Size/Count] at $[X.XX] → $[X.XX]/oz → Index 100
  Better (core):  [Size/Count] at $[X.XX] → $[X.XX]/oz → Index [XX]
  Best (premium): [Size/Count] at $[X.XX] → $[X.XX]/oz → Index [XX]

Key PPA Metrics:
  - Price per unit consistency across sizes (should reward larger sizes)
  - Margin per unit by tier (Best > Better > Good)
  - Volume distribution across tiers (healthy: 20/50/30 or similar)
  - Channel appropriateness (Club = large sizes, C-Store = small/single serve)
```

**Size Optimization**: Calculate the price-per-unit curve to ensure logical step-ups:
```
Price/oz should decrease with size: Single Serve > Multi-Pack > Family Size
Exception: Premium/craft segments may maintain flat $/oz across sizes
```

### Step 5: Promotional Pricing Simulation

Model promotional depth and frequency:

```
Baseline Volume: [units/week at regular price]
Promoted Volume at X% discount:
  = Baseline × (1 + |Promo Elasticity| × Discount %)
  Note: Promo elasticity typically 2-4x regular elasticity

Promotional Profit:
  = Promoted Volume × (Promoted Price − COGS) − Promo Funding Cost
  vs.
  Baseline Profit = Baseline Volume × (Regular Price − COGS)

Incremental Profit = Promotional Profit − Baseline Profit
```

**EDLP vs Hi-Lo Comparison:**
| Dimension | EDLP | Hi-Lo |
|-----------|------|-------|
| Avg shelf price | Lower, stable | Higher regular, lower promo |
| Volume pattern | Steady | Spiky (promo-driven) |
| Supply chain | Predictable | Volatile (bullwhip) |
| Consumer type | Price-conscious, planned | Deal-seekers, cherry-pickers |
| Trade spend | Lower (less promo funding) | Higher (deep promotional events) |
| Margin profile | Consistent | Variable (deep promos can be negative) |

### Step 6: Scenario Matrix Construction

Build a comprehensive pricing scenario matrix:

| Scenario | Your Action | Competitor Response | Volume Impact | Revenue Impact | Margin Impact |
|----------|------------|-------------------|---------------|----------------|---------------|
| A: Full pass-through | +X% | Match | Low/Med/High | $XM | +Xpp |
| B: Full pass-through | +X% | Hold | Low/Med/High | $XM | +Xpp |
| C: Partial pass-through | +Y% | Match | Low/Med/High | $XM | +Xpp |
| D: Partial + resize | +Y% + downsize | Hold | Low/Med/High | $XM | +Xpp |
| E: Absorb | No change | N/A | None | $0 | −Xpp |

Probability-weight the scenarios and calculate expected value.

### Step 7: Revenue Growth Management (RGM) Synthesis

Integrate pricing with the full RGM toolkit:

```
Revenue Growth Levers:
1. List Price Increase — direct margin expansion
2. Mix Management — shift volume to premium tiers
3. Pack Size Optimization — reduce $/oz while maintaining absolute price
4. Trade Spend Efficiency — same volume at lower promotional investment
5. White Space — new price points/formats without cannibalization
6. Reduce Promotions — fewer, deeper, more targeted promotions

Quantify each lever's contribution to total revenue growth target.
```

## Output Specification

```markdown
# Pricing Strategy Simulation — [Brand/Portfolio]

## Recommendation Summary
**Recommended Strategy**: [Strategy name]
**Expected Revenue Impact**: $XM (+X.X%)
**Expected Margin Impact**: +/-X.Xpp
**Volume Risk Range**: -X% to -X% (optimistic to pessimistic elasticity)

## Current Pricing Landscape
[Pricing architecture from MSLP to shelf price]
[Price gap analysis vs. key competitors and private label]

## Elasticity-Based Impact Model

| Scenario | Price Change | Volume Impact | Revenue Impact | Margin Impact |
|----------|-------------|---------------|----------------|---------------|
| [Scenario A] | +X% | −X% to −X% | +$XM to +$XM | +Xpp |
| [Scenario B] | +X% | −X% to −X% | +$XM to +$XM | +Xpp |

## Competitive Response Analysis
[Scenario matrix with competitor response assumptions]

## Price Pack Architecture Analysis
[Good/Better/Best ladder with price-per-unit curve]

## Promotional Depth Optimization
[Recommended promotional mechanics and depth with ROI by tier]

## RGM Lever Summary
| Lever | Estimated Impact | Confidence | Timeline |
|-------|-----------------|-----------|----------|
| List price | $XM | High | Q[X] |
| Mix management | $XM | Medium | Ongoing |
| Pack optimization | $XM | Medium | Q[X] |

## Risks and Mitigations
[Key risks with probability, impact, and contingency plans]
```

## Analysis Framework

**Price-Volume-Profit Triangle**: Every pricing decision involves trade-offs among three dimensions. Visualize the trade-off:
- Price increase → volume risk → margin benefit (if volume decline < price gain)
- Price decrease → volume gain → margin risk (if margin dilution > volume gain)
- Breakeven volume change = Price Change % / (CM% + Price Change %)

## Example

**Input**: "Cost increase of 8%. Current shelf price $4.99, COGS $2.30, margin 42.5%. Elasticity estimated at -2.0. Private label is at $3.49."

**Analysis**:
> "An 8% cost increase raises COGS from $2.30 to $2.48, compressing margin from 42.5% to 38.5% if absorbed. **Recommended: 5% shelf price increase to $5.24 with simultaneous introduction of a 'Value Size' at $7.99/24oz ($0.33/oz vs current $0.42/oz).** The 5% increase at -2.0 elasticity yields an expected -10% volume decline on the core SKU, partially offset by trade-up to the Value Size. Net revenue impact: +$1.2M (+2.8%). Margin recovers to 40.8% (+230bps vs absorption scenario). The private label gap widens from 43% to 50% premium — approaching the danger zone. Monitor private label unit share weekly; if private label share gains >200bps in 8 weeks, deploy targeted competitive-response coupon ($0.75 off) at affected retailers."

## Guidelines

- Always model a range of elasticities, not a single point estimate
- Include competitive response scenarios — pricing doesn't happen in a vacuum
- Check price gaps vs. private label after every pricing action
- Price pack architecture must maintain logical price-per-unit progression
- Separate regular shelf pricing strategy from promotional pricing strategy
- Calculate breakeven volume change for every pricing scenario
- Consider retailer margin impact — retailers must accept the shelf price

## Validation Checklist

- [ ] Current pricing architecture mapped from list price to shelf price
- [ ] Elasticity applied with confidence range (optimistic/base/pessimistic)
- [ ] At least 3 pricing scenarios modeled with full financial impact
- [ ] Competitive price gaps analyzed with danger zone flagging
- [ ] Cross-price elasticity and competitor response scenarios included
- [ ] Price pack architecture evaluated for logical step-ups
- [ ] Promotional pricing depth optimized with ROI calculations
- [ ] RGM lever contribution quantified
- [ ] Breakeven volume change calculated for recommended strategy
- [ ] Retailer margin impact assessed
- [ ] Risks identified with monitoring triggers and contingency plans
