---
name: Access Friction Detector
description: Systematically identify and quantify barriers to healthcare access across scheduling, geographic, financial, cultural, and digital dimensions using CMS access standards and health equity frameworks.

metadata:
  display_name: "Access Friction Detector"
  short_description: "Detect and quantify healthcare access barriers by type"
  default_prompt: "Review my access friction and highlight top risks and next actions"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Access Friction Detector

## Overview

This skill detects and quantifies friction points that prevent or delay patients from accessing healthcare services. It evaluates access across five core dimensions aligned with the Penchansky-Thomas Access Framework: availability, accessibility, accommodation, affordability, and acceptability. The analysis incorporates CMS network adequacy standards, ADA compliance requirements, and health equity benchmarks to produce actionable findings with regulatory context.

## When to Use

- Evaluating access barriers after patient complaint trend analysis reveals scheduling or availability themes
- Preparing for NCQA accreditation or CMS network adequacy reviews
- Assessing health equity impact of service changes (clinic closures, hour reductions, telehealth transitions)
- Investigating disparities in appointment wait times, no-show rates, or patient leakage by demographic
- Supporting Community Health Needs Assessment (CHNA) access components
- Designing patient access center workflows or digital front-door strategies

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `appointment_data` | Scheduling records with request date, appointment date, type, location, provider | De-identified CSV/JSON |
| `patient_demographics` | Aggregate demographic data (zip code, language, insurance, age, disability) | JSON array |
| `facility_locations` | Addresses and service hours for all access points | JSON array |
| `payer_mix` | Insurance type distribution across patient population | JSON object |
| `complaint_data` | Access-related complaints categorized by theme | JSON array |
| `telehealth_utilization` | Virtual visit adoption rates by service and demographic | JSON object |
| `referral_data` | Referral completion rates and time-to-appointment | JSON object |

## Methodology

### Step 1: Availability Analysis
- Calculate third-next-available appointment (TNAA) by provider, specialty, and location
- Benchmark against specialty-specific access standards:
  - Primary care: 7 days or fewer for routine, 48 hours or fewer for urgent
  - Specialty care: 14 days or fewer for routine referrals
  - Behavioral health: 10 business days or fewer (per NCQA)
  - Post-discharge follow-up: 7 days or fewer (per CMS readmission reduction)
- Identify capacity bottlenecks by day of week, time of day, and provider panel saturation
- Flag providers operating above 85% panel capacity as at-risk for access degradation

### Step 2: Accessibility Analysis (Geographic and Physical)
- Compute drive-time and public-transit-time isochrones from patient zip code centroids to facilities
- Apply CMS time-distance standards:
  - Primary care: 30 min / 15 miles (urban), 60 min / 60 miles (rural)
  - Specialty: 60 min / 30 miles (urban), 120 min / 75 miles (rural)
- Assess ADA physical accessibility for each facility (parking, entrance, exam room, equipment)
- Evaluate public transportation proximity (within 0.5 miles from transit stop)
- Map geographic deserts where access standards are not met

### Step 3: Accommodation Analysis
- Evaluate scheduling flexibility:
  - Extended hours availability (before 8 AM, after 5 PM, weekends)
  - Same-day and walk-in capacity
  - Online self-scheduling adoption rate
  - Cancellation and reschedule ease (number of steps, channels available)
- Assess communication accommodation:
  - Language services availability (interpreter access within 10 minutes per LEP standards)
  - TTY/TDD availability for deaf and hard-of-hearing patients
  - Health literacy accommodations in intake and instructions

### Step 4: Affordability Analysis
- Analyze cost-related access barriers:
  - Percentage of patients with high-deductible health plans (HDHP)
  - Financial assistance and charity care application rates and approval rates
  - Copay and cost-sharing transparency at point of scheduling
  - Prescription affordability barriers flagged in clinical notes (de-identified aggregate)
- Identify insurance-related friction:
  - Prior authorization denial rates and average turnaround time
  - Out-of-network referral frequency
  - Medicaid acceptance gaps across specialties

