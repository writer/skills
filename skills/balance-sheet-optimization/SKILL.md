---
name: balance-sheet-optimization
description: Generate balance sheet optimization insights including RWA efficiency, NIM enhancement, HQLA portfolio optimization, FTP-aligned product mix, and regulatory capital leverage. Use when analyzing balance sheet efficiency, evaluating asset allocation trade-offs, optimizing capital deployment, or preparing strategic balance sheet reviews for ALCO.

metadata:
  display_name: "Balance Sheet Optimization"
  short_description: "Optimize bank balance sheet and capital efficiency"
  default_prompt: "Optimize my bank balance sheet and capital efficiency and suggest the best next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Balance Sheet Optimization

## Overview

Provides a structured framework for analyzing and optimizing bank balance sheet composition across competing objectives—return on equity, regulatory capital efficiency, liquidity compliance, interest margin, and risk appetite. Integrates RWA optimization, FTP-adjusted product economics, HQLA portfolio construction, and strategic asset allocation into actionable ALCO recommendations.

## When to Use

- Conducting strategic balance sheet reviews for ALCO or board
- Evaluating asset class allocation for optimal risk-adjusted returns
- Analyzing RWA density reduction opportunities
- Optimizing the HQLA investment portfolio for yield within regulatory constraints
- Assessing FTP-adjusted profitability of business lines for capital allocation decisions
- Preparing medium-term balance sheet strategy and capital deployment plans

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Balance sheet | Assets and liabilities by product, maturity, rate type | Detailed BS data |
| RWA by portfolio | Credit, market, operational RWA with exposure and density | Portfolio-level data |
| NIM components | Yield on assets, cost of funds, NIM by product | Product-level margins |
| FTP rates | Transfer pricing rates by tenor and product | FTP curve + product FTP |
| Capital ratios | CET1, Tier 1, leverage ratio with buffer positions | Current and target ratios |
| LCR/NSFR components | HQLA stock, net outflows, ASF/RSF | Regulatory liquidity data |
| Return metrics | ROAA, ROAE, RAROC by business line | Performance data |
| Peer benchmarks | Peer group balance sheet composition and efficiency metrics | Comparable data |

## Methodology

### Step 1 — Construct the Balance Sheet Efficiency Dashboard

Compute key efficiency metrics across the balance sheet:

**Return metrics:**
- **ROAA**: Net income / Average total assets — overall asset productivity
- **ROAE**: Net income / Average equity — shareholder return
- **RAROC**: Risk-adjusted return on capital = (Revenue − Expenses − Expected Loss) / Economic Capital
- **NIM**: Net interest income / Average earning assets — spread efficiency

**Capital efficiency:**
- **RWA density**: Total RWA / Total assets — lower is more capital-efficient
- **RWA-to-equity multiplier**: Total RWA / CET1 capital — leverage of regulatory capital
- **Return on RWA (RoRWA)**: Net income / Average RWA — profitability per unit of regulatory capital consumed

**Liquidity efficiency:**
- **HQLA yield**: Weighted average yield on the HQLA portfolio vs. benchmark sovereign curve
- **HQLA carry cost**: Opportunity cost of holding HQLA vs. higher-yielding alternatives
- **NSFR excess**: ASF above RSF representing structurally surplus stable funding

### Step 2 — Map the Product-Level Economics

For each major product line, compute the FTP-adjusted economic contribution:

`Product Economic Profit = (Customer Rate − FTP Rate) × Balance − Credit Cost − Operating Cost − Capital Charge`

Where:
- **Customer rate**: Actual yield (assets) or cost (liabilities) to the customer
- **FTP rate**: Internal transfer price at the product's maturity/repricing profile
- **Credit cost**: Expected loss (PD × LGD × EAD) for the product portfolio
- **Operating cost**: Allocated direct and indirect costs
- **Capital charge**: RWA × Target CET1% × Cost of Equity

Rank products by:
1. Economic profit per dollar of balance ($EP/$B)
2. Economic profit per dollar of RWA ($EP/$RWA) — capital efficiency ranking
3. Marginal economic profit — incremental return on the next dollar deployed

### Step 3 — Identify RWA Optimization Opportunities

Analyze the RWA book for capital-release opportunities:

