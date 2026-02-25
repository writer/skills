---
name: care-pathway-summarization
description: Summarize patient care journeys across encounters into concise clinical pathway narratives with key milestones, transitions, and outcome tracking. Use when reviewing longitudinal patient records, preparing care coordination summaries, generating transition-of-care documents, or analyzing patient journeys across multiple providers and settings.

metadata:
  display_name: "Care Pathway Summarization"
  short_description: "Summarize patient care journeys across clinical encounters"
  default_prompt: "Summarize my care pathway with key findings and next steps"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Care Pathway Summarization

## Overview

Synthesize longitudinal patient records spanning multiple encounters, providers, and care settings into concise, clinically actionable pathway summaries. This skill traces the patient journey from initial presentation through diagnosis, treatment, and outcomes — highlighting key decision points, care transitions, complications, and adherence to evidence-based protocols.

## When to Use

- Preparing transition-of-care or handoff summaries
- Reviewing patient journeys for care coordination meetings
- Generating case summaries for utilization review or peer review
- Analyzing treatment trajectories for quality improvement
- Building patient timeline visualizations for clinical dashboards
- Supporting continuity of care across provider changes

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Patient encounter history | Chronological list of encounters with notes | Array of encounter objects |
| Problem list | Active and resolved conditions | ICD-10 coded list |
| Medication history | Current and historical medications | RxNorm-coded list with dates |
| Care setting context | Primary care, specialty, hospital, post-acute | Enum string |
| Summary purpose | Handoff, UR, quality review, patient-facing | Enum string |

## Methodology

### Step 1: Temporal Encounter Mapping

1. Order all encounters chronologically
2. Classify each encounter by type: ambulatory, inpatient, ED, observation, post-acute, telehealth
3. Identify care episodes by grouping related encounters (e.g., surgery then post-op visits then rehab)
4. Map care transitions: setting changes, provider handoffs, level-of-care changes

### Step 2: Clinical Thread Extraction

For each active problem, trace its thread through the encounter history:

- **Onset/Presentation**: When and how the condition first appeared
- **Diagnostic workup**: Tests ordered, results, differential narrowing
- **Treatment initiation**: First-line therapy, rationale, response
- **Treatment modifications**: Escalations, switches, adverse reactions
- **Current status**: Stable, improving, worsening, resolved

### Step 3: Key Milestone Identification

Extract significant clinical events:

Milestone Categories:
- Diagnosis confirmed (with supporting evidence)
- Major procedure or intervention
- Hospitalization (admission and discharge)
- Medication change (new, discontinued, dose adjustment)
- Adverse event or complication
- Care setting transition
- Specialist referral and outcome
- Goals-of-care discussion
- Disease progression or remission marker

### Step 4: Pathway Quality Assessment

Evaluate the care pathway against applicable standards:

- **Guideline adherence**: Were evidence-based protocols followed?
- **Timeliness**: Were interventions delivered within recommended timeframes?
- **Care gaps**: Were recommended screenings, tests, or follow-ups missed?
- **Coordination quality**: Were transitions smooth with appropriate information transfer?

### Step 5: Summary Generation

Produce a structured summary tailored to the stated purpose:

- **Clinical handoff**: Focus on active problems, pending items, anticipated needs
- **Utilization review**: Emphasize medical necessity, level-of-care appropriateness
- **Quality review**: Highlight guideline adherence, outcomes, variance analysis
- **Patient-facing**: Plain language, key dates, action items, medication list

## Output Specification

The structured output includes:

**patient_identifier**: MRN or de-identified ID

**summary_period**: start date and end date

**encounter_timeline**: total_encounters, by_type (inpatient, outpatient, ed, telehealth), care_episodes (episode_id, primary_condition with description and icd10, encounters with date/type/provider/setting/key_actions, status as active/resolved/ongoing)

**clinical_threads**: condition (description, icd10), onset_date, thread_summary narrative, milestones (date, event, significance, details), current_status, current_treatment

**key_milestones**: date, event description, category, clinical_significance (high/medium/low)

**active_problems**: condition (description, icd10), since date, current_management, pending_actions

**medications**: current (name, dose, indication, start_date), recently_changed (name, change, date, reason)

**care_quality**: guideline_adherence (guideline, status, details), care_gaps (gap, recommendation, priority), transition_quality (score 0-100, issues)

**summary_narrative**: concise prose summary

**pending_items**: item, owner, due_date, priority

## Analysis Framework

### Care Episode Classification

| Episode Type | Definition | Typical Duration |
|-------------|------------|-----------------|
| Acute | Single illness or injury event | Days to weeks |
| Chronic management | Ongoing condition monitoring | Months to years |
| Surgical | Pre-op through post-op recovery | Weeks to months |
| Preventive | Screening and wellness | Annual or per-guideline |
| Palliative/Hospice | Comfort-focused care | Variable |

### Transition Quality Scoring

Evaluate each care transition on:

1. **Information transfer** (0-25): Was a complete summary transmitted?
2. **Medication reconciliation** (0-25): Were medications reconciled at transition?
3. **Follow-up plan** (0-25): Were follow-up appointments scheduled?
4. **Patient understanding** (0-25): Was teach-back or patient education documented?

## Examples

**Input**: 12 encounters over 6 months for a patient with new-onset heart failure.

**Summary Output (abbreviated)**:
- Episode: Heart failure diagnosis and management (Oct 2025 to Mar 2026)
- Milestones: ED visit with dyspnea (Oct 5) > Echo showing EF 30% (Oct 6) > Cardiology consult (Oct 8) > Started on sacubitril/valsartan + carvedilol (Oct 10) > 30-day follow-up showing improvement (Nov 8) > Repeat echo EF 38% (Jan 2026) > ICD evaluation (Feb 2026)
- Guideline adherence: ACC/AHA HFrEF pathway — GDMT initiated appropriately, ICD evaluation per guidelines
- Gap: Cardiac rehab referral not documented

## Guidelines

1. **Maintain chronological integrity** — present events in temporal order within each thread
2. **Distinguish documented facts from inferences** — clearly label any inferred connections
3. **Prioritize clinically significant events** — omit routine stable follow-ups unless they mark a change
4. **Tailor language to audience** — clinical terminology for clinicians, plain language for patients
5. **Highlight pending and unresolved items** prominently — these drive the next action

## Validation Checklist

- [ ] All encounters in the input appear in the timeline
- [ ] Clinical threads trace each active problem from onset to current status
- [ ] Milestones are ordered chronologically with accurate dates
- [ ] Medication list reflects current state with recent changes highlighted
- [ ] No encounter or clinical event is attributed to the wrong date or provider
- [ ] Summary purpose drives the appropriate level of detail and language
- [ ] Pending items are actionable with clear ownership

## HIPAA Compliance Notes

- Patient identifiers must be handled per minimum necessary standard
- When generating patient-facing summaries, exclude sensitive diagnoses per 42 CFR Part 2 (substance use) and state-specific regulations
- De-identify summaries used for quality review or analytics unless a valid authorization or permitted use applies
- Maintain audit trails for all summary generation activities involving PHI
- Apply role-based access controls — not all summary types should be accessible to all roles
