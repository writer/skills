---
name: loan-pricing-optimization
description: Provide risk-adjusted loan pricing guidance using PD/LGD models, cost-of-funds analysis, and competitive market data. Use when setting rate sheets, analyzing pricing exceptions, evaluating risk-return trade-offs for new products, optimizing relationship pricing, or ensuring pricing meets target ROE/RAROC thresholds.

metadata:
  display_name: "Loan Pricing Optimization"
  short_description: "Optimize risk-adjusted loan pricing using PD/LGD models"
  default_prompt: "Optimize my loan pricing and suggest the best next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Loan Pricing Optimization

## Overview

Determine optimal risk-adjusted loan pricing that balances credit risk, funding costs, operational expenses, capital requirements, and competitive positioning. This skill builds loan-level pricing from component costs using a bottom-up RAROC (Risk-Adjusted Return on Capital) framework, then applies competitive overlays and relationship pricing adjustments. Outputs support rate sheet construction, pricing exception analysis, and profitability-at-origination monitoring.

## When to Use

- Building or refreshing risk-based pricing grids (rate sheets)
- Evaluating pricing exception requests for large or strategic relationships
- Analyzing profitability of new loan products or market segments
- Benchmarking pricing competitiveness against market rates
- Optimizing relationship pricing to maximize share-of-wallet
- Ensuring compliance with disparate pricing regulations and fair lending requirements

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Cost of funds | FTP (funds transfer pricing) curve by term | Yield curve data |
| Credit risk parameters | PD, LGD, EAD by risk grade and product | Risk model outputs |
| Operating costs | Origination, servicing, overhead cost per loan | Cost accounting data |
| Capital requirements | Regulatory and economic capital by risk weight | Capital model |
| Target returns | Board-approved ROE, RAROC, NIM targets | Strategic plan |
| Market rates | Competitor pricing, benchmark indices, spread data | Market intelligence |
| Relationship data | Borrower's total relationship value and cross-sell potential | CRM data |

## Methodology

### Step 1 — Funds Transfer Pricing (FTP) Foundation

Establish the base cost of funds for each loan:

- **Matched-term FTP**: Assign funding cost matching the loan's repricing tenor
  - Fixed-rate: Use the swap curve or internal FTP curve at the loan's term
  - Variable-rate: Use the short-term index (SOFR, Prime) plus term liquidity premium
- **Liquidity premium**: Add the incremental cost of holding less-liquid loan assets
- **Optionality cost**: Price the prepayment option using an option-adjusted spread (OAS) approach
  - Higher for fixed-rate mortgages with no prepayment penalty
  - Lower for commercial loans with prepayment protection
- **Duration adjustment**: Account for expected vs. contractual maturity based on prepayment models

### Step 2 — Expected Loss Pricing

Add the expected credit loss cost to the base funding cost:

- **Expected Loss = PD × LGD × EAD**
- Source PD from internal rating model or regulatory PD estimates by grade:
  - Investment grade (1–4): PD 0.03%–0.50%
  - Pass (5–6): PD 0.50%–2.00%
  - Watch/Special Mention (7): PD 2.00%–5.00%
  - Substandard (8): PD 5.00%–20.00%
- Apply through-the-cycle (TTC) PD for pricing stability; point-in-time (PIT) for CECL reserves
- LGD varies by collateral type and seniority:
  - Senior secured (real estate): 15%–35%
  - Senior secured (other collateral): 25%–45%
  - Senior unsecured: 40%–60%
  - Subordinated: 60%–80%
- EAD = outstanding balance + expected utilization of undrawn commitments (CCF × unused line)

### Step 3 — Capital Charge Allocation

Price the capital cost of supporting the loan:

- **Regulatory capital**: Risk-weighted assets × minimum capital ratio (typically 8%–10.5% with buffers)
- **Economic capital**: Internal model-derived capital at target confidence level (typically 99.9%)
- **Capital charge = max(regulatory, economic) × target ROE**
- Risk weight assignments:
  - Residential mortgage (50%–100% depending on LTV)
  - Commercial real estate (100%–150%)
  - C&I secured (100%)
  - Consumer unsecured (75%–100%)

### Step 4 — Operating Cost Allocation

Add fully-loaded operational costs:

- **Origination cost**: Application processing, underwriting, closing, documentation
  - Residential: $5,000–$10,000 per loan (amortized over expected life)
  - Commercial: $10,000–$50,000+ depending on complexity
- **Servicing cost**: Payment processing, escrow management, investor reporting
  - Residential: 25–30 bps annually
  - Commercial: 10–20 bps annually
- **Overhead allocation**: Compliance, risk management, technology, facilities
- **Amortization**: Spread origination costs over expected loan life using CPR/CDR assumptions

### Step 5 — Build the Minimum Pricing Grid

Assemble the component pricing into a minimum rate:

```
Minimum Rate = FTP Base Rate
             + Liquidity Premium
             + Optionality Cost
             + Expected Loss (PD × LGD × EAD / Balance)
             + Capital Charge (Capital × Target ROE / Balance)
             + Operating Cost (annualized)
             + Target Profit Margin
```

Build a pricing matrix by risk grade and collateral type:

| Risk Grade | Secured RE | Secured Other | Unsecured |
|------------|-----------|---------------|-----------|
| 1–2 | FTP + XXX bps | FTP + XXX bps | FTP + XXX bps |
| 3–4 | FTP + XXX bps | FTP + XXX bps | FTP + XXX bps |
| 5–6 | FTP + XXX bps | FTP + XXX bps | FTP + XXX bps |
| 7 | FTP + XXX bps | FTP + XXX bps | FTP + XXX bps |

