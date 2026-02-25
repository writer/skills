---
name: stress-test-scenario-narratives
description: Explain stress test scenarios, assumptions, and results for CCAR/DFAST and internal capital adequacy assessments. Use when drafting scenario narratives, interpreting stress test outputs, preparing board submissions, or documenting capital planning assumptions for supervisory stress testing programs.

metadata:
  display_name: "Stress Test Scenario Narratives"
  short_description: "Write CCAR/DFAST stress test scenario narratives for banks"
  default_prompt: "Summarize my stress test scenario with key findings and next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Stress Test Scenario Narratives

## Overview

This skill produces clear, regulator-ready narratives for stress testing programs including CCAR (Comprehensive Capital Analysis and Review), DFAST (Dodd-Frank Act Stress Test), and internal capital adequacy assessment processes (ICAAP). It covers macroeconomic scenario design, loss and revenue projection explanations, capital impact analysis, and post-stress capital ratio interpretation. Output aligns with Federal Reserve SR 15-18 and SR 15-19 capital planning guidance.

## When to Use

- Drafting macroeconomic scenario narratives for supervisory and internal stress tests
- Explaining pre-provision net revenue (PPNR) projections under stress
- Interpreting credit loss projections by portfolio segment
- Documenting capital action assumptions and post-stress capital ratios
- Preparing board risk committee materials for capital plan approval
- Responding to supervisory feedback on stress testing methodology
- Supporting mid-cycle stress test analysis and sensitivity testing

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Scenario variables | GDP, unemployment, HPI, CRE index, rates, spreads | Macro forecast tables |
| Projection horizon | Typically 9 quarters (CCAR/DFAST) or custom | Time horizon |
| Portfolio data | Loan balances, securities, trading positions by segment | As-of-date snapshots |
| Loss projections | ECL, charge-offs, provisions by segment under each scenario | Model output |
| Revenue projections | NII, non-interest income, non-interest expense under stress | Model output |
| Capital ratios | CET1, Tier 1, Total, leverage — pre-stress and post-stress | Calculation output |
| Capital actions | Dividends, buybacks, issuances assumed under stress | Capital plan |

## Methodology

### Step 1: Describe the Scenario Design

Narrate each scenario's macroeconomic storyline:

**Baseline scenario**: Reflects consensus economic forecast
- GDP growth trajectory, inflation path, unemployment trend
- Interest rate path (fed funds, 10-year Treasury, mortgage rates)
- Asset price assumptions (equity markets, HPI, CRE price index)
- Source: Federal Reserve supervisory scenarios or internal economics team

**Adverse scenario**: Moderate recession
- Recession depth and duration (peak-to-trough GDP decline, unemployment peak)
- Asset price declines (peak-to-trough equity market, HPI, CRE)
- Interest rate environment (rate cuts, yield curve shape)
- Key differentiators from severely adverse

**Severely adverse scenario**: Deep recession with financial market stress
- Severe recession characteristics (comparable historical period)
- Financial market dislocation (credit spread widening, VIX spike, liquidity stress)
- Global dimensions (international GDP, trade, emerging market stress)
- Recovery path and speed

For each scenario, present the key variables in a summary table:

| Variable | Current | Baseline Peak/Trough | Adverse Peak/Trough | Severely Adverse Peak/Trough |
|----------|---------|---------------------|---------------------|------------------------------|
| Real GDP growth (Q4/Q4) | [X%] | [X%] | [X%] | [X%] |
| Unemployment rate (peak) | [X%] | [X%] | [X%] | [X%] |
| HPI change (trough) | — | [X%] | [X%] | [X%] |
| 10-year Treasury (trough) | [X%] | [X%] | [X%] | [X%] |
| BBB spread (peak) | [Xbps] | [Xbps] | [Xbps] | [Xbps] |

### Step 2: Explain Loss Projections

Narrate credit loss projections by portfolio segment:

For each material portfolio segment, document:
1. **Model methodology**: Model type (regression, transition matrix, vintage, roll-rate)
2. **Key loss drivers**: Which macro variables are most influential and why
3. **Loss projection path**: Quarterly loss trajectory (peak quarter, cumulative)
4. **Historical comparison**: How projected losses compare to actual losses in prior downturns (2008-2009 GFC, 2020 COVID)
5. **Conservatism assessment**: Where projections may be conservative or optimistic relative to model output

