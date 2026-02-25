---
name: pricing-strategy-evaluation
description: Evaluate pricing strategy effectiveness for banking products including FTP-adjusted breakeven analysis, price elasticity, competitive positioning, and margin optimization. Use when reviewing deposit or loan pricing, assessing pricing power, analyzing rate sensitivity of volumes, or optimizing relationship pricing strategies.

metadata:
  display_name: "Pricing Strategy Evaluation"
  short_description: "Evaluate bank deposit and loan pricing effectiveness"
  default_prompt: "Evaluate my pricing strategy results and recommend clear next actions"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Pricing Strategy Evaluation

## Overview

Provides a structured methodology for evaluating and optimizing banking product pricing by integrating FTP-adjusted economics, competitive analysis, price elasticity estimation, customer segmentation, and regulatory constraints. Covers both asset-side (loan) and liability-side (deposit) pricing with attention to relationship-level value, cross-product bundling, and the tension between margin maximization and volume/market-share objectives.

## When to Use

- Reviewing the competitiveness and profitability of deposit rate schedules
- Evaluating loan pricing adequacy against FTP-adjusted hurdle rates
- Analyzing the price sensitivity of deposit volumes (deposit beta optimization)
- Assessing relationship pricing and bundling strategies
- Responding to competitive pricing pressure with data-driven recommendations
- Preparing pricing committee or ALCO pricing strategy reviews

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Current pricing | Posted rates and fee schedules by product and tier | Rate cards |
| FTP rates | Internal transfer pricing rates by product maturity/repricing | FTP schedule |
| Volume data | Account volumes, balances, and flows by rate tier | Product data |
| Competitive rates | Peer and market rate intelligence by product | Market data |
| Customer data | Segment, relationship depth, product holdings, attrition rates | CRM data |
| Cost data | FTP-adjusted product costs (origination, servicing, credit) | Cost analysis |
| Historical pricing | Prior rate changes with corresponding volume/balance impacts | Time series |
| Elasticity estimates | Price sensitivity data from prior changes or econometric analysis | Statistical data |

## Methodology

### Step 1 — Establish the FTP-Adjusted Pricing Framework

Compute the pricing architecture for each product:

**Asset products (loans) — Minimum Pricing:**
`Minimum Rate = FTP Rate + Expected Loss Rate + Operating Cost Rate + Capital Charge Rate`

Where:
- FTP Rate: Internal cost of funds at the loan's repricing/maturity profile
- Expected Loss Rate: Through-the-cycle PD × LGD annualized
- Operating Cost Rate: Origination + servicing costs annualized per dollar of balance
- Capital Charge Rate: (RWA Density × Target CET1%) × Cost of Equity, annualized

`Target Rate = Minimum Rate + Target Profit Margin`
`Pricing Power = Actual Rate − Minimum Rate` (positive = value creation)

**Liability products (deposits) — Maximum Pricing:**
`Maximum Rate = FTP Rate − Operating Cost Rate − Capital Charge Rate − Target Profit Margin`

The FTP rate represents the value of the deposit to treasury; the maximum rate is the highest rate that can be offered while still generating positive economic profit.

`Deposit Value Margin = FTP Rate − Customer Rate − Operating Cost Rate`

### Step 2 — Analyze Competitive Positioning

Map current pricing against the competitive landscape:

**Rate positioning matrix:**
For each product, plot the institution's rate against the market distribution:
- **Quartile ranking**: Q1 (highest/most competitive) through Q4 (lowest/least competitive)
- **Spread to market median**: Difference in bps from the median competitor rate
- **Spread to market leader**: Difference from the most aggressive competitor

**Competitive response analysis:**
- Identify which competitors are pricing leaders (first to move) vs. followers
- Assess competitors' strategic intent: Are they pricing for growth, retention, or margin?
- Determine the institution's price-setting role in the market
- Track competitive pricing changes with a 30/60/90-day lag analysis

**Digital vs. branch pricing:**
- Compare online-only rates (typically 25-75bps higher for deposits, tighter for loans)
- Assess whether the institution is losing volume to digital competitors
- Evaluate whether a dual pricing strategy (branch vs. digital) is appropriate

### Step 3 — Estimate Price Elasticity

Quantify how volume and balances respond to price changes:

