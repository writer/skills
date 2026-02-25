---
name: product-profitability-analysis
description: Analyze product-level profitability using FTP-adjusted margins, fully allocated costs, and risk-adjusted returns for banking products. Use when evaluating product line economics, performing product rationalization analysis, optimizing pricing strategies, or supporting ALCO capital allocation decisions.

metadata:
  display_name: "Product Profitability Analysis"
  short_description: "Analyze bank product profitability with FTP-adjusted margins"
  default_prompt: "Analyze my product profitability and recommend clear next actions"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Product-Level Profitability Analysis

## Overview

Decomposes banking product profitability to the unit economics level using funds transfer pricing (FTP), activity-based costing (ABC), credit cost allocation, and risk-adjusted return metrics. Enables management to identify value-creating vs. value-destroying products, optimize the product mix, calibrate pricing, and allocate capital efficiently across business lines.

## When to Use

- Evaluating the economic contribution of individual banking products
- Performing product rationalization or product line simplification reviews
- Calibrating product pricing against FTP-adjusted breakeven
- Supporting ALCO capital allocation decisions across business lines
- Analyzing cross-subsidy dynamics between products and customer segments
- Benchmarking product economics against peers or market rates

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Product balances | Average balances by product line (assets and liabilities) | Balance data |
| Customer rates | Interest rates charged/paid by product | Rate schedule |
| FTP rates | Transfer pricing rates by product tenor/repricing profile | FTP schedule |
| Fee income | Non-interest income attributable to each product | Revenue data |
| Direct costs | Direct operating costs by product (origination, servicing, collections) | Cost data |
| Indirect costs | Allocated overhead (technology, compliance, management) | Allocation methodology |
| Credit costs | Expected loss and provision expense by product portfolio | Credit data |
| Capital allocation | RWA and economic capital by product | Capital data |
| Volume data | Account counts, transaction volumes, utilization rates | Activity data |

## Methodology

### Step 1 — Calculate FTP-Adjusted Net Interest Margin by Product

For each product, compute the FTP spread:

**Asset products (loans, investments):**
`FTP Spread = Customer Rate − FTP Rate`
- The FTP rate represents the internal cost of funding the asset at its maturity/repricing profile
- Positive FTP spread = product contributes positively to NII after funding cost

**Liability products (deposits):**
`FTP Spread = FTP Rate − Customer Rate`
- The FTP rate represents the internal value of the funding provided to treasury
- Positive FTP spread = product provides funding at a cost below its internal value

**FTP-adjusted NII per product:**
`NII_product = FTP Spread × Average Balance`

