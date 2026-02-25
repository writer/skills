---
name: sanctions-screening-review
description: Review and explain sanctions screening results, OFAC match dispositions, and sanctions compliance decisions. Use when analyzing sanctions screening hits, documenting true match vs. false positive determinations, assessing sanctions risk for customers or transactions, or supporting OFAC compliance program requirements.

metadata:
  display_name: "Sanctions Screening Review"
  short_description: "Review OFAC sanctions screening hits and match decisions"
  default_prompt: "Check my sanctions screening for gaps risks and required fixes"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Sanctions Screening Review

## Overview

This skill produces structured reviews of sanctions screening results for OFAC, EU, UN, and other sanctions programs. It covers SDN (Specially Designated Nationals) list screening, sectoral sanctions (SSI), correspondent and payable-through account sanctions (CAPTA), secondary sanctions exposure, and country-based sanctions programs. Output supports compliance analysts in documenting screening dispositions and sanctions risk assessments.

## When to Use

- Reviewing sanctions screening hits and determining true match vs. false positive
- Documenting OFAC screening disposition rationale for audit trail
- Assessing sanctions risk for new customer onboarding or transaction processing
- Analyzing potential sanctions exposure in correspondent banking relationships
- Reviewing trade finance transactions for sanctions compliance
- Preparing OFAC voluntary self-disclosure (VSD) narratives
- Supporting sanctions compliance program assessments and examinations

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Screening hit details | Match score, matched list entry, matching fields | Screening system output |
| Customer/transaction data | Name, address, nationality, counterparties | KYC/transaction record |
| Sanctions list reference | SDN, SSI, CAPTA, 561, EU Consolidated, UN | List identification |
| Screening system | Vendor, algorithm type, threshold settings | System documentation |
| Prior screening history | Previous hits, dispositions, escalations | Case history |
| Transaction context | Product type, currency, routing, purpose | Transaction details |

## Methodology

### Step 1: Identify the Sanctions Program

Map the screening hit to the applicable sanctions program:

| Program | Authority | Scope | Blocking vs. Restrictions |
|---------|-----------|-------|--------------------------|
| **SDN List** | OFAC (31 CFR 501) | Named individuals and entities | Full blocking; reject and freeze |
| **Sectoral Sanctions (SSI)** | OFAC Directives 1-4 | Russian energy, financial, defense sectors | Transaction restrictions (not full block) |
| **CAPTA (Correspondent)** | OFAC | Foreign FIs (e.g., Venezuela, Iran) | Correspondent account prohibitions |
| **Country programs** | OFAC | Cuba, Iran, North Korea, Syria, Crimea | Comprehensive embargoes |
| **EU Consolidated** | EU Council | EU-designated persons and entities | Asset freeze, travel ban |
| **UN Sanctions** | UN Security Council | UNSC-designated persons and entities | Asset freeze, arms embargo |
| **Secondary sanctions** | OFAC (CAATSA, IFCA) | Non-US persons transacting with targets | Risk of losing US access |

### Step 2: Analyze the Screening Match

Evaluate the match quality using structured comparison:

| Field | Screened Party | List Entry | Match Quality |
|-------|---------------|------------|---------------|
| Name | [Customer name] | [SDN name] | [Exact/Partial/Phonetic/Weak] |
| AKA/aliases | [Known aliases] | [Listed aliases] | [Match assessment] |
| DOB | [Customer DOB] | [Listed DOB] | [Match/No match/Not available] |
| Nationality | [Customer nationality] | [Listed nationality] | [Match/No match] |
| Address | [Customer address] | [Listed address] | [Match/Partial/No match] |
| ID numbers | [Passport, SSN, etc.] | [Listed IDs] | [Match/No match] |
| Vessel/aircraft | [If applicable] | [Listed vessel] | [Match assessment] |

**Match scoring framework**:
- **Strong match (>85%)**: Multiple field matches including name + at least one identifier; escalate to compliance officer
- **Moderate match (60-85%)**: Name match with some corroborating fields; requires detailed analysis
- **Weak match (<60%)**: Name-only similarity with no corroborating identifiers; likely false positive
- **Exact match (100%)**: All available fields match; immediate escalation and blocking action

