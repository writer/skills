---
name: patient-stratification-engine
description: Risk-stratify patients into actionable tiers using clinical, utilization, and social determinant data with validated risk models. Use when building risk-stratified patient panels, prioritizing care management resources, supporting population health initiatives, or identifying patients for intensive intervention programs.

metadata:
  display_name: "Patient Stratification Engine"
  short_description: "Stratify patients into risk tiers for care management"
  default_prompt: "Analyze my patient stratification and recommend clear next actions"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Patient Stratification Engine

## Overview

Classify patients into risk tiers based on clinical complexity, utilization patterns, social determinants, and predicted outcomes using validated risk stratification methodologies. This skill supports population health management, care management resource allocation, and value-based care program design by identifying which patients need which level of intervention.

## When to Use

- Building risk-stratified patient panels for care management programs
- Prioritizing high-risk patients for proactive outreach
- Allocating care management resources based on patient acuity
- Supporting ACO/value-based care population segmentation
- Identifying rising-risk patients before they become high-cost
- Designing tiered intervention programs based on risk levels

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Patient demographics | Age, sex, race/ethnicity, insurance, ZIP | Structured object |
| Clinical profile | Active diagnoses (ICD-10), medications, labs | Structured arrays |
| Utilization history | ED visits, admissions, office visits (12-24 months) | Structured array with dates |
| Claims/cost data | Total cost of care, cost by category | Numeric |
| SDOH indicators | Housing, food security, transportation, social support | Structured object |
| Functional status | ADL/IADL scores, cognitive status if available | Structured object |

## Methodology

### Step 1: Clinical Complexity Scoring

Calculate disease burden and clinical complexity:

**HCC (Hierarchical Condition Category) Risk Score:**
- Map active ICD-10 diagnoses to HCC categories
- Calculate CMS-HCC risk adjustment factor (RAF)
- Benchmark against population average (1.0)
- Higher RAF = higher predicted cost and clinical complexity

**Charlson Comorbidity Index (CCI):**
- Score comorbidities: MI, CHF, PVD, CVD, dementia, COPD, connective tissue disease, PUD, liver disease, diabetes, hemiplegia, CKD, cancer, AIDS
- Each condition scores 1-6 based on severity
- Total CCI predicts 10-year mortality risk

**Elixhauser Comorbidity Measure:**
- 31 comorbidity categories beyond Charlson
- Captures conditions like depression, obesity, drug abuse, psychoses
- Better predictor for in-hospital mortality and LOS

### Step 2: Utilization Pattern Analysis

Evaluate healthcare utilization intensity:

| Metric | Low Risk | Moderate | High | Very High |
|--------|----------|----------|------|-----------|
| ED visits (12 mo) | 0-1 | 2-3 | 4-5 | 6+ |
| Inpatient admits (12 mo) | 0 | 1 | 2-3 | 4+ |
| Specialists seen | 0-2 | 3-4 | 5-7 | 8+ |
| Total cost of care | Below 50th pctl | 50-75th pctl | 75-90th pctl | Above 90th pctl |
| Readmissions (30-day) | None | 1 | 2+ | Multiple |

### Step 3: Social Risk Assessment

Evaluate social determinants that amplify clinical risk:

**SDOH Risk Factors (scored 0-2 each):**
- Housing instability or homelessness (0=stable, 1=at risk, 2=unstable)
- Food insecurity (0=secure, 1=low security, 2=very low)
- Transportation barriers (0=none, 1=occasional, 2=frequent)
- Social isolation (0=connected, 1=limited, 2=isolated)
- Health literacy (0=adequate, 1=limited, 2=low)
- Financial strain (0=stable, 1=some stress, 2=severe)

Total SDOH score: 0-12 (Low: 0-3, Moderate: 4-7, High: 8-12)

### Step 4: Composite Risk Tier Assignment

Combine clinical, utilization, and social scores into a composite tier:

| Risk Tier | Clinical | Utilization | SDOH | Recommended Intervention Level |
|-----------|----------|-------------|------|-------------------------------|
| Tier 1 - Healthy/Low | Low CCI, few conditions | Minimal utilization | Low SDOH risk | Prevention and wellness |
| Tier 2 - Rising Risk | Moderate CCI, chronic conditions emerging | Increasing utilization | Low-Moderate SDOH | Disease management, self-management support |
| Tier 3 - High Risk | High CCI, multiple chronic conditions | Frequent utilization | Moderate-High SDOH | Care management, care coordination |
| Tier 4 - Complex/Very High | Very high CCI, frailty, functional decline | Very frequent utilization | High SDOH | Intensive care management, multidisciplinary team |

