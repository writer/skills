---
name: credit-risk-explanation
description: Explain credit risk drivers, scoring methodologies, and loss estimation for lending portfolios. Use when analyzing borrower creditworthiness, PD/LGD/EAD components, CECL/IFRS 9 expected credit loss calculations, credit rating migrations, or risk-adjusted pricing decisions.

metadata:
  display_name: "Credit Risk Explanation"
  short_description: "Explain credit risk drivers, scoring, and loss estimation"
  default_prompt: "Explain my credit risk in simple words and next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Credit Risk Explanation

## Overview

This skill produces clear, regulator-ready explanations of credit risk drivers for consumer and commercial lending portfolios. It covers probability of default (PD), loss given default (LGD), exposure at default (EAD), expected credit loss (ECL) under CECL (ASC 326) and IFRS 9, internal rating systems, and risk-adjusted return on capital (RAROC) pricing.

## When to Use

- Explaining why a borrower's internal risk rating changed
- Interpreting credit scorecard outputs (application or behavioral)
- Drafting ECL methodology narratives for 10-K/10-Q disclosures
- Summarizing credit migration trends for portfolio reviews
- Supporting credit committee memos with risk factor analysis
- Documenting model inputs and assumptions for examiner inquiries
- Translating quantitative risk metrics into business-language narratives

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Borrower/segment data | Financials, scores, collateral, industry | Structured data or summary |
| Risk rating or score | Internal grade, FICO, or scorecard output | Numeric or alphanumeric |
| Portfolio context | Asset class, vintage, geography | Text description |
| Regulatory framework | CECL, IFRS 9, Basel III/IV, or internal | Specification |
| Time horizon | Reporting period, forecast window | Date range |
| Macro scenario (if applicable) | Baseline, adverse, severely adverse | Scenario parameters |

## Methodology

### Step 1: Identify the Credit Risk Question

Classify the request into one of these categories:
- **Borrower-level**: Individual obligor rating rationale, scorecard factor attribution
- **Segment-level**: Portfolio concentration, migration trends, vintage analysis
- **Loss estimation**: ECL calculation walkthrough (PD × LGD × EAD), qualitative adjustments
- **Pricing**: Risk-adjusted spread, RAROC, hurdle rate justification
- **Regulatory**: Disclosure narrative, model documentation, examiner response

### Step 2: Decompose Risk Drivers

Break credit risk into its component drivers using the following hierarchy:

1. **Obligor risk factors**: Financial leverage (Debt/EBITDA), liquidity (current ratio), profitability (DSCR, interest coverage), management quality, industry outlook
2. **Facility risk factors**: Collateral type and coverage (LTV), seniority, covenants, guarantees, maturity
3. **Portfolio risk factors**: Concentration (single-name, industry, geographic), correlation, diversification benefit
4. **Macroeconomic factors**: GDP growth, unemployment rate, HPI, interest rates, credit spreads
5. **Qualitative overlays**: Management judgment adjustments per CECL Q-factor framework

### Step 3: Map to Regulatory Framework

Apply the appropriate regulatory lens:

**CECL (ASC 326)**:
- Lifetime expected loss from origination
- Reasonable and supportable forecast period + historical reversion
- Segmentation by shared risk characteristics
- Qualitative adjustment factors (Q-factors) with documented rationale

**IFRS 9**:
- Three-stage impairment: Stage 1 (12-month ECL), Stage 2 (lifetime ECL, performing), Stage 3 (lifetime ECL, credit-impaired)
- Significant increase in credit risk (SICR) assessment criteria
- Forward-looking information incorporation

**Basel III/IV**:
- IRB PD, LGD, EAD parameter estimation
- Risk-weight formulas and capital requirement calculations
- Standardized approach floor (72.5% output floor under Basel IV)
- Credit risk mitigation (CRM) techniques

### Step 4: Construct the Narrative

Build the explanation following this structure:

1. **Context statement**: Portfolio/borrower identification and reporting period
2. **Risk assessment summary**: Current rating/score with directional trend
3. **Key driver analysis**: Top 3-5 factors ordered by materiality with quantification
4. **Migration analysis**: Rating/score movement vs. prior period with drivers of change
5. **Loss estimate walkthrough**: ECL components with assumptions stated explicitly
6. **Outlook and watchlist**: Forward-looking risk indicators and early warning signals

### Step 5: Apply Quantitative Rigor

Every assertion must be supported by data:
- Use basis-point precision for loss rates and spreads
- Express concentrations as percentages of total exposure
- Show vintage curves with delinquency and loss progression
- Present sensitivity analysis: "A 100bp increase in PD would increase ECL by $X"
- Compare current metrics to historical averages, peer benchmarks, and policy limits

### Step 6: Address Model and Data Limitations

Document known limitations transparently:
- Model performance metrics (Gini, KS, accuracy ratio) and validation outcomes
- Data gaps and their impact on estimation uncertainty
- Assumption sensitivity (e.g., prepayment rates, recovery timing)
- Override rates and their directional impact on risk estimates

