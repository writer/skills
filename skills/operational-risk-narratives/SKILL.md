---
name: operational-risk-narratives
description: Analyze operational risk events and produce structured loss event narratives, root cause analyses, and OpRisk reports. Use when documenting operational loss events, conducting RCSA analysis, preparing OpRisk committee reports, or supporting Basel III operational risk capital calculations under the standardized measurement approach.

metadata:
  display_name: "Operational Risk Narratives"
  short_description: "Write operational risk event loss narratives for banks"
  default_prompt: "Summarize my operational risk with key findings and next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Operational Risk Narratives

## Overview

This skill produces structured operational risk event narratives and analyses for financial institutions. It covers loss event documentation, root cause analysis (RCA), risk and control self-assessments (RCSA), key risk indicator (KRI) analysis, scenario analysis, and operational risk capital estimation. Output aligns with Basel III/IV operational risk framework, OCC Heightened Standards, and industry taxonomies (ORX, Basel event types).

## When to Use

- Documenting operational loss events for the internal loss database
- Conducting root cause analysis for material loss events
- Drafting operational risk committee reports and board summaries
- Analyzing KRI breaches and trend deterioration
- Performing RCSA facilitation and documentation
- Supporting Basel III standardized measurement approach (SMA) calculations
- Preparing operational risk scenario analysis narratives for stress testing

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Event details | What happened, when, where, who was involved | Incident report |
| Financial impact | Gross loss, recoveries, near-miss estimate | Dollar amounts |
| Basel event type | Level 1 and Level 2 event classification | Basel taxonomy |
| Business line | Affected business unit per Basel classification | Business line mapping |
| Control environment | Controls that failed or were absent | Control inventory |
| Timeline | Event occurrence, detection, escalation, resolution | Chronological dates |
| Prior events | Related historical events or trends | Loss database query |

## Methodology

### Step 1: Classify the Event

Apply the Basel II/III operational risk event type taxonomy:

| Level 1 Category | Level 2 Examples | Typical Drivers |
|-------------------|-----------------|-----------------|
| **Internal fraud** | Unauthorized activity, theft | Insider threat, control bypass |
| **External fraud** | Theft/robbery, systems security, forgery | Cyber attack, social engineering |
| **Employment practices** | Discrimination, workers comp, labor disputes | HR policy gaps, culture issues |
| **Clients, products, suitability** | Fiduciary breaches, mis-selling, disclosure | Compliance failures, training gaps |
| **Damage to physical assets** | Natural disasters, terrorism, vandalism | BCP gaps, physical security |
| **Business disruption** | Systems failures, utility outages, telecom | IT resilience, vendor dependency |
| **Execution, delivery, process management** | Data entry errors, accounting errors, failed settlement | Process design, human error |

Also classify by:
- **Business line**: Corporate finance, trading, retail banking, commercial banking, payment and settlement, agency services, asset management, retail brokerage
- **Boundary event**: Credit-risk-related operational events, market-risk-related operational events

### Step 2: Document the Event Narrative

Construct a comprehensive, fact-based narrative:

**Event description** (what happened):
- Precise description of the event without editorializing
- Specific actions or failures that occurred
- Systems, processes, and people involved

**Detection** (how it was found):
- How and when the event was detected
- Time lag between occurrence and detection (detection gap)
- Detection mechanism (automated alert, employee report, customer complaint, audit finding, regulatory examination)

**Impact** (what was the result):
- Direct financial loss (gross amount before recoveries)
- Indirect costs (remediation, legal, regulatory fines, reputational)
- Customer impact (number of customers affected, complaint volume)
- Regulatory impact (enforcement action, MRA/MRIA, consent order)

**Resolution** (what was done):
- Immediate containment actions
- Customer remediation steps
- Process or control changes implemented
- Timeline to full resolution

### Step 3: Perform Root Cause Analysis

Apply structured RCA methodology:

