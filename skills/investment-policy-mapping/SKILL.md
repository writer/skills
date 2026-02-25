---
name: investment-policy-mapping
description: Map client portfolios against their Investment Policy Statement (IPS) to verify compliance with allocation targets, asset class constraints, and risk parameters. Use when conducting IPS compliance reviews, preparing portfolio rebalancing recommendations, onboarding new clients with existing IPS documents, or documenting fiduciary adherence for ERISA or trust accounts.

metadata:
  display_name: "Investment Policy Mapping"
  short_description: "Check portfolio compliance against IPS allocation guidelines"
  default_prompt: "Map my investment policy and show key friction points and improvements"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Investment Policy Mapping

## Overview

Systematically compare actual portfolio holdings against the constraints, targets, and guidelines defined in the client's Investment Policy Statement. This skill identifies deviations from IPS-mandated allocation ranges, prohibited holdings, liquidity requirements, income needs, and risk parameters, then generates compliant rebalancing recommendations. Outputs support fiduciary documentation for trust and ERISA accounts and demonstrate adherence to Reg BI suitability standards.

## When to Use

- Periodic IPS compliance reviews (quarterly or semi-annual)
- Post-rebalancing verification that all IPS constraints are satisfied
- New client onboarding with an existing IPS from a prior advisor
- IPS revision — comparing current holdings against proposed new IPS targets
- Fiduciary documentation for trust, ERISA, or institutional accounts
- Regulatory examination preparation demonstrating systematic compliance

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Investment Policy Statement | Complete IPS with targets, ranges, and constraints | PDF or structured doc |
| Portfolio holdings | Current positions with market values and classifications | Custodian data |
| Benchmark data | IPS-designated benchmark(s) with component weights | Index data |
| Performance data | Account and benchmark returns by period | Performance report |
| Risk metrics | Portfolio volatility, beta, Sharpe ratio, max drawdown | Risk analytics |
| Transaction history | Recent trades and cash flows for context | Account activity |
| Client profile | Updated risk tolerance, goals, time horizon | Client records |

## Methodology

### Step 1 — IPS Constraint Extraction

Parse the IPS to extract all testable constraints and parameters:

**Allocation Targets and Ranges:**

| Asset Class | Target | Minimum | Maximum | Current | Status |
|-------------|--------|---------|---------|---------|--------|
| US Large Cap Equity | XX% | XX% | XX% | XX% | [In/Out] |
| US Small/Mid Cap Equity | XX% | XX% | XX% | XX% | [In/Out] |
| International Developed | XX% | XX% | XX% | XX% | [In/Out] |
| Emerging Markets | XX% | XX% | XX% | XX% | [In/Out] |
| US Investment Grade FI | XX% | XX% | XX% | XX% | [In/Out] |
| High Yield / Credit | XX% | XX% | XX% | XX% | [In/Out] |
| Real Assets | XX% | XX% | XX% | XX% | [In/Out] |
| Alternatives | XX% | XX% | XX% | XX% | [In/Out] |
| Cash / Short-term | XX% | XX% | XX% | XX% | [In/Out] |

**Additional Constraints:**
- Prohibited investments (e.g., tobacco, firearms, gambling — ESG screens)
- Single security concentration limits (typically ≤5% or ≤10% per position)
- Credit quality minimums for fixed income (e.g., minimum BBB-/Baa3)
- Duration range for fixed income portfolios
- Liquidity requirements (% of portfolio liquidable within 5 business days)
- Income generation requirements (minimum annual distribution yield)
- Tax management directives (loss harvesting, gain deferral, asset location)

### Step 2 — Holdings Classification and Mapping

Map each portfolio holding to the IPS asset class taxonomy:

- Classify every position into the IPS-defined asset class categories
- Resolve ambiguous holdings (e.g., balanced funds split across equity/FI, REITs classified as real assets or equity)
- Handle multi-asset funds by look-through to underlying allocation when available
- Classify cash across categories (cash as strategic allocation vs. frictional cash)
- Map alternative investments (hedge funds, private equity, private credit) to IPS categories
- Flag any holdings that do not fit any IPS category as "unclassified — action required"

