---
name: kyc-completeness-validator
description: Validate KYC/CDD documentation completeness and identify gaps in customer due diligence files. Use when reviewing customer onboarding packages, assessing CDD/EDD requirements, validating beneficial ownership under CDD Rule, or preparing for BSA/AML examinations requiring documentation compliance.

metadata:
  display_name: "Kyc Completeness Validator"
  short_description: "Validate KYC/CDD documentation completeness and gaps"
  default_prompt: "Check my kyc completeness for gaps risks and required fixes"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# KYC Completeness Validator

## Overview

This skill systematically validates Know Your Customer (KYC) and Customer Due Diligence (CDD) documentation against regulatory requirements. It covers CIP (Customer Identification Program) under USA PATRIOT Act Section 326, the FinCEN CDD Rule (31 CFR 1010.230), Enhanced Due Diligence (EDD) for high-risk customers, and beneficial ownership certification. The output is a gap analysis with remediation priorities.

## When to Use

- Validating new account onboarding packages for regulatory completeness
- Conducting periodic KYC refresh reviews (risk-based, typically 1-3 year cycle)
- Preparing for BSA/AML regulatory examinations
- Assessing CDD/EDD documentation for risk-rated customers
- Validating beneficial ownership certifications for legal entity customers
- Reviewing remediation queues during look-back exercises
- Supporting merger/acquisition due diligence on acquired customer portfolios

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Customer type | Individual, legal entity, trust, correspondent bank | Classification |
| Risk rating | Low, medium, high, or prohibited | Risk tier |
| CIF/KYC record | Current documentation on file | System extract |
| Entity formation docs | Articles, operating agreements, trust instruments | Document inventory |
| Beneficial ownership cert | FinCEN beneficial ownership form | Certification record |
| Screening results | OFAC, PEP, adverse media, 314(a) | Screening output |
| Account products | Products and services utilized | Product listing |
| Jurisdiction | Customer domicile and transaction jurisdictions | Country/state |

## Methodology

### Step 1: Determine the CDD Tier

Classify the customer into the appropriate due diligence tier:

| Tier | Criteria | Documentation Standard |
|------|----------|----------------------|
| **Standard CDD** | Low/medium-risk individuals and entities | CIP minimums + CDD Rule requirements |
| **Enhanced (EDD)** | High-risk customers, PEPs, high-risk jurisdictions, MSBs, correspondent banks | Standard + additional EDD elements |
| **Simplified** | Low-risk, well-known entities (publicly traded, regulated FIs) | Streamlined with documented rationale |
| **Prohibited** | OFAC-blocked, terminated for cause | No account opening; document rejection |

### Step 2: Validate CIP Requirements (Section 326)

Check the four minimum CIP data elements for individuals:

| Element | Individual | Legal Entity | Verified? |
|---------|-----------|--------------|-----------|
| **Name** | Full legal name | Legal entity name | [ ] |
| **Date of birth** | DOB | Formation date | [ ] |
| **Address** | Residential or business | Principal place of business | [ ] |
| **Identification number** | SSN or passport + country | EIN or equivalent | [ ] |