**Deposit price elasticity:**
- **Beta (pass-through rate)**: ΔDeposit Rate / ΔBenchmark Rate — measures how much deposit rates move when benchmark rates change
- **Volume elasticity**: %ΔBalance / %ΔRate — measures balance sensitivity to own-rate changes
- **Cross-elasticity**: %ΔBalance / %ΔCompetitor Rate — measures sensitivity to competitor rate changes

Segment elasticity by:
- Product type (demand deposits are rate-insensitive; CDs are highly rate-elastic)
- Customer segment (mass market is less elastic than affluent; institutional is most elastic)
- Balance tier (large balances are more rate-sensitive than small balances)
- Channel (branch-acquired deposits less elastic than online-acquired)

**Loan price elasticity:**
- **Win rate analysis**: Loan approval-to-close ratio at different pricing tiers
- **Competitive loss analysis**: Deals lost to competitors by pricing differential
- **Volume response**: Origination volume change following rate adjustments

### Step 4 — Evaluate Relationship Pricing Dynamics

Assess pricing in the context of total customer relationships:

**Relationship value analysis:**
- Total relationship revenue: Sum of NII + fees across all products held by the customer
- Relationship depth: Number of products, tenure, transaction activity
- Cross-sell potential: Estimated incremental revenue from additional product adoption

**Pricing tier structure:**
- Evaluate whether pricing tiers (based on relationship depth or total balances) are appropriately calibrated
- Assess the breakpoints: Are tier thresholds aligned with natural customer segmentation?
- Analyze the share of customers near tier boundaries who could be nudged up with modest incentives

**Bundling effectiveness:**
- Measure the take-up rate on bundled pricing offers
- Quantify the retention benefit of bundled relationships (lower attrition)
- Calculate the net economic impact: pricing concession cost vs. retention/cross-sell benefit

### Step 5 — Perform Margin Sensitivity Analysis

Model the P&L impact of pricing changes across scenarios:

**Deposit pricing scenarios:**
- Base case: Current pricing maintained
- Competitive match: Raise rates to market median — quantify balance retention vs. cost increase
- Growth pricing: Raise rates to Q1 — quantify projected balance growth vs. margin compression
- Margin protection: Maintain rates below market — quantify projected balance attrition vs. NII preservation

For each scenario, compute:
- Projected balance trajectory (using elasticity estimates)
- NII impact = ΔBalance × FTP Spread + Balance × ΔRate
- Net EP impact after volume and rate effects

**Loan pricing scenarios:**
- Tighten pricing (wider spreads): Higher margin per loan, lower volume
- Loosen pricing (narrower spreads): Lower margin per loan, higher volume
- Selective pricing: Differentiate by risk grade, relationship depth, or sector

**Optimal pricing point:** The rate that maximizes total economic profit (not margin per unit or volume independently). This is the point where marginal revenue from additional volume equals marginal cost of the rate concession.

### Step 6 — Assess Regulatory and Conduct Constraints

Evaluate regulatory limitations on pricing:

- **Usury limits**: State-specific rate caps on consumer lending
- **Fair lending**: Pricing differentials across demographic groups must be explainable by risk factors
- **UDAAP**: Pricing practices must not be unfair, deceptive, or abusive
- **Rate parity**: If offering promotional rates, assess cannibalization of existing book
- **Deposit rate caps**: Institutions under regulatory orders may face deposit rate restrictions (e.g., less-than-well-capitalized institutions)

Document any pricing constraints that limit the theoretical optimal pricing strategy.

### Step 7 — Formulate Pricing Recommendations

Synthesize findings into actionable pricing recommendations:

1. **Product-level pricing changes**: Specific rate adjustments with projected impact on volumes, NII, and EP
2. **Tier structure modifications**: Adjustments to tier breakpoints or relationship pricing incentives
3. **Competitive response protocol**: Decision framework for responding to competitor rate changes (match, partially match, hold)
4. **Deposit beta strategy**: Target pass-through rates for the next rate cycle (hiking vs. cutting)
5. **Exception pricing governance**: Framework for relationship managers to deviate from posted rates (approval levels, minimum hurdle rates, documentation requirements)
6. **Monitoring framework**: KPIs to track pricing effectiveness (NIM, deposit flow, competitive position, win rates)

## Output Specification

