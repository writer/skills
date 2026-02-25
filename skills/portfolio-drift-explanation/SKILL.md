---
name: portfolio-drift-explanation
description: Explain portfolio drift from target allocations in client-friendly language with actionable rebalancing guidance. Use when preparing client review presentations, explaining allocation changes caused by market movements, justifying rebalancing trades, or helping clients understand why their portfolio looks different from the original plan.

metadata:
  display_name: "Portfolio Drift Explanation"
  short_description: "Explain portfolio allocation drift with rebalancing advice"
  default_prompt: "Explain my portfolio drift in simple words and next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Portfolio Drift Explanation

## Overview

Generate clear, client-appropriate explanations of how and why a portfolio has drifted from its target allocation. This skill decomposes drift into market-driven and cash-flow-driven components, explains the risk implications of the drift, and presents rebalancing options with trade-off analysis. Explanations are designed for client-facing communication — plain language with visual-ready data that advisors can use in review meetings.

## When to Use

- Quarterly or annual client review meetings to explain allocation changes
- When drift has triggered rebalancing thresholds requiring client notification
- Client inquiries about why their portfolio "looks different" from what was agreed
- Preparing rebalancing proposals with clear rationale for recommended trades
- Explaining the risk impact of allowing drift to continue vs. rebalancing
- Documenting fiduciary decision-making around drift management

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Target allocation | IPS or planning-defined target weights | Allocation model |
| Current allocation | Actual portfolio weights by asset class | Current holdings |
| Historical allocation | Allocation snapshots over trailing periods | Time series |
| Market returns | Asset class returns over the drift period | Return data |
| Cash flows | Contributions, withdrawals, distributions | Transaction history |
| Risk metrics | Portfolio risk before and after drift | Risk analytics |
| Rebalancing bands | IPS-defined tolerance ranges per asset class | Policy parameters |

## Methodology

### Step 1 — Drift Quantification

Calculate the precise drift for each asset class:

| Asset Class | Target | Current | Drift | Band | Status |
|-------------|--------|---------|-------|------|--------|
| US Equity | 40.0% | 44.8% | +4.8% | ±5% | Approaching limit |
| Int'l Equity | 15.0% | 16.2% | +1.2% | ±3% | Within band |
| Fixed Income | 30.0% | 25.6% | -4.4% | ±5% | Approaching limit |
| Alternatives | 10.0% | 9.8% | -0.2% | ±3% | Within band |
| Cash | 5.0% | 3.6% | -1.4% | ±2% | Within band |

Calculate aggregate drift measures:
- **Sum of absolute deviations**: Total portfolio drift magnitude
- **Tracking error vs. target**: Expected return difference from target portfolio
- **Risk budget utilization**: Current portfolio risk vs. target risk budget

### Step 2 — Drift Decomposition

Separate drift into its component causes:

**Market-driven drift:**
- Calculate the hypothetical allocation assuming no cash flows (pure market returns applied to starting weights)
- Compare to actual allocation to isolate market effect
- Example: "US equities returned 18% while bonds returned 3% over the past year, naturally increasing equity weight"

**Cash-flow-driven drift:**
- Calculate the allocation change attributable to contributions, withdrawals, and income reinvestment
- Common patterns: Regular withdrawals from fixed income reducing FI weight; contributions invested in cash pending deployment
- Example: "Your monthly $5,000 distribution was funded from bonds, reducing fixed income weight by 1.2%"

**Rebalancing lag drift:**
- Time elapsed since last rebalancing event
- Cumulative drift that would have been corrected by more frequent rebalancing

**Drift attribution formula:**
Total Drift = Market Effect + Cash Flow Effect + Rebalancing Lag Effect

### Step 3 — Risk Impact Assessment

Quantify how drift has changed the portfolio's risk characteristics:

- **Volatility change**: Portfolio standard deviation at target vs. current allocation
  - Example: "Your portfolio's expected volatility has increased from 10.2% to 11.4% due to higher equity weight"
- **Maximum drawdown exposure**: Expected worst-case loss at target vs. current
  - Example: "In a 2008-like scenario, your portfolio would now decline an estimated 32% vs. 27% at target weights"
- **Income impact**: Change in expected portfolio income yield
- **Sharpe ratio comparison**: Risk-adjusted return at target vs. current allocation
- **Downside risk**: Value-at-Risk (VaR) or Conditional VaR at both allocations
- **Correlation shift**: How drift has changed the portfolio's diversification benefit

Present risk impacts in client-friendly terms: "The drift has modestly increased your portfolio's risk. In a market downturn similar to 2020, your portfolio would experience approximately $X more in temporary losses than at target weights."

### Step 4 — Scenario Analysis

Show forward-looking implications of rebalancing vs. staying drifted:

**Scenario 1 — Rebalance now:**
- Return to target allocation, realize the risk/return profile originally agreed
- Tax cost of rebalancing (estimated gains/losses from selling over-weighted positions)
- Transaction costs

**Scenario 2 — Partial rebalance:**
- Bring most over-weight positions back to range maximum (not target)
- Reduces tax impact while addressing largest deviations
- Maintains some market momentum benefit

**Scenario 3 — No action (continue drift):**
- If market trends continue, projected allocation in 3/6/12 months
- Risk metrics at projected future allocation
- Probability of breaching IPS bands within the next quarter

### Step 5 — Client-Friendly Narrative Construction

Translate the technical analysis into a clear client narrative:

**Structure:**
1. **What happened**: "Over the past [period], your portfolio's mix has shifted because [primary reason]"
2. **Why it happened**: "Stock markets gained [X%] while bonds returned [X%], which naturally pushed your equity allocation higher"
3. **What it means**: "This means your portfolio is taking slightly [more/less] risk than we originally planned"
4. **What we recommend**: "We recommend [action] to bring your portfolio back in line with your investment plan"
5. **Trade-offs**: "This will involve [costs/taxes/considerations], which we believe is outweighed by [benefit]"

Avoid jargon: Use "stock portion" instead of "equity allocation," "bonds" instead of "fixed income," "mix" instead of "allocation."

### Step 6 — Rebalancing Recommendation

Present specific rebalancing recommendations with tax analysis:

- List specific trades needed to return to target or range
- Estimate tax impact: short-term gains, long-term gains, harvestable losses
- Consider tax-loss harvesting opportunities created by rebalancing
- Evaluate using new contributions to rebalance passively (cash flow rebalancing)
- For retirement accounts: Rebalance first in tax-deferred accounts (no tax impact)
- Provide net-of-tax benefit analysis of rebalancing vs. not rebalancing

### Step 7 — Documentation and Next Steps

Document the drift analysis and decision for compliance records:

## Output Specification

```
## Portfolio Drift Report — [Client Name]

### Summary
Your portfolio has drifted from its target allocation over the past [period].
The primary driver was [market returns / cash flows / both].

### Allocation Comparison
| Asset Class | Target | Current | Drift | Action Needed |
|-------------|--------|---------|-------|---------------|
| Stocks (US) | XX% | XX.X% | +X.X% | [Reduce/None] |
| Stocks (Int'l) | XX% | XX.X% | +/-X.X% | [Reduce/Add/None] |
| Bonds | XX% | XX.X% | -X.X% | [Add/None] |
| Alternatives | XX% | XX.X% | +/-X.X% | [Adjust/None] |
| Cash | XX% | XX.X% | +/-X.X% | [Deploy/None] |

### Why This Happened
[2–3 sentence plain-language explanation]

### What This Means for You
- Risk level: [Slightly higher / lower / unchanged] than planned
- In a market downturn: Your portfolio could temporarily decline by approximately $[X] more/less than at target
- Income: Your expected annual income is approximately $[X] [higher/lower]

### Our Recommendation
[Clear recommendation with rationale]

### Tax Impact of Recommended Rebalancing
- Estimated taxable gains: $[X] ([ST/LT])
- Estimated harvestable losses: $[X]
- Net tax cost: $[X]

### Decision
- [ ] Rebalance to targets (recommended)
- [ ] Partial rebalance (bring within ranges)
- [ ] No action at this time
- Client decision: _________________ Date: _________
```

## Analysis Framework

Apply the **DRIP** framework:

- **D**rift — Quantify the deviation from target for every asset class
- **R**eason — Decompose drift into market, cash flow, and timing components
- **I**mpact — Assess risk and return implications of the drift
- **P**lan — Present actionable rebalancing options with trade-off analysis

## Examples

**Example 1 — Post-Rally Equity Drift**

Client with 60/40 target. After a 25% equity rally, portfolio is now 68/32. Drift explanation: "Over the past 12 months, the stock market rose significantly — about 25% — while your bonds earned about 4%. This strong stock performance naturally increased your stock portion from 60% to 68%. While this extra growth is good news, it means your portfolio is now taking about 15% more risk than we planned. We recommend selling about $85,000 of stock funds and purchasing bonds to bring you back to 60/40. This would generate approximately $12,000 in long-term capital gains ($2,400 in taxes at your rate), but it restores the risk level we agreed is right for your situation."

**Example 2 — Withdrawal-Driven Drift**

Retired client taking $8,000/month distributions funded from bond ladder. Target: 50/50. Current: 56/44 after 18 months. Drift explanation: "Your monthly income distributions have been coming from your bond investments as planned, but over 18 months this has gradually reduced your bond portion from 50% to 44%. We recommend redirecting the next 3 months of distributions from your stock account and making a one-time $45,000 exchange from stocks to bonds in your IRA (no tax impact) to restore your 50/50 balance."

## Guidelines

- Use plain language throughout — this is a client-facing document
- Quantify risk impacts in dollar terms, not just percentages (more intuitive for clients)
- Always present tax costs alongside rebalancing recommendations
- Prioritize tax-free rebalancing (retirement accounts) before taxable trades
- Consider cash flow rebalancing (directing new money to underweight classes) as the first option
- Document the client's rebalancing decision with date and signature for compliance
- Include visual aids (pie charts, before/after comparisons) when possible
- Frame drift management as maintaining the agreed-upon plan, not predicting markets

## Validation Checklist

- [ ] All asset classes represented with accurate current and target weights
- [ ] Drift decomposition correctly isolates market vs. cash flow effects
- [ ] Risk impact is quantified in both percentage and dollar terms
- [ ] Rebalancing scenarios include tax impact estimates
- [ ] Narrative uses plain language appropriate for the client's financial literacy
- [ ] Retirement accounts are prioritized for rebalancing to minimize tax impact
- [ ] Recommendations are consistent with the IPS rebalancing policy
- [ ] Client decision is documented with date for compliance records
- [ ] Drift analysis covers the period since the last rebalancing event
- [ ] Forward-looking projections are clearly labeled as estimates
