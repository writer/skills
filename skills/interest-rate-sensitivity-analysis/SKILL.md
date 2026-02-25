---
name: interest-rate-sensitivity-analysis
description: Analyze and explain interest rate risk impact on NII and EVE, including duration gap analysis, repricing profiles, basis risk, and yield curve scenario modeling. Use when assessing NII sensitivity, EVE delta, rate shock scenarios, IRRBB analysis, or explaining interest rate risk to ALCO committees.

metadata:
  display_name: "Interest Rate Sensitivity Analysis"
  short_description: "Analyze interest rate risk impact on NII, EVE, and duration"
  default_prompt: "Analyze my interest rate sensitivity and recommend clear next actions"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Interest Rate Sensitivity Analysis

## Overview

Translates interest rate risk data—repricing gaps, NII sensitivity, EVE changes, duration profiles—into structured analysis and narratives for ALCO review, IRRBB regulatory submissions, and strategic planning. Applies Basel Committee IRRBB standards (BCBS 368) including the six prescribed shock scenarios and institution-specific behavioral assumptions.

## When to Use

- Preparing NII-at-risk and EVE-at-risk reports for ALCO
- Analyzing impact of parallel and non-parallel yield curve shifts
- Explaining basis risk between funding and lending benchmarks
- Drafting IRRBB sections of ICAAP or Pillar 2 submissions
- Evaluating hedging strategy effectiveness
- Assessing embedded optionality (prepayment, early redemption, behavioral deposits)

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Repricing gap report | Assets and liabilities by repricing bucket | Time-bucketed table |
| NII sensitivity | NII change per +/- 100bps, 200bps parallel shift | Basis point sensitivities |
| EVE sensitivity | EVE change under six BCBS prescribed shocks | Scenario-result pairs |
| Yield curve data | Current and forward curves for relevant benchmarks | Rate term structure |
| Behavioral assumptions | NMD repricing, prepayment models, pipeline assumptions | Model parameters |
| Hedge portfolio | IRS, caps, floors, swaptions with notional, tenor, rates | Position-level detail |
| Balance sheet composition | Fixed vs. floating mix, benchmark index distribution | Percentage breakdown |

## Methodology

### Step 1 — Map the Repricing Profile

Construct the repricing gap across standardized time buckets:
- Overnight, 1M, 3M, 6M, 12M, 2Y, 3Y, 5Y, 7Y, 10Y, 15Y, 20Y, 20Y+
- Classify each asset and liability as **rate-sensitive** (reprices within bucket) or **non-rate-sensitive**
- Apply behavioral repricing assumptions for non-maturing deposits (NMDs): segment by product type (demand deposits, savings, money market) and apply institution-specific pass-through rates and decay functions
- Identify **repricing mismatches** — buckets where asset repricing materially differs from liability repricing

### Step 2 — Compute NII Sensitivity (Earnings Perspective)

Calculate NII impact under rate scenarios over a 12-month horizon:
- **Parallel shifts**: +/- 100bps, +/- 200bps, +/- 300bps
- **Non-parallel scenarios**: Bull steepener, bear flattener, short-rate shock
- For each scenario, compute: ΔRevenue on assets + ΔCost on liabilities + ΔHedge P&L = ΔNII
- Decompose ΔNII by business line and product to identify concentration of rate sensitivity
- Apply **repricing beta** (pass-through rate) for managed-rate products: ΔProduct Rate / ΔBenchmark Rate
- Account for balance sheet dynamics: volume growth assumptions, planned originations, run-off

### Step 3 — Compute EVE Sensitivity (Economic Value Perspective)

Apply the six BCBS 368 prescribed interest rate shock scenarios:
1. **Parallel up** (+200bps across all tenors)
2. **Parallel down** (-200bps, floored at effective lower bound)
3. **Steepener** (short rates down, long rates up)
4. **Flattener** (short rates up, long rates down)
5. **Short rate up** (front-end shock with decay)
6. **Short rate down** (front-end shock with decay)

For each scenario:
- Revalue all cash flows using shocked discount curves
- EVE = PV(Asset cash flows) − PV(Liability cash flows) under each scenario
- ΔEVE = Shocked EVE − Base EVE
- Express as percentage of Tier 1 capital to assess materiality (BCBS threshold: 15% of Tier 1)

### Step 4 — Analyze Duration Gap and Convexity

- **Modified duration of assets** (DA) and **modified duration of liabilities** (DL)
- **Duration gap** = DA − (L/A × DL), where L/A is the leverage ratio
- Positive gap: EVE falls when rates rise; negative gap: EVE falls when rates fall
- **Convexity effects**: Assess non-linear price sensitivity, particularly from:
  - Mortgage prepayment optionality (negative convexity on MBS)
  - Callable bond portfolios
  - Deposit early withdrawal behavior
  - Cap/floor asymmetry in floating-rate instruments

### Step 5 — Assess Basis Risk

Identify and quantify basis risk exposure:
- **Benchmark mismatch**: Assets on SOFR vs. liabilities on Fed Funds, or mixed legacy LIBOR exposures
- **Tenor mismatch**: 1M SOFR assets funded by 3M SOFR liabilities
- **Cross-currency basis**: Foreign currency assets funded through basis swaps
- Quantify basis risk as NII impact per 10bps widening/tightening of relevant basis spreads
- Evaluate historical basis volatility to calibrate scenario severity