### Step 3 — Compliance Testing

Test the portfolio against every IPS constraint:

**Allocation compliance:**
- Calculate current weight of each asset class
- Compare to IPS minimum and maximum ranges
- Flag any asset class outside its permitted range
- Calculate the magnitude of each deviation (percentage points out of range)
- Prioritize deviations by materiality and duration (recently drifted vs. persistently out of range)

**Security-level compliance:**
- Check single-position concentration against limits
- Screen all holdings against prohibited investment list
- Verify fixed income credit quality meets minimum standards
- Check portfolio duration against IPS-specified range
- Verify counterparty exposure limits for alternatives

**Risk and return compliance:**
- Compare portfolio volatility to IPS-specified risk budget
- Verify tracking error vs. benchmark is within IPS tolerance
- Check portfolio beta relative to benchmark
- Assess drawdown experience vs. IPS maximum drawdown tolerance
- Compare Sharpe ratio to benchmark Sharpe ratio

### Step 4 — Deviation Analysis and Root Cause

For each deviation identified, determine the root cause:

- **Market drift**: Asset class outperformance/underperformance caused allocation shift
- **Cash flow impact**: Contributions, withdrawals, or income reinvestment altered allocation
- **Manager action**: Active manager positioning moved the allocation
- **Deliberate tilt**: Advisor intentionally deviated (requires documentation)
- **New investment**: Recent addition that was not yet rebalanced
- **Stale classification**: Holding characteristics changed (e.g., credit downgrade moved a bond below minimum quality)

### Step 5 — Rebalancing Recommendations

Generate specific, actionable rebalancing trades:

- **Priority 1**: Correct any compliance violations (prohibited holdings, concentration breaches)
- **Priority 2**: Bring out-of-range asset classes back within IPS ranges
- **Priority 3**: Move toward target weights from within-range-but-off-target positions
- **Tax-aware sequencing**: Prioritize selling positions with losses or minimal gains; defer large embedded gains
- **Transaction cost consideration**: Avoid rebalancing immaterial deviations where trading costs exceed benefit
- **Rebalancing threshold**: Only trade when deviation exceeds the specified rebalancing band (typically ±3–5%)

Generate a specific trade list:

| Action | Security | Shares/Units | Estimated Amount | Asset Class Impact | Tax Impact |
|--------|----------|-------------|-----------------|-------------------|------------|
| Sell | [Ticker] | XXX | $XX,XXX | Reduces [Class] by X% | [ST/LT Gain/Loss] |
| Buy | [Ticker] | XXX | $XX,XXX | Increases [Class] by X% | N/A |

### Step 6 — Performance Attribution vs. IPS Benchmark

Compare portfolio performance to the IPS-designated benchmark:

- **Total return comparison**: Portfolio vs. benchmark for QTD, YTD, 1Y, 3Y, 5Y, inception
- **Brinson attribution**: Decompose excess return into allocation effect, selection effect, and interaction effect
- **Risk-adjusted metrics**:
  - Sharpe ratio: (Portfolio return - Risk-free rate) / Portfolio std dev
  - Information ratio: Excess return / Tracking error
  - Sortino ratio: Excess return / Downside deviation
- **Benchmark appropriateness**: Confirm the IPS benchmark remains suitable for the client's current objectives

### Step 7 — Compliance Report Generation

Produce the final IPS compliance report:

## Output Specification

