---
name: third-party-risk-summaries
description: Generate vendor and third-party risk assessment summaries for financial institutions. Use when conducting third-party due diligence, preparing vendor risk assessments, evaluating critical vendor relationships, reviewing concentration risk across the vendor portfolio, or responding to OCC/Fed third-party risk management guidance (OCC 2023-17).

metadata:
  display_name: "Third Party Risk Summaries"
  short_description: "Summarize third-party vendor risk assessments for banks"
  default_prompt: "Summarize my third party risk with key findings and next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Third-Party Risk Assessment Summaries

## Overview

Generate comprehensive third-party risk assessment summaries aligned with OCC Bulletin 2023-17 (Third-Party Relationships: Risk Management Guidance), Federal Reserve SR 13-19, and FFIEC IT Examination Handbook. This skill supports the full third-party risk management lifecycle: planning, due diligence, contract negotiation support, ongoing monitoring, and termination assessment.

## When to Use

- Conducting initial due diligence on prospective third-party vendors
- Preparing periodic risk assessments for existing third-party relationships
- Evaluating whether a third-party relationship is critical per OCC 2023-17 criteria
- Analyzing concentration risk across the third-party portfolio
- Preparing board or committee reporting on third-party risk exposure
- Responding to regulatory findings on third-party risk management practices
- Assessing fourth-party (subcontractor) risk exposure through critical vendors

## Required Inputs

- **Vendor profile**: Name, services provided, contract terms, relationship tenure, financial data
- **Criticality assessment**: Business impact analysis, substitutability, customer data exposure
- **Due diligence materials**: SOC reports, financial statements, BCP documentation, information security assessments
- **Performance data**: SLA metrics, incident history, complaint volumes, audit findings
- **Regulatory context**: Applicable regulations, prior examination findings, consent orders
- **Contract terms**: Key provisions including termination rights, data handling, subcontracting

## Methodology

### Step 1: Criticality Determination

Classify the third-party relationship per OCC 2023-17 criteria for critical activities:

A third-party relationship involves a **critical activity** if it could:
- Cause a bank to face significant risk if the third party fails to meet expectations
- Have significant customer impacts
- Have a significant impact on the bank's financial condition or operations
- Involve critical bank functions (payments, clearing, settlements, custody)
- Involve significant shared bank or customer data

Apply a structured assessment:

| Criticality Factor | Assessment Criteria |
|-------------------|-------------------|
| Financial impact | Revenue dependency, loss exposure if disrupted |
| Operational impact | Process dependency, recovery time objectives |
| Customer impact | Customer data exposure, service delivery reliance |
| Regulatory impact | Regulated activity involvement, compliance obligations |
| Substitutability | Alternative provider availability, transition complexity |
| Data sensitivity | Volume and classification of data shared |

Classify as: **Critical** (enhanced due diligence required) or **Non-Critical** (standard due diligence).

### Step 2: Due Diligence Assessment

Evaluate the third party across required due diligence domains per OCC 2023-17:

- **Financial condition**: Analyze audited financial statements, credit ratings, going-concern indicators. Assess financial viability over the contract term.
- **Business experience and reputation**: Evaluate industry tenure, client references, regulatory history, litigation exposure, media and public reputation.
- **Information security**: Review SOC 2 Type II reports, penetration test results, vulnerability management programs, incident response capabilities, data encryption practices.
- **Operational resilience**: Assess BCP/DR plans, RTO/RPO commitments, geographic diversification, pandemic preparedness, testing frequency and results.
- **Compliance management**: Evaluate regulatory compliance programs, applicable licensing, AML/BSA controls (if applicable), consumer protection practices.
- **Human resources**: Assess training programs, background check practices, key-person dependencies, employee turnover in critical roles.
- **Subcontractor management**: Identify fourth-party dependencies, assess the vendor's subcontractor oversight program, evaluate concentration risk in the supply chain.

### Step 3: Risk Assessment and Scoring

Apply a multi-dimensional risk scoring model:

| Risk Domain | Weight | Assessment Areas |
|------------|--------|-----------------|
| Strategic risk | 15% | Alignment with bank strategy, market position, innovation capability |
| Operational risk | 25% | Service delivery, process maturity, incident history, resilience |
| Compliance risk | 20% | Regulatory adherence, licensing, consumer protection, change management |
| Information security risk | 20% | Data protection, access controls, vulnerability management, breach history |
| Financial/credit risk | 10% | Financial stability, concentration, pricing sustainability |
| Reputation risk | 10% | Public perception, litigation, regulatory actions, media exposure |

Score each domain: 1 (Low) to 4 (Critical). Weighted aggregate determines the overall risk rating.

### Step 4: Contract Risk Assessment

Evaluate key provisions: performance SLAs with remedies, audit and examination rights for bank and regulators, data ownership and return/destruction obligations, subcontracting approval and flow-down requirements, BCP/DR obligations and testing, termination provisions with transition assistance, insurance coverage (cyber, E&O, general liability), and indemnification commensurate with risk.

### Step 5: Ongoing Monitoring Framework Assessment

