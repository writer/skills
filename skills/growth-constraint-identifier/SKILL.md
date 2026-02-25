---
name: growth-constraint-identifier
description: Identify and prioritize bottlenecks constraining CPG brand or portfolio growth using Theory of Constraints, value chain analysis, and growth decomposition frameworks. Use when diagnosing growth slowdowns, preparing strategic plans, conducting portfolio reviews, or investigating why a brand is underperforming its potential.

metadata:
  display_name: "Growth Constraint Identifier"
  short_description: "Pinpoint bottlenecks constraining CPG brand growth"
  default_prompt: "Review my growth constraint and highlight top risks and next actions"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Growth Constraint Identifier

## Overview

Systematically diagnose the binding constraints that prevent a CPG brand, portfolio, or business unit from achieving its growth potential. This skill applies Theory of Constraints (TOC), growth decomposition, and value chain analysis to identify, rank, and develop resolution plans for the highest-impact bottlenecks — converting strategic ambiguity into prioritized action.

## When to Use

- Brand growth deceleration diagnosis
- Annual strategic planning — identifying the critical few priorities
- Portfolio review — why are certain brands underperforming?
- Post-acquisition integration — identifying scaling barriers
- Investor/board growth story articulation
- Operational bottleneck identification (capacity, supply chain)
- Go-to-market effectiveness assessment

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Growth target | Revenue/volume growth objective vs current trajectory | $ or % target |
| Historical performance | 3-5 years of revenue, volume, distribution, market share | Time series |
| Market data | Category growth, competitive share, market size | Syndicated or estimated |
| Distribution data | Weighted/numeric distribution, velocity by channel | ACV % and turns |
| Consumer data | Awareness, trial, repeat, household penetration | Funnel metrics |
| P&L structure | Revenue, margin, trade spend, A&P by brand/channel | Financial data |
| Supply chain status | Capacity utilization, lead times, service levels | Operational metrics |
| Innovation pipeline | New products in development, launch dates, expected contribution | Pipeline list |

## Methodology

### Step 1: Growth Decomposition

Decompose total growth into its mathematical components:

**Revenue Growth Tree:**
```
Revenue Growth
├── Volume Growth
│   ├── Distribution Growth (more doors/shelves)
│   │   ├── New Retailer Wins
│   │   ├── New Channel Entry
│   │   └── Shelf Expansion (existing retailers)
│   ├── Velocity Growth (more units per point of distribution)
│   │   ├── Household Penetration Increase
│   │   ├── Purchase Frequency Increase
│   │   └── Units per Occasion Increase
│   └── Innovation Contribution
│       ├── Line Extensions
│       └── New Platforms
├── Price Growth
│   ├── List Price Increases
│   ├── Mix Improvement (trade-up)
│   └── Reduced Promotional Depth
└── Channel Mix
    ├── Shift to Higher-ASP Channels
    └── International Expansion
```

Quantify each branch: What is the contribution of each driver to total growth? Which branches are growing vs. declining?

### Step 2: Growth Gap Analysis

Calculate the gap between aspiration and trajectory:

```
Growth Target:           +$XM (+X%)
Current Trajectory:      +$YM (+Y%)  [based on run-rate]
Growth Gap:              $ZM  (Target − Trajectory)

Gap Decomposition:
  Distribution gap:      $AM  (ACV opportunity × estimated velocity)
  Velocity gap:          $BM  (penetration/frequency opportunity)
  Innovation gap:        $CM  (pipeline contribution shortfall)
  Pricing gap:           $DM  (price realization opportunity)
  Total addressable:     $(A+B+C+D)M
  Gap coverage ratio:    (A+B+C+D) / Z  [should be >1.5x for confidence]
```

If the gap coverage ratio is below 1.5x, the growth target may be unrealistic without new strategic initiatives.

### Step 3: Constraint Identification Using Theory of Constraints

Apply TOC's Five Focusing Steps:

**1. IDENTIFY the constraint** — Find the bottleneck:

