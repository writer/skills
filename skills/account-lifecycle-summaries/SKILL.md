---
name: account-lifecycle-summaries
description: Generate comprehensive account history narratives covering the full lifecycle from opening through closure. Use when preparing customer relationship summaries, investigating account activity patterns, supporting dispute resolution, or creating account histories for regulatory or legal requests.

metadata:
  display_name: "Account Lifecycle Summaries"
  short_description: "Summarize full account history from opening through closure"
  default_prompt: "Summarize my account lifecycle with key findings and next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Account Lifecycle Summaries

## Overview

This skill produces structured, end-to-end narratives of customer account lifecycles for banking operations. It covers account opening, product utilization, service interactions, account modifications, dispute history, fee assessment, and closure events. Output supports relationship management, dispute resolution, regulatory response, legal discovery, and customer retention analysis.

## When to Use

- Preparing account histories for customer complaints or regulatory inquiries
- Creating relationship summaries for retention or cross-sell analysis
- Supporting legal discovery or subpoena responses with account timelines
- Investigating account activity patterns for BSA/AML or fraud reviews
- Documenting account closure circumstances and final disposition
- Preparing materials for customer escalations or executive complaints
- Supporting Reg E or Reg CC dispute investigation timelines

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Account data | Account number, type, open date, status | Core system extract |
| Transaction history | Full transaction ledger for the account | Transaction file |
| Service interactions | Call logs, branch visits, digital sessions, complaints | CRM/interaction records |
| Product changes | Upgrades, downgrades, rate changes, feature modifications | Product history |
| Fee history | Fees assessed, reversed, waived with reasons | Fee ledger |
| Dispute history | Claims filed, provisional credits, resolutions | Dispute system |
| Closure details | Closure date, reason, final balance disposition | Account records |

## Methodology

### Step 1: Establish Account Context

Build the foundational profile:

- **Account type and product**: Checking, savings, CD, money market, loan, credit card, LOC
- **Opening channel**: Branch, online, mobile, call center, referral
- **Opening date and circumstances**: Promotion, relationship expansion, new-to-bank
- **Initial funding**: Source and amount of initial deposit or credit line
- **Account ownership**: Individual, joint, UTMA, trust, business, estate
- **Associated accounts**: Related accounts in the household or entity relationship
- **Account features**: Overdraft protection, direct deposit, automatic payments, linked accounts

### Step 2: Map the Activity Timeline

Create a chronological narrative organized by lifecycle phase:

**Phase 1 — Onboarding (0-90 days)**:
- Account funding pattern (how quickly was the account funded?)
- Product activation (debit card activation, online enrollment, direct deposit setup)
- Initial transaction patterns establishing baseline behavior
- Early attrition indicators (low activity, funding shortfall)

**Phase 2 — Active Usage (ongoing)**:
- Average monthly balance trajectory (growing, stable, declining)
- Transaction volume and mix (debits, credits, ACH, wires, checks, POS)
- Product deepening events (new products added to relationship)
- Service channel usage patterns (branch, digital, ATM, call center)
- Fee patterns (overdraft frequency, maintenance fee assessment/waiver)

**Phase 3 — Relationship Changes**:
- Product modifications (upgrades, downgrades, feature changes)
- Rate changes and repricing events
- Address or contact information changes
- Ownership changes (add/remove signers, beneficiary updates)
- Risk rating changes

**Phase 4 — Distress Signals (if applicable)**:
- Balance decline trajectory and acceleration
- Overdraft frequency increase
- Return item patterns (NSF)
- Collection activity on linked loan products
- Service complaint escalation
- Delinquency progression

**Phase 5 — Closure**:
- Closure date and method (customer-initiated, bank-initiated, inactivity)
- Reason for closure (customer stated reason, bank documented reason)
- Final balance disposition (check issued, transfer, escheatment)
- Outstanding items at closure (pending transactions, holds, disputes)
- Post-closure activity (returned items, incoming deposits, tax reporting)

### Step 3: Analyze Service Interactions

Summarize the customer service history:

| Date | Channel | Type | Summary | Resolution | Sentiment |
|------|---------|------|---------|------------|-----------|
| [Date] | [Channel] | [Inquiry/Complaint/Request] | [Brief summary] | [Resolution] | [Positive/Neutral/Negative] |

Calculate service metrics:
- Total interactions over account life
- Complaint frequency and escalation rate
- Average resolution time
- Channel preference distribution
- Net sentiment trajectory (improving, stable, deteriorating)

### Step 4: Document Fee and Pricing History

Provide a comprehensive fee narrative:
- Total fees assessed over account life by fee type
- Fee waivers and reversals with documented reasons
- Net fee revenue from the account
- Fee-related complaints and their outcomes
- Comparison to product fee schedule and any exceptions granted
- Pricing changes (rate adjustments, fee schedule changes) and their timing

### Step 5: Summarize Dispute History

For accounts with Reg E or Reg CC disputes:

