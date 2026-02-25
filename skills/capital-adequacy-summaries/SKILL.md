---
name: capital-adequacy-summaries
description: Summarize capital adequacy positions including CET1, Tier 1, Total Capital ratios, RWA decomposition, leverage ratio, and capital planning. Use when preparing capital reports, explaining ICAAP narratives, analyzing RWA movements, or summarizing capital buffer compliance for ALCO or board reporting.

metadata:
  display_name: "Capital Adequacy Summaries"
  short_description: "Summarize capital adequacy ratios and regulatory buffers"
  default_prompt: "Summarize my capital adequacy with key findings and next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Capital Adequacy Summaries

## Overview

Generates structured, regulator-ready summaries of the bank's capital position covering CET1/Tier 1/Total Capital ratios, RWA composition and movement, leverage ratio, capital buffers (CCB, CCyB, G-SIB/D-SIB), and forward capital planning under stress. Designed for ALCO reporting, board risk committee presentations, ICAAP narratives, and investor communications.

## When to Use

- Preparing quarterly capital adequacy reports for ALCO or board
- Drafting ICAAP narrative sections on capital adequacy and planning
- Explaining period-over-period movements in capital ratios
- Analyzing RWA density and optimization opportunities
- Assessing capital buffer compliance and distribution constraints
- Supporting stress testing capital projections and management actions

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Capital components | CET1, AT1, Tier 2 capital with regulatory adjustments | Detailed breakdown |
| RWA breakdown | Credit risk, market risk, operational risk RWA by approach | Category-level data |
| Leverage exposure | Total leverage exposure measure and Tier 1 capital | Numeric |
| Buffer requirements | CCB, CCyB, G-SIB/D-SIB buffer rates | Percentage requirements |
| Prior period data | Previous quarter capital ratios and RWA for trend analysis | Same format |
| Stress test results | Capital ratios under adverse/severely adverse scenarios | Scenario-outcome pairs |
| Capital plan | Dividend, buyback, issuance, and organic capital generation assumptions | Forward projections |
| Peer data | Peer group capital ratios for benchmarking | Comparable ratios |

## Methodology

### Step 1 — Compile the Capital Stack

Build the regulatory capital waterfall:

**CET1 Capital:**
- Common shares and share premium
- Retained earnings
- Accumulated other comprehensive income (AOCI) — note AOCI opt-out elections if applicable
- Minus: Goodwill and intangibles (net of deferred tax)
- Minus: Deferred tax assets exceeding 10%/15% thresholds
- Minus: Investments in financial institutions (reciprocal, non-significant, significant)
- Minus: Other regulatory deductions (expected loss shortfall, securitization deductions)

**Additional Tier 1 (AT1):** Qualifying perpetual instruments with loss absorption triggers (CET1 trigger ≥ 5.125%)

**Tier 2 Capital:** Qualifying subordinated debt (minimum 5-year original maturity, amortized in final 5 years), eligible general provisions (up to 1.25% of credit risk RWA under standardized approach)

### Step 2 — Decompose Risk-Weighted Assets

Break down total RWA by risk type and sub-category:

**Credit risk RWA** (typically 80-90% of total):
- By approach: Standardized (SA) vs. Internal Ratings-Based (IRB: Foundation or Advanced)
- By asset class: Sovereign, institution, corporate, retail (mortgage, qualifying revolving, other), equity, securitization
- RWA density (RWA / Exposure at Default) by asset class to identify heavy vs. light portfolios

**Market risk RWA** (typically 3-8%):
- Standardized approach vs. Internal Models Approach (IMA)
- By risk factor: interest rate, equity, FX, commodity, credit spread (FRTB SA-specific)
- Stressed VaR and incremental risk charge contributions

**Operational risk RWA** (typically 8-15%):
- Basic Indicator, Standardized, or Advanced Measurement Approach
- Business Indicator Approach (BIA) under Basel III finalization

**Credit valuation adjustment (CVA) RWA**: Mark-to-market counterparty credit risk on derivatives

