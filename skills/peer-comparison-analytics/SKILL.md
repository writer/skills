---
name: peer-comparison-analytics
description: Compare provider performance metrics against specialty-matched peers using wRVU productivity, quality outcomes, patient satisfaction, and financial benchmarks from MGMA and similar datasets. Use when evaluating provider productivity, supporting compensation discussions, identifying performance outliers, benchmarking against national standards, or developing provider improvement plans.

metadata:
  display_name: "Peer Comparison Analytics"
  short_description: "Benchmark provider performance against specialty-matched peers"
  default_prompt: "Analyze my peer comparison analytics and recommend clear next actions"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Peer Comparison Analytics

## Overview

Analyze and compare provider performance across productivity, quality, patient experience, and financial dimensions using specialty-matched peer cohorts and nationally recognized benchmarks (MGMA DataDive, AMGA, SullivanCotter). This skill enables health system leaders to identify performance variation, recognize high performers, support compensation model discussions, and develop data-driven improvement plans. Comparisons are risk-adjusted and context-appropriate, accounting for patient panel complexity, practice setting, geographic factors, and scope of practice differences that influence raw performance metrics.

## When to Use

- Annual provider performance reviews and compensation discussions
- Identifying outlier performance (high or low) for investigation
- Benchmarking provider productivity against MGMA national and specialty-specific data
- Supporting physician recruitment with competitive market data
- Evaluating practice efficiency and panel optimization opportunities
- Informing value-based contract negotiations with payer-relevant performance data
- Developing targeted provider development and improvement plans
- Assessing new provider ramp-up against expected trajectories

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `provider_data` | Provider demographics, specialty, FTE status, start date, practice setting | Structured object |
| `wrvu_data` | Work RVU production by month, CPT code, and service location | Array of records |
| `quality_metrics` | Clinical quality measures (HEDIS, MIPS, organization-specific) | Structured object |
| `patient_experience` | CG-CAHPS or organizational patient satisfaction scores | Structured object |
| `financial_data` | Collections, charges, overhead, net revenue per provider | Structured object |
| `benchmark_source` | MGMA, AMGA, SullivanCotter, or internal peer group data | Reference dataset |
| `panel_data` | Patient panel size, complexity (average HCC score), payer mix | Structured object |

## Methodology

### Step 1: Peer Cohort Definition

Define the appropriate comparison group:

**Primary Matching Criteria:**
- Specialty/subspecialty (use MGMA specialty taxonomy)
- Practice setting: academic, hospital-employed, independent, multispecialty group
- Geographic region: Eastern, Southern, Midwestern, Western (MGMA regions) or CBSA-based
- FTE status: Normalize all metrics to 1.0 FTE equivalents
- Provider type: Physician vs. APP (NP/PA) — compare within type

**Secondary Adjustments:**
- Years in practice (new providers under 3 years compared to early-career cohort)
- Scope of practice (surgical vs. non-surgical within specialty)
- Teaching responsibilities (academic FTE carved out)
- Administrative time (medical directorship, committee work carved out of clinical FTE)
- Call responsibilities and coverage obligations

### Step 2: Productivity Analysis (wRVU-Based)

Measure and benchmark clinical productivity:

**Core Productivity Metrics:**

| Metric | Calculation | MGMA Benchmark Reference |
|--------|------------|--------------------------|
| Total wRVUs | Sum of work RVUs for all billed services | MGMA median, 75th, 90th by specialty |
| wRVUs per clinical FTE | Total wRVUs / clinical FTE | Primary productivity measure |
| wRVUs per patient visit | Total wRVUs / total patient encounters | Intensity/complexity indicator |
| wRVUs per clinic session | Total wRVUs / half-day clinic sessions | Session efficiency measure |
| Monthly wRVU trend | Rolling 12-month wRVU trajectory | Seasonality and trend analysis |

**MGMA Benchmark Percentiles (Reference Examples):**

