---
name: longitudinal-patient-summaries
description: Generate timeline-based patient summaries that synthesize clinical events, diagnoses, treatments, and utilization across multi-year care histories. Use when preparing care transition summaries, complex case reviews, care coordination briefs, or longitudinal health records for clinical decision support.

metadata:
  display_name: "Longitudinal Patient Summaries"
  short_description: "Build multi-year patient clinical event timeline summaries"
  default_prompt: "Summarize my longitudinal patient with key findings and next steps"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Longitudinal Patient Summaries

## Overview

This skill synthesizes multi-source patient data — claims, encounters, lab results, pharmacy fills, referrals, and care management notes — into a structured chronological narrative that highlights clinically significant events, treatment trajectories, care transitions, and emerging patterns. It is designed for care coordinators, hospitalists, PCPs, and case reviewers who need rapid comprehension of complex patient histories.

## When to Use

- Preparing for complex care conferences or multidisciplinary team rounds
- Creating transition-of-care summaries for patients moving between settings
- Building clinical summaries for utilization review or prior authorization support
- Generating longitudinal views for case management or care coordination
- Supporting peer-to-peer reviews with comprehensive patient context
- Compiling patient histories for quality case reviews or M&M conferences

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Claims/encounters | All claims with diagnosis, procedure codes, dates, providers, settings | Claims detail |
| Pharmacy data | Medication fills with NDC, drug name, dose, days supply, prescriber | Rx claims |
| Lab results | Lab test name, value, units, reference range, date | Lab file |
| Problem list | Active and historical diagnoses with onset dates | EHR problem list |
| Referrals | Referral orders with specialty, status, completion | Referral data |
| Care management notes | Assessments, care plans, interventions, barriers | Program data |
| Hospitalizations | Admission/discharge dates, discharge disposition, DRG | IP claims |

## Methodology

### Step 1 — Aggregate and Deduplicate Source Data

Consolidate all data sources into a unified patient timeline:

- Merge claims, encounters, and EHR data by patient identifier
- Deduplicate encounters (same date, same provider, same diagnosis = single event)
- Resolve date conflicts across sources (prefer encounter date over claim processed date)
- Identify and flag data gaps (periods with no claims — eligibility gap? data feed issue?)
- Tag each event with source system for provenance tracking

### Step 2 — Identify Clinically Significant Events

Apply clinical significance filters to prioritize events:

**High significance** (always include):
- Inpatient admissions and discharges with DRG and discharge disposition
- ED visits with primary diagnosis
- Surgical procedures (CPT 10000-69999)
- New chronic condition diagnoses (first occurrence of HCC-mapped condition)
- Medication starts/stops for chronic disease or high-risk medications
- Abnormal lab results outside critical thresholds
- ICU stays, intubation, code events

**Medium significance** (include for relevant conditions):
- Specialist referrals and consultation notes
- Imaging studies with significant findings
- Medication dose changes
- Care management enrollment/transitions
- DME orders (oxygen, CPAP, mobility devices)

**Low significance** (summarize in aggregate):
- Routine PCP visits without new findings
- Stable lab results within normal limits
- Pharmacy refills at same dose
- Preventive services (flu shot, wellness visit)

### Step 3 — Construct Chronological Timeline

Organize events into a structured timeline:

```
[Date] | [Setting] | [Event Type] | [Description] | [Key Details]
────────────────────────────────────────────────────────────────────
2024-01-15 | PCP      | Office Visit  | Annual wellness  | BP 142/88, HbA1c 7.8%
2024-02-03 | ED       | ED Visit      | Chest pain       | Troponin neg, d/c home
2024-03-10 | PCP      | Office Visit  | DM follow-up     | Metformin → +glipizide
2024-04-22 | Hospital | Admission     | CHF exacerbation | DRG 291, LOS 4 days
2024-04-26 | Hospital | Discharge     | CHF              | Home with home health
2024-05-01 | Home     | Care Mgmt     | TCM enrollment   | 7-day follow-up scheduled
```

### Step 4 — Extract Problem Trajectories

For each active chronic condition, trace its longitudinal trajectory:

- **Onset**: When first diagnosed, initial severity, initial treatment
- **Progression**: Key milestone events (complications, hospitalizations, medication escalations)
- **Current state**: Most recent status indicators (labs, functional status, symptoms)
- **Treatment history**: Medications tried, procedures performed, specialist involvement
- **Gaps**: Missed screenings, medication non-adherence signals, lost-to-follow-up periods

### Step 5 — Identify Care Patterns and Red Flags

Analyze the timeline for clinically concerning patterns:

- **Fragmented care**: Multiple providers for same condition without coordination evidence
- **Polypharmacy risk**: ≥ 10 concurrent medications, drug-drug interaction potential
- **Frequent ED use**: ≥ 3 ED visits in 6 months for ambulatory-sensitive conditions
- **Readmission risk**: Hospitalization within 30 days of prior discharge
- **Medication adherence signals**: Gaps in refill patterns, therapeutic switching
- **Declining trajectory**: Worsening lab trends, escalating utilization, increasing acuity

