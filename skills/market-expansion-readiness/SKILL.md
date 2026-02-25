---
name: market-expansion-readiness
description: Analyze new market or region viability for CPG expansion with structured scoring across demand, supply chain, regulatory, and competitive dimensions. Use when evaluating geographic expansion, new channel entry, international market assessment, or regional launch readiness.

metadata:
  display_name: "Market Expansion Readiness"
  short_description: "Score CPG market expansion readiness by region and channel"
  default_prompt: "Optimize my market expansion and suggest the best next steps"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Market Expansion Readiness Assessment

## Overview

Conduct a structured, multi-dimensional viability assessment for CPG market expansion opportunities. This skill evaluates demand potential, supply chain feasibility, regulatory complexity, competitive intensity, and financial attractiveness to produce a quantified readiness score and go/no-go recommendation.

## When to Use

- Evaluating entry into a new geographic market (domestic or international)
- Assessing a new retail channel (e.g., Club, Dollar, C-Store, Quick Commerce)
- Reviewing international expansion opportunities
- Prioritizing among multiple expansion candidates
- Annual strategic planning — market portfolio optimization

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Target market(s) | Region, country, or channel under evaluation | Name + geographic scope |
| Category data | Market size, growth rate, per-capita consumption | $ and unit volume |
| Current footprint | Existing markets, revenue, margin profile | Summary by region/channel |
| Product portfolio | SKUs under consideration for expansion | List with COGS and ASP |
| Competitive landscape | Key competitors, market shares, positioning | Qualitative + quantitative |
| Regulatory requirements | Known labeling, import, compliance requirements | Text summary |
| Supply chain constraints | Manufacturing locations, logistics capabilities | Facility list + lead times |

## Methodology

### Step 1: Market Attractiveness Scoring (40% of total score)

Evaluate across five sub-dimensions, each scored 1-5:

| Sub-Dimension | Weight | Scoring Criteria |
|---------------|--------|-----------------|
| Market Size | 30% | 1=<$50M TAM; 3=$50-500M; 5=>$500M |
| Growth Rate | 25% | 1=<2% CAGR; 3=2-8%; 5=>8% |
| Per-Capita Consumption Gap | 20% | 1=at parity; 5=significant under-penetration |
| Price Realization Potential | 15% | 1=heavy price pressure; 5=premium pricing viable |
| Category Development Index | 10% | CDI vs national average: 1=<60; 3=60-100; 5=>100 |

### Step 2: Competitive Position Assessment (20% of total score)

| Sub-Dimension | Weight | Scoring Criteria |
|---------------|--------|-----------------|
| Competitor Concentration | 35% | 1=monopoly; 3=oligopoly; 5=fragmented |
| Brand Awareness Transfer | 25% | 1=no awareness; 5=strong brand equity in market |
| Differentiation Opportunity | 25% | 1=commodity; 5=clear white space |
| Retailer Relationship Leverage | 15% | 1=no relationships; 5=existing partnerships |

### Step 3: Supply Chain & Operational Feasibility (20% of total score)

| Sub-Dimension | Weight | Scoring Criteria |
|---------------|--------|-----------------|
| Manufacturing Proximity | 30% | 1=>5000 miles; 3=1000-5000; 5=<1000 miles |
| Cold Chain / Logistics | 25% | 1=no infrastructure; 5=mature logistics network |
| Regulatory Compliance Burden | 25% | 1=extensive reformulation; 5=no changes needed |
| Co-Packer / 3PL Availability | 20% | 1=none; 5=multiple qualified options |

### Step 4: Financial Viability Analysis (20% of total score)

Build a 3-year discounted contribution margin model:

```
Year 1-3 Revenue = Addressable Distribution Points × Velocity Assumption × ASP
COGS = Base COGS + Incremental Logistics + Tariff/Duty
Gross Profit = Revenue − COGS
Contribution = Gross Profit − Trade Spend − Slotting − Market Entry A&P
NPV = Σ (Contribution_t / (1 + WACC)^t) − Initial Investment
```

Score: 1=negative NPV at year 5; 3=breakeven by year 3; 5=positive NPV by year 2

### Step 5: Risk Assessment

Apply a structured risk matrix across:

| Risk Category | Assessment Areas |
|---------------|-----------------|
| Political/Regulatory | Trade policy stability, regulatory predictability |
| Currency/Economic | FX volatility, inflation, tariff exposure |
| Execution | Team capability, partner reliability, timeline risk |
| Cannibalization | Impact on existing market/channel revenue |
| Reputational | Brand perception risk in new market |

