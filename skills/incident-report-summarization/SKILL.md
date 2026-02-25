---
name: incident-report-summarization
description: Summarize patient safety events and incident reports into structured, actionable summaries by extracting key facts, classifying event type and severity, identifying contributing factors, and generating preliminary recommendations. Use when processing incoming incident reports, preparing safety event reviews for committees, trending safety data, communicating event summaries to leadership, or preparing for root cause analysis.

metadata:
  display_name: "Incident Report Summarization"
  short_description: "Summarize patient safety incidents into actionable reports"
  default_prompt: "Summarize my incident report with key findings and next steps"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Incident Report Summarization

## Overview

Transform raw patient safety incident reports into structured, standardized summaries that support rapid triage, committee review, regulatory reporting, and quality improvement action. Healthcare organizations generate hundreds to thousands of incident reports annually, and the narrative-heavy format makes it difficult to identify patterns, prioritize responses, and extract actionable insights efficiently. This skill applies standardized event classification taxonomies (AHRQ Common Formats, WHO ICPS), severity scoring, and contributing factor analysis to produce summaries that accelerate safety event response while maintaining the clinical nuance needed for effective follow-up.

## When to Use

- Processing incoming patient safety event reports for triage and routing
- Preparing event summaries for Patient Safety Committee or Quality Committee review
- Classifying and categorizing events for trending and pattern analysis
- Identifying events requiring root cause analysis (RCA) or immediate investigation
- Preparing regulatory reports (state adverse event reporting, CMS, Joint Commission)
- Generating periodic safety event trend reports for leadership
- Screening events for sentinel event criteria (Joint Commission definition)
- Supporting just culture classification of event contributing factors

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `incident_report` | Original incident/occurrence report narrative and structured fields | Text and structured data |
| `patient_context` | Patient demographics, acuity, diagnoses, care setting (de-identified) | Structured object |
| `event_taxonomy` | Classification system: AHRQ Common Formats, WHO ICPS, or organizational | Reference configuration |
| `severity_framework` | Harm classification: NCC MERP (medication events) or AHRQ Harm Scale | Reference configuration |
| `reporter_info` | Reporter role, department, relationship to event | Structured object |
| `related_events` | Prior similar events for pattern identification | Array of records |
| `regulatory_criteria` | State and federal reportable event definitions | Reference configuration |

## Methodology

### Step 1: Event Narrative Extraction

Parse the incident report to extract structured facts:

**Core Event Facts:**
- **What happened**: Clear, objective description of the event
- **When**: Date, time, shift (day/evening/night)
- **Where**: Unit, department, room, care area
- **Who was involved**: Patient, staff roles (de-identified), providers, family
- **Who discovered**: How and when the event was identified
- **Patient impact**: Immediate effect on the patient (if any)
- **Immediate actions taken**: Response and mitigation steps performed
- **Current patient status**: Patient condition at time of report

**Narrative Quality Assessment:**
- Is the report factual and objective (vs. opinion-laden)?
- Are all relevant details included (5 Ws: who, what, when, where, why)?
- Are there gaps requiring follow-up investigation?
- Is the report timely (within 24 hours of event discovery)?

### Step 2: Event Classification

Classify the event using standardized taxonomy:

**AHRQ Common Formats Event Types:**

| Category | Examples | Code |
|----------|----------|------|
| Medication/fluid | Wrong drug, dose, route, time, patient; adverse drug reaction | MED |
| Procedure/surgery | Wrong site, retained foreign body, unplanned return | SURG |
| Fall | Patient fall with or without injury | FALL |
| Healthcare-associated infection | CLABSI, CAUTI, SSI, CDI | HAI |
| Pressure injury | Hospital-acquired pressure injury (stage 2+) | PI |
| Device/equipment | Malfunction, misuse, failure | DEV |
| Laboratory/blood bank | Mislabeled specimen, transfusion reaction | LAB |
| Perinatal | Neonatal injury, maternal hemorrhage | PERI |
| Diagnostic | Missed or delayed diagnosis, wrong diagnosis | DIAG |
| Patient behavior | Self-harm, elopement, violence | BEHAV |
| Other | Dietary, environment, security | OTHER |

**WHO International Classification for Patient Safety (ICPS):**
- Incident type, patient outcome, contributing factors, mitigating factors, actions taken

