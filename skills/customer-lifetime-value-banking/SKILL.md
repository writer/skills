---
name: customer-lifetime-value-banking
description: Build and analyze banking CLV models incorporating deposit stickiness, product adoption curves, attrition modeling, and relationship-level economics. Use when calculating customer lifetime value, optimizing acquisition spend, analyzing retention strategies, or evaluating customer segment profitability for strategic planning.

metadata:
  display_name: "Customer Lifetime Value Banking"
  short_description: "Model customer lifetime value for banking relationships"
  default_prompt: "Optimize my customer lifetime value banking and suggest the best next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Customer Lifetime Value — Banking

## Overview

Applies Customer Lifetime Value (CLV) modeling to banking relationships, incorporating deposit stickiness dynamics, product adoption and deepening curves, relationship attrition modeling, FTP-adjusted product economics, and credit risk through the customer lifecycle. Enables strategic decisions on customer acquisition investment, retention program ROI, segment prioritization, and channel optimization by quantifying the economic value each customer relationship generates over its expected lifetime.

## When to Use

- Calculating CLV by customer segment for strategic planning and resource allocation
- Determining maximum customer acquisition cost (CAC) for marketing investment optimization
- Evaluating the ROI of retention programs and loyalty initiatives
- Analyzing the lifetime profitability of different customer segments (mass market, mass affluent, HNW)
- Supporting product bundling and cross-sell strategy with CLV-based prioritization
- Assessing the long-term value impact of pricing or service model changes

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Customer data | Relationship tenure, demographics, product holdings, balances | Customer-level extract |
| Revenue data | NII, fee income by product per customer or segment | Revenue attribution |
| Cost data | Servicing costs by channel, product, and segment | Cost allocation |
| Attrition data | Historical attrition rates by segment, tenure cohort, product count | Survival analysis data |
| Product adoption | Cross-sell rates and timing by product, segment, and tenure | Transition probabilities |
| Deposit behavior | Balance trends, rate sensitivity, stickiness by product and segment | Behavioral data |
| Credit performance | Default rates, loss given default by customer segment | Credit data |
| Discount rate | Risk-adjusted discount rate for NPV calculation | Financial parameter |

## Methodology

### Step 1 — Define Customer Segments

Segment the customer base for differentiated CLV modeling:

**Segmentation dimensions:**
- **Value tier**: Mass market (<$100K total relationship), mass affluent ($100K-$1M), HNW ($1M-$10M), UHNW (>$10M)
- **Lifecycle stage**: New-to-bank (0-12 months), developing (1-3 years), mature (3-10 years), tenured (>10 years)
- **Engagement level**: Primary bank (payroll DD, bill pay, multiple products) vs. secondary (single product, low activity)
- **Channel preference**: Branch-primary, digital-primary, hybrid

Apply segments that are **actionable** (marketing can target them differently), **measurable** (data exists to classify customers), and **substantial** (large enough to justify differentiated strategies).

### Step 2 — Model Revenue Streams

Project future revenue by component for each segment:

**Deposit revenue (FTP-adjusted):**
- Current deposit balances × FTP value margin (FTP rate − deposit rate − operating cost)
- Balance growth trajectory: Model deposit balance evolution using segment-specific growth curves
- **Deposit stickiness modeling**: Estimate the behavioral maturity of deposits using:
  - Historical balance decay analysis (what % of balances remain after 1, 3, 5, 10 years?)
  - Vintage cohort analysis (how do balances evolve by origination vintage?)
  - Rate sensitivity: How much balance leakage occurs per 100bps rate differential with competitors?
  - Stickiness index = (Balance at t=N / Balance at t=0) for each product and segment

**Lending revenue:**
- Outstanding loan balances × FTP spread (customer rate − FTP rate)
- Probability of future loan adoption by product (mortgage, auto, HELOC, credit card)
- Loan balance trajectory based on typical amortization and refinancing patterns
- Origination fee income at expected adoption points

**Fee income:**
- Recurring fees: Account maintenance, advisory, card annual fees
- Transaction-based fees: Interchange (projected from transaction volume trends), wire fees, FX
- Wealth management: AUM-based fees projected from investable asset growth

**Cross-sell revenue acceleration:**
- Model the product adoption curve: Probability of adding the 2nd, 3rd, 4th product by year
- Revenue uplift per additional product: Incremental NII + fees from the new product
- Primary bank conversion premium: Revenue increase when a customer makes the institution their primary bank (typically 3-5x secondary bank relationship)

### Step 3 — Model Costs

Project costs across the customer lifecycle:

**Acquisition cost:**
- Marketing and advertising cost per acquired customer (by channel: branch walk-in, digital, referral, direct mail)
- Onboarding cost: Account opening, KYC/AML verification, initial product setup
- Promotional cost: Introductory rate premiums, sign-up bonuses, fee waivers

**Servicing cost:**
- Channel cost: Branch transaction cost ($4-8/visit), call center ($5-12/call), digital ($0.10-0.50/session)
- Product servicing: Statement generation, payment processing, collections
- Relationship management: RM compensation allocated to customer segment (for mass affluent and above)
- Compliance cost: Ongoing KYC refresh, transaction monitoring, regulatory reporting per customer

**Credit cost:**
- Expected loss = PD × LGD × EAD projected over the customer's lending lifecycle
- Provision for new lending at adoption points
- Loss rate typically varies by lifecycle stage (lower for mature, well-known customers)

### Step 4 — Model Attrition and Retention

Build a survival model for customer relationship duration:

**Attrition rate modeling:**
- Compute attrition rates by segment, tenure cohort, and product count
- Apply the **hazard function**: Attrition risk is typically highest in Year 1 (15-25% for mass market) and declines with tenure (3-5% for 5+ year relationships)
- **Product count effect**: Each additional product reduces attrition probability — model the retention multiplier (e.g., 1 product: 25% attrition, 2 products: 12%, 3+: 5%)
- **Deposit stickiness as retention predictor**: Customers with payroll direct deposit have 60-70% lower attrition rates

**Survival curve construction:**
- S(t) = Probability of surviving to year t
- S(t) = S(t-1) × (1 − Attrition Rate at t)
- Project S(t) for each segment over 20+ years
- **Expected lifetime** = Σ S(t) from t=1 to T (sum of survival probabilities)

**Retention program ROI:**
- Model the attrition rate reduction from specific retention interventions
- Calculate incremental CLV from retained customers
- ROI = Incremental CLV × Number Retained / Program Cost

### Step 5 — Calculate CLV

Compute Customer Lifetime Value as the net present value of future cash flows:

**CLV Formula:**
`CLV = Σ [S(t) × (Revenue(t) − Cost(t)) / (1 + r)^t] from t=1 to T`

Where:
- S(t) = Survival probability at year t
- Revenue(t) = Projected total revenue (NII + fees) at year t
- Cost(t) = Projected total cost (servicing + credit) at year t — exclude acquisition cost (sunk)
- r = Risk-adjusted discount rate (typically WACC or cost of equity: 10-14%)
- T = Modeling horizon (typically 20-30 years, with terminal value for perpetuity)

**CLV components to report:**
- **Gross CLV**: Total PV of revenue streams
- **Net CLV**: Gross CLV minus PV of servicing and credit costs
- **Net CLV after acquisition**: Net CLV minus acquisition cost (for CAC justification)
- **Marginal CLV**: Incremental CLV from one additional product or balance tier upgrade

### Step 6 — Perform Segment-Level Analysis

Analyze CLV across segments to drive strategic decisions:

**Segment CLV comparison:**
| Segment | Avg CLV | Expected Lifetime | Revenue/Yr | Cost/Yr | Acquisition Cost | CLV/CAC Ratio |
|---------|---------|-------------------|-----------|---------|-----------------|---------------|

**Key insights to extract:**
- Which segments have the highest CLV/CAC ratio (most efficient acquisition targets)?
- Where is the largest gap between current and potential CLV (cross-sell opportunity)?
- Which segments have the highest attrition-adjusted lifetime (longest and most stable)?
- What is the CLV impact of converting a secondary-bank relationship to primary-bank?

**Cohort vintage analysis:**
- Compare CLV trajectories of recent vintages to older vintages
- Identify whether CLV is trending up or down for new customer cohorts
- Assess whether acquisition channel affects long-term CLV (branch-acquired vs. digital-acquired)

### Step 7 — Generate Strategic Recommendations

Translate CLV insights into actionable strategies:

**Acquisition strategy:**
- Set maximum CAC by segment: CAC ≤ CLV × Target CLV/CAC Ratio (typically 3-5x)
- Prioritize acquisition channels with the highest CLV-per-acquisition-dollar
- Target segments with the highest marginal CLV opportunity

**Retention strategy:**
- Invest retention spend proportional to CLV at risk (high-CLV customers warrant higher retention investment)
- Prioritize cross-sell to customers in the 1-3 year tenure band (highest attrition risk, highest CLV uplift potential)
- Design loyalty programs that reward relationship deepening, not just tenure

**Pricing strategy:**
- Accept lower margins on products that serve as relationship anchors (high retention value)
- Price premium products at market for high-CLV segments where relationship stickiness provides pricing power
- Allocate promotional budget to segments with highest CLV/CAC improvement potential

