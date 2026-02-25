---
name: digital-channel-migration-analysis
description: Analyze customer channel shift patterns from physical to digital banking channels. Use when measuring digital adoption rates, evaluating digital banking KPIs, assessing channel migration impact on branch operations, optimizing omnichannel strategy, or supporting digital transformation business cases.

metadata:
  display_name: "Digital Channel Migration Analysis"
  short_description: "Analyze bank digital channel adoption and migration trends"
  default_prompt: "Analyze my digital channel migration and recommend clear next actions"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Digital Channel Migration Analysis

## Overview

This skill produces structured analyses of customer migration patterns across banking channels (branch, ATM, call center, online, mobile, chatbot). It covers digital adoption measurement, channel preference analysis, migration driver identification, cost-to-serve impact, and omnichannel optimization. Output supports digital transformation strategy, channel investment decisions, and branch network rationalization.

## When to Use

- Measuring digital banking adoption rates and trends across customer segments
- Analyzing which transactions are migrating to digital and which remain branch-dependent
- Evaluating the ROI of digital banking investments
- Assessing the impact of digital migration on branch staffing and format
- Supporting branch consolidation or transformation business cases with channel data
- Optimizing omnichannel customer journeys to reduce friction and cost
- Benchmarking digital KPIs against industry standards

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Channel transaction data | Volume by channel (branch, ATM, mobile, online, call center) | Transaction reporting |
| Customer segmentation | Demographic, product, value tier, digital enrollment status | Customer analytics |
| Digital enrollment data | Mobile/online banking enrollment and active usage rates | Digital banking platform |
| Channel cost data | Cost per transaction by channel | Finance/activity-based costing |
| Customer satisfaction | NPS/CSAT by channel | Survey data |
| Feature adoption | Usage of specific digital features (mobile deposit, Zelle, bill pay) | Platform analytics |
| Time series | Historical data (minimum 8 quarters) for trend analysis | Historical reporting |

## Methodology

### Step 1: Establish Channel Volume Baseline

Document current-state channel distribution:

| Channel | Transaction Volume | % of Total | YoY Change | Cost per Txn |
|---------|-------------------|-----------|------------|--------------|
| Branch (teller) | [N] | [X%] | [X%] | [$X.XX] |
| Branch (platform) | [N] | [X%] | [X%] | [$X.XX] |
| ATM (owned) | [N] | [X%] | [X%] | [$X.XX] |
| ATM (network) | [N] | [X%] | [X%] | [$X.XX] |
| Online banking | [N] | [X%] | [X%] | [$X.XX] |
| Mobile banking | [N] | [X%] | [X%] | [$X.XX] |
| Call center (live) | [N] | [X%] | [X%] | [$X.XX] |
| Call center (IVR) | [N] | [X%] | [X%] | [$X.XX] |
| Chatbot/virtual assistant | [N] | [X%] | [X%] | [$X.XX] |

**Industry benchmark cost per transaction** (approximate):
- Branch teller: $4.00-$5.00
- Call center (live agent): $3.50-$5.00
- ATM: $0.65-$0.85
- Online banking: $0.15-$0.25
- Mobile banking: $0.08-$0.15
- Chatbot: $0.05-$0.10

### Step 2: Measure Digital Adoption KPIs

Track the key digital banking performance indicators:

| KPI | Definition | Current | Prior Year | Benchmark |
|-----|-----------|---------|------------|-----------|
| Digital enrollment rate | Enrolled / eligible customers | [X%] | [X%] | 75-85% |
| Mobile adoption rate | Active mobile users / total customers (90-day) | [X%] | [X%] | 55-65% |
| Digital-active rate | Customers using digital as primary channel | [X%] | [X%] | 50-60% |
| Mobile deposit adoption | Customers using mobile deposit / eligible | [X%] | [X%] | 40-50% |
| P2P payment adoption | Customers using Zelle or equivalent | [X%] | [X%] | 30-40% |
| Digital account opening | % of new accounts opened digitally | [X%] | [X%] | 25-40% |
| Bill pay active users | Active digital bill pay / enrolled | [X%] | [X%] | 35-45% |
| Self-service resolution | Customer issues resolved without agent | [X%] | [X%] | 60-70% |
| Digital engagement | Average logins per active user/month | [N] | [N] | 18-25 |

### Step 3: Analyze Migration Patterns by Transaction Type

Identify which transactions are migrating and which are "branch-sticky":

