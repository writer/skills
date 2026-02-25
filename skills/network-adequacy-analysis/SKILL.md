---
name: Network Adequacy Analysis
description: Assess provider network adequacy against CMS, state, and NCQA standards for time-distance, provider-to-member ratios, appointment wait times, and essential community provider requirements to ensure regulatory compliance and member access.

metadata:
  display_name: "Network Adequacy Analysis"
  short_description: "Assess provider network adequacy against CMS standards"
  default_prompt: "Analyze my network adequacy and recommend clear next actions"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Network Adequacy Analysis

## Overview

This skill evaluates healthcare provider network adequacy against regulatory requirements from CMS (42 CFR 438.68 for Medicaid, Medicare Advantage network adequacy), state insurance department standards, and NCQA accreditation criteria. Network adequacy ensures health plan members have reasonable access to covered services within acceptable time, distance, and availability parameters. Inadequate networks result in regulatory penalties, member complaints, delayed care, and potential CMS sanctions. This skill performs comprehensive quantitative analysis across time-distance, provider ratios, and appointment availability dimensions.

## When to Use

- Preparing for CMS network adequacy reviews (Medicare Advantage, Medicaid managed care)
- Responding to state insurance department network filing requirements
- Supporting NCQA health plan accreditation or re-accreditation
- Evaluating network impact of provider terminations, retirements, or practice closures
- Assessing network for new market entry or service area expansion
- Analyzing member access complaints and grievances related to provider availability
- Informing provider recruitment and contracting strategy
- Evaluating adequacy for special populations (behavioral health, pediatrics, OB/GYN)

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `provider_network` | Contracted providers with specialty, address, accepting status, panel capacity | JSON array |
| `member_data` | Member distribution by zip code, age, sex, plan type, special needs | JSON object |
| `regulatory_standards` | Applicable CMS, state, and NCQA time-distance and ratio requirements | JSON object |
| `geo_data` | Road network and public transit data for travel time calculations | JSON object |
| `appointment_availability` | Secret shopper or reported appointment availability data | JSON object |
| `grievance_data` | Access-related member grievances and complaints | JSON array |
| `essential_community_providers` | ECP list and contracting status | JSON array |

## Methodology

### Step 1: Provider Inventory Validation
- Validate provider network data accuracy:
  - Confirm provider active status (not deceased, retired, or relocated)
  - Verify accepting new patients status (critical for adequacy assessment)
  - Confirm practice location addresses are current
  - Validate specialty taxonomy codes (NUCC taxonomy)
  - Identify ghost network providers (contracted but not actually available)
  - Cross-reference with NPPES database for active NPI status
- Calculate effective network size (only providers actively accepting plan members)
- CMS No Surprises Act and Transparency requirements: directory accuracy within 48 hours of changes

### Step 2: Time-Distance Analysis
- Apply CMS and state-specific time-distance standards by provider type and county designation:
  - **CMS Medicare Advantage standards** (by county type):
    - Primary Care: Large Metro 10 min, Metro 15 min, Micro 30 min, Rural 40 min, CEAC 60 min
    - Cardiology: Large Metro 20 min, Metro 30 min, Micro 60 min, Rural 75 min, CEAC 110 min
    - Behavioral Health: Large Metro 15 min, Metro 25 min, Micro 45 min, Rural 60 min, CEAC 90 min
    - Hospital: Large Metro 20 min, Metro 30 min, Micro 45 min, Rural 60 min, CEAC 75 min
  - Calculate drive time from each member zip code centroid to nearest 2 network providers per specialty
  - Identify members exceeding time-distance standards (compliance gap)
  - Calculate percentage meeting standard per specialty per county (target: 90% of members)
- Apply state-specific standards where more stringent than CMS
- Document distance methodology (driving, public transit, straight line)

### Step 3: Provider-to-Member Ratio Analysis
- Calculate ratios by specialty per service area:
  - Primary Care: benchmark 1:1,500 to 1:2,500 (varies by state)
  - Behavioral Health: benchmark 1:1,000 to 1:2,000
  - OB/GYN: 1:2,000 to 1:3,000
  - Pediatrics: 1:1,500 to 1:2,500
- Adjust for provider FTE (part-time providers count proportionally)
- Adjust for provider panel capacity (a provider at 95% panel capacity provides minimal access)
- Compare to regulatory requirements and peer plan benchmarks
- Flag specialties falling below minimum ratio thresholds

### Step 4: Appointment Availability Assessment
- Measure actual appointment availability (not just contracted presence):
  - **Secret shopper surveys**: Call network providers requesting appointments as new patients
  - **Appointment wait time standards**:
    - Urgent care: 24-48 hours
    - Primary care routine: 7-14 days (varies by state)
    - Specialist routine: 14-30 days
    - Behavioral health non-urgent: 10-14 business days (NCQA)
    - Prenatal care (first trimester): 14 days
  - Measure actual wait times against applicable standards
  - Identify providers who are contracted but have excessive wait times (de facto inadequacy)
- Calculate appointment availability scores by specialty and geography

