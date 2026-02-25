---
name: internal-policy-alignment-checker
description: Ensure CPG business activities align with internal policies on pricing, trade spend, sustainability, ethics, and brand guidelines. Use when validating initiatives against company policy, preparing for internal audits, reviewing cross-functional proposals for policy compliance, or assessing governance gaps.

metadata:
  display_name: "Internal Policy Alignment Checker"
  short_description: "Check CPG activities against internal governance policies"
  default_prompt: "Check my internal policy alignment for gaps risks and required fixes"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Internal Policy Alignment Checker

## Overview

Systematically verify that proposed or active business initiatives comply with the organization's internal policies, standards, and governance frameworks. This skill reviews activities across pricing policy, trade spend authority, brand guidelines, sustainability commitments, ethical standards, and delegation of authority to identify misalignment before it creates risk — functioning as a pre-audit governance check.

## When to Use

- Pre-approval review of new programs, promotions, or partnerships
- Internal audit preparation — self-assessment before formal audit
- Cross-functional proposal review (marketing, sales, finance alignment)
- Post-incident policy compliance investigation
- New employee onboarding — policy awareness verification
- Annual governance gap analysis
- M&A integration — policy harmonization between entities
- ESG/sustainability commitment compliance monitoring

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Activity description | Business initiative, program, or action to review | Detailed description |
| Applicable policies | Relevant internal policies and standards | Policy documents |
| Delegation of authority | Approval thresholds and authorization matrix | DOA matrix |
| Activity financials | Budget, spend, revenue impact of the initiative | Financial summary |
| Stakeholders | Functions and individuals involved | Stakeholder list |
| Prior audit findings | Previous audit results relevant to the activity area | Audit report excerpts |
| ESG commitments | Published sustainability and social responsibility commitments | CSR/ESG report excerpts |

## Methodology

### Step 1: Policy Universe Identification

Map all internal policies potentially applicable to the activity:

**CPG Internal Policy Categories:**

| Category | Common Policies | Typical Owner |
|----------|----------------|--------------|
| Pricing & Revenue | Pricing authority, discount limits, MAP enforcement | Revenue Management / Finance |
| Trade & Promotional | Trade spend authority, promotional approval, co-op guidelines | Sales / Trade Marketing |
| Brand & Marketing | Brand guidelines, claim approval, agency management | Brand Marketing / Legal |
| Procurement & Sourcing | Supplier approval, competitive bidding, conflict of interest | Procurement |
| Financial Controls | Delegation of authority, expense approval, contract signing | Finance / Legal |
| Ethics & Compliance | Anti-bribery (FCPA/UKBA), gifts & entertainment, conflicts | Legal / Compliance |
| Data & Privacy | Data handling, consent management, retention | IT / Legal / Privacy |
| Sustainability / ESG | Packaging commitments, carbon targets, sourcing standards | Sustainability / CSR |
| Quality & Safety | Product safety, recall procedures, quality standards | Quality / Regulatory |
| HR & Employment | Hiring, compensation, anti-harassment, diversity | HR |

### Step 2: Delegation of Authority (DOA) Verification

Check whether the activity has appropriate authorization:

```
DOA Matrix Check:
  Activity Type: [Category — e.g., Trade Commitment]
  Financial Value: $XXK
  
  Authorization Required:
  | Threshold | Approver Level | Approval Status |
  |-----------|---------------|----------------|
  | <$25K | Manager | ✓/✗ |
  | $25K-$100K | Director | ✓/✗ |
  | $100K-$500K | VP | ✓/✗ |
  | $500K-$1M | SVP/GM | ✓/✗ |
  | >$1M | C-Suite/Board | ✓/✗ |
  
  Current Approval: [Who approved, at what level]
  Required Approval: [Who should approve per DOA]
  Gap: [Adequate / Under-authorized / Not yet approved]
```

### Step 3: Policy-by-Policy Compliance Assessment

Review the activity against each applicable policy:

**Assessment Framework per Policy:**

```
Policy: [Policy Name]
Version/Date: [Current version and effective date]
Applicability: [Why this policy applies to the activity]

Requirements:
1. [Specific requirement from policy]
   Status: Compliant / Non-Compliant / Partial / Not Assessed
   Evidence: [How compliance is demonstrated]
   Gap: [If non-compliant, what specifically is missing]

2. [Next requirement]
   Status: ...
   Evidence: ...
   Gap: ...

Overall Policy Compliance: Compliant / Non-Compliant / Partial
Risk if Non-Compliant: [Consequence per policy — disciplinary, financial, legal]
```