Evaluate: monitoring frequency commensurate with risk and criticality, KPIs/KRIs defined and reported to governance bodies, escalation triggers for performance deterioration and security incidents, annual due diligence refresh scheduled, and relationship manager accountability clearly defined.

### Step 6: Concentration and Portfolio Risk Analysis

Assess systemic portfolio risks: vendor concentration (single vendors across multiple services), geographic concentration (regional disaster/geopolitical exposure), technology concentration (shared platforms across vendors), fourth-party concentration (multiple vendors relying on same subcontractors like cloud providers), and revenue concentration (mutual dependency risk).

### Step 7: Summary Report Generation

Compile findings into a structured risk assessment summary suitable for committee review and regulatory examination.

## Output Specification

```markdown
# Third-Party Risk Assessment Summary

## Vendor Overview
| Field | Detail |
|-------|--------|
| Vendor Name | [name] |
| Services Provided | [description] |
| Contract Term | [start] - [end] |
| Annual Spend | [$amount] |
| Criticality Classification | [Critical / Non-Critical] |
| Overall Risk Rating | [Low / Moderate / High / Critical] |
| Relationship Manager | [name] |

## Executive Summary
[2-3 paragraphs summarizing the risk profile, key findings, and recommended actions]

## Criticality Assessment
[Detailed assessment against OCC 2023-17 critical activity criteria]

## Due Diligence Findings
### Financial Condition
[Analysis with supporting data]

### Information Security
[SOC report findings, security assessment results]

### Operational Resilience
[BCP/DR assessment, RTO/RPO evaluation]

### Compliance
[Regulatory compliance assessment, licensing verification]

### Subcontractor / Fourth-Party Risk
[Key dependencies, oversight assessment]

## Risk Scoring
| Risk Domain | Score (1-4) | Key Factors |
|------------|-------------|-------------|

## Contract Risk Assessment
[Key contractual provision evaluation]

## Monitoring Recommendations
[Frequency, KPIs, KRIs, escalation triggers]

## Concentration Risk Considerations
[Portfolio-level concentration analysis]

## Action Items
| Priority | Action | Owner | Due Date |
|----------|--------|-------|----------|

## Appendix
[Supporting documentation references, SOC report summary, financial ratio analysis]
```

## Analysis Framework

Third-party risk escalation matrix:

| Overall Risk Rating | Governance Requirements |
|---------------------|------------------------|
| Critical (3.5-4.0) | Board-level oversight, quarterly monitoring, enhanced due diligence, contingency planning |
| High (2.5-3.4) | Senior management oversight, semi-annual monitoring, annual due diligence refresh |
| Moderate (1.5-2.4) | Management oversight, annual monitoring, periodic due diligence refresh |
| Low (1.0-1.4) | Standard oversight, annual review, standard due diligence cycle |

## Examples

**Example 1 — Critical Vendor Assessment**:
"CoreBanking Solutions LLC provides the institution's core banking platform serving 1.2M customer accounts. The relationship is classified as Critical under OCC 2023-17 due to: (1) significant operational dependency with no viable short-term alternative, (2) access to all customer PII and financial data, (3) direct impact on regulatory reporting capabilities. The vendor's SOC 2 Type II report contained two exceptions related to access provisioning controls, and financial analysis indicates declining operating margins (18% to 12% over 3 years). Recommend: Enhanced quarterly monitoring, updated contingency/exit plan, and escalation of SOC exceptions to the Technology Risk Committee."

**Example 2 — Concentration Risk Finding**:
"Portfolio analysis reveals that Amazon Web Services (AWS) serves as the primary infrastructure provider for 7 of the institution's 12 critical vendors, representing a significant fourth-party concentration risk. A sustained AWS outage could simultaneously impact core banking, payments processing, fraud detection, and customer communications. Recommend: (1) Mandate multi-cloud resilience requirements for critical vendors, (2) Conduct a tabletop exercise simulating extended AWS outage, (3) Report fourth-party concentration to the Enterprise Risk Committee."

## Guidelines

- Apply due diligence rigor commensurate with the criticality classification and risk rating
- Consider the entire lifecycle: planning, due diligence, negotiation, ongoing monitoring, termination
- Assess risk from the institution's perspective, not solely based on vendor self-assessments
- Evaluate SOC reports critically; review complementary user entity controls and noted exceptions
- Consider the cumulative risk of the third-party portfolio, not just individual relationships
- Engage subject matter experts for specialized assessments (information security, legal, compliance)
- Document all assessments to support regulatory examination readiness
- Ensure board-level reporting includes critical vendor risk summaries and emerging concentration risks

## Validation Checklist

- [ ] Criticality classification completed using OCC 2023-17 criteria
- [ ] All due diligence domains assessed with supporting evidence
- [ ] Risk scoring applied consistently; SOC reports reviewed with exceptions tracked
- [ ] Financial viability assessed with quantitative ratio analysis
- [ ] Contract provisions evaluated against regulatory expectations
- [ ] Fourth-party dependencies identified and assessed
- [ ] Concentration risk analysis performed at portfolio level
- [ ] Monitoring plan defined with frequency, KPIs, and escalation triggers
- [ ] Report formatted for committee consumption and regulatory examination