| Value Chain Stage | Potential Constraints | Diagnostic Question |
|-------------------|----------------------|-------------------|
| Consumer Demand | Low awareness, low trial, poor repeat | Is the consumer funnel leaking? Where? |
| Brand Positioning | Unclear differentiation, weak value prop | Does the brand have a right to win? |
| Innovation | Weak pipeline, slow speed-to-market | Is innovation filling the growth gap? |
| Distribution | Low ACV, poor shelf position, gaps in channels | Are we in enough stores/shelves? |
| Velocity | Low turns, poor merchandising, weak promo ROI | Are we selling fast enough where we are? |
| Pricing | Uncompetitive gaps, margin pressure, trade dependency | Is pricing enabling or inhibiting growth? |
| Supply Chain | Capacity limits, service failures, high cost | Can we reliably deliver growth volume? |
| Organization | Talent gaps, structural misalignment, decision speed | Can the organization execute at the required pace? |

**2. EXPLOIT the constraint** — Maximize throughput at the bottleneck without new investment.

**3. SUBORDINATE** — Align all other activities to support the constraint.

**4. ELEVATE** — Invest to expand the constraint's capacity.

**5. REPEAT** — After resolving, the constraint moves; re-diagnose.

### Step 4: Consumer Funnel Diagnostics

Analyze the consumer conversion funnel:

```
Total Category Buyers:         XX M households
  × Brand Awareness:           XX% → XX M aware
  × Consideration:             XX% → XX M considering
  × Trial:                     XX% → XX M trialed
  × Repeat:                    XX% → XX M repeat buyers
  × Loyalty (sole/primary):    XX% → XX M loyal

Funnel Conversion Benchmarks (vs. category average):
  Awareness → Consideration:    XX% (benchmark: XX%) → Gap: Xpp
  Consideration → Trial:        XX% (benchmark: XX%) → Gap: Xpp
  Trial → Repeat:               XX% (benchmark: XX%) → Gap: Xpp
  Repeat → Loyalty:             XX% (benchmark: XX%) → Gap: Xpp

Constraint: The largest gap vs. benchmark indicates the funnel bottleneck.
```

### Step 5: Distribution Effectiveness Analysis

**Distribution Quality Assessment:**
```
Numeric Distribution:  XX% of stores carry the brand
Weighted Distribution: XX% ACV (dollar-weighted)
Quality Index:         Weighted / Numeric = X.X
  >1.2: Skewed to large stores (good for volume, may miss breadth)
  <0.8: Skewed to small stores (broad but low-volume)

Velocity by Distribution Tier:
  Top 20% of stores by volume:  $XX/store/week
  Middle 60%:                   $XX/store/week
  Bottom 20%:                   $XX/store/week
  If bottom 20% velocity is <30% of top 20% → distribution quality issue
```

**White Space Analysis:**
```
Retailers where you have 0% distribution but category is active:
  [Retailer A]: $XM category volume → $XM addressable at XX% fair share
  [Retailer B]: $XM category volume → $XM addressable
  Total White Space: $XM
```

### Step 6: Constraint Prioritization Matrix

Rank constraints by impact and feasibility:

| Constraint | Growth Impact ($M) | Feasibility (1-5) | Time to Impact | Investment Required | Priority Score |
|-----------|-------------------|-------------------|----------------|-------------------|---------------|
| [Constraint 1] | $XM | X | Q/Months | $XM | Calculated |
| [Constraint 2] | $XM | X | Q/Months | $XM | Calculated |

**Priority Score Calculation:**
```
Priority Score = (Growth Impact × Feasibility) / (Time to Impact × Investment)
```

Rank by Priority Score. Focus organizational energy on the top 2-3 constraints.

### Step 7: Constraint Resolution Planning

For each top constraint, define a resolution plan:

```
Constraint: [Name]
Current State: [Metric value]
Target State: [Metric target]
Gap: [Quantified gap]

Resolution Approach:
  Short-term (0-3 months): [Exploit — maximize within current resources]
  Medium-term (3-12 months): [Elevate — invest to expand capacity]
  Long-term (12+ months): [Transform — structural change]

Resources Required: [People, budget, capabilities]
Success Metrics: [Leading indicators to track weekly/monthly]
Risk: [What could prevent resolution]
```

## Output Specification

