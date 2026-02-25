---
name: stress-liquidity-narratives
description: Explain stress liquidity impact scenarios including contingency funding plans, survival horizon analysis, stress LCR, and idiosyncratic/systemic liquidity stress events. Use when drafting ILAAP stress sections, explaining CFP activation triggers, or narrating liquidity stress test outcomes for ALCO or regulators.

metadata:
  display_name: "Stress Liquidity Narratives"
  short_description: "Narrate liquidity stress test scenarios and impact"
  default_prompt: "Summarize my stress liquidity with key findings and next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Stress Liquidity Narratives

## Overview

Generates narratives explaining the bank's resilience under liquidity stress scenarios—idiosyncratic, market-wide, and combined—covering survival horizons, contingency funding plan (CFP) activation, stress LCR projections, counterbalancing capacity deployment, and management actions. Designed for ILAAP submissions, recovery plan liquidity sections, ALCO stress reporting, and regulatory dialogue.

## When to Use

- Drafting liquidity stress test narrative sections of ILAAP
- Explaining contingency funding plan trigger status and escalation procedures
- Communicating survival horizon analysis to ALCO or board
- Preparing recovery plan liquidity indicators and calibration rationale
- Responding to supervisory liquidity stress test feedback
- Narrating reverse stress test results for liquidity risk

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Stress scenarios | Defined idiosyncratic, market-wide, and combined scenarios with parameters | Scenario definitions |
| Cash-flow projections | Stressed inflows and outflows by time bucket per scenario | Time-bucketed tables |
| Counterbalancing capacity | Unencumbered assets by liquidity class, repo haircuts, central bank eligibility | Asset inventory |
| CFP triggers | Early-warning indicators, escalation thresholds, activation criteria | Trigger framework |
| Stress LCR | LCR under each stress scenario with modified run-off rates | Scenario-specific ratios |
| Historical stress data | Observed deposit outflows, wholesale funding access during past events | Historical data points |
| Management actions | Predetermined actions with estimated liquidity impact and execution timeline | Action catalog |

## Methodology

### Step 1 — Define the Stress Scenario Taxonomy

Establish three canonical stress types with clear parameters:

**Idiosyncratic stress** (institution-specific crisis):
- Trigger: Rating downgrade (2+ notches), operational loss event, fraud allegation, regulatory enforcement action
- Deposit outflows: Retail 5-10% over 30 days, wholesale/institutional 30-50% at maturity
- Wholesale market access: Fully closed for unsecured; secured available at stressed haircuts
- Derivatives: Collateral calls from rating-trigger CSAs, increased initial margin
- Duration: 30-90 days to stabilization

**Market-wide stress** (systemic event):
- Trigger: Credit market freeze, sovereign crisis, banking sector contagion
- Deposit outflows: Retail 3-5% (flight-to-quality may benefit strong institutions), wholesale 10-20%
- Wholesale markets: Unsecured spreads +200-400bps, secured haircuts widen 10-25%, term markets closed
- Asset liquidation: Fire-sale discounts of 5-20% on non-sovereign HQLA
- Duration: 90-180 days

**Combined stress** (idiosyncratic during systemic event):
- Overlay both scenarios simultaneously
- Represents the severest but plausible liquidity stress
- No assumed access to unsecured wholesale markets
- Deposit outflows at the higher of both scenarios
- Counterbalancing capacity subject to maximum haircuts

### Step 2 — Project Stressed Cash Flows

For each scenario, model stressed inflows and outflows across time buckets (daily for week 1, weekly for month 1, monthly thereafter):

**Outflows under stress:**
- Retail deposit withdrawals: Apply scenario-specific run-off rates by product and channel (digital deposits typically higher run-off)
- Wholesale funding non-renewal: Apply rollover assumptions (0% for unsecured CP under idiosyncratic, 50% for secured)
- Derivative collateral calls: Rating-trigger CSAs, variation margin from market moves, increased initial margin
- Committed facility drawdowns: Apply stressed drawdown rates (10-30% for committed credit facilities)
- Intraday liquidity: Payment and settlement obligations