| Dispute # | Date Filed | Type | Amount | Provisional Credit | Final Resolution | Timeline Compliance |
|-----------|-----------|------|--------|--------------------|--------------------|---------------------|
| [#] | [Date] | [Type] | [$Amount] | [Date/Amount] | [Outcome] | [Yes/No] |

Document Reg E compliance:
- Was provisional credit issued within 10 business days (20 for new accounts)?
- Was the investigation completed within 45 days (90 for certain transactions)?
- Was the customer notified of the outcome in writing within 3 business days?
- If provisional credit was reversed, was proper notice given?

### Step 6: Calculate Relationship Economics

Assess the account's financial contribution:

| Metric | Value | Benchmark |
|--------|-------|-----------|
| Average monthly balance | [$X] | [$X peer average] |
| Net interest margin contribution | [$X/year] | |
| Fee revenue (gross) | [$X/year] | |
| Fee waivers/reversals | -[$X/year] | |
| Service cost (estimated) | -[$X/year] | |
| Net relationship value | [$X/year] | |
| Lifetime value (total) | [$X] | |

### Step 7: Produce the Narrative Summary

Synthesize all elements into a cohesive account story:

- Focus on material events and inflection points
- Highlight patterns and trends rather than exhaustive detail
- Note regulatory compliance touchpoints (Reg E, Reg CC, UDAAP)
- Identify lessons learned for process improvement
- Recommend follow-up actions if the account is still active

## Output Specification

```markdown
# Account Lifecycle Summary: [Account Number (masked)]

## Account Profile
- **Account Type**: [Product name]
- **Open Date**: [Date]
- **Close Date**: [Date or "Active"]
- **Ownership**: [Individual/Joint/Business]
- **Opening Channel**: [Channel]
- **Relationship Tenure**: [Duration]

## Lifecycle Timeline
### Onboarding ([Date range])
[Narrative summary of opening and initial usage]

### Active Period ([Date range])
[Key activity patterns, product changes, milestone events]

### [Distress/Closure Period] ([Date range])
[Decline indicators, closure circumstances, final disposition]

## Key Metrics
| Metric | Value |
|--------|-------|
| Peak balance | [$X] |
| Average balance (lifetime) | [$X] |
| Total transactions | [N] |
| Total fees assessed | [$X] |
| Total fees waived/reversed | [$X] |
| Service interactions | [N] |
| Disputes filed | [N] |

## Service History Summary
[Interaction analysis with sentiment trajectory]

## Dispute History
[Dispute details with Reg E compliance assessment]

## Relationship Economics
[Financial contribution analysis]

## Key Observations
- [Material finding 1]
- [Material finding 2]
- [Material finding 3]

## Recommendations
- [Recommendation based on account analysis]
```

## Analysis Framework

### Attrition Risk Indicators

When analyzing active accounts for retention:
- Balance decline >25% over 3 consecutive months
- Direct deposit removal or reduction
- Debit card usage decline >50%
- Multiple fee complaints in 90-day window
- Digital banking login frequency drop >40%
- Competitor ACH credits appearing (new account funding elsewhere)

### Complaint Pattern Analysis

Categorize complaints for systemic identification:
- Product-related (fee disputes, feature limitations)
- Service-related (wait times, resolution quality, channel access)
- Error-related (posting errors, system issues, misapplied payments)
- Policy-related (hold policies, overdraft practices, closure policies)

## Examples

**Example 1 — Closed Account Summary**:
"Account #XXXX4477 (Premium Checking) was opened 2022-06-15 at the Main Street branch with an initial deposit of $5,000 via cashier's check. Direct deposit of $6,200/month was established within 30 days, waiving the $25 monthly maintenance fee. The account maintained an average balance of $8,400 through Q2 2024. Beginning July 2024, the balance declined to $2,100 as the customer's direct deposit shifted to a competitor. Seven overdraft fees ($35 each, $245 total) were assessed in Q4 2024; four were reversed following customer calls. The customer filed a complaint on 01/10/2025 regarding overdraft practices, which was escalated to the branch manager. The account was closed customer-initiated on 01/22/2025 with a final balance of $847 disbursed by official check. Lifetime relationship value: $1,840 in net revenue over 31 months."

**Example 2 — Regulatory Response Summary**:
"Per CFPB inquiry #2025-XXXX, the following account history is provided for account #XXXX8893 (consumer checking, individual ownership). The account was opened 2023-01-09 via online application. Consumer filed a Reg E dispute on 2024-11-15 for an unauthorized ACH debit of $1,200.00. Provisional credit of $1,200.00 was issued on 2024-11-19 (business day 2, within 10-business-day requirement). Investigation completed 2024-12-20 (business day 25, within 45-calendar-day requirement). Finding: claim denied, unauthorized transaction not substantiated based on IP address and device matching customer's enrolled device. Provisional credit reversed 2024-12-23 with written notice mailed 2024-12-20 (within 3-business-day requirement). All Reg E timeline requirements were satisfied."

## Guidelines

- Mask account numbers in all output (show last 4 digits only)
- Include only information relevant to the stated purpose of the summary
- For legal/regulatory requests, adhere strictly to the scope of the request
- Document Reg E and Reg CC compliance at each applicable touchpoint
- Present financial data in consistent units and time periods
- Distinguish between customer-stated reasons and bank-documented reasons for events
- Note any UDAAP concerns identified during the review (unfair, deceptive, abusive acts)
- Maintain chronological accuracy; verify dates against source systems
- Include both positive and negative aspects of the relationship for objectivity
- Preserve confidentiality; summaries may contain sensitive personal financial information

## Validation Checklist

- [ ] Account profile data matches core system of record
- [ ] Timeline covers all material events from opening through current status
- [ ] Service interaction history includes all channels (branch, digital, phone)
- [ ] Fee history is complete with assessments, waivers, and reversals
- [ ] Dispute history includes Reg E compliance assessment for each claim
- [ ] Relationship economics are calculated with stated methodology
- [ ] Key observations identify actionable insights
- [ ] Account numbers and sensitive data are appropriately masked
- [ ] Narrative is objective and fact-based without editorializing
- [ ] Summary scope matches the stated purpose and any regulatory request parameters
