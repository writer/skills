---
name: Patient Journey Mapping
description: End-to-end patient journey mapping and analysis across care episodes, identifying friction points, emotional states, and optimization opportunities using CAHPS-aligned touchpoint evaluation.

metadata:
  display_name: "Patient Journey Mapping"
  short_description: "Map end-to-end patient journeys and identify friction points"
  default_prompt: "Map my patient journey and show key friction points and improvements"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Patient Journey Mapping

## Overview

This skill constructs comprehensive patient journey maps spanning the full care continuum from pre-visit awareness through post-discharge follow-up. It applies human-centered design principles combined with CAHPS (Consumer Assessment of Healthcare Providers and Systems) survey domains to evaluate each touchpoint for accessibility, communication quality, care coordination, and emotional impact. The output is a structured journey model that identifies systemic friction, moments of truth, and actionable improvement opportunities.

## When to Use

- Designing or redesigning a clinical service line or care pathway
- Investigating root causes behind low CAHPS or Press Ganey scores
- Preparing for CMS Star Rating improvement initiatives
- Evaluating patient experience across transitions of care (ED to inpatient to post-acute)
- Supporting patient-centered medical home (PCMH) certification efforts
- Onboarding new service lines and anticipating experience gaps

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `care_episode_type` | Type of care episode (surgical, chronic management, ED visit) | String |
| `patient_personas` | Representative patient demographics, health literacy, insurance types | JSON array |
| `touchpoint_inventory` | List of known interaction points (scheduling, check-in, consult) | JSON array |
| `cahps_scores` | Historical CAHPS domain scores if available | JSON object |
| `complaint_themes` | Aggregated patient complaint categories | JSON array |
| `operational_data` | Wait times, cycle times, handoff counts per stage | JSON object |

## Methodology

### Step 1: Define Journey Scope and Patient Personas
- Establish journey boundaries (first contact through 30-day post-discharge or ongoing management)
- Build 3-5 representative patient personas incorporating:
  - Health literacy level (per REALM-SF or NVS screening classification)
  - Insurance type and prior authorization burden
  - Social determinants (transportation, language, digital access)
  - Condition complexity and comorbidity burden

### Step 2: Map Touchpoint Inventory
- Enumerate every patient-facing interaction across the episode:
  - **Pre-visit**: Awareness, appointment scheduling, pre-registration, insurance verification
  - **Arrival**: Wayfinding, check-in, identity verification, intake forms
  - **Clinical encounter**: Rooming, nursing assessment, provider consultation, shared decision-making
  - **Ancillary services**: Lab, imaging, pharmacy, referral coordination
  - **Discharge/transition**: Discharge education, medication reconciliation, follow-up scheduling
  - **Post-visit**: Portal communication, billing, care plan adherence, readmission prevention
- Tag each touchpoint with responsible department, channel (in-person, phone, digital), and average duration

### Step 3: Evaluate Each Touchpoint Against CAHPS Domains
- Score each touchpoint across applicable CAHPS composite domains:
  - **Communication with Providers** (clarity, listening, respect)
  - **Responsiveness of Staff** (timeliness of help, call button response)
  - **Communication about Medicines** (side effects explained, purpose communicated)
  - **Discharge Information** (self-care instructions, symptom watch)
  - **Care Coordination** (transitions, handoffs, information continuity)
  - **Overall Rating** (global satisfaction indicator)
- Use a 1-5 severity scale for each domain at each touchpoint

### Step 4: Emotional Journey Overlay
- Map patient emotional states at each touchpoint using a valence scale:
  - **Positive**: Confident, informed, cared-for, relieved
  - **Neutral**: Waiting, processing, uncertain
  - **Negative**: Anxious, confused, frustrated, fearful, abandoned
- Identify moments of truth: high-stakes interactions where experience shifts dramatically