| Transaction Type | Branch % | Digital % | Migration Velocity | Migratable? |
|-----------------|----------|-----------|-------------------|-------------|
| Balance inquiry | [X%] | [X%] | [Fast/Moderate/Slow] | Fully digital |
| Funds transfer | [X%] | [X%] | [Fast/Moderate/Slow] | Fully digital |
| Bill payment | [X%] | [X%] | [Fast/Moderate/Slow] | Fully digital |
| Check deposit | [X%] | [X%] | [Fast/Moderate/Slow] | Mostly digital |
| Cash deposit | [X%] | [X%] | [Fast/Moderate/Slow] | ATM/ITM only |
| Cash withdrawal | [X%] | [X%] | [Fast/Moderate/Slow] | ATM/ITM only |
| New account opening | [X%] | [X%] | [Fast/Moderate/Slow] | Partially digital |
| Loan application | [X%] | [X%] | [Fast/Moderate/Slow] | Partially digital |
| Problem resolution | [X%] | [X%] | [Fast/Moderate/Slow] | Partially digital |
| Advisory/planning | [X%] | [X%] | [Fast/Moderate/Slow] | Branch-dependent |
| Notary/medallion | [X%] | [X%] | [N/A] | Branch-only |
| Safe deposit access | [X%] | [X%] | [N/A] | Branch-only |

### Step 4: Segment Customer Migration Behavior

Analyze digital adoption by customer segment:

| Segment | Digital Active Rate | Branch Visit Frequency | Preferred Channel | Migration Potential |
|---------|--------------------|-----------------------|-------------------|---------------------|
| Gen Z (18-28) | [X%] | [X/year] | Mobile | Already digital |
| Millennials (29-44) | [X%] | [X/year] | Mobile/Online | Accelerating |
| Gen X (45-60) | [X%] | [X/year] | Mixed | Moderate |
| Baby Boomers (61-78) | [X%] | [X/year] | Branch/Online | Slower |
| Silent/Greatest (79+) | [X%] | [X/year] | Branch | Limited |
| Small business | [X%] | [X/year] | Mixed (cash needs) | Moderate |
| Commercial | [X%] | [X/year] | Online/Treasury mgmt | Specialized |
| Wealth | [X%] | [X/year] | Advisory + digital | Hybrid |

### Step 5: Calculate Financial Impact

Quantify the cost-to-serve impact of channel migration:

**Transaction migration savings**:
- Transactions shifted from branch to digital in past 12 months: [N]
- Average cost differential per transaction: [$X.XX]
- Gross annual savings from migration: [$X]
- Less: Digital platform investment (amortized): -[$X]
- Net annual savings: [$X]

**Branch optimization enabled by digital migration**:
- Branches where teller transaction volume declined >30%: [N]
- FTE reduction opportunity from transaction decline: [N FTEs]
- Branches eligible for format transformation: [N]
- Branch closure candidates (volume + market analysis): [N]
- Estimated savings from network optimization: [$X]

**Revenue impact**:
- Digital cross-sell conversion rates vs. branch
- Customer retention rates by primary channel
- New customer acquisition through digital channels
- Fee income from digital features (instant transfers, digital wallets)

### Step 6: Identify Migration Barriers

Analyze why certain customers or transactions remain branch-dependent:

| Barrier Category | Specific Barriers | Affected Segments | Remediation |
|-----------------|-------------------|-------------------|-------------|
| **Awareness** | Don't know features exist | Older segments, low engagement | Targeted marketing, in-branch demos |
| **Trust** | Don't trust digital for large transactions | Risk-averse, older segments | Security education, guarantees |
| **Capability** | Lack device or digital literacy | Low-income, elderly, rural | Simplified UX, community outreach |
| **Functionality** | Feature not available digitally | All segments | Product roadmap prioritization |
| **Preference** | Prefer human interaction | Relationship-oriented, complex needs | Video banking, scheduled digital advisory |
| **Cash dependency** | Need cash deposits/withdrawals | Small business, cash-intensive | ITM deployment, cash recyclers |
| **Complexity** | Transaction too complex for self-service | Business banking, lending | Guided digital workflows |

### Step 7: Develop Channel Strategy Recommendations

Based on the analysis, provide strategic direction:

**Digital acceleration priorities**:
- Features to develop or enhance based on adoption gaps
- Customer segments with highest migration potential and ROI
- Digital marketing and education initiatives
- UX improvements to reduce abandonment

**Branch network evolution**:
- Branches to transform from transactional to advisory format
- Branches to consolidate based on digital migration and market overlap
- Investment in ITM/ATM to replace routine teller transactions
- Staffing model evolution (universal bankers replacing teller/platform split)

**Omnichannel optimization**:
- Seamless handoff points between digital and physical channels
- Appointment scheduling integration (digital to branch)
- Video banking capability for complex transactions
- Unified customer profile across all channels

## Output Specification

