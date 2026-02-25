---
name: risk-adjustment-support
description: Support HCC coding accuracy, RAF score optimization, and risk adjustment documentation completeness for Medicare Advantage and ACA populations. Use when analyzing risk adjustment factor scores, identifying suspected coding gaps, validating HCC capture, or preparing for RADV audits.

metadata:
  display_name: "Risk Adjustment Support"
  short_description: "Optimize HCC coding accuracy and risk adjustment scores"
  default_prompt: "Help me with risk adjustment and give clear next steps"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Risk Adjustment Support

## Overview

This skill analyzes diagnostic coding patterns, clinical documentation, and claims data to identify risk adjustment opportunities and documentation gaps. It applies CMS-HCC v28 model logic, RAF score calculations, and coding accuracy validation to support compliant revenue integrity for Medicare Advantage, ACA marketplace, and Medicaid managed care programs.

## When to Use

- Identifying suspected HCC coding gaps where conditions are documented but not captured in claims
- Validating RAF score accuracy against clinical documentation
- Preparing for CMS Risk Adjustment Data Validation (RADV) audits
- Analyzing year-over-year RAF score trends and explaining variances
- Prioritizing provider education on condition documentation and specificity
- Estimating revenue impact of coding accuracy improvements

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Diagnosis claims | ICD-10-CM codes with claim type, provider, DOS | Claims detail |
| Member demographics | DOB, sex, Medicaid dual status, disability status | Enrollment file |
| CMS-HCC model mappings | ICD-10 to HCC crosswalk (v28) | Reference table |
| RAF score output | Current and prior year RAF scores by member | Score file |
| Clinical notes (optional) | Provider documentation for chart review validation | Unstructured text |
| Pharmacy claims (optional) | Medication history for condition inference | Rx claims |

## Methodology

### Step 1 — Map Diagnoses to HCC Categories

Process all diagnosis codes through the CMS-HCC v28 model:

- Map each ICD-10-CM code to its HCC category using the official CMS crosswalk
- Apply hierarchical logic: when multiple HCCs exist within a hierarchy, retain only the most severe
- Handle interaction terms (e.g., diabetes + CHF interaction, HCC 18 × HCC 85)
- Calculate demographic base score (age/sex/disability/dual status factors)
- Compute total RAF score: demographic factor + sum of HCC coefficients + interaction terms

### Step 2 — Identify Suspected Coding Gaps

Detect conditions likely present but not captured in current-year claims:

- **Historical drop-off**: Conditions coded in prior year but absent in current year (chronic conditions should persist)
- **Pharmacy inference**: Active prescriptions suggesting uncoded conditions (e.g., insulin without diabetes HCC, anticoagulants without AFib HCC)
- **Lab inference**: Abnormal lab values without corresponding diagnosis (e.g., eGFR < 60 without CKD code)
- **Clinical plausibility**: Comorbidity patterns suggesting missing conditions (e.g., diabetes complications without base diabetes code)

### Step 3 — Assess Documentation Specificity

Review coding specificity for revenue-impacting distinctions:

- **Diabetes**: E11.65 (with hyperglycemia, HCC 18) vs. E11.9 (without complication, HCC 19) — significant RAF difference
- **CKD staging**: N18.3 (stage 3, HCC 329) vs. N18.4 (stage 4, HCC 328) — higher RAF for advanced stages
- **Heart failure**: I50.22 (chronic systolic, HCC 85) vs. I50.9 (unspecified, HCC 85) — specificity supports RADV
- **Malnutrition**: E43 (severe, HCC 21) vs. E44.1 (mild, HCC 23) — major coefficient difference

### Step 4 — Quantify Revenue Impact

Calculate the financial impact of identified gaps and specificity improvements:

- Per-member RAF impact: multiply HCC coefficient by the CMS normalization factor and base rate
- Aggregate revenue impact: sum across identified members, apply expected capture rate (typically 60-80%)
- Segment by: condition category, provider, clinic site, and line of business
- Model scenarios: best case (100% capture), expected (70% capture), conservative (40% capture)

### Step 5 — Prioritize Provider Outreach

Rank opportunities for provider engagement:

| Priority | Criteria | Action |
|----------|----------|--------|
| Critical | High-RAF HCCs with strong clinical evidence, RADV risk | Immediate chart review + provider query |
| High | Historical drop-offs for well-documented chronic conditions | Prospective visit preparation |
| Medium | Pharmacy/lab inferred gaps needing clinical confirmation | Pre-visit medical record review |
| Low | Specificity improvements with modest RAF impact | Provider education sessions |

