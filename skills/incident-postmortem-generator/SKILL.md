---
name: incident-postmortem-generator
description: Generate incident postmortem reviews for financial institution operational events. Use when conducting root cause analysis, documenting operational incidents, preparing lessons-learned reports, assessing control failures, or creating management and board-ready incident reviews aligned with OCC Heightened Standards, FFIEC guidance, and the Three Lines of Defense model.

metadata:
  display_name: "Incident Postmortem Generator"
  short_description: "Generate bank operational incident postmortem reviews"
  default_prompt: "Generate incident postmortem for my case with clear next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Incident Postmortem Generator

## Overview

Generate comprehensive incident postmortem reviews that document the timeline, root cause, control failures, customer and financial impact, and corrective actions for operational incidents in financial institutions. This skill applies OCC Heightened Standards (12 CFR 30 Appendix D), FFIEC IT Examination Handbook, COSO Internal Control Framework, and the Three Lines of Defense model to ensure postmortems meet regulatory expectations and drive meaningful risk reduction.

## When to Use

- Conducting root cause analysis following operational incidents
- Documenting cybersecurity incidents for regulatory reporting and internal governance
- Preparing lessons-learned reviews following system outages, processing failures, or data breaches
- Generating board or committee-ready incident reports
- Analyzing control failures to identify systemic governance weaknesses
- Supporting regulatory notification and communication following reportable incidents

## Required Inputs

- **Incident details**: Description, detection method, timeline of events, affected systems and services
- **Impact assessment**: Customer impact (number, type, harm), financial impact, regulatory implications
- **Response actions**: Containment, recovery steps, communication actions taken
- **Root cause data**: Investigation findings, technical analysis, contributing factors
- **Control environment**: Relevant controls that should have prevented or detected the incident
- **Organizational context**: Business unit, technology stack, regulatory profile, prior similar incidents

## Methodology

### Step 1: Incident Classification and Scoping

Classify the incident using a severity matrix:

| Severity | Criteria | Postmortem Requirements |
|----------|----------|----------------------|
| Critical (S1) | Systemic outage, significant customer harm, regulatory reporting required | Full postmortem with board reporting, regulatory communication |
| High (S2) | Major service degradation, moderate customer impact | Full postmortem with senior management reporting |
| Medium (S3) | Limited service impact, contained customer impact | Standard postmortem with management review |
| Low (S4) | Minor operational issue, negligible customer impact | Abbreviated postmortem or trend-tracking only |

Define incident boundaries, identify all affected services and stakeholders, determine regulatory notification requirements, and assess connections to prior incidents.

### Step 2: Timeline Reconstruction

Build a detailed, fact-based timeline covering: (1) Origination — when the condition first occurred, (2) Detection — when and how discovered, (3) Escalation — when response teams and management were engaged, (4) Containment — actions to stop spreading, (5) Recovery — restoration steps, (6) Resolution — full service restoration, (7) Post-recovery verification.

Capture key metrics: Time to Detect (TTD), Time to Escalate (TTE), Time to Contain (TTC), Time to Recover (TTR), and Total Duration. Document each timeline entry with timestamp, action/event, actor/system, and evidence source.

### Step 3: Root Cause Analysis

Apply structured root cause analysis using **5 Whys Analysis** as the primary technique — iterate "why" questioning until reaching an actionable organizational, process, or technology root cause. Supplement with **Fishbone (Ishikawa) diagrams** categorizing factors across People, Process, Technology, Environment, and Third Parties, and **Fault tree analysis** for complex multi-failure incidents.

Root cause categories: Process (inadequate procedures, missing runbooks), People (training gaps, key-person dependency), Technology (system defects, capacity limitations, configuration errors), Third party (vendor failure, service degradation), Governance (policy gaps, inadequate oversight), Change management (insufficient testing, rollback failure).

**Critical rule**: Never attribute root cause solely to "human error." Identify the systemic conditions that made the error possible (poor interface design, inadequate training, excessive workload, missing automation).

### Step 4: Control Failure Analysis

Assess which controls should have prevented or detected the incident, mapped to COSO principles:

- **Preventive controls**: Which controls should have prevented the incident? Why did they fail?
- **Detective controls**: Which controls should have detected the incident earlier?
- **Corrective controls**: How effective were response and recovery controls?

Map each failure to COSO components: Control Environment (Principles 1-5), Risk Assessment (Principles 6-9), Control Activities (Principles 10-12), Information and Communication (Principles 13-15), and Monitoring (Principles 16-17).

### Step 5: Impact Assessment