Rate each: Probability (1-5) × Impact (1-5) = Risk Score. Flag any score ≥15 as critical.

### Step 6: Composite Scoring and Recommendation

```
Readiness Score = (Market Attractiveness × 0.40)
                + (Competitive Position × 0.20)
                + (Supply Chain Feasibility × 0.20)
                + (Financial Viability × 0.20)

Scale: 1.0-5.0
```

| Score Range | Recommendation |
|-------------|---------------|
| 4.0-5.0 | Strong Go — prioritize for immediate investment |
| 3.0-3.9 | Conditional Go — proceed with identified mitigations |
| 2.0-2.9 | Hold — requires significant capability building |
| 1.0-1.9 | No-Go — insufficient readiness |

## Output Specification

```markdown
# Market Expansion Readiness — [Target Market]

## Executive Summary
[Go/Conditional Go/Hold/No-Go recommendation with composite score and 3-sentence rationale]

## Readiness Scorecard

| Dimension | Score (1-5) | Weight | Weighted Score | Key Driver |
|-----------|-------------|--------|---------------|------------|
| Market Attractiveness | X.X | 40% | X.X | [driver] |
| Competitive Position | X.X | 20% | X.X | [driver] |
| Supply Chain Feasibility | X.X | 20% | X.X | [driver] |
| Financial Viability | X.X | 20% | X.X | [driver] |
| **Composite** | | | **X.X** | |

## Detailed Dimension Analysis
### Market Attractiveness
[Sub-dimension scores with evidence and data sources]

### Competitive Landscape
[Key competitors, market share, white space analysis]

### Supply Chain Assessment
[Logistics feasibility, manufacturing options, lead time analysis]

### Financial Model Summary
| Metric | Year 1 | Year 2 | Year 3 |
|--------|--------|--------|--------|
| Revenue | $XM | $XM | $XM |
| Contribution Margin | $XM | $XM | $XM |
| Cumulative Investment | $XM | $XM | $XM |
| Payback Status | — | — | ✓/✗ |

## Risk Matrix
[Top 5 risks with probability, impact, risk score, and mitigation]

## Recommended Entry Strategy
[Phased approach with milestones, investment requirements, and kill criteria]

## Key Assumptions and Sensitivities
[Critical assumptions with sensitivity ranges]
```

## Analysis Framework

**Porter's Five Forces Application**:
- Supplier power: Ingredient/packaging sourcing in new market
- Buyer power: Retailer concentration and negotiating leverage
- Substitutes: Private label and adjacent category threats
- New entrants: Barriers to entry that protect post-entry
- Rivalry: Intensity and basis of competition

**PESTEL Scan**: Political, Economic, Social, Technological, Environmental, Legal factors specific to target market and category.

## Example

**Input**: "Evaluate expansion of our premium snack brand into the UK market. Current revenue is US-only at $200M. UK snack market is $8B growing 4% with fragmented competition."

**Output excerpt**:
> "**Composite Readiness Score: 3.7 — Conditional Go.** The UK premium snack market presents a $300M addressable opportunity within a fragmented competitive landscape (top 3 players hold 35% combined share), offering meaningful white space for a differentiated US brand. Supply chain feasibility scores moderately (3.2/5.0) due to the need for a European co-packing partner and HFSS regulatory compliance on 40% of the portfolio. Financial modeling indicates breakeven contribution by month 22 at 1,500 distribution points, with £2.8M required pre-launch investment. Critical path items: (1) secure FSA-compliant labeling for full portfolio by Q2, (2) execute co-packer qualification by Q3, (3) confirm Tesco/Sainsbury's category review timing."

## Guidelines

- Score every sub-dimension with explicit evidence — no unsubstantiated ratings
- Always include cannibalization analysis for adjacent market expansion
- Financial models must use conservative velocity assumptions (benchmark: 50th percentile of category)
- Include explicit kill criteria: conditions under which the expansion should be halted
- Sensitivity test the top 3 assumptions (±20%) and show NPV impact
- Document data sources and confidence levels for each input

## Validation Checklist

- [ ] All four dimensions scored with sub-dimension breakdowns
- [ ] Composite score calculated with correct weighting
- [ ] Financial model includes 3-year projection with NPV
- [ ] Risk matrix includes ≥5 risks with probability × impact scoring
- [ ] Entry strategy is phased with clear milestones and kill criteria
- [ ] Cannibalization impact quantified
- [ ] Key assumptions listed with sensitivity ranges
- [ ] Recommendation is clearly stated with supporting rationale
- [ ] Data sources and confidence levels documented
