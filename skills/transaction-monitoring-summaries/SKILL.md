---
name: transaction-monitoring-summaries
description: Generate AML/BSA transaction monitoring alert summaries and suspicious activity explanations. Use when reviewing transaction monitoring alerts, drafting SAR narratives, explaining unusual activity patterns, or supporting BSA/AML compliance investigations under FinCEN and OCC requirements.

metadata:
  display_name: "Transaction Monitoring Summaries"
  short_description: "Summarize AML/BSA transaction monitoring alerts and SARs"
  default_prompt: "Review my aml bsa transaction alerts and sars and highlight top risks and next actions"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Transaction Monitoring Summaries

## Overview

This skill produces structured, investigation-ready summaries of transaction monitoring alerts for BSA/AML compliance. It covers alert disposition narratives, pattern-of-activity analysis, SAR narrative drafting support, and escalation recommendations aligned with FinCEN guidance, FFIEC BSA/AML Examination Manual, and OCC supervisory expectations.

## When to Use

- Summarizing transaction monitoring system alerts for analyst review
- Explaining why a set of transactions triggered a detection scenario
- Drafting or reviewing SAR (Suspicious Activity Report) narrative sections
- Documenting alert disposition decisions (file, escalate, or close)
- Identifying activity patterns across related accounts or entities
- Supporting look-back reviews and 314(b) information-sharing requests
- Preparing case summaries for BSA Officer review

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Alert details | Scenario triggered, score, alert ID | System export or summary |
| Transaction data | Amounts, dates, counterparties, channels | Transaction listing |
| Customer profile | KYC data, account type, expected activity | CIF/CDD record |
| Prior alert history | Previous alerts, SARs, case dispositions | Case management data |
| Scenario threshold | Rule parameters that triggered the alert | Scenario documentation |
| Investigation notes | Analyst observations, outreach results | Free text |

## Methodology

### Step 1: Contextualize the Alert

Establish the foundation for analysis:
- Identify the detection scenario (e.g., structuring, rapid movement, geographic risk, third-party funders)
- Document the specific threshold breached (e.g., "aggregate cash deposits of $28,400 across 4 branches in 3 business days vs. $10,000 CTR threshold")
- Pull the customer's KYC profile: occupation, expected income range, account purpose, risk rating
- Retrieve alert and SAR filing history for the customer and related parties

### Step 2: Analyze Transaction Patterns

Examine the flagged activity against BSA/AML red flag indicators:

**Structuring indicators**: Transactions just below CTR threshold ($10,000), round-dollar amounts, multiple branches/ATMs, compressed timeframes
**Rapid movement**: Funds in and out within 24-72 hours with no apparent business purpose
**Geographic risk**: Transactions involving FATF high-risk jurisdictions, OFAC-sanctioned regions, or known narcotics corridors
**Third-party activity**: Deposits or wires from unrelated parties, nominee account patterns
**Shell company indicators**: Newly formed entity, nominal capitalization, no web presence, mismatched business type and transaction profile
**Funnel account patterns**: Multiple incoming transfers aggregated and sent to single beneficiary

### Step 3: Assess Against Expected Activity

Compare flagged transactions to the customer's established baseline:
- Historical average transaction volume and value (prior 12 months)
- Stated occupation and income reasonableness
- Account opening purpose and product type alignment
- Peer group comparison (similar account types, demographics)
- Seasonal patterns and known legitimate spikes

### Step 4: Determine Suspicion Level

Apply the three-tier assessment framework:

| Level | Criteria | Disposition |
|-------|----------|-------------|
| **No suspicion** | Activity consistent with customer profile, legitimate explanation confirmed | Close alert with documented rationale |
| **Unusual but explained** | Activity deviates from baseline but has plausible explanation | Document explanation, enhance monitoring, close |
| **Suspicious** | Activity inconsistent with profile, no legitimate explanation, matches typology | Escalate for SAR filing consideration |

### Step 5: Draft the Summary Narrative