Structure the loss narrative by segment:

| Segment | 9Q Cumulative Loss Rate | Peak Quarter Loss Rate | Primary Driver | Historical Comparison |
|---------|------------------------|----------------------|----------------|----------------------|
| Residential mortgage | [X%] | [X%] Q[N] | HPI, unemployment | [vs. GFC: X%] |
| CRE | [X%] | [X%] Q[N] | CRE price index, vacancy | [vs. GFC: X%] |
| C&I | [X%] | [X%] Q[N] | GDP, BBB spreads | [vs. GFC: X%] |
| Credit card | [X%] | [X%] Q[N] | Unemployment, rates | [vs. GFC: X%] |
| Auto | [X%] | [X%] Q[N] | Unemployment, used car prices | [vs. GFC: X%] |

### Step 3: Explain Revenue Projections (PPNR)

Document pre-provision net revenue projections:

**Net interest income (NII)**:
- Balance sheet assumptions (growth/runoff under stress)
- Rate sensitivity (NII impact per 100bp rate change)
- Funding cost changes under stress (deposit beta, wholesale funding spread)
- Prepayment speed assumptions under different rate environments

**Non-interest income**:
- Fee income sensitivity to economic conditions and activity levels
- Trading revenue under market stress (P&L impact of market shocks)
- Mortgage banking revenue sensitivity to rate environment
- Wealth management/AUM sensitivity to equity market decline

**Non-interest expense**:
- Expense flexibility under stress (variable vs. fixed cost base)
- Litigation and remediation cost assumptions
- Severance and restructuring provisions
- Inflation assumptions for compensation and occupancy

### Step 4: Calculate Capital Impact

Walk through the capital waterfall from pre-stress to post-stress:

```
Pre-stress CET1 ratio:                    [X.X%]
  + PPNR (after tax)                      +[X.X%]
  − Provision for credit losses            −[X.X%]
  − Trading and counterparty losses        −[X.X%]
  − AOCI impact (AFS securities losses)   −[X.X%]
  − Capital actions (dividends, buybacks)  −[X.X%]
  + Other adjustments                      +/−[X.X%]
= Post-stress CET1 ratio (minimum):       [X.X%]
  vs. minimum requirement:                 [4.5%]
  Buffer above minimum:                    [X.X%]
```

Repeat for Tier 1, Total Capital, Leverage, and SLR (if applicable).

### Step 5: Interpret Results

Provide executive-level interpretation:
- **Adequacy assessment**: Do post-stress ratios exceed regulatory minimums with sufficient buffer?
- **Binding constraint**: Which capital ratio is most constraining under stress?
- **Loss drivers**: Which portfolio segments contribute most to stress losses?
- **Revenue offset**: How much loss absorption does PPNR provide?
- **Capital action capacity**: Can planned dividends and buybacks be sustained under stress?
- **Comparison to prior cycle**: How do results compare to last year's stress test?
- **Sensitivity**: What scenario assumptions would cause the binding ratio to breach minimums?

### Step 6: Address Supervisory Expectations

Ensure alignment with Federal Reserve guidance:
- **SR 15-18**: Capital planning and positions expectations
- **SR 15-19**: Federal Reserve supervisory assessment framework
- Stress capital buffer (SCB) calculation and interaction with planned distributions
- Qualitative assessment elements (governance, risk management, internal controls)
- Sensitivity analysis around key assumptions
- Reverse stress testing: identify scenarios that would breach capital minimums

### Step 7: Prepare Governance Documentation

Package the narrative for governance review:
- Board risk committee summary (2-3 page executive summary)
- Management-level detailed report with segment-level analysis
- Model methodology appendix with key assumption tables
- Sensitivity analysis results showing impact of alternative assumptions
- Year-over-year comparison highlighting material changes

## Output Specification

