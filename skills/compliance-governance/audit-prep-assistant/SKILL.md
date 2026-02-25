---
name: audit-prep-assistant
description: Prepare audit-ready documentation packages for internal audits, external audits, regulatory inspections, and retailer compliance audits in CPG organizations. Use when preparing for an upcoming audit, organizing evidence, conducting pre-audit self-assessments, or building audit response strategies.

metadata:
  display_name: "Audit Prep Assistant"
  short_description: "Prepare CPG audit documentation and compliance evidence"
  default_prompt: "Check my audit prep for gaps risks and required fixes"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Audit Prep Assistant

## Overview

Prepare comprehensive, organized documentation packages for audits across the CPG enterprise — including internal financial audits, external audits (Big 4), FDA/regulatory inspections, retailer compliance audits, and sustainability/ESG audits. This skill systematizes evidence gathering, gap identification, pre-audit self-assessment, and response preparation to minimize findings and demonstrate governance maturity.

## When to Use

- Preparing for scheduled internal audit engagements
- External financial audit (SOX, Big 4) support
- FDA facility inspection preparation (FSMA, cGMP)
- Retailer quality/compliance audits (SQF, BRC, GFSI)
- ESG/sustainability audit preparation (GRI, SASB reporting)
- Regulatory agency investigation response
- Post-audit corrective action plan development
- Annual audit readiness assessment

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Audit scope | Type of audit, areas covered, time period | Audit notification or plan |
| Audit timeline | Key dates (fieldwork start, draft report, final report) | Calendar |
| Auditor identity | Internal audit team, external firm, regulatory agency, or retailer | Profile |
| Prior audit reports | Previous findings and corrective action status | Audit reports |
| Process documentation | SOPs, policies, controls relevant to audit scope | Document inventory |
| Transaction data | Financial or operational records to be examined | Data access details |
| Responsible parties | Process owners for each auditable area | RACI matrix |
| Known issues | Pre-existing gaps or concerns the team is aware of | Issue log |

## Methodology

### Step 1: Audit Scope and Risk Assessment

Map the audit scope to your organization's risk and control landscape:

**Audit Type Classification:**

| Audit Type | Auditor | Focus Areas | Typical Duration | Formality |
|-----------|--------|-------------|-----------------|-----------|
| Internal Financial | Internal Audit team | SOX controls, financial accuracy, fraud risk | 2-4 weeks | Formal |
| External Financial | Big 4 / external firm | Financial statements, material misstatement | 4-8 weeks | Formal |
| FDA Inspection | FDA investigator | FSMA compliance, cGMP, HACCP, labeling | 1-5 days | Regulatory |
| Retailer Quality | Retailer QA or 3rd party | SQF/BRC/GFSI standards, facility compliance | 1-3 days | Contractual |
| ESG/Sustainability | 3rd party assessor | Environmental impact, social governance, reporting | 1-2 weeks | Voluntary/Mandated |
| Trade/Commercial | Internal/external | Trade spend compliance, pricing, deductions | 1-3 weeks | Internal |
| IT/Cybersecurity | Internal/external | Data protection, system controls, access management | 1-3 weeks | Formal |

**Pre-Audit Risk Heat Map:**
Identify areas of highest audit risk based on:

| Risk Factor | Weight | Assessment |
|-------------|--------|-----------|
| Prior audit findings (unresolved) | 25% | Count and severity of open items |
| Process changes since last audit | 20% | New systems, reorganizations, policy changes |
| Personnel turnover in key roles | 15% | Loss of institutional knowledge |
| Transaction volume/complexity | 15% | Higher volume = higher sampling risk |
| Regulatory scrutiny intensity | 15% | Recent enforcement actions in industry |
| Known control weaknesses | 10% | Self-identified gaps |

Score each factor 1-5 and compute weighted risk score. Areas scoring >3.5 require priority preparation.

### Step 2: Documentation Inventory and Gap Analysis

Create a comprehensive inventory of required evidence:

**Evidence Collection Framework:**

```
For each auditable area:

Area: [e.g., Trade Spend Compliance]
Key Control: [What control should be operating?]
Evidence Required:
  1. Policy/Procedure: [Document name, version, date]
     Status: Current / Outdated / Missing
  2. Control Evidence: [What proves the control is operating?]
     Status: Available / Partial / Missing
  3. Transaction Testing: [Sample of transactions for testing]
     Status: Accessible / Needs preparation
  4. Monitoring Reports: [Ongoing monitoring evidence]
     Status: Up to date / Outdated / Not performed

Gap: [Description of any documentation gaps]
Remediation: [Action to close gap before audit fieldwork]
Owner: [Person responsible]
Due Date: [Must complete before fieldwork]
```

**Common Documentation Requirements by Audit Type:**

| Audit Type | Critical Documents |
|-----------|-------------------|
| Financial (SOX) | Control narratives, test of design/operating effectiveness, reconciliations, journal entry approvals, segregation of duties matrix |
| FDA Inspection | HACCP plans, sanitation records, allergen controls, supplier certifications, complaint files, recall procedures, training records |
| Retailer Quality (SQF) | Food safety plan, prerequisite programs, internal audit records, CAPA log, calibration records, pest control logs |
| ESG | Carbon emissions data, water usage records, waste diversion metrics, supply chain assessments, community impact reports |
| Trade/Commercial | Trade spend approvals, promotional contracts, deduction support, pricing authorization, customer rebate calculations |

