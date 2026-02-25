---
name: health-equity-monitoring
description: Identify and track health disparities across race, ethnicity, socioeconomic status, geography, and other equity dimensions. Use when analyzing health equity metrics, monitoring disparity trends, stratifying outcomes by social determinants, or meeting CMS health equity reporting requirements.

metadata:
  display_name: "Health Equity Monitoring"
  short_description: "Track health disparities across race, geography, and income"
  default_prompt: "Review my health equity and highlight top risks and next actions"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Health Equity Monitoring

## Overview

This skill systematically measures and monitors health disparities across patient populations using standardized equity indices, social determinant data, and stratified outcome analysis. It applies the CDC Social Vulnerability Index (SVI), Area Deprivation Index (ADI), CMS Health Equity measures, and WHO health equity frameworks to identify, quantify, and track disparities in access, quality, outcomes, and patient experience.

## When to Use

- Conducting health equity assessments for organizational strategic planning
- Monitoring disparity trends for CMS Health Equity Index or NCQA Health Equity Accreditation
- Stratifying quality measures and outcomes by race, ethnicity, language, and disability (RELD)
- Analyzing social determinant impacts on clinical outcomes and utilization
- Identifying priority populations for targeted intervention programs
- Meeting regulatory requirements for health equity data collection and reporting

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Demographics | Race, ethnicity, preferred language, sex, age, disability status | Patient master |
| SDOH data | Z-codes (Z55-Z65), SDOH screening results, ADI scores | Clinical/claims |
| Quality measures | HEDIS, Star Ratings, clinical outcomes by population | Measure data |
| Utilization data | IP, ED, outpatient visits with cost | Claims detail |
| Geographic data | Patient zip codes, census tract, FIPS codes | Address file |
| SVI/ADI reference | CDC SVI by census tract, ADI by census block group | Reference data |

## Methodology

### Step 1 — Establish Equity Stratification Dimensions

Define the dimensions for disparity analysis per CMS and NCQA frameworks:

- **Race/Ethnicity**: OMB minimum categories (White, Black/African American, Asian, AIAN, NHPI, Hispanic/Latino, multiracial); use indirect estimation (BISG) when self-reported data is incomplete
- **Language**: Preferred language, LEP status, interpreter utilization
- **Socioeconomic**: ADI national rank quintiles, dual-eligible status, Medicaid enrollment
- **Geographic**: Urban/rural (RUCA codes), SVI composite and theme scores, health professional shortage areas (HPSA)
- **Disability**: Functional limitation indicators, SNP enrollment, I/DD flags
- **Sex/Gender**: Biological sex, gender identity where captured

Assess data completeness for each dimension. Flag dimensions with > 20% missing data for imputation or exclusion decisions.

### Step 2 — Calculate Disparity Metrics

Apply standardized disparity quantification methods:

- **Absolute difference**: Rate(disadvantaged) - Rate(reference), expressed in percentage points
- **Relative difference**: Rate(disadvantaged) / Rate(reference), expressed as ratio
- **Index of Disparity (IDoD)**: Average absolute deviation across all groups from the overall mean
- **Theil Index**: Entropy-based measure of inequality across multiple groups simultaneously
- **Concentration Index**: Measures socioeconomic gradient in health outcomes

For each quality measure and outcome, calculate disparity metrics across all stratification dimensions.

### Step 3 — Map Social Vulnerability

Overlay patient populations against area-level indices:

- **CDC SVI**: Composite score and four themes (socioeconomic status, household characteristics, racial/ethnic minority status, housing type/transportation)
- **ADI**: National and state-level rankings by census block group
- **Food access**: USDA Food Access Research Atlas (food desert designation)
- **Environmental**: EPA EJScreen environmental justice indicators

Assign each patient an area-level vulnerability profile based on residential address. Calculate population distribution across vulnerability quintiles.

### Step 4 — Conduct Stratified Outcome Analysis

For each priority outcome, measure performance across equity dimensions:

- Quality measures: HEDIS rates stratified by race/ethnicity, ADI quintile, language
- Utilization: ED visit rates, preventable hospitalizations (AHRQ PQI) by SVI quartile
- Clinical outcomes: Disease control rates, mortality, complications by demographic
- Patient experience: CAHPS domain scores by race/ethnicity and language
- Access: Appointment wait times, no-show rates, telehealth utilization by geography

Apply risk adjustment (age, sex, comorbidity) to isolate disparity from case-mix differences.

### Step 5 — Identify Priority Disparity Areas

Rank disparities by severity and actionability:

| Priority | Criteria |
|----------|----------|
| Critical | > 10 percentage-point gap in life-impacting outcomes (e.g., cancer screening, chronic disease control) |
| High | 5-10 point gap in quality measures affecting Star Ratings or accreditation |
| Moderate | Statistically significant gap (p < 0.05) with < 5 point absolute difference |
| Monitor | Emerging trend or gap approaching significance threshold |

