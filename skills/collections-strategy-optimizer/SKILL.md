---
name: collections-strategy-optimizer
description: Optimize collections strategies using segmentation, channel effectiveness analysis, and recovery maximization modeling. Use when designing collection workflows, allocating collector resources, evaluating third-party agency performance, analyzing roll rates, or maximizing recovery while minimizing cost-to-collect and borrower friction.

metadata:
  display_name: "Collections Strategy Optimizer"
  short_description: "Optimize debt collection strategies and recovery rates"
  default_prompt: "Optimize my collections strategy and suggest the best next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Collections Strategy Optimizer

## Overview

Design and optimize collections strategies that maximize recovery rates while minimizing cost-to-collect and maintaining regulatory compliance. This skill segments delinquent accounts by risk, balance, and behavioral characteristics, then maps optimal contact strategies, channel selection, treatment intensity, and escalation paths. Outputs include champion/challenger test designs, agency placement optimization, and recovery forecasting models.

## When to Use

- Designing or refreshing internal collections treatment strategies
- Optimizing contact channel mix (call, text, email, letter, digital)
- Allocating collector capacity across delinquency buckets
- Evaluating and benchmarking third-party collection agency performance
- Analyzing roll rates to identify intervention timing sweet spots
- Building champion/challenger testing frameworks for strategy improvement
- Forecasting recovery amounts for reserve and P&L planning

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Delinquent inventory | All accounts 1+ DPD with current status | Loan-level extract |
| Contact history | All collection attempts, channels, outcomes | CRM/dialer data |
| Payment history | Post-delinquency payment patterns | Servicing system |
| Roll rate data | Historical state-to-state transition rates | Monthly snapshots |
| Collector performance | Calls, contacts, promises, payments by collector | Workforce data |
| Agency scorecards | Third-party agency placement volumes and recoveries | Agency reporting |
| Cost data | Cost per contact attempt by channel, agency fees | Finance data |

## Methodology

### Step 1 — Delinquent Portfolio Segmentation

Segment the delinquent inventory into actionable treatment groups:

- **Delinquency stage**: Early (1–29 DPD), Mid (30–59 DPD), Late (60–89 DPD), Severe (90+ DPD), Charge-off
- **Balance tier**: Micro (<$1K), Small ($1K–$10K), Medium ($10K–$50K), Large (>$50K)
- **Collectability score**: Model-derived probability of curing within 90 days
  - High collectability (>60%): Self-cure likely, light touch
  - Medium collectability (30–60%): Responsive to contact, standard treatment
  - Low collectability (<30%): Intensive treatment or agency placement candidate
- **Behavioral segment**: First-time delinquent, chronic delinquent, broken-promise, skipped, hardship
- **Contact accessibility**: Right-party contact rate, phone/email validity, channel preference

### Step 2 — Roll Rate Analysis and Intervention Timing

Analyze historical roll rates to identify optimal intervention points:

- Calculate monthly roll rates: Current → 30 → 60 → 90 → charge-off
- Identify the **critical intervention window**: the delinquency stage with the highest marginal impact of contact on cure rate
- Compute **self-cure rates** by stage and segment (typically 60–70% of 30 DPD accounts self-cure)
- Calculate the **net roll rate** (gross rolls minus cures) for each stage transition
- Determine the **point of diminishing returns**: stage beyond which incremental contact investment yields insufficient recovery

### Step 3 — Channel Optimization

Evaluate and optimize the contact channel mix:

| Channel | Cost per Contact | Right-Party Contact Rate | Promise Rate | Payment Rate |
|---------|-----------------|------------------------|-------------|-------------|
| Outbound call | $X.XX | XX% | XX% | XX% |
| Predictive dialer | $X.XX | XX% | XX% | XX% |
| SMS/text | $X.XX | XX% | XX% | XX% |
| Email | $X.XX | XX% | XX% | XX% |
| Letter/notice | $X.XX | N/A | XX% | XX% |
| Digital (app/portal) | $X.XX | XX% | XX% | XX% |

Optimize channel selection by segment:
- Early stage + high collectability → Digital self-service + SMS reminder
- Early stage + medium collectability → Automated call + email + SMS sequence
- Mid stage + any collectability → Live collector call with digital follow-up
- Late stage + low collectability → Intensive multi-channel blitz or agency placement

### Step 4 — Treatment Waterfall Design

Build a sequenced treatment waterfall for each segment:

```
Day 1–5:   Automated reminder (SMS + email)
Day 6–10:  IVR outbound call + digital portal notification
Day 11–15: Live collector call attempt (3 attempts across different times)
Day 16–20: Right-party contact letter + supervisor escalation
Day 21–25: Hardship assessment offer + payment plan proposal
Day 26–30: Final demand notice + agency placement evaluation
```

Define escalation triggers, attempt limits per channel, contact frequency caps (Reg F compliance: 7 calls per 7 days per account), and time-of-day windows (8am–9pm borrower local time).

### Step 5 — Collector Workforce Optimization

Allocate collector resources for maximum recovery per labor hour:

- **Skill-based routing**: Match collector skill level to account complexity
  - Junior: Early-stage, high-collectability accounts
  - Senior: Mid/late-stage, negotiation-intensive accounts
  - Specialist: Hardship, bankruptcy, deceased, litigation
- **Capacity modeling**: Calculate accounts-per-collector ratio by stage and complexity
- **Performance scoring**: Rank collectors by recovery-per-hour, promise-to-pay conversion, and payment-to-promise ratio
- **Queue prioritization**: Score-order accounts within each collector's queue by expected recovery value (balance × collectability score)