### Step 6 — Generate Narrative Summary

Compose a structured narrative with three sections:

**Clinical Synopsis** (1 paragraph):
Key conditions, current status, recent significant events, overall trajectory (stable, improving, declining).

**Active Problem Summary** (per condition):
Condition name, duration, severity, current treatment, last relevant metric, next action needed.

**Care Coordination Notes**:
Current care team, recent transitions, active care management programs, identified barriers, upcoming appointments or pending orders.

### Step 7 — Format for Target Use Case

Adapt the summary format to the intended consumer:

| Use Case | Format | Emphasis |
|----------|--------|----------|
| Care conference | Concise brief (1 page) | Active problems, recent changes, decisions needed |
| Transition of care | CCD/C-CDA compatible | Medications, allergies, diagnoses, recent procedures |
| Case review | Detailed timeline | Chronological completeness, decision points |
| UM/prior auth | Clinical justification | Medical necessity evidence, treatment history |
| PCP handoff | Problem-oriented summary | Problem list, medications, pending items |

## Output Specification

```
Longitudinal Patient Summary:
├── Patient Overview (demographics, coverage, attribution, risk score)
├── Clinical Synopsis (1-paragraph narrative summary)
├── Chronological Timeline (all significant events, filterable)
├── Problem Trajectory Cards (per active condition)
├── Medication Timeline (current list, historical starts/stops)
├── Utilization Summary (IP, ED, specialist visit counts and trends)
├── Lab Trend Panels (key labs with sparkline trends)
├── Red Flag Alerts (identified concerning patterns)
├── Care Team Directory (active providers with roles)
└── Pending Actions (upcoming appointments, open orders, care gaps)
```

## Analysis Framework

### Patient Complexity Score

| Factor | Low (1) | Medium (2) | High (3) |
|--------|---------|------------|----------|
| Chronic conditions | 0-1 | 2-3 | 4+ |
| Medications | 0-4 | 5-9 | 10+ |
| Hospitalizations (12 mo) | 0 | 1 | 2+ |
| Active providers | 1-2 | 3-4 | 5+ |
| SDOH barriers | None identified | 1-2 | 3+ |

Total score: 5-7 = low complexity, 8-11 = moderate, 12-15 = high complexity.

### Recency Weighting

Apply recency weighting to prioritize recent events:
- Last 30 days: Full detail, all events included
- 31-90 days: Significant events only
- 91-365 days: High-significance events and condition milestone markers
- > 1 year: Condition onset dates, major surgeries, key diagnostic events only

## Examples

**Example 1 — Complex Chronic Patient Summary**
Generate a longitudinal summary for a 72-year-old Medicare patient with diabetes, CHF, CKD stage 3, and depression. Three-year history includes 4 hospitalizations (2 CHF, 1 AKI, 1 pneumonia), 8 ED visits, 14 specialist encounters, and 22 active medications. Highlight declining eGFR trend (52→38 over 18 months), three CHF medication changes, and recent antidepressant start. Flag polypharmacy and fragmented care (cardiology and nephrology with no shared care plan).

**Example 2 — Transition of Care Summary**
Prepare a discharge-to-SNF transition summary for a patient hospitalized for hip fracture surgery. Include: surgical details, post-op course, current medications (with pre-admission reconciliation), functional status, weight-bearing restrictions, PT/OT recommendations, follow-up appointments, and red flags requiring ED return. Format as structured CCD-compatible document.

## Guidelines

- Always verify patient identity matching across data sources before merging
- Prioritize clinical accuracy over completeness — better to flag uncertainty than to include erroneous data
- Include data provenance for all clinical assertions (which source system, which encounter)
- Apply clinical judgment in significance filtering — not all claims data represents true clinical events
- Use standardized terminology (SNOMED-CT for problems, RxNorm for medications) where possible

## Validation Checklist

- [ ] Patient identity confirmed across all data sources
- [ ] Timeline is chronologically correct with no impossible date sequences
- [ ] Active medication list reconciled against pharmacy claims
- [ ] Problem list validated against diagnosis history
- [ ] No data gaps unexplained (eligibility gaps documented)
- [ ] Red flag patterns are clinically valid and actionable
- [ ] Summary length is appropriate for target use case

## HIPAA Compliance

This skill processes detailed Protected Health Information (PHI) including complete patient medical histories. All outputs must comply with HIPAA Privacy and Security Rules. Longitudinal summaries contain highly sensitive PHI and must be transmitted only through secure, encrypted channels. Access must be limited to individuals with treatment, payment, or health care operations authorization. Apply minimum necessary standards — include only information relevant to the stated use case. Maintain audit logs of all summary generation and access. Never store patient summaries in unsecured locations or transmit via unencrypted email.
