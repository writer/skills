---
name: funding-cost-decomposition
description: Decompose funding cost drivers across deposit pricing, wholesale funding, FTP curves, and liquidity premiums. Use when analyzing cost of funds, explaining funding mix changes, evaluating FTP methodologies, or preparing treasury funding cost reports for ALCO.

metadata:
  display_name: "Funding Cost Decomposition"
  short_description: "Break down bank funding costs, FTP curves, and drivers"
  default_prompt: "Analyze my funding cost decomposition and recommend clear next actions"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Funding Cost Decomposition

## Overview

Breaks down the bank's all-in funding cost into constituent components—deposit pricing, wholesale spreads, liquidity premiums, FTP allocations, and structural mix effects—to reveal the true economic cost of each funding source. Enables treasury to identify cost optimization levers, assess funding strategy effectiveness, and provide transparent cost attribution to business lines through FTP.

## When to Use

- Analyzing period-over-period changes in weighted average cost of funds
- Evaluating the cost-effectiveness of funding sources (retail deposits vs. wholesale vs. secured)
- Reviewing or redesigning the FTP framework
- Preparing funding cost commentary for ALCO or CFO reporting
- Assessing the marginal cost of incremental funding for business-line pricing
- Comparing funding cost benchmarks against peers

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Funding composition | Outstanding balances by funding source and product | Balance table with rates |
| Deposit portfolio | Balances, rates, maturity/behavioral profile by product | Product-level detail |
| Wholesale funding | Issuance details, spreads, tenors, benchmarks | Instrument-level data |
| FTP curve | Internal transfer pricing rates by tenor point | Term structure |
| Market reference rates | SOFR, Treasury yields, swap rates, credit spreads | Market data |
| Historical funding data | Prior period composition and costs for trend analysis | Same format as current |
| Operating costs | Cost-to-serve for each funding channel (branch, digital, wholesale) | Cost allocation data |

## Methodology

### Step 1 — Segment the Funding Stack

Classify all funding sources into a structured taxonomy:

**Core deposits (stable funding):**
- Demand deposits / checking (zero or low-rate, highest behavioral stability)
- Savings and money market accounts (managed-rate, moderate stability)
- Time deposits / CDs (contractual maturity, rate-certain)

**Market-sensitive deposits:**
- Brokered deposits (rate-competitive, lower stickiness)
- Institutional deposits (large, relationship-driven, rate-sensitive)
- Online/digital deposits (rate-competitive, lower acquisition cost)

**Wholesale funding:**
- Senior unsecured bonds (term, benchmark + credit spread)
- Covered bonds (secured, tighter spreads)
- Repo / secured borrowing (overnight to term, haircut-dependent)
- FHLB advances / central bank facilities
- Commercial paper (short-term, rolling)

**Capital instruments:**
- Subordinated debt (Tier 2, higher spread)
- AT1 / preferred equity (highest cost, regulatory capital benefit)

### Step 2 — Calculate Component Costs

For each funding segment, compute the **all-in cost** as:

`All-in Cost = Interest Cost + Issuance/Origination Cost + Operating Cost + FDIC Assessment + Liquidity Premium`

- **Interest cost**: Stated rate or benchmark + spread
- **Issuance cost**: Underwriting fees, legal, listing costs amortized over term
- **Operating cost**: Branch network, digital platform, relationship management costs allocated per dollar of funding raised
- **FDIC/DGS assessment**: Deposit insurance premium per dollar of deposits
- **Liquidity premium**: Incremental cost attributable to LCR/NSFR treatment (short-term wholesale funding carries higher implicit cost due to LCR outflow assumptions)

### Step 3 — Construct the Weighted Average Cost of Funds

`WACF = Σ (Balance_i × All-in Cost_i) / Σ Balance_i`

Decompose WACF into:
- **Base rate component**: Weighted contribution of benchmark rates (SOFR, Treasury)
- **Credit spread component**: Average credit spread on market-based funding
- **Deposit spread component**: Margin between deposit rates and equivalent-maturity market rates
- **Structural mix component**: Impact of the proportion allocated to each funding type
- **Operating cost component**: Non-interest costs of funding channels

### Step 4 — Perform Period-over-Period Variance Analysis

Decompose WACF change (ΔWACF) into:
- **Rate effect**: Change in cost holding mix constant = Σ (Balance_i,prior × ΔRate_i) / Σ Balance_i,prior
- **Mix effect**: Change in mix holding rates constant = Σ (ΔBalance_i × Rate_i,prior) / Σ Balance_i,current
- **Cross effect**: Interaction of simultaneous rate and mix changes
- **Volume effect**: Impact of overall balance sheet growth on fixed operating cost dilution

Present as a waterfall: Prior WACF → +Rate Effect → +Mix Effect → +Cross Effect → +Volume Effect = Current WACF

### Step 5 — Assess FTP Alignment

Evaluate whether the FTP curve accurately reflects marginal funding costs:
- Compare FTP rates at each tenor point to actual marginal funding costs
- Identify FTP subsidies (FTP rate < actual cost, business line under-charged) and taxes (FTP rate > actual cost)
- Assess behavioral assumptions embedded in FTP (e.g., demand deposit FTP maturity)
- Evaluate the liquidity premium component of FTP: does it appropriately charge business lines for generating LCR-unfriendly assets or attracting LCR-friendly stable deposits?
- Recommend FTP curve adjustments where material misalignment exists (threshold: >15bps divergence from marginal cost)

