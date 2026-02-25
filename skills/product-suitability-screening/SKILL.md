---
name: product-suitability-screening
description: Screen investment products for suitability alignment with specific client profiles per Reg BI and fiduciary standards. Use when evaluating new product recommendations, comparing alternative products for a client, conducting product shelf reviews, assessing complex products for appropriateness, or documenting the best interest determination for regulatory compliance.

metadata:
  display_name: "Product Suitability Screening"
  short_description: "Screen investment product suitability per Reg BI standards"
  default_prompt: "Check my product suitability screening for gaps risks and required fixes"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Product Suitability Screening

## Overview

Evaluate investment products against individual client profiles to determine suitability and document the best interest rationale. This skill screens products across risk, cost, complexity, liquidity, tax efficiency, and objective alignment dimensions, compares alternatives, and produces Reg BI-compliant recommendation documentation. Outputs ensure every product recommendation has a defensible suitability basis and that lower-cost, less-complex alternatives were considered.

## When to Use

- Evaluating a specific product for recommendation to a client
- Comparing multiple product alternatives for the same investment objective
- Conducting annual product shelf reviews for the advisory platform
- Assessing complex or alternative products for client appropriateness
- Documenting Reg BI best interest determination for a recommendation
- Responding to compliance inquiries about product selection rationale

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Product details | Prospectus, fact sheet, fee schedule, risk characteristics | Product documentation |
| Client profile | Risk tolerance, time horizon, net worth, income, goals, sophistication | Client data |
| Alternative products | Comparable products available on the platform | Product shelf data |
| Account type | Registration, tax status, purpose designation | Account records |
| Existing holdings | Current portfolio composition and overlap analysis | Custodian data |
| Compliance rules | Firm-approved product list, concentration limits, suitability criteria | Compliance policy |

## Methodology

### Step 1 — Product Characteristic Assessment

Catalog the product's key characteristics for suitability evaluation:

**Risk characteristics:**
- Asset class and sub-strategy classification
- Historical volatility (standard deviation, 3/5/10 year)
- Maximum drawdown (worst peak-to-trough decline)
- Beta relative to broad market index
- Credit risk (if fixed income: average credit quality, default rate)
- Concentration risk (top holdings, sector concentration)
- Leverage usage (if any)
- Derivative usage and counterparty risk

**Cost structure:**
- Management fee / expense ratio
- Sales charges (front-end load, deferred sales charge, level load)
- 12b-1 fees
- Performance fees (if applicable)
- Surrender charges and schedule
- Trading costs (bid-ask spreads for ETFs, transaction fees for mutual funds)
- Total cost of ownership (TCO) over 1, 3, 5, 10-year horizons

**Liquidity characteristics:**
- Daily liquidity (open-end mutual fund, ETF)
- Periodic liquidity (interval fund — quarterly/semi-annual tender)
- Lock-up period (private fund — 1–10+ years)
- Redemption gates and suspension provisions
- Secondary market availability and typical discount/premium

**Complexity assessment:**
| Level | Examples | Appropriate For |
|-------|---------|----------------|
| 1 — Basic | Index funds, bond funds, balanced funds | All clients |
| 2 — Moderate | Active equity, sector funds, REITs, high-yield | Intermediate+ clients |
| 3 — Complex | Options strategies, alternatives, structured notes | Sophisticated clients with specific need |
| 4 — Highly complex | Private equity, hedge funds, derivatives-based | Qualified/accredited investors with advisor guidance |

**Tax characteristics:**
- Tax efficiency rating (turnover rate, distribution history)
- Capital gains distribution frequency and magnitude
- Qualified dividend percentage
- Tax-loss harvesting compatibility
- Appropriate account type (taxable, tax-deferred, tax-exempt)

### Step 2 — Client Profile Matching

Score the product against the client's profile across each dimension:

| Dimension | Client Requirement | Product Characteristic | Match |
|-----------|-------------------|----------------------|-------|
| Risk level | [Score/Category] | [Score/Category] | [✓/✗/~] |
| Time horizon | [X years] | [Min recommended hold: X years] | [✓/✗/~] |
| Liquidity need | [Within X days] | [Liquidity: X] | [✓/✗/~] |
| Income need | [$X annual] | [Yield: X%] | [✓/✗/~] |
| Sophistication | [Level] | [Complexity: Level X] | [✓/✗/~] |
| Tax situation | [Rate: XX%] | [Tax efficiency: X] | [✓/✗/~] |
| Net worth / QI | [$X] | [Min: $X / Accredited req] | [✓/✗/~] |
| Concentration | [Current: X%] | [Post-add: X%] | [✓/✗/~] |

