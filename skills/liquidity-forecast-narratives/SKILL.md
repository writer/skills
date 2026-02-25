---
name: liquidity-forecast-narratives
description: Generate executive-ready narratives explaining liquidity forecasts, LCR/NSFR positions, HQLA composition, and cash flow projections. Use when explaining liquidity positions, writing ALCO reports, summarizing Basel III liquidity metrics, or narrating funding gaps and surplus positions.

metadata:
  display_name: "Liquidity Forecast Narratives"
  short_description: "Narrate liquidity forecasts and LCR/NSFR positions"
  default_prompt: "Summarize my liquidity forecast with key findings and next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Liquidity Forecast Narratives

## Overview

Produces clear, regulator-aware narratives that translate raw liquidity data—LCR, NSFR, cash-flow ladders, HQLA buffers—into actionable commentary for ALCO committees, board risk reports, and regulatory submissions. The skill bridges quantitative treasury output and stakeholder communication by applying Basel III liquidity framework terminology with business-context interpretation.

## When to Use

- Preparing ALCO meeting packs with liquidity position commentary
- Drafting Internal Liquidity Adequacy Assessment (ILAAP) narrative sections
- Explaining month-over-month or quarter-over-quarter LCR/NSFR movements
- Summarizing contingency funding plan trigger status
- Communicating forecast liquidity surplus or shortfall to senior management
- Responding to regulatory inquiries about liquidity risk posture

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| LCR components | HQLA stock (Level 1, 2A, 2B), total net cash outflows | Numeric with currency |
| NSFR components | Available stable funding (ASF), required stable funding (RSF) | Numeric with currency |
| Cash-flow ladder | Contractual and behavioral cash flows across time buckets (overnight to 12M) | Time-bucketed table |
| HQLA portfolio | Composition by asset class, encumbrance status, currency | Breakdown table |
| Prior period data | Previous reporting period LCR/NSFR and ladder for trend analysis | Same format as current |
| Stress overlays | Management buffer, stress scenario outflows if available | Optional numeric |
| Limit framework | Internal liquidity limits, early-warning indicators, trigger levels | Threshold table |

## Methodology

### Step 1 — Validate Metric Integrity

Confirm that LCR = HQLA Stock / Total Net Cash Outflows over 30 days, and NSFR = ASF / RSF. Cross-check component totals. Flag any data where Level 2B assets exceed the 15% HQLA cap or Level 2 assets exceed the 40% cap after haircuts. Verify currency-matched positions versus consolidated figures.

### Step 2 — Decompose Period-over-Period Movements

Identify the primary drivers of LCR/NSFR changes by decomposing into:
- **Numerator effects**: Changes in HQLA stock (new sovereign bond purchases, maturities, encumbrance changes, rating migrations affecting Level classification)
- **Denominator effects**: Shifts in net cash outflows (deposit flow changes, wholesale funding maturities, drawdown assumptions on committed facilities, derivative collateral calls)
- **Behavioral overlays**: Changes in deposit run-off assumptions, prepayment speeds, or roll-over rates versus contractual terms

### Step 3 — Assess HQLA Quality and Concentration

Evaluate HQLA composition across:
- **Level 1** (sovereigns, central bank reserves, qualifying cash): Target >60% of buffer
- **Level 2A** (covered bonds, qualifying corporates rated AA- or higher): Haircut 15%
- **Level 2B** (lower-rated corporates, RMBS, qualifying equities): Haircut 25-50%
- Concentration by issuer, currency, and jurisdiction
- Monetization readiness: average days to liquidate under stressed conditions

### Step 4 — Interpret the Cash-Flow Ladder

Walk through the contractual maturity ladder:
- Identify **cumulative funding gaps** by time bucket (overnight, 1W, 2W, 1M, 2M, 3M, 6M, 9M, 12M)
- Separate contractual flows from behavioral assumptions (deposit stickiness, loan prepayments)
- Highlight any bucket where the cumulative gap exceeds internal limits or early-warning thresholds
- Note the **survival horizon** — the point at which cumulative outflows exhaust the liquidity buffer without access to unsecured wholesale markets

### Step 5 — Evaluate Limit Utilization and Trigger Proximity

Map current metrics against the internal limit framework:
- **Green zone**: Metric above internal target (e.g., LCR > 120%)
- **Amber zone**: Metric between regulatory minimum and internal target (e.g., LCR 100-120%)
- **Red zone**: Metric at or below regulatory minimum
- Calculate headroom in absolute terms (e.g., "$2.3B HQLA surplus above minimum requirement")
- Flag any early-warning indicators that have been breached or are within 10% of breach

### Step 6 — Construct the Narrative Arc