### Step 5: Actionable Segmentation

Assign patients to intervention programs based on tier and dominant risk drivers:

**Tier-Based Program Mapping:**
- Tier 1: Preventive outreach, annual wellness visits, gap closure
- Tier 2: Chronic disease education, medication management, care gap alerts
- Tier 3: Assigned care manager, regular check-ins, transition management
- Tier 4: Intensive care team (RN + SW + pharmacist + CHW), home visits, high-touch coordination

## Output Specification

The output includes:

**patient_profile**: demographics, insurance, pcp assignment

**clinical_complexity**: hcc_raf_score, charlson_cci, active_conditions_count, medication_count, high_risk_conditions list

**utilization_profile**: ed_visits_12mo, admissions_12mo, readmissions, specialist_count, total_cost_of_care, cost_percentile

**sdoh_assessment**: individual factor scores, total_sdoh_score, sdoh_risk_level

**composite_stratification**: risk_tier (1-4), tier_label, composite_score, dominant_risk_domain, confidence_level

**intervention_assignment**: program_name, intervention_level, recommended_team_composition, key_focus_areas, engagement_frequency

**rising_risk_indicators**: flags for patients trending toward higher tier (increasing utilization, new diagnoses, SDOH changes)

## Analysis Framework

### Impactability Assessment

Not all high-risk patients are equally impactable. Assess:

1. **Modifiable risk factors present**: Can interventions change the trajectory?
2. **Patient engagement likelihood**: History of appointment adherence, responsiveness
3. **Intervention availability**: Are appropriate programs and resources available?
4. **Cost-effectiveness**: Will intervention costs be offset by utilization reduction?

Impactability Score: High (good candidate for intensive program), Medium (moderate intervention), Low (maintain monitoring, fewer modifiable factors)

### Trend Analysis

Track tier movement over time:
- **Improving**: Moving to lower risk tier (intervention success indicator)
- **Stable**: Remaining in same tier (maintenance mode)
- **Worsening**: Moving to higher tier (intervention escalation needed)
- **Rising risk**: Not yet high tier but trending upward (early intervention opportunity)

## Examples

**Input**: 72-year-old male, CHF (EF 35%), DM2 with neuropathy, CKD Stage 3a, depression. On 12 medications. 3 ED visits in 12 months, 2 hospital admissions (1 readmission). Lives alone in rural area. Limited transportation. Income below 200% FPL.

**Stratification**:
- Clinical: HCC-RAF 2.4 (high), CCI 6 (high), 4 active chronic conditions, polypharmacy
- Utilization: 3 ED, 2 admits, 1 readmission — HIGH
- SDOH: Social isolation (2) + transportation (2) + financial (2) = 6/12 — MODERATE
- Composite: **Tier 4 - Complex/Very High**
- Dominant driver: Clinical complexity + utilization intensity
- Recommended: Intensive care management team with home health, telemonitoring, community health worker for transportation, pharmacist for medication management

## Guidelines

1. **Stratification is dynamic** — reassess at least quarterly or after significant clinical events
2. **Avoid label bias** — risk tiers inform resource allocation, not patient worth
3. **Include rising-risk identification** — intervening before patients become high-risk is most cost-effective
4. **Validate models against outcomes** — regularly calibrate stratification against actual utilization and costs
5. **Ensure equity** — audit stratification for demographic bias and disparities

## Validation Checklist

- [ ] All data inputs are current (within 90 days for clinical, 12 months for utilization)
- [ ] HCC coding is complete and accurate (capture all relevant conditions)
- [ ] SDOH assessment is completed (not defaulted to zero/unknown)
- [ ] Composite tier assignment reflects the dominant risk driver
- [ ] Intervention assignments match available program capacity
- [ ] Rising-risk indicators are flagged for proactive intervention
- [ ] Stratification model is calibrated against actual outcomes

## HIPAA Compliance Notes

- Risk stratification data aggregates extensive PHI and requires strict access controls
- Share stratification results only with care team members with a need to know
- De-identify population-level stratification reports for quality improvement
- SDOH data may have additional privacy requirements under state law
- Patient consent should be obtained before enrolling in care management programs based on stratification
- Maintain audit logs for all stratification data access and sharing
