---
name: lab-result-explanation
description: Explain laboratory results for clinicians with clinical context, reference range interpretation, critical value flagging, trending analysis, and diagnostic significance mapping. Use when interpreting lab panels, explaining abnormal results, correlating lab findings with clinical conditions, or generating lab summary reports.

metadata:
  display_name: "Lab Result Explanation"
  short_description: "Interpret lab results with clinical context and trends"
  default_prompt: "Explain my lab result in simple words and next steps"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Lab Result Explanation

## Overview

Provide comprehensive, clinically contextualized explanations of laboratory results including reference range interpretation, critical value identification, result trending over time, inter-test correlations, and diagnostic significance. This skill translates raw lab data into actionable clinical intelligence for healthcare providers, supporting diagnostic reasoning and treatment monitoring.

## When to Use

- Interpreting comprehensive metabolic panels, CBCs, or specialty lab panels
- Explaining abnormal lab results in the context of patient conditions
- Identifying critical values requiring immediate clinical action
- Trending serial lab results to assess treatment response or disease progression
- Correlating lab findings across multiple tests for diagnostic patterns
- Generating lab summary reports for clinical handoffs

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Lab results | Test name, value, unit, reference range, specimen date | Array of lab objects |
| Patient context | Age, sex, diagnoses, medications, renal/hepatic function | Structured object |
| Historical labs | Prior results for trending (if available) | Array with dates |
| Clinical question | Specific clinical context for interpretation | Free text |
| Lab panel type | BMP, CMP, CBC, lipid, hepatic, thyroid, coagulation, etc. | String |

## Methodology

### Step 1: Result Classification

Classify each lab result:

**Status Categories:**
- NORMAL: Within reference range, clinically insignificant
- ABNORMAL-LOW: Below reference range
- ABNORMAL-HIGH: Above reference range
- CRITICAL-LOW: Below critical threshold, immediate action needed
- CRITICAL-HIGH: Above critical threshold, immediate action needed
- BORDERLINE: Near reference range boundary, clinical judgment needed

**Reference Range Adjustments:**
- Age-adjusted ranges (e.g., creatinine in elderly, alkaline phosphatase in children)
- Sex-adjusted ranges (e.g., hemoglobin, creatinine)
- Pregnancy-adjusted ranges (e.g., TSH, alkaline phosphatase)
- Medication-adjusted interpretation (e.g., INR on warfarin, TSH on levothyroxine)

### Step 2: Critical Value Assessment

Identify results requiring immediate clinical notification:

| Test | Critical Low | Critical High |
|------|-------------|---------------|
| Potassium | Less than 2.5 mEq/L | Greater than 6.5 mEq/L |
| Sodium | Less than 120 mEq/L | Greater than 160 mEq/L |
| Glucose | Less than 40 mg/dL | Greater than 500 mg/dL |
| Calcium (total) | Less than 6.0 mg/dL | Greater than 13.0 mg/dL |
| Hemoglobin | Less than 7.0 g/dL | Greater than 20.0 g/dL |
| Platelets | Less than 20K/uL | Greater than 1000K/uL |
| INR | N/A | Greater than 5.0 |
| Troponin | N/A | Above 99th percentile URL |
| Lactate | N/A | Greater than 4.0 mmol/L |
| WBC | Less than 1.0 K/uL | Greater than 30.0 K/uL |

### Step 3: Clinical Contextualization

Map lab abnormalities to the patient's clinical context:

**Diagnosis-Lab Correlation:**
- For each abnormal result, identify the most likely clinical explanation given active diagnoses
- Flag unexpected abnormalities that do not fit the clinical picture (potential new findings)
- Note medication effects on lab values (e.g., ACEi raising potassium, thiazides lowering sodium)
- Identify lab patterns suggestive of specific conditions (e.g., elevated AST:ALT ratio greater than 2:1 suggesting alcoholic liver disease)

**Inter-Test Correlations:**
- Anion gap with BMP results (metabolic acidosis workup)
- BUN:Creatinine ratio (pre-renal vs. intrinsic renal)
- Albumin correction for calcium (corrected Ca = measured Ca + 0.8 x (4.0 - albumin))
- Calculated GFR from creatinine using CKD-EPI equation
- Iron studies pattern recognition (iron deficiency vs. anemia of chronic disease vs. hemochromatosis)

### Step 4: Trend Analysis

When historical labs are available, analyze trends:

**Trending Parameters:**
- Direction: rising, falling, stable, fluctuating
- Rate of change: rapid, gradual, expected for clinical context
- Clinical significance: trending toward or away from critical thresholds
- Treatment response: improving toward target or worsening despite treatment

**Visual Trend Indicators:**
- Significant improvement (moving toward normal)
- Stable abnormality (consistently out of range, chronic condition)
- Worsening trend (moving away from normal)
- Acute change (sudden significant shift from baseline)

### Step 5: Explanation Generation

Produce the lab explanation tailored to the clinical audience:

**For each abnormal result, provide:**
1. What the test measures (brief)
2. What the result means clinically in this patient context
3. Most likely explanation given diagnoses and medications
4. Clinical significance and urgency level
5. Recommended follow-up testing or actions
6. If trending: direction and clinical implications of the trend

## Output Specification

The output includes:

**lab_panel_summary**: panel_type, collection_date, overall_assessment (normal/mixed/significantly abnormal)

**results** (for each test): test_name, loinc_code, value, unit, reference_range, status (normal/abnormal-low/abnormal-high/critical), clinical_explanation, likely_etiology, related_diagnoses, medication_effects, recommended_action

**critical_values**: list of critical results requiring immediate notification with urgency_level and recommended_immediate_action

**patterns_identified**: pattern_name, involved_tests, clinical_significance, suggested_diagnosis_or_condition

**trends** (if historical data available): test_name, current_value, prior_values with dates, trend_direction, rate_of_change, clinical_interpretation

**follow_up_recommendations**: recommended_tests, rationale, timing, clinical_priority

## Analysis Framework

### Common Lab Panel Interpretive Patterns

| Pattern | Key Findings | Suggests |
|---------|-------------|----------|
| Pre-renal azotemia | BUN:Cr ratio greater than 20:1 | Dehydration, CHF, GI bleed |
| Hepatocellular injury | AST/ALT elevated, Alk Phos normal | Hepatitis, drug toxicity, ischemia |
| Cholestatic pattern | Alk Phos/GGT elevated, AST/ALT mildly elevated | Biliary obstruction, infiltrative disease |
| DIC | Low platelets, elevated PT/PTT, low fibrinogen, elevated D-dimer | Disseminated intravascular coagulation |
| Iron deficiency | Low iron, low ferritin, high TIBC, low transferrin sat | Iron deficiency anemia |
| Tumor lysis | High K+, high phosphorus, high uric acid, low calcium | Cell lysis from chemotherapy |
| SIADH | Low sodium, low serum osmolality, high urine osmolality | Inappropriate ADH secretion |

### eGFR Staging (CKD-EPI 2021)

| Stage | eGFR (mL/min/1.73m2) | Description |
|-------|----------------------|-------------|
| G1 | 90 or greater | Normal or high |
| G2 | 60-89 | Mildly decreased |
| G3a | 45-59 | Mildly to moderately decreased |
| G3b | 30-44 | Moderately to severely decreased |
| G4 | 15-29 | Severely decreased |
| G5 | Less than 15 | Kidney failure |

## Examples

**Input**: CMP results for 68-year-old male with DM2, CHF, on lisinopril and furosemide. Na 131, K 5.8, BUN 45, Cr 2.1 (baseline 1.4), Glucose 210, CO2 18, Ca 8.2, Albumin 2.8.

**Explanation (abbreviated)**:
- CRITICAL: K+ 5.8 — hyperkalemia likely multifactorial (ACEi + worsening renal function). Immediate EKG needed. Consider holding lisinopril, kayexalate, recheck in 2 hours
- Cr 2.1 (baseline 1.4): Acute kidney injury, likely pre-renal given CHF context. BUN:Cr ratio 21:1 supports pre-renal etiology. Assess volume status, consider holding/reducing furosemide
- Na 131: Mild hyponatremia, likely hypervolemic in CHF context. Fluid restriction
- CO2 18: Low, non-anion-gap metabolic acidosis, consistent with renal tubular acidosis in AKI
- Ca corrected: 8.2 + 0.8 x (4.0 - 2.8) = 9.16 — corrected calcium is normal
- Glucose 210: Uncontrolled, assess medication adherence, consider adjustment when renal function stabilizes

## Guidelines

1. **Always flag critical values prominently** — these require immediate clinical action
2. **Contextualize, do not just report** — raw abnormal flags without context are not clinically useful
3. **Account for medication effects** — many abnormalities are expected consequences of treatment
4. **Calculate derived values** — anion gap, corrected calcium, eGFR, BUN:Cr ratio
5. **Correlate across panels** — patterns spanning multiple tests are more informative than isolated values

## Validation Checklist

- [ ] All critical values are prominently flagged with immediate action recommendations
- [ ] Reference ranges are adjusted for patient demographics (age, sex, pregnancy)
- [ ] Medication effects on lab values are identified and noted
- [ ] Derived values (anion gap, corrected calcium, eGFR) are calculated where applicable
- [ ] Inter-test correlations and diagnostic patterns are identified
- [ ] Trend analysis is provided when historical data is available
- [ ] Each abnormal result includes a clinical explanation specific to the patient context

## HIPAA Compliance Notes

- Lab results are PHI and must be handled with appropriate access controls
- Lab explanation reports stored or transmitted must be encrypted (AES-256 at rest, TLS 1.2+ in transit)
- De-identify lab data used for educational or research purposes
- Critical value notifications must follow institutional notification policies and CLIA regulations
- Patient access to their own lab results is required under HIPAA and 21st Century Cures Act information blocking rules