### Step 3: Prior Findings Remediation Status

Review and update status of all prior audit findings:

```
Prior Finding Tracker:

| # | Finding | Original Date | Severity | Corrective Action | Status | Evidence of Closure |
|---|---------|--------------|----------|-------------------|--------|-------------------|
| 1 | [Finding text] | [Date] | High | [Action taken] | Closed/Open/In Progress | [Evidence ref] |
| 2 | ... | ... | ... | ... | ... | ... |

Summary:
  Total Prior Findings: XX
  Closed: XX (XX%)
  In Progress: XX (XX%)
  Open/Past Due: XX (XX%) ← HIGH RISK — auditors will focus here

For each Open/Past Due finding:
  - Root cause for delay
  - Revised completion date
  - Interim mitigating controls
  - Escalation status
```

### Step 4: Control Self-Assessment

Conduct a pre-audit self-assessment to identify issues before the auditor does:

**Self-Assessment Protocol:**

1. **Walk-through testing**: Walk through each key process with the process owner to verify the control narrative matches actual practice.

2. **Sample testing**: Select a small sample (5-10 transactions) from each auditable area and test:
   - Is the control operating as designed?
   - Is there evidence of the control operating?
   - Are exceptions identified and resolved?

3. **Segregation of duties review**: Verify no single individual can:
   - Initiate AND approve transactions
   - Record AND reconcile entries
   - Authorize AND execute payments

4. **System access review**: Verify:
   - Access rights match current roles (no terminated employees)
   - Admin/superuser access is appropriately limited
   - Access changes are documented and approved

**Self-Assessment Results Template:**
```
Control: [Control name/description]
Design Assessment: Effective / Needs Improvement / Ineffective
Operating Assessment: Effective / Needs Improvement / Ineffective
Sample Tested: X of Y transactions
Exceptions Found: X
Exception Rate: X%
Overall Status: Pass / Fail / Conditional Pass
Remediation (if needed): [Action, owner, date]
```

### Step 5: Audit Day Preparation

Prepare the team for audit execution:

**Logistics Preparation:**
```
Audit Logistics Checklist:
  □ Conference room / workspace reserved for auditors
  □ System access provisioned (read-only for relevant systems)
  □ Wi-Fi credentials and building access arranged
  □ Key contact list provided to lead auditor
  □ Document request list (PBC list) responses organized
  □ Interview schedule coordinated with process owners
  □ Catering/hospitality arranged (if applicable)
```

**Team Preparation:**

| Role | Responsibility | Preparation |
|------|---------------|------------|
| Audit Coordinator | Single point of contact for auditors | Familiar with scope, timeline, document location |
| Process Owners | Answer questions about their area | Review controls, have evidence ready, practice responses |
| Data Providers | Pull requested data/reports | Pre-pull anticipated reports, verify accuracy |
| Executive Sponsor | Opening/closing meetings | Brief on scope, prior findings, key messages |

**Interview Preparation Guidelines:**
```
DO:
  ✓ Answer questions directly and truthfully
  ✓ Provide evidence when available
  ✓ Say "I don't know, but I'll find out" if uncertain
  ✓ Take notes on questions asked
  ✓ Follow up promptly on open items

DON'T:
  ✗ Volunteer information beyond the question asked
  ✗ Speculate about areas outside your responsibility
  ✗ Argue with the auditor's interpretation
  ✗ Provide draft or unapproved documents
  ✗ Make commitments without consulting the audit coordinator
```

### Step 6: PBC (Prepared by Client) List Management

Organize the document request list systematically:

```
PBC Tracking Matrix:

| # | Document Requested | Audit Area | Owner | Status | Due Date | Notes |
|---|-------------------|-----------|-------|--------|----------|-------|
| 1 | Q1-Q4 Trade Spend Approvals | Trade Compliance | [Name] | Complete | [Date] | Uploaded to portal |
| 2 | Vendor Master Change Log | Procurement | [Name] | In Progress | [Date] | Extracting from ERP |
| 3 | HACCP Plan (current) | Food Safety | [Name] | Complete | [Date] | v4.2, dated MM/DD |

Summary:
  Total Items Requested: XX
  Provided: XX (XX%)
  In Progress: XX (XX%)
  Not Yet Started: XX (XX%)
  Cannot Provide: XX (XX%) — document reason for each
```

### Step 7: Post-Audit Response Strategy

Prepare for responding to draft findings:

**Finding Response Framework:**
```
For each draft finding:

Finding: [Auditor's finding text]
Factual Accuracy: Agree / Partially Agree / Disagree

If Disagree:
  Counter-evidence: [Specific evidence that contradicts the finding]
  Proposed revision: [Suggested rewording if partially disagree]

If Agree:
  Root Cause: [Why the gap exists]
  Corrective Action Plan:
    Immediate: [Action within 30 days]
    Systemic: [Process/system change within 90 days]
  Owner: [Name and title]
  Target Date: [Realistic completion date]
  
Severity Negotiation:
  Auditor's rating: [Critical / High / Medium / Low]
  Your assessment: [Your proposed rating with rationale]
  Compensating controls: [Controls that mitigate the risk even without the primary control]
```