### Step 6 — Third-Party Agency Management

Optimize external agency placements:

- **Placement timing**: Determine optimal DPD for agency referral (typically 90–120 DPD for primary, 180+ for secondary)
- **Agency scoring**: Rank agencies by net recovery rate (gross recovery minus fees), complaint rate, and compliance score
- **Allocation strategy**: Split placements across top-performing agencies with holdback for champion/challenger testing
- **Performance benchmarking**: Compare agency-vs-agency and agency-vs-internal recovery on equivalent populations
- **Fee optimization**: Negotiate contingency fee tiers based on age of debt and balance size

### Step 7 — Measurement Framework and Continuous Improvement

Establish metrics for ongoing strategy optimization:

- **Primary KPIs**: Recovery rate, cost-to-collect ratio, cure rate by stage, net loss rate
- **Efficiency KPIs**: Right-party contact rate, promise-to-pay rate, payment-to-promise rate, calls-per-recovery
- **Compliance KPIs**: Complaint rate, CFPB complaint volume, Reg F contact limit adherence, TCPA consent rate
- **Champion/challenger testing**: Continuously test treatment variations with proper randomization, minimum sample sizes, and statistical significance requirements (p < 0.05, 4-week minimum run)

## Output Specification

```
## Collections Strategy Optimization Report — [Period]

### Portfolio Summary
| Stage | Accounts | Balance ($M) | Avg Collectability | Cure Rate | Roll Rate |
|-------|----------|-------------|-------------------|-----------|-----------|
| 1–29 DPD | X,XXX | $XX | XX% | XX% | XX% |
| 30–59 DPD | X,XXX | $XX | XX% | XX% | XX% |
| 60–89 DPD | XXX | $XX | XX% | XX% | XX% |
| 90+ DPD | XXX | $XX | XX% | XX% | XX% |

### Channel Effectiveness
| Channel | Volume | RPC Rate | Promise Rate | Payment Rate | Cost/$ Recovered |
|---------|--------|----------|-------------|-------------|-----------------|
| [Channel] | X,XXX | XX% | XX% | XX% | $X.XX |

### Recommended Treatment Changes
1. [Change]: Expected impact [+X% recovery / -$X cost]
2. [Change]: Expected impact [+X% recovery / -$X cost]

### Agency Performance
| Agency | Placements | Gross Recovery | Net Recovery | Complaints | Rank |
|--------|-----------|---------------|-------------|------------|------|
| [Agency] | X,XXX | XX% | XX% | X.X‰ | [1–N] |

### Active Champion/Challenger Tests
| Test | Hypothesis | Status | Preliminary Result |
|------|-----------|--------|--------------------|
| [Test] | [Hypothesis] | [Running/Complete] | [Result or N/A] |
```

## Analysis Framework

Apply the **SCRA** framework:

- **S**egmentation — Divide inventory into actionable treatment groups
- **C**hannel — Optimize contact channels for each segment by cost-effectiveness
- **R**esource — Allocate collector capacity and agency placements for maximum yield
- **A**nalytics — Measure, test, and continuously improve strategy performance

## Examples

**Example 1 — Early Stage Digital Shift**

Finding: 72% of 1–15 DPD accounts with high collectability scores self-cure without live contact. Current strategy calls all accounts at day 5. Recommendation: Replace day-5 call with SMS + email reminder for high-collectability segment, reserve live calls for medium/low collectability. Expected impact: -35% call volume, -$180K annual cost, +0.2pp cure rate (fewer right-party contact failures disrupting self-cure behavior).

**Example 2 — Agency Reallocation**

Finding: Agency B recovers 18.2% net on 90–120 DPD accounts vs. Agency A at 12.4% on equivalent populations. Agency A has operated under a legacy allocation of 60% of placements. Recommendation: Shift to 70% Agency B / 30% Agency A allocation. Project incremental recovery of $2.1M annually on current placement volumes. Maintain 30% Agency A allocation for competitive benchmarking.

## Guidelines

- Comply with FDCPA, Reg F (contact frequency limits), TCPA (consent for auto-dialed calls/texts), and state-specific collection laws
- Cap outbound call attempts at 7 per 7-day period per Reg F safe harbor
- Maintain TCPA express consent records for all automated contact channels
- Document all treatment strategy changes with effective dates and rationale
- Use proper randomization and control groups for champion/challenger testing
- Never combine champion/challenger results across materially different segments
- Review agency compliance certifications (SOC 2, E&O insurance, licensing) annually
- Exclude accounts in active bankruptcy, litigation hold, SCRA protection, or disaster forbearance from standard treatment

## Validation Checklist

- [ ] Segmentation is based on objective, validated scoring models
- [ ] Roll rate analysis uses at least 12 months of historical data
- [ ] Channel cost calculations include fully loaded costs (labor, technology, postage)
- [ ] Treatment waterfall respects all applicable contact frequency limits
- [ ] Collector allocation model accounts for availability, skill level, and language capability
- [ ] Agency performance comparison uses equivalent populations (matched placement characteristics)
- [ ] Champion/challenger tests have adequate sample sizes for statistical significance
- [ ] Compliance KPIs are monitored in real-time with automated breach alerts
- [ ] SCRA, bankruptcy, and disaster-protected accounts are excluded from outbound contact
- [ ] Strategy changes are version-controlled with rollback capability
