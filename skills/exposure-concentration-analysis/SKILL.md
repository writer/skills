---
name: exposure-concentration-analysis
description: Analyze portfolio concentration risks across borrower, industry, geography, product, and collateral dimensions. Use when monitoring regulatory concentration limits, preparing board risk reports, conducting CRE concentration analysis per SNC/interagency guidance, evaluating single-name exposure, or stress testing portfolio concentrations under adverse scenarios.

metadata:
  display_name: "Exposure Concentration Analysis"
  short_description: "Analyze lending portfolio concentration by sector and name"
  default_prompt: "Analyze my exposure concentration and recommend clear next actions"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Exposure Concentration Analysis

## Overview

Measure, monitor, and report portfolio concentration risks across multiple dimensions. This skill applies regulatory concentration frameworks (interagency CRE guidance, large exposure rules, single-borrower lending limits) and internal risk appetite thresholds to identify excessive concentrations that could amplify losses during stress events. Outputs include concentration dashboards, limit monitoring reports, diversification metrics, and concentration stress testing results.

## When to Use

- Monitoring regulatory concentration thresholds (CRE/ADC 100%/300% of capital)
- Evaluating single-name and connected-borrower exposure limits
- Preparing concentration risk sections for board and risk committee reporting
- Conducting stress tests on concentrated portfolio segments
- Analyzing industry/sector correlation risk during economic downturns
- Assessing geographic concentration in areas with localized economic stress
- Evaluating new loan originations for marginal concentration impact

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Loan portfolio | Full loan tape with balances, commitments, and utilization | Loan-level data |
| Borrower linkage | Connected borrower/guarantor relationship mapping | Entity hierarchy |
| Industry codes | NAICS/SIC codes for all commercial borrowers | Coded data |
| Geographic data | Property/borrower location at ZIP, MSA, state level | Address data |
| Capital data | Tier 1 capital, total capital, risk-based capital ratios | Call report data |
| Risk ratings | Internal risk grades for all facilities | Rating data |
| Collateral types | Collateral classification for secured facilities | Collateral data |
| Limits framework | Board-approved concentration limits by dimension | Policy document |

## Methodology

### Step 1 — Single-Name and Connected Borrower Analysis

Identify and aggregate exposure across connected entities:

- **Legal lending limit**: Verify no single borrower exceeds 15% of capital (unsecured) or 25% (fully secured) per 12 CFR 32
- **Connected borrower aggregation**: Link entities through common ownership (>50%), common control, financial interdependence, or guarantor relationships
- **Exposure measurement**: Sum funded outstandings + unfunded commitments × credit conversion factor (CCF)
- **Top exposures report**:
  - Top 10 individual borrowers with % of capital
  - Top 10 connected groups with % of capital
  - Trend analysis (quarter-over-quarter change in concentration)
- **Granularity assessment**: Calculate portfolio-level Herfindahl-Hirschman Index (HHI) and Gini coefficient

### Step 2 — CRE Concentration Analysis

Apply interagency CRE concentration guidance (2006 joint guidance, updated 2015):

- **CRE to capital ratio**: Total CRE loans / Total risk-based capital — flag if > 300%
- **ADC to capital ratio**: Acquisition, Development & Construction loans / Total risk-based capital — flag if > 100%
- **CRE sub-segment analysis**:

| CRE Segment | Outstanding ($M) | % of CRE Portfolio | % of Capital | Limit | Status |
|-------------|-----------------|-------------------|-------------|-------|--------|
| Multifamily | $XX | XX% | XXX% | XXX% | [G/Y/R] |
| Office | $XX | XX% | XXX% | XXX% | [G/Y/R] |
| Retail | $XX | XX% | XXX% | XXX% | [G/Y/R] |
| Industrial | $XX | XX% | XXX% | XXX% | [G/Y/R] |
| Hotel | $XX | XX% | XXX% | XXX% | [G/Y/R] |
| ADC | $XX | XX% | XXX% | XXX% | [G/Y/R] |

