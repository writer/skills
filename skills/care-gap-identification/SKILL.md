---
name: care-gap-identification
description: Identify missing or overdue care steps against HEDIS, STAR, USPSTF, and disease-specific quality measures for individual patients or populations. Use when performing care gap analysis, generating patient outreach lists, preparing for quality measure reporting, or supporting value-based care performance improvement.

metadata:
  display_name: "Care Gap Identification"
  short_description: "Find missing care steps against HEDIS and STAR measures"
  default_prompt: "Review my care gap and highlight top risks and next actions"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Care Gap Identification

## Overview

Systematically identify missing, overdue, or incomplete care activities by comparing patient clinical records against evidence-based quality measures and preventive care guidelines. This skill evaluates compliance with HEDIS (Healthcare Effectiveness Data and Information Set), CMS Star Ratings, USPSTF recommendations, and disease-specific protocols to surface actionable care gaps for individual patients or population panels.

## When to Use

- Running care gap analyses for patient panels or individual patients
- Preparing for HEDIS or STAR rating measurement periods
- Generating patient outreach lists for preventive services
- Supporting value-based care contract performance
- Identifying gaps before annual wellness visits or chronic care appointments
- Building quality dashboards with gap closure tracking

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Patient clinical record | Diagnoses, procedures, labs, medications, demographics | Structured object |
| Applicable measure set | HEDIS, STAR, MIPS, or custom measure set | Enum or array |
| Measurement period | Calendar year or custom date range | Date range |
| Claims/encounter data | Service dates and codes for completed services | Array |
| Pharmacy data | Filled prescriptions with dates and days supply | Array |

## Methodology

### Step 1: Measure Applicability Determination

Identify which quality measures apply based on patient demographics and conditions:

1. Evaluate age, sex, and insurance type against measure denominators
2. Check active diagnoses for disease-specific measures (diabetes, hypertension, depression)
3. Apply exclusion criteria (hospice, terminal illness, denominator exclusions)
4. Generate the applicable measure list for this patient

### Step 2: Service History Evaluation

For each applicable measure, check if the required service has been completed:

- **Screenings**: Was the test performed within the required interval?
- **Immunizations**: Is the vaccine series complete and current?
- **Chronic disease management**: Were required labs and visits completed?
- **Medication adherence**: Does PDC (Proportion of Days Covered) meet threshold?
- **Follow-up care**: Were post-event follow-ups completed within required timeframes?

### Step 3: Gap Classification

Classify each gap by type and urgency:

| Gap Type | Description | Example |
|----------|-------------|---------|
| Overdue screening | Preventive service past due | Mammogram overdue by 8 months |
| Missing lab | Required monitoring lab not done | HbA1c not done in 12 months for diabetic |
| Medication gap | PDC below threshold or Rx not filled | Statin PDC at 72% (threshold 80%) |
| Missing follow-up | Required follow-up not completed | No 7-day follow-up after MH hospitalization |
| Immunization due | Vaccine not current | Pneumococcal vaccine not administered for 65+ |
| Assessment missing | Required screening tool not administered | PHQ-9 not done for depression patient |

### Step 4: Priority Scoring

Score each gap by clinical impact and measure weight:

**Priority Factors:**
- Clinical urgency (immediate health impact vs. long-term prevention)
- Measure weight in quality programs (triple-weighted STAR measures carry more impact)
- Time sensitivity (approaching measure close date, overdue duration)
- Patient risk level (high-risk patients have amplified gap impact)
- Contractual significance (tied to value-based payment)

### Step 5: Intervention Recommendation

For each identified gap, recommend closure actions:

- Specific service needed with CPT/HCPCS code
- Preferred provider or care setting
- Patient outreach method (phone, portal message, mail)
- Scheduling guidance (combine with upcoming visit if possible)
- Documentation requirements for measure credit

## Output Specification

The output includes:

**patient_summary**: demographics, risk_level, payer, applicable_measure_count

**applicable_measures**: measure_id, measure_name, domain (preventive/chronic/behavioral/medication), denominator_criteria_met, exclusions_evaluated