### Step 3 — Calculate Ratios and Buffer Compliance

Compute regulatory ratios:
- **CET1 ratio** = CET1 Capital / Total RWA
- **Tier 1 ratio** = (CET1 + AT1) / Total RWA
- **Total Capital ratio** = (CET1 + AT1 + Tier 2) / Total RWA
- **Leverage ratio** = Tier 1 Capital / Leverage Exposure Measure (target ≥ 3%)

Assess buffer compliance:
- **Pillar 1 minimums**: CET1 ≥ 4.5%, Tier 1 ≥ 6.0%, Total Capital ≥ 8.0%
- **Capital Conservation Buffer (CCB)**: 2.5% CET1
- **Countercyclical Buffer (CCyB)**: Jurisdiction-weighted average (0-2.5% CET1)
- **G-SIB / D-SIB surcharge**: Institution-specific (1-3.5% CET1)
- **Combined buffer requirement (CBR)** = CCB + CCyB + G-SIB/D-SIB
- **Maximum Distributable Amount (MDA)**: If CET1 falls within CBR, dividend and AT1 coupon restrictions apply proportionally

### Step 4 — Analyze Period-over-Period Movements

Decompose capital ratio changes into:
- **Numerator effects** (ΔCapital):
  - Organic capital generation: Net income − Dividends − Share buybacks
  - AOCI movements (unrealized gains/losses on AFS securities, pension adjustments)
  - Regulatory deduction changes (goodwill from acquisitions, DTA movements)
  - Issuance or redemption of AT1/Tier 2 instruments
- **Denominator effects** (ΔRWA):
  - Asset growth/contraction effect
  - Credit quality migration (rating upgrades/downgrades in IRB portfolios)
  - Model updates or recalibration
  - Regulatory methodology changes
  - Securitization or risk transfer transactions

### Step 5 — Stress Test Capital Trajectory

Present capital projections under stress scenarios:
- **Base case**: Business-as-usual with plan assumptions
- **Adverse**: Moderate economic downturn (200-300bps GDP decline)
- **Severely adverse**: Severe recession (400bps+ GDP decline, 30%+ equity market decline, credit spread widening)

For each scenario, project:
- Pre-provision net revenue (PPNR) trajectory
- Credit loss projections by portfolio
- RWA migration under stressed PDs and LGDs
- Capital ratio trajectory over 9-quarter (CCAR) or 3-year (EBA) horizon
- Minimum capital ratio reached (trough) and quarter in which it occurs
- Distance to MDA trigger at trough

### Step 6 — Assess Capital Optimization Opportunities

Identify levers to improve capital efficiency:
- **RWA optimization**: Credit risk mitigation (guarantees, collateral, netting), securitization, portfolio rebalancing toward lower-density asset classes
- **Capital structure optimization**: Replace expensive equity with AT1 or Tier 2 where capacity exists
- **Model enhancements**: IRB model recalibration, data quality improvements reducing conservatism
- **Exposure management**: Active credit portfolio management, loan sales, synthetic risk transfer
- Quantify each opportunity in bps of CET1 ratio improvement and dollar RWA reduction

### Step 7 — Construct the Executive Summary

Synthesize into a structured narrative:
1. **Headline ratios**: Current CET1, Tier 1, Total Capital, Leverage ratios with trend direction
2. **Key movements**: Top 3-5 drivers of ratio change with quantified impacts
3. **Buffer compliance**: Distance to MDA restriction in bps and absolute terms
4. **Stress resilience**: Trough CET1 under severely adverse with distance to minimum
5. **Capital actions**: Planned dividends, buybacks, issuance, and their ratio impact
6. **Peer positioning**: Ranking relative to peers on CET1 and leverage ratio
7. **Outlook and risks**: Known upcoming impacts (regulatory changes, model approvals, planned transactions)

## Output Specification