## Output Specification

```markdown
# Customer Lifetime Value Analysis — [Date]

## CLV Summary by Segment
| Segment | Customers | Avg CLV | Avg Lifetime (Yrs) | Avg Revenue/Yr | Avg Cost/Yr | CLV/CAC |
|---------|-----------|---------|--------------------|----|-----|---------|

## CLV Component Breakdown
| Component | Mass Market | Mass Affluent | HNW | Total |
|-----------|------------|---------------|-----|-------|
| Deposit NII (PV) | | | | |
| Lending NII (PV) | | | | |
| Fee Income (PV) | | | | |
| Cross-Sell (PV) | | | | |
| Servicing Cost (PV) | | | | |
| Credit Cost (PV) | | | | |
| **Net CLV** | | | | |

## Attrition and Retention Analysis
| Segment | Year 1 Attrition | Year 5 Attrition | Expected Lifetime | Products Effect |
|---------|-----------------|-----------------|-------------------|-----------------|

## Deposit Stickiness Metrics
| Product | 1-Yr Retention | 3-Yr Retention | 5-Yr Retention | Stickiness Index | Rate Sensitivity |
|---------|---------------|---------------|---------------|-----------------|-----------------|

## Strategic Recommendations
| # | Strategy | Target Segment | CLV Impact ($M) | Investment ($M) | ROI |
|---|----------|---------------|----------------|-----------------|-----|

## Acquisition Economics
| Channel | CAC | Avg CLV | CLV/CAC | Recommendation |
|---------|-----|---------|---------|----------------|
```

## Analysis Framework

Apply the **CLV Value Lever Framework**:
1. **Extend** (increase relationship lifetime): Reduce attrition through product deepening, service excellence, and proactive retention
2. **Expand** (increase annual revenue): Cross-sell additional products, grow balances through relationship pricing, convert to primary bank
3. **Economize** (reduce cost-to-serve): Migrate servicing to lower-cost channels, automate routine processes, optimize credit decisioning
4. **Acquire efficiently** (lower CAC): Target high-CLV-propensity prospects, optimize channel mix, leverage referral networks

Each lever independently increases CLV; the combined effect is multiplicative.

## Examples

**Example — CLV Segment Comparison:**
"Mass affluent customers ($250K-$1M total relationship) generate average CLV of $8,420 over a projected 14.2-year lifetime, representing 31% of total customer value from 8% of the customer base. Their CLV/CAC ratio of 6.8x significantly exceeds the mass market ratio of 2.1x, driven by higher deposit balances (average $185K, generating $4,200 annual FTP value), lower attrition (4.2% annual vs. 11.8% for mass market), and superior cross-sell adoption (2.8 products vs. 1.6). Recommendation: Increase mass affluent acquisition spend by 40% and launch a dedicated relationship management program for mass affluent households in the $500K-$1M tier."

**Example — Deposit Stickiness Impact on CLV:**
"Deposit stickiness analysis reveals that customers with payroll direct deposit retain 89% of their deposit balance after 5 years versus 52% for customers without DD. This stickiness differential translates to a $2,340 CLV premium (+38% vs. non-DD customers). The DD conversion cost is $45/customer (promotional incentive), yielding a 52x return. Recommendation: Launch an aggressive DD conversion campaign targeting the 180K checking account customers without active DD, prioritizing the mass affluent segment."

## Guidelines

- Use FTP-adjusted revenue, not gross interest income, for CLV calculations
- Model attrition as a declining hazard function, not a flat annual rate
- Include the product count effect on retention — it is the single strongest retention predictor in banking
- Apply deposit stickiness modeling at the product level (checking vs. savings vs. CD)
- Discount future cash flows at the cost of equity, not a lower rate — CLV should reflect equity-investor returns
- Validate CLV models using out-of-sample backtesting on historical cohorts
- Update CLV models at least semi-annually to incorporate behavioral changes and rate environment shifts

## Validation Checklist

- [ ] Customer segments are actionable, measurable, and substantial
- [ ] Revenue streams modeled at the product level with FTP-adjusted margins
- [ ] Deposit stickiness modeled with balance decay curves by product and segment
- [ ] Attrition rates reflect tenure-dependent hazard functions, not flat rates
- [ ] Product count effect on retention quantified and incorporated
- [ ] Acquisition costs captured by channel with all components (marketing, onboarding, promotional)
- [ ] Discount rate reflects cost of equity (10-14%), not risk-free rate
- [ ] CLV validated through backtesting on historical cohorts
- [ ] CLV/CAC ratios computed and compared across segments and channels
- [ ] Strategic recommendations quantified with CLV impact and investment ROI