**Five Whys Analysis**:
1. Why did the event occur? → [Proximate cause]
2. Why did the proximate cause exist? → [Contributing factor]
3. Why was that factor present? → [Process weakness]
4. Why wasn't the weakness addressed? → [Governance gap]
5. Why did governance fail? → [Root cause]

**Root Cause Categories**:
| Category | Sub-Categories |
|----------|---------------|
| **People** | Training, competency, staffing, misconduct, culture |
| **Process** | Design gaps, procedure non-compliance, handoff failures |
| **Systems** | IT failure, data quality, system capacity, cyber vulnerability |
| **External** | Vendor failure, regulatory change, fraud, natural disaster |
| **Governance** | Oversight gaps, policy deficiency, risk appetite misalignment |

### Step 4: Assess Control Failures

Evaluate the control environment that should have prevented or detected the event:

| Control | Type | Design | Operating Effectiveness | Failure Mode |
|---------|------|--------|------------------------|-------------|
| [Control 1] | Preventive/Detective | Adequate/Inadequate | Effective/Ineffective | [How it failed] |
| [Control 2] | Preventive/Detective | Adequate/Inadequate | Effective/Ineffective | [How it failed] |

Distinguish between:
- **Control design failure**: The control was not designed to address this risk
- **Control operating failure**: The control was properly designed but not executed correctly
- **Control absence**: No control existed for this risk scenario

### Step 5: Quantify Financial Impact

Calculate the full financial impact:

| Component | Amount | Status |
|-----------|--------|--------|
| Gross loss (direct) | [$X] | Actual / Estimated |
| Legal and regulatory costs | [$X] | Actual / Estimated |
| Remediation costs | [$X] | Actual / Estimated |
| **Total gross loss** | **[$X]** | |
| Insurance recovery | -[$X] | Received / Expected |
| Other recoveries | -[$X] | Received / Expected |
| **Net loss** | **[$X]** | |

For near-miss events, estimate the potential loss had the event not been detected or contained.

### Step 6: Develop Corrective Action Plan

Define specific, measurable remediation actions:

| # | Action | Owner | Deadline | Priority | Status |
|---|--------|-------|----------|----------|--------|
| 1 | [Specific action] | [Name/Role] | [Date] | [Critical/High/Medium] | [Open/In Progress/Complete] |

Each action must:
- Address a specific root cause or control gap identified
- Be measurable (clear definition of "done")
- Have an accountable owner (individual, not committee)
- Include a realistic deadline based on complexity
- Be tracked to completion with evidence of implementation

### Step 7: Connect to Risk Framework

Link the event to the broader operational risk framework:
- Update the RCSA to reflect the event and new/modified controls
- Review and adjust KRI thresholds if the event signals calibration issues
- Assess whether scenario analysis assumptions need revision
- Evaluate impact on operational risk capital (SMA calculation under Basel IV)
- Update risk appetite and tolerance metrics if breached
- Report through governance (OpRisk committee, board risk committee)

## Output Specification

```markdown
# Operational Risk Event Report: [Event ID]

## Event Summary
- **Event ID**: [ID]
- **Event Date**: [Occurrence date]
- **Detection Date**: [When discovered]
- **Basel Event Type**: [Level 1 / Level 2]
- **Business Line**: [Basel business line]
- **Gross Loss**: [$Amount]
- **Net Loss**: [$Amount]
- **Status**: [Open / Closed]

## Narrative
[Comprehensive event description following Step 2 structure]

## Root Cause Analysis
- **Root Cause**: [Category: specific root cause]
- **Contributing Factors**: [List of contributing factors]
- **Five Whys**:
  1. [Why 1]
  2. [Why 2]
  3. [Why 3]
  4. [Why 4]
  5. [Why 5 — root cause]

## Control Assessment
[Control failure analysis per Step 4]

## Financial Impact
[Loss quantification per Step 5]

## Corrective Actions
[Action plan per Step 6]

## Lessons Learned
[Institutional takeaways applicable beyond this specific event]

## Risk Framework Updates
[RCSA, KRI, scenario analysis, and capital implications]
```