| Specialty | 25th %ile | Median | 75th %ile | 90th %ile |
|-----------|-----------|--------|-----------|-----------|
| Family Medicine | 4,200 | 5,100 | 6,200 | 7,500 |
| Internal Medicine | 3,800 | 4,600 | 5,800 | 7,200 |
| Cardiology (Non-invasive) | 5,500 | 7,200 | 9,100 | 11,500 |
| Orthopedic Surgery | 7,200 | 9,000 | 11,500 | 14,000 |
| General Surgery | 5,800 | 7,500 | 9,500 | 12,000 |

**Productivity Assessment Categories:**
- Below 25th percentile: Underperforming — investigate root causes
- 25th-50th percentile: Below median — improvement opportunity
- 50th-75th percentile: Solid performer — meets expectations
- 75th-90th percentile: High performer
- Above 90th percentile: Exceptional — verify data accuracy, assess sustainability and burnout risk

### Step 3: Quality Performance Comparison

Benchmark quality metrics against peers:

**MIPS Quality Categories (if applicable):**
- Quality: Performance on selected MIPS quality measures vs. benchmark
- Cost: Per-capita cost and episode-based cost measures
- Improvement Activities: Participation in qualifying activities
- Promoting Interoperability: EHR meaningful use metrics

**Clinical Quality Indicators:**
- Disease-specific outcome measures (e.g., HbA1c control rates, blood pressure control)
- Preventive screening rates (mammography, colonoscopy, cervical cancer screening)
- Hospital readmission rates (attributed to provider)
- Surgical complication rates (SSI, VTE, unplanned return to OR)
- Mortality rates (risk-adjusted by case mix index)

**Quality-Productivity Balance:**
- Plot quality scores against productivity — identify providers with high productivity but low quality (burnout risk) or high quality with low productivity (capacity opportunity)
- Target: both productivity and quality above specialty median

### Step 4: Patient Experience Benchmarking

Compare patient satisfaction scores:

- **CG-CAHPS domains**: Access, communication, care coordination, provider rating
- **Press Ganey or organizational survey**: Provider-specific scores by domain
- **Top-box scores**: Percentage of patients rating "always" or "definitely yes"
- **Benchmark against**: National CG-CAHPS database percentiles by specialty
- **Volume considerations**: Minimum 30 completed surveys for reliable comparison

### Step 5: Financial Performance Analysis

Evaluate financial contribution and efficiency:

| Metric | Calculation | Benchmark |
|--------|------------|-----------|
| Net collections per wRVU | Net collections / total wRVUs | MGMA by specialty |
| Total compensation per wRVU | Total comp / total wRVUs | MGMA comp-to-production ratio |
| Overhead ratio | Direct expenses / net revenue | MGMA by specialty/setting |
| Collection rate | Net collections / net charges | 95%+ is benchmark |
| Revenue per encounter | Net revenue / patient encounters | By specialty and POS |

**Compensation-to-Production Ratio Analysis:**
- Ratio below 1.0: Provider generates more revenue than compensation (financial positive)
- Ratio above 1.0: Provider compensation exceeds revenue generated (investigate)
- MGMA benchmark: Median comp-to-wRVU ratio by specialty

### Step 6: Variance Analysis and Root Cause Investigation

For providers showing significant variance from peers, investigate drivers:

- **Schedule utilization**: Are available appointment slots being filled? (Target above 85%)
- **No-show rates**: Higher no-shows reduce productivity without reducing overhead
- **Patient mix complexity**: Higher-complexity patients generate more wRVUs per visit but require more time
- **Procedure mix**: Procedural specialties with lower procedure volumes will show lower wRVUs
- **Support staff adequacy**: MA/nurse ratios, scribe utilization, APP leverage
- **Operational barriers**: Referral access, OR block time availability, EMR burden
- **Personal factors**: Part-time schedule, leave, onboarding ramp-up, approaching retirement

### Step 7: Performance Improvement Planning

Generate targeted improvement recommendations:

- **Productivity enhancement**: Schedule optimization, patient access expansion, APP integration
- **Quality improvement**: Peer learning from high performers, clinical pathway adoption
- **Experience improvement**: Communication coaching, workflow redesign for access
- **Financial optimization**: Coding education, charge capture improvement, payer mix management
- **Monitoring plan**: Monthly or quarterly review cadence with defined improvement targets
- **Recognition**: Identify and celebrate top performers to reinforce desired behaviors

