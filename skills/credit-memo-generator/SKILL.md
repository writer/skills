---
name: credit-memo-generator
description: Generate investment-grade credit memoranda for commercial and institutional lending decisions. Use when preparing loan committee packages, documenting credit analysis for new originations or renewals, structuring deal summaries for syndication, or creating standardized credit write-ups that meet regulatory and investor documentation requirements.

metadata:
  display_name: "Credit Memo Generator"
  short_description: "Generate commercial and institutional lending credit memos"
  default_prompt: "Generate credit memo for my case with clear next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Credit Memo Generator

## Overview

Produce comprehensive credit memoranda that document the analysis, risk assessment, and recommendation for commercial lending transactions. This skill generates memos conforming to regulatory expectations (OCC Comptroller's Handbook, FDIC Risk Management Manual) and institutional standards, covering borrower analysis, industry context, financial performance, collateral, structure, and risk mitigation. Memos serve as the primary credit decision document for loan committee approval and regulatory examination.

## When to Use

- Preparing new loan origination packages for credit committee
- Documenting annual loan reviews and renewals
- Structuring syndicated loan information memoranda
- Preparing credit analysis for participation purchases
- Documenting material modifications, waivers, or amendments
- Creating standardized credit documentation for regulatory examinations

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Borrower financials | 3+ years of financial statements (audited preferred) | Financial statements |
| Tax returns | 3 years of business and personal (guarantor) tax returns | Tax documents |
| Loan request | Amount, purpose, term, collateral, guarantees | Term sheet |
| Industry data | Sector reports, peer comparisons, market outlook | Industry research |
| Credit bureau | Business and personal credit reports for guarantors | Bureau pulls |
| Existing exposure | Current relationship, payment history, prior memos | Internal records |
| Collateral data | Appraisals, valuations, lien searches | Collateral documents |
| Management bios | Key principal backgrounds, experience, track records | Borrower-provided |

## Methodology

### Step 1 — Executive Summary Construction

Draft a concise executive summary that enables the approver to understand the request without reading the full memo:

- **Borrower**: Legal name, DBA, entity type, ownership structure
- **Request**: Loan amount, type, term, purpose, and source of repayment
- **Recommendation**: Approve/decline with key conditions
- **Risk rating**: Proposed risk grade with brief justification
- **Key strengths**: Top 3 credit strengths (in bullet form)
- **Key risks**: Top 3 risk concerns with mitigants (in bullet form)
- **Relationship context**: Existing exposure, deposit balances, ancillary business, tenure

The executive summary should not exceed one page and must enable a senior credit officer to form a preliminary view before reading the detail.

### Step 2 — Borrower and Industry Analysis

Document the borrower's business model and competitive position:

- **Company overview**: History, legal structure, products/services, geographic footprint, number of employees
- **Ownership and management**: Principals, ownership percentages, key person dependencies, succession planning
- **Management assessment**: Experience depth, track record through economic cycles, management quality rating
- **Industry analysis**: Market size, growth trends, competitive dynamics, cyclicality, regulatory environment
- **Competitive position**: Market share, differentiation, barriers to entry, customer concentration
- **SWOT analysis**: Structured assessment of strengths, weaknesses, opportunities, and threats

### Step 3 — Financial Statement Spreading and Analysis

Perform detailed financial analysis covering a minimum 3-year historical period plus projections:

**Income Statement Analysis:**
- Revenue trend (CAGR, year-over-year growth, seasonality)
- Gross margin trend and comparison to industry benchmarks
- Operating expense efficiency (SG&A as % of revenue)
- EBITDA margin and its stability/trend
- Non-recurring or extraordinary items requiring normalization

**Balance Sheet Analysis:**
- Liquidity: Current ratio, quick ratio, working capital adequacy
- Leverage: Debt-to-equity, debt-to-EBITDA, funded debt-to-EBITDA
- Asset quality: Receivables aging, inventory turnover, fixed asset condition
- Off-balance-sheet items: Operating leases (pre/post ASC 842), contingent liabilities, guarantees

**Cash Flow Analysis:**
- Cash flow from operations (CFO) — the primary source of repayment
- Fixed charge coverage ratio: (EBITDA - CapEx - Taxes - Distributions) / (Interest + Principal + Lease Payments)
- Debt service coverage ratio: NOI or EBITDA / Total Debt Service
- Free cash flow trend and adequacy for debt service plus growth investment
- Capital expenditure requirements (maintenance vs. growth CapEx)

**Key Financial Ratios Summary:**

| Ratio | Year 1 | Year 2 | Year 3 | Projected | Covenant |
|-------|--------|--------|--------|-----------|----------|
| Debt/EBITDA | X.Xx | X.Xx | X.Xx | X.Xx | ≤ X.Xx |
| FCCR | X.Xx | X.Xx | X.Xx | X.Xx | ≥ X.Xx |
| DSCR | X.Xx | X.Xx | X.Xx | X.Xx | ≥ X.Xx |
| Current ratio | X.Xx | X.Xx | X.Xx | X.Xx | ≥ X.Xx |
| Debt/Equity | X.Xx | X.Xx | X.Xx | X.Xx | ≤ X.Xx |

### Step 4 — Loan Structure and Terms

Document the proposed loan structure:

- **Facility type**: Term loan, revolving credit, letter of credit, construction-to-perm
- **Amount and availability**: Commitment amount, borrowing base (if ABL), sublimits
- **Term and amortization**: Maturity date, amortization schedule, balloon payment
- **Pricing**: Interest rate (fixed/variable), spread, floor, fee structure (commitment, unused, origination)
- **Collateral**: Detailed description, valuation, advance rates, lien position
- **Guarantees**: Personal guarantees, corporate guarantees, guarantee coverage and financial capacity
- **Financial covenants**: Specific covenants with testing frequency, cure periods, and consequences
- **Reporting requirements**: Financial statement delivery, compliance certificate, borrowing base certificate
- **Special conditions**: Material adverse change clause, key person provisions, change of control

### Step 5 — Risk Assessment and Grading

Assign and justify the internal risk rating:

- **Probability of Default (PD)**: Based on financial analysis, industry risk, management quality
- **Loss Given Default (LGD)**: Based on collateral coverage, guarantee strength, structural protections
- **Expected Loss (EL)**: PD × LGD applied to exposure
- **Rating justification**: Map specific financial and qualitative factors to the rating grade definitions
- **Rating trend**: Stable, improving, or deteriorating — with justification

### Step 6 — Stress Testing and Sensitivity Analysis

Test borrower resilience under adverse conditions:

- **Revenue stress**: Impact of 10%, 20%, 30% revenue decline on DSCR/FCCR
- **Margin compression**: Impact of gross margin decline of 200–500 bps
- **Interest rate stress**: Impact of 200 bps rate increase on variable-rate debt service
- **Collateral stress**: LTV impact of 10%–20% collateral value decline
- **Break-even analysis**: Revenue level at which DSCR = 1.00x
- **Covenant headroom**: Distance from covenant trigger under stress scenarios

### Step 7 — Recommendation and Conditions

Formulate the credit recommendation:

- **Clear recommendation**: Approve, approve with conditions, decline — with rationale
- **Conditions precedent**: Items required before closing/funding
- **Conditions subsequent**: Items required after closing within specified timeframes
- **Ongoing monitoring requirements**: Frequency of financial reviews, site visits, covenant testing
- **Risk mitigants**: Specific structural protections addressing identified risks
- **Approval authority**: Required approval level per delegation matrix

## Output Specification

```
## Credit Memorandum

### Executive Summary
- Borrower: [Legal Name]
- Request: [Amount, type, term, purpose]
- Risk Grade: [Grade] ([Trend])
- Recommendation: [Approve/Decline]

#### Key Strengths
- [Strength 1]
- [Strength 2]
- [Strength 3]

#### Key Risks and Mitigants
- [Risk 1] — Mitigant: [Description]
- [Risk 2] — Mitigant: [Description]
- [Risk 3] — Mitigant: [Description]

### Borrower Overview
[Company description, ownership, management, industry position]

### Financial Analysis
[Spreading results, ratio analysis, cash flow assessment, trend commentary]

### Loan Structure
[Terms, collateral, covenants, reporting requirements]

### Risk Assessment
[Rating assignment, PD/LGD analysis, stress testing results]

### Recommendation
[Clear recommendation with conditions and monitoring plan]

### Appendices
- A: Financial statement spreads
- B: Collateral valuation summary
- C: Guarantor personal financial statements
- D: Industry research summary
- E: Organizational chart
```

## Analysis Framework

Apply the **CAMPARI** framework:

- **C**haracter — Management quality, integrity, track record
- **A**bility — Demonstrated capacity to manage and generate cash flow
- **M**argin — Adequate pricing for the risk assumed
- **P**urpose — Clear, legitimate, and verifiable loan purpose
- **A**mount — Loan amount appropriate relative to need, capacity, and collateral
- **R**epayment — Identified, reliable, and sufficient primary and secondary repayment sources
- **I**nsurance — Adequate collateral, guarantees, and structural protections

## Examples

**Example 1 — C&I Term Loan**

Borrower: Precision Manufacturing LLC — $15M revenue, EBITDA $2.8M, 10-year operating history. Request: $5M 7-year term loan to fund equipment expansion. DSCR: 1.85x historical, 1.52x stressed. Debt/EBITDA: 1.8x. Collateral: First lien on all business assets including new equipment (OLV $4.2M). Personal guarantee of majority owner (PNW $8.2M). Risk grade: 4 (Pass — Acceptable). Recommendation: Approve with leverage covenant (Debt/EBITDA ≤ 3.0x) and minimum DSCR covenant (≥ 1.25x) tested quarterly.

**Example 2 — CRE Acquisition Loan**

Borrower: Metro Office Partners LLC — SPE acquiring 120,000 SF Class A office building. Request: $18M acquisition loan, 65% LTV, 5-year term with 25-year amortization. NOI: $1.62M, DSCR: 1.35x. Major tenant (55% of NGL) lease expires in Year 3. Risk grade: 5 (Pass — Watch). Recommendation: Approve with lease rollover reserve ($500K), cash management lockbox trigger at DSCR < 1.15x, and requirement to present re-leasing plan by Month 18.

## Guidelines

- Use audited financial statements when available; note qualification if unaudited or compiled
- Normalize EBITDA for non-recurring items but disclose all adjustments with justification
- Present financial data in a consistent format matching the institution's spreading template
- Include at minimum 3 years of historical data plus 1–2 years of projections
- Document all assumptions underlying projections and stress scenarios
- Ensure the memo is self-contained — an examiner should not need to request additional information
- Use objective, professional language — avoid promotional or advocacy tone
- Clearly distinguish facts from analysis/opinion throughout the memo
- Version-control the memo with the date, author, and any subsequent amendments

## Validation Checklist

- [ ] Executive summary is accurate, concise, and includes recommendation with risk grade
- [ ] Borrower/industry analysis reflects current market conditions and competitive dynamics
- [ ] Financial analysis covers at least 3 years historical with consistent spreading methodology
- [ ] All EBITDA adjustments are disclosed, justified, and defensible
- [ ] DSCR/FCCR calculated using the institution's standard methodology
- [ ] Loan structure includes all material terms, covenants, and reporting requirements
- [ ] Risk rating is supported by quantitative analysis and qualitative assessment
- [ ] Stress testing covers revenue, margin, rate, and collateral scenarios
- [ ] Collateral valuation is current and supported by independent appraisal if required
- [ ] Recommendation includes specific conditions precedent and subsequent with deadlines
