---
name: credit-policy-interpretation
description: Explain credit policy rules, exceptions, and eligibility criteria in plain language. Use when loan officers need policy guidance, when determining borrower eligibility against complex policy matrices, interpreting investor overlay requirements, documenting exception-to-policy rationale, or resolving conflicts between base policy and investor/agency guidelines.

metadata:
  display_name: "Credit Policy Interpretation"
  short_description: "Interpret credit policy rules, exceptions, and eligibility"
  default_prompt: "Explain my credit policy in simple words and next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Credit Policy Interpretation

## Overview

Interpret and explain credit policy rules, eligibility matrices, and exception frameworks for lending personnel. This skill translates complex policy documents—including base credit policy, investor overlays, agency guidelines (Fannie Mae, Freddie Mac, FHA, VA), and regulatory requirements—into clear, actionable guidance. Outputs help loan officers determine eligibility, structure compliant loans, and document exception requests with appropriate compensating factors.

## When to Use

- Loan officers need guidance on borrower eligibility for a specific product
- Interpreting overlapping or conflicting policy requirements across investors
- Structuring loans to meet multiple guideline layers simultaneously
- Preparing exception-to-policy requests with compensating factor documentation
- Training new underwriters on policy application
- Evaluating impact of policy changes on eligible borrower populations

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Credit policy manual | Current base credit policy with all sections | Policy document |
| Investor overlays | Agency and correspondent investor-specific overlays | Overlay matrices |
| Loan scenario | Specific borrower and loan characteristics | Structured data |
| Exception history | Prior approved exceptions with justification | Exception log |
| Regulatory guidance | Applicable regulations (QM, ATR, TRID, state-specific) | Regulatory references |
| Product matrix | Available products with eligibility parameters | Product guide |

## Methodology

### Step 1 — Identify Applicable Policy Layers

Determine all policy layers that apply to the loan scenario:

1. **Base institutional credit policy** — Internal minimum standards
2. **Agency/GSE guidelines** — Fannie Mae Selling Guide, Freddie Mac Guide, FHA Handbook 4000.1, VA Lender's Handbook
3. **Investor overlays** — Correspondent or aggregator-specific additions to agency guidelines
4. **Regulatory requirements** — QM/ATR (Reg Z), TRID, ECOA, state-specific restrictions
5. **MI requirements** — Private mortgage insurance eligibility criteria for high-LTV loans
6. **Program-specific rules** — First-time homebuyer, community lending, affordable housing

Apply the **most restrictive rule** when multiple layers address the same parameter. Document which layer drives each constraint.

### Step 2 — Evaluate Eligibility Against Each Parameter

Systematically check the loan scenario against all eligibility parameters:

- **Credit score**: Minimum FICO (representative score, lowest mid-score for multiple borrowers)
- **LTV/CLTV/HCLTV**: Maximum ratios by product, occupancy, property type, and transaction type
- **DTI**: Front-end (housing ratio) and back-end (total DTI) maximums, QM 43% threshold or agency patch
- **Reserves**: Minimum months of PITIA reserves by LTV tier and property count
- **Property type eligibility**: SFR, condo (warrantable/non-warrantable), 2–4 unit, manufactured, co-op
- **Occupancy**: Primary residence, second home, investment property — requirements vary significantly
- **Income documentation**: Full doc, alt-doc, bank statement, asset depletion eligibility
- **Employment**: Minimum tenure, gap documentation, self-employment seasoning (typically 2 years)
- **Down payment source**: Acceptable sources, gift rules, seller concession limits

### Step 3 — Identify Policy Conflicts and Layering Issues

When multiple guidelines interact, identify and resolve conflicts:

- **Conflict resolution hierarchy**: Regulatory > Agency > Investor overlay > Base policy
- **Common conflicts**:
  - Agency allows 50% DTI with DU/LP approval, but investor overlay caps at 45%
  - FHA allows 580 FICO with 10% down, but institution requires 620 minimum
  - VA has no maximum DTI, but QM rules impose reasonableness standard
- **Documentation requirements**: Different layers may require different documentation levels for the same parameter
- Clearly state which layer is the binding constraint for each parameter

### Step 4 — Structure Compliant Loan Options

When a borrower does not meet the most restrictive criteria, identify alternatives:

- **Product substitution**: Switch from conventional to FHA/VA if more favorable guidelines apply
- **Structure adjustment**: Increase down payment to reduce LTV below an overlay threshold
- **Co-borrower addition**: Add income or credit strength to meet DTI or score requirements
- **Compensating factors**: Identify and document factors that may support an exception
  - Significant reserves (12+ months PITIA)
  - Conservative LTV (<75%) offsetting high DTI
  - Long employment tenure and stable income trend
  - Minimal payment shock from current housing payment
  - Low total debt with only the mortgage as the primary obligation

### Step 5 — Exception Request Preparation

When no compliant structure exists, prepare an exception request:

- **Exception type**: Identify the specific parameter(s) requiring exception
- **Magnitude of exception**: How far outside policy (1 point FICO, 2% DTI, etc.)
- **Compensating factors**: Minimum 2 documented compensating factors per exception
- **Historical precedent**: Cite approved exceptions for comparable scenarios
- **Risk assessment**: Provide the incremental PD/LGD impact of the exception
- **Approval authority**: Identify the required approval level (underwriter, senior UW, credit officer, committee)

### Step 6 — Generate Policy Interpretation Memo

Produce a clear, structured memo that explains:

- The applicable policy rules and their sources
- How the borrower's profile maps to each rule (pass/fail/marginal)
- The binding constraint(s) and which policy layer drives them
- Recommended loan structure for compliance
- Exception request details if applicable, with full compensating factor documentation

### Step 7 — Impact Assessment for Policy Changes

When evaluating proposed policy modifications:

- Estimate the population of currently-eligible borrowers affected
- Calculate the incremental risk (PD/LGD change) from loosening or tightening
- Assess fair lending impact of the proposed change across demographic segments
- Model the revenue impact (volume change × margin per loan)
- Provide a recommendation with risk/reward analysis

## Output Specification

```
## Credit Policy Interpretation Memo

### Loan Scenario Summary
- Borrower: [Name/ID]
- Product requested: [Type, term, amount]
- Key metrics: FICO [XXX], DTI [XX%], LTV [XX%], Reserves [X months]

### Policy Layer Analysis
| Parameter | Base Policy | Agency Guide | Investor Overlay | Borrower Value | Status |
|-----------|-------------|-------------|-----------------|---------------|--------|
| Min FICO | 640 | 620 | 660 | [XXX] | [Pass/Fail] |
| Max DTI | 45% | 50% (DU) | 43% | [XX%] | [Pass/Fail] |
| Max LTV | 95% | 97% | 95% | [XX%] | [Pass/Fail] |
| Reserves | 2 mo | 0 mo | 2 mo | [X mo] | [Pass/Fail] |

### Binding Constraints
- [Parameter]: Limited by [Policy layer] at [Value]

### Recommended Structure
- [Description of compliant loan structure, if available]

### Exception Request (if needed)
- Parameter(s): [What is out of policy]
- Deviation: [Magnitude]
- Compensating factors:
  1. [Factor with documentation]
  2. [Factor with documentation]
- Approval authority required: [Level]
- Historical precedent: [Reference]

### Risk Assessment
- Base PD: [X.XX%] → Exception PD: [X.XX%]
- Incremental risk: [Quantified]
```

## Analysis Framework

Apply the **LACE** framework:

- **L**ayers — Identify all applicable policy layers and their hierarchy
- **A**ssessment — Evaluate the scenario against every parameter in every layer
- **C**onflicts — Resolve conflicts using the regulatory precedence hierarchy
- **E**xceptions — Structure exception requests with documented compensating factors

## Examples

**Example 1 — Multi-Layer Eligibility Check**

Scenario: Borrower with 655 FICO, 46% DTI, 90% LTV seeking conventional 30-year. Base policy minimum FICO: 640 (pass). Fannie Mae minimum with DU: 620 (pass). Investor overlay minimum: 660 (fail by 5 points). DTI: base 45% (fail by 1%), Fannie Mae 50% (pass), investor 45% (fail by 1%). Binding constraints: investor overlay FICO 660 and DTI 45%. Options: (1) seek different investor with lower overlay, (2) request exception for 5-point FICO and 1% DTI deviation with compensating factors of 6 months reserves and 15-year stable employment.

**Example 2 — FHA vs. Conventional Comparison**

Scenario: First-time buyer, 610 FICO, 3.5% down, 41% DTI. Conventional: Ineligible (most investors require 620+ FICO at >90% LTV). FHA: Eligible (580+ FICO with 3.5% down, 43% DTI max with TOTAL scorecard approval). Recommendation: Structure as FHA 30-year fixed with UFMIP and annual MIP. Note 610 FICO will result in higher MIP tier.

## Guidelines

- Always cite the specific policy section, version number, and effective date
- Use the most recently published guidelines — agency guidelines update frequently
- Apply the most restrictive applicable standard unless an exception is approved
- Document compensating factors with objective, verifiable evidence
- Never recommend structuring that circumvents the spirit of a policy (e.g., straw buyers)
- Track exception approval rates by type to calibrate future recommendations
- Highlight any parameters that are marginally passing (within 5% of the limit)
- Flag scenarios where guideline differences are driven by ambiguous interpretation

## Validation Checklist

- [ ] All applicable policy layers identified and version-dated
- [ ] Every eligibility parameter checked against every applicable layer
- [ ] Binding constraint correctly attributed to the driving policy layer
- [ ] Conflicts resolved using proper hierarchy (regulatory > agency > overlay > base)
- [ ] Alternative structures explored before recommending an exception
- [ ] Exception requests include minimum 2 compensating factors with documentation
- [ ] Risk assessment quantifies incremental PD/LGD for the exception
- [ ] Approval authority correctly identified per delegation matrix
- [ ] Fair lending considerations addressed (exception consistency across segments)
- [ ] Memo is clear enough for an underwriter unfamiliar with the scenario to follow