**Inflows under stress:**
- Contractual loan repayments (apply haircut for delayed payments)
- Maturing investment securities (sovereign only under severe stress)
- Central bank facility access (available stable funding, not new borrowing)
- Exclude any discretionary inflows (new lending can be curtailed)

### Step 3 — Calculate the Survival Horizon

The survival horizon is the number of days the bank can meet all obligations using only:
1. Maturing assets (net of haircuts)
2. Monetization of counterbalancing capacity (unencumbered HQLA and central bank eligible assets)
3. Committed central bank facilities

**No access** to unsecured wholesale markets or new deposit gathering.

Calculate for each scenario:
- **Cumulative net cash position** = Running sum of (Inflows + CBC monetization − Outflows)
- **Survival point** = Day on which cumulative position reaches zero
- **Survival horizon** = Number of days from stress onset to survival point
- Internal minimum: Typically 90 days for combined stress, 180 days for idiosyncratic alone

### Step 4 — Assess Counterbalancing Capacity Deployment

Map the monetization of the CBC over the stress horizon:
- **Day 1-5**: Central bank reserves, overnight reverse repo unwinds
- **Day 1-7**: Level 1 HQLA liquidation (sovereigns, central bank deposits) at minimal haircut
- **Day 7-14**: Level 2A HQLA liquidation at 15% haircut, repo of eligible collateral
- **Day 14-30**: Level 2B HQLA liquidation at 25-50% haircut, fire-sale of non-HQLA liquid assets
- **Day 30+**: Central bank emergency lending facilities (discount window, ELA), if accessible

Track the **encumbrance waterfall**: As assets are pledged or sold, remaining unencumbered capacity diminishes. Show the time-series of available vs. deployed CBC.

### Step 5 — Map CFP Triggers and Escalation

Document the contingency funding plan activation framework:

| Phase | Trigger | Indicators | Actions | Authority |
|-------|---------|------------|---------|-----------|
| **Monitoring** | Normal operations | All indicators green | Standard liquidity management | Treasury |
| **Heightened Alert** | Early-warning breach | LCR declining trend, deposit outflows >1σ, CDS widening | Enhanced monitoring, pre-position collateral | Treasury Head |
| **Contingency** | Material stress | LCR <120%, survival horizon <120 days, wholesale market closure | Activate CBC monetization, halt new lending growth | ALCO |
| **Crisis** | Severe stress | LCR <105%, survival horizon <90 days, rating downgrade | Full CFP activation, engage regulator, management actions | CEO / Board |

For each phase, document the specific management actions available, their estimated liquidity impact, and execution timeline.

### Step 6 — Compute Stress LCR

Calculate LCR under each stress scenario using modified parameters:
- Adjust HQLA stock for fire-sale haircuts and encumbrance changes
- Apply stressed outflow rates (higher than regulatory standard for institution-specific calibration)
- Apply stressed inflow caps and haircuts
- Compare stress LCR to the regulatory 100% minimum and internal targets
- Identify the binding scenario (lowest stress LCR) and the primary driver

### Step 7 — Construct the Stress Narrative

Structure the narrative per scenario:
1. **Scenario description**: What triggers the stress, severity, and duration
2. **Impact timeline**: Phase-by-phase evolution of the liquidity position
3. **Survival statement**: Survival horizon with confidence level
4. **CBC deployment**: How and when counterbalancing capacity is used
5. **CFP activation**: Which triggers are breached and what management actions are taken
6. **Residual risk**: Remaining vulnerabilities and assumptions that could worsen outcomes
7. **Recovery path**: Expected stabilization trajectory and conditions for return to normal

## Output Specification

