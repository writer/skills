---
name: customer-issue-root-cause
description: Perform root cause analysis on banking customer complaints and operational issues. Use when investigating the underlying causes of customer complaints, service failures, processing errors, or recurring operational issues in retail or commercial banking operations.

metadata:
  display_name: "Customer Issue Root Cause"
  short_description: "Root cause analysis for banking customer complaints"
  default_prompt: "Analyze my customer issue root cause and recommend clear next actions"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Customer Issue Root Cause Analysis

## Overview

This skill produces structured root cause analyses for banking customer complaints and operational issues. It applies systematic RCA methodologies (Five Whys, Fishbone/Ishikawa, fault tree analysis) to identify systemic causes of service failures, processing errors, and customer dissatisfaction. Output supports complaint resolution, process improvement, UDAAP risk mitigation, and regulatory complaint management requirements.

## When to Use

- Investigating the root cause of customer complaints escalated to management
- Analyzing patterns in recurring operational errors or service failures
- Supporting CFPB or state regulator complaint response requirements
- Identifying systemic issues from complaint trend analysis
- Documenting RCA for executive complaint resolution reports
- Feeding findings into Six Sigma or Lean process improvement initiatives
- Assessing UDAAP risk from complaint patterns

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Complaint details | Customer complaint narrative, category, severity | Complaint record |
| Account/transaction data | Related account and transaction information | System extracts |
| Process documentation | SOPs, policies, workflows for the affected area | Procedure documents |
| System logs | Application logs, audit trails, error codes | Technical logs |
| Historical complaints | Similar complaints from the past 12 months | Complaint database |
| Staff interviews | Input from involved employees | Interview notes |
| Regulatory context | Applicable regulations (Reg E, Reg CC, UDAAP, FCRA) | Regulatory mapping |

## Methodology

### Step 1: Define the Problem Statement

Craft a precise problem statement using the 5W1H framework:

| Element | Question | Answer |
|---------|----------|--------|
| **What** | What went wrong? | [Specific failure or error] |
| **Who** | Who is affected? | [Customer segment, volume of affected customers] |
| **When** | When did it occur/start? | [Date/time, duration] |
| **Where** | Where in the process did it fail? | [Process step, system, channel] |
| **Why** | Why is it a problem? | [Customer impact, financial impact, regulatory risk] |
| **How** | How was it detected? | [Customer report, internal monitoring, audit] |

**Problem statement template**: "[What] occurred affecting [Who] starting [When] in the [Where] process, resulting in [impact]. The issue was detected via [How]."

### Step 2: Gather and Verify Facts

Collect evidence from multiple sources to avoid bias:

1. **Customer perspective**: Complaint narrative, interaction history, stated expectations
2. **Transaction/system data**: Actual transaction records, system timestamps, error codes
3. **Process execution**: What steps were followed vs. what the SOP prescribes
4. **Staff perspective**: Employee account of what happened and why
5. **Control evidence**: Whether preventive and detective controls functioned
6. **Regulatory timeline**: Applicable response deadlines and compliance requirements

Cross-reference sources to identify discrepancies and establish the factual timeline.

### Step 3: Apply Root Cause Analysis Framework

Use appropriate RCA methodology based on complexity:

**Five Whys** (for straightforward issues):
1. Why did [problem] occur? → [Direct cause]
2. Why did [direct cause] happen? → [Contributing factor]
3. Why did [contributing factor] exist? → [Process gap]
4. Why wasn't [process gap] caught? → [Control failure]
5. Why did [control] fail? → [Root cause]

**Fishbone (Ishikawa) Diagram** (for complex, multi-factor issues):

| Category | Potential Causes |
|----------|-----------------|
| **People** | Training gaps, staffing levels, skill mismatches, turnover |
| **Process** | Procedure gaps, handoff failures, exception handling |
| **Policy** | Outdated policy, ambiguous guidance, conflicting rules |
| **Technology** | System errors, integration failures, data quality |
| **Communication** | Customer miscommunication, internal miscommunication |
| **External** | Vendor failures, regulatory changes, customer behavior |