Structure the narrative following FinCEN SAR filing guidance (five W's):

1. **Who**: Subject identification (name, account numbers, roles, relationships)
2. **What**: Description of suspicious activity with specific transaction details
3. **When**: Date range of activity with key dates highlighted
4. **Where**: Channels, branches, jurisdictions involved
5. **Why**: Explanation of why the activity is suspicious, referencing specific red flags and typology alignment

### Step 6: Document Disposition and Next Steps

Record the investigation outcome with required elements:
- Clear disposition decision with regulatory basis
- Supporting evidence cited (transaction records, public records, customer outreach)
- Enhanced due diligence actions taken or recommended
- Follow-up SAR filing timeline (if applicable, initial filing within 30 days)
- Continuing activity review schedule (90-day follow-up SAR assessment)

### Step 7: Quality Assurance Review

Validate the summary against BSA program requirements:
- Ensure narrative stands alone without requiring reference to attachments
- Verify all transaction amounts, dates, and counterparties are accurate
- Confirm customer identification information is complete
- Check that the disposition is consistent with similar prior cases
- Validate that SAR-reportable activity is not inadvertently closed

## Output Specification

```markdown
# Transaction Monitoring Alert Summary

## Alert Information
- **Alert ID**: [ID]
- **Scenario**: [Detection scenario name and code]
- **Score/Priority**: [Risk score and priority tier]
- **Alert Date**: [Date generated]
- **Review Period**: [Transaction date range]

## Subject Information
- **Customer Name**: [Name]
- **Account(s)**: [Account numbers and types]
- **Customer Risk Rating**: [Rating]
- **Relationship Tenure**: [Duration]
- **Prior Alerts/SARs**: [Count and summary]

## Activity Summary
| Date | Transaction Type | Amount | Channel | Counterparty | Red Flag |
|------|-----------------|--------|---------|--------------|----------|
| [Date] | [Type] | [$Amount] | [Channel] | [Party] | [Flag] |

**Total Flagged Activity**: [$Amount] across [N] transactions

## Analysis
### Pattern Identified
[Description of the activity pattern and why it triggered the alert]

### Comparison to Expected Activity
[How flagged activity compares to customer baseline and peer group]

### Red Flags Identified
- [Red flag 1 with specific evidence]
- [Red flag 2 with specific evidence]

## Disposition
- **Decision**: [Close / Escalate / SAR Filing]
- **Rationale**: [Specific basis for disposition]
- **Follow-up Actions**: [Enhanced monitoring, account restrictions, etc.]
```

## Analysis Framework

### Structuring Detection

Evaluate potential structuring using these quantitative tests:
- Individual transactions between $3,000-$9,999 (cash) with aggregate above $10,000
- Multiple transactions at different branches or ATMs within same business day
- Pattern breaks: customer historically makes single large deposits but shifts to multiple smaller ones
- Round-dollar or just-below-threshold amounts ($9,900, $9,500, $5,000)

### Network Analysis

When multiple subjects are involved:
- Map fund flows between accounts (source → intermediary → destination)
- Identify common addresses, phone numbers, employers, or IP addresses
- Calculate velocity metrics (how quickly funds transit through accounts)
- Flag accounts opened within 30 days of each other with similar profiles

### Typology Matching

Compare activity against FinCEN advisories and known typologies:
- FIN-2021-A003 (ransomware), FIN-2020-A005 (COVID fraud)
- Trade-based money laundering (TBML) invoice patterns
- Funnel account / money mule patterns
- Professional money laundering network indicators

## Examples

**Example 1 — Structuring Alert Summary**:
"Customer John Doe (Acct #XXXX4521, personal checking) triggered Scenario SC-003 (Cash Structuring) on 2025-09-15. Between 09/10 and 09/14, five cash deposits totaling $47,200 were made across three branches (Main: $9,800 + $9,500; Elm St: $9,900 + $9,000; Oak Ave: $9,000). All deposits occurred between 11am-2pm. Customer's stated occupation is retired schoolteacher with monthly Social Security income of $2,400. No prior commercial activity. Two prior structuring alerts in 2024 were closed as inconclusive. The compressed timeframe, multi-branch pattern, just-below-threshold amounts, and activity inconsistent with stated income collectively indicate potential structuring to evade CTR filing. Recommend escalation for SAR filing."

**Example 2 — Rapid Movement Alert**:
"Business account for ABC Consulting LLC (Acct #XXXX7893) triggered Scenario RM-012 (Rapid Movement of Funds). On 2025-08-20, an incoming wire of $185,000 from an offshore entity (XYZ Holdings, Cayman Islands) was received and, within 4 hours, $180,000 was wired to three domestic entities with no apparent relationship to consulting services. The LLC was incorporated 45 days ago with a registered agent; no web presence or business filings found. CDD file shows expected annual revenue of $50,000. Activity is inconsistent with stated business purpose and matches FinCEN shell company typology. Recommend SAR filing and account restriction pending enhanced review."

## Guidelines

- Never disclose the existence of a SAR or SAR filing to the subject (31 USC 5318(g)(2))
- Do not reference specific detection scenarios or thresholds in SAR narratives
- Use objective, factual language; avoid conclusory terms like "laundering" or "criminal"
- State that activity is "suspicious" or "unusual" rather than making legal determinations
- Include all material transactions, not just those above threshold
- Cross-reference OFAC SDN and 314(a) lists for all subjects and counterparties
- Document the absence of suspicious indicators when closing alerts (negative findings matter)
- Maintain audit trail of all investigative steps taken
- SAR narrative must be self-contained; examiners should understand without attachments

## Validation Checklist

- [ ] Alert scenario and threshold breach are specifically identified
- [ ] All five W's (who, what, when, where, why) are addressed in the narrative
- [ ] Transaction details include dates, amounts, types, and counterparties
- [ ] Customer profile and expected activity baseline are documented
- [ ] Red flags are individually identified with supporting evidence
- [ ] Disposition decision has clear, documented rationale
- [ ] Prior alert and SAR history is referenced
- [ ] No tipping-off language or scenario-specific thresholds disclosed
- [ ] Narrative uses objective, factual language throughout
- [ ] Follow-up actions and timeline are specified
