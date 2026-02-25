---
name: chronic-condition-cohorting
description: Cohort and segment chronic disease patient populations using clinical registries, claims data, and risk models. Use when building disease-specific cohorts, stratifying patients by severity, analyzing chronic condition prevalence, or preparing population segments for care management programs.

metadata:
  display_name: "Chronic Condition Cohorting"
  short_description: "Segment chronic disease patients into risk-based cohorts"
  default_prompt: "Analyze my chronic condition cohorting and recommend clear next actions"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Chronic Condition Cohorting

## Overview

This skill segments patient populations into clinically meaningful chronic disease cohorts using diagnosis codes, lab values, pharmacy claims, and utilization patterns. It applies CMS Chronic Conditions Warehouse (CCW) algorithms, HCC groupings, and clinical severity staging to produce actionable patient segments for care management, quality reporting, and risk stratification.

## When to Use

- Building disease registries for diabetes, COPD, CHF, CKD, or other chronic conditions
- Stratifying patients within a cohort by acuity, complexity, or progression risk
- Identifying patients with multiple chronic conditions (MCC) for care coordination
- Preparing cohort definitions for quality measure denominators (HEDIS, MSSP)
- Feeding downstream analytics such as risk adjustment, cost prediction, or care gap detection

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Claims/encounter data | Diagnosis codes (ICD-10-CM), procedure codes, revenue codes | Structured tables |
| Enrollment/eligibility | Coverage periods, LOB, plan type | Member-month records |
| Pharmacy claims | NDC codes, days supply, therapeutic class | Prescription records |
| Lab results (optional) | HbA1c, eGFR, BNP, lipid panels | Discrete lab values |
| Demographics | Age, sex, zip code, race/ethnicity (if available) | Patient master |

## Methodology

### Step 1 — Define Condition Algorithms

Apply CMS CCW reference algorithms or custom clinical logic. Each condition requires:

- **Inclusion ICD-10 codes**: Primary and secondary diagnosis positions
- **Look-back window**: Typically 1-2 years of claims history
- **Minimum claim count**: Usually ≥ 2 outpatient or ≥ 1 inpatient to confirm chronic presence
- **Exclusion logic**: Rule out rule-out diagnoses, lab-only encounters

For HCC-based grouping, map ICD-10 codes through the CMS-HCC v28 model crosswalk to assign HCC categories and hierarchical condition interactions.

### Step 2 — Apply Severity Staging

Within each condition cohort, assign clinical severity tiers:

- **Diabetes**: Use HbA1c ranges (<7% controlled, 7-9% moderate, >9% uncontrolled), presence of complications (retinopathy HCC 27, neuropathy, nephropathy HCC 18)
- **CKD**: Stage by eGFR (G1-G5) per KDIGO guidelines; flag dialysis dependence
- **COPD**: Stratify by exacerbation frequency, oxygen dependence, FEV1 if available
- **CHF**: NYHA functional class proxy via utilization intensity and BNP levels

### Step 3 — Identify Multi-Morbidity Patterns

Cross-tabulate conditions to detect clinically significant comorbidity clusters:

- Cardiometabolic syndrome (diabetes + hypertension + dyslipidemia)
- Cardio-renal overlap (CHF + CKD stages 3-5)
- Behavioral health comorbidity (any chronic condition + depression/anxiety/SUD)

Calculate Elixhauser or Charlson comorbidity indices as supplementary complexity scores.

### Step 4 — Segment by Utilization and Cost

Overlay utilization data on clinical cohorts:

- **Rising risk**: Patients with worsening lab trends or increasing visit frequency but low current cost
- **High utilizers**: Top 5% by total cost of care; ≥ 3 ED visits or ≥ 2 inpatient admissions in 12 months
- **Stable managed**: Controlled metrics, regular PCP engagement, low acute utilization

### Step 5 — Apply Attribution and Geographic Filters

- Attribute patients to primary care providers using plurality-of-visits or formal panel assignment
- Apply geographic overlays (HSA, HRR, zip-code clusters) for regional analysis
- Filter by line of business (Commercial, Medicare Advantage, Medicaid, ACA Exchange)

### Step 6 — Validate Cohort Integrity

