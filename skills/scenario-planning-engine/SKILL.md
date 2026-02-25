---
name: scenario-planning-engine
description: Build structured what-if scenario models for CPG strategic planning using Monte Carlo simulation concepts, sensitivity analysis, and decision trees. Use when modeling pricing changes, market disruptions, capacity planning, commodity cost volatility, or any strategic decision requiring probabilistic analysis.

metadata:
  display_name: "Scenario Planning Engine"
  short_description: "Build what-if scenario models for CPG strategic planning"
  default_prompt: "Optimize my what if scenario models for cpg and suggest the best next steps"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Scenario Planning Engine

## Overview

Construct rigorous "what if" scenario models that quantify the range of outcomes for strategic CPG decisions. This skill combines deterministic scenario construction with Monte Carlo simulation concepts, sensitivity analysis, and decision-tree frameworks to produce probability-weighted projections and risk-adjusted recommendations.

## When to Use

- Pricing strategy decisions (cost pass-through, promotional depth changes)
- Commodity cost volatility planning (raw materials, packaging, freight)
- Capacity and supply chain investment decisions
- M&A scenario modeling (acquisition targets, integration assumptions)
- Market disruption preparedness (competitive entry, regulation changes)
- Annual operating plan stress testing
- Capital allocation decisions across brands/channels

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Decision context | What strategic question needs answering | Clear problem statement |
| Base case assumptions | Current state P&L, volume, pricing, costs | Financial data |
| Variable parameters | Which inputs to vary in scenarios | List with current values |
| Parameter ranges | Min/max/most-likely for each variable | Triangular or uniform range |
| Constraints | Budget limits, capacity ceilings, contractual obligations | Quantified boundaries |
| Time horizon | Projection period | Quarters or years |
| Success criteria | What defines a good outcome | KPI thresholds |

## Methodology

### Step 1: Decision Framing

Structure the strategic question using the MECE framework:

```
Decision: [Clear statement of the decision to be made]
Alternatives: [2-5 mutually exclusive options]
Criteria: [How success will be measured — revenue, margin, market share, NPV]
Constraints: [Non-negotiable boundaries]
Time Horizon: [Period over which to evaluate outcomes]
```

### Step 2: Variable Identification and Classification

Categorize all model variables:

| Variable Type | Description | Treatment |
|--------------|-------------|-----------|
| Decision variables | Inputs you control (price, spend, investment) | Set by scenario |
| Uncertain variables | Inputs you cannot control (demand, costs, competition) | Model with distributions |
| Fixed parameters | Inputs that don't change across scenarios | Hold constant |

For each uncertain variable, define a probability distribution:
- **Triangular**: Min, Most Likely, Max — use when limited data available
- **Normal**: Mean, Std Dev — use for well-understood variables with historical data
- **Uniform**: Min, Max — use when all outcomes equally likely
- **Binary**: Probability of occurrence — use for discrete events (competitor entry: 30%)

### Step 3: Deterministic Scenario Construction

Build three to five named scenarios:

| Scenario | Definition | Key Assumptions |
|----------|-----------|-----------------|
| Bull Case | Top-decile outcomes across key variables | [Specific assumptions] |
| Base Case | Most likely outcome; management plan | [Specific assumptions] |
| Bear Case | Bottom-decile; plausible downside | [Specific assumptions] |
| Stress Test | Tail risk; worst realistic combination | [Specific assumptions] |
| Black Swan | Extreme disruption (optional) | [Specific assumptions] |

Each scenario must be internally consistent — variable assumptions should be logically coherent (e.g., recession scenario should have both demand decline AND cost pressure relief).

### Step 4: Monte Carlo Simulation Framework

For complex decisions, layer probabilistic analysis:

```
For N iterations (recommend N = 1,000-10,000):
    1. Sample each uncertain variable from its distribution
    2. Calculate the outcome metric (Revenue, Margin, NPV)
    3. Store the result

Outputs:
    - Mean expected outcome
    - Median outcome
    - Standard deviation
    - 5th percentile (downside risk)
    - 95th percentile (upside potential)
    - Probability of meeting success threshold
    - Distribution histogram
```

**Correlation handling**: If variables are correlated (e.g., commodity cost and competitor pricing), specify the correlation coefficient and use correlated sampling.

### Step 5: Sensitivity Analysis

Identify which variables drive the most variance in outcomes:

**Tornado Analysis:**
- Hold all variables at base case
- Vary each variable independently across its range (10th to 90th percentile)
- Rank by absolute impact on the outcome metric
- Present as a tornado chart showing impact magnitude

**Two-Variable Sensitivity Matrix:**
For the top two variables, build a matrix showing outcomes across combinations:

```
              | Price -5% | Price Base | Price +5% |
|-------------|-----------|-----------|-----------|
| Volume -10% |  $XXM     |  $XXM     |  $XXM     |
| Volume Base |  $XXM     |  $XXM     |  $XXM     |
| Volume +10% |  $XXM     |  $XXM     |  $XXM     |
```

### Step 6: Decision Tree Integration

For sequential decisions, structure as a decision tree:

```
Decision Node 1: [Invest / Don't Invest]
  → If Invest:
      Chance Node: Market Response
        → 40% probability: Strong uptake → Outcome A ($XM NPV)
        → 45% probability: Moderate uptake → Outcome B ($XM NPV)
        → 15% probability: Weak uptake → Outcome C ($XM NPV)
      Expected Value = 0.40(A) + 0.45(B) + 0.15(C) = $XM
  → If Don't Invest:
      Outcome D: Status quo ($XM NPV)
```

Calculate Expected Monetary Value (EMV) for each decision path. Apply risk-adjustment using utility functions if the organization is risk-averse.

### Step 7: Recommendation Synthesis

Combine scenario analysis with decision criteria:

```
Recommended Action: [Decision]
Expected Value: $XM (probability-weighted)
Downside Risk (5th %ile): $XM
Upside Potential (95th %ile): $XM
Probability of Exceeding Threshold: XX%
Key Assumption to Monitor: [Variable with highest sensitivity]
Decision Reversal Point: [At what value of key variable does the decision change?]
```

## Output Specification

```markdown
# Scenario Analysis — [Decision Context]

## Decision Summary
**Question**: [What are we deciding?]
**Recommendation**: [Recommended action]
**Expected Value**: $XM | **Downside Risk**: $XM | **Upside Potential**: $XM

## Scenario Comparison

| Metric | Bull | Base | Bear | Stress |
|--------|------|------|------|--------|
| Revenue | $XM | $XM | $XM | $XM |
| Gross Margin % | XX% | XX% | XX% | XX% |
| EBITDA | $XM | $XM | $XM | $XM |
| NPV | $XM | $XM | $XM | $XM |
| Probability Weight | X% | X% | X% | X% |

## Sensitivity Analysis
### Tornado Chart (Top Variables by Impact)
1. [Variable 1]: $XM swing (from $XM to $XM)
2. [Variable 2]: $XM swing
3. [Variable 3]: $XM swing

### Two-Variable Matrix
[Price × Volume or top-2 variable matrix]

## Monte Carlo Results (if applicable)
- Mean: $XM | Median: $XM | Std Dev: $XM
- 5th percentile: $XM | 95th percentile: $XM
- P(exceeding target): XX%

## Decision Tree
[Structured decision tree with EMV calculations]

## Key Assumptions and Monitoring Plan
| Assumption | Base Value | Sensitivity | Monitoring Metric | Review Frequency |
|-----------|-----------|-------------|-------------------|-----------------|
| ... | ... | High/Med/Low | ... | Weekly/Monthly |

## Contingency Triggers
| Trigger Condition | Action |
|------------------|--------|
| [Variable] exceeds [threshold] | [Contingency action] |
```

## Analysis Framework

**Real Options Thinking**: For irreversible investments, consider the value of waiting:
- Option to defer: What is gained by delaying 1 quarter?
- Option to stage: Can investment be phased to reduce risk?
- Option to abandon: What is the exit cost if assumptions prove wrong?

**Regret Minimization**: For each decision alternative, calculate maximum regret (the worst outcome minus the best alternative's outcome in that scenario). Choose the alternative that minimizes maximum regret for risk-averse organizations.

## Example

**Input**: "Should we pass through a 7% cost increase to retailers? Our brand elasticity is estimated at -1.8. Current revenue $50M, margin 35%."

**Output excerpt**:
> "**Recommended: Staged pass-through of 5% with 2% absorbed.** Monte Carlo simulation (5,000 iterations) with elasticity sampled from a triangular distribution (-1.2, -1.8, -2.5) shows: Full 7% pass-through yields an expected revenue of $47.8M with 38.2% margin (base), but a 22% probability of revenue falling below $45M if elasticity exceeds -2.0. A 5% pass-through yields $48.5M expected revenue at 37.1% margin with only 8% probability of the $45M downside. The incremental $0.7M revenue protection plus lower downside risk justifies absorbing 2pp of the cost increase ($350K annual margin cost). **Decision reversal point**: If true elasticity is below -1.4, full pass-through becomes optimal. Monitor velocity at key accounts weekly for 8 weeks post-implementation."

## Guidelines

- Every scenario must be internally consistent — don't combine "recession" demand with "boom" pricing
- Always include a stress test scenario beyond the normal bear case
- Probability weights across deterministic scenarios must sum to 100%
- Sensitivity analysis should test ±20% as default range unless better data exists
- Include decision reversal points — the threshold at which the recommendation changes
- Document all assumptions with their source and confidence level
- Use Monte Carlo concepts for high-stakes decisions (>$5M impact)

## Validation Checklist

- [ ] Decision framed with MECE alternatives and clear success criteria
- [ ] Variables classified as decision, uncertain, or fixed
- [ ] At least 3 named scenarios with internally consistent assumptions
- [ ] Probability distributions defined for key uncertain variables
- [ ] Sensitivity (tornado) analysis identifies top 3 drivers
- [ ] Two-variable sensitivity matrix for top 2 variables
- [ ] Monte Carlo framework applied for high-stakes decisions
- [ ] Decision tree constructed for sequential decisions
- [ ] Expected values calculated with probability weights
- [ ] Decision reversal points identified
- [ ] Contingency triggers defined with specific thresholds and actions
- [ ] All assumptions documented with sources and confidence levels