Decompose FTP into components:
- **Base rate** (risk-free benchmark at the product's repricing tenor)
- **Liquidity premium** (compensation for LCR/NSFR impact of the product)
- **Credit spread** (for asset products, the funding spread above risk-free)
- **Option cost** (for products with embedded options: prepayment, early withdrawal)

### Step 2 — Allocate Non-Interest Income

Assign fee and non-interest income directly to products where possible:

- **Direct fees**: Origination fees, annual fees, transaction fees, late fees, interchange
- **Indirect fees**: Wealth management referral fees, cross-sell revenue attributable to the relationship
- **Ancillary income**: Insurance premiums, brokerage commissions linked to the product relationship

Apply the **revenue attribution principle**: Revenue is attributed to the product that generates the customer interaction, not the product where it is booked. Cross-sell revenue should be shared using a defined attribution model.

### Step 3 — Allocate Operating Costs Using Activity-Based Costing

Apply ABC methodology to allocate costs accurately:

**Direct costs (fully traceable):**
- Origination/underwriting costs per unit originated
- Servicing costs per account per month
- Collections costs per delinquent account
- Technology costs directly attributable (product-specific platforms)

**Indirect costs (allocated):**
- Branch network costs: Allocate based on transaction volumes or customer visits by product
- Technology infrastructure: Allocate based on system usage, data storage, or processing volumes
- Compliance and regulatory: Allocate based on regulatory intensity (AML monitoring costs higher for transaction accounts)
- Management and overhead: Allocate using a cost driver hierarchy (headcount, revenue, or balance-based)

**Cost allocation hierarchy:**
1. Direct assignment (preferred — highest accuracy)
2. Activity-based allocation (where direct assignment not possible)
3. Balance-based or revenue-based allocation (last resort — lowest accuracy)

Clearly identify the allocation methodology tier used for each cost category.

### Step 4 — Compute Credit Costs and Expected Losses

Allocate credit-related costs to asset products:

- **Expected credit loss (ECL)**: PD × LGD × EAD for the product portfolio, reflecting through-the-cycle loss expectations
- **Provision expense**: Actual provision charges recorded in the period (may differ from ECL due to IFRS 9 staging, macro scenario weights)
- **Net charge-offs**: Actual losses realized, net of recoveries
- **ECL cost rate**: ECL / Average Balance (expressed in bps annually)

For liability products, credit cost is zero but allocate fraud loss costs where applicable.

### Step 5 — Calculate Risk-Adjusted Returns

Compute risk-adjusted profitability metrics for each product:

**Product Economic Profit (EP):**
`EP = FTP-Adjusted NII + Fee Income − Operating Costs − Credit Costs − Capital Charge`

Where Capital Charge = Allocated RWA × Target CET1 Ratio × Cost of Equity

**Key return metrics:**
- **RAROC**: EP / Economic Capital — risk-adjusted return on capital
- **RoRWA**: Net Income (after all costs) / RWA — return on regulatory capital
- **EP per account**: EP / Number of accounts — unit economics measure
- **EP per dollar of balance**: EP / Average Balance — balance sheet efficiency
- **Cost-to-income ratio**: Operating Costs / (NII + Fees) — operational efficiency

**Hurdle rate test:**
- Products with RAROC above the cost of equity are value-creating
- Products with RAROC below the cost of equity destroy shareholder value
- Products with negative EP should be examined for cross-subsidy justification or rationalization

### Step 6 — Analyze Cross-Subsidy Dynamics

Identify and quantify cross-subsidy flows between products:

- Map which products subsidize others (e.g., low-rate checking accounts funded by high-spread lending)
- Assess whether cross-subsidies are intentional (strategic bundling) or accidental (mispricing)
- Evaluate the customer relationship economics: Does a loss-making product anchor a profitable relationship?
- Compute the **relationship-level EP**: Sum of all product EPs for multi-product customers

**Cross-subsidy matrix:**
| Product | Standalone EP | Relationship Contribution | Net Position |
|---------|---------------|---------------------------|-------------|
| Checking | Negative | High anchoring value | Subsidized |
| Mortgage | Low positive | Drives checking + wealth | Contributor |
| Wealth | High positive | Primary profit driver | Subsidizer |

### Step 7 — Generate Optimization Recommendations

Based on the analysis, recommend specific actions:

**Pricing optimization:**
- Products priced below FTP-adjusted breakeven: Identify repricing opportunity
- Products with RAROC significantly above hurdle: Assess competitive positioning and market share growth opportunity
- Fee income opportunities: Identify below-market fee schedules

**Product rationalization:**
- Products with negative EP, no cross-subsidy justification, and declining volumes: Candidates for discontinuation
- Products with low EP but high strategic value (customer acquisition, retention): Re-evaluate pricing and cost structure

**Capital reallocation:**
- Redirect capital from low-RAROC products to high-RAROC products
- Quantify the incremental EP from reallocation (RAROC differential × capital shifted)

**Cost reduction:**
- Products with cost-to-income ratios significantly above peers: Target for operational efficiency improvement
- Migration from high-cost channels (branch) to low-cost channels (digital)

## Output Specification

```markdown
# Product Profitability Analysis — [Period]

## Product Economics Summary
| Product | Avg Bal ($M) | FTP Spread (bps) | Fee ($M) | OpEx ($M) | Credit ($M) | EP ($M) | RAROC | RoRWA |
|---------|-------------|------------------|----------|-----------|-------------|---------|-------|-------|

## Product Ranking by RAROC
| Rank | Product | RAROC | Hurdle Rate | Value Creation | Recommendation |
|------|---------|-------|-------------|----------------|----------------|

## FTP Decomposition
| Product | Customer Rate | FTP Rate | Base | Liquidity | Credit | Option | FTP Spread |
|---------|--------------|----------|------|-----------|--------|--------|-----------|

## Cost Allocation Summary
| Product | Direct Cost | Allocated Cost | Total Cost | Cost/Account | Cost-to-Income |
|---------|------------|----------------|-----------|-------------|---------------|

## Cross-Subsidy Analysis
| Subsidizing Product | Subsidized Product | Subsidy Amount ($M) | Justification |
|--------------------|-------------------|--------------------|----|

## Optimization Recommendations
| # | Action | Product | EP Impact ($M) | Implementation | Priority |
|---|--------|---------|----------------|----------------|----------|
```

## Analysis Framework

Apply the **Product Value Chain** framework:
1. **Originate**: What does it cost to acquire the customer and originate the product?
2. **Fund**: What is the internal cost (FTP) of funding the asset or value of the deposit?
3. **Service**: What is the ongoing cost to maintain and service the product?
4. **Risk**: What credit, market, or operational losses does the product generate?
5. **Capitalize**: What regulatory and economic capital does the product consume?
6. **Return**: What is the net economic value after accounting for all five prior stages?

Products that fail to generate positive economic value at Stage 6, after accounting for relationship-level cross-subsidies, are candidates for repricing, restructuring, or rationalization.

## Examples

**Example — Product RAROC Analysis:**
"Commercial real estate lending generates the highest RAROC at 18.2%, driven by a 285bps FTP spread and strong fee income from origination and unused commitment fees. However, it consumes 34% of total allocated capital at an RWA density of 92%. Residential mortgages, by contrast, earn a RAROC of only 8.4% — below the 12% hurdle rate — reflecting compressed FTP spreads of 95bps and elevated servicing costs of $145/loan/year. The mortgage product destroys $12M of shareholder value annually but anchors $3.2B of core deposit relationships with combined positive EP."

**Example — Cross-Subsidy Insight:**
"The free checking account product generates negative EP of -$28M annually (operating cost of $164/account exceeds the FTP value of $112/account). However, 72% of checking customers hold at least one additional product with the bank. Relationship-level analysis shows that multi-product households anchored by checking generate average EP of $340/household, making the cross-subsidy economically rational. Recommendation: Maintain the product but migrate servicing to digital channels to reduce cost-to-serve by $35/account."

## Guidelines

- Always use FTP-adjusted margins, never gross interest margins, for product economics
- Apply ABC costing where possible; clearly flag balance-based allocations as lower accuracy
- Include the capital charge in all EP calculations — products consuming capital must earn above the cost of equity
- Assess cross-subsidies at the relationship level before recommending product rationalization
- Express RAROC, RoRWA, and EP in consistent units for cross-product comparability
- Benchmark product economics against peers and best-in-class to identify improvement potential
- Update product profitability analysis at least quarterly to capture rate and volume changes

## Validation Checklist

- [ ] FTP rates correctly matched to each product's repricing/maturity profile
- [ ] FTP spreads decomposed into base, liquidity, credit, and option components
- [ ] Fee income attributed to originating product with cross-sell allocation documented
- [ ] Operating costs allocated using ABC hierarchy with methodology tier identified
- [ ] Credit costs reflect through-the-cycle expected losses, not single-period provisions
- [ ] Capital charge computed using allocated RWA × target CET1 × cost of equity
- [ ] RAROC compared to cost-of-equity hurdle rate for value creation assessment
- [ ] Cross-subsidy analysis performed at relationship level before rationalization recommendations
- [ ] Optimization recommendations quantified with EP impact
- [ ] Peer benchmarking applied to cost ratios and return metrics