**Automatic disqualifiers:**
- Product risk exceeds client's governing risk level
- Client cannot meet minimum investment or accreditation requirements
- Liquidity terms exceed client's liquidity needs
- Product complexity exceeds client's demonstrated sophistication
- Position would breach concentration limits

### Step 3 — Alternative Product Comparison

Identify and compare alternatives that could serve the same investment objective:

| Criterion | Product A (Proposed) | Product B (Alt 1) | Product C (Alt 2) |
|-----------|---------------------|-------------------|-------------------|
| Strategy | [Description] | [Description] | [Description] |
| Expense ratio | X.XX% | X.XX% | X.XX% |
| 5Y return (ann.) | X.XX% | X.XX% | X.XX% |
| Sharpe ratio (5Y) | X.XX | X.XX | X.XX |
| Max drawdown | -XX% | -XX% | -XX% |
| Liquidity | [Daily/Qtly/Lock-up] | [Daily/Qtly/Lock-up] | [Daily/Qtly/Lock-up] |
| Min investment | $X | $X | $X |
| Tax efficiency | [High/Med/Low] | [High/Med/Low] | [High/Med/Low] |

**Cost comparison over client's time horizon:**
- 10-year cost of ownership per $100,000 invested:
  - Product A: $[X]
  - Product B: $[X]
  - Product C: $[X]

**Reg BI requirement**: If recommending a higher-cost product, document the specific, articulable reason why it is in the client's best interest despite the cost differential (e.g., access to strategy unavailable at lower cost, superior risk-adjusted returns, tax advantages, specific client need).

### Step 4 — Conflict of Interest Assessment

Identify and document all material conflicts:

- **Revenue sharing**: Does the product provider pay the firm revenue sharing or shelf-space fees?
- **Proprietary product**: Is this a firm-affiliated product? If yes, document why it's preferred over third-party alternatives
- **Compensation differential**: Does the advisor receive higher compensation for this product vs. alternatives?
- **12b-1 fees**: Are there ongoing distribution fees that benefit the firm?
- **Non-cash compensation**: Any conferences, trips, or gifts from the product provider?

For each identified conflict, document the mitigation:
- Disclosure to client (written, verbal, Form CRS reference)
- Offsetting client benefit that justifies the recommendation despite the conflict
- Compliance-approved rationale

### Step 5 — Portfolio Fit Analysis

Assess how the product fits within the client's existing portfolio:

- **Asset class gap**: Does this product fill an allocation gap vs. the IPS target?
- **Overlap analysis**: Correlation with existing holdings — avoid adding redundant exposure
- **Diversification impact**: How does adding this product change portfolio risk metrics?
  - Portfolio volatility before and after addition
  - Maximum drawdown before and after
  - Sharpe ratio before and after
- **Rebalancing implications**: Will adding this product require selling other positions?
- **Portfolio-level cost impact**: How does this product change the overall portfolio expense ratio?

### Step 6 — Best Interest Determination Documentation

Compile the Reg BI best interest determination:

**Care obligation documentation:**
- Reasonable basis: Product is suitable for at least some investors (general suitability)
- Customer-specific: Product is suitable for THIS client based on their profile
- Quantitative: Recommendation frequency is reasonable (no excessive trading)
- Alternatives considered: At least 2 alternatives evaluated with documented rationale for selection

**Documentation template:**

```
Best Interest Determination — [Client Name] — [Date]

Product recommended: [Name]
Investment objective served: [Objective]

Suitability basis:
- Client risk profile: [Category] — Product risk: [Category] — Match: [Yes]
- Time horizon: [Client X years] — Product minimum: [X years] — Match: [Yes]
- Liquidity: [Client need] — Product liquidity: [Terms] — Match: [Yes]

Alternatives considered:
- [Alt 1]: Not selected because [specific reason]
- [Alt 2]: Not selected because [specific reason]

Cost analysis: [Proposed product cost vs. alternatives — justification if higher cost]

Conflicts: [Identified conflicts and mitigations]

Conclusion: This recommendation is in [Client Name]'s best interest because
[specific, articulable reasons tied to the client's individual circumstances].
```

### Step 7 — Ongoing Monitoring Framework