```markdown
# Pricing Strategy Evaluation — [Product/Portfolio]

## Current Pricing Position
| Product | Current Rate | FTP Rate | FTP Spread | Market Median | Quartile | EP/Account |
|---------|-------------|----------|-----------|---------------|----------|-----------|

## FTP-Adjusted Breakeven
| Product | FTP | Credit | OpEx | Capital | Min Rate | Target Rate | Actual Rate | Margin |
|---------|-----|--------|------|---------|----------|-------------|-------------|--------|

## Competitive Positioning
| Product | Our Rate | Market Q1 | Median | Q3 | Spread to Median | Position |
|---------|----------|-----------|--------|-----|-----------------|----------|

## Price Elasticity Estimates
| Product/Segment | Volume Elasticity | Cross-Elasticity | Deposit Beta | Confidence |
|----------------|-------------------|-----------------|--------------|------------|

## Pricing Scenario Analysis
| Scenario | Rate Change (bps) | Volume Impact ($M) | NII Impact ($M) | EP Impact ($M) |
|----------|-------------------|--------------------|-----------------|----------------|

## Recommendations
| # | Action | Product | Rate Δ (bps) | NII Impact | EP Impact | Timeline |
|---|--------|---------|-------------|-----------|-----------|----------|

## Monitoring KPIs
| KPI | Current | Target | Review Frequency |
|-----|---------|--------|-----------------|
```

## Analysis Framework

Apply the **Price-Volume-Margin Triangle**:
- **Price** moves inversely to **Volume** (higher price reduces volume, lower price increases it)
- The relationship between Price changes and Volume changes is governed by **Elasticity**
- **Margin** is determined by Price minus Cost (FTP-adjusted)
- The optimal pricing point maximizes total **Economic Profit** = Margin × Volume − Fixed Costs
- There is no universally correct price — only the price that best serves the institution's strategic objective (growth, margin, or retention)

## Examples

**Example — Deposit Pricing Evaluation:**
"The money market account is currently priced at 3.85%, positioned at the 35th percentile of the competitive market (median: 4.10%). The FTP value of this deposit is 4.45% (at a 2-year behavioral maturity), yielding a deposit value margin of 34bps after operating costs. Elasticity analysis indicates that a 25bps rate increase would attract approximately $340M in incremental balances (volume elasticity: -1.3). The incremental EP from these balances would be $3.1M annually, net of the $2.8M cost of paying 25bps more on existing $4.5B balances. Recommendation: Increase the rate by 15bps to 4.00%, positioning at the 45th percentile — this captures an estimated $200M of inflows while limiting the repricing cost on the existing book to $1.7M."

**Example — Loan Pricing Adequacy:**
"The C&I term loan portfolio is priced at an average spread of SOFR + 225bps. FTP-adjusted breakeven is SOFR + 182bps (FTP: 58bps, expected loss: 42bps, OpEx: 28bps, capital charge: 54bps), yielding an economic margin of 43bps — below the 60bps target. Win-rate analysis shows 78% close rate at current pricing, suggesting modest pricing power remains. Recommendation: Tighten new origination pricing to SOFR + 250bps, accepting an estimated 5pp decline in win rate (to 73%) in exchange for a 25bps margin improvement that increases portfolio EP by $6.2M annually."

## Guidelines

- Always price against FTP-adjusted economics, not gross interest margin
- Estimate elasticity empirically from historical data rather than assuming fixed values
- Segment elasticity by customer type — do not apply a single elasticity across the entire book
- Include the repricing cost on existing balances when evaluating rate increases for deposits
- Assess competitive positioning at the product-tier level, not just the product level
- Distinguish between posted rates and actual (negotiated) rates in competitive analysis
- Model relationship-level economics before adjusting individual product pricing
- Document pricing constraints (regulatory, strategic, competitive) that limit optimization

## Validation Checklist

- [ ] FTP-adjusted breakeven calculated with all cost components (FTP, credit, OpEx, capital)
- [ ] Competitive positioning based on current market survey data (within 30 days)
- [ ] Elasticity estimates sourced from empirical data or peer benchmarks (not assumed)
- [ ] Pricing scenarios model both volume and margin effects simultaneously
- [ ] Repricing cost on existing book included in deposit rate increase analyses
- [ ] Relationship-level economics assessed before single-product pricing changes
- [ ] Fair lending and UDAAP compliance reviewed for all pricing recommendations
- [ ] Exception pricing governance framework defined with approval levels and documentation
- [ ] Monitoring KPIs identified with review frequency and escalation triggers
- [ ] Recommendations quantified with NII and EP impact
