---
name: loan-application-explanation
description: Explain loan approval and denial decisions with full regulatory compliance. Use when generating adverse action notices, explaining credit decisions to applicants, producing Reg B/ECOA-compliant reason codes, or when loan officers need decision transparency for borrower-facing communications.

metadata:
  display_name: "Loan Application Explanation"
  short_description: "Explain loan approval and denial decisions with reason codes"
  default_prompt: "Explain my loan application in simple words and next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Loan Application Decision Explanation

## Overview

Generate clear, compliant explanations of loan approval or denial decisions. This skill produces borrower-facing narratives that satisfy Regulation B adverse action notice requirements, ECOA fair lending obligations, and internal audit documentation standards. Explanations decompose the decision into contributing factors—credit score, DTI, employment stability, collateral, and policy overlays—ranked by materiality.

## When to Use

- Generating adverse action notices under Reg B / ECOA
- Explaining approval conditions (rate tier, required reserves, co-signer)
- Responding to borrower inquiries about decision rationale
- Producing audit-ready decision documentation
- Supporting fair lending examination preparedness
- Reviewing model-driven decisions for human-readable justification

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Application data | Borrower demographics, income, employment, assets | JSON or tabular |
| Credit bureau pull | FICO score, tradeline summary, derogatory marks | Bureau report extract |
| Decision output | Approve/deny/counter-offer with conditions | Decision engine output |
| Reason codes | Top 4 adverse action reason codes (if denial) | Standard reason code set |
| Product parameters | Loan type, term, requested amount, LTV | Loan product spec |
| Policy overlays | Any investor or institution-specific overlays applied | Policy rule set |

## Methodology

### Step 1 — Parse the Decision Engine Output

Extract the binary decision (approve/deny/counter), the scorecard tier, and all triggered rules. Map each triggered rule to its human-readable policy description. Identify whether the decision was purely model-driven, policy-overlaid, or manually overridden.

### Step 2 — Rank Contributing Factors by Materiality

Order the decision factors by their marginal contribution to the outcome:

1. **Credit score impact** — Distance from cutoff, score band placement
2. **DTI ratio** — Front-end and back-end DTI vs. product maximums (e.g., 43% QM threshold)
3. **LTV/CLTV** — Loan-to-value against program limits and PMI triggers
4. **Employment/income stability** — Verification status, gap analysis, income trending
5. **Collateral adequacy** — Appraisal vs. purchase price, property condition flags
6. **Compensating factors** — Reserves, residual income, co-borrower strength

### Step 3 — Map to Regulatory Reason Codes

For denials and adverse actions, map the top contributing factors to the standardized adverse action reason codes (OCC/FFIEC model codes or proprietary mappings). Select the top 4 reason codes ranked by impact. Verify codes align with the actual decision drivers—never use generic placeholders.

### Step 4 — Generate Borrower-Facing Narrative

Compose a plain-language explanation that:

- States the decision clearly in the first sentence
- Lists specific factors in order of importance
- Avoids prohibited language (no references to protected classes)
- Includes required disclosures (credit bureau source, score used, score range)
- Provides the applicant's right to obtain a free credit report within 60 days
- References the CFPB or appropriate regulatory contact for disputes

### Step 5 — Produce Internal Audit Documentation

Generate a parallel internal document that includes:

- Full factor decomposition with numeric values
- Policy rules triggered with version identifiers
- Any manual override justification and approver identity
- Comparative analysis against similarly situated applicants (fair lending lens)
- Exception tracking reference number if applicable

### Step 6 — Fair Lending Compliance Review

Cross-check the explanation against fair lending red flags:

- Ensure no prohibited basis factors influenced the decision
- Verify similarly situated borrowers received consistent treatment
- Flag any statistical outliers for second-look review
- Document disparate impact analysis results if available

### Step 7 — Assemble Final Deliverable

Package the explanation into the required format: adverse action notice (denial), statement of credit terms (approval with conditions), or counter-offer letter. Include all regulatory disclosures, timing requirements (30-day notice window), and delivery method documentation.

## Output Specification

```
## Loan Decision Explanation

### Decision Summary
- **Application ID**: [ID]
- **Decision**: [Approved / Denied / Counter-Offered]
- **Date**: [Decision date]
- **Product**: [Loan type and term]

### Primary Decision Factors (Ranked)
1. [Factor]: [Plain-language explanation with specific values]
2. [Factor]: [Plain-language explanation with specific values]
3. [Factor]: [Plain-language explanation with specific values]
4. [Factor]: [Plain-language explanation with specific values]

### Adverse Action Reason Codes (if applicable)
- Code [X]: [Description]
- Code [Y]: [Description]
- Code [Z]: [Description]
- Code [W]: [Description]

### Regulatory Disclosures
- Credit score used: [Score] from [Bureau] (range [XXX]–[XXX])
- Right to free credit report within 60 days from [Bureau contact]
- Right to dispute accuracy of information with [Bureau]

### Internal Audit Trail
- Scorecard version: [ID]
- Policy overlay version: [ID]
- Override: [Yes/No — if yes, justification and approver]
- Fair lending flag: [None / Flagged for review — reason]
```

## Analysis Framework

Apply the **FACT** framework for every explanation:

- **F**actors — Enumerate all contributing decision factors with values
- **A**ction codes — Map to regulatory-compliant reason codes
- **C**ompliance — Verify ECOA/Reg B/TILA disclosure requirements
- **T**ransparency — Ensure plain-language accessibility (8th-grade reading level)

## Examples

**Example 1 — Conventional Mortgage Denial**

Input: FICO 612, DTI 48%, LTV 95%, 2 years employment, 1 month reserves
Decision: Denied
Explanation: "Your application for a 30-year conventional mortgage was not approved. The primary factors were: (1) your credit score of 612 is below the minimum threshold of 640 for this program; (2) your total debt-to-income ratio of 48% exceeds the maximum of 45%; (3) your available reserves of 1 month are below the 2-month minimum required for loans with LTV above 90%."

**Example 2 — Auto Loan Approval with Conditions**

Input: FICO 695, DTI 38%, employment 5 years, requested $35,000
Decision: Approved at Tier 2 pricing
Explanation: "Your auto loan application has been approved for $35,000 at 6.49% APR for 60 months. Your rate reflects Tier 2 pricing because your credit score of 695 falls in the 680–719 band. A score of 720 or above would qualify for our best rate of 4.99% APR."

## Guidelines

- Always use the specific credit score, DTI ratio, and LTV values — never vague language
- Limit adverse action notices to exactly 4 reason codes per Reg B convention
- Include the credit score disclosure addendum on every denial and counter-offer
- Use plain language at an 8th-grade reading level for borrower-facing content
- Never reference race, ethnicity, sex, marital status, age, or other prohibited bases
- Maintain separate internal and external explanation documents
- Timestamp all explanations and link to the specific scorecard/policy version
- Retain explanation records for the regulatory minimum retention period (25 months for ECOA)

## Validation Checklist

- [ ] Decision factors are ranked by actual materiality, not arbitrary order
- [ ] Adverse action codes match the true decision drivers
- [ ] All Reg B required disclosures are present (bureau, score, range, rights)
- [ ] No prohibited basis language or proxies appear in the explanation
- [ ] Internal documentation includes scorecard version and policy overlay IDs
- [ ] Plain-language readability target met (Flesch-Kincaid grade 8 or below)
- [ ] Counter-offer letters include both original and revised terms
- [ ] Explanation is timestamped within the 30-day adverse action notice window
- [ ] Fair lending comparative analysis is documented for denials
- [ ] Exception-to-policy decisions have documented justification and approval chain