- **Growth rate**: CRE portfolio growth over 36 months — flag if > 50% cumulative
- **Supervisory expectations**: If CRE > 300% or ADC > 100%, document enhanced risk management practices per interagency guidance

### Step 3 — Industry/Sector Concentration Assessment

Evaluate diversification across economic sectors:

- **NAICS 2-digit sector distribution**: Aggregate exposure by major sector
- **Sector concentration limits**: Compare to board-approved limits (typically 15%–25% of portfolio per sector)
- **Correlation analysis**: Identify sectors with high economic correlation that compound concentration risk
  - Example: CRE office + professional services have correlated downturns
  - Example: Energy + energy-dependent regional economies
- **Sector trend monitoring**: Quarter-over-quarter exposure changes by sector with commentary on growth drivers
- **Sector risk rating**: Calculate weighted average risk grade by sector to identify quality concentration

### Step 4 — Geographic Concentration Assessment

Measure geographic diversification:

- **State-level distribution**: Exposure by state with percentage of portfolio and capital
- **MSA-level concentration**: Identify MSAs representing >10% of portfolio
- **Economic dependency assessment**: For concentrated geographies, assess:
  - Employment base diversification
  - Major employer dependency
  - Home price trends and housing supply
  - Population and income growth trajectory
- **HHI by geography**: Calculate and track diversification index
- **Regulatory perspective**: Institutions with >75% of exposure in a single state or >50% in a single MSA warrant enhanced geographic monitoring

### Step 5 — Product and Collateral Concentration

Analyze concentration by product type and collateral:

- **Product mix**: Distribution across product types (C&I term, revolver, CRE, construction, consumer, residential)
- **Fixed vs. variable rate**: Interest rate exposure concentration
- **Maturity distribution**: Concentration of maturities in any single period (refinance/rollover risk)
- **Collateral type distribution**: Real estate, equipment, receivables, unsecured, mixed
- **Collateral value concentration**: Geographic or property-type clustering of collateral values
- **Cross-collateralization**: Identify pools where collateral failure affects multiple facilities

### Step 6 — Concentration Stress Testing

Stress test concentrated segments:

- **Single-name stress**: Model the impact of the top 5 individual borrower defaults on capital ratios
- **Sector stress**: Apply sector-specific PD shocks (2x–5x base PD) to concentrated sectors
- **Geographic stress**: Model localized recession impact on concentrated geographies
  - Apply regional unemployment increase of 300–500 bps
  - Apply property value decline of 15%–30% in concentrated markets
- **CRE stress**: Apply cap rate expansion of 100–200 bps and NOI decline of 10%–20%
- **Correlated stress**: Model simultaneous stress across correlated concentrations

Calculate capital impact under each scenario: incremental provision required, impact on CET1 and total capital ratios, and distance to well-capitalized thresholds.

### Step 7 — Reporting and Limit Monitoring

Generate comprehensive concentration reporting:

- **Traffic-light dashboard**: Green (within limits), Yellow (approaching limits — within 10%), Red (at or exceeding limits)
- **Trend analysis**: 8-quarter trend for all concentration metrics
- **New origination impact**: Prospective analysis of how pending approvals will affect concentrations
- **Limit breach escalation**: Automatic notification to risk committee when limits are breached or approached
- **Remediation tracking**: For existing breaches, document the remediation plan and timeline
- **Peer benchmarking**: Compare concentration metrics to peer group (UBPR/FFIEC data)

## Output Specification

