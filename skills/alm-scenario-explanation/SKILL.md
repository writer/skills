---
name: alm-scenario-explanation
description: Explain Asset-Liability Management scenarios including gap analysis, NII/EVE projections, ALCO decision frameworks, and balance sheet strategy. Use when interpreting ALM reports, preparing ALCO materials, explaining maturity mismatches, or analyzing balance sheet structural risk.

metadata:
  display_name: "Alm Scenario Explanation"
  short_description: "Explain ALM scenarios and balance sheet structural risk"
  default_prompt: "Explain my alm scenario in simple words and next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# ALM Scenario Explanation

## Overview

Interprets and explains ALM scenario analyses for ALCO committees and senior management. Covers maturity transformation dynamics, structural balance sheet positioning, NII/EVE trade-offs under multiple rate and business scenarios, and the strategic implications of ALM decisions. Applies ALCO governance frameworks and integrates with funds transfer pricing (FTP) to connect treasury strategy to business-line incentives.

## When to Use

- Preparing or interpreting ALCO meeting materials
- Explaining ALM scenario results to non-treasury stakeholders
- Analyzing strategic balance sheet positioning decisions
- Documenting maturity transformation and structural risk appetite
- Evaluating the NII/EVE trade-off of proposed ALM actions
- Assessing FTP implications of balance sheet rebalancing

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Balance sheet by maturity | Assets and liabilities bucketed by contractual/behavioral maturity | Time-bucketed table |
| Gap analysis | Cumulative maturity and repricing gaps | Gap report |
| NII projection scenarios | Base case and alternative rate/business scenarios | Multi-scenario table |
| EVE scenarios | Economic value under rate shocks | ΔEVE results |
| FTP curve | Current FTP rates by tenor | Term structure |
| Strategic plan assumptions | Volume growth, mix shifts, new product plans | Business plan data |
| Risk appetite limits | NII-at-risk, EVE-at-risk, duration gap limits | Limit framework |

## Methodology

### Step 1 — Characterize the Structural Balance Sheet Position

Map the bank's maturity transformation profile:
- **Asset-side duration**: Weighted average maturity/duration of the loan book, investment portfolio, and other earning assets
- **Liability-side duration**: Weighted average maturity/duration of deposits (contractual vs. behavioral), wholesale funding, and subordinated debt
- **Net maturity transformation**: Excess of asset duration over liability duration, representing the structural earnings from maturity mismatch
- Identify the largest contributors to maturity transformation by product and business line

### Step 2 — Construct Scenario Matrix

Define the scenario set covering both rate and business dimensions:

**Interest rate scenarios:**
- Base case (forward curve implied)
- Parallel +100bps / +200bps / -100bps / -200bps
- Steepener and flattener
- Rate-cycle scenarios (hiking cycle, easing cycle, prolonged low rates)

**Business scenarios:**
- Base case growth
- Accelerated deposit outflows (competitive pressure or digital disruption)
- Loan demand surge / contraction
- Wholesale funding market disruption
- Planned strategic initiatives (new product launch, portfolio acquisition)

Cross-combine rate and business scenarios for a minimum of 12 scenario combinations.

### Step 3 — Analyze NII Projections Across Scenarios

For each scenario, decompose the projected NII into:
- **Volume effect**: Impact of balance sheet growth or contraction
- **Mix effect**: Shift between fixed and floating assets/liabilities
- **Rate effect**: Direct impact of rate changes on repricing assets and liabilities
- **Basis effect**: Changes in benchmark spreads
- **Behavioral effect**: Changes in deposit stickiness, prepayment speeds, or drawdown patterns

Present the NII waterfall: Base NII → +Volume → +Mix → +Rate → +Basis → +Behavioral = Scenario NII

### Step 4 — Evaluate EVE Trade-offs

For each scenario, present:
- ΔEVE absolute and as percentage of Tier 1 capital
- Comparison to risk appetite limits
- The NII/EVE tension: scenarios where optimizing NII worsens EVE and vice versa

Construct the **NII-EVE efficient frontier**: Plot scenarios on an NII-change vs EVE-change plane to identify the optimal strategic position that maximizes NII within EVE risk appetite constraints.

### Step 5 — Assess FTP Implications

Connect ALM scenarios to business-line incentives through FTP:
- Map the current FTP curve and explain how it allocates interest rate risk between treasury and business lines
- Identify how each scenario affects FTP revenue attribution
- Assess whether FTP methodology captures the risks being generated (e.g., behavioral deposit assumptions creating implicit FTP subsidies)
- Flag any scenarios where FTP signals diverge from economic risk (misaligned incentives)

### Step 6 — Evaluate Strategic Options