```markdown
# Stress Test Results Narrative: [Cycle Year]

## Scenario Overview
### [Scenario Name]
[2-3 paragraph storyline describing the macroeconomic environment]

### Key Variables
[Summary table of macro variables by scenario]

## Loss Projections
### Portfolio Summary
[Aggregate loss projection table by segment and scenario]

### Segment Analysis
[Detailed narrative for each material segment]

## Revenue Projections
### PPNR Summary
| Component | Baseline | Adverse | Severely Adverse |
|-----------|----------|---------|-------------------|
| NII | [$XM] | [$XM] | [$XM] |
| Non-interest income | [$XM] | [$XM] | [$XM] |
| Non-interest expense | -[$XM] | -[$XM] | -[$XM] |
| **PPNR** | **[$XM]** | **[$XM]** | **[$XM]** |

## Capital Impact
### Capital Waterfall
[Pre-stress to post-stress walkthrough by ratio]

### Post-Stress Capital Ratios
| Ratio | Pre-Stress | Minimum Under Stress | Quarter of Minimum | Regulatory Minimum | Buffer |
|-------|-----------|---------------------|-------------------|-------------------|--------|
| CET1 | [X.X%] | [X.X%] | Q[N] | 4.5% | [X.X%] |

## Key Findings
[Executive interpretation of results]

## Sensitivity Analysis
[Impact of alternative assumptions on key ratios]
```

## Analysis Framework

### Scenario Severity Benchmarking

Compare scenario severity against historical events:
- GFC (2007-2009): unemployment peak 10.0%, GDP decline -4.3%, HPI decline -27%
- COVID-19 (2020): unemployment peak 14.7%, GDP decline -9.0% (Q2 annualized), rapid recovery
- Dot-com/9-11 (2001-2002): mild recession, unemployment peak 6.3%, equity market -49%

### Reverse Stress Testing

Identify the break point:
- What unemployment rate would cause CET1 to breach the 4.5% minimum?
- What HPI decline would exhaust the CRE portfolio's loss absorption capacity?
- What combination of loss and revenue stress depletes the capital buffer?

## Examples

**Example 1 — Severely Adverse Scenario Narrative**:
"The severely adverse scenario contemplates a severe global recession triggered by a sharp correction in commercial real estate markets and tightening financial conditions. US real GDP declines 8.5% peak-to-trough over six quarters, with unemployment rising to 10.8% by Q7. The HPI declines 28% nationally, with CRE price indices falling 40%. The 10-year Treasury falls to 0.8%, compressing NIM, while BBB corporate spreads widen to 550bps. Equity markets decline 55% from peak. Under this scenario, the institution projects 9-quarter cumulative credit losses of $3.8B (cumulative loss rate of 6.2%), with CRE contributing 42% of total losses. PPNR of $2.1B partially offsets losses. Post-stress minimum CET1 ratio of 7.2% (Q6) provides a 270bp buffer above the 4.5% regulatory minimum."

**Example 2 — Capital Action Justification**:
"Under the severely adverse scenario, post-stress CET1 of 7.2% supports the proposed capital plan including $400M in common dividends and $200M in share repurchases. Eliminating the share repurchase would increase post-stress CET1 to 7.5% (+30bps). The stress capital buffer of 2.8% exceeds the 2.5% floor, resulting in a preliminary SCB of 2.8%. The planned payout ratio of 65% is sustainable under all three scenarios."

## Guidelines

- Use supervisory scenarios as published by the Federal Reserve; clearly distinguish from internal scenarios
- All projections must state the as-of date of the portfolio data
- Loss rate projections should be expressed as both percentages and dollar amounts
- Always show the quarter of minimum capital ratio, not just the minimum value
- Include AOCI impact for AFS securities portfolios, especially under rising rate scenarios
- Capital actions under stress should reflect the capital plan submitted to the Fed
- Sensitivity analysis must test at least 3 alternative assumptions
- Compare current cycle results to prior cycle to explain material changes
- Document all model overlays and management adjustments with rationale
- Clearly label projections as model outputs subject to uncertainty

## Validation Checklist

- [ ] All three scenarios (baseline, adverse, severely adverse) are narrated with economic storylines
- [ ] Key macro variables are presented in a comparative table
- [ ] Loss projections are broken out by material portfolio segment
- [ ] Historical loss comparisons provide context for projection reasonableness
- [ ] PPNR components (NII, non-interest income, expense) are individually addressed
- [ ] Capital waterfall shows the path from pre-stress to post-stress for all required ratios
- [ ] Post-stress minimums are shown with quarter of occurrence and buffer above regulatory minimum
- [ ] Sensitivity analysis tests alternative assumptions around key drivers
- [ ] Year-over-year comparison explains material changes from prior cycle
- [ ] Documentation is sufficient for board approval and supervisory review