**identified_gaps**: measure_id, measure_name, gap_type, gap_description, last_completed_date (if ever), due_date, overdue_by, priority_score, clinical_urgency, closure_action with CPT code and service description, estimated_effort

**gap_summary_by_domain**: domain, total_measures, gaps_found, gap_rate

**closed_measures**: measures where criteria are met (for completeness tracking)

**outreach_recommendations**: patient contact preferences, suggested outreach message, scheduling recommendations

## Analysis Framework

### Key HEDIS/STAR Measures

| Measure ID | Measure Name | Service Required | Frequency |
|-----------|--------------|-----------------|-----------|
| BCS | Breast Cancer Screening | Mammography | Every 2 years, age 50-74 |
| CCS | Cervical Cancer Screening | Pap/HPV test | Every 3-5 years, age 21-64 |
| COL | Colorectal Cancer Screening | Colonoscopy/FIT/Cologuard | Per modality schedule, 45-75 |
| CDC-HbA1c | Diabetes: HbA1c Testing | HbA1c lab | Annual |
| CDC-Eye | Diabetes: Eye Exam | Retinal exam | Annual |
| CDC-Kidney | Diabetes: Kidney Health | eGFR + uACR | Annual |
| CBP | Controlling High Blood Pressure | BP reading under 140/90 | Annual |
| SPC | Statin Use in CVD | Statin therapy + PDC 80%+ | Ongoing |
| FUH | Follow-Up After MH Hospitalization | Outpatient visit | 7 and 30 days post-discharge |

### Medication Adherence Measures (Triple-Weighted in STAR)

- **Diabetes medications**: PDC threshold 80%
- **RAS antagonists (hypertension)**: PDC threshold 80%
- **Statins (cholesterol)**: PDC threshold 80%

PDC = (Total days covered by fills in period) / (Days in measurement period) x 100

## Examples

**Input**: 58-year-old female with type 2 diabetes, hypertension, on metformin and lisinopril. Last HbA1c: 14 months ago. Last mammogram: 3 years ago. Last eye exam: 2 years ago. Statin not prescribed despite ASCVD risk score >20%.

**Gaps Identified**:
1. CDC-HbA1c: OVERDUE (14 months, annual required) — Priority: HIGH. Action: Order HbA1c lab
2. BCS: OVERDUE (3 years, every 2 years required) — Priority: HIGH. Action: Schedule mammogram
3. CDC-Eye: OVERDUE (2 years, annual required) — Priority: MEDIUM. Action: Refer to ophthalmology
4. SPC: NOT MET (statin not prescribed, ASCVD risk >20%) — Priority: HIGH. Action: Prescribe statin therapy
5. CDC-Kidney: UNKNOWN (no eGFR/uACR on file) — Priority: MEDIUM. Action: Order renal panel with uACR

## Guidelines

1. **Apply exclusions before flagging gaps** — ensure patients are truly in the measure denominator
2. **Check supplemental data sources** — patients may have completed services outside the primary system
3. **Combine gap closure with existing visits** — maximize efficiency by bundling services
4. **Prioritize triple-weighted measures** for STAR rating impact
5. **Track gap closure rates over time** to measure program effectiveness

## Validation Checklist

- [ ] All applicable measures are identified based on demographics and conditions
- [ ] Exclusion criteria are properly evaluated before flagging gaps
- [ ] Gap dates are calculated correctly against measurement period requirements
- [ ] Priority scoring reflects both clinical urgency and quality program impact
- [ ] Closure actions include specific CPT/HCPCS codes and service descriptions
- [ ] Medication adherence gaps include current PDC calculations
- [ ] Output distinguishes between "never done" and "overdue" gaps

## HIPAA Compliance Notes

- Care gap data involves PHI and must be processed within BAA-covered systems
- Patient outreach for gap closure must comply with communication preferences and consent
- Population-level gap reports should be de-identified for quality improvement analysis
- Share gap data with contracted providers only under appropriate data use agreements
- Medication adherence data sourced from pharmacy claims requires appropriate authorization chains
