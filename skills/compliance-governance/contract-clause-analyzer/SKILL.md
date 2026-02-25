---
name: contract-clause-analyzer
description: Analyze CPG commercial contracts to highlight risky clauses, unfavorable terms, and missing protections in retailer agreements, co-packing contracts, and supplier agreements. Use when reviewing trade agreements, JBP contracts, co-manufacturer agreements, licensing deals, or any commercial contract requiring risk assessment.

metadata:
  display_name: "Contract Clause Analyzer"
  short_description: "Analyze CPG contracts for risky or missing clauses"
  default_prompt: "Analyze my contract clause and recommend clear next actions"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Contract Clause Analyzer

## Overview

Perform structured risk analysis of commercial contracts common in the CPG industry. This skill identifies risky clauses, unfavorable terms, missing protections, and non-market provisions across retailer agreements, co-packing contracts, supplier agreements, and distribution arrangements. Each finding is risk-rated with specific remediation language and market benchmark comparisons.

## When to Use

- Reviewing new retailer trading agreements or amendments
- Evaluating co-packer/co-manufacturer contracts
- Assessing supplier/ingredient supply agreements
- Reviewing distribution or broker agreements
- M&A due diligence — contract portfolio risk assessment
- Annual contract renewal preparation
- Dispute resolution — identifying contractual leverage points

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Contract document | Full contract text or key excerpts | Document or text |
| Contract type | Retailer, co-packer, supplier, distribution, licensing | Selection |
| Counterparty profile | Who you're contracting with and their market position | Summary |
| Your negotiating position | Relative power and strategic importance of the relationship | Assessment |
| Industry context | Relevant industry norms and standards | Optional context |
| Priority areas | Specific concerns or clauses to focus on | Optional list |

## Methodology

### Step 1: Contract Taxonomy and Structure Assessment

Identify the contract type and expected clause universe:

**Retailer Trading Agreements:**
| Expected Clause | Purpose | Risk Focus |
|----------------|---------|-----------|
| Payment terms | When invoices are paid | Extended terms = working capital drag |
| Deduction rights | Retailer right to offset invoices | Unilateral deduction authority |
| Promotional terms | Trade spend commitments | Escalation clauses, minimums |
| Slotting/new item fees | Cost to gain shelf space | Non-refundable, guaranteed minimums |
| Performance penalties | Chargeback triggers (fill rate, labeling) | Strict liability vs. good faith cure |
| Exclusivity provisions | Channel or product exclusivity | Overly broad restrictions |
| Termination | How either party can exit | Asymmetric notice periods |
| Indemnification | Liability allocation | Broad, uncapped indemnification |
| Insurance requirements | Coverage mandates | Excessive minimums |
| MFN/Price parity | Most-favored-nation pricing | Constrains pricing flexibility |

**Co-Packer/Co-Manufacturer Agreements:**
| Expected Clause | Risk Focus |
|----------------|-----------|
| Minimum volume commitments | Take-or-pay exposure |
| Quality standards and testing | Who bears cost of quality failures |
| IP and recipe confidentiality | Competitive protection |
| Capacity allocation | Guaranteed capacity vs. best efforts |
| Cost escalation | Pass-through mechanisms and caps |
| Audit rights | Ability to inspect facility |
| Termination and transition | Knowledge transfer and ramp-down |

### Step 2: Risk Clause Identification

Analyze each clause against a risk framework:

**Risk Rating Criteria:**

| Rating | Definition | Financial Exposure |
|--------|-----------|-------------------|
| Critical | Clause could result in material financial loss, litigation, or business disruption | >$500K or >5% of contract value |
| High | Clause creates significant unfavorable obligations or exposure | $100K-$500K or 2-5% |
| Medium | Clause is below market standard but manageable | $25K-$100K or 1-2% |
| Low | Minor deviation from best practice | <$25K or <1% |
| Acceptable | Clause is at or above market standard | No material exposure |

**Common High-Risk Clause Patterns in CPG:**

1. **Unilateral Deduction Rights**: Retailer can deduct from invoices without prior notice or dispute process. Risk: Uncontrolled cash flow reduction.