**Credit risk RWA optimization:**
- **Portfolio rebalancing**: Shift allocation from high-density (corporate unsecured: 100% RW) to lower-density (residential mortgage: 35-50% RW) asset classes where risk-return is favorable
- **Credit risk mitigation (CRM)**: Increase eligible collateral, guarantees, or credit insurance to reduce risk weights
- **Securitization**: Off-balance-sheet transfer of loan portfolios (true sale or synthetic) to release capital
- **IRB model optimization**: For IRB banks, refine PD/LGD models with better data to reduce conservatism
- **Exposure netting**: Enhance master netting agreements for derivatives and repo exposures

**Market risk RWA optimization:**
- Reduce desk-level VaR through position management
- Optimize the boundary between banking and trading book

**Operational risk RWA optimization:**
- Under Basel III standardized approach, manage the Business Indicator components (interest, services, financial)

### Step 4 — Optimize the HQLA Portfolio

Construct the HQLA investment portfolio to maximize yield within LCR constraints:

**Constraints:**
- Level 1 ≥ 60% of total HQLA (after haircuts)
- Level 2 ≤ 40% (Level 2B ≤ 15%)
- Portfolio must remain unencumbered and operationally monetizable
- Currency composition aligned with net cash outflow currency profile

**Optimization levers:**
- **Duration management**: Extend HQLA duration within risk appetite to capture term premium
- **Level 2A allocation**: Maximize allocation to qualifying covered bonds and high-grade corporates (higher yield than sovereigns, 15% haircut)
- **Level 2B allocation**: Selectively include qualifying RMBS or equities at higher haircuts for yield enhancement
- **Repo optimization**: Use the HQLA book in repo markets to generate incremental income while maintaining LCR eligibility through title-transfer arrangements
- **Cross-currency HQLA**: Hold foreign-currency HQLA to natural-hedge FX net outflows and access higher-yielding sovereign markets

### Step 5 — Evaluate the Funding Mix Optimization

Assess the optimal liability-side composition:

- **Deposit mix**: Determine target allocation between core deposits (low-cost, stable, favorable LCR/NSFR) and market-rate deposits (higher cost but scalable)
- **Wholesale funding tenor**: Optimize the maturity profile to minimize cost while meeting NSFR requirements (ASF factor: <6M = 0%, 6M-1Y = 50%, >1Y = 100%)
- **Secured vs. unsecured funding**: Evaluate the cost-benefit of increasing secured funding (lower spread but encumbers assets)
- **Capital structure**: Assess optimal mix of CET1, AT1, and Tier 2 to minimize weighted average cost of capital while meeting buffer requirements

Compute the **marginal value of stable funding**: Additional basis points of NIM sacrifice justified by NSFR improvement, quantified as NSFR-adjusted cost of funds.

### Step 6 — Construct Optimization Scenarios

Build three to five balance sheet optimization scenarios:

**Scenario 1 — Return Maximization:**
- Tilt toward highest-RAROC products
- Minimize HQLA to regulatory minimum
- Maximize leverage within capital limits
- Outcome: Highest ROAE, highest risk

**Scenario 2 — Capital Efficiency:**
- Prioritize low-RWA-density assets
- Optimize CRM and securitization
- Improve RoRWA while maintaining ROAE
- Outcome: Capital release for dividends or growth

**Scenario 3 — Liquidity Fortress:**
- Build excess HQLA and NSFR buffers
- Extend funding duration
- Sacrifice NIM for stability
- Outcome: Maximum stress resilience, lower return

**Scenario 4 — Balanced Optimization:**
- Blend return, capital, and liquidity objectives
- Target the efficient frontier of ROAE vs. capital/liquidity constraints
- Outcome: Sustainable medium-term positioning

For each scenario, project the impact on: ROAE, ROAA, RoRWA, NIM, CET1 ratio, LCR, NSFR.

### Step 7 — Formulate Strategic Recommendations

Synthesize findings into ALCO-actionable recommendations:
1. **Asset allocation shifts**: Specific portfolio rebalancing with volumes, timeline, and return impact
2. **RWA actions**: Capital release transactions with estimated ratio improvement
3. **HQLA portfolio restructuring**: Reallocation trades with yield pickup and LCR impact
4. **Funding strategy adjustments**: Deposit campaign targets, wholesale issuance plan, tenor optimization
5. **Business-line capital allocation**: Revised capital budgets based on FTP-adjusted RAROC ranking
6. **Implementation roadmap**: Phased execution plan with milestones and monitoring KPIs