### Step 5: Friction and Failure Mode Analysis
- Identify systemic friction points:
  - Information asymmetry (patient does not know what to expect next)
  - Redundant data collection (repeating history, re-signing forms)
  - Handoff failures (no warm handoff, context loss between providers)
  - Access barriers (scheduling lag, transportation, language)
  - Wait time outliers (greater than 2 standard deviations from mean at any stage)
- Classify each friction point by severity (low/medium/high/critical) and frequency

### Step 6: Generate Improvement Recommendations
- Prioritize improvements using an impact-effort matrix
- Map recommendations to CMS quality program alignment (Star Ratings, MIPS, VBP)
- Include quick wins (under 30 days), medium-term projects (1-3 months), and strategic initiatives (3-12 months)

## Output Specification

```yaml
journey_map:
  episode_type: string
  personas: array
  stages:
    - stage_name: string
      touchpoints:
        - name: string
          channel: string
          responsible_dept: string
          avg_duration_min: number
          cahps_scores:
            communication: number
            responsiveness: number
            coordination: number
          emotional_valence: string
          friction_points:
            - description: string
              severity: string
              frequency: string
          improvement_opportunities:
            - recommendation: string
              impact: string
              effort: string
              timeline: string
              cms_alignment: string
  moments_of_truth: array
  overall_experience_score: number
  priority_actions: array
```

## Analysis Framework

Apply the **Service Blueprint + CAHPS Hybrid Model**:
1. **Frontstage actions**: What the patient sees and experiences directly
2. **Backstage actions**: Staff processes invisible to the patient that impact experience
3. **Support processes**: Systems, policies, and technology enabling the interaction
4. **CAHPS overlay**: Quantitative domain scoring at each layer
5. **Equity lens**: Differential experience analysis across demographics, insurance types, and SDoH factors

## Examples

**Example 1: Total Joint Replacement Journey**
- Pre-surgical education class: CAHPS Communication score 4.2
- Day-of-surgery check-in wait: 47 min avg, Emotional valence: Anxious, Friction: HIGH
- Post-op nursing responsiveness score: 3.1, Below CMS benchmark, Priority action flagged
- Discharge instruction comprehension: 62% at adequate literacy level, Health literacy adaptation needed
- 30-day follow-up scheduling: 23% completed at discharge, Care coordination gap: CRITICAL

**Example 2: Chronic Disease Management (Diabetes)**
- New patient onboarding: 3 touchpoints before first clinical visit, Friction: redundant intake forms
- Lab result communication: 4.8-day average turnaround to patient, Below patient expectation
- Annual wellness visit: CAHPS overall rating 4.5, Moment of truth: shared decision-making on insulin

## Guidelines

- **HIPAA Compliance**: Journey maps must use de-identified, aggregate data only. Never include individual patient identifiers, MRN, or PHI in journey artifacts. All persona data must be synthetic or properly de-identified per Safe Harbor or Expert Determination methods.
- **Equity Considerations**: Always analyze journey variations across race, ethnicity, language, insurance status, and disability. Flag disparities exceeding 10% as requiring investigation.
- **Data Governance**: CAHPS data used in mapping must comply with CMS data use agreements. Press Ganey or proprietary survey data must respect vendor licensing terms.
- **Validation**: Journey maps should be validated with patient advisory councils or focus groups before finalizing improvement recommendations.
- **Update Cadence**: Refresh journey maps quarterly or after significant operational changes.

## Validation Checklist

- [ ] Journey scope clearly defined with start/end boundaries
- [ ] Minimum 3 patient personas representing diverse demographics
- [ ] All touchpoints enumerated with responsible department and channel
- [ ] CAHPS domain scores applied to each relevant touchpoint
- [ ] Emotional journey overlay completed with moments of truth identified
- [ ] Friction points classified by severity and frequency
- [ ] Improvement recommendations prioritized with impact-effort scoring
- [ ] HIPAA compliance verified: no PHI in output artifacts
- [ ] Equity analysis completed across key demographic dimensions
- [ ] Recommendations mapped to CMS quality program metrics
- [ ] Stakeholder validation plan documented
