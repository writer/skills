---
name: audit-response-drafting
description: Draft regulator-ready audit responses, MRA/MRIA remediation plans, and examination finding replies for banking supervisory agencies. Use when responding to OCC, Federal Reserve, FDIC, or CFPB examination findings, internal audit observations, consent order requirements, or supervisory letters requiring formal institutional response.

metadata:
  display_name: "Audit Response Drafting"
  short_description: "Draft formal responses to bank regulatory exam findings"
  default_prompt: "Check my audit response for gaps risks and required fixes"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Audit Response Drafting

## Overview

This skill produces formal, regulator-quality responses to examination findings, audit observations, and supervisory actions. It covers Matter Requiring Attention (MRA), Matter Requiring Immediate Attention (MRIA), consent order corrective action plans, internal audit finding responses, and supervisory letter replies. Output follows the tone, structure, and specificity expected by OCC, Federal Reserve, FDIC, and CFPB examiners.

## When to Use

- Drafting management responses to regulatory examination findings (MRA/MRIA)
- Preparing corrective action plans for consent orders or formal enforcement actions
- Responding to internal audit observations and recommendations
- Addressing supervisory letters (SR letters, OCC bulletins) with required institutional actions
- Documenting remediation progress for follow-up examinations
- Preparing board-level response packages for significant supervisory findings
- Drafting responses to 4(m) commitments or safety and soundness concerns

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Finding text | Exact language of the examination finding or audit observation | Regulatory document |
| Finding classification | MRA, MRIA, observation, violation, consent order provision | Classification |
| Root cause | Institutional assessment of why the finding occurred | Analysis |
| Current state | Existing controls, policies, and practices in the affected area | Documentation |
| Remediation plan | Proposed corrective actions with timelines | Action plan |
| Responsible parties | Individuals accountable for remediation | Org chart/assignments |
| Evidence of progress | Actions already taken since the finding was issued | Documentation |

## Methodology

### Step 1: Analyze the Finding

Deconstruct the regulatory finding into actionable components:

1. **Identify the core deficiency**: What specific requirement, standard, or expectation was not met?
2. **Determine the regulatory basis**: Which law, regulation, guidance, or supervisory standard is cited?
3. **Assess the severity**: MRA (deficiency requiring corrective action) vs. MRIA (deficiency requiring immediate corrective action) vs. violation (non-compliance with law/regulation)
4. **Map the scope**: Which business lines, processes, products, and systems are affected?
5. **Identify the implicit expectations**: What does the examiner expect to see in the response?

### Step 2: Acknowledge the Finding

Draft the acknowledgment with appropriate regulatory tone:

**Effective acknowledgment components**:
- Express understanding of the examiner's concern without being defensive
- Demonstrate awareness of the regulatory standard or expectation
- Accept institutional responsibility (avoid blaming individuals or predecessors)
- Acknowledge the importance of the area to safety and soundness
- Reference any self-identified issues that align with the finding

**Tone guidance**:
- Use professional, respectful, direct language
- Avoid: defensiveness, minimizing the finding, excessive qualification
- Avoid: "we disagree with the finding" (unless factually inaccurate — rare and requires legal counsel)
- Appropriate: "Management acknowledges the finding and has developed a comprehensive remediation plan"
- Appropriate: "The institution recognizes the importance of [area] and has prioritized corrective action"

### Step 3: Provide Root Cause Analysis

Document the institutional assessment of why the deficiency exists:

| Root Cause Category | Specific Cause | Evidence |
|---------------------|---------------|----------|
| **Governance** | Insufficient board/committee oversight of [area] | [Meeting minutes, reporting gaps] |
| **Policy** | Policy did not address [specific requirement] | [Policy review findings] |
| **Process** | Procedures lacked [specific step or control] | [Process documentation gaps] |
| **Technology** | Systems did not support [capability] | [System assessment] |
| **Staffing** | Insufficient expertise/capacity in [function] | [Staffing analysis] |
| **Training** | Staff not trained on [requirement] | [Training records review] |
| **Monitoring** | QC/QA program did not identify the issue | [Monitoring program gaps] |