### Step 5: Essential Community Provider (ECP) Analysis
- Evaluate ECP contracting compliance:
  - CMS requires QHP issuers to contract with minimum 35% of available ECPs in service area
  - Identify all ECPs in service area from HHS ECP list:
    - Federally Qualified Health Centers (FQHCs)
    - Ryan White HIV/AIDS providers
    - Family planning providers
    - Indian Health Service providers
    - DSH hospitals
    - Critical access hospitals
    - Children's hospitals
  - Calculate ECP contracting percentage by category
  - Identify uncontracted ECPs with strategic importance (high utilization, underserved areas)

### Step 6: Gap Remediation Planning
- For each identified adequacy gap:
  - Quantify the gap (number of members affected, severity)
  - Identify remediation options:
    - Provider recruitment or contracting in gap areas
    - Single-case agreements for members in underserved areas
    - Telehealth extension to expand geographic reach
    - Transportation assistance programs
    - Out-of-network access at in-network cost (when no adequate option exists)
  - Estimate remediation timeline and cost
  - Document alternative access standards submission to regulators (when gaps cannot be closed)
- Prepare regulatory filing with gap analysis and remediation plans

## Output Specification

```yaml
network_adequacy_report:
  analysis_date: date
  service_area: string
  total_members: number
  total_network_providers: number
  effective_network_providers: number
  time_distance_analysis:
    - specialty: string
      standard_minutes: number
      members_meeting_standard: number
      members_meeting_standard_pct: number
      gap_member_count: number
      gap_zip_codes: array
      compliance_status: string
  ratio_analysis:
    - specialty: string
      provider_count: number
      member_count: number
      ratio: string
      benchmark: string
      compliance_status: string
  appointment_availability:
    - specialty: string
      standard_days: number
      actual_median_days: number
      pct_meeting_standard: number
      compliance_status: string
  ecp_analysis:
    total_ecps_in_area: number
    contracted_ecps: number
    contracting_pct: number
    compliance_threshold: number
    compliance_status: string
    uncontracted_priority: array
  gaps_identified:
    - specialty: string
      gap_type: string
      severity: string
      affected_members: number
      remediation_options: array
      remediation_timeline: string
  overall_compliance_status: string
  regulatory_filing_readiness: boolean
```

## Analysis Framework

Apply the **CMS Network Adequacy Framework** (three pillars):
1. **Quantitative standards**: Time-distance and provider ratio minimums per specialty and county type
2. **Qualitative standards**: Appointment availability, cultural competency, language access, ADA accessibility
3. **Ongoing compliance**: Monitoring, reporting, and remediation processes

Enhanced with **NCQA Network Management Standards**:
- Standard 5: Provider directory accuracy
- Standard 6: Availability of practitioners
- Standard 7: Accessibility of services (after-hours, cultural, linguistic)

## Examples

**Example: Medicaid Managed Care Plan (150,000 Members, 12-County Service Area)**
- Provider network: 3,200 contracted providers (2,890 effective after ghost network removal)
- Time-distance gaps: Psychiatry fails in 4 rural counties (only 67% of members within standard)
- Ratio gaps: Endocrinology 1:8,200 (standard: 1:5,000), Dermatology 1:9,100 (standard: 1:5,000)
- Appointment availability: Behavioral health median wait 28 days (standard: 10 business days)
- ECP contracting: 72% of FQHCs contracted (above 35% threshold), but 0 of 3 Ryan White providers contracted
- Ghost network finding: 312 providers (9.7%) listed but not accepting plan members
- Priority remediation: Recruit 2 psychiatrists for rural coverage, contract with Ryan White providers, telehealth behavioral health expansion
- Regulatory filing status: 3 alternative access standard requests needed for rural psychiatry

## Guidelines

- **HIPAA Compliance**: Member geographic data used in time-distance analysis must be at zip code level, not individual addresses. Provider data is generally not PHI but may be proprietary. Grievance data must be de-identified for trend analysis.
- **CMS Regulatory Compliance**: Network adequacy is a regulatory requirement with enforcement consequences. Non-compliance can result in corrective action plans, enrollment sanctions, or contract termination. Treat adequacy analysis as compliance-critical.
- **Data Currency**: Provider directory data decays rapidly. Validate data within 90 days of analysis. Ghost network identification is a regulatory priority under the No Surprises Act.
- **Health Equity**: Analyze adequacy specifically for vulnerable populations (dual-eligible, special needs, LEP). Ensure network includes providers with cultural and linguistic competency for major demographic groups.
- **Telehealth Consideration**: Telehealth can extend geographic reach but does not fully substitute for in-person access. Apply telehealth credit cautiously per state-specific guidance on counting telehealth toward adequacy standards.

## Validation Checklist

- [ ] Provider network data validated for accuracy and currency
- [ ] Ghost network providers identified and flagged
- [ ] Time-distance analysis completed for all required specialties
- [ ] County type classifications (metro, micro, rural, CEAC) correctly applied
- [ ] Provider-to-member ratios calculated with FTE and capacity adjustments
- [ ] Appointment availability measured via secret shopper or equivalent method
- [ ] Essential community provider contracting percentage calculated
- [ ] Gaps quantified with affected member counts
- [ ] Remediation plans developed for each identified gap
- [ ] Alternative access standard requests prepared where applicable
- [ ] Health equity analysis completed for vulnerable populations
- [ ] Regulatory filing package complete and reviewed by compliance
