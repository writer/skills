---
name: early-delinquency-predictor
description: Predict early-stage default risk for individual loans and portfolio segments using behavioral, bureau, and macroeconomic signals. Use when building early warning systems, prioritizing loss mitigation outreach, forecasting delinquency pipelines, or identifying loans at risk of 30/60/90-day delinquency within the next 3–6 months.

metadata:
  display_name: "Early Delinquency Predictor"
  short_description: "Predict early-stage loan delinquency and default risk"
  default_prompt: "Review my early delinquency and highlight top risks and next actions"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Early Delinquency Predictor

## Overview

Identify loans at elevated risk of transitioning into delinquency before the first missed payment occurs. This skill combines behavioral payment signals, credit bureau trend data, macroeconomic overlays, and account-level risk characteristics to produce a probability-of-delinquency score. Outputs enable proactive loss mitigation outreach, reserve forecasting, and targeted collections resource allocation.

## When to Use

- Building or refining early warning systems for retail or commercial portfolios
- Prioritizing pre-delinquency outreach and borrower assistance programs
- Forecasting delinquency pipelines for reserve adequacy (CECL Stage 1 → Stage 2 migration)
- Evaluating loan modification or forbearance program targeting
- Identifying origination risk factors correlated with early payment default (EPD)
- Stress testing portfolio delinquency under adverse macroeconomic scenarios

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Payment history | Monthly payment records with amounts and dates | Time series |
| Bureau refreshes | Updated FICO, tradeline data, inquiry activity | Periodic pulls |
| Account attributes | Origination terms, current balance, rate, LTV | Loan-level data |
| Behavioral data | Login frequency, contact history, payment channel changes | CRM/servicing |
| Macro indicators | Unemployment rate, HPI, consumer confidence by geography | Economic feeds |
| Historical outcomes | Prior delinquency and default outcomes for model calibration | Performance data |

## Methodology

### Step 1 — Feature Engineering from Payment Behavior

Extract predictive signals from payment patterns before a missed payment occurs:

- **Payment timing drift**: Moving average of days-before-due-date trending toward due date or past it
- **Partial payment frequency**: Increasing incidence of payments below scheduled amount
- **Payment channel changes**: Shift from auto-pay to manual payment (disengagement signal)
- **Payment amount volatility**: Standard deviation of payment amounts over trailing 6 months
- **Excess payment cessation**: Borrower who previously paid above minimum now pays exactly minimum
- **NSF/returned payment history**: Any returned payments in trailing 12 months

### Step 2 — Bureau-Based Deterioration Signals

Identify credit deterioration from refreshed bureau data:

- **FICO score decline**: Drop of >20 points from origination or trailing 6-month trend
- **Utilization spike**: Revolving utilization increase >15 percentage points
- **New derogatory tradelines**: 30+ DPD on other accounts, collections, judgments
- **Inquiry velocity**: >3 new credit inquiries in 90 days (liquidity-seeking behavior)
- **New debt accumulation**: Significant increase in total outstanding debt
- **Account closures**: Creditor-initiated closures on other tradelines

### Step 3 — Account-Level Risk Characteristics

Assess static and dynamic account risk factors:

- **Seasoning**: Months on book (EPD risk highest in months 1–12)
- **Current LTV**: Mark-to-market LTV using updated property/collateral values
- **Rate type and reset risk**: ARM reset proximity, payment shock magnitude
- **DTI at origination**: Higher origination DTI correlates with lower payment cushion
- **Borrower reserves at origination**: Months of reserves documented at closing
- **Exception-to-policy origination**: Loans originated with policy exceptions carry elevated risk

### Step 4 — Macroeconomic Overlay

Incorporate geographic and macroeconomic conditions:

- **Local unemployment rate**: Current and trajectory for the borrower's MSA
- **Home price index**: HPI trend for the property's ZIP code (collateral support erosion)
- **Consumer confidence**: Regional consumer sentiment indices
- **Interest rate environment**: Impact on variable-rate payment obligations
- **Industry-specific stress**: Sector-level employment and revenue trends for commercial borrowers

Weight macroeconomic factors by their historical correlation with delinquency in the portfolio's specific asset class.

### Step 5 — Probability Scoring and Segmentation

Combine all features into a delinquency probability score:

- Apply a calibrated logistic regression, gradient-boosted tree, or ensemble model
- Output a probability of 30+ DPD within the next 3 months and 6 months
- Segment the portfolio into risk tiers:
  - **Green (0–5%)**: Standard monitoring
  - **Yellow (5–15%)**: Enhanced monitoring, soft-touch outreach eligible
  - **Orange (15–30%)**: Proactive loss mitigation contact required
  - **Red (>30%)**: Urgent intervention, workout team assignment
- Calculate expected roll rates from each tier to deeper delinquency stages

### Step 6 — Model Validation and Calibration

Ensure prediction quality through:

- **Discrimination**: Gini coefficient / AUC-ROC > 0.70 (target > 0.75)
- **Calibration**: Hosmer-Lemeshow test, predicted vs. actual by decile
- **Stability**: Population Stability Index (PSI) < 0.10 for feature distributions
- **Back-testing**: Out-of-time validation on most recent 4 quarters
- **Segmental performance**: AUC by product type, geography, and vintage
- **Override tracking**: Monitor manual overrides of model scores for effectiveness

### Step 7 — Action Framework and Reporting

Map prediction tiers to specific interventions:

- **Green**: Standard servicing, no additional action
- **Yellow**: Automated borrower check-in (email/SMS), payment reminder enhancement
- **Orange**: Live outreach call, financial hardship assessment, modification evaluation
- **Red**: Dedicated workout specialist, forbearance/modification offer, collateral review

Generate reports showing:
- Portfolio distribution across risk tiers with period-over-period trend
- Top contributing features for each tier (model explainability)
- Projected delinquency pipeline (expected new 30/60/90 DPD accounts)
- Resource allocation recommendations for collections/loss mitigation staff

## Output Specification

```
## Early Delinquency Prediction Report — [Date]

### Portfolio Risk Distribution
| Tier | Accounts | Balance ($M) | Avg Score | Predicted 30+ Rate | Action |
|------|----------|-------------|-----------|--------------------|---------| 
| Green | X,XXX | $XXX | X.XX | X.X% | Standard |
| Yellow | X,XXX | $XXX | X.XX | X.X% | Enhanced monitor |
| Orange | XXX | $XX | X.XX | XX.X% | Proactive outreach |
| Red | XX | $X | X.XX | XX.X% | Urgent intervention |

### Delinquency Pipeline Forecast
| Metric | Current Month | +30 Days | +60 Days | +90 Days |
|--------|---------------|----------|----------|----------|
| New 30 DPD | XXX | XXX | XXX | XXX |
| Roll to 60 DPD | XX | XX | XX | XX |
| Roll to 90+ DPD | X | X | X | X |

### Top Risk Drivers (Across Orange/Red Tiers)
1. [Feature]: [Description of signal and prevalence]
2. [Feature]: [Description of signal and prevalence]
3. [Feature]: [Description of signal and prevalence]

### Model Performance Metrics
- AUC-ROC: [X.XX]
- Gini: [X.XX]
- PSI: [X.XX] (stable / warning / action required)
- Calibration: [Aligned / Overpredicting / Underpredicting]

### Recommended Resource Allocation
- Outreach calls required (Orange tier): [N] accounts
- Workout assignments required (Red tier): [N] accounts
- Estimated staff hours: [N] hours
```

## Analysis Framework

Apply the **BERM** framework:

- **B**ehavioral signals — Payment pattern changes preceding delinquency
- **E**xternal data — Bureau deterioration and macroeconomic stress
- **R**isk characteristics — Account-level static and dynamic risk factors
- **M**odel governance — Validation, calibration, and monitoring rigor

## Examples

**Example 1 — Behavioral Signal Detection**

Loan 10045832: 30-year mortgage, 18 MOB. Payment timing drifted from avg 12 days early to 2 days before due date over 4 months. Auto-pay cancelled in month 16. Revolving utilization spiked from 42% to 78%. FICO dropped 35 points. Model score: 0.34 (Red tier). Action: Assigned to workout specialist for proactive hardship assessment. Outcome: Borrower disclosed job loss; approved for 3-month forbearance, avoided default.

**Example 2 — Geographic Macro Overlay**

Portfolio segment: 847 auto loans in Houston MSA. Local unemployment rose from 4.1% to 6.8% in 2 quarters. Model recalibrated with macro overlay shifted 124 accounts from Green to Yellow, 38 from Yellow to Orange. Automated outreach campaign triggered for Yellow accounts; live calls initiated for Orange. Result: 60-day delinquency rate for the cohort was 3.2% vs. 5.8% for non-contacted comparable accounts.

## Guidelines

- Refresh bureau-based features at least quarterly; payment behavior features monthly
- Calibrate the model at least annually; recalibrate immediately after significant macro shifts
- Monitor PSI monthly to detect feature distribution drift that degrades model performance
- Ensure fair lending compliance: model features must not include prohibited basis factors or proxies
- Document feature selection rationale and adverse impact testing results
- Integrate prediction outputs with the loan servicing platform for automated action triggers
- Track intervention outcomes to measure lift from proactive outreach programs
- Maintain model governance documentation per SR 11-7 / OCC 2011-12 guidance

## Validation Checklist

- [ ] All predictive features are permissible under fair lending (no prohibited basis or proxies)
- [ ] Model AUC-ROC exceeds 0.70 on out-of-time validation
- [ ] Calibration is aligned (predicted vs. actual within 10% across all deciles)
- [ ] PSI is below 0.10 for all material features
- [ ] Roll rate assumptions are validated against actual historical transition data
- [ ] Macro overlay weights reflect current economic conditions, not stale coefficients
- [ ] Action thresholds (tier boundaries) are validated for cost-effectiveness
- [ ] Model documentation meets SR 11-7 requirements (development, validation, governance)
- [ ] Override policy is documented and override outcomes are tracked
- [ ] Intervention effectiveness is measured with appropriate control groups