### Step 6 — Validate Compliance Guardrails

Ensure all risk adjustment activities comply with CMS guidelines:

- Confirm every HCC is supported by face-to-face encounter documentation
- Verify conditions meet MEAT criteria (Monitor, Evaluate, Assess/Address, Treat)
- Check that diagnoses are not carried forward without clinical re-evaluation
- Ensure no upcoding: codes must be supported by clinical documentation
- Flag any patterns suggesting problematic coding (e.g., identical HCC profiles across large patient panels)

### Step 7 — Generate RADV-Ready Documentation

Prepare audit-ready artifacts:

- Member-level HCC inventory with supporting claim references
- Documentation sufficiency scores per HCC (high/medium/low confidence)
- Provider attestation tracking for condition recapture
- Trend analysis showing RAF score changes with explanatory narratives

## Output Specification

```
Risk Adjustment Report:
├── RAF Score Summary (avg RAF, distribution, YoY change, benchmark comparison)
├── HCC Gap Inventory (suspected gaps with evidence type and confidence level)
├── Revenue Impact Model (per-member and aggregate, by scenario)
├── Specificity Opportunity List (current vs. optimal code, RAF delta)
├── Provider Scorecard (coding accuracy rate, gap density, capture trends)
├── RADV Readiness Assessment (documentation confidence by HCC)
└── Compliance Attestation (guardrail validation results)
```

## Analysis Framework

### RAF Score Benchmarking

| Population | Expected Avg RAF | Low Concern | Investigate |
|------------|-----------------|-------------|-------------|
| MA general | 0.95 - 1.10 | 0.85 - 1.20 | < 0.80 or > 1.30 |
| MA D-SNP | 1.30 - 1.60 | 1.10 - 1.80 | < 1.00 or > 2.00 |
| ACA Individual | 1.00 - 1.20 | 0.90 - 1.40 | < 0.80 or > 1.50 |

### HCC Impact Tiers (v28 Approximate Coefficients)

- **Tier 1 (RAF > 0.30)**: Severe conditions — transplant status, protein-calorie malnutrition, quadriplegia
- **Tier 2 (RAF 0.15-0.30)**: Major chronic — diabetes with complications, CHF, COPD, vascular disease
- **Tier 3 (RAF 0.05-0.15)**: Moderate chronic — specified arrhythmias, CKD 3, rheumatoid arthritis
- **Tier 4 (RAF < 0.05)**: Lower impact — hypertension (no longer in HCC model), obesity, depression

## Examples

**Example 1 — MA Plan Annual Coding Review**
Analyze 50,000 MA members. Identify 8,200 suspected HCC gaps based on historical drop-off (4,100), pharmacy inference (2,800), and lab inference (1,300). Estimate $12.4M in recoverable revenue at 70% capture rate. Prioritize top 15 provider groups covering 60% of gaps for prospective chart review.

**Example 2 — RADV Audit Preparation**
Prepare for CMS RADV audit on 200 sampled members. Score documentation confidence for each claimed HCC. Flag 34 HCCs across 22 members with low documentation confidence for pre-audit chart improvement. Estimate financial exposure of $890K if flagged HCCs are invalidated.

## Guidelines

- Use the CMS-HCC model version applicable to the current payment year (v28 for PY2025+)
- Never recommend adding diagnosis codes without supporting clinical documentation — this constitutes fraud
- Distinguish between compliant coding accuracy improvement and impermissible upcoding
- Apply CMS normalization factor to RAF scores when calculating revenue impact
- Account for coding intensity factor (CIF) adjustments applied by CMS to MA plans
- Track and report recapture rates separately from new condition capture

## Validation Checklist

- [ ] All HCC mappings use current CMS-HCC crosswalk version
- [ ] Suspected gaps have at least one supporting evidence type (historical, pharmacy, lab, clinical)
- [ ] Revenue calculations use current CMS base rate and normalization factor
- [ ] Compliance guardrails have been applied to every recommendation
- [ ] No recommendations suggest coding without face-to-face encounter documentation
- [ ] RADV confidence scores are calibrated against historical audit outcomes
- [ ] Provider scorecards use peer-adjusted benchmarks (specialty, panel complexity)

## HIPAA Compliance

This skill processes Protected Health Information (PHI) including diagnosis codes, clinical documentation, and member identifiers. All outputs must comply with HIPAA Privacy and Security Rules. Risk adjustment analytics must be conducted under covered entity or business associate authority. De-identify outputs per 45 CFR §164.514 before sharing outside authorized workforce. Audit trails must be maintained for all chart review and coding modification activities.