2. **Automatic Renewal with Escalation**: Contract auto-renews with built-in cost increases. Risk: Lock-in at above-market rates.

3. **Broad Indemnification**: "Indemnify and hold harmless from any and all claims." Risk: Unlimited liability exposure.

4. **Most-Favored-Nation (MFN)**: Must offer this partner the best price/terms given to any other partner. Risk: Cascading price reductions, constrains channel strategy.

5. **Termination for Convenience (asymmetric)**: They can terminate on 30 days' notice; you require 180 days. Risk: Business disruption without adequate transition.

6. **IP Assignment**: Ownership of custom formulations, packaging designs, or co-developed IP transfers to counterparty. Risk: Loss of innovation investment.

7. **Non-Compete/Exclusivity**: Prevents selling to other retailers/channels or developing competing products. Risk: Growth limitation.

8. **Unlimited Liability**: No cap on damages. Risk: Existential financial exposure from operational failure.

9. **Cost Pass-Through Without Cap**: Counterparty can pass through "all cost increases." Risk: Uncontrolled cost escalation.

10. **Change of Control**: Counterparty can terminate if you're acquired. Risk: M&A value destruction.

### Step 3: Benchmark Against Market Standards

Compare each flagged clause against industry benchmarks:

| Clause | Contract Language | Market Standard | Gap Assessment |
|--------|------------------|----------------|---------------|
| Payment terms | Net 90 | Net 30-45 (CPG industry standard) | Unfavorable: 45-60 days excess |
| Fill rate penalty | 98% threshold, $XX/case | 95% threshold, $X/case | Overly strict threshold |
| Deduction dispute | 30 days to dispute | 60-90 days | Inadequate dispute window |
| Liability cap | None stated | 2x annual contract value | Missing protection |

### Step 4: Missing Clause Analysis

Identify critical clauses that are absent from the contract:

| Missing Clause | Why It Matters | Recommended Language |
|---------------|---------------|---------------------|
| Force majeure | Excuses performance during extraordinary events | Include pandemic, supply chain disruption, weather |
| Dispute resolution | Structured escalation before litigation | Negotiation → Mediation → Arbitration |
| Data rights | Who owns data generated from the relationship | Clearly allocate POS, shopper, and derived data rights |
| Confidentiality | Protection of trade secrets and business information | Mutual NDA with carve-outs for required disclosures |
| Annual review | Mechanism to revisit terms | Annual review window for pricing, volume, terms |
| Limitation of liability | Cap on damages | Typically 1-3x annual contract value |
| Insurance requirements | Coverage minimums | Proportionate to risk profile |

### Step 5: Financial Exposure Quantification

For each flagged clause, estimate the financial exposure:

```
Exposure Calculation:
  Probability of clause being invoked: X% (based on historical experience)
  Potential financial impact if invoked: $X (based on contract value)
  Expected Loss = Probability × Impact = $X

  Example: Unilateral deduction right
    Historical deduction rate at this retailer: 3% of gross invoices
    Annual invoiced revenue: $10M
    Expected annual deduction exposure: $300K
    Disputed deduction recovery rate: 40%
    Net expected loss: $180K/year
```

### Step 6: Remediation Strategy

For each finding, provide specific remediation:

**Remediation Framework:**
1. **Ideal Language**: What you want the clause to say
2. **Fallback Language**: Acceptable compromise if ideal is rejected
3. **Walk-Away Threshold**: The minimum acceptable version of the clause
4. **Negotiation Rationale**: Why the change benefits both parties (not just you)

## Output Specification