## Output Specification

```yaml
peer_comparison_report:
  provider_id: string
  specialty: string
  fte: number
  reporting_period: string
  peer_cohort:
    size: number
    definition: string
    benchmark_source: string
  productivity:
    total_wrvus: number
    wrvus_per_fte: number
    percentile_rank: number
    benchmark_median: number
    variance_from_median: number
    trend: string  # improving, stable, declining
  quality:
    composite_score: number
    percentile_rank: number
    measure_details: array
  patient_experience:
    overall_rating: number
    percentile_rank: number
    domain_scores: array
  financial:
    net_collections_per_wrvu: number
    comp_to_production_ratio: number
    overhead_ratio: number
  variance_analysis:
    primary_drivers: array
    modifiable_factors: array
  improvement_plan:
    - area: string
      target: string
      actions: array
      timeline: string
      review_date: string
```

## Analysis Framework

### Balanced Performance Dashboard

Evaluate providers across four balanced dimensions:

| Dimension | Weight | Key Metrics | Data Source |
|-----------|--------|-------------|------------|
| Productivity | 30% | wRVUs per FTE, patients per day | Billing/EHR |
| Quality | 30% | Clinical outcomes, process measures | Quality registry |
| Experience | 20% | CG-CAHPS, patient ratings | Survey data |
| Citizenship | 20% | Teaching, committee work, call equity | Administrative records |

## Examples

**Example: Internal Medicine Physician Performance Review**

- Provider: Dr. Smith, Internal Medicine, 0.9 clinical FTE, academic medical center
- Annual wRVUs: 4,100 (4,556 per 1.0 FTE) — 45th percentile MGMA
- Quality composite: 82nd percentile (strong diabetes and hypertension management)
- Patient experience: 65th percentile (access scores below median, communication above)
- Collections per wRVU: $52.10 (MGMA median $48.50) — positive variance due to higher complexity mix
- Comp-to-production ratio: 1.05 (slightly above median — explained by academic FTE)
- Root cause for productivity gap: 22% no-show rate (peer average 15%), 3 half-days allocated to non-clinical duties
- Recommendation: Implement overbooking protocol for high no-show slots, verify administrative FTE is accurately carved out

## Guidelines

1. **Always normalize to FTE** — raw wRVU comparisons without FTE adjustment are misleading
2. **Use specialty-matched benchmarks** — comparing across specialties is invalid
3. **Account for practice maturity** — new providers (under 18 months) should use ramp-up trajectories
4. **Present data constructively** — performance data should support improvement, not punishment
5. **Verify data accuracy** — charge capture, provider attribution, and FTE calculation errors are common
6. **Respect Stark Law** — compensation models tied to productivity must meet fair market value and commercial reasonableness standards
7. **Consider the full picture** — no single metric tells the complete performance story

## Validation Checklist

- [ ] Peer cohort defined with appropriate matching criteria and sufficient sample size
- [ ] All metrics normalized to 1.0 FTE with academic and administrative carve-outs
- [ ] MGMA or equivalent benchmark data referenced with appropriate year and survey methodology
- [ ] Quality metrics include both process and outcome measures
- [ ] Patient experience data meets minimum sample size for reliability
- [ ] Financial analysis includes compensation-to-production ratio evaluation
- [ ] Variance analysis identifies modifiable vs. non-modifiable performance drivers
- [ ] Improvement plan includes specific actions, targets, and review timeline
- [ ] Stark Law and fair market value compliance noted for compensation discussions

## HIPAA Compliance Notes

- Provider performance data may include patient-level attribution requiring PHI protections (45 CFR 164.501)
- Aggregate performance reports should use de-identified patient data wherever possible
- Individual provider performance reports are confidential under peer review protections in many jurisdictions
- Quality metric calculations involving patient outcomes must maintain minimum necessary access (45 CFR 164.502(b))
- Benchmark data from external sources (MGMA) is typically de-identified and non-PHI
- Access to provider performance dashboards must be role-restricted (45 CFR 164.312(a))