### Step 3: Perform Enhanced Due Diligence on Hits

For moderate and strong matches, conduct additional analysis:

1. **Name analysis**: Assess linguistic variations, transliteration differences, common name frequency
2. **Geographic analysis**: Compare customer jurisdiction to sanctions program geography
3. **Temporal analysis**: Check SDN list entry date vs. customer relationship start
4. **Network analysis**: Screen associated parties (beneficial owners, directors, counterparties)
5. **50% Rule application**: Assess whether entities are 50%+ owned by blocked persons (even if not individually listed)
6. **Public source verification**: Check OFAC website, OFAC search tool, Treasury press releases, court records

### Step 4: Apply the OFAC 50% Rule

Determine if the 50% Rule creates blocking obligations:

- Any entity owned 50% or more, directly or indirectly, by one or more blocked persons is itself considered blocked
- Aggregate ownership: if two blocked persons each own 25% = 50% blocked
- Indirect ownership: trace through ownership chains to identify blocked ownership at any level
- Document the ownership analysis with percentage calculations

### Step 5: Determine Disposition

Apply one of these disposition categories:

| Disposition | Criteria | Action | Documentation |
|-------------|----------|--------|---------------|
| **True positive — Block** | Confirmed match to blocked person/entity | Reject/freeze, file blocking report within 10 days | Full match analysis, blocking report |
| **True positive — Reject** | Match to sanctions program prohibition | Reject transaction, do not process | Match documentation, rejection notice |
| **False positive** | Name similarity only; identifiers do not match | Release with documented rationale | Detailed field-by-field comparison |
| **Escalate** | Insufficient information to determine | Hold pending additional research | Analysis completed to date, open questions |
| **License/exemption** | Match confirmed but OFAC license applies | Process per license terms | License number, scope, expiration |

### Step 6: Document the Decision

Record all elements required for a defensible audit trail:

- Analyst name and date of review
- Screening system, algorithm, and threshold used
- Complete field-by-field comparison table
- Sources consulted (OFAC search tool, public records, KYC file)
- Rationale for disposition with specific factual basis
- Supervisor review and approval (for true positives and escalations)
- OFAC reporting actions taken (blocking report, voluntary self-disclosure)

### Step 7: Assess Systemic Sanctions Risk

Beyond individual hit resolution, evaluate:
- Screening system effectiveness (false positive rate, miss rate from testing)
- Coverage gaps (are all required lists included? Are updates timely?)
- High-risk products and services requiring enhanced screening (trade finance, correspondent banking, wire transfers)
- Sanctions risk in the institution's geographic and customer footprint
- OFAC enforcement trends and risk appetite calibration

## Output Specification

```markdown
# Sanctions Screening Review: [Case ID]

## Screening Details
- **Case ID**: [ID]
- **Screening Date**: [Date]
- **Screening System**: [Vendor/system name]
- **Match Score**: [Score/percentage]
- **Matched List**: [SDN/SSI/EU/UN]
- **List Entry ID**: [OFAC/list entry number]

## Match Analysis
| Field | Screened Party | List Entry | Match Quality |
|-------|---------------|------------|---------------|
| Full Name | [Value] | [Value] | [Assessment] |
| DOB | [Value] | [Value] | [Assessment] |
| Nationality | [Value] | [Value] | [Assessment] |
| Address | [Value] | [Value] | [Assessment] |
| ID Number | [Value] | [Value] | [Assessment] |

## 50% Rule Assessment
- **Applicable**: [Yes/No]
- **Analysis**: [Ownership chain documentation if applicable]

## Disposition
- **Decision**: [True Positive — Block / True Positive — Reject / False Positive / Escalate]
- **Rationale**: [Specific factual basis for decision]
- **Reviewer**: [Analyst name]
- **Approver**: [Supervisor name, if required]
- **Date**: [Decision date]

## Regulatory Actions
- **Blocking Report Filed**: [Yes/No, date if yes]
- **VSD Filed**: [Yes/No, if applicable]
- **SAR Filed**: [Yes/No, if applicable]

## Follow-Up Actions
- [Actions required, including ongoing monitoring adjustments]
```

