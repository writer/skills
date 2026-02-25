---
name: readmission-risk-explanation
description: Explain readmission risk drivers using LACE index scoring, clinical and social determinant analysis, and targeted intervention recommendations. Use when assessing 30-day readmission risk, explaining readmission prediction model outputs, designing readmission reduction interventions, or reporting on Hospital Readmissions Reduction Program metrics.

metadata:
  display_name: "Readmission Risk Explanation"
  short_description: "Explain 30-day readmission risk factors and drivers"
  default_prompt: "Explain my readmission risk in simple words and next steps"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Readmission Risk Explanation

## Overview

Analyze and explain the key drivers of hospital readmission risk for individual patients or patient populations. This skill applies validated scoring models (LACE, HOSPITAL score, CMS risk-standardized models), decomposes risk factors into actionable categories, and generates targeted intervention recommendations to reduce preventable readmissions — aligned with the CMS Hospital Readmissions Reduction Program (HRRP).

## When to Use

- Calculating and explaining LACE or HOSPITAL readmission risk scores
- Identifying high-risk patients at discharge for care management enrollment
- Explaining readmission prediction model outputs to clinical teams
- Designing patient-specific readmission prevention plans
- Reporting on HRRP performance metrics and penalty avoidance strategies
- Performing root cause analysis on readmission events

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Discharge summary | Diagnoses, procedures, discharge disposition | Structured object |
| LACE components | Length of stay, acuity, comorbidities, ED visits | Numeric values |
| Patient demographics | Age, sex, insurance, social determinants | Structured object |
| Medication list | Discharge medications with reconciliation status | Array |
| Prior utilization | ED visits and admissions in prior 6 months | Count and details |

## Methodology

### Step 1: LACE Index Calculation

Calculate the LACE score (validated 30-day readmission predictor):

**L - Length of Stay (days):**
- 1 day = 1 point, 2 days = 2, 3 days = 3, 4-6 days = 4, 7-13 days = 5, 14+ days = 7

**A - Acuity of Admission:**
- Elective = 0 points, Emergent/Urgent = 3 points

**C - Comorbidity (Charlson Comorbidity Index):**
- CCI 0 = 0 points, CCI 1 = 1, CCI 2 = 2, CCI 3 = 3, CCI 4+ = 5

**E - Emergency Department visits (prior 6 months):**
- 0 visits = 0 points, 1 = 1, 2 = 2, 3 = 3, 4+ = 4

Total Score Range: 0-19

Risk Stratification:
- 0-4: Low risk (approximately 2-5% readmission probability)
- 5-9: Moderate risk (approximately 10-15%)
- 10-14: High risk (approximately 20-30%)
- 15-19: Very high risk (approximately 35%+)

### Step 2: Multidimensional Risk Factor Analysis

Evaluate risk across five domains:

**1. Clinical Factors**
- Disease severity and instability at discharge
- Number of active diagnoses (comorbidity burden)
- Medication complexity (polypharmacy: 5 or more medications, high-alert medications)
- Procedure-related complications
- Incomplete treatment course

**2. Transitional Care Factors**
- Discharge destination (home alone vs. home with support vs. facility)
- Follow-up appointment scheduled within 7 days (yes/no)
- Medication reconciliation completed
- Discharge instructions comprehension verified
- Durable medical equipment arranged

**3. Social Determinants of Health (SDOH)**
- Social isolation or inadequate caregiver support
- Food insecurity or housing instability
- Transportation barriers to follow-up care
- Health literacy level
- Language barriers

**4. Behavioral Factors**
- Medication non-adherence history
- Substance use disorders
- Mental health conditions (depression linked to 2x readmission risk)
- Missed appointment history

**5. Health System Factors**
- Primary care physician engagement
- Care coordination across settings
- Post-discharge outreach protocols
- Prior readmission history (strongest predictor)

### Step 3: Risk Driver Prioritization

Rank risk factors by modifiability and impact:

| Category | Modifiability | Impact on Risk | Priority |
|----------|--------------|----------------|----------|
| Medication non-adherence | High | High | 1 - Immediate |
| Missing follow-up appointment | High | High | 1 - Immediate |
| Inadequate discharge education | High | Medium | 2 - High |
| Social isolation | Medium | High | 2 - High |
| Comorbidity burden | Low | High | 3 - Monitor |
| Disease severity | Low | High | 3 - Monitor |

### Step 4: Intervention Mapping

Map prioritized risk factors to evidence-based interventions:

**Pre-Discharge Interventions:**
- Teach-back method for discharge instructions
- Medication reconciliation with pharmacist review
- Schedule follow-up within 7 days (within 48h for high-risk)
- Assess and address SDOH barriers

**Transition Interventions:**
- Warm handoff to PCP/specialist
- Transitional care nursing (Coleman CTI or Naylor TCM model)
- Medication delivery or assistance program enrollment
- Home health referral if indicated

**Post-Discharge Interventions (within 72 hours):**
- Phone call by RN to assess symptoms, medication adherence
- Confirm follow-up appointment and transportation
- Remote patient monitoring for applicable conditions
- Community health worker engagement for SDOH

**Ongoing Interventions (30-day window):**
- Care management enrollment for high-risk patients
- Chronic disease self-management education
- Behavioral health integration
- Palliative care referral if appropriate

### Step 5: Explanation Generation

Produce a clear, stakeholder-appropriate explanation:

- **For clinicians**: Quantitative risk score with key clinical drivers and targeted interventions
- **For case managers**: Actionable risk factors with specific care transition recommendations
- **For quality leaders**: Population-level risk trends, HRRP performance, and intervention effectiveness
- **For patients/families**: Plain-language explanation of what to watch for and how to prevent return visits

## Output Specification

The output includes:

**index_admission**: admission_date, discharge_date, primary_diagnosis (description, icd10, ms_drg), discharge_disposition

**lace_score**: total score, risk_tier, and individual component breakdowns

**risk_factors**: organized by domain (clinical, transitional, sdoh, behavioral, system) with factor, detail, severity, and modifiable flag

**priority_drivers**: ranked list with factor, domain, contribution_to_risk, modifiability

**interventions**: target_risk_factor, intervention description, evidence_basis, owner, timing

**readmission_probability**: estimated percentage

**explanation_narrative**: clear prose explanation tailored to audience

## Analysis Framework

### HRRP Applicable Conditions

CMS penalizes excess readmissions for these conditions/procedures:

1. Acute myocardial infarction (AMI)
2. Heart failure (HF)
3. Pneumonia
4. COPD
5. Total hip/knee arthroplasty (THA/TKA)
6. Coronary artery bypass graft (CABG)

### Root Cause Analysis for Readmission Events

When analyzing actual readmissions, classify by:

- **Potentially preventable**: Related to index condition, inadequate transition, missed follow-up
- **Planned**: Scheduled readmission (staged procedure, chemotherapy)
- **Unrelated**: New condition unrelated to index admission

## Examples

**Input**: 68-year-old female, discharged after HF exacerbation. LOS: 5 days. Emergent admission. Charlson: 4. ED visits in 6 months: 3. Lives alone. On 8 medications. No follow-up scheduled at discharge.

**LACE**: L=4 + A=3 + C=5 + E=3 = 15 (Very High Risk)

**Priority Drivers**: (1) No follow-up scheduled — immediate intervention required. (2) Polypharmacy with complex regimen. (3) Lives alone — no caregiver support. (4) High prior ED utilization suggesting inadequate outpatient management.

**Recommended Interventions**: Schedule cardiology follow-up within 48 hours, pharmacist medication reconciliation and teach-back, home health referral with telemonitoring, social work SDOH assessment, 48-hour post-discharge RN call.

## Guidelines

1. **LACE is a screening tool, not a clinical decision** — use it to prioritize intervention intensity, not to deny care
2. **Modifiable factors take priority** — focus interventions on factors that can be changed
3. **SDOH are clinical factors** — treat social determinants with the same rigor as clinical risk factors
4. **Document interventions delivered** — track which interventions were implemented and their outcomes
5. **Consider health equity** — ensure risk models and interventions do not perpetuate disparities

## Validation Checklist

- [ ] LACE score components are calculated correctly from documented values
- [ ] All five risk domains are assessed (clinical, transitional, SDOH, behavioral, system)
- [ ] Risk factors are classified by modifiability and impact
- [ ] Each priority driver has at least one mapped intervention
- [ ] Interventions have clear ownership and timing
- [ ] Explanation is appropriate for the target audience
- [ ] HRRP applicability is noted for relevant diagnoses

## HIPAA Compliance Notes

- Readmission risk data often includes sensitive information (behavioral health, substance use, SDOH) requiring enhanced privacy protections
- Risk scores shared across care settings must comply with minimum necessary standard
- Patient consent may be required for SDOH data sharing depending on state law
- De-identify risk data used for population analytics and program evaluation
- Ensure risk model outputs are not used in discriminatory ways that violate civil rights protections
