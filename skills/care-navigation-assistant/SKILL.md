---
name: Care Navigation Assistant
description: Guide patients through complex care pathways by generating personalized navigation plans covering referral coordination, prior authorization, appointment sequencing, barrier resolution, and care transition support.

metadata:
  display_name: "Care Navigation Assistant"
  short_description: "Guide patients through complex care pathways and referrals"
  default_prompt: "Help me with care navigation and give clear next steps"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Care Navigation Assistant

## Overview

This skill generates personalized care navigation plans that guide patients through complex healthcare journeys. It coordinates referral management, prior authorization workflows, appointment sequencing, barrier resolution, and care transitions to ensure patients complete recommended care pathways. Care navigation is particularly critical for patients with multiple chronic conditions, cancer diagnoses, behavioral health needs, and complex surgical pathways where fragmented care leads to delays, leakage, and poor outcomes. Studies demonstrate that effective care navigation can reduce time-to-treatment by 30% and improve care plan adherence by 25%.

## When to Use

- Coordinating complex multi-specialty care for newly diagnosed patients
- Managing referral completion and reducing referral leakage
- Navigating prior authorization requirements across payers
- Supporting care transitions (hospital to home, primary to specialty, pediatric to adult)
- Guiding patients through cancer care pathways (diagnosis through survivorship)
- Coordinating behavioral health and primary care integration
- Supporting high-risk patients in care management programs

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `care_plan` | Recommended care pathway with sequenced interventions | JSON object |
| `patient_profile` | Demographics, insurance, PCP, preferred language, SDoH factors | JSON object |
| `referral_orders` | Active referral orders with specialty, urgency, and clinical indication | JSON array |
| `insurance_details` | Plan type, network, prior auth requirements, benefit limitations | JSON object |
| `provider_directory` | Available specialists with availability, location, and network status | JSON array |
| `patient_preferences` | Location, time, provider gender, telehealth willingness, communication channel | JSON object |
| `barrier_history` | Known barriers (transportation, language, financial, health literacy) | JSON array |

## Methodology

### Step 1: Care Pathway Mapping
- Construct the complete care pathway from current state to care plan completion:
  - Identify all required appointments, tests, procedures, and interventions
  - Determine clinical sequencing requirements (what must happen before what)
  - Map dependencies: test results needed before specialist visits, clearances before procedures
  - Identify time-sensitive steps (urgent referrals, surgical windows, treatment protocols)
- Create a visual care pathway timeline with milestones and decision points
- Flag pathway complexity level: Simple (1-3 steps), Moderate (4-7 steps), Complex (8+ steps)

### Step 2: Referral Management
- Process each referral order:
  - Verify clinical indication and supporting documentation completeness
  - Match referral to in-network specialists based on:
    - Network status (in-network strongly preferred to minimize patient cost)
    - Geographic proximity to patient (apply access standards from Penchansky-Thomas model)
    - Availability (next available appointment meeting urgency timeline)
    - Patient preferences (provider gender, language, telehealth option)
  - Track referral status through lifecycle: ordered, sent, received, scheduled, completed
- Calculate referral completion risk score:
  - High risk: Medicaid, behavioral health referrals, distance above 30 minutes, prior no-show history
  - Apply proactive outreach for high-risk referrals

### Step 3: Prior Authorization Navigation
- Identify prior authorization requirements for each care plan element:
  - Query payer-specific PA requirements by CPT/HCPCS code and diagnosis
  - Determine PA submission method (electronic, fax, phone) and typical turnaround time
  - Identify clinical documentation requirements for PA approval
- Manage PA workflow:
  - Submit PA requests with complete clinical documentation
  - Track PA status: submitted, in review, approved, denied, appealed
  - Initiate peer-to-peer review for denied PAs
  - Manage PA expiration dates and renewal requirements
  - Document all PA interactions for audit trail
- Calculate PA risk: flag services with historical denial rates above 15%

### Step 4: Appointment Sequencing and Scheduling
- Optimize appointment scheduling across the care pathway:
  - Respect clinical sequencing (labs before specialist, clearance before surgery)
  - Batch appointments when possible (same day, same location) to reduce patient trips
  - Align with patient availability and preferences
  - Account for payer-specific authorization timelines in scheduling
  - Build in buffer time for PA approvals and result availability
- Generate patient-friendly appointment calendar:
  - Include: date, time, provider, location, purpose, preparation instructions
  - Highlight what to bring (insurance card, medication list, imaging CDs)
  - Include transportation and parking information
  - Provide estimated visit duration