**Common CPG Policy Checks:**

| Policy Area | Key Questions | Red Flags |
|-------------|-------------|-----------|
| Pricing | Is the discount within authorized limits? Is channel pricing consistent? | Discounts >20% without VP approval; MAP violation |
| Trade Spend | Is the commitment within budget? Is the ROI threshold met? | Off-budget commitments; ROI <1.0x without justification |
| Brand | Do materials comply with brand guidelines? Are claims approved? | Unapproved claims; off-brand visual identity |
| Ethics | Any gifts, entertainment, or conflicts of interest? | Gifts >$250; entertainment of government officials |
| Procurement | Was competitive bidding followed? Is the supplier approved? | Sole-source without justification; unapproved supplier |
| Sustainability | Does the initiative align with published ESG commitments? | New packaging that contradicts recyclability targets |
| Data | Is customer data handled per privacy policy? | PII sharing without DPA; missing consent records |

### Step 4: Cross-Functional Alignment Check

Verify alignment across functions:

```
Cross-Functional Alignment Matrix:

| Function | Aware? | Aligned? | Concerns? | Sign-Off? |
|----------|--------|----------|-----------|-----------|
| Finance | Y/N | Y/N | [Details] | Y/N |
| Legal | Y/N | Y/N | [Details] | Y/N |
| Marketing | Y/N | Y/N | [Details] | Y/N |
| Sales | Y/N | Y/N | [Details] | Y/N |
| Supply Chain | Y/N | Y/N | [Details] | Y/N |
| Regulatory | Y/N | Y/N | [Details] | Y/N |
| Sustainability | Y/N | Y/N | [Details] | Y/N |

Minimum Alignment Requirement:
  - All impacted functions must be Aware
  - Finance and Legal must be Aligned for any commitment >$50K
  - Regulatory must sign off on any consumer-facing claims
```

### Step 5: ESG and Sustainability Commitment Verification

Cross-reference against published sustainability commitments:

**Sustainability Commitment Audit:**
| Commitment | Target | Activity Impact | Aligned? |
|-----------|--------|----------------|----------|
| 100% recyclable packaging by 2025 | On track / At risk | Does this initiative use recyclable materials? | Y/N |
| 50% reduction in Scope 1+2 emissions | XX% achieved | Does this initiative increase or decrease emissions? | Y/N |
| Responsible sourcing (100% certified palm oil) | XX% achieved | Does this initiative use certified ingredients? | Y/N |
| Diversity in supplier base (25% diverse spend) | XX% achieved | Is the selected supplier diverse-certified? | Y/N |
| Water reduction (20% per unit) | XX% achieved | Impact on water usage? | Y/N |

### Step 6: Risk Rating and Remediation

Assign a compliance risk rating to the overall activity:

| Rating | Definition | Action Required |
|--------|-----------|----------------|
| Compliant | All applicable policies satisfied | Proceed — document compliance evidence |
| Minor Gap | 1-2 low-severity gaps, easily remediated | Remediate within 2 weeks; proceed conditionally |
| Material Gap | Significant policy deviations requiring correction | Pause activity; remediate before proceeding |
| Critical Violation | Violation of law, ethics policy, or major financial control | Stop immediately; escalate to Legal/Compliance |

### Step 7: Documentation and Audit Trail

Ensure proper documentation for governance:

```
Required Documentation:
1. Business case / initiative description
2. DOA approval chain (documented sign-offs)
3. Policy compliance self-assessment (this analysis)
4. Cross-functional alignment confirmation
5. Financial authorization / budget confirmation
6. Risk assessment and mitigation plan
7. Monitoring plan for ongoing compliance

Storage: [Document management system / policy repository]
Retention: [Per records retention policy — typically 7 years for financial]
```

## Output Specification