**Fault Tree Analysis** (for high-severity or recurring issues):
- Start with the undesired event (top event)
- Decompose into intermediate events using AND/OR logic gates
- Identify the minimal cut sets (combinations of basic events that cause the top event)
- Prioritize based on probability and impact

### Step 4: Assess Customer Impact

Quantify the impact across dimensions:

| Impact Dimension | Assessment | Metric |
|------------------|------------|--------|
| Financial harm | Direct monetary loss to customer | [$Amount per customer] |
| Inconvenience | Time, effort, disruption to customer | [Hours, interactions required] |
| Breadth | Number of customers affected | [Count and % of base] |
| Duration | How long the issue persisted | [Days/weeks] |
| Vulnerability | Were vulnerable populations disproportionately affected? | [Yes/No, details] |
| Reputation | Social media, press, or viral complaint risk | [Low/Medium/High] |

### Step 5: Evaluate Regulatory Risk

Assess the complaint against regulatory frameworks:

**UDAAP Analysis** (Unfair, Deceptive, Abusive Acts or Practices):
- **Unfair**: Does the practice cause substantial injury not reasonably avoidable by consumers, not outweighed by benefits?
- **Deceptive**: Was there a material misrepresentation or omission likely to mislead a reasonable consumer?
- **Abusive**: Did the practice take unreasonable advantage of consumer's lack of understanding, inability to protect their interests, or reasonable reliance on the institution?

**Regulation-Specific Assessment**:
- Reg E: Electronic fund transfer rights and error resolution
- Reg CC: Funds availability and check hold policies
- Reg DD: Truth in Savings disclosure accuracy
- Reg Z: Truth in Lending disclosure and billing error rights
- FCRA: Credit reporting accuracy and dispute rights
- SCRA: Servicemembers Civil Relief Act protections

### Step 6: Identify Systemic Patterns

Look beyond the individual complaint to identify systemic issues:

- **Volume analysis**: How many similar complaints in the past 12 months?
- **Trend analysis**: Is the complaint rate increasing, stable, or decreasing?
- **Cluster analysis**: Are complaints concentrated in specific branches, channels, or products?
- **Timing analysis**: Do complaints correlate with system changes, policy updates, or staffing changes?
- **Demographic analysis**: Are certain customer segments disproportionately affected?

### Step 7: Develop and Document Recommendations

Structure recommendations by category:

**Immediate remediation** (0-30 days):
- Customer-specific resolution (refund, correction, apology)
- Interim process changes to prevent recurrence
- Communication to affected customers if broader impact identified

**Short-term fixes** (30-90 days):
- Process redesign for the affected workflow
- System configuration changes or defect fixes
- Staff retraining on corrected procedures
- Enhanced monitoring for the affected area

**Long-term improvements** (90-365 days):
- Policy or procedure rewrite
- Technology solution for error prevention
- Organizational or staffing changes
- Customer experience redesign

## Output Specification

```markdown
# Root Cause Analysis: [Case/Complaint ID]

## Problem Statement
[Structured problem statement per Step 1]

## Facts and Timeline
| Date/Time | Event | Source |
|-----------|-------|--------|
| [Date] | [Event description] | [Evidence source] |

## Root Cause Analysis
### Method Used: [Five Whys / Fishbone / Fault Tree]
[Analysis detail per Step 3]

### Root Cause(s) Identified
1. **[Root Cause]**: [Description with evidence]
2. **[Contributing Factor]**: [Description with evidence]

### Root Cause Category
[People / Process / Policy / Technology / Communication / External]

## Impact Assessment
| Dimension | Assessment |
|-----------|------------|
| Financial harm | [$X per customer, $X total] |
| Customers affected | [N customers] |
| Duration | [X days] |
| UDAAP risk | [Low/Medium/High] |

## Regulatory Assessment
[Applicable regulations and compliance status]

## Systemic Pattern Analysis
[Volume, trend, cluster, and timing analysis results]

## Recommendations
### Immediate (0-30 days)
- [Action with owner and date]

### Short-term (30-90 days)
- [Action with owner and date]

### Long-term (90-365 days)
- [Action with owner and date]

## Prevention
[How recurrence will be prevented and monitored]
```