```markdown
# Digital Channel Migration Analysis: [Period]

## Executive Summary
[2-3 sentences on overall digital adoption trajectory, key findings, and strategic implications]

## Channel Distribution
[Current-state channel volume table with YoY trends]

## Digital KPI Dashboard
[KPI table with current values, targets, and benchmarks]

## Migration Analysis
### Transaction Migration Patterns
[Transaction type analysis showing what's migrating and what's sticky]

### Customer Segment Analysis
[Digital adoption by demographic and behavioral segment]

## Financial Impact
| Metric | Value |
|--------|-------|
| Transaction cost savings (annualized) | [$X] |
| Digital platform investment | [$X] |
| Net savings | [$X] |
| Branch optimization opportunity | [$X] |

## Migration Barriers
[Analysis of barriers with remediation strategies]

## Strategic Recommendations
### Digital Priorities
- [Priority 1 with expected impact]

### Branch Network Evolution
- [Recommendation with supporting data]

### Omnichannel Improvements
- [Enhancement with customer experience impact]

## Forecast
[3-year channel distribution projection based on current trends]
```

## Analysis Framework

### Digital Maturity Model

Assess the institution's digital maturity stage:
- **Stage 1 — Basic**: Online banking with basic transactions
- **Stage 2 — Mobile-first**: Full mobile capabilities, mobile deposit, P2P
- **Stage 3 — Digital sales**: Account opening, loan applications fully digital
- **Stage 4 — Intelligent**: AI-powered personalization, predictive servicing, proactive alerts
- **Stage 5 — Ecosystem**: Open banking, embedded finance, marketplace integration

### Channel Elasticity Analysis

Measure how responsive transaction migration is to digital improvements:
- For each digital feature launch, measure the reduction in corresponding branch transactions
- Calculate the "substitution rate": % of branch transactions replaced per feature adoption point
- Identify features with highest channel substitution elasticity for investment prioritization

## Examples

**Example 1 — Digital Migration Dashboard**:
"Q3 2025 digital migration report: Mobile banking active users reached 62% of the customer base (up from 54% in Q3 2024), while branch teller transactions declined 14% YoY. Mobile deposit now handles 38% of all check deposits (up from 28%). Key finding: bill payment is 89% digital, but new account opening remains 71% branch-based due to identity verification friction in the digital flow. The 8% of customers who are branch-only (no digital enrollment) account for 24% of teller transactions. Cost-to-serve impact: $2.3M in annualized transaction cost savings from digital migration, offset by $1.1M in platform investment, yielding $1.2M net savings. Recommendation: prioritize digital account opening redesign with embedded identity verification to reduce the largest remaining branch-dependent activity."

**Example 2 — Branch Format Decision**:
"Digital migration analysis for Branch #0339 (Westside): Teller transactions declined 42% over 3 years (2022-2025) while digital adoption among branch customers reached 71%. Remaining teller transactions are 55% cash-related (deposits and withdrawals). Platform activity (account opening, advisory) remained stable at 12 interactions/day. Recommendation: Transform to advisory format — replace 4 teller windows with 2 ITMs, reduce teller FTEs from 4 to 1 universal banker, maintain 2 platform/advisory staff. Expected expense reduction: $185K annually. Customer impact: ITM provides 24/7 access for cash transactions with live video teller during business hours. Risk: 8% of branch customers (predominantly 65+) have not adopted digital banking; implement a 90-day assisted migration program before format change."

## Guidelines

- Use minimum 8 quarters of historical data for trend analysis to establish reliable trajectories
- Define "active" digital user consistently (industry standard: logged in within 90 days)
- Separate enrollment (signed up) from active usage (using regularly); enrollment alone is insufficient
- Cost-per-transaction calculations should use activity-based costing, not simple averages
- Account for channel interactions that span multiple channels (started online, completed in branch)
- Consider accessibility requirements (ADA, elderly, low-income) before reducing physical channel access
- CRA obligations may constrain branch closure decisions in LMI assessment areas
- Digital adoption benchmarks vary significantly by institution size and market demographics
- Include both customer adoption and employee adoption of digital tools in the analysis
- Present channel migration as opportunity, not threat, to stakeholders; focus on experience improvement

## Validation Checklist

- [ ] Channel volumes are sourced from authoritative transaction systems, not estimates
- [ ] Digital KPIs use consistent definitions across time periods
- [ ] Transaction type migration analysis identifies both migrating and sticky transactions
- [ ] Customer segmentation includes demographic, behavioral, and value dimensions
- [ ] Financial impact calculation includes both savings and investment costs
- [ ] Migration barriers are identified with specific remediation strategies
- [ ] Branch network implications are assessed with CRA considerations
- [ ] Benchmarks are sourced and appropriate for institution size and market
- [ ] Forecast methodology and assumptions are transparent
- [ ] Recommendations balance cost optimization with customer experience and accessibility