## Analysis Framework

### KRI Breach Analysis

When a KRI breaches its threshold, produce:
- KRI metric, current value, threshold (amber and red), and trend direction
- Root cause of the breach (event-driven, systemic deterioration, data quality)
- Comparison to historical KRI performance (is this an outlier or trend?)
- Recommended management response and threshold recalibration assessment

### RCSA Facilitation

For risk and control self-assessment narratives:
- Identify inherent risk level for each operational risk category
- Assess control effectiveness (1-5 scale with evidence)
- Calculate residual risk (inherent risk adjusted for control effectiveness)
- Compare residual risk to risk appetite and identify gaps
- Document action plans for residual risk exceeding appetite

### Loss Distribution Analysis

For capital and trending purposes:
- Frequency analysis: event count by category, business line, and time period
- Severity analysis: loss distribution with mean, median, 95th, and 99th percentiles
- Trend analysis: rolling 12-month loss trends by category
- Concentration: identify categories representing disproportionate loss share

## Examples

**Example 1 — Process Failure Event**:
"Event OR-2025-0847: On 2025-09-12, a wire transfer of $3.2M was executed to an incorrect beneficiary due to a manual data entry error in the wire instruction template. The error was detected by the receiving bank within 4 hours, and $3.05M was recovered within 3 business days. Net loss of $150K reflects the unrecovered portion plus legal costs. Root cause: absence of maker-checker control for wire template modifications exceeding $1M (control gap). Contributing factors: staffing pressure due to month-end processing volume and lack of automated beneficiary validation against master file. Corrective actions: (1) Implement dual authorization for wire template changes >$500K (owner: Payments Ops Manager, due: 2025-10-31); (2) Deploy automated beneficiary name/account matching against counterparty master file (owner: IT, due: 2025-12-31)."

**Example 2 — Cyber Event**:
"Event OR-2025-1203: Business email compromise (BEC) attack targeted the CFO's email account, resulting in a fraudulent wire instruction of $890K to an overseas account. The attack exploited a phishing email that bypassed email security filters. Detection occurred 48 hours after wire execution when the CFO identified the spoofed email during routine inbox review. $0 recovered; funds moved through multiple intermediary accounts. Basel Event Type: External Fraud — Systems Security. Root cause: inadequate email authentication controls (DMARC policy set to 'none' rather than 'reject'). Corrective actions: (1) Implement DMARC reject policy (IT Security, 30 days); (2) Deploy callback verification for all wire requests >$100K (Treasury Ops, 15 days); (3) Mandatory BEC awareness training for all finance staff (HR/Compliance, 45 days)."

## Guidelines

- Document all operational loss events exceeding the institution's reporting threshold (typically $10K-$25K)
- Capture near-miss events for trend analysis even when no financial loss occurs
- Apply consistent Basel event type taxonomy; avoid creating custom categories
- Root cause analysis must go beyond proximate cause to identify systemic issues
- Corrective actions must address root causes, not symptoms
- Track corrective actions to closure with evidence that the fix is effective
- Distinguish between actual losses (realized) and provisions/reserves (estimated future)
- Include timing information: occurrence-to-detection gap is a key control effectiveness metric
- Maintain objectivity; event narratives are factual records, not blame assignments
- Aggregate related events when a single root cause produces multiple loss impacts

## Validation Checklist

- [ ] Basel event type is assigned at Level 1 and Level 2
- [ ] Business line mapping follows Basel/regulatory classification
- [ ] Event narrative covers what, when, how detected, impact, and resolution
- [ ] Root cause analysis identifies systemic cause (not just proximate trigger)
- [ ] Control assessment distinguishes design vs. operating effectiveness failures
- [ ] Financial impact includes gross loss, recoveries, and net loss
- [ ] Corrective actions are specific, owned, and time-bound
- [ ] Lessons learned are documented for institutional knowledge
- [ ] Risk framework connections (RCSA, KRI, scenario, capital) are assessed
- [ ] Event report is reviewed and approved by appropriate governance level