```
## Portfolio Concentration Analysis — [Period]

### Executive Dashboard
| Dimension | Metric | Current | Limit | Status | Trend |
|-----------|--------|---------|-------|--------|-------|
| CRE/Capital | CRE ratio | XXX% | 300% | [G/Y/R] | [↑↓→] |
| ADC/Capital | ADC ratio | XXX% | 100% | [G/Y/R] | [↑↓→] |
| Top borrower | % of capital | XX% | 25% | [G/Y/R] | [↑↓→] |
| Top sector | % of portfolio | XX% | 25% | [G/Y/R] | [↑↓→] |
| Top MSA | % of portfolio | XX% | XX% | [G/Y/R] | [↑↓→] |
| HHI (borrower) | Index | X,XXX | X,XXX | [G/Y/R] | [↑↓→] |

### Top Exposures
| Rank | Borrower/Group | Outstanding ($M) | Committed ($M) | % Capital | Rating |
|------|---------------|-----------------|----------------|-----------|--------|
| 1 | [Name] | $XX | $XX | XX% | [Grade] |

### Sector Distribution
[Table of NAICS sector exposures with percentages and limits]

### Geographic Distribution
[Table of state/MSA exposures with percentages and limits]

### CRE Detailed Analysis
[Sub-segment breakdown with capital ratios and growth rates]

### Stress Test Results
| Scenario | Incremental Loss ($M) | Capital Impact (bps) | Post-Stress CET1 |
|----------|----------------------|---------------------|--------------------|
| [Scenario] | $XX | -XX bps | XX.X% |

### Limit Breaches and Remediation
| Dimension | Breach | Magnitude | Remediation Plan | Target Date |
|-----------|--------|-----------|-----------------|-------------|
| [Dim] | [Detail] | [X% over] | [Plan] | [Date] |
```

## Analysis Framework

Apply the **CRISP** framework:

- **C**oncentration measurement — Quantify exposure across all dimensions
- **R**egulatory benchmarking — Compare against supervisory thresholds and guidance
- **I**nterdependency — Identify correlated concentrations that compound risk
- **S**tress testing — Model loss impact of concentrated segment deterioration
- **P**olicy monitoring — Track limits, breaches, and remediation continuously

## Examples

**Example 1 — CRE Concentration Approaching Limit**

Finding: CRE-to-capital ratio is 285% (limit 300%). Office sub-segment is 38% of CRE book and has experienced 12% growth in 2 quarters. Three new office deals in pipeline totaling $18M would push ratio to 308%. Recommendation: Pause new office originations, require credit committee approval for any CRE deal >$2M, present remediation plan showing path back to 275% within 4 quarters through planned payoffs and portfolio sales.

**Example 2 — Single-Sector Correlation Risk**

Finding: Energy sector is 22% of C&I portfolio (limit 20%). Oil-field services sub-sector is 8%. Additionally, Houston MSA is 28% of total portfolio. Correlation analysis shows 0.82 correlation between energy sector loan performance and Houston MSA overall loan performance. Effective combined concentration is significantly higher than individual metrics suggest. Recommendation: Reduce explicit energy exposure to 15%, apply geographic overlay stress test combining energy downturn with Houston economic scenario, increase reserves for the correlated segment.

## Guidelines

- Use committed exposure (funded + unfunded × CCF) as the primary concentration measure
- Update concentration reports at least quarterly; monthly for breached limits
- Apply connected borrower rules consistently — document linkage criteria and methodology
- Use NAICS codes at the 3-digit level for sector concentration (2-digit is too coarse)
- Include off-balance-sheet items (letters of credit, derivatives) in exposure calculations
- Document the methodology for any concentration exemptions or exclusions
- Present concentration metrics alongside the trend — a static snapshot is insufficient
- Coordinate with the strategic plan — growth targets must be consistent with concentration limits

## Validation Checklist

- [ ] Connected borrower linkages are complete and current
- [ ] Exposure calculations include both funded and unfunded (with appropriate CCF)
- [ ] CRE definitions align with regulatory definition (not internal product codes)
- [ ] Industry codes are assigned at 3-digit NAICS level and validated for accuracy
- [ ] Geographic aggregation uses property location (not borrower HQ) for real estate
- [ ] Concentration limits reflect current board-approved risk appetite
- [ ] Stress test scenarios are severe but plausible and internally consistent
- [ ] Capital impact calculations use current capital levels and risk-weighted assets
- [ ] Peer benchmarking data is current and uses appropriate peer group
- [ ] Limit breaches trigger documented escalation and remediation tracking