## Output Specification

```markdown
# Audit Preparation Package — [Audit Type] [Period]

## Audit Overview
- **Type**: [Internal / External / Regulatory / Retailer]
- **Auditor**: [Firm or team name]
- **Scope**: [Areas covered]
- **Period**: [Time period under audit]
- **Fieldwork Dates**: [Start - End]

## Pre-Audit Risk Assessment
[Heat map of auditable areas by risk score]

## Prior Findings Status
| Status | Count | % |
|--------|-------|---|
| Closed | XX | XX% |
| In Progress | XX | XX% |
| Open/Past Due | XX | XX% |

[Detail on open/past due items with remediation plans]

## Documentation Readiness

| Area | Policy Current? | Evidence Available? | Self-Assessment | Gaps |
|------|----------------|-------------------|----------------|------|
| [Area 1] | ✅ | ✅ | Pass | None |
| [Area 2] | ✅ | ⚠️ Partial | Conditional | [Gap description] |

## PBC List Status
[Tracking matrix with completion percentages]

## Self-Assessment Results
[Control-level results with exception rates and remediation actions]

## Team Assignments
[RACI matrix for audit support]

## Key Messages for Auditors
[Top 3-5 themes to emphasize during opening meeting and interviews]

## Risk Mitigation Actions (Before Fieldwork)
1. [Action with owner and deadline]
2. [Action with owner and deadline]

## Post-Audit Response Plan
[Strategy for managing draft findings and severity negotiations]
```

## Analysis Framework

**Audit Readiness Maturity Scale:**
| Level | Description | Indicators |
|-------|------------|-----------|
| 1 - Unprepared | Scrambling when audit is announced | Missing documents, no prior findings tracking, no self-assessment |
| 2 - Reactive | Preparing after notification | Documents gathered ad hoc, prior findings partially addressed |
| 3 - Prepared | Systematic preparation process | PBC pre-staged, self-assessment completed, team briefed |
| 4 - Proactive | Continuous audit readiness | Always ready, prior findings closed promptly, controls monitored |
| 5 - Exemplary | Audit-ready culture | Self-assessment exceeds audit rigor, zero repeat findings |

## Example

**Input**: "Internal audit is scheduled in 3 weeks to review trade spend compliance for Q1-Q3. Last audit had 4 findings: 2 closed, 1 in progress, 1 open. We recently changed our trade spend approval system."

**Analysis excerpt**:
> "**Risk Assessment: ELEVATED** due to (1) open prior finding, (2) system change during audit period, and (3) compressed preparation timeline. **Priority actions for the next 3 weeks:**
> Week 1: (1) Resolve the open prior finding or document interim compensating controls and revised target date. Auditors will focus heavily on repeat findings — an unresolved finding from the prior audit is the highest-risk item. (2) Document the system change: prepare a change management memo covering business justification, testing performed, parallel run results, and control continuity between old and new system.
> Week 2: (3) Conduct self-assessment on 20 trade spend transactions (10 pre-system change, 10 post) verifying approval authority, ROI documentation, and budget compliance. (4) Pre-stage the PBC list: pull all trade commitment approvals, promotional post-event analyses, and budget vs actual reports for Q1-Q3.
> Week 3: (5) Brief process owners — especially anyone who joined after the last audit. (6) Prepare opening meeting deck: lead with improvements made (2 prior findings closed, new system implemented) and proactively disclose the open finding with remediation plan.
> **Key risk to manage**: The system transition creates a natural control gap. Prepare a bridge document showing that no transactions fell through during the transition period by reconciling the old system's final approvals with the new system's initial transactions."

## Guidelines

- Start preparation immediately upon audit notification — time is the most constrained resource
- Prioritize open prior findings — repeat findings indicate control environment degradation
- Self-assessment should be more rigorous than the audit itself — finding your own issues is far better than having them found
- Organize all evidence in a logical structure matching the audit scope — disorganized evidence suggests disorganized controls
- Never withhold known issues — proactive disclosure with a remediation plan is viewed favorably
- Train interviewees: answer the question asked, provide evidence, don't speculate
- The audit coordinator role is critical — assign someone with organizational knowledge and auditor relationship skills

## Validation Checklist

- [ ] Audit scope mapped to risk and control landscape
- [ ] Pre-audit risk heat map completed with priority areas identified
- [ ] All prior findings reviewed with current remediation status
- [ ] Open/past due findings have documented escalation and interim controls
- [ ] Documentation inventory completed with gap analysis
- [ ] PBC list items tracked with completion status and owners
- [ ] Self-assessment conducted on high-risk areas with sample testing
- [ ] Segregation of duties and system access reviewed
- [ ] Team assignments and interview preparation completed
- [ ] Logistics arranged (workspace, access, schedule)
- [ ] Post-audit response strategy prepared
- [ ] Key messages for auditors defined and rehearsed