### Step 5: Acceptability Analysis
- Evaluate cultural and trust barriers:
  - Provider demographic concordance rates (race, ethnicity, gender, language)
  - Patient-reported experience scores segmented by demographic group
  - Trust indicators from community health assessments
  - Cultural competency training completion rates among staff
- Assess digital acceptability:
  - Patient portal adoption by age group and digital literacy level
  - Telehealth utilization disparities by race, age, rurality, and insurance
  - Digital divide indicators (broadband access rates by patient zip code)

### Step 6: Friction Scoring and Prioritization
- Assign composite friction scores per dimension (0-100):
  - 0-25: Low friction (meeting standards)
  - 26-50: Moderate friction (approaching risk)
  - 51-75: High friction (below standards, action needed)
  - 76-100: Critical friction (regulatory or equity risk)
- Aggregate into an overall Access Friction Index (AFI)
- Rank barriers by population impact (number of patients affected multiplied by severity)

## Output Specification

```yaml
access_friction_report:
  analysis_date: date
  population_scope: string
  overall_afi_score: number
  dimension_scores:
    availability: number
    accessibility: number
    accommodation: number
    affordability: number
    acceptability: number
  critical_barriers:
    - dimension: string
      barrier_description: string
      affected_population: string
      patient_count_estimate: number
      severity: string
      regulatory_reference: string
      recommendation: string
  geographic_gaps:
    - area: string
      population: number
      nearest_facility_minutes: number
      standard_exceeded_by: number
  equity_disparities:
    - metric: string
      advantaged_group_value: number
      disadvantaged_group_value: number
      gap_percentage: number
  recommendations:
    - action: string
      priority: string
      estimated_impact: string
      timeline: string
```

## Analysis Framework

Use the **Penchansky-Thomas 5A Framework** enhanced with equity stratification:

| Dimension | Core Question | Key Metrics |
|-----------|--------------|-------------|
| Availability | Is there enough supply? | TNAA, panel size, provider FTE |
| Accessibility | Can patients get there? | Drive time, transit time, ADA compliance |
| Accommodation | Does the system flex for patients? | Hours, channels, language services |
| Affordability | Can patients pay? | HDHP rates, PA denials, charity care |
| Acceptability | Will patients engage? | Concordance, cultural competency, digital divide |

## Examples

**Example: Urban Health System Access Audit**
- Availability: TNAA for dermatology = 47 days, CRITICAL (benchmark: 14 days)
- Accessibility: 12% of Medicaid patients live more than 45 min from nearest PCP, HIGH
- Accommodation: Online scheduling available for only 3 of 12 specialties, MODERATE
- Affordability: PA denial rate for behavioral health = 31%, HIGH
- Acceptability: Telehealth adoption among 65+ = 8% vs. 45% overall, Equity gap flagged
- Overall AFI: 62/100, HIGH friction, priority intervention recommended

## Guidelines

- **HIPAA Compliance**: All analysis must use de-identified or aggregate data. Geographic analysis should use zip code or census tract level, never individual addresses. Complaint data must be stripped of PHI before ingestion.
- **Regulatory Alignment**: Reference CMS network adequacy standards (42 CFR 438.68), ADA Title III requirements, and Section 1557 language access provisions in findings.
- **Equity-First Approach**: Always stratify findings by race, ethnicity, language, insurance type, disability status, and rurality. Report disparities explicitly.
- **Actionability**: Every identified barrier must include at least one specific, implementable recommendation with timeline and responsible party.
- **Community Input**: Validate findings with patient advisory councils and community health workers when possible.

## Validation Checklist

- [ ] All five access dimensions analyzed with quantitative metrics
- [ ] Benchmarks sourced from CMS, NCQA, or evidence-based standards
- [ ] Geographic analysis uses time-distance standards appropriate to urban/rural classification
- [ ] Equity stratification completed across minimum 4 demographic dimensions
- [ ] No PHI present in any output artifact
- [ ] Regulatory references cited for all standard comparisons
- [ ] Recommendations are specific, actionable, and time-bound
- [ ] Access Friction Index calculated with transparent methodology
- [ ] Findings validated against patient complaint data for consistency
- [ ] Report formatted for executive and operational audiences
