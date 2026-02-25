---
name: No-Show Risk Predictor
description: Predict patient appointment no-show probability using multi-factor risk modeling incorporating historical patterns, social determinants, behavioral signals, and operational context to enable targeted intervention strategies.

metadata:
  display_name: "No Show Risk Predictor"
  short_description: "Predict patient appointment no-show probability and risk"
  default_prompt: "Review my no show risk and highlight top risks and next actions"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# No-Show Risk Predictor

## Overview

This skill builds and applies a multi-factor predictive model for patient appointment no-shows. It integrates historical attendance patterns, social determinants of health (SDoH), scheduling characteristics, and behavioral signals to generate per-appointment risk scores. The model enables targeted outreach interventions (reminder calls, transportation assistance, telehealth conversion) to reduce no-show rates while maintaining equity across patient populations. National benchmarks indicate average no-show rates of 18-23% across ambulatory settings, with significant variation by specialty, payer, and demographics.

## When to Use

- Implementing or improving patient reminder and outreach programs
- Designing overbooking algorithms that balance access with operational efficiency
- Targeting care coordination resources toward high-risk patients
- Evaluating financial impact of no-shows on revenue cycle and provider productivity
- Supporting value-based care programs that depend on care gap closure
- Reducing disparities in appointment adherence across demographic groups

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `appointment_history` | Historical records with status (kept, no-show, cancelled, rescheduled) | De-identified CSV/JSON |
| `patient_features` | Demographics, insurance, zip code, preferred language, portal status | JSON array |
| `scheduling_features` | Lead time, day of week, time of day, appointment type, provider, location | JSON object |
| `visit_history` | Prior visit frequency, last visit date, no-show history count | JSON object |
| `sdoh_indicators` | Area-level deprivation index (ADI), transportation access, broadband access | JSON object |
| `weather_data` | Historical weather conditions for appointment dates (optional) | JSON object |
| `reminder_history` | Prior reminder contacts (type, timing, response) | JSON array |

## Methodology

### Step 1: Feature Engineering
- **Historical behavior features**:
  - No-show rate over last 12 months (overall and by appointment type)
  - Consecutive no-show streak length
  - Cancellation-to-no-show ratio
  - Average reschedule frequency
  - Time since last completed visit
- **Scheduling features**:
  - Lead time (days between scheduling and appointment): risk increases beyond 14 days
  - Day of week (Monday and Friday typically higher risk)
  - Time of day (early morning and late afternoon higher risk)
  - New patient vs. established patient
  - Appointment type (routine follow-up vs. procedure vs. new complaint)
- **Demographic and SDoH features**:
  - Area Deprivation Index (ADI) decile for patient zip code
  - Distance from residence to facility (drive time minutes)
  - Public transportation accessibility score
  - Insurance type (Medicaid and uninsured historically higher no-show rates)
  - Preferred language (LEP status indicator)
  - Age group (18-30 typically highest risk)
- **Engagement features**:
  - Patient portal activation and recent login
  - Reminder response history (confirmed, no response, opted out)
  - Prior telehealth utilization (telehealth-willing patients may convert)

### Step 2: Risk Model Construction
- Apply gradient-boosted decision tree (GBDT) or logistic regression model
- Target variable: binary no-show outcome (1 = no-show, 0 = attended or cancelled)
- Use time-based train/test split (train on months 1-9, validate on months 10-12)
- Key modeling considerations:
  - Handle class imbalance via SMOTE or class weighting
  - Use area under ROC curve (AUC-ROC) of 0.75 or higher as minimum performance threshold
  - Calculate calibration curve to ensure predicted probabilities are well-calibrated
  - Perform fairness audit: compare model performance (FPR, FNR) across race, ethnicity, and insurance groups

### Step 3: Risk Stratification
- Assign risk tiers based on predicted probability:
  - **Low risk** (0-15%): Standard reminder workflow
  - **Moderate risk** (16-35%): Enhanced reminder (additional touchpoint, preferred channel)
  - **High risk** (36-60%): Proactive outreach (live call, barrier assessment, telehealth offer)
  - **Very high risk** (above 60%): Intensive intervention (care coordination, transportation, reschedule)
- Calculate expected no-show volume per clinic session for overbooking guidance