Root cause analysis must go beyond the surface issue to explain systemic drivers. Examiners expect depth; "human error" or "oversight" alone is insufficient.

### Step 4: Detail the Corrective Action Plan

Structure each remediation action with precision:

```markdown
### Corrective Action [#]: [Title]

**Finding Reference**: [Finding number or section]
**Root Cause Addressed**: [Which root cause this action remediates]
**Description**: [Detailed description of the corrective action]
**Deliverables**:
  1. [Specific deliverable with measurable completion criteria]
  2. [Specific deliverable with measurable completion criteria]
**Responsible Party**: [Name, title — individual, not committee]
**Target Completion Date**: [Specific date]
**Milestones**:
  - [Milestone 1]: [Date]
  - [Milestone 2]: [Date]
  - [Milestone 3]: [Date]
**Sustainability**: [How the institution will ensure the fix is lasting]
**Validation**: [How completion and effectiveness will be verified]
```

### Step 5: Demonstrate Progress Already Made

Show that the institution has not waited for the formal response to begin remediation:

- List specific actions taken since the finding was communicated
- Provide evidence of early wins (policies drafted, systems configured, training delivered)
- Quantify progress (e.g., "65% of impacted accounts have been reviewed and remediated")
- Show governance attention (board briefed, committee charter amended, resources approved)

Examiners view prompt institutional response favorably. Demonstrating immediate action is a critical element of the response.

### Step 6: Address Sustainability

Examiners want assurance that fixes will be durable. Document:

**First line of defense**: Business line ownership of corrective processes
- Updated procedures embedded in day-to-day operations
- Performance metrics and accountability for compliance

**Second line of defense**: Independent compliance/risk monitoring
- Ongoing monitoring program for the remediated area
- Quality assurance testing with defined sampling methodology
- KRI dashboard for early detection of recurrence

**Third line of defense**: Internal audit coverage
- Audit plan inclusion for validation of remediation effectiveness
- Follow-up audit timing and scope

### Step 7: Package for Governance Approval

Prepare the response package with required governance artifacts:
- Board or committee resolution approving the remediation plan
- Resource commitment (budget, FTEs, technology investment)
- Escalation protocol if milestones are at risk
- Reporting cadence to board/committee on remediation progress
- Timeline for completion and self-assessment before next examination

## Output Specification

```markdown
# Management Response to [Examination/Audit] Findings
## [Institution Name] — [Date]

## Executive Summary
[1-2 paragraph overview of findings received, institutional response posture, and remediation commitment]

## Response to Finding [#]: [Finding Title]

### Finding
[Exact text of the examination finding]

### Classification
[MRA / MRIA / Violation / Observation]

### Regulatory Basis
[Cited regulation, guidance, or supervisory standard]

### Management Acknowledgment
[Acknowledgment statement per Step 2 guidance]

### Root Cause Analysis
[Structured analysis per Step 3]

### Corrective Action Plan
[Detailed actions per Step 4, each with deliverables, owners, dates]

### Progress to Date
[Actions already taken per Step 5]

### Sustainability Controls
[First, second, and third line of defense per Step 6]

### Timeline Summary
| Milestone | Target Date | Owner | Status |
|-----------|------------|-------|--------|
| [Milestone] | [Date] | [Name] | [Not started / In progress / Complete] |

---
[Repeat for each finding]

## Governance
- **Board Approval Date**: [Date]
- **Oversight Committee**: [Committee name]
- **Reporting Cadence**: [Frequency]
- **Next Self-Assessment**: [Date]

## Appendices
- A: Detailed Project Plan
- B: Policy/Procedure Updates (draft or final)
- C: Resource Allocation Summary
- D: Governance Approvals
```

## Analysis Framework

### Finding Severity Assessment

Determine the appropriate response intensity:

| Classification | Response Intensity | Timeline | Governance Level |
|---------------|-------------------|----------|-----------------|
| **MRIA** | Highest priority, may require interim corrective action | 30-90 days | Board notification, executive ownership |
| **MRA** | High priority, structured remediation plan | 90-180 days | Board committee oversight |
| **Violation** | Must cure the violation; may overlap with MRA/MRIA | Per regulation | Compliance officer and legal |
| **Observation** | Management attention recommended | 180-365 days | Senior management |
| **Consent Order** | Mandatory compliance, subject to enforcement | Per order terms | Board approval required |

### Regulatory Tone Calibration

Match language formality to the recipient:

- **OCC**: Formal, precise, reference Comptroller's Handbook and OCC bulletins
- **Federal Reserve**: Formal, reference SR letters and supervisory expectations
- **FDIC**: Formal, reference FIL letters and risk management examination guidance
- **Internal Audit**: Professional but slightly less formal; focus on practical remediation
- **Board reporting**: Executive summary with strategic context; avoid excessive technical detail

## Examples

**Example 1 — MRA Response (BSA/AML)**:
"Management acknowledges the MRA regarding the transaction monitoring program's coverage gaps for electronic banking channels. Root cause analysis identified three contributing factors: (1) the transaction monitoring system was not configured to capture mobile deposit and Zelle transactions introduced in 2024; (2) the BSA risk assessment was not updated to reflect the volume growth in electronic channels; and (3) QA testing did not include electronic banking scenarios. Corrective actions: (1) Configure transaction monitoring rules for mobile deposit and Zelle (BSA Systems Manager, complete by 03/31/2026); (2) Update BSA/AML risk assessment to incorporate electronic banking channel volumes and typologies (BSA Officer, complete by 02/28/2026); (3) Add electronic banking scenarios to QA testing program (Compliance Testing Manager, complete by 04/30/2026). Progress: System vendor engaged on 01/15/2026; rule configuration 40% complete; updated risk assessment in draft. Board BSA Committee briefed on 01/22/2026."

**Example 2 — MRIA Response (Credit Risk)**:
"Management treats this MRIA regarding the commercial real estate concentration risk management program with the highest urgency. The institution acknowledges that CRE concentration (385% of total risk-based capital) exceeds the 300% supervisory guidance threshold without commensurate risk management infrastructure. Immediate actions taken: (1) Board approved a CRE concentration policy with sublimits by property type (01/05/2026); (2) Origination of new CRE office loans suspended pending policy implementation (effective 12/20/2025); (3) Enhanced monitoring report for CRE portfolio risk metrics delivered to board weekly (started 12/22/2025). Corrective action plan: (1) Implement CRE stress testing at the loan and portfolio level (Chief Credit Officer, 03/31/2026); (2) Establish CRE concentration committee with monthly review cadence (CRO, 02/15/2026); (3) Develop CRE reduction strategy targeting 340% within 18 months (CFO/CCO, 04/30/2026)."

## Guidelines

- Always use the exact finding text as provided by the examiner; do not paraphrase
- Responses must be specific and measurable; avoid vague commitments like "will enhance" without specifics
- Every corrective action must have a single accountable individual (name and title)
- Dates must be specific (month/day/year), not relative ("within 90 days")
- Demonstrate institutional self-awareness; examiners value organizations that understand their weaknesses
- Do not over-promise on timelines; missed commitments damage credibility
- Show how the fix integrates into the existing risk management framework
- Reference prior remediation successes to establish credibility
- Include budget and resource commitments to demonstrate seriousness
- Have legal counsel review responses before submission, especially for MRIAs and consent orders
- Treat all examination communications as confidential supervisory information

## Validation Checklist

- [ ] Each finding is addressed individually with its exact text quoted
- [ ] Acknowledgment is professional, accepting, and non-defensive
- [ ] Root cause analysis identifies systemic causes, not just symptoms
- [ ] Corrective actions are specific, measurable, and time-bound
- [ ] Each action has a single named accountable owner
- [ ] Target dates are realistic and achievable
- [ ] Progress to date demonstrates prompt institutional response
- [ ] Sustainability section covers all three lines of defense
- [ ] Governance approval is documented (board resolution or committee minutes)
- [ ] Response tone matches the formality expected by the examining agency
