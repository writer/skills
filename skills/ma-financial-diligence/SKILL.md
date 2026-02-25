---
name: ma-financial-diligence
description: Conduct M&A financial due diligence analysis for bank acquisitions including accretion/dilution modeling, fair value marks, cost synergy validation, and pro-forma capital impact. Use when evaluating bank acquisition targets, preparing deal committee materials, analyzing merger economics, or assessing financial institution M&A feasibility.

metadata:
  display_name: "M&A Financial Diligence"
  short_description: "Run financial due diligence for bank M&A transactions"
  default_prompt: "Analyze my m a financial diligence and recommend clear next actions"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# M&A Financial Due Diligence

## Overview

Provides a structured framework for financial due diligence in bank M&A transactions, covering earnings quality assessment, balance sheet fair value adjustments, accretion/dilution analysis, cost and revenue synergy validation, pro-forma capital and liquidity impact, and deal pricing evaluation. Designed for deal committee presentations, board approval packages, and regulatory application support (OCC/FDIC/Fed merger applications).

## When to Use

- Evaluating a potential bank or financial institution acquisition target
- Building or reviewing accretion/dilution models for proposed transactions
- Assessing fair value marks on target loan portfolios, securities, and deposits
- Validating cost and revenue synergy assumptions
- Preparing financial analysis sections of regulatory merger applications
- Presenting deal economics to board of directors or deal committee

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Target financials | 3-5 years of income statement, balance sheet, regulatory filings | Call reports / 10-K/Q |
| Acquirer financials | Same period financial statements for the acquiring institution | Financial statements |
| Target loan tape | Loan-level data (balances, rates, maturities, grades, collateral) | Loan detail extract |
| Securities portfolio | CUSIP-level holdings with book value, market value, duration | Investment detail |
| Deposit composition | Account-level or product-level deposit data with rates and maturities | Deposit detail |
| Deal terms | Purchase price, consideration mix (cash/stock), exchange ratio | Term sheet |
| Synergy assumptions | Cost savings by category, revenue synergies, timing | Management estimates |
| Market data | Comparable transaction multiples, trading multiples | M&A comps data |

## Methodology

### Step 1 — Assess Target Earnings Quality

Evaluate the sustainability and quality of the target's reported earnings:

**NII quality:**
- Decompose NIM into asset yield, cost of funds, and free-funds contribution
- Identify non-recurring interest income (accretion from prior deals, penalty income, one-time items)
- Assess the proportion of NII from purchase accounting accretion on prior acquisitions (declining asset)
- Evaluate the loan portfolio yield relative to current origination rates (above-market = roll-off risk)

**Fee income quality:**
- Separate recurring fees (service charges, wealth management) from volatile income (trading, gain on sale)
- Identify fee income dependent on the rate environment (mortgage banking volumes)
- Assess customer retention risk for fee-generating relationships

**Expense normalization:**
- Identify one-time costs (restructuring, litigation settlements, deal costs from prior M&A)
- Normalize compensation for above/below-market levels or unfunded pension obligations
- Assess technology and infrastructure spend: underinvestment creating future catch-up requirements

**Core earnings run-rate:** Adjusted net income after removing non-recurring items, representing sustainable earnings power.

### Step 2 — Mark the Balance Sheet to Fair Value

Estimate fair value adjustments (purchase accounting marks) on major balance sheet categories:

**Loan portfolio mark:**
- Apply credit mark: Estimate remaining lifetime losses above the existing allowance using loan-level analysis (PD × LGD × EAD) and stress-adjusted scenarios
- Apply rate mark: Discount contractual cash flows at current market rates — below-market fixed-rate loans receive a negative mark, above-market a positive mark
- Segment by loan type (CRE, C&I, resi mortgage, consumer) and apply distinct discount rates and loss assumptions
- Total loan mark = Credit mark + Rate mark (typically a net negative in rising-rate environments)

**Securities mark:**
- Mark all AFS and HTM securities to current market value
- HTM securities often carry significant unrealized losses in rising-rate environments — these crystallize in a purchase
- Apply haircuts for illiquid or structured securities

**Deposit intangible (CDI):**
- Core deposit intangible reflects the value of the below-market-rate deposit franchise
- Calculate as: PV of the cost savings from paying deposit rates below wholesale funding rates over the expected life of the deposit base
- Typical valuation: 1-3% of core deposits, amortized over 7-10 years
- Apply deposit decay assumptions based on historical attrition rates

**Other fair value adjustments:**
- Fixed assets: Appraisal vs. book value
- Trust preferred or subordinated debt: Mark to current market spreads
- Lease obligations: Fair value adjustment for above/below-market leases
- Contingent liabilities: Legal, regulatory, environmental exposures