Present actionable ALM strategies with their scenario-dependent outcomes:
- **Extend liability duration**: Issue term funding or promote time deposits to reduce liability-side repricing risk
- **Shorten asset duration**: Increase floating-rate or shorter-tenor lending, sell fixed-rate securities
- **Hedge overlay**: Add interest rate swaps, caps, or swaptions to modify duration without balance sheet restructuring
- **Natural hedge optimization**: Reallocate between business lines to exploit offsetting positions

For each option, quantify the NII and EVE impact, implementation cost, and reversibility.

### Step 7 — Draft the ALCO Decision Package

Structure the ALCO narrative:
1. **Current position**: Structural balance sheet characterization and key metrics
2. **Scenario analysis**: Outcome matrix showing NII and EVE under each scenario
3. **Risk appetite compliance**: Current metrics vs. limits with traffic-light status
4. **Strategic options**: Quantified alternatives with recommendation
5. **Decision required**: Specific ALCO decision points (approve hedge, adjust limits, rebalance FTP)
6. **Monitoring plan**: Key indicators to track between ALCO meetings

## Output Specification

```markdown
# ALCO Scenario Analysis — [Period]

## Current Structural Position
- Asset weighted average duration: [X] years
- Liability weighted average duration: [Y] years
- Net maturity transformation: [Z] years
- NII run-rate (annualized): $[N]M

## Scenario Outcome Matrix
| Scenario | ΔNII ($M) | ΔNII % | ΔEVE ($M) | ΔEVE % Tier1 | Limit Status |
|----------|-----------|--------|-----------|--------------|-------------|

## NII Waterfall — [Selected Scenario]
Base NII: $[X]M
→ Volume: +/- $[A]M
→ Mix: +/- $[B]M
→ Rate: +/- $[C]M
→ Basis: +/- $[D]M
→ Behavioral: +/- $[E]M
= Scenario NII: $[Y]M

## Strategic Options Assessment
| Option | ΔNII Impact | ΔEVE Impact | Cost | Reversibility |
|--------|-------------|-------------|------|---------------|

## Recommendation
[Recommended action with rationale tied to scenario analysis]

## Decision Points for ALCO
1. [Specific approval or directive required]
2. [Limit adjustment if applicable]
```

## Analysis Framework

Apply the **Maturity Transformation Value Chain**:
1. **Originate**: Business lines create assets and liabilities with embedded rate and maturity profiles
2. **Transfer**: FTP transfers rate and liquidity risk from business lines to treasury at arm's length prices
3. **Manage**: Treasury actively manages the residual structural position through the investment portfolio and hedging
4. **Monitor**: ALCO oversees the aggregate position against risk appetite and adjusts strategic direction

Each scenario should be evaluated at every stage of this chain to identify where value is created or destroyed.

## Examples

**Example — ALCO Scenario Summary:**
"Under the base case forward curve, NII is projected at $1,240M for the next 12 months. A +200bps parallel shock increases NII by $86M (+6.9%) reflecting the bank's asset-sensitive repricing profile, but reduces EVE by $420M (8.2% of Tier 1), approaching the 10% internal limit. The ALCO is asked to approve the execution of $2B receive-fixed IRS (5Y tenor) to reduce EVE sensitivity by approximately $180M while sacrificing $18M of NII upside in the rising-rate scenario."

**Example — FTP Misalignment Flag:**
"The current FTP framework assigns a 2.1% cost-of-funds to retail demand deposits based on a 3-year behavioral maturity assumption. Scenario analysis reveals that under a +200bps rate shock, actual deposit repricing occurs within 9 months (pass-through beta of 0.65), suggesting the FTP rate understates the true cost by approximately 45bps. This subsidizes Retail Banking NII by an estimated $28M annually at Treasury's expense."

## Guidelines

- Present all scenarios with both NII and EVE outcomes simultaneously
- Use waterfall decomposition to make drivers transparent
- Connect every strategic recommendation to specific scenario outcomes
- Explicitly state FTP methodology assumptions and their limitations
- Frame ALCO decisions as choices between quantified trade-offs, not open-ended requests
- Distinguish between static (run-off) and dynamic (growth-adjusted) balance sheet assumptions
- Ensure scenario severity is calibrated to historical experience and regulatory expectations

## Validation Checklist

- [ ] Balance sheet items correctly classified by maturity/repricing bucket
- [ ] Scenario matrix covers both rate and business dimensions (minimum 12 combinations)
- [ ] NII waterfall components sum correctly to scenario NII
- [ ] EVE expressed as % of Tier 1 capital and compared to risk appetite limits
- [ ] FTP implications assessed for material scenarios
- [ ] Strategic options quantified with NII, EVE, cost, and reversibility
- [ ] ALCO decision points are specific and actionable
- [ ] Behavioral assumptions documented for NMDs, prepayments, and pipeline
- [ ] NII/EVE trade-off explicitly addressed where perspectives conflict
- [ ] Monitoring indicators defined for inter-meeting tracking
