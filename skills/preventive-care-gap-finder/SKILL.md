---
name: preventive-care-gap-finder
description: Identify missed preventive care opportunities using HEDIS measures, USPSTF recommendations, and ACIP immunization schedules. Use when detecting care gaps, generating patient outreach lists, measuring preventive care compliance, or supporting quality improvement programs.

metadata:
  display_name: "Preventive Care Gap Finder"
  short_description: "Find missed preventive care and screening gaps per HEDIS"
  default_prompt: "Check my preventive care gap for gaps risks and required fixes"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Preventive Care Gap Finder

## Overview

This skill analyzes claims, EHR, and eligibility data to identify patients who are overdue for evidence-based preventive services. It maps patient demographics and clinical history against HEDIS technical specifications, USPSTF A/B recommendations, and ACIP immunization schedules to produce actionable gap-closure lists with prioritization and outreach recommendations.

## When to Use

- Running quarterly or annual preventive care gap analyses for quality reporting
- Generating patient outreach lists for care gap closure campaigns
- Measuring HEDIS compliance rates for NCQA accreditation or Star Ratings
- Identifying disparities in preventive care delivery across demographics or providers
- Supporting value-based care contract quality metric performance

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Claims/encounter data | CPT, HCPCS, ICD-10 codes with dates of service | Structured claims |
| Eligibility data | Enrollment spans, LOB, benefit plan | Member-month file |
| Demographics | DOB, sex, zip code, race/ethnicity | Patient master |
| Pharmacy claims | NDC codes, fill dates | Rx claims |
| Lab results (optional) | Screening results (e.g., HbA1c, lipid panels, colonoscopy findings) | Lab file |
| Immunization registry (optional) | Administered vaccines with CVX codes | Immunization records |

## Methodology

### Step 1 — Build Eligible Population Denominators

For each preventive measure, define the eligible population per HEDIS MY2025 technical specifications:

- **Age/sex criteria**: e.g., Breast Cancer Screening (BCS) = women 50-74
- **Continuous enrollment**: Typically 12 months with no more than one 45-day gap
- **Exclusion logic**: Apply required exclusions (bilateral mastectomy for BCS, hospice, etc.)
- **Anchor date**: Measurement year end (December 31) or rolling 12-month window

Key HEDIS measures to evaluate:
- BCS (Breast Cancer Screening), CCS (Cervical Cancer Screening), COL (Colorectal Cancer Screening)
- CDC (Comprehensive Diabetes Care — HbA1c, eye exam, nephropathy)
- CBP (Controlling High Blood Pressure), AWC/WCV (Well-Child/Adolescent Visits)
- FVA/FVO (Flu Vaccinations), PNU (Pneumococcal Vaccination)

### Step 2 — Scan for Completed Services (Numerator)

Search claims and encounter data for evidence of service completion:

- Match CPT/HCPCS codes specified in HEDIS value sets (e.g., CPT 77067 for screening mammography)
- Check for equivalent services (e.g., FOBT, FIT-DNA, colonoscopy all satisfy COL)
- Apply valid date ranges (service must occur within measurement period or look-back)
- Check pharmacy claims for medication-based proxies where applicable

### Step 3 — Identify Open Gaps

Subtract numerator-compliant members from denominator to produce open-gap populations:

- Calculate gap rate per measure: `(Denominator - Numerator) / Denominator × 100`
- Assign gap priority based on: clinical urgency, time since last service, number of concurrent open gaps
- Flag patients approaching deadline for gap closure within the measurement year

### Step 4 — Apply USPSTF Supplemental Recommendations

Extend beyond HEDIS to capture USPSTF Grade A and B recommendations not in standard measure sets:

- Lung cancer screening (LDCT for 50-80 year-olds with ≥ 20 pack-year history)
- Hepatitis C screening (all adults 18-79)
- Statin use for primary prevention (USPSTF Grade B, adults 40-75 with CVD risk ≥ 10%)
- Depression screening (PHQ-2/PHQ-9 annually for all adults)
- Fall prevention counseling (≥ 65 years, community-dwelling)

### Step 5 — Prioritize and Score Gaps

Apply a composite priority score to each patient-gap combination:

| Factor | Weight | Scoring |
|--------|--------|---------|
| Clinical impact | 30% | Cancer screening > immunization > monitoring |
| Time overdue | 25% | > 24 months overdue = high, 12-24 = moderate |
| Concurrent gaps | 20% | ≥ 3 open gaps = high priority for bundled outreach |
| Quality measure impact | 15% | Gaps affecting Star Ratings or P4P bonuses weighted higher |
| Patient engagement likelihood | 10% | Prior appointment adherence, portal activity |

### Step 6 — Generate Outreach Recommendations

For each gap, produce an outreach recommendation:

- **Preferred modality**: Patient portal message, phone call, mailed reminder, text/SMS
- **Bundling opportunity**: Group multiple gaps into single visit recommendations
- **Provider routing**: Direct to PCP, specialist, or community screening event
- **Scheduling window**: Recommend specific timeframe based on measure deadline

### Step 7 — Aggregate for Quality Reporting

Roll up individual gaps into population-level quality dashboards:

- Measure-level compliance rates with trend (current vs. prior year)
- Provider-level variation (identify low-performing panels)
- Demographic stratification (age, sex, race/ethnicity, geography)
- Projected year-end rates based on current closure velocity

## Output Specification

```
Gap Analysis Report:
├── Executive Summary (total gaps, top 5 measures by gap volume)
├── Measure-Level Dashboard (denominator, numerator, rate, benchmark, trend)
├── Patient Gap List (member ID, open gaps, priority score, outreach recommendation)
├── Provider Scorecard (panel size, gap rate by measure, peer comparison)
├── Disparity Analysis (gap rates by race/ethnicity, age band, geography)
├── Projected Year-End Rates (current trajectory vs. target)
└── Methodology Appendix (measure specs, value sets, exclusions applied)
```

## Analysis Framework

### Quality Benchmarks

| Measure | HEDIS 50th %ile | HEDIS 90th %ile | Star Rating 4-Star |
|---------|-----------------|-----------------|---------------------|
| BCS | 77.2% | 85.1% | ≥ 79% |
| COL | 72.8% | 82.4% | ≥ 75% |
| CDC HbA1c Control | 60.1% | 72.3% | ≥ 65% |
| CBP | 63.5% | 75.8% | ≥ 68% |

### Gap Closure Economics

Estimate financial impact of gap closure:
- Medicare Star Rating improvement: Each 0.5-star increase ≈ 3-5% quality bonus revenue
- VBC quality withhold recapture per gap closed
- Avoided downstream costs from early detection (e.g., stage I vs. stage III cancer treatment cost differential)

## Examples

**Example 1 — Medicare Advantage Annual Gap Analysis**
For a 60,000-member MA plan, run full HEDIS gap analysis across 15 Star Rating measures. Identify 18,400 total open gaps across 12,200 unique members. Prioritize 3,100 members with ≥ 3 concurrent gaps for intensive outreach. Project that closing 40% of BCS gaps would move the plan from 3.5 to 4.0 stars on that measure.

**Example 2 — Disparity-Focused Gap Detection**
Stratify colorectal cancer screening gaps by race/ethnicity and ADI quintile. Identify that members in ADI quintile 5 (most disadvantaged) have a COL compliance rate of 54% vs. 78% for quintile 1. Recommend targeted community screening events in high-ADI zip codes.

## Guidelines

- Always use the current HEDIS measurement year technical specifications; value sets update annually
- Apply HEDIS-specified exclusions exactly as documented — do not add or remove exclusions
- When claims data is incomplete, flag measures as potentially understated rather than artificially inflating rates
- Consider hybrid (chart + claims) methodology for measures where chart review significantly improves rates
- Run data completeness checks: claims lag, missing demographics, enrollment file recency

## Validation Checklist

- [ ] Denominator counts are within expected range based on plan demographics
- [ ] Exclusion rates are reasonable (e.g., bilateral mastectomy exclusion for BCS typically < 3%)
- [ ] Compliance rates fall within plausible range compared to HEDIS benchmarks
- [ ] No duplicate counting of services (same service counted once per measurement period)
- [ ] Continuous enrollment logic correctly handles gaps and benefit changes
- [ ] Value set codes match current HEDIS version
- [ ] Patient outreach list excludes deceased members and those who have disenrolled

## HIPAA Compliance

This skill processes Protected Health Information (PHI). All outputs must comply with HIPAA Privacy and Security Rules. Apply minimum necessary standards, ensure outreach lists are transmitted via secure channels, and apply de-identification per 45 CFR §164.514 for any reporting shared outside the covered entity. Patient-level gap lists must be stored in access-controlled systems with audit logging.