### Step 7: Validate Completeness

Cross-check the explanation against:
- OCC Comptroller's Handbook for Credit Risk
- SR 11-7 (model risk management) requirements for documented rationale
- FASB ASC 326-20 disclosure requirements
- Institution's credit risk policy and appetite statement

## Output Specification

```markdown
# Credit Risk Analysis: [Borrower/Segment Name]

## Executive Summary
[2-3 sentence overview: current risk posture, direction, key concern or strength]

## Risk Rating Assessment
- **Current Rating**: [Rating] ([PD range])
- **Prior Rating**: [Rating] ([PD range])
- **Rating Direction**: [Upgrade/Stable/Downgrade]
- **Rating Date**: [Date]

## Key Risk Drivers
| Driver | Current | Prior Period | Trend | Materiality |
|--------|---------|--------------|-------|-------------|
| [Driver 1] | [Value] | [Value] | [↑↓→] | [High/Med/Low] |

## Expected Credit Loss
| Component | Value | Methodology |
|-----------|-------|-------------|
| PD | [X.XX%] | [Model/approach] |
| LGD | [X.XX%] | [Model/approach] |
| EAD | [$XXM] | [Calculation basis] |
| ECL | [$XXM] | PD × LGD × EAD [+ qualitative] |

## Forward-Looking Assessment
[Macro scenario impact, early warning indicators, recommended actions]

## Limitations and Caveats
[Model limitations, data quality issues, assumption sensitivities]
```

## Analysis Framework

### Credit Scorecard Factor Attribution

When explaining scorecard outputs, decompose the score into factor contributions:
- List each scorecard variable, its value, points contributed, and direction of risk
- Identify the top positive and negative contributors
- Compare variable values to population medians and cutoff thresholds
- Flag any variables near decision boundaries that could shift the outcome

### Portfolio Concentration Analysis

Apply the Herfindahl-Hirschman Index (HHI) and single-name concentration metrics:
- HHI by industry (NAICS 2-digit), geography, obligor
- Top 10/20 exposure concentration ratios
- Compare to regulatory guidance thresholds (OCC large bank concentration limits)

### Vintage Analysis

Structure loss progression by origination cohort:
- Cumulative net charge-off rates by vintage at 12, 24, 36, 48 months
- Compare current vintage performance to historical benchmarks
- Identify vintages exhibiting adverse selection or underwriting drift

## Examples

**Example 1 — Borrower Downgrade Explanation**:
"Borrower XYZ was downgraded from Risk Rating 5 (Pass) to Risk Rating 6 (Special Mention) effective Q3 2025. The downgrade reflects deterioration in debt service coverage to 1.05x (from 1.35x in Q2 2025, policy minimum 1.20x), driven by a 12% revenue decline in the regional retail sector. Leverage increased to 4.8x Debt/EBITDA (from 3.9x), exceeding the 4.0x covenant threshold. Collateral coverage remains adequate at 1.45x LTV. Management has submitted a turnaround plan; however, the 90-day cure period has not yet elapsed."

**Example 2 — CECL ECL Narrative**:
"The allowance for credit losses on the commercial real estate portfolio increased $4.2M (18%) to $27.5M as of Q4 2025. The increase was driven by: (1) a 45bp upward adjustment to the baseline PD curve reflecting rising vacancy rates in the office subsegment; (2) incorporation of the Moody's December 2025 baseline forecast projecting 5.2% unemployment through Q2 2026; and (3) a $1.1M qualitative overlay for CRE office exposure in three metro areas with vacancy rates exceeding 20%. The reasonable and supportable forecast period remains two years with a one-year straight-line reversion to historical loss rates."

## Guidelines

- Always state whether PD is point-in-time (PIT) or through-the-cycle (TTC)
- Distinguish between regulatory capital (Basel) and accounting reserves (CECL/IFRS 9)
- Use institution-specific rating scales; map to agency equivalents only for context
- Present loss estimates as ranges when uncertainty is material
- Flag any data older than 90 days as potentially stale
- Reference specific policy sections and regulatory guidance by citation
- Avoid unsupported opinions; every risk statement requires quantitative backing
- Use consistent units (dollars in millions, rates in basis points or percentages)

## Validation Checklist

- [ ] Risk rating rationale cites specific financial metrics with values
- [ ] ECL components (PD, LGD, EAD) are individually stated and sourced
- [ ] Macro scenario assumptions are identified by name and date
- [ ] Qualitative adjustments have documented rationale and directional impact
- [ ] Regulatory framework (CECL/IFRS 9/Basel) is explicitly identified
- [ ] Forward-looking statements are labeled as projections, not assertions
- [ ] Limitations section addresses model performance and data quality
- [ ] All figures reconcile to source data with stated as-of dates
- [ ] Narrative avoids jargon inappropriate for the target audience
- [ ] Analysis is consistent with the institution's credit risk appetite statement
