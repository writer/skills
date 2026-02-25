---
name: root-cause-analysis-generator
description: Generate comprehensive root cause analysis (RCA) drafts for adverse events and sentinel events using the VA National Center for Patient Safety RCA methodology, including causal factor charting, five whys analysis, and corrective action development. Use when conducting RCAs for sentinel events, serious safety events, near misses with high potential for harm, or recurring incident patterns requiring systematic investigation.

metadata:
  display_name: "Root Cause Analysis Generator"
  short_description: "Generate root cause analysis drafts for safety events"
  default_prompt: "Generate root cause for my case with clear next steps"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Root Cause Analysis Generator

## Overview

Generate structured root cause analysis (RCA) drafts following the VA National Center for Patient Safety (NCPS) model — the most widely adopted RCA methodology in US healthcare. This skill guides the systematic investigation of adverse events from event timeline reconstruction through causal factor identification to strong corrective action development. Joint Commission requires RCA completion within 45 business days of a sentinel event, and this skill accelerates the process by structuring the analysis, ensuring all required elements are addressed, and generating corrective actions that meet the Joint Commission's criteria for acceptability.

## When to Use

- Conducting RCA for Joint Commission-defined sentinel events
- Investigating serious safety events resulting in moderate-to-severe patient harm
- Analyzing near-miss events with high potential severity
- Investigating recurring event patterns despite prior interventions
- Preparing RCA documentation for Joint Commission Sentinel Event review
- Supporting Patient Safety Committee review of adverse events
- Developing corrective action plans with measurable effectiveness indicators
- Training staff on RCA methodology and facilitation

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `event_summary` | Detailed event description including timeline, participants, and outcome | Text narrative |
| `patient_record` | Relevant medical record entries surrounding the event (de-identified) | Clinical documentation |
| `interviews` | Staff interview notes from involved individuals and witnesses | Text summaries |
| `policies_procedures` | Applicable organizational policies, protocols, and guidelines | Document references |
| `equipment_info` | Device or equipment data relevant to the event | Structured object |
| `environmental_data` | Staffing levels, census, physical environment conditions at time of event | Structured object |
| `prior_events` | Previous similar events and prior corrective actions | Array of records |

## Methodology

### Step 1: Event and Causal Factor Charting

Construct a detailed chronological timeline and identify causal factors:

**Timeline Construction:**
- Map every relevant event on a time-sequenced chart
- Begin with the earliest contributing event and end with the adverse outcome and discovery
- Include parallel tracks for different participants (patient, nurse, physician, pharmacy, etc.)
- Mark each decision point where an alternative action could have changed the outcome
- Identify handoff points and transitions of care
- Note time gaps or delays that may have contributed

**Causal Factor Identification:**
- At each timeline node, identify conditions that allowed the event to progress
- Distinguish between:
  - **Active causes**: Proximate actions or inactions by individuals
  - **Latent causes**: Systemic conditions that enabled the active causes
  - **Contributing conditions**: Factors that increased likelihood but did not directly cause the event

### Step 2: Root Cause Identification (Five Whys + Ishikawa)

Apply the Five Whys technique iteratively to each causal factor:

**Five Whys Process:**
1. Why did this happen? → Identify immediate cause
2. Why did that occur? → Identify underlying process failure
3. Why does that process fail? → Identify systemic gap
4. Why does that gap exist? → Identify organizational factor
5. Why hasn't it been addressed? → Identify root cause (management system, culture, resource allocation)

**Stop when you reach a factor that is:**
- Under organizational control (can be changed)
- Systemic (not dependent on individual performance)
- Actionable (a feasible intervention can address it)

**Ishikawa (Fishbone) Categories for Healthcare:**

| Category | Focus Areas |
|----------|------------|
| Human factors | Knowledge, skills, fatigue, distraction, workload, teamwork |
| Communication | Handoffs, orders, documentation, terminology, hierarchy |
| Equipment/technology | Design, maintenance, availability, user interface, alarms |
| Environment | Staffing, workspace, noise, lighting, interruptions |
| Policies/procedures | Adequacy, clarity, currency, accessibility, enforcement |
| Patient factors | Acuity, complexity, language, behavior, preferences |
| Organizational/management | Culture, resources, priorities, training investment, oversight |

### Step 3: VA NCPS Triage Questions

Apply the VA National Center for Patient Safety triage framework to validate root causes:

**For each identified root cause, answer:**

1. **Was the task that had to be performed clearly communicated?**
   - Were there ambiguities in the task assignment or instructions?
   - Was relevant information available to the person performing the task?