- Compare prevalence rates against CDC national benchmarks (e.g., 11.6% diabetes prevalence nationally)
- Verify cohort sizes are statistically meaningful for planned analyses
- Check for coding artifacts: suspiciously uniform diagnosis patterns, missing demographic segments
- Reconcile against clinical registries or EHR problem lists where available

### Step 7 — Document Cohort Definitions

Produce a cohort specification document including:

- Exact ICD-10, CPT, NDC code lists used
- Look-back windows and minimum claim thresholds
- Exclusion criteria and rationale
- Date ranges and data sources
- Cohort size, demographic composition, and prevalence benchmarks

## Output Specification

```
Cohort Report:
├── Cohort Summary Table (condition, N, prevalence, avg RAF, avg cost PMPM)
├── Severity Distribution (tier counts and percentages per condition)
├── Comorbidity Matrix (co-occurrence rates for top 10 conditions)
├── Rising Risk Segment (patients meeting escalation criteria)
├── Provider Attribution Summary (panel sizes, condition density)
├── Geographic Heat Map Data (prevalence by zip/HSA)
└── Cohort Definition Appendix (full algorithm specification)
```

## Analysis Framework

### Prevalence Benchmarking

Compare observed prevalence against:
- CDC Chronic Disease Indicators for national/state rates
- AHRQ HCUP data for inpatient condition mix
- Plan-specific historical trends (year-over-year)

### Risk Stratification Matrix

| Dimension | Low | Medium | High |
|-----------|-----|--------|------|
| Clinical severity | Controlled metrics | Moderate decompensation | Uncontrolled / complications |
| Utilization intensity | PCP-only engagement | Specialist referrals | ED/IP heavy |
| Cost trajectory | Stable or declining | Moderate growth | Rapid escalation |
| Comorbidity burden | 0-1 chronic conditions | 2-3 conditions | 4+ conditions |

### Cohort Quality Metrics

- Sensitivity: Percentage of known disease patients captured
- Specificity: Rate of false-positive inclusion
- Stability: Month-over-month cohort membership churn rate (target < 5%)

## Examples

**Example 1 — Diabetes Cohort for MA Plan**
Build a Type 2 diabetes cohort for a 45,000-member Medicare Advantage plan. Apply CCW diabetes algorithm (ICD-10 E11.x, look-back 24 months, ≥ 2 outpatient claims). Layer HbA1c severity staging. Identify 5,400 diabetics (12% prevalence). Segment into controlled (58%), moderate (28%), uncontrolled (14%). Flag 756 members with diabetic CKD overlap for nephrology co-management.

**Example 2 — Multi-Condition Rising Risk**
Across a 200,000-member commercial population, identify members with ≥ 2 chronic conditions whose cost trajectory has increased > 20% over the prior 6 months while severity indicators worsen. Produce a list of 3,200 rising-risk members for care management outreach prioritization.

## Guidelines

- Always use the most current CMS-HCC model version (v28 for payment year 2025+) for risk-adjusted analyses
- Apply minimum cell-size suppression (n ≥ 11) for any patient-level or sub-group reporting per CMS cell-size policy
- Validate ICD-10 codes against current fiscal year code sets; retired codes produce false negatives
- Separate incident (new-onset) from prevalent (existing) cases when trend analysis requires it
- Document all assumptions, especially around look-back windows and claim-count thresholds

## Validation Checklist

- [ ] Cohort prevalence rates are within ±20% of CDC/national benchmarks
- [ ] No single provider accounts for > 30% of cohort (attribution skew check)
- [ ] Severity tiers sum to 100% of cohort membership
- [ ] Comorbidity rates are biologically plausible (e.g., T1D + T2D co-occurrence should be near zero)
- [ ] Enrollment gaps are handled (continuous enrollment requirement documented)
- [ ] Cohort definition is fully reproducible from documented algorithm
- [ ] Minimum cell-size suppression applied to all sub-group outputs

## HIPAA Compliance

This skill processes Protected Health Information (PHI). All outputs must comply with HIPAA Privacy and Security Rules. Apply minimum necessary standards, de-identify data where feasible using Safe Harbor or Expert Determination methods (45 CFR §164.514), and ensure all patient-level outputs are transmitted and stored in accordance with organizational BAA and data governance policies. Never include direct identifiers (name, SSN, MRN) in analytical outputs without explicit authorization.