### Step 4: Intervention Matching
- Map risk tier to intervention protocol:
  - Low: Automated text/email reminder at 72h and 24h
  - Moderate: Automated reminder plus IVR confirmation call at 48h
  - High: Live agent call with barrier screening (transportation, childcare, cost concerns)
  - Very high: Care coordinator outreach with SDoH resource linkage; offer telehealth conversion
- Track intervention effectiveness to create feedback loop for model improvement

### Step 5: Overbooking Optimization
- Calculate optimal overbooking rate per provider session:
  - overbook_slots = floor(scheduled_slots x session_predicted_no_show_rate x overbooking_factor)
  - Overbooking factor: 0.5 (conservative) to 0.8 (aggressive), calibrated to provider tolerance
- Apply constraints:
  - Never exceed provider-specific maximum daily volume
  - Weight by appointment complexity (do not overbook procedural slots)
  - Monitor patient wait time impact: cap acceptable increase at 15 minutes

## Output Specification

```yaml
no_show_prediction:
  model_performance:
    auc_roc: number
    precision_at_30pct_threshold: number
    recall_at_30pct_threshold: number
    calibration_error: number
    fairness_metrics:
      - group: string
        fpr: number
        fnr: number
  appointment_scores:
    - appointment_id: string
      predicted_probability: number
      risk_tier: string
      top_risk_factors:
        - factor: string
          contribution: number
      recommended_intervention: string
  session_summary:
    - session_date: date
      provider_id: string
      scheduled_count: number
      predicted_no_shows: number
      recommended_overbooks: number
  population_insights:
    overall_predicted_rate: number
    rate_by_specialty: object
    rate_by_insurance: object
    rate_by_adi_quintile: object
    top_modifiable_risk_factors: array
```

## Analysis Framework

Apply a **Predict-Stratify-Intervene-Measure** cycle:

1. **Predict**: Generate per-appointment no-show probability using multi-factor model
2. **Stratify**: Assign risk tiers with matched intervention protocols
3. **Intervene**: Execute targeted outreach based on risk tier and patient preferences
4. **Measure**: Track intervention effectiveness, update model, and assess equity impact

Feature importance analysis should use SHAP (SHapley Additive exPlanations) values to ensure model transparency and enable clinically meaningful risk factor communication.

## Examples

**Example: Multi-Specialty Ambulatory Network**
- Model AUC-ROC: 0.81 on validation set
- Top predictive features: prior no-show count (SHAP 0.23), lead time beyond 21 days (0.18), ADI decile 9-10 (0.14), no portal activation (0.12), Medicaid payer (0.09)
- Predicted no-show rate: 19.2% overall; 34.1% for behavioral health; 11.3% for oncology
- Intervention impact: High-risk live call outreach reduced no-show rate from 42% to 26% (38% relative reduction)
- Overbooking recommendation: Internal medicine sessions add 1.5 overbook slots per session
- Equity finding: Model FNR 2.3% higher for Hispanic patients, recalibration scheduled

## Guidelines

- **HIPAA Compliance**: All patient-level data must be de-identified before model training and output. Use surrogate appointment IDs. Aggregate reporting by zip code requires minimum cell size of 11 per HHS guidance. Never expose individual patient identifiers in risk scores shared beyond the care team.
- **Algorithmic Fairness**: Conduct disparate impact analysis across race, ethnicity, sex, age, and insurance type. If any group FNR exceeds another by more than 5 percentage points, retrain with fairness constraints. Document fairness audit results.
- **Patient Autonomy**: Interventions must respect patient communication preferences and opt-out rights. Never penalize patients for no-shows in model design (model predicts, not judges).
- **Overbooking Ethics**: Overbooking must not degrade care quality. Monitor patient wait times and provider overtime as safety valves.
- **Model Governance**: Retrain model quarterly. Monitor for data drift monthly. Maintain model card documenting training data, performance, limitations, and fairness metrics.

## Validation Checklist

- [ ] Model trained on minimum 12 months of historical data
- [ ] AUC-ROC of 0.75 or higher on held-out validation set
- [ ] Calibration curve shows well-calibrated probabilities
- [ ] SHAP or equivalent explainability analysis completed
- [ ] Fairness audit across race, ethnicity, insurance, and age
- [ ] Risk tiers defined with matched intervention protocols
- [ ] Overbooking recommendations include safety constraints
- [ ] All data de-identified per HIPAA Safe Harbor
- [ ] Feedback loop designed for continuous model improvement
- [ ] Model card documented with limitations and governance plan
- [ ] Stakeholder sign-off from operations, clinical, and compliance