2. **Was there a clearly defined process/procedure for the task?**
   - Did a policy or protocol exist?
   - Was it current, evidence-based, and accessible?
   - Was it known to the staff involved?

3. **Were the right people assigned to the task?**
   - Appropriate credentials, competencies, and experience?
   - Adequate staffing levels for the workload?
   - Appropriate supervision available?

4. **Was the environment conducive to safe task performance?**
   - Physical layout, lighting, noise, interruption frequency?
   - Equipment functioning and available?
   - Workload and fatigue levels?

5. **Were there adequate barriers/safeguards in place?**
   - Independent double-checks, forcing functions, redundancies?
   - Clinical decision support, checklists, standardized processes?
   - Were barriers bypassed, and if so, why?

### Step 4: Root Cause Validation

Validate identified root causes against acceptance criteria:

**A valid root cause must be:**
- **Specific**: Clearly describes the systemic failure (not vague, e.g., "communication failure" must specify what communication, between whom, about what)
- **Systemic**: Addresses a system, process, or design issue (not individual performance alone)
- **Actionable**: The organization has the ability to implement a fix
- **Evidenced**: Supported by facts gathered during the investigation
- **Foundational**: Removal of this cause would prevent or significantly reduce recurrence

**Root Cause Quality Test:**
- If this root cause were eliminated, would the event still have occurred? (If yes, continue analysis)
- Is this root cause under organizational control? (If no, it is a contributing factor, not a root cause)
- Can we develop a feasible corrective action for this root cause? (If no, reframe)

### Step 5: Corrective Action Development

Develop strong corrective actions for each root cause:

**Action Strength Hierarchy (strongest to weakest):**

| Strength | Action Type | Examples | Sustainability |
|----------|------------|---------|----------------|
| Strong | Architectural/physical change | Forcing functions, equipment redesign, eliminating look-alike packaging | High — does not depend on human behavior |
| Strong | Standardize/simplify | Checklists, standard order sets, simplified processes | High — reduces complexity |
| Strong | Tangible involvement of leadership | Executive safety rounds, resource allocation decisions | High — signals organizational priority |
| Intermediate | Increase staffing/redesign workflow | Dedicated safety personnel, workload redistribution | Moderate — requires sustained investment |
| Intermediate | Software/technology enhancement | CDS alerts, barcode scanning, smart pumps | Moderate — requires maintenance |
| Intermediate | Redundancy/independent checks | Double-check processes, read-back verification | Moderate — requires compliance |
| Weak | Education/training | In-service training, competency validation | Low — knowledge decays without reinforcement |
| Weak | New policy/procedure | Written policy without enforcement mechanism | Low — awareness and adherence decline |
| Weak | Increased awareness/vigilance | Posters, reminders, "be more careful" | Very Low — unsustainable |

**Joint Commission Corrective Action Requirements:**
- Actions must address identified root causes (not symptoms)
- Include at least one strong action for each sentinel event RCA
- Define measurable outcomes to evaluate effectiveness
- Assign responsibility and implementation timeline
- Include a plan to sustain the improvement

### Step 6: Outcome Measures and Monitoring Plan

Define how corrective action effectiveness will be measured:

**Outcome Measures:**
- **Process measure**: Is the corrective action being implemented as designed? (compliance rate)
- **Outcome measure**: Has the adverse event type been reduced or eliminated? (recurrence rate)
- **Balancing measure**: Has the corrective action created any unintended negative consequences?

**Monitoring Plan:**
- Define measurement frequency (weekly during initial implementation, then monthly)
- Establish monitoring duration (minimum 12 months for sentinel event corrective actions)
- Identify responsible person for data collection and analysis
- Define success criteria (e.g., zero recurrence for 12 months)
- Plan for reassessment if corrective action is not achieving desired results

### Step 7: RCA Report Compilation

Assemble the complete RCA document:

**Required RCA Report Sections:**
1. **Event description**: Factual summary with relevant clinical context
2. **Event timeline**: Chronological causal factor chart
3. **Investigation process**: Team members, interviews conducted, data reviewed
4. **Root cause findings**: Each root cause with supporting evidence and Five Whys chain
5. **Contributing factors**: Factors that contributed but are not root causes
6. **Corrective action plan**: Each action linked to a root cause, with owner, timeline, and measures
7. **Monitoring plan**: How effectiveness will be tracked
8. **Risk reduction assessment**: How corrective actions will reduce future risk
9. **Leadership review**: Sign-off by organizational leadership
10. **Lessons learned**: Key insights for organizational learning

## Output Specification