```markdown
# Growth Constraint Analysis — [Brand/Portfolio]

## Executive Summary
[Growth target, growth gap, #1 binding constraint, recommended action]

## Growth Decomposition
[Revenue growth tree with quantified contribution by driver]

## Growth Gap Analysis
| Component | Trajectory | Target | Gap |
|-----------|-----------|--------|-----|
| Total | $XM | $XM | $XM |
| Distribution | +$XM | +$XM | $XM |
| Velocity | +$XM | +$XM | $XM |
| Innovation | +$XM | +$XM | $XM |
| Pricing | +$XM | +$XM | $XM |

## Constraint Identification
### Binding Constraint: [Name]
[Detailed diagnosis with supporting evidence]

### Secondary Constraints
[2-3 additional constraints with evidence]

## Consumer Funnel Diagnostic
[Funnel stages with conversion rates vs benchmarks; bottleneck identified]

## Distribution White Space
[Addressable distribution opportunities quantified]

## Constraint Priority Matrix
[Ranked constraints with impact, feasibility, priority score]

## Resolution Plans
### Constraint 1: [Name]
- Short-term: [Action]
- Medium-term: [Action]
- Long-term: [Action]
- Investment: $XM | Expected Impact: $XM | Timeline: [X months]

## Monitoring Framework
| Constraint | Leading Indicator | Current | Target | Frequency |
|-----------|-------------------|---------|--------|-----------|
| ... | ... | ... | ... | Weekly/Monthly |
```

## Analysis Framework

**Ansoff Matrix Application**: Map growth initiatives to risk profile:
| | Existing Products | New Products |
|---|------------------|--------------|
| Existing Markets | Market Penetration (lowest risk) | Product Development |
| New Markets | Market Development | Diversification (highest risk) |

Most CPG growth constraints are in Market Penetration (distribution + velocity) — resolve these before pursuing higher-risk quadrants.

## Example

**Input**: "Brand revenue is $80M, growing 3% but target is 10%. Category growing 5%. Market share declining from 12% to 11%. Available in 65% ACV."

**Analysis excerpt**:
> "**Binding Constraint: Distribution (65% ACV vs 85% category leader).** Growth decomposition shows distribution contributes only +$0.5M to the $8M growth gap, but is the gate to velocity gains. At current velocity ($4.20/store/week), expanding from 65% to 80% ACV would add $6.2M in annualized revenue — covering 78% of the growth gap alone. Consumer funnel analysis reveals Trial → Repeat conversion at 32% vs 45% category benchmark, suggesting a secondary product experience constraint. **Resolution**: Short-term: Secure distribution at Albertsons (0% ACV today, $3.2M category volume = $1.4M addressable) and expand Walmart from 2 to 4 facings. Medium-term: Reformulate SKU #3 and #7 (lowest repeat rates at 22% and 25%) to address the trial-to-repeat gap. Long-term: Enter Club channel with exclusive multi-pack to step-change distribution and trial simultaneously."

## Guidelines

- Always start with the growth decomposition tree — it prevents symptom-chasing
- The binding constraint is the ONE thing that, if resolved, would unlock the most growth
- Theory of Constraints mandates focus: resolve #1 before moving to #2
- Distribution constraints should be assessed before velocity constraints (you can't grow velocity in stores you're not in)
- Consumer funnel gaps reveal demand-side constraints; distribution/supply reveal supply-side
- Gap coverage ratio must exceed 1.5x — if not, flag the target as aspirational
- Organizational constraints (talent, structure, decision speed) are real and should be assessed

## Validation Checklist

- [ ] Growth decomposition tree fully quantified across all branches
- [ ] Growth gap calculated with gap coverage ratio
- [ ] Theory of Constraints 5 focusing steps applied
- [ ] Consumer funnel analyzed with benchmark comparisons
- [ ] Distribution white space quantified
- [ ] At least 5 constraint categories assessed
- [ ] Constraints ranked using priority score (impact × feasibility / time × investment)
- [ ] Top 2-3 constraints have detailed resolution plans (short/medium/long-term)
- [ ] Monitoring framework established with leading indicators
- [ ] Binding constraint clearly identified with evidence-based rationale