Establish post-recommendation monitoring:

- **Performance monitoring**: Review product performance vs. expectations quarterly
- **Suitability reassessment**: Re-evaluate product suitability at each periodic review
- **Cost competitiveness**: Reassess cost vs. alternatives annually (fee reductions, new entrants)
- **Product changes**: Monitor for material changes (manager departure, strategy drift, fee increases)
- **Client changes**: Reassess suitability when client circumstances change materially

## Output Specification

```
## Product Suitability Screening Report

### Product Overview
- Name: [Product name]
- Category: [Asset class / strategy]
- Expense ratio: [X.XX%]
- Risk level: [Score/Category]
- Complexity: Level [1–4]
- Liquidity: [Terms]

### Client Suitability Match
| Dimension | Requirement | Product | Result |
|-----------|------------|---------|--------|
| [Dim] | [Req] | [Product char] | [Pass/Fail/Marginal] |

### Alternative Comparison
[Comparison table with rationale for selection]

### Conflict Assessment
[Conflicts identified and mitigations documented]

### Portfolio Fit
- Allocation gap filled: [Yes/No — which asset class]
- Diversification impact: [Positive/Neutral/Negative]
- Portfolio cost impact: [+/- X bps]

### Best Interest Determination
[Completed Reg BI documentation template]

### Recommendation: [Suitable / Not Suitable / Suitable with Conditions]
```

## Analysis Framework

Apply the **PRISM** framework:

- **P**roduct analysis — Catalog risk, cost, liquidity, complexity, and tax characteristics
- **R**equirements matching — Score product against client profile dimensions
- **I**nterest conflicts — Identify and document all material conflicts with mitigations
- **S**election rationale — Compare alternatives and document why this product was chosen
- **M**onitoring — Establish ongoing suitability surveillance framework

## Examples

**Example 1 — Index Fund vs. Active Fund Comparison**

Client: 45-year-old moderate-risk investor, $500K taxable account, 20-year horizon. Objective: US large-cap equity exposure. Product A: Vanguard S&P 500 ETF (VOO), ER 0.03%. Product B: Active large-cap fund, ER 0.75%. 10-year cost per $100K: VOO $300 vs. Active $7,500. Active fund has underperformed benchmark 7 of 10 years. No specific alpha thesis that justifies 25x cost differential. Recommendation: VOO — lower cost, better tax efficiency, consistent benchmark exposure. Best interest basis: cost advantage of $72,000 over 10 years per $1M invested, with no demonstrated value-add from active management for this client's objectives.

**Example 2 — Alternative Investment Screening**

Client: 62-year-old, $3.2M portfolio, moderate-conservative risk, needs $10K/month income starting in 2 years. Product: Private real estate fund, 5-year lock-up, 7% target yield, minimum $250K. Screening result: NOT SUITABLE. Reason: Client's 2-year income need conflicts with 5-year lock-up. At $250K investment, 7.8% of portfolio would be illiquid — acceptable, but the income timing mismatch is the critical issue. Alternative: Publicly traded REIT fund with daily liquidity, 4.2% yield, no lock-up. Lower yield but aligned with client's liquidity and income timing requirements.

## Guidelines

- Screen every product recommendation against at least 2 alternatives
- Document cost comparisons over the client's specific time horizon, not generic periods
- Never recommend a higher-cost product without an articulable, client-specific benefit
- Treat complexity as a risk factor — don't recommend Level 3–4 products without specific need
- Verify accreditation and minimum investment requirements BEFORE discussing with client
- Update product suitability assessments when either the product or the client changes materially
- Maintain the best interest determination file for each recommendation per SEC record retention rules
- Coordinate with compliance on any products flagged for heightened supervision

## Validation Checklist

- [ ] Product risk, cost, liquidity, complexity, and tax characteristics fully cataloged
- [ ] Client profile matching completed across all required dimensions
- [ ] At least 2 alternative products compared with documented selection rationale
- [ ] All material conflicts of interest identified, disclosed, and mitigated
- [ ] Portfolio fit assessed including overlap, diversification, and cost impact
- [ ] Reg BI best interest determination completed with all four obligations addressed
- [ ] Cost comparison uses client-specific time horizon and investment amount
- [ ] Accreditation and minimum investment requirements verified
- [ ] Post-recommendation monitoring framework established
- [ ] Documentation archived per SEC/FINRA record retention requirements