```yaml
rca_report:
  event_id: string
  event_date: string
  event_type: string
  severity: string
  sentinel_event: boolean
  rca_team:
    - name: string
      role: string
  investigation_summary:
    interviews_conducted: number
    documents_reviewed: number
    investigation_duration: string
  timeline:
    - timestamp: string
      event_description: string
      actor: string
      causal_factor_identified: boolean
  root_causes:
    - root_cause_id: string
      description: string
      category: string  # Ishikawa category
      five_whys_chain: array
      evidence: string
      validated: boolean
  contributing_factors: array
  corrective_actions:
    - action_id: string
      linked_root_cause: string
      description: string
      strength: string  # strong, intermediate, weak
      responsible_party: string
      implementation_date: string
      outcome_measure: string
      monitoring_plan: string
      status: string
  risk_reduction_assessment: string
  leadership_approval:
    approved_by: string
    approval_date: string
```

## Analysis Framework

### VA NCPS RCA Process Flow

| Phase | Activities | Output |
|-------|-----------|--------|
| Organize | Assemble team, secure records, plan investigation | Investigation charter |
| Investigate | Timeline, interviews, document review, site visit | Causal factor chart |
| Analyze | Five Whys, triage questions, root cause validation | Validated root causes |
| Act | Develop corrective actions, assign ownership | Action plan |
| Measure | Monitor effectiveness, report outcomes | Outcome data |
| Sustain | Reassess, adjust, embed in operations | Sustained improvement |

## Examples

**Example: Wrong-Site Surgery RCA**

- Event: Left knee arthroscopy performed when right knee was indicated
- Severity: Sentinel event (wrong-site surgery)
- Timeline: Pre-op verification completed but laterality discrepancy not detected; surgical time-out performed but site marking not visible under draping
- Root causes identified:
  1. Pre-operative verification process did not include independent cross-check of imaging with consent and OR schedule (Process gap — no redundancy)
  2. Site marking was performed but not visible after draping, and time-out protocol did not require visualization of mark (Policy gap — incomplete protocol)
  3. OR schedule displayed abbreviated laterality ("L knee") that was ambiguous in context (System design — ambiguous information display)
- Corrective actions:
  1. (Strong) Implement hard-stop in OR system requiring imaging laterality confirmation before case can proceed
  2. (Strong) Revise draping protocol to ensure site mark remains visible; add marking verification to time-out checklist
  3. (Intermediate) Standardize OR schedule laterality display to full text with redundant notation
- Monitoring: Zero wrong-site events for 12 months; monthly time-out compliance audits

## Guidelines

1. **Focus on systems, not blame** — RCA is a systems improvement methodology, not a disciplinary tool
2. **Include at least one strong corrective action** — Joint Commission will not accept RCAs with only weak actions
3. **Complete within 45 business days** — Joint Commission timeline for sentinel event RCA
4. **Involve front-line staff** — those closest to the work provide the most accurate insights
5. **Validate root causes rigorously** — a poorly identified root cause leads to ineffective corrective actions
6. **Avoid "education only" as a sole corrective action** — training alone does not prevent recurrence
7. **Measure effectiveness** — a corrective action without outcome measurement is incomplete

## Validation Checklist

- [ ] Detailed event timeline with causal factor chart completed
- [ ] Five Whys analysis applied to each causal factor to appropriate depth
- [ ] VA NCPS triage questions answered for each potential root cause
- [ ] Root causes validated as specific, systemic, actionable, evidenced, and foundational
- [ ] At least one strong corrective action included per Joint Commission requirements
- [ ] Each corrective action linked to a specific root cause
- [ ] Outcome measures defined with monitoring plan and success criteria
- [ ] Contributing factors documented separately from root causes
- [ ] RCA report reviewed and approved by organizational leadership
- [ ] Lessons learned documented for organizational sharing
- [ ] Completion timeline meets Joint Commission 45 business day requirement

## HIPAA Compliance Notes

- RCA investigation requires access to detailed PHI in medical records (45 CFR 164.501)
- RCA activities constitute quality improvement/healthcare operations under HIPAA (45 CFR 164.501)
- RCA documents containing PHI must be secured with access controls (45 CFR 164.312(a))
- Consider reporting to a Patient Safety Organization for federal privilege protections under the Patient Safety Act (42 CFR Part 3)
- De-identify RCA findings before sharing for organizational learning beyond the investigation team
- State peer review and quality improvement protections may apply to RCA documents — consult legal counsel
- Staff interviews during RCA should be conducted with awareness of confidentiality protections and limits