```markdown
# Stress Liquidity Analysis — [Scenario Name]

## Scenario Summary
- **Type**: [Idiosyncratic / Market-wide / Combined]
- **Trigger**: [Description]
- **Duration**: [Expected length]
- **Severity**: [Calibration basis]

## Cash Flow Impact (30-Day Horizon)
| Time Bucket | Outflows ($M) | Inflows ($M) | Net ($M) | Cumulative ($M) |
|-------------|---------------|--------------|----------|-----------------|

## Survival Horizon
- Survival horizon: [X] days under [scenario]
- Internal minimum: [Y] days
- Headroom: [X-Y] days
- Binding constraint: [What exhausts first]

## Counterbalancing Capacity Deployment
| Day | CBC Available ($B) | CBC Deployed ($B) | Remaining ($B) |
|-----|--------------------|--------------------|----------------|

## CFP Trigger Status
| Indicator | Current | Trigger Level | Status | Phase |
|-----------|---------|---------------|--------|-------|

## Stress LCR
| Scenario | Stress LCR | Δ vs Base LCR | Status vs 100% |
|----------|-----------|---------------|----------------|

## Management Actions
| Action | Liquidity Impact ($M) | Execution Time | Feasibility |
|--------|-----------------------|----------------|-------------|

## Recovery Path
[Expected trajectory to normalization]
```

## Analysis Framework

Apply the **Three Lines of Liquidity Defense**:
1. **First line — Operating liquidity**: Day-to-day cash management, intraday liquidity, operational cash buffers
2. **Second line — Counterbalancing capacity**: HQLA buffer, central bank eligible collateral, committed facilities
3. **Third line — Contingency actions**: Asset sales, balance sheet deleveraging, emergency central bank facilities, capital market access (if available)

Each stress scenario should show at which point each line of defense is exhausted and the next is activated.

## Examples

**Example — Idiosyncratic Stress Narrative:**
"Under the idiosyncratic scenario triggered by a two-notch rating downgrade to BBB+, the bank faces $8.2B of cumulative outflows over 30 days, comprising $3.1B of wholesale funding non-renewal, $2.4B of derivative collateral calls from rating-trigger CSAs, and $2.7B of institutional deposit outflows. The counterbalancing capacity of $14.6B (including $9.8B of Level 1 HQLA) provides a survival horizon of 124 days, exceeding the 90-day internal minimum by 34 days. CFP Phase 2 (Heightened Alert) activates on Day 3 as the LCR projection falls below 120%. No Phase 3 activation is anticipated under this scenario."

**Example — Combined Stress Narrative:**
"The combined stress scenario overlays an idiosyncratic 2-notch downgrade onto a market-wide credit freeze, producing $12.7B of cumulative 30-day outflows. The survival horizon compresses to 87 days, breaching the 90-day internal minimum by 3 days. CFP Phase 3 (Contingency) activates on Day 8, triggering $2.3B of management actions including halting new loan originations ($1.1B liquidity preservation), accelerating $800M of planned ABS issuance, and liquidating $400M of non-core equity investments. With management actions, the effective survival horizon extends to 108 days."

## Guidelines

- Calibrate scenario severity to historical precedent (e.g., GFC, SVB, European sovereign crisis)
- State all outflow assumptions explicitly with behavioral justification
- Never assume access to unsecured wholesale markets under idiosyncratic or combined stress
- Distinguish between contractual (committed) and discretionary (uncommitted) liquidity sources
- Include management actions only if they are pre-approved, documented, and executable within stated timelines
- Apply central bank facility access conservatively (available but not assumed for survival calculation)
- Show the full time-series of cumulative net cash position, not just the endpoint

## Validation Checklist

- [ ] Three canonical scenario types defined with distinct parameters
- [ ] Outflow rates calibrated to historical stress events with justification
- [ ] Inflows haircut appropriately (no optimistic inflow assumptions)
- [ ] Survival horizon calculated as days to cumulative net cash zero
- [ ] CBC deployment sequenced by liquidity priority (Level 1 first)
- [ ] CFP triggers mapped to specific quantitative indicators
- [ ] Management actions quantified and assessed for execution feasibility
- [ ] Stress LCR computed with scenario-specific modified parameters
- [ ] Combined scenario represents overlay (not average) of idiosyncratic and market-wide
- [ ] Recovery path stated with qualifying conditions