```markdown
# Internal Policy Alignment Review — [Activity/Initiative Name]

## Executive Summary
**Overall Compliance Status**: [Compliant / Minor Gap / Material Gap / Critical Violation]
**Policies Assessed**: [X]
**Findings**: [X Compliant, X Minor Gap, X Material Gap, X Critical]
**Recommendation**: [Proceed / Proceed with Conditions / Pause / Stop and Escalate]

## Activity Description
[Summary of the business initiative under review]

## Delegation of Authority Check
**Activity Value**: $XXK
**Required Approval Level**: [Level per DOA]
**Actual Approval**: [Who approved]
**DOA Status**: [Adequate / Under-Authorized / Pending]

## Policy Compliance Summary

| Policy | Status | Risk | Key Finding |
|--------|--------|------|------------|
| Pricing Authority | ✅ Compliant | — | Within limits |
| Trade Spend | ⚠️ Minor Gap | Low | ROI documentation missing |
| Brand Guidelines | ✅ Compliant | — | Approved by brand team |
| Ethics/Anti-Bribery | ✅ Compliant | — | No concerns |
| Sustainability | ❌ Material Gap | Medium | Conflicts with packaging commitment |

## Detailed Findings

### Finding 1: [Policy Area]
- **Status**: [Compliant / Non-Compliant / Partial]
- **Policy Reference**: [Policy name, section]
- **Issue**: [Specific gap or violation]
- **Risk**: [Consequence of non-compliance]
- **Remediation**: [Specific action to resolve]
- **Owner**: [Person/function responsible]
- **Due Date**: [Deadline for remediation]

## Cross-Functional Alignment
[Alignment matrix showing function-level awareness, alignment, and sign-off status]

## ESG Commitment Check
[Sustainability commitment verification results]

## Required Actions Before Proceeding
1. [Action with owner and deadline]
2. [Action with owner and deadline]

## Audit Trail Documentation
[Checklist of required documentation with status]
```

## Analysis Framework

**Three Lines of Defense Model:**
```
1st Line: Business/Operations (owns the risk)
  → Self-assessment using this skill
  → Policy awareness and day-to-day compliance

2nd Line: Risk Management & Compliance (oversees risk)
  → Policy development and maintenance
  → Monitoring and advisory

3rd Line: Internal Audit (independent assurance)
  → Independent verification of 1st and 2nd line effectiveness
  → Reports to Audit Committee/Board

This skill operates at the 1st Line, strengthening self-assessment to reduce 3rd Line findings.
```

## Example

**Input**: "Sales team wants to offer a new retailer a $500K annual trade commitment with a 60-day exclusive on our new product launch. The deal was verbally agreed by the Regional Sales Director."

**Analysis excerpt**:
> "**Material Gap identified — 2 findings requiring remediation before proceeding.**
> (1) **DOA violation**: A $500K annual trade commitment requires VP-level approval per Delegation of Authority policy (threshold: >$250K requires VP Sales + VP Finance joint sign-off). The Regional Sales Director's verbal agreement exceeds their $100K authority limit. **Remediation**: Obtain VP Sales and VP Finance written approval before formalizing any commitment. Note: Verbal agreements may be enforceable — flag to Legal.
> (2) **Exclusivity policy conflict**: The 60-day exclusive on the new product launch conflicts with the Innovation Commercialization Policy, which requires simultaneous launch across all Tier 1 retailers unless approved by the GM. This exclusivity could trigger MFN clauses in two other retailer agreements (Retailer B §4.3 and Retailer C §7.1). **Remediation**: Obtain GM approval for exclusive launch with documentation of MFN impact assessment. **Recommendation**: Pause formal commitment until both approvals are secured. Brief Legal on the verbal agreement for risk assessment."

## Guidelines

- Start with DOA verification — unauthorized commitments are the most common and most serious finding
- Review policies in their current version — outdated policy references create false compliance
- Cross-functional alignment is as important as policy compliance — misalignment causes downstream problems
- ESG commitments are increasingly audited — treat them with the same rigor as financial policies
- Document everything — the audit trail is the evidence of compliance
- This skill is a 1st-line self-assessment — it does not replace formal Internal Audit
- When in doubt about a policy interpretation, escalate to the policy owner

## Validation Checklist

- [ ] All applicable policies identified and current versions referenced
- [ ] Delegation of Authority verified with appropriate approval level
- [ ] Each applicable policy assessed with compliance status and evidence
- [ ] Cross-functional alignment matrix completed
- [ ] ESG/sustainability commitments cross-referenced
- [ ] Each finding rated (Compliant / Minor Gap / Material Gap / Critical)
- [ ] Remediation actions specified with owners and deadlines
- [ ] Overall compliance status determined
- [ ] Audit trail documentation checklist completed
- [ ] Escalation triggered if any Critical Violation found