### Step 6 — Evaluate Hedge Effectiveness

Review the derivatives hedge portfolio:
- Map hedge notionals and tenors against the underlying exposure they offset
- Calculate the **hedge ratio**: notional hedged / total exposure per repricing bucket
- Assess **P&L offset**: correlation between hedge MTM and underlying NII/EVE movement
- Identify **over-hedged** or **under-hedged** buckets
- Review hedge accounting designations (fair value vs. cash flow hedges) and effectiveness testing results
- Flag any hedges rolling off within 6 months that will leave unhedged exposure

### Step 7 — Synthesize Findings and Recommend Actions

Construct the analysis output:
1. **Risk profile summary**: Overall characterization (asset-sensitive, liability-sensitive, neutral)
2. **Earnings-at-risk**: NII sensitivity table with business-line attribution
3. **Economic value-at-risk**: ΔEVE under six scenarios against Tier 1 capital thresholds
4. **Key vulnerabilities**: Concentrations, cliff risks, basis exposures, option risk
5. **Hedge assessment**: Effectiveness, gaps, upcoming roll-offs
6. **Recommended actions**: Hedging adjustments, balance sheet restructuring, limit changes

## Output Specification

```markdown
# Interest Rate Risk Analysis — [Period]

## Risk Profile Summary
The balance sheet is [asset/liability]-sensitive with a duration gap of [X] years.
A +100bps parallel shift would [increase/decrease] NII by $[X]M ([Y]% of base NII)
and [increase/decrease] EVE by $[Z]M ([W]% of Tier 1 capital).

## NII Sensitivity (12-Month Horizon)
| Scenario | ΔNII ($M) | % of Base NII | Primary Driver |
|----------|-----------|---------------|----------------|
| +100bps parallel | | | |
| -100bps parallel | | | |
| Steepener | | | |
| Flattener | | | |

## EVE Sensitivity
| BCBS Scenario | ΔEVE ($M) | % of Tier 1 | Status vs 15% Threshold |
|---------------|-----------|-------------|------------------------|

## Duration Profile
| | Modified Duration | DV01 ($M/bp) |
|----------|-------------------|--------------|
| Assets | | |
| Liabilities | | |
| Gap | | |

## Basis Risk Exposure
[Quantified basis risk by type]

## Hedge Portfolio Assessment
[Coverage ratios, effectiveness, roll-off schedule]

## Recommendations
1. [Specific hedging or restructuring action with expected impact]
2. [Action]
```

## Analysis Framework

Apply the **Earnings vs. Economic Value dual lens**:
- **Earnings perspective** (NII): Short-to-medium term (1-2 year horizon), captures repricing dynamics, volume effects, and managed-rate behavior. Preferred by management for P&L planning.
- **Economic value perspective** (EVE): Full balance sheet present value, captures long-duration mismatches invisible to NII. Preferred by regulators for structural risk assessment.
- Both perspectives must be reported; conflicts between the two (e.g., a position that protects NII but increases EVE risk) must be explicitly discussed.

## Examples

**Example — Asset-Sensitive Profile Narrative:**
"The bank exhibits moderate asset sensitivity, with a +100bps parallel shock increasing projected 12-month NII by $47M (3.2% of base NII), primarily driven by $18B of floating-rate commercial loans repricing within 90 days against a deposit base with an average behavioral repricing lag of 6 months. EVE declines $210M under the same scenario (4.1% of Tier 1), reflecting a duration gap of +1.8 years. The interest rate swap portfolio provides $23M of NII offset, representing a 49% hedge ratio on the net repricing exposure."

**Example — Basis Risk Highlight:**
"Basis risk contributes $12M of NII volatility per 10bps of SOFR-Fed Funds spread movement. The $6.4B commercial loan book prices off 1M SOFR while $4.1B of the corresponding funding references 3M SOFR, creating a $2.3B tenor basis mismatch concentrated in the 0-3M repricing bucket."

## Guidelines

- Always present both NII and EVE perspectives; never one without the other
- State all rate shocks in basis points and express impacts in both absolute and relative terms
- Clearly separate contractual repricing from behavioral assumptions
- Use effective lower bound (not zero) when applying downward rate shocks
- Present ΔEVE as percentage of Tier 1 capital for regulatory comparability
- Identify and quantify embedded options separately from linear rate sensitivity
- State the yield curve date and source for all scenario analysis

## Validation Checklist

- [ ] Repricing gap sums across buckets equal total balance sheet
- [ ] NII sensitivity decomposition reconciles to total ΔNII
- [ ] EVE computed under all six BCBS prescribed scenarios
- [ ] ΔEVE expressed as % of Tier 1 and compared to 15% outlier threshold
- [ ] Duration gap computed correctly (DA − L/A × DL)
- [ ] Behavioral assumptions for NMDs documented and justified
- [ ] Basis risk exposures identified and quantified
- [ ] Hedge portfolio mapped to underlying exposures with coverage ratios
- [ ] Both earnings and economic value perspectives presented
- [ ] All rate shocks and curves dated and sourced