```markdown
# Capital Adequacy Summary — [Period]

## Headline Ratios
| Metric | Current | Prior Qtr | Δ (bps) | Requirement | Buffer |
|--------|---------|-----------|---------|-------------|--------|
| CET1 Ratio | | | | | |
| Tier 1 Ratio | | | | | |
| Total Capital Ratio | | | | | |
| Leverage Ratio | | | | | |

## CET1 Movement Waterfall
Prior CET1: [X]%
→ Organic capital generation: +[A]bps
→ Dividends/buybacks: -[B]bps
→ AOCI movement: +/-[C]bps
→ RWA growth: -[D]bps
→ Other regulatory deductions: +/-[E]bps
= Current CET1: [Y]%

## RWA Composition
| Risk Type | RWA ($B) | % of Total | Δ vs Prior | RWA Density |
|-----------|----------|------------|------------|-------------|

## Buffer Compliance
| Buffer | Required | Available CET1 above P1 Min | Status |
|--------|----------|----------------------------|--------|

## Stress Test Capital Trajectory
| Scenario | Starting CET1 | Trough CET1 | Trough Quarter | Distance to MDA |
|----------|---------------|-------------|----------------|-----------------|

## Capital Plan
| Action | Timeline | CET1 Impact (bps) |
|--------|----------|--------------------|

## Peer Comparison
| Institution | CET1 | Leverage | RWA Density |
|-------------|-------|----------|-------------|
```

## Analysis Framework

Apply the **Capital Adequacy Triangle**:
1. **Regulatory compliance**: Meeting minimum ratios plus buffer requirements without distribution restrictions
2. **Stress resilience**: Maintaining adequate capital through severe but plausible stress scenarios
3. **Strategic capacity**: Retaining sufficient headroom to fund organic growth, M&A, and shareholder returns

All three dimensions must be satisfied simultaneously; optimizing one at the expense of others creates vulnerability.

## Examples

**Example — CET1 Improvement Narrative:**
"CET1 strengthened 32bps to 13.2% in Q3, driven by organic capital generation of +48bps ($1.9B retained earnings after dividends) partially offset by RWA growth of -22bps from $8.4B of commercial loan originations (average RWA density 72%). The ratio stands 420bps above the MDA trigger of 8.98% (P1 minimum 4.5% + CCB 2.5% + G-SIB 1.5% + CCyB 0.48%), providing $16.7B of distributable capital capacity."

**Example — Stress Resilience Statement:**
"Under the severely adverse scenario, CET1 declines from 13.2% to a trough of 9.8% in Q6, driven by $7.2B of projected credit losses (primarily CRE and leveraged lending) and $2.1B of AOCI deterioration on the AFS portfolio. The trough ratio remains 82bps above the MDA trigger, confirming the capital plan's sustainability through severe stress without distribution restrictions."

## Guidelines

- Always present the full capital stack (CET1, Tier 1, Total Capital) not just CET1
- Include the leverage ratio alongside risk-based ratios
- Express buffer compliance in both bps and absolute dollar terms
- Decompose ratio movements into numerator and denominator effects separately
- Include MDA trigger calculation and distance to restriction
- Use consistent RWA density metrics (RWA/EAD) for cross-portfolio comparability
- State all ratios on a transitional and fully-loaded basis where AOCI phase-in applies

## Validation Checklist

- [ ] Capital components reconcile to published regulatory returns
- [ ] RWA by risk type sums to total RWA
- [ ] Ratios calculated correctly (numerator/denominator)
- [ ] Buffer requirements reflect current jurisdiction-specific rates
- [ ] MDA trigger computed correctly as sum of P1 minimum + CCB + CCyB + G-SIB/D-SIB
- [ ] CET1 waterfall components sum to actual Δ in ratio
- [ ] Stress test trough compared to both MDA trigger and P1 minimum
- [ ] Peer comparison uses consistent ratio definitions (transitional vs. fully loaded)
- [ ] Capital plan actions quantified with ratio impact
- [ ] Forward-looking statements qualified with assumptions