## Analysis Framework

### Complaint Categorization Taxonomy

Classify complaints for pattern analysis:
- **Account services**: Opening/closing, maintenance, access, statements
- **Transactions**: Posting errors, holds, delays, unauthorized activity
- **Fees**: Overdraft, maintenance, ATM, wire, early closure
- **Lending**: Application, servicing, payoff, escrow, rate
- **Digital banking**: Mobile app, online banking, bill pay, transfers
- **Customer service**: Wait times, staff behavior, resolution quality

### UDAAP Risk Matrix

| Likelihood | Low Impact | Medium Impact | High Impact |
|-----------|-----------|---------------|------------|
| **High** (frequent complaints) | Monitor | Remediate | Escalate immediately |
| **Medium** (periodic complaints) | Track | Investigate | Remediate |
| **Low** (isolated complaint) | Document | Monitor | Investigate |

## Examples

**Example 1 — Fee Complaint RCA**:
"Problem: Customer charged $175 in overdraft fees (5 x $35) on 2025-08-15 for transactions totaling $47.32. Customer states she had sufficient funds. Five Whys: (1) Why were fees charged? Five transactions posted against insufficient funds. (2) Why were funds insufficient? A $1,200 mobile deposit was placed on extended hold. (3) Why was an extended hold placed? The deposit exceeded the $225 next-day availability threshold and the account was <30 days old (Reg CC exception). (4) Why wasn't the customer notified of the hold? The mobile deposit flow does not display hold duration for new accounts. (5) Root cause: Mobile deposit user experience does not communicate Reg CC hold policies for new accounts, creating a gap between customer expectation and actual funds availability. UDAAP risk: Medium — while the hold is permitted under Reg CC, the failure to clearly communicate availability timing could be considered deceptive. Recommendation: Update mobile deposit confirmation screen to display expected availability date and amount for all deposits subject to holds."

**Example 2 — Systemic Pattern RCA**:
"Analysis of 847 complaints received in Q3 2025 categorized as 'transaction posting error' reveals a 340% increase from Q2. Cluster analysis shows 78% originated from customers using the mobile bill pay feature launched June 2025. Root cause: a system defect causes duplicate payment submissions when users tap the 'Pay' button during processing latency >3 seconds. The defect was introduced in the v4.2 mobile app release (06/01/2025). Customer impact: 1,247 customers affected, $892K in duplicate payments, $43K in overdraft fees. Immediate action: Deploy hotfix to disable duplicate button press (v4.2.1, released 09/25/2025). Remediation: Refund all overdraft fees caused by duplicate payments ($43K); reverse duplicate payments still in processing ($218K). Long-term: Implement idempotency controls in all payment APIs to prevent duplicate submission regardless of UI behavior."

## Guidelines

- Begin every RCA with verified facts, not assumptions or customer allegations alone
- Root cause must be systemic (process, policy, technology, training); individual blame is not an RCA outcome
- Always assess UDAAP risk for consumer complaints, even when the practice is technically compliant
- Document both the root cause and contributing factors; most issues have multiple contributors
- Quantify customer impact in both individual and aggregate terms
- Check for patterns before assuming a complaint is isolated
- Reg E disputes have specific timeline requirements; document compliance in every applicable case
- Recommendations must be actionable with specific owners and deadlines
- Track recommendation implementation to closure and measure effectiveness
- Preserve RCA documentation for 5 years (regulatory examination and legal discovery retention)

## Validation Checklist

- [ ] Problem statement uses the 5W1H framework and is specific
- [ ] Factual timeline is established from verified sources
- [ ] RCA method is appropriate for the complexity of the issue
- [ ] Root cause is systemic, not individual-level blame
- [ ] Customer impact is quantified across all relevant dimensions
- [ ] UDAAP risk assessment is completed for consumer complaints
- [ ] Applicable regulations are identified and compliance assessed
- [ ] Systemic pattern analysis checks for similar complaints
- [ ] Recommendations are categorized by timeline with owners and dates
- [ ] Prevention measures and monitoring plans are specified