Structure the narrative following this arc:
1. **Headline position**: One sentence stating the current LCR/NSFR level and directional trend
2. **Key drivers**: Two to three sentences explaining the primary movement factors
3. **HQLA quality commentary**: Assessment of buffer composition and monetization readiness
4. **Forward-looking view**: Expected trajectory based on known maturities, planned issuance, or seasonal deposit patterns
5. **Risk and action items**: Any limit breaches, near-breaches, or management actions required

### Step 7 — Apply Regulatory and Governance Calibration

Tailor language and depth to the audience:
- **ALCO**: Full technical detail, basis-point-level movements, action recommendations
- **Board Risk Committee**: Summarized to traffic-light status, material changes only, strategic implications
- **Regulatory submission**: Precise terminology matching Basel III / CRR2 / local implementing rules, no ambiguity, footnoted assumptions
- **Rating agency**: Emphasis on structural funding stability, diversification, contingency preparedness

## Output Specification

```markdown
# Liquidity Position Narrative — [Period]

## Headline
[LCR] stood at [X]% as of [date], [up/down] [Y]bps from [prior period].
NSFR was [Z]%, [above/below] the internal target of [T]%.

## Key Drivers
- [Driver 1 with quantified impact, e.g., "$500M increase in Level 1 HQLA from sovereign bond purchases lifted the numerator by 4pp"]
- [Driver 2]
- [Driver 3]

## HQLA Composition
| Category | Amount | % of Buffer | Δ vs Prior |
|----------|--------|-------------|------------|
| Level 1  |        |             |            |
| Level 2A |        |             |            |
| Level 2B |        |             |            |

## Cash-Flow Ladder Summary
[Cumulative gap analysis with survival horizon statement]

## Limit Status
| Metric | Current | Limit | Headroom | Status |
|--------|---------|-------|----------|--------|

## Forward Outlook
[Expected trajectory over next 30/90 days with key events]

## Actions Required
- [Action items with owners and deadlines]
```

## Analysis Framework

Apply the **Sources-Uses-Buffer** framework:
- **Sources**: Identify all inflow channels (maturing assets, deposit growth, repo capacity, committed facilities)
- **Uses**: Map all outflow obligations (maturing wholesale funding, deposit attrition, off-balance-sheet commitments, collateral calls)
- **Buffer**: Quantify the unencumbered HQLA stock available to bridge any mismatch
- **Net position**: Sources + Buffer − Uses = Liquidity surplus or deficit per time bucket

## Examples

**Example — LCR Improvement Narrative:**
"The consolidated LCR increased to 138% from 131% at prior quarter-end, driven primarily by a $1.2B increase in Level 1 HQLA following the reinvestment of maturing agency MBS into U.S. Treasuries. Total net cash outflows declined modestly (-$340M) as 30-day wholesale funding maturities rolled into longer-dated tenors. The HQLA buffer now comprises 78% Level 1 assets, well above the internal 60% quality floor. The 90-day survival horizon extends to 147 days under the base case, providing comfortable headroom above the 90-day internal minimum."

**Example — NSFR Deterioration Narrative:**
"NSFR declined 4pp to 108%, reflecting the draw-down of a $2B committed warehouse facility that increased RSF without a corresponding increase in ASF. The shift from term deposits into overnight money-market placements reduced available stable funding by $600M. Management has approved issuance of a $1.5B 3-year senior unsecured bond in Q2, expected to restore NSFR above the 115% internal target."

## Guidelines

- Always state metrics with one decimal place for ratios and whole numbers for absolute amounts
- Use basis points (bps) for period-over-period changes in ratios
- Attribute movements to specific balance-sheet line items, not vague categories
- Distinguish between contractual and behavioral assumptions explicitly
- Never present LCR or NSFR without stating the reporting date and consolidation scope
- Avoid forward-looking statements without qualifying assumptions
- Use consistent terminology: "HQLA" not "liquid assets," "net cash outflows" not "outflows"

## Validation Checklist

- [ ] LCR and NSFR calculated correctly from stated components
- [ ] HQLA caps (Level 2: 40%, Level 2B: 15%) verified post-haircut
- [ ] Period-over-period movements reconcile to stated drivers
- [ ] Cash-flow ladder cumulative gaps foot to total figures
- [ ] Limit status correctly mapped to green/amber/red zones
- [ ] Survival horizon stated and consistent with ladder data
- [ ] Audience-appropriate language applied (ALCO vs board vs regulator)
- [ ] All figures carry currency denomination and reporting date
- [ ] No forward-looking statements without qualifying assumptions
- [ ] Narrative arc follows headline → drivers → quality → outlook → actions