### Step 5: Barrier Resolution
- Proactively identify and address barriers to care completion:
  - **Transportation**: Arrange Medicaid NEMT, ride-share vouchers, volunteer drivers
  - **Financial**: Financial counseling referral, charity care application, copay assistance
  - **Language**: Ensure interpreter services at all appointments
  - **Health literacy**: Provide simplified care pathway explanation and appointment reminders
  - **Childcare/eldercare**: Identify family support or community resources
  - **Work schedule**: Prioritize early morning, evening, or weekend appointments
  - **Digital access**: Offer phone-based alternatives to portal communication
- Document barrier resolutions and track effectiveness

### Step 6: Care Transition Coordination
- Manage handoffs between care settings and providers:
  - Ensure clinical summaries transfer with the patient (per CMS Care Coordination requirements)
  - Verify receiving provider has all necessary information before appointment
  - Coordinate medication reconciliation at each transition
  - Schedule follow-up within appropriate timeframes post-transition
  - Provide patient with updated care plan after each transition point
- For hospital-to-home transitions, apply Project RED or BOOST protocols
- Monitor for gaps: missed appointments, incomplete tests, care plan deviations

## Output Specification

```yaml
care_navigation_plan:
  patient_id: string
  care_pathway:
    complexity: string
    total_steps: number
    estimated_duration_weeks: number
    steps:
      - step_number: number
        description: string
        type: string
        provider: string
        urgency: string
        dependencies: array
        prior_auth_required: boolean
        prior_auth_status: string
        appointment:
          date: date
          time: string
          location: string
          preparation: string
        status: string
  referral_tracker:
    - referral_id: string
      specialty: string
      status: string
      completion_risk: string
      days_since_order: number
  prior_auth_tracker:
    - service: string
      payer: string
      status: string
      expiration_date: date
      denial_appeal_status: string
  barrier_resolutions:
    - barrier: string
      resolution: string
      status: string
      resource_linked: string
  patient_calendar:
    - date: date
      appointments: array
  next_actions:
    - action: string
      responsible: string
      due_date: date
      priority: string
```

## Analysis Framework

Apply the **Patient Navigation Continuum Model**:
1. **Assess**: Identify patient needs, barriers, preferences, and clinical pathway
2. **Plan**: Map pathway, sequence appointments, identify PA requirements
3. **Coordinate**: Schedule, authorize, arrange logistics, resolve barriers
4. **Monitor**: Track completion, identify delays, intervene proactively
5. **Transition**: Ensure smooth handoffs with complete information transfer
6. **Evaluate**: Measure pathway completion rate, time-to-treatment, patient satisfaction

## Examples

**Example: Newly Diagnosed Breast Cancer Navigation**
- Pathway: 12 steps from diagnostic biopsy through treatment initiation
- Referrals: Surgical oncology (3-day TNAA), medical oncology (5-day), radiation oncology (7-day), genetic counseling
- Prior authorizations: PET/CT (approved, 2 days), port placement (approved, 1 day), chemotherapy (submitted)
- Batched appointments: Surgical and medical oncology same day at cancer center
- Barriers resolved: Transportation arranged via ACS Road to Recovery, interpreter for Spanish-speaking patient, FMLA paperwork assistance
- Time from diagnosis to treatment initiation: 18 days (benchmark: 21 days)
- Referral completion rate: 100% (vs. 72% system average without navigation)

## Guidelines

- **HIPAA Compliance**: Care navigation involves sharing PHI across providers and must comply with HIPAA minimum necessary standards. Obtain patient authorization for communication with non-covered entities (community organizations, employers). Ensure all navigation documentation is part of the medical record.
- **Scope of Practice**: Care navigators facilitate, not diagnose or prescribe. Navigation recommendations must be based on existing provider orders and care plans. Escalate clinical questions to appropriate providers.
- **Patient Autonomy**: Present options, do not mandate. Respect patient decisions even when they deviate from recommended care pathways. Document patient-directed modifications to care plans.
- **Equity**: Monitor navigation outcomes by demographics. Ensure navigation resources are allocated based on need, not ability to self-navigate. Prioritize patients with highest barrier burden.
- **Timeliness**: Apply evidence-based time-to-treatment benchmarks. Cancer care should follow Commission on Cancer timeliness standards. Chronic disease follow-up should meet HEDIS timeframes.

## Validation Checklist

- [ ] Complete care pathway mapped with clinical sequencing
- [ ] All referrals processed with in-network, accessible providers
- [ ] Prior authorization requirements identified and tracked
- [ ] Appointments sequenced and optimized for patient convenience
- [ ] Patient barriers identified with specific resolutions
- [ ] Transportation, financial, and language needs addressed
- [ ] Care transition protocols applied at each handoff point
- [ ] Patient-friendly calendar and instructions generated
- [ ] Navigation outcomes tracked (completion rate, time-to-treatment)
- [ ] HIPAA compliance maintained across all coordination activities
- [ ] Patient preferences documented and respected
- [ ] Escalation protocol defined for clinical questions