### Step 6 — Benchmark Against Peers and Market

Compare funding costs against:
- **Peer group**: WACF, deposit beta, wholesale credit spreads for comparable institutions
- **Market indicators**: Swap spreads, CDS levels, new-issue concessions
- **Historical trend**: 4-8 quarter time series of own WACF to identify structural trends
- Compute the **funding advantage/disadvantage** vs. peers in bps and absolute dollars

### Step 7 — Identify Optimization Opportunities

Assess cost reduction levers:
- **Deposit mix optimization**: Shift from rate-sensitive to stable core deposits
- **Wholesale tenor management**: Extend or shorten term funding to optimize spread vs. liquidity cost
- **Secured funding utilization**: Increase repo or covered bond funding against eligible collateral
- **Geographic/channel diversification**: Exploit lower-cost digital deposit channels
- **Behavioral repricing**: Adjust deposit pass-through strategies to manage deposit beta
- Quantify each opportunity in annual dollar savings and implementation effort

## Output Specification

```markdown
# Funding Cost Decomposition — [Period]

## Summary
Weighted average cost of funds: [X]%, [up/down] [Y]bps from [prior period].

## Funding Stack
| Source | Balance ($B) | % of Total | All-in Cost | Δ vs Prior (bps) |
|--------|-------------|------------|-------------|-------------------|
| Core deposits | | | | |
| Market-sensitive deposits | | | | |
| Senior unsecured | | | | |
| Secured funding | | | | |
| Subordinated debt | | | | |
| **Total** | | **100%** | **[WACF]** | |

## Cost Variance Waterfall
Prior WACF: [X]%
→ Rate effect: +/- [A]bps
→ Mix effect: +/- [B]bps
→ Cross effect: +/- [C]bps
→ Volume effect: +/- [D]bps
= Current WACF: [Y]%

## FTP Alignment Assessment
| Tenor | FTP Rate | Marginal Cost | Gap (bps) | Action |
|-------|----------|---------------|-----------|--------|

## Peer Comparison
| Metric | Institution | Peer Median | Rank |
|--------|-------------|-------------|------|

## Optimization Opportunities
| Opportunity | Annual Savings ($M) | Effort | Timeline |
|-------------|--------------------|---------|-----------| 

## Recommendations
1. [Specific funding strategy adjustment with quantified benefit]
```

## Analysis Framework

Apply the **Marginal Cost of Funds** framework:
- The relevant cost for business-line pricing decisions is the **marginal** cost of the next dollar of funding, not the **average** (blended) cost of the existing stock
- Marginal cost should reflect: (a) the actual market rate for new funding at the relevant tenor, (b) the liquidity premium for LCR/NSFR impact, (c) the credit spread appropriate to current market conditions
- Distinguish between **stock cost** (weighted average of existing book) and **flow cost** (rate on new/renewed funding) to identify pricing lag or acceleration
- FTP should be calibrated to marginal cost to send correct pricing signals to business lines

## Examples

**Example — Funding Cost Increase Narrative:**
"WACF increased 23bps to 2.87% in Q3, driven primarily by the rate effect (+31bps) as the deposit book repriced in response to the Fed's cumulative 75bps of hikes. This was partially offset by a favorable mix effect (-11bps) as the bank grew non-interest-bearing demand deposits by $1.4B through targeted commercial relationship deepening. The deposit beta for the quarter was 0.41, below the cycle-to-date average of 0.48, reflecting the lag in savings account repricing."

**Example — FTP Misalignment Finding:**
"The FTP curve underprices 3-year funding by 22bps relative to the marginal cost of a new 3-year senior unsecured issuance (FTP: 3.95% vs. marginal cost: 4.17%). This subsidizes the auto lending business, whose average loan tenor is 3.2 years, by approximately $14M annually. Recommendation: adjust the 3-year FTP rate to 4.15% to restore incentive alignment."

## Guidelines

- Always decompose WACF into interest and non-interest components
- Distinguish between average/stock cost and marginal/flow cost explicitly
- Report deposit betas with clear specification of the reference rate
- Present variance analysis using the rate-mix-cross-volume decomposition
- Compare FTP rates to marginal (not average) funding costs
- Include FDIC/DGS assessments and operating costs in all-in calculations
- State all rates on a consistent day-count and compounding basis

## Validation Checklist

- [ ] All funding sources classified and balances reconcile to total liabilities
- [ ] All-in costs include interest, issuance, operating, insurance, and liquidity components
- [ ] WACF calculated correctly as balance-weighted average of all-in costs
- [ ] Variance waterfall (rate + mix + cross + volume) reconciles to total ΔWACF
- [ ] FTP rates compared to marginal (not average) funding costs at each tenor
- [ ] Deposit betas specified with reference rate and observation period
- [ ] Peer comparison uses consistent cost definitions
- [ ] Optimization opportunities quantified with annual dollar impact
- [ ] Marginal vs. average cost distinction clearly made
- [ ] All rates stated on consistent day-count basis