```markdown
# Contract Clause Analysis — [Contract Name/Counterparty]

## Executive Summary
**Overall Risk Rating**: [Critical / High / Medium / Low]
**Findings**: [X Critical, X High, X Medium, X Low]
**Top 3 Risks**: [Brief list]
**Estimated Total Exposure**: $XM (annualized expected loss)

## Contract Overview
- Type: [Retailer/Co-packer/Supplier/Distribution]
- Counterparty: [Name]
- Term: [Duration with renewal provisions]
- Total Value: $XM (annual)

## Findings Detail

### Finding 1: [Clause Name]
- **Risk Rating**: Critical / High / Medium / Low
- **Contract Reference**: Section X.X, Page X
- **Current Language**: "[Exact contract text]"
- **Issue**: [Why this is risky]
- **Market Benchmark**: [What standard market language looks like]
- **Financial Exposure**: $XK (probability × impact)
- **Recommended Language**: "[Specific proposed revision]"
- **Fallback Position**: "[Minimum acceptable revision]"
- **Negotiation Rationale**: [Why counterparty should accept]

### Finding 2: [Clause Name]
[Same structure]

## Missing Clauses
| Clause | Risk of Absence | Recommended Addition |
|--------|----------------|---------------------|
| ... | ... | ... |

## Financial Exposure Summary
| Finding | Probability | Impact | Expected Loss |
|---------|------------|--------|---------------|
| ... | X% | $XK | $XK |
| **Total** | | | **$XK** |

## Negotiation Priority Matrix
| Finding | Financial Impact | Negotiability | Priority |
|---------|-----------------|---------------|----------|
| ... | High/Med/Low | High/Med/Low | 1/2/3... |

## Recommended Negotiation Sequence
[Ordered list of clauses to negotiate, starting with highest-priority]
```

## Analysis Framework

**Contract Risk Scoring Model:**
```
Clause Risk Score = Severity × Probability × (1 − Mitigation Effectiveness)

Where:
  Severity (1-5): Financial impact magnitude
  Probability (1-5): Likelihood clause is invoked
  Mitigation (0-1): Existing controls that reduce impact

Contract Composite Risk = Σ (Clause Risk Scores) / Number of Clauses Assessed
```

## Example

**Input**: "Retailer agreement includes: 'Vendor agrees to indemnify and hold harmless Retailer from any and all claims, damages, losses, and expenses arising from Vendor's products, including but not limited to product liability, recalls, and regulatory non-compliance, without limitation.'"

**Analysis**:
> "**CRITICAL RISK: Unlimited broad-form indemnification.** This clause creates uncapped liability exposure across an expansive scope including product liability, recalls, and regulatory issues — with no limitation on damages, no fault requirement, and no exclusion for retailer's own negligence. **Market benchmark**: Standard CPG retailer indemnification is mutual, fault-based, with a liability cap of 2x annual contract value and exclusion for consequential damages. **Financial exposure**: At $5M annual revenue with this retailer, an uncapped indemnification on a product liability claim could result in $10M+ exposure including retailer's defense costs, lost profits claims, and consequential damages. **Recommended revision**: 'Vendor agrees to indemnify Retailer from third-party claims directly caused by defects in Vendor's products, subject to a liability cap of [2x] annual purchase volume. This indemnification excludes claims arising from Retailer's negligence, modification of products, or failure to follow storage and handling instructions. Consequential, incidental, and punitive damages are excluded.' **Fallback**: Accept broader scope if a liability cap of 3x annual volume is included and consequential damages are excluded."

## Guidelines

- Always read the full contract before analyzing individual clauses — context matters
- Focus analysis on the highest-risk clauses first — not every clause needs deep analysis
- Quantify financial exposure wherever possible — it drives negotiation prioritization
- Provide specific alternative language, not just "revise this clause"
- Frame remediation as mutually beneficial — counterparties reject one-sided demands
- Flag missing clauses with the same rigor as problematic present clauses
- This analysis is a risk assessment tool, not legal advice — recommend legal counsel for Critical findings

## Validation Checklist

- [ ] Contract type identified and expected clause universe established
- [ ] All clauses assessed against risk rating criteria
- [ ] At least 10 common high-risk patterns checked
- [ ] Flagged clauses benchmarked against market standards
- [ ] Missing clauses identified with risk of absence
- [ ] Financial exposure quantified for each critical/high finding
- [ ] Remediation includes ideal, fallback, and walk-away language
- [ ] Negotiation rationale framed as mutually beneficial
- [ ] Findings prioritized by financial impact and negotiability
- [ ] Recommended negotiation sequence provided
