---
name: board-ready-kpi-narratives
description: Generate investor-safe, board-ready narratives from raw KPI data for CPG companies. Use when preparing board decks, investor updates, earnings commentary, or when translating raw metrics into strategic storytelling for governance audiences.

metadata:
  display_name: "Board Ready Kpi Narratives"
  short_description: "Turn raw CPG KPI data into investor-safe board narratives"
  default_prompt: "Summarize my board ready kpi with key findings and next steps"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Board-Ready KPI Narratives

## Overview

Transform raw performance metrics into polished, investor-grade narratives suitable for board presentations, quarterly business reviews, and investor communications. Each narrative contextualizes metrics within strategic objectives, applies appropriate financial frameworks, and maintains the precision and tone required for fiduciary audiences.

## When to Use

- Quarterly board meeting preparation
- Investor update letters and earnings call scripts
- Annual strategic review presentations
- Audit committee financial commentary
- PE/VC portfolio company reporting
- IPO roadshow metric narratives

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| KPI dataset | Metrics with current, prior period, plan/budget values | Table with time series |
| Strategic priorities | Company's 3-5 declared strategic pillars | Text list |
| OKR/goal framework | Current quarter/annual objectives and key results | Structured OKR format |
| Audience context | Board, investors, audit committee, or mixed | Selection |
| Materiality thresholds | Revenue/margin thresholds for disclosure | Dollar or % thresholds |
| Prior narrative | Last period's board narrative for consistency | Document or text |

## Methodology

### Step 1: Strategic Pillar Mapping

Map every KPI to one of the company's declared strategic pillars. Orphan metrics (those not tied to a pillar) should be flagged — they indicate either a measurement gap or strategic misalignment. Use an OKR cascade:

```
Company Objective -> Key Result -> Supporting KPI -> Data Point
```

### Step 2: Materiality Assessment

Apply a materiality filter before narrating any metric:
- **Quantitative materiality**: >5% of revenue, >100bps of margin, or >$X threshold
- **Qualitative materiality**: New capability, strategic pivot, regulatory trigger, or reputational risk
- **Trend materiality**: 3+ consecutive periods of directional movement regardless of absolute size

Only narrate metrics that pass at least one materiality gate.

### Step 3: DuPont Decomposition for Financial Metrics

For return-based metrics, decompose using the DuPont framework:

```
ROE = Net Margin x Asset Turnover x Equity Multiplier

For CPG-specific application:
ROIC = NOPAT / Invested Capital
     = (Revenue x Net Margin) / (Working Capital + Fixed Assets)
     Decompose into: Volume x Price x Mix x Cost x Capital Efficiency
```

This enables precise attribution of return changes to operational drivers.

### Step 4: Narrative Construction

Write each KPI narrative using the **MECE Narrative Framework**:

1. **Metric**: State the KPI, its value, and comparison basis
2. **Explanation**: Attribute the variance to no more than 3 root causes, ranked by impact
3. **Context**: Place the metric in industry/competitive/historical context
4. **Expectation**: State the forward-looking trajectory and any actions underway

Tone requirements for board audiences:
- Factual, not promotional — avoid superlatives ("best ever", "incredible")
- Balanced — pair wins with associated risks
- Precise — exact figures, not approximations, with stated rounding conventions
- Forward-looking statements must include appropriate caveats

### Step 5: Sensitivity and Risk Framing

For any metric with >10% variance to plan, include:
- Base/bull/bear scenario range
- Key assumptions underlying the plan figure
- Management actions taken or planned
- Leading indicators that will confirm trajectory

### Step 6: Consistency and Disclosure Review

Cross-check against:
- Prior period narrative for consistency of definitions and methodology
- SEC Regulation FD requirements (if public company) — no selective disclosure
- Non-GAAP reconciliation requirements if using adjusted metrics
- Forward-looking statement safe harbor language

## Output Specification

```markdown
# [Company] — Q[X] FY[YYYY] Board Narrative

## Strategic Performance Summary
[2-3 paragraphs linking overall performance to strategic pillars]

## Pillar 1: [Name]
### Key Metric: [Metric Name]
**Result**: [Value] vs [Plan] ([Variance%])
**Attribution**: [Root cause 1 (X%), Root cause 2 (Y%), Root cause 3 (Z%)]
**Context**: [Industry benchmark, historical trend, competitive position]
**Outlook**: [Forward trajectory with key assumptions stated]

## Financial Health
### P&L Summary
[Revenue to Gross Profit to EBITDA waterfall narrative]
### Balance Sheet Highlights
[Working capital, inventory, cash position]

## Risk Register Update
| Risk | Probability | Impact | Trend | Mitigation |
|------|------------|--------|-------|------------|

## Appendix: KPI Definitions
[Precise definitions for all non-standard metrics used]
```

## Analysis Framework

**Balanced Scorecard Integration**: Organize narratives across four perspectives:

| Perspective | Example KPIs | Strategic Pillar Link |
|-------------|-------------|----------------------|
| Financial | Revenue growth, EBITDA margin, ROIC | Profitable Growth |
| Customer | NPS, market share, distribution points | Brand Leadership |
| Process | Fill rate, inventory turns, speed-to-shelf | Operational Excellence |
| Learning | Innovation pipeline, capability build | Future Readiness |

**Contribution Margin Analysis**: For brand/channel narratives, decompose contribution:
```
Net Revenue
  - COGS (variable)
  = Contribution Margin I
  - Trade Spend
  = Contribution Margin II
  - Brand Investment (A&P)
  = Contribution Margin III (Brand P&L)
```

## Example

**Input KPI**: Revenue $142M vs $150M plan (-5.3%), prior year $128M (+10.9% YoY)

**Board narrative**:
> "Q3 net revenue of $142M grew 10.9% year-over-year, reflecting continued momentum in the Club channel (+18%) and the successful national launch of the Plant-Based line ($8.2M incremental). The result fell 5.3% below plan, primarily attributable to (1) delayed Walmart shelf reset timing, which shifted ~$5M into Q4 (confirmed via revised PO schedule), (2) lower-than-modeled promotional lift on the back-to-school campaign, and (3) a 200bps headwind from unfavorable regional mix. Management has accelerated the Walmart reset to early October and revised Q4 promotional depth to recover the shortfall. We expect full-year revenue within the $560-575M guided range, contingent on Holiday promotional execution."

## Guidelines

- Never present a miss without a recovery narrative and timeline
- Always decompose variances into volume, price, and mix components
- Include "quality of revenue" commentary — is growth sustainable or pull-forward?
- Use consistent KPI definitions across periods; flag any methodology changes
- Apply appropriate rounding: Revenue to $M with 1 decimal; margins to 1 decimal %
- Ensure every forward-looking statement is qualified with assumptions
- Include Non-GAAP to GAAP reconciliation references where applicable

## Validation Checklist

- [ ] Every narrated KPI maps to a strategic pillar
- [ ] Materiality filter applied — no immaterial metrics narrated
- [ ] Variances decomposed into 3 or fewer ranked root causes
- [ ] Forward-looking statements include assumptions and caveats
- [ ] Consistent definitions with prior period narrative
- [ ] DuPont decomposition applied to return metrics
- [ ] Tone is factual, balanced, and free of promotional language
- [ ] Risk register updated with probability/impact/trend
- [ ] Non-GAAP metrics reconciled or referenced
- [ ] Appendix includes KPI definitions for non-standard metrics