## Analysis Framework

### Name Matching Linguistics

Common sources of false positives requiring linguistic expertise:
- **Arabic names**: Transliteration variations (Mohammed/Muhammad/Mohamed), patronymic vs. family name
- **Chinese names**: Pinyin romanization variations, surname/given name order reversal
- **Russian names**: Cyrillic transliteration variants, patronymic middle names
- **Hispanic names**: Dual surname conventions, maternal vs. paternal surname usage
- **Common names**: Frequency analysis (how common is this name in the relevant population?)

### Trade Finance Sanctions Screening

Additional screening points for trade finance:
- All parties to the letter of credit (applicant, beneficiary, advising bank, confirming bank)
- Vessel name, IMO number, and flag state against OFAC vessel lists
- Port of loading and discharge against sanctioned jurisdictions
- Goods description against sanctioned commodities (luxury goods, dual-use items)
- Insurance and reinsurance parties

### Correspondent Banking Sanctions Risk

For correspondent banking relationships:
- Screen the respondent bank and its ownership against all applicable lists
- Assess the respondent's own sanctions compliance program
- Evaluate nested correspondent risk (respondent's downstream correspondents)
- Monitor for payable-through account activity from sanctioned jurisdictions
- Apply CAPTA restrictions where applicable

## Examples

**Example 1 — False Positive Resolution**:
"Screening hit SC-20251015-4472: Customer 'Ahmad Hassan Al-Rashid' (US citizen, DOB 1985-03-22, SSN XXX-XX-4521, Chicago, IL) matched SDN entry 'Ahmed Hassan AL-RASHIDI' (Iraqi national, DOB 1967-09-14, Baghdad, Iraq, SDN ID 12847). Analysis: Name similarity is phonetic (Arabic transliteration variant), but DOB differs by 18 years, nationality differs (US vs. Iraqi), and no geographic nexus to Iraq. SSN confirms US citizenship. No corroborating identifiers match. Disposition: False positive. Name similarity is attributable to common Arabic naming conventions. Released with documented analysis."

**Example 2 — True Positive Blocking**:
"Screening hit SC-20251020-5891: Incoming wire $250,000 from 'Petrov Energy Trading Ltd' (Cyprus) to correspondent account. Match to SSI List: 'Petrov Energy Trading Limited' (Directive 4, energy sector, Russia-related). Analysis: Exact name match, matching Cyprus registration jurisdiction (known Russian corporate structure), and beneficial owner Alexei Petrov matches SDN entry #29847. 50% Rule analysis confirms Petrov holds 72% equity. Disposition: True positive. Transaction rejected, funds returned to originating bank with sanctions rejection code. Blocking report filed with OFAC within 10 business days. Correspondent bank notified of sanctions concern."

## Guidelines

- Process all sanctions screening hits within 24 hours; blocking decisions are time-critical
- Never tip off the customer about a potential sanctions match during investigation
- Apply the 50% Rule to all entities, even those not individually listed
- Keep sanctions lists updated in real-time or at minimum within 24 hours of OFAC publication
- Document negative screening results (no match) as well as positive hits
- For rejected transactions, use appropriate rejection codes per payment network rules
- Voluntary self-disclosure to OFAC should be made promptly for apparent violations
- Maintain screening records for 5 years per BSA recordkeeping requirements
- Train all staff in sanctions red flags, not just compliance analysts
- When in doubt, block first and investigate; releasing a blocked transaction is preferable to processing a prohibited one

## Validation Checklist

- [ ] Applicable sanctions program(s) are identified (OFAC, EU, UN)
- [ ] Field-by-field match comparison is completed and documented
- [ ] 50% Rule ownership analysis is performed where applicable
- [ ] Disposition category is assigned with specific factual rationale
- [ ] Linguistic and cultural naming considerations are addressed for false positives
- [ ] OFAC blocking report is filed within 10 business days for true positives
- [ ] Supervisor review and approval is obtained for true positive and escalation dispositions
- [ ] Follow-up actions (SAR, account restriction, enhanced monitoring) are specified
- [ ] Documentation is sufficient for OFAC examination review
- [ ] Screening system parameters (lists, threshold, update frequency) are documented