Cross-reference disparities with organizational capacity to intervene. Prioritize areas where evidence-based interventions exist.

### Step 6 — Design Equity-Focused Interventions

For each priority disparity, recommend targeted interventions:

- **Access barriers**: Mobile health units, extended hours, transportation assistance, telehealth expansion
- **Language barriers**: Interpreter services, translated materials, bilingual provider recruitment
- **Socioeconomic barriers**: Medication assistance programs, SDOH resource navigation, community health workers
- **Cultural barriers**: Culturally tailored health education, community partnership programs
- **Structural barriers**: Clinic siting analysis, network adequacy in underserved areas

### Step 7 — Establish Monitoring Dashboard

Create an ongoing equity monitoring framework:

- Define disparity reduction targets with timelines (e.g., reduce BCS disparity by 50% over 3 years)
- Establish quarterly reporting cadence with automated stratification
- Track intervention participation and engagement by target population
- Monitor for unintended consequences (improving one group while another declines)
- Report to leadership and board using CMS Health Equity Index format

## Output Specification

```
Health Equity Report:
├── Equity Dashboard Summary (overall disparity index, trend, priority areas)
├── Demographic Profile (population composition, data completeness rates)
├── Stratified Quality Measures (by race/ethnicity, ADI, language, geography)
├── Disparity Heat Map (measures × dimensions with severity coding)
├── Social Vulnerability Profile (SVI/ADI distribution, high-vulnerability segments)
├── SDOH Prevalence (screening rates, identified needs, referral completion)
├── Priority Disparity Inventory (ranked with intervention recommendations)
├── Intervention Tracking (active programs, enrollment, early outcomes)
└── CMS Health Equity Index Components (if applicable)
```

## Analysis Framework

### Disparity Classification

| Severity | Absolute Gap | Relative Ratio | Action Required |
|----------|-------------|----------------|-----------------|
| Severe | > 15 pp | > 1.50 | Immediate intervention, leadership escalation |
| Significant | 10-15 pp | 1.25-1.50 | Targeted program within 6 months |
| Moderate | 5-10 pp | 1.10-1.25 | Monitoring with improvement plan |
| Minimal | < 5 pp | < 1.10 | Continued surveillance |

### CMS Health Equity Index Components

- Collection of patient-level demographic data (race, ethnicity, language)
- SDOH screening and referral programs
- Stratified quality measure reporting
- Equity-focused quality improvement activities
- Board/leadership equity accountability

## Examples

**Example 1 — Racial Disparity in Diabetes Control**
Stratify HbA1c < 8% control rate by race/ethnicity for an MA plan. White: 72%, Black: 58%, Hispanic: 61%, Asian: 74%. Absolute gap (Black vs. White): 14 percentage points. Investigate root causes: identify that Black members have 23% lower endocrinology referral rates and 35% higher ADI scores. Recommend targeted care navigation program for Black members in high-ADI areas with diabetes.

**Example 2 — Geographic Access Disparity**
Map preventive screening completion rates by SVI quartile. SVI Q4 (highest vulnerability): BCS 62%, COL 58%. SVI Q1 (lowest vulnerability): BCS 82%, COL 79%. Deploy mobile mammography and FIT kit mailing program to Q4 zip codes. Track quarterly narrowing of gap.

## Guidelines

- Use self-reported race/ethnicity data as primary source; BISG imputation as supplement, not replacement
- Never use race as a biological variable in risk models — use as a marker of social/structural exposure
- Apply intersectional analysis where possible (e.g., race × income × geography)
- Report both adjusted and unadjusted disparity metrics — adjustment should not mask systemic inequity
- Comply with CMS data collection requirements under Section 1557 of the ACA

## Validation Checklist

- [ ] Race/ethnicity data completeness ≥ 80% (or imputation methodology documented)
- [ ] ADI/SVI data is matched to current census vintage
- [ ] Disparity metrics are calculated using validated methods
- [ ] Risk adjustment does not inappropriately attenuate real disparities
- [ ] Minimum cell-size suppression applied (n ≥ 11) for sub-group reporting
- [ ] Intervention recommendations are evidence-based and culturally appropriate
- [ ] Dashboard is designed for ongoing automated monitoring

## HIPAA Compliance

This skill processes Protected Health Information (PHI) including sensitive demographic data (race, ethnicity, language, disability status). All outputs must comply with HIPAA Privacy and Security Rules. Race and ethnicity data require particular sensitivity in storage and access controls. Apply minimum cell-size suppression (n ≥ 11) for all stratified reporting to prevent re-identification. SDOH data may carry additional state-level privacy protections. De-identify all externally shared reports per 45 CFR §164.514. Ensure data collection practices comply with Section 1557 anti-discrimination requirements.
