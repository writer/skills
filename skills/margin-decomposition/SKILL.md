---
name: margin-decomposition
description: Decompose and explain margin erosion or expansion drivers across CPG P&L layers using waterfall analysis, DuPont framework, and contribution margin bridges. Use when diagnosing margin changes, explaining profitability trends, preparing margin deep-dives for finance/leadership, or investigating cost structure shifts.

metadata:
  display_name: "Margin Decomposition"
  short_description: "Decompose CPG margin changes with waterfall analysis"
  default_prompt: "Analyze my margin decomposition and recommend clear next actions"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Margin Decomposition

## Overview

Systematically decompose margin changes into their root cause drivers across the CPG P&L. This skill identifies whether margin movement is driven by price, mix, volume leverage, input costs, trade spend, or structural changes — and quantifies each driver's contribution to the total change. Outputs are structured for CFO-level presentations and finance committee reviews.

## When to Use

- Quarterly margin review and variance analysis
- Gross margin erosion investigation
- Contribution margin trending by brand/channel/customer
- Cost inflation impact assessment
- M&A due diligence — target margin quality analysis
- Annual budget margin bridge construction
- Board/investor questions about profitability trends

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| P&L data | Revenue, COGS components, gross profit, trade spend, A&P, SG&A | Current and prior period |
| Volume data | Units sold by SKU, brand, channel | Current and prior period |
| Pricing data | ASP, list price, net price by SKU/channel | Current and prior period |
| Cost detail | Raw materials, packaging, co-pack/manufacturing, freight, labor | By component, current and prior |
| Mix data | Revenue and margin by brand, channel, customer, or SKU tier | Current and prior period |
| Trade spend | By type and by retailer/channel | Current and prior period |

## Methodology

### Step 1: Margin Layer Definition

Analyze margin at four distinct P&L layers:

```
Gross Revenue
  − Returns & Allowances
  = Net Revenue                        → Gross Revenue Margin
  − COGS
    − Raw Materials
    − Packaging
    − Manufacturing / Co-Pack Labor
    − Freight-In
  = Gross Profit                       → Gross Margin %
  − Trade Spend
  = Net Gross Profit                   → Net Margin after Trade
  − Brand Investment (A&P)
  = Contribution Margin                → Contribution Margin %
  − Allocated SG&A
  = Brand / Channel Operating Profit   → Operating Margin %
```

Calculate each margin layer for current period and comparison period. Identify which layer(s) are responsible for the total margin change.

### Step 2: Volume / Price / Mix Decomposition

Decompose net revenue change into three components:

**Price Effect:**
```
= (Current ASP − Prior ASP) × Current Volume
```
Captures the pure pricing impact at constant volume.

**Volume Effect:**
```
= (Current Volume − Prior Volume) × Prior ASP
```
Captures the pure volume change at constant pricing.

**Mix Effect:**
```
= Total Revenue Change − Price Effect − Volume Effect
```
Captures the impact of shifting between high/low-priced products or channels. A positive mix effect means the portfolio shifted toward higher-priced items.

### Step 3: COGS Decomposition

Break COGS change into constituent drivers:

| Driver | Calculation | Typical CPG Range |
|--------|------------|-------------------|
| Raw material cost | Δ commodity cost × current volume | 30-50% of COGS |
| Packaging cost | Δ packaging cost × current volume | 8-15% of COGS |
| Manufacturing efficiency | Δ cost per unit from throughput/yield | 15-25% of COGS |
| Freight-in | Δ inbound logistics cost | 5-10% of COGS |
| Volume leverage | Fixed cost absorption on Δ volume | 10-20% of COGS |
| Mix impact on COGS | Shift to higher/lower cost SKUs | Residual |

**Volume leverage calculation:**
```
Fixed Manufacturing Cost per Unit:
  Prior period: Fixed Costs / Prior Volume = $X/unit
  Current period: Fixed Costs / Current Volume = $Y/unit
  Leverage effect: (Y − X) × Current Volume
  Positive volume → favorable leverage (lower cost/unit)
```

### Step 4: Gross Margin Bridge

Construct a waterfall bridge from prior period margin to current:

```
Prior Period Gross Margin %          XX.X%
  + Price effect                    +X.Xpp
  + Volume leverage                 +X.Xpp
  − Raw material inflation          −X.Xpp
  − Packaging inflation             −X.Xpp
  +/− Mix effect                    +/-X.Xpp
  +/− Manufacturing efficiency      +/-X.Xpp
  +/− Freight                       +/-X.Xpp
= Current Period Gross Margin %      XX.X%
  Total Change:                      X.Xpp
```

Each bridge element must be expressed in basis points or percentage points and reconcile exactly to the total change.

### Step 5: DuPont Decomposition

For return-based margin analysis, apply the DuPont framework:

```
Return on Invested Capital (ROIC)
= NOPAT Margin × Capital Turnover
= (Net Operating Profit / Revenue) × (Revenue / Invested Capital)

Decompose NOPAT Margin:
= Gross Margin − Trade Spend Rate − A&P Rate − SG&A Rate − Tax Rate

Decompose Capital Turnover:
= 1 / (Receivable Days + Inventory Days − Payable Days + Fixed Asset Intensity)

Margin improvement paths:
1. Pricing/mix → higher gross margin
2. Trade efficiency → lower trade spend rate
3. Operating leverage → lower SG&A rate
4. Working capital → higher capital turnover
```

### Step 6: Structural vs. Transient Analysis

Classify each margin driver as structural or transient:

| Classification | Definition | Action |
|---------------|-----------|--------|
| Structural favorable | Permanent improvement (pricing, reformulation, automation) | Embed in forward plan |
| Structural unfavorable | Permanent headwind (regulation, commodity regime change) | Plan mitigation |
| Transient favorable | One-time benefit (inventory release, timing) | Do not extrapolate |
| Transient unfavorable | One-time cost (recall, launch expense, weather) | Normalize in adjusted view |

This classification is essential for forward projection and investor communication.

### Step 7: Forward Margin Outlook

Build a forward margin bridge using the structural/transient classification:

```
Current Period Margin              XX.X%
  + Structural tailwinds          +X.Xpp  [list items]
  − Structural headwinds          −X.Xpp  [list items]
  + Transient items rolling off   +X.Xpp  [list items]
  − Known new transient costs     −X.Xpp  [list items]
  + Management actions            +X.Xpp  [list items with confidence]
= Projected Next Period Margin     XX.X%
```

## Output Specification

```markdown
# Margin Decomposition — [Period] vs [Comparison Period]

## Executive Summary
[2-3 sentences: total margin change, top 2 drivers, outlook]

## Margin Summary

| Metric | Current | Prior | Change | Driver |
|--------|---------|-------|--------|--------|
| Gross Margin % | XX.X% | XX.X% | +/-X.Xpp | [Primary driver] |
| Net Margin after Trade | XX.X% | XX.X% | +/-X.Xpp | [Primary driver] |
| Contribution Margin % | XX.X% | XX.X% | +/-X.Xpp | [Primary driver] |

## Gross Margin Waterfall Bridge
[Prior Margin → individual drivers → Current Margin]
[Each driver quantified in pp with explanation]

## Revenue Decomposition
| Component | Impact ($) | Impact (pp on margin) |
|-----------|-----------|----------------------|
| Price | $XM | +X.Xpp |
| Volume | $XM | +/-X.Xpp |
| Mix | $XM | +/-X.Xpp |

## COGS Decomposition
| Component | Impact ($) | Impact (pp on margin) |
|-----------|-----------|----------------------|
| Raw Materials | $XM | −X.Xpp |
| Packaging | $XM | −X.Xpp |
| Manufacturing | $XM | +/-X.Xpp |
| Freight | $XM | +/-X.Xpp |
| Volume Leverage | $XM | +X.Xpp |

## Structural vs. Transient Classification
[Table classifying each driver with forward implications]

## DuPont Analysis (if applicable)
[ROIC decomposition with margin × turnover components]

## Forward Margin Bridge
[Current → projected next period with driver-level detail]

## Recommendations
1. [Margin recovery/expansion action with quantified impact]
2. [Cost mitigation initiative with timeline]
3. [Mix management strategy]
```

## Analysis Framework

**Margin Quality Assessment**: Rate the margin profile on sustainability:

| Quality Indicator | Good | Concerning |
|-------------------|------|------------|
| Pricing power | Consistent price realization | Reliance on promotional volume |
| Cost trajectory | Declining cost per unit (scale) | Rising input costs without offset |
| Mix trend | Shifting to premium/higher-margin | Shifting to value/lower-margin |
| Trade spend trend | Stable or declining rate | Increasing rate without volume gain |
| Volume leverage | Growing volume on fixed base | Declining volume with fixed cost drag |

## Example

**Input**: "Q3 gross margin was 34.2% vs 36.8% prior year. Revenue grew 5% to $85M. Commodity costs up 12%. New value line launched in Q2."

**Output excerpt**:
> "Gross margin contracted 260bps YoY (34.2% vs 36.8%), driven by three primary factors: (1) Raw material inflation: −180bps. Soybean oil (+18%) and packaging resin (+9%) drove $3.1M of incremental COGS, partially offset by $0.8M in reformulation savings. (2) Mix dilution: −140bps. The new Value Line, contributing 12% of Q3 volume at 22% gross margin vs 38% portfolio average, created significant mix drag. (3) Partially offset by pricing: +80bps. The April price increase (weighted average +3.2%) contributed $2.7M, though elasticity reduced units by 1.4%. **Structural/Transient**: Commodity inflation is classified as structural given the 18-month forward curve; mix dilution is structural as the Value Line is planned to reach 18% of volume. **Forward bridge**: Q4 margin projected at 35.0-35.5% as the June pricing action fully annualizes (+40bps) and manufacturing line consolidation delivers productivity savings (+30bps)."

## Guidelines

- Margin bridges must reconcile exactly — the sum of drivers must equal total change
- Express all drivers in both absolute dollars and basis points/percentage points
- Always classify drivers as structural vs. transient for forward projection
- Include volume leverage analysis — it is frequently the most misunderstood driver
- Apply the DuPont framework for any ROIC or ROE analysis
- Show margin at multiple P&L layers — gross margin alone is insufficient
- Highlight "margin quality" — is the margin sustainable or artificially inflated?

## Validation Checklist

- [ ] Margin calculated at all four P&L layers
- [ ] Revenue decomposed into volume, price, and mix effects
- [ ] COGS decomposed into ≥5 component drivers
- [ ] Waterfall bridge reconciles exactly to total margin change
- [ ] Each driver quantified in both $ and pp/bps
- [ ] Structural vs. transient classification applied to every driver
- [ ] DuPont decomposition included for return-based analysis
- [ ] Forward margin bridge constructed with confidence levels
- [ ] Margin quality indicators assessed
- [ ] Recommendations linked to specific drivers with quantified impact
