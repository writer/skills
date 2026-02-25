---
name: policy-exception-review
description: Analyze policy exceptions for risk patterns, concentration risks, and control gaps in financial institutions. Use when reviewing policy exception requests, analyzing exception trends, assessing exception backlogs, or evaluating whether exceptions indicate systemic control weaknesses under COSO, OCC Heightened Standards, or SOX frameworks.

metadata:
  display_name: "Policy Exception Review"
  short_description: "Review bank policy exceptions for risk patterns and gaps"
  default_prompt: "Check my policy exception for gaps risks and required fixes"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Policy Exception Review

## Overview

Analyze policy exception requests and exception portfolios to identify risk patterns, concentration risks, approval governance weaknesses, and systemic control gaps. This skill applies the COSO Internal Control Framework (2013), OCC Heightened Standards (12 CFR 30 Appendix D), and Three Lines of Defense model to evaluate whether exceptions are appropriately governed, time-bound, and monitored for escalation.

## When to Use

- Reviewing individual policy exception requests for completeness and risk assessment
- Analyzing exception portfolios for concentration patterns and trend analysis
- Assessing whether recurring exceptions indicate a need for policy revision
- Evaluating exception governance processes against regulatory expectations
- Preparing board or committee reporting on exception volumes and risk exposure
- Responding to regulatory findings related to exception management practices

## Required Inputs

- **Exception request details**: Policy name, exception description, business justification, requestor, approver
- **Exception portfolio data**: Active exceptions by policy domain, age, risk rating, business unit
- **Policy framework**: Applicable policies, risk appetite statements, materiality thresholds
- **Governance structure**: Approval authority matrix, escalation procedures, committee charters
- **Historical data** (optional): Prior exception trends, audit findings, regulatory feedback

## Methodology

### Step 1: Exception Request Completeness Assessment

Validate each exception request contains all required elements per OCC Heightened Standards:

- **Business justification**: Clear articulation of why the exception is necessary and why policy compliance is not feasible
- **Risk assessment**: Identification of incremental risk introduced by the exception, mapped to the institution's risk taxonomy
- **Compensating controls**: Specific mitigating actions that reduce residual risk to within risk appetite
- **Duration and expiration**: Defined time boundary with a remediation plan to return to compliance
- **Approval authority**: Confirmation that the approver has delegated authority commensurate with the risk level
- **Monitoring plan**: Ongoing oversight mechanisms during the exception period

Flag any exception lacking these elements as governance-deficient.

### Step 2: Risk Pattern and Concentration Analysis

Analyze the exception portfolio for systemic risk indicators:

- **Policy concentration**: Identify policies with disproportionately high exception volumes, which may indicate policy misalignment with business operations
- **Business unit concentration**: Flag units generating >15% of total exceptions relative to their risk profile
- **Temporal clustering**: Detect spikes in exception requests that correlate with regulatory deadlines, system migrations, or organizational changes
- **Risk rating distribution**: Assess whether high-risk exceptions are appropriately limited and receive enhanced oversight
- **Aging analysis**: Identify exceptions exceeding their original duration, indicating remediation failures

### Step 3: Compensating Control Adequacy Evaluation

Assess compensating controls against COSO Principle 10 (selects and develops control activities that mitigate risks) and Principle 11 (selects and develops general controls over technology):

- Verify compensating controls are specific, measurable, and directly address the risk introduced by the exception
- Confirm controls are operationally feasible and currently active (not aspirational)
- Evaluate whether manual compensating controls introduce operational risk that offsets the benefit
- Assess control owner accountability and monitoring frequency
- Determine if compensating controls have been independently tested by the second or third line

### Step 4: Governance and Approval Authority Review

Evaluate the exception approval process against the Three Lines of Defense model:

- **First Line**: Business unit risk acceptance is documented with management attestation
- **Second Line**: Independent risk management has reviewed and concurred on the risk assessment and compensating controls
- **Third Line**: Internal audit has periodic coverage of the exception management process
- Validate approval authorities against the institution's delegated authority matrix
- Confirm that exceptions exceeding materiality thresholds are escalated to appropriate board-level or senior management committees
- Assess whether conflicts of interest exist in the approval chain (e.g., requestor and approver in same reporting line)

### Step 5: Regulatory Alignment Assessment

Map exception management practices to regulatory expectations:

- **OCC Heightened Standards**: Evaluate whether the exception process supports the institution's risk governance framework and three lines of defense obligations
- **SOX 302/404**: For exceptions affecting financial reporting controls, assess impact on management's assessment of internal control effectiveness
- **COSO Principle 2**: Confirm the board exercises oversight of the development and performance of internal control, including exception governance
- Identify any exceptions that could constitute a "significant deficiency" or "material weakness" under SOX if not properly remediated

### Step 6: Trend Analysis and Predictive Indicators

Perform longitudinal analysis to identify emerging risks:

- Compare current exception volumes against rolling 12-month and 24-month averages
- Identify policies with increasing exception rates that may require revision
- Track remediation success rates and average time-to-closure
- Correlate exception trends with operational loss events, audit findings, or regulatory actions
- Assess whether exception volume growth outpaces the institution's control infrastructure capacity

### Step 7: Reporting and Recommendations

Generate structured findings with prioritized recommendations:

- Classify findings by severity: Critical, High, Medium, Low
- Map each finding to the relevant COSO principle, OCC standard, or regulatory expectation
- Provide specific, actionable remediation steps with ownership and target dates
- Include forward-looking risk indicators and early warning metrics for ongoing monitoring

## Output Specification

```markdown
# Policy Exception Review Report

## Executive Summary
[2-3 paragraph overview of exception portfolio health, key risk concentrations, and governance effectiveness]

## Exception Portfolio Metrics
| Metric | Current Period | Prior Period | Trend |
|--------|---------------|-------------|-------|
| Total Active Exceptions | [count] | [count] | [↑↓→] |
| High-Risk Exceptions | [count] | [count] | [↑↓→] |
| Overdue Exceptions | [count] | [count] | [↑↓→] |
| Average Age (days) | [days] | [days] | [↑↓→] |
| Remediation Success Rate | [%] | [%] | [↑↓→] |

## Risk Concentration Analysis
[Policy-level and business-unit-level concentration findings]

## Compensating Control Assessment
[Evaluation of control adequacy across the exception portfolio]

## Governance Findings
[Findings mapped to COSO principles and OCC Heightened Standards]

## Regulatory Impact Assessment
[SOX implications, examination readiness considerations]

## Recommendations
| Priority | Finding | Recommendation | Owner | Target Date |
|----------|---------|----------------|-------|-------------|

## Appendix: Exception Detail
[Individual exception summaries with risk ratings and status]
```

## Analysis Framework

Apply the following risk-scoring matrix for individual exceptions:

| Factor | Weight | Scoring Criteria |
|--------|--------|-----------------|
| Risk severity of underlying policy | 30% | Critical=4, High=3, Medium=2, Low=1 |
| Compensating control adequacy | 25% | Absent=4, Weak=3, Adequate=2, Strong=1 |
| Duration / age of exception | 20% | >12mo=4, 6-12mo=3, 3-6mo=2, <3mo=1 |
| Approval governance quality | 15% | Deficient=4, Needs improvement=3, Satisfactory=2, Strong=1 |
| Remediation plan credibility | 10% | No plan=4, Vague=3, Defined=2, Executed=1 |

Aggregate score interpretation: 3.5-4.0 Critical, 2.5-3.4 High, 1.5-2.4 Medium, 1.0-1.4 Low.

## Examples

**Example 1 — Concentration Risk Finding**:
"Policy XYZ-003 (Vendor Due Diligence) has 47 active exceptions representing 22% of the total exception portfolio, a 35% increase from the prior quarter. 60% of these exceptions originate from the Operations division. This concentration suggests the policy requirements may be misaligned with current vendor onboarding volumes, or the division lacks adequate resources to achieve compliance. Recommend: (1) Policy owner conducts a feasibility review within 30 days, (2) Operations division presents a remediation roadmap to the Risk Committee."

**Example 2 — Governance Gap Finding**:
"12 high-risk exceptions were approved without documented second-line concurrence, violating the institution's Three Lines of Defense framework and OCC Heightened Standards requirements for independent risk management oversight. Recommend: (1) Retroactive second-line review within 15 days, (2) Update approval workflow to enforce mandatory second-line sign-off for all high-risk exceptions."

## Guidelines

- Always map findings to specific COSO principles, OCC standards, or regulatory requirements
- Distinguish between isolated exceptions and systemic patterns requiring policy or process changes
- Avoid treating all exceptions as negative; some indicate appropriate risk-taking within appetite
- Consider the institution's size, complexity, and risk profile when benchmarking exception volumes
- Maintain objectivity; do not advocate for blanket exception denial, which can drive shadow risk-taking
- Ensure recommendations are specific, actionable, and include clear ownership and timelines
- Consider the cumulative risk of multiple individually-acceptable exceptions across related policies

## Validation Checklist

- [ ] All active exceptions reviewed for completeness against required data elements
- [ ] Concentration analysis performed by policy, business unit, risk rating, and duration
- [ ] Compensating controls assessed for specificity, operability, and independent testing
- [ ] Approval governance evaluated against the delegated authority matrix and Three Lines of Defense
- [ ] SOX-relevant exceptions flagged for financial reporting impact assessment
- [ ] Trend analysis covers minimum 12-month lookback period
- [ ] Findings mapped to specific regulatory standards and COSO principles
- [ ] Recommendations include priority, ownership, and target remediation dates
- [ ] Report reviewed for consistency, accuracy, and appropriate tone for the target audience