## Output Specification

```markdown
# Balance Sheet Optimization Analysis — [Period]

## Efficiency Dashboard
| Metric | Current | Target | Peer Median | Gap |
|--------|---------|--------|-------------|-----|
| ROAE | | | | |
| ROAA | | | | |
| RoRWA | | | | |
| NIM | | | | |
| RWA Density | | | | |
| CET1 Ratio | | | | |
| LCR | | | | |
| NSFR | | | | |

## Product Economics Ranking (FTP-Adjusted)
| Product | Balance ($B) | EP ($M) | EP/RWA (bps) | RWA Density | Recommendation |
|---------|-------------|---------|--------------|-------------|----------------|

## RWA Optimization Opportunities
| Opportunity | RWA Release ($B) | CET1 Impact (bps) | Implementation | Timeline |
|-------------|------------------|--------------------|----------------|----------|

## HQLA Portfolio Optimization
| Current Allocation | Proposed Allocation | Yield Pickup (bps) | LCR Impact |
|--------------------|---------------------|--------------------|------------|

## Optimization Scenario Comparison
| Metric | Status Quo | Return Max | Capital Eff | Liquidity | Balanced |
|--------|-----------|------------|-------------|-----------|----------|

## Strategic Recommendations
1. [Recommendation with quantified impact and implementation plan]
```

## Analysis Framework

Apply the **Quadruple Constraint Optimization** framework:
1. **Return objective**: Maximize risk-adjusted returns (ROAE, RAROC)
2. **Capital constraint**: Meet all regulatory ratios with adequate buffers
3. **Liquidity constraint**: Comply with LCR/NSFR with prudent surplus
4. **Risk appetite constraint**: Stay within board-approved risk limits (credit concentration, duration, sector)

The optimal balance sheet is the composition that maximizes the return objective subject to the three constraints. No single optimization lever should be evaluated in isolation—each action affects multiple constraints simultaneously.

## Examples

**Example — RWA Optimization Narrative:**
"RWA density of 48% exceeds the peer median of 42%, primarily driven by an overweight allocation to unsecured commercial lending (RWA density 85%) at 34% of total assets vs. peer average of 28%. Rebalancing $3.2B from unsecured commercial to government-guaranteed SME loans (RWA density 0-20%) would release $2.1B of RWA, improving CET1 by 28bps while sacrificing only 4bps of NIM given the compressed spread differential in the current rate environment."

**Example — HQLA Optimization Narrative:**
"The current HQLA portfolio yields 4.12%, 23bps below the optimized allocation. Shifting $1.8B from overnight central bank deposits (yielding 3.85%) into 3-year covered bonds qualifying as Level 2A (yielding 4.42% after 15% haircut) would increase annual investment income by $10.3M while maintaining Level 2A within the 40% cap at 36%. The duration extension of 1.4 years remains within the investment portfolio duration limit of 3.5 years."

## Guidelines

- Always present optimization as trade-offs between competing objectives, not free improvements
- Use FTP-adjusted (not gross) margins for product economics to avoid cross-subsidy distortions
- Quantify every recommendation with specific dollar or basis-point impact
- Include implementation costs and reversibility in all scenario assessments
- Benchmark against peers using consistent definitions and data periods
- Account for second-order effects (e.g., RWA reduction that also affects NIM or LCR)
- Present scenarios as a spectrum from aggressive to conservative positioning

## Validation Checklist

- [ ] Efficiency metrics computed consistently with standard definitions
- [ ] Product economics reflect FTP-adjusted margins, not gross spreads
- [ ] RWA optimization opportunities verified against current regulatory treatment
- [ ] HQLA optimization respects Level 1/2A/2B caps and encumbrance constraints
- [ ] Funding mix optimization accounts for NSFR ASF factor impacts
- [ ] All scenarios project impact across ROAE, CET1, LCR, and NSFR simultaneously
- [ ] Peer comparisons use consistent metrics and time periods
- [ ] Recommendations quantified with dollar and basis-point impact
- [ ] Implementation roadmap includes timeline, milestones, and monitoring KPIs
- [ ] Trade-offs between objectives explicitly acknowledged in every recommendation