Quantify full impact across: **Customer** (number affected, nature of harm, complaints, remediation provided), **Financial** (direct costs, indirect costs, customer remediation, potential penalties), **Regulatory** (reporting obligations triggered, examination implications, supervisory rating impact), **Reputational** (media coverage, social media, customer sentiment), **Operational** (processing backlogs, manual workarounds, downstream effects).

### Step 6: Corrective Action Development

For each root cause and contributing factor, define: action description (specific enough for independent verification), action type (Preventive/Detective/Corrective), named owner, target date with interim milestones, success criteria, and priority (Critical=immediate, High=30 days, Medium=90 days, Low=180 days).

Actions must address root causes not symptoms. Prefer systemic fixes (automation, architecture) over procedural fixes. Include validation testing and track to closure with effectiveness validation 90 days post-implementation.

### Step 7: Lessons Learned and Pattern Analysis

Compare to prior incidents for recurring themes. Identify systemic weaknesses spanning multiple incidents. Assess whether prior corrective actions prevented recurrence. Determine if the incident reveals previously unidentified risks. Recommend enterprise-level improvements beyond the specific incident. Update risk and control assessments to reflect the experience.

## Output Specification

```markdown
# Incident Postmortem Report

## Incident Overview
| Field | Detail |
|-------|--------|
| Incident ID / Severity / Dates / Duration / Affected Services / Customers / Manager | [details] |

## Executive Summary
[2-3 paragraphs: what happened, why, impact, key corrective actions]

## Timeline
| Time | Event | Actor/System | Evidence |

## Detection and Response Metrics
| Metric | Value | Target | Assessment |

## Root Cause Analysis
[Primary root cause with 5 Whys; contributing factors]

## Control Failure Analysis
| Control | Expected Function | Failure Mode | COSO Principle |

## Impact Assessment
[Customer, financial, regulatory, reputational impacts quantified]

## Corrective Actions
| ID | Action | Type | Owner | Priority | Target Date | Status |

## Lessons Learned
[Systemic insights, pattern analysis, enterprise recommendations]
```

## Analysis Framework

| Indicator | Strong Practice | Weak Practice |
|-----------|----------------|---------------|
| Root cause depth | Systemic root causes identified | Stops at proximate cause or "human error" |
| Action quality | Specific, measurable, addresses root cause | Vague, procedural band-aids |
| Timeliness | Postmortem completed within 5-10 business days | Months of delay, findings stale |
| Follow-through | Actions tracked with effectiveness validation | Actions closed without verification |
| Pattern recognition | Connected to prior incidents and risk themes | Treated as isolated event |

## Examples

**Example 1 — System Outage Postmortem**:
"On 2025-11-15 at 14:23 EST, the consumer online banking platform experienced a complete outage lasting 4 hours 37 minutes, affecting 340,000 active users. Root cause: a database schema migration deployed during peak hours exceeded connection pool capacity, causing cascading failures. Contributing factors: (1) no peak-hour deployment restrictions for Tier 1 systems, (2) monitoring alerts set at 30-minute thresholds delaying detection by 22 minutes, (3) untested rollback procedures. Corrective actions: (1) Implement deployment freeze windows [Critical, 15-day], (2) Reduce alert thresholds to 5 minutes [High, 30-day], (3) Require validated rollback procedures for all database migrations [High, 45-day]."

**Example 2 — Control Failure Analysis**:
"The unauthorized wire transfer incident exposed failures in three control layers: (1) Preventive — dual-authorization for wires >$100K bypassed due to configuration error (COSO Principle 11), (2) Detective — daily reconciliation excluded same-day wires creating a blind spot (COSO Principle 16), (3) Corrective — team unable to initiate wire recall within the 30-minute SWIFT window due to unclear escalation procedures (COSO Principle 15). Common root cause: change management testing did not include regression testing of existing controls."

## Guidelines

- Maintain a blameless culture; focus on systemic causes, not individual fault
- Ensure the postmortem is fact-based and evidence-supported
- Engage all relevant stakeholders: technology, operations, risk, compliance, legal
- Calibrate postmortem depth to incident severity
- Connect incidents to the broader risk landscape; isolated treatment misses systemic patterns
- Regulatory-reportable incidents require legal review before finalizing
- Complete postmortems within 10 business days of resolution for S1/S2 incidents

## Validation Checklist

- [ ] Incident classified using defined severity criteria
- [ ] Complete timeline reconstructed with evidence sources
- [ ] Root cause analysis reaches systemic causes beyond proximate triggers
- [ ] Control failure analysis maps to specific COSO principles
- [ ] Customer, financial, regulatory, and reputational impacts quantified
- [ ] Corrective actions are specific, owned, time-bound, and address root causes
- [ ] Pattern analysis conducted against prior incidents
- [ ] Report reviewed by risk management and legal (for S1/S2 incidents)
- [ ] Actions entered into centralized tracking system