### Step 6 — Competitive and Relationship Adjustments

Adjust minimum pricing for market reality:

- **Competitive overlay**: Compare minimum rates against market intelligence
  - If minimum > market: Accept lower margin, seek offsetting relationship revenue, or decline to compete
  - If minimum < market: Price to market and capture excess return
- **Relationship pricing**: Adjust for total relationship value
  - Cross-sell revenue (deposits, treasury management, insurance, wealth)
  - Deposit-implied funding benefit (core deposits below wholesale funding cost)
  - Lifetime customer value and retention probability
- **Volume/promotional pricing**: Time-limited rate reductions for market share objectives
  - Require approval with documented revenue offset plan
  - Cap promotional volume at [X]% of quarterly production

### Step 7 — Pricing Exception and Profitability Monitoring

Establish pricing governance:

- **Exception authority matrix**: Define who can approve pricing below minimum by magnitude
  - 0–25 bps below: Relationship manager with supervisor
  - 25–50 bps below: Market president or regional credit officer
  - 50+ bps below: Executive committee or pricing committee
- **Profitability-at-origination (PAO)**: Calculate RAROC for every booked loan
- **Portfolio yield monitoring**: Track actual portfolio yield vs. rate sheet pricing
- **Fair lending pricing analysis**: Ensure pricing discretion does not result in disparate impact

## Output Specification

```
## Loan Pricing Analysis — [Borrower/Product]

### Pricing Components
| Component | Rate/Spread | Notes |
|-----------|------------|-------|
| FTP base rate | X.XX% | [Term]-year matched funding |
| Liquidity premium | XX bps | [Liquidity tier] |
| Optionality cost | XX bps | [Prepayment model] |
| Expected loss | XX bps | PD [X.XX%] × LGD [XX%] |
| Capital charge | XX bps | [X]% capital × [XX]% target ROE |
| Operating cost | XX bps | Amortized over [X]-year expected life |
| Target margin | XX bps | Per strategic plan |
| **Minimum rate** | **X.XX%** | |

### Market Comparison
- Minimum rate: X.XX%
- Market midpoint: X.XX%
- Recommended rate: X.XX%
- RAROC at recommended rate: XX.X%

### Relationship Value Assessment
- Loan-only RAROC: XX.X%
- Relationship RAROC: XX.X% (including cross-sell)
- Deposit benefit: XX bps
- Total relationship revenue: $XXX,XXX

### Pricing Decision
- Recommended rate: X.XX%
- Exception required: [Yes/No]
- Exception magnitude: [XX bps below minimum]
- Approval authority: [Level]
```

## Analysis Framework

Apply the **FACE** framework:

- **F**unding — Establish accurate matched-term cost of funds with optionality
- **A**djustment — Layer in expected loss, capital, and operating costs
- **C**ompetitive — Overlay market intelligence and relationship value
- **E**xception — Govern and monitor pricing discretion rigorously

## Examples

**Example 1 — Commercial Real Estate Loan Pricing**

Scenario: $5M 5-year fixed CRE term loan, risk grade 4, 65% LTV. FTP: 4.25% (5-year). Liquidity: +15 bps. EL: +22 bps (PD 0.45% × LGD 30% + seasoning adjustment). Capital: +35 bps (100% RW × 10% capital × 20% ROE target / balance). OpEx: +18 bps. Target margin: +15 bps. Minimum: 5.30%. Market: 5.75%. Recommended: 5.60% (RAROC 22.3%, well above minimum and below market).

**Example 2 — Relationship Pricing Exception**

Scenario: Fortune 500 company requests $50M revolver at SOFR + 125 bps. Minimum pricing: SOFR + 165 bps. Exception: 40 bps below minimum. Justification: $200M deposit relationship generating $3.2M annual net funding benefit + $800K annual treasury management fees. Relationship RAROC: 18.7% (above 15% threshold). Loan-only RAROC: 8.2% (below threshold). Approval: Pricing committee with relationship revenue documentation.

## Guidelines

- Update FTP curves daily; reprice rate sheets at least weekly
- Use through-the-cycle PDs for pricing stability; avoid pro-cyclical whiplash
- Document all pricing exceptions with relationship justification and approval chain
- Monitor pricing discretion for fair lending disparate impact quarterly
- Ensure origination staff understand that minimum rates are floors, not targets
- Separate rate sheet pricing (standard) from negotiated pricing (exception) in reporting
- Recalibrate operating cost allocations annually as volume and efficiency change
- Validate prepayment models quarterly against actual prepayment experience

## Validation Checklist

- [ ] FTP curve is current and matches the institution's actual funding structure
- [ ] PD/LGD parameters are from validated, approved credit risk models
- [ ] Capital charge uses the higher of regulatory and economic capital
- [ ] Operating costs are fully loaded (no material cost categories omitted)
- [ ] Competitive pricing data is current (within 2 weeks) and from reliable sources
- [ ] Relationship revenue projections are realistic and documented
- [ ] Exception authority matrix is current and aligned with board-approved policy
- [ ] RAROC calculations use consistent methodology across all products
- [ ] Fair lending analysis of pricing outcomes is conducted quarterly
- [ ] PAO monitoring is operational and exceptions are tracked to maturity