Verify the identity verification method:
- **Documentary**: Unexpired government-issued photo ID (driver's license, passport, state ID)
- **Non-documentary**: Credit bureau, public database, financial reference
- **Combination**: Both methods for higher confidence or when single method is insufficient
- Document any exceptions or alternative verification methods with supervisory approval

### Step 3: Validate CDD Rule Requirements (31 CFR 1010.230)

For legal entity customers, verify the four CDD pillars:

1. **Customer identification and verification** (CIP — Step 2 above)
2. **Beneficial ownership identification**: Each individual owning 25%+ equity AND one individual with significant management control
3. **Understanding the nature and purpose of the relationship**: Business type, expected products, anticipated activity
4. **Ongoing monitoring**: Transaction monitoring enrollment, periodic review schedule

**Beneficial Ownership Certification checklist**:
- [ ] Certification form on file (FinCEN standard or equivalent)
- [ ] All 25%+ equity owners identified with name, DOB, address, SSN/passport
- [ ] One control person identified (CEO, CFO, managing member, GP, or equivalent)
- [ ] Ownership percentages total to at least 75% or exclusion documented
- [ ] Identity verification performed on each beneficial owner
- [ ] Certification signed and dated by authorized representative
- [ ] Exemptions properly documented (publicly traded, regulated FI, etc.)

### Step 4: Assess Enhanced Due Diligence Requirements

For high-risk customers, validate additional EDD elements:

| EDD Element | Requirement | Status |
|-------------|-------------|--------|
| Source of wealth | Documented origin of customer's assets | [ ] |
| Source of funds | Documented origin of specific transaction funds | [ ] |
| Purpose of account | Detailed description beyond standard CDD | [ ] |
| Expected activity profile | Quantified: monthly volume, transaction types, counterparties | [ ] |
| Senior management approval | Documented approval for relationship | [ ] |
| Enhanced monitoring | Elevated monitoring parameters applied | [ ] |
| PEP screening | Screening against PEP databases with results documented | [ ] |
| Adverse media | Negative news search with results documented | [ ] |
| Country risk assessment | FATF, Transparency International CPI, US State Dept evaluation | [ ] |

### Step 5: Validate Screening Completeness

Verify all required screening has been performed:
- **OFAC SDN List**: Screened at onboarding and ongoing (real-time or daily batch)
- **OFAC Consolidated Sanctions**: Non-SDN lists (sectoral sanctions, correspondent account sanctions)
- **314(a) requests**: Process for matching against FinCEN 314(a) subjects
- **PEP databases**: Domestic and foreign PEP screening
- **Adverse media**: Negative news screening with defined search parameters
- **Internal watchlists**: Terminated-for-cause list, prior SAR subjects

Document the screening date, source, and results (positive match, false positive resolved, or no match).

### Step 6: Perform Gap Analysis

For each requirement, assign a status:

| Status | Definition | Action Required |
|--------|------------|-----------------|
| **Complete** | Documentation meets all requirements | None |
| **Partial** | Some elements present, gaps identified | Remediation within 30 days |
| **Missing** | Required documentation absent | Immediate remediation or account restriction |
| **Expired** | Documentation beyond refresh cycle | Refresh within policy timeframe |
| **Exempt** | Requirement not applicable with documented basis | Document exemption rationale |

Prioritize gaps by regulatory risk:
1. **Critical**: Missing CIP, absent beneficial ownership, unscreened against OFAC
2. **High**: Incomplete EDD for high-risk customers, expired documentation
3. **Medium**: Missing source-of-wealth documentation, incomplete activity profile
4. **Low**: Administrative gaps (unsigned forms, missing copies of verified documents)

### Step 7: Generate Remediation Plan

For each identified gap, prescribe:
- Specific document or information required
- Responsible party (relationship manager, operations, compliance)
- Deadline based on risk severity (critical: 5 business days, high: 15, medium: 30, low: 60)
- Escalation path if deadline is missed
- Account restriction recommendations for unresolved critical gaps

## Output Specification

```markdown
# KYC Completeness Assessment: [Customer Name]

## Customer Profile
- **Customer ID**: [CIF number]
- **Customer Type**: [Individual / Legal Entity / Trust]
- **Risk Rating**: [Low / Medium / High]
- **Relationship Start Date**: [Date]
- **Last KYC Refresh**: [Date]
- **Next Scheduled Refresh**: [Date]

## Compliance Summary
| Category | Status | Gaps Found |
|----------|--------|------------|
| CIP (Section 326) | [Complete/Gaps] | [Count] |
| CDD Rule | [Complete/Gaps] | [Count] |
| Beneficial Ownership | [Complete/Gaps/N/A] | [Count] |
| EDD (if applicable) | [Complete/Gaps/N/A] | [Count] |
| Screening | [Complete/Gaps] | [Count] |

**Overall Completeness Score**: [X/Y required elements satisfied] ([percentage]%)

## Gap Details
| # | Category | Element | Status | Priority | Remediation |
|---|----------|---------|--------|----------|-------------|
| 1 | [Cat] | [Element] | [Status] | [Critical/High/Med/Low] | [Action required] |

## Remediation Plan
| # | Action | Owner | Deadline | Escalation |
|---|--------|-------|----------|------------|
| 1 | [Action] | [Role] | [Date] | [Path] |

## Examiner Readiness Assessment
[Summary of documentation's readiness for regulatory examination]
```

## Analysis Framework

### Legal Entity Complexity Assessment

For complex ownership structures, trace the ownership chain:
- Direct ownership: Entity → 25%+ individual owners
- Indirect ownership: Entity → intermediate entities → ultimate beneficial owners
- Multi-layered structures: Document each entity in the chain with formation jurisdiction
- Trust structures: Identify trustee, settlor, beneficiaries, and protector
- Nominee arrangements: Look through to beneficial owner

### Risk-Based Refresh Cycles

Apply differentiated refresh frequencies:
- **High risk**: Annual full refresh with EDD update
- **Medium risk**: Every 2 years with CDD confirmation
- **Low risk**: Every 3 years with CIP verification
- **Trigger events**: Risk rating change, SAR filing, adverse media, product change, material transaction anomaly

### Regulatory Examination Preparation

Pre-examination KYC file checklist (OCC/Fed expectations):
- CIP documentation with verification evidence
- CDD form with nature and purpose of relationship
- Beneficial ownership certification (legal entities opened after May 11, 2018)
- Risk rating with documented methodology and factors
- OFAC screening evidence with date stamps
- EDD file (if applicable) with senior management approval
- Ongoing monitoring evidence (alert history, periodic reviews)
- Account activity vs. expected profile comparison

## Examples

**Example 1 — Legal Entity Gap Identification**:
"KYC review of ABC Holdings LLC (CIF #88421, high-risk) identified 4 gaps: (1) Beneficial ownership certification lists two 30% owners but no control person is designated (Critical — CDD Rule violation); (2) Source of wealth documentation references 'investment income' without supporting evidence (High — EDD requirement); (3) OFAC screening was last performed 8 months ago with no evidence of ongoing screening enrollment (High — sanctions compliance gap); (4) Operating agreement on file is from 2019 initial formation; no amendment reflecting 2024 ownership change has been obtained (Medium — stale documentation). Remediation deadline: Items 1 and 3 within 5 business days; Items 2 and 4 within 30 days."

**Example 2 — Individual Account Refresh**:
"Periodic KYC refresh for John Martinez (CIF #45672, medium-risk, last refresh 2023-03-15) is due by 2025-03-15. Current file status: CIP elements complete (unexpired passport verified 2023); address confirmed via credit bureau 2023; SSN verified at account opening. Gaps: (1) Customer occupation updated to 'self-employed consultant' in CRM but no updated expected activity profile documenting anticipated transaction volume and types (Medium); (2) Adverse media screening not evidenced since 2023 refresh (Medium). No critical or high-priority gaps. File is substantially complete pending two medium-priority remediations."

## Guidelines

- Apply CDD Rule requirements to all legal entity accounts opened after May 11, 2018
- For accounts opened before the CDD Rule, apply beneficial ownership requirements at next trigger event
- Do not collect more information than the risk tier requires (avoid over-collection)
- Document the specific verification source for each CIP element
- For non-US persons, accept passport with country of issuance as identification number
- Maintain documentary evidence of all screening results, including "no match" results
- Apply consistent risk rating methodology across all customer types
- Flag any customer with connections to FATF high-risk jurisdictions for automatic EDD
- Exemptions from beneficial ownership (publicly traded, regulated FIs, etc.) must be individually documented

## Validation Checklist

- [ ] Customer type is correctly classified (individual, legal entity, trust)
- [ ] Risk rating is assigned and documented with supporting rationale
- [ ] All four CIP elements are verified with documentary or non-documentary evidence
- [ ] Beneficial ownership certification is complete for legal entities (25% equity + 1 control person)
- [ ] Nature and purpose of the customer relationship are documented
- [ ] OFAC and sanctions screening is current with evidence retained
- [ ] EDD elements are satisfied for high-risk customers
- [ ] Gap analysis assigns priority levels consistently based on regulatory risk
- [ ] Remediation plan includes specific actions, owners, and deadlines
- [ ] Assessment is ready for regulatory examination review