### Step 3 — Build the Accretion/Dilution Model

Compute the EPS impact of the transaction on the acquirer:

**Key model components:**
- **Target's contribution**: Core earnings run-rate (from Step 1)
- **Purchase accounting adjustments**: Amortization of loan mark (accretive as discount accretes into income), amortization of CDI (reduces income), amortization of securities mark
- **Cost synergies**: Phased-in expense reductions (typically 25-35% of target's non-interest expense)
- **Revenue synergies**: Cross-sell, de novo revenue (apply significant haircut — typically 50% of management estimate)
- **Funding cost impact**: Any change in the combined entity's funding cost
- **Share dilution**: Additional shares issued in stock transactions
- **Financing cost**: Interest expense on debt financing for cash transactions

**Accretion/dilution calculation:**
`Pro-forma EPS = (Acquirer Earnings + Target Core Earnings + Synergies + PA Adjustments − Financing Costs) / Pro-forma Shares`
`A/D = (Pro-forma EPS − Standalone Acquirer EPS) / Standalone Acquirer EPS`

Model over a 5-year horizon showing crossover from dilutive to accretive (if applicable).

### Step 4 — Assess Pro-Forma Capital and Liquidity Impact

Evaluate regulatory capital and liquidity impact of the combination:

**Capital impact:**
- Goodwill creation: Purchase price − Target's fair-value-adjusted net assets = Goodwill
- Goodwill is deducted from CET1 capital (significant negative impact)
- Pro-forma CET1 ratio: (Combined CET1 − Goodwill) / Combined RWA
- Assess whether the combined entity requires a capital raise to maintain target ratios
- Model capital trajectory under internal capital generation assumptions

**Liquidity impact:**
- Combined LCR and NSFR with pro-forma adjustments
- Assess target's funding profile stability (concentration risk, brokered deposits, FHLB reliance)
- Evaluate incremental borrowing capacity at FHLB and the discount window
- Model pro-forma deposit concentration and diversification benefits

### Step 5 — Validate Synergy Assumptions

Critically assess the achievability of projected synergies:

**Cost synergies (higher confidence):**
- Branch overlap: Map branch networks, identify overlapping markets, estimate closable branches × average branch cost
- Back-office consolidation: Technology platform migration, operations centers, shared services
- Compensation: Eliminate duplicate senior management, overlapping roles
- Vendor rationalization: Consolidate contracts at better pricing
- Apply realistic phase-in: 25% Year 1, 75% Year 2, 100% Year 3
- One-time restructuring costs: Typically 150-200% of annual synergies

**Revenue synergies (lower confidence):**
- Cross-sell: Target's customer base × acquirer's superior product set × take-up rate
- Apply significant haircut (50-75%) to management revenue synergy estimates
- Revenue synergies typically take 2-3 years to materialize and have high execution risk
- Never model revenue synergies as the primary economic justification for a deal

### Step 6 — Evaluate Deal Pricing

Assess whether the price represents fair value:

**Valuation multiples:**
- Price / Tangible Book Value (P/TBV): Compare to precedent transactions and trading multiples
- Price / Core Earnings (P/E): Based on normalized core earnings, not GAAP
- Core deposit premium: (Purchase Price − Target TBV) / Core Deposits
- Premium to market: % above target's current trading price (for public targets)

**Breakeven analysis:**
- Cost synergies required for break-even accretion (what percentage of target opex must be eliminated?)
- Tangible book value earnback period: Years for acquirer's TBV per share to recover to pre-deal level through retained earnings
- IRR of the investment: Discount rate at which NPV of target's future cash flows equals purchase price

### Step 7 — Compile the Due Diligence Assessment

Structure the output as a comprehensive deal assessment:
1. **Transaction summary**: Price, structure, strategic rationale
2. **Earnings quality**: Normalized core earnings and sustainability assessment
3. **Fair value marks**: Balance sheet adjustments with total goodwill estimation
4. **Accretion/dilution**: 5-year EPS trajectory with crossover point
5. **Capital and liquidity impact**: Pro-forma ratios and trajectory
6. **Synergy assessment**: Validated cost and revenue synergies with confidence levels
7. **Pricing evaluation**: Multiples comparison and breakeven analysis
8. **Key risks**: Deal-specific risks and mitigants
9. **Recommendation**: Proceed / Renegotiate / Decline with supporting rationale

## Output Specification

```markdown
# M&A Financial Due Diligence — [Target Name]

## Transaction Summary
- Purchase price: $[X]M ([Y]x P/TBV, [Z]x P/E)
- Consideration: [% cash / % stock]
- Core deposit premium: [X]%
- Strategic rationale: [Brief statement]

## Earnings Quality Assessment
| Metric | Reported | Adjustments | Core Run-Rate |
|--------|----------|-------------|---------------|
| NII | | | |
| Fee Income | | | |
| Expenses | | | |
| Provisions | | | |
| Net Income | | | |

## Fair Value Marks ($M)
| Category | Book Value | Fair Value | Mark | Key Assumptions |
|----------|-----------|-----------|------|-----------------|
| Loan portfolio | | | | |
| Securities | | | | |
| CDI | n/a | | | |
| Fixed assets | | | | |
| Deposits (premium) | | | | |
| **Net adjustments** | | | **[Total]** | |
| **Goodwill** | | | **[Total]** | |

## Accretion/Dilution Summary
| | Year 1 | Year 2 | Year 3 | Year 4 | Year 5 |
|------------|--------|--------|--------|--------|--------|
| EPS Impact | | | | | |
| A/D % | | | | | |

## Pro-Forma Capital & Liquidity
| Metric | Acquirer | Pro-Forma | Target | Impact |
|--------|----------|-----------|--------|--------|
| CET1 | | | ≥[X]% | |
| Leverage | | | ≥[Y]% | |
| LCR | | | ≥100% | |

## Synergy Assessment
| Category | Mgmt Estimate ($M) | Validated ($M) | Confidence | Phase-in |
|----------|--------------------|--------------------|------------|----------|

## Pricing Evaluation
| Multiple | This Deal | Precedent Median | Premium/(Discount) |
|----------|-----------|------------------|--------------------|

TBV Earnback: [X] years | Deal IRR: [Y]%

## Key Risks
1. [Risk with probability and mitigation]

## Recommendation
[Proceed / Renegotiate / Decline with rationale]
```

## Analysis Framework

Apply the **Three Tests of Deal Value**:
1. **Strategic test**: Does the target fill a genuine strategic gap (geography, capability, scale)?
2. **Financial test**: Is the transaction accretive within 2 years with realistic (not aspirational) synergies?
3. **Execution test**: Can the integration be executed without disrupting either institution's operations or customers?

A deal should pass all three tests before receiving a positive recommendation. Financial attractiveness alone does not justify execution risk.

## Examples

**Example — Accretion/Dilution Summary:**
"At the proposed price of 1.65x TBV ($342M), the transaction is 3.2% dilutive to EPS in Year 1 primarily due to CDI amortization and restructuring charges. With validated cost synergies of $28M (32% of target non-interest expense), the deal crosses to accretive in Q3 of Year 2, reaching 4.8% accretive by Year 3. TBV per share declines from $28.42 to $26.15 at close, with an earnback period of 3.4 years through retained earnings and synergy realization."

**Example — Fair Value Mark Narrative:**
"The loan portfolio carries a net negative mark of $67M (3.8% of book value), comprising a $42M credit mark reflecting estimated additional lifetime losses in the CRE portfolio above existing reserves, and a $25M rate mark on $480M of fixed-rate residential mortgages originated at 3.25% average coupon. The credit mark is driven by 12 classified CRE relationships totaling $184M with updated appraisals showing LTVs of 85-110%. The rate mark accretes into income over the portfolio's 6.2-year weighted average life."

## Guidelines

- Always normalize target earnings before applying valuation multiples
- Apply independent credit judgment on the loan portfolio — do not rely solely on target's internal grades
- Model accretion/dilution over 5 years, not just Year 1
- Haircut revenue synergies by at least 50% from management estimates
- Include one-time restructuring costs in accretion/dilution (not just run-rate synergies)
- Assess pro-forma capital impact including full goodwill deduction from CET1
- Compare deal pricing to both precedent transactions and current trading multiples
- Never justify a deal primarily on revenue synergies — cost synergies must independently support the price

## Validation Checklist

- [ ] Target earnings normalized for non-recurring items with clear adjustments documented
- [ ] Loan portfolio mark reflects both credit and rate components
- [ ] CDI valuation uses appropriate deposit decay and discount rate assumptions
- [ ] Goodwill calculated as purchase price minus fair-value-adjusted net assets
- [ ] Accretion/dilution model includes PA amortization, synergies, restructuring, and financing costs
- [ ] Pro-forma CET1 ratio computed with full goodwill deduction
- [ ] Cost synergies benchmarked against comparable transactions (25-35% of target OpEx)
- [ ] Revenue synergies haircut by ≥50% from management estimates
- [ ] Deal multiples compared to precedent transactions and current trading multiples
- [ ] TBV earnback period and deal IRR calculated and assessed against thresholds