```
## IPS Compliance Report — [Client Name] — [Date]

### Compliance Summary
- Overall IPS compliance: [Compliant / Non-Compliant]
- Deviations identified: [N]
- Critical violations: [N]
- Rebalancing recommended: [Yes/No]

### Asset Allocation Compliance
| Asset Class | Target | Range | Current | Deviation | Status |
|-------------|--------|-------|---------|-----------|--------|
| [Class] | XX% | XX–XX% | XX.X% | +/- X.X% | [✓/✗] |

### Security-Level Compliance
- Prohibited holdings: [None / List]
- Concentration breaches: [None / List]
- Credit quality violations: [None / List]
- Duration compliance: [Within range / Out of range]

### Risk Compliance
| Metric | IPS Limit | Current | Status |
|--------|-----------|---------|--------|
| Volatility | ≤ XX% | XX.X% | [✓/✗] |
| Max drawdown | ≤ XX% | XX.X% | [✓/✗] |
| Tracking error | ≤ XX% | X.X% | [✓/✗] |

### Performance vs. Benchmark
| Period | Portfolio | Benchmark | Excess | Attribution |
|--------|-----------|-----------|--------|-------------|
| QTD | X.X% | X.X% | +/- X.X% | [Allocation/Selection] |
| YTD | X.X% | X.X% | +/- X.X% | [Allocation/Selection] |
| 1Y | X.X% | X.X% | +/- X.X% | [Allocation/Selection] |

### Recommended Rebalancing Trades
[Trade list with tax impact analysis]

### Advisor Certification
- Reviewed by: [Advisor name]
- Date: [Review date]
- Next review date: [Date]
```

## Analysis Framework

Apply the **CIGAR** framework:

- **C**onstraints — Extract all IPS constraints into testable criteria
- **I**nventory — Classify every holding against the IPS taxonomy
- **G**ap analysis — Identify all deviations from targets and ranges
- **A**ction — Generate prioritized, tax-aware rebalancing recommendations
- **R**eport — Document compliance status for fiduciary records

## Examples

**Example 1 — Equity Drift After Bull Market**

Client IPS targets 60% equity / 35% FI / 5% cash with ±5% bands. Current: 68% equity / 28% FI / 4% cash. Equity is 3 percentage points above the maximum (65%). Root cause: US Large Cap equity returned 22% YTD while FI returned 2%. Recommendation: Sell $142K US Large Cap equity (prioritize lots with losses for tax harvesting), purchase $128K intermediate bond fund and $14K to cash. Post-rebalance: 60.5% equity / 34.5% FI / 5% cash — all within IPS ranges.

**Example 2 — ERISA Plan Compliance Violation**

ERISA 401(k) plan IPS prohibits single-stock positions exceeding 10%. Employer stock (ESOP) has grown to 14.2% of plan assets through appreciation. This is a fiduciary compliance violation requiring immediate attention. Recommendation: Diversify employer stock to bring below 10% within 30 days, provide QDIA-compliant notification to participants, document the remediation in committee minutes.

## Guidelines

- Review IPS compliance at least quarterly for managed accounts; monthly for institutional/trust
- Document all deviations with root cause and planned remediation timeline
- Tax implications must be modeled before executing any rebalancing trades
- For ERISA accounts, maintain committee-level documentation of compliance reviews
- Ensure the IPS itself remains current — recommend IPS revision if client circumstances have changed materially
- Use look-through analysis for fund-of-funds and multi-asset holdings
- Apply rebalancing bands to avoid excessive trading on immaterial deviations
- Keep a compliance exception log with advisor justification for any intentional deviations

## Validation Checklist

- [ ] All IPS constraints extracted and documented as testable criteria
- [ ] Every holding classified into the IPS asset class taxonomy (no unclassified positions)
- [ ] Allocation compliance tested against ranges (not just targets)
- [ ] Security-level checks completed (concentration, prohibited, credit quality)
- [ ] Risk metrics calculated and compared to IPS limits
- [ ] Deviations root-caused (market drift, cash flow, manager action, deliberate tilt)
- [ ] Rebalancing trades are tax-aware with gain/loss impact estimated
- [ ] Performance attribution completed using Brinson or comparable methodology
- [ ] Report includes advisor certification and next review date
- [ ] ERISA/trust fiduciary documentation meets DOL/state law requirements