### Step 3: Severity Assessment

Score the severity of harm (if any) to the patient:

**NCC MERP Harm Categories (Medication Events):**

| Category | Description | Severity Level |
|----------|-------------|----------------|
| A | Circumstances with capacity to cause error | No event |
| B | Error occurred but did not reach patient | Near miss |
| C | Error reached patient, no harm | No harm |
| D | Error reached patient, monitoring required | No harm, monitoring |
| E | Error contributed to temporary harm, intervention needed | Mild harm |
| F | Error contributed to temporary harm, extended stay | Moderate harm |
| G | Error contributed to permanent harm | Severe harm |
| H | Error required life-saving intervention | Severe harm |
| I | Error contributed to patient death | Death |

**AHRQ Harm Scale (Non-Medication Events):**
- No harm (near miss or no injury)
- Mild harm (temporary, minimal intervention)
- Moderate harm (temporary, significant intervention or extended stay)
- Severe harm (permanent injury or life-threatening)
- Death

**Sentinel Event Determination:**
- Apply Joint Commission Sentinel Event definition: unexpected occurrence involving death or serious physical or psychological injury (or risk thereof)
- If sentinel event criteria are met, flag for immediate leadership notification and RCA

### Step 4: Contributing Factor Identification

Identify factors that contributed to the event:

**Factor Categories (based on James Reason's Swiss Cheese Model):**

| Level | Factor Type | Examples |
|-------|-----------|----------|
| Active failures | Human error (slip, lapse, mistake, violation) | Medication calculated incorrectly, assessment not performed |
| Task/technology | Process or equipment design | Complex order entry, ambiguous labels, alarm fatigue |
| Individual | Knowledge, skill, fatigue, health | Staff unfamiliar with protocol, fatigued after long shift |
| Team | Communication, supervision, teamwork | Handoff failure, inadequate supervision, hierarchy gradient |
| Work environment | Staffing, workload, physical environment | Short-staffed, high patient acuity, noise, interruptions |
| Organization | Culture, policies, resources | Inadequate policy, culture discouraging reporting, budget constraints |
| Patient | Acuity, behavior, communication | Non-English speaking, altered mental status, non-adherence |

**Just Culture Classification:**
- **Human error**: Inadvertent action, system-designed slip → Console the individual
- **At-risk behavior**: Conscious choice, risk not appreciated → Coach and improve awareness
- **Reckless behavior**: Conscious disregard of substantial risk → Disciplinary action

### Step 5: Regulatory Reporting Assessment

Determine if the event meets regulatory reporting thresholds:

**State Adverse Event Reporting:**
- Never events (National Quality Forum Serious Reportable Events list)
- State-specific reportable events (varies by jurisdiction — check state health department requirements)
- Typical reporting deadline: 24 hours to 5 business days depending on state

**CMS Reporting:**
- Hospital-acquired conditions not present on admission
- Events affecting Medicare/Medicaid patients meeting specific criteria

**Joint Commission Sentinel Event Reporting:**
- Voluntary self-reporting to Joint Commission
- Required to conduct RCA and submit action plan within 45 business days

**FDA Reporting:**
- Device-related events (MedWatch/MDR within 10 business days for death, 30 for serious injury)
- Medication events involving product quality issues (MedWatch)

### Step 6: Summary Generation

Produce a structured event summary:

**Executive Summary Format:**
- **Event type**: [Classification code and plain language]
- **Severity**: [Harm category with brief description]
- **Brief description**: [2-3 sentence factual summary]
- **Contributing factors**: [Top 3 identified factors]
- **Immediate actions**: [Steps already taken]
- **Regulatory reporting**: [Required/Not required with rationale]
- **Recommended follow-up**: [Investigation level: RCA, focused review, monitor, or close]
- **Similar events**: [Count and trend of related events in past 12 months]

### Step 7: Trend Analysis and Pattern Identification

When processing multiple events, identify patterns:

- **Temporal trends**: Events by month, day of week, shift
- **Location clustering**: Units or departments with elevated event rates
- **Event type trends**: Increasing or decreasing categories
- **Severity trends**: Shift in harm severity distribution
- **Contributing factor patterns**: Recurring systemic factors across events
- **Reporter patterns**: Reporting rates by unit (low reporting may indicate underreporting, not safety)

## Output Specification

```yaml
incident_summary:
  event_id: string
  report_date: string
  event_date: string
  event_type: string
  event_subtype: string
  classification_code: string
  severity:
    harm_level: string
    ncc_merp_category: string  # if medication event
    sentinel_event: boolean
  summary:
    brief_description: string
    patient_impact: string
    immediate_actions: string
  contributing_factors:
    - factor: string
      category: string
      just_culture_class: string
  regulatory_reporting:
    required: boolean
    agencies: array
    deadline: string
  recommended_followup:
    investigation_level: string  # RCA, focused review, monitor, close
    assigned_to: string
    deadline: string
  related_events:
    count_past_12_months: number
    trend_direction: string
    pattern_identified: boolean
```

## Analysis Framework

### Event Triage Matrix

| Severity | Frequency | Action Level |
|----------|-----------|-------------|
| Death or severe harm | Any | Immediate RCA, leadership notification, regulatory report |
| Moderate harm | Any | Focused investigation within 30 days |
| Mild harm | Isolated | Standard review, monitor for recurrence |
| Mild harm | Recurring (3+ similar events) | Aggregate analysis, process improvement |
| Near miss / No harm | Isolated | Standard review, close |
| Near miss / No harm | Recurring | System-level review, proactive risk reduction |

## Examples

**Example: Medication Event Summary**

- **Event type**: MED — Wrong dose administered
- **Severity**: NCC MERP Category E (temporary harm, intervention required)
- **Summary**: Patient received 10x the prescribed dose of insulin (50 units instead of 5 units) due to verbal order transcription error. Hypoglycemia detected within 30 minutes by nurse during routine blood glucose check. Treated with IV dextrose; patient recovered without residual effect.
- **Contributing factors**: (1) Verbal order used instead of computerized order entry — Task/technology, (2) No independent double-check for high-alert medication — Team/process, (3) Sound-alike confusion: "fifty" vs. "five" — Communication
- **Just culture**: Human error (slip due to verbal communication) — Console and implement systemic fix
- **Regulatory**: State reportable as serious medication error with harm. Not sentinel event.
- **Follow-up**: Focused investigation; recommend eliminating verbal orders for high-alert medications; implement mandatory independent double-check for insulin
- **Related events**: 4 insulin-related events in past 12 months — increasing trend

## Guidelines

1. **Maintain objectivity** — summaries should be factual, not judgmental or blame-assigning
2. **Preserve reporter confidentiality** — per Patient Safety Act (42 CFR Part 3) protections where applicable
3. **Focus on systems, not individuals** — contributing factor analysis should emphasize system failures
4. **Apply Just Culture principles** — distinguish human error from at-risk and reckless behavior
5. **Prioritize by severity and frequency** — resource allocation follows the triage matrix
6. **Close the loop** — every summarized event should have a defined follow-up action and timeline
7. **Report to Patient Safety Organization** — aggregate event data reported to PSO receives federal privilege protections

## Validation Checklist

- [ ] Event narrative parsed for all core facts (who, what, when, where, impact)
- [ ] Event classified using standardized taxonomy (AHRQ or WHO ICPS)
- [ ] Severity scored using appropriate harm scale (NCC MERP or AHRQ)
- [ ] Sentinel event criteria evaluated with appropriate flagging
- [ ] Contributing factors identified across multiple system levels
- [ ] Just culture classification applied to human factors
- [ ] Regulatory reporting requirements assessed against applicable thresholds
- [ ] Structured summary generated with recommended follow-up and timeline
- [ ] Related events identified for trend and pattern analysis
- [ ] Reporter confidentiality preserved in summary documentation

## HIPAA Compliance Notes

- Incident reports contain PHI including patient identifiers, diagnoses, and care details (45 CFR 164.501)
- Patient safety event analysis is a healthcare operations activity permitted under HIPAA (45 CFR 164.501)
- Summaries shared with committees should use minimum necessary PHI (45 CFR 164.502(b))
- Reports submitted to Patient Safety Organizations receive additional federal protections under the Patient Safety Act (42 CFR Part 3)
- De-identify event data used for aggregate trending and external reporting
- Maintain access controls on incident reporting systems containing PHI (45 CFR 164.312(a))
- State peer review and quality improvement privilege protections may apply — consult legal counsel
