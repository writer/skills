---
name: branch-performance-analysis
description: Analyze branch-level performance metrics and generate actionable insights for retail banking branch networks. Use when evaluating branch profitability, productivity, customer acquisition, CRA performance, staffing optimization, or branch network strategy decisions.

metadata:
  display_name: "Branch Performance Analysis"
  short_description: "Analyze retail bank branch performance and productivity"
  default_prompt: "Analyze my branch performance and recommend clear next actions"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Branch Performance Analysis

## Overview

This skill produces comprehensive branch-level performance analyses for retail banking networks. It covers financial performance (profitability, revenue, cost), operational efficiency (productivity, utilization), customer metrics (acquisition, retention, satisfaction), CRA (Community Reinvestment Act) assessment area performance, and strategic recommendations. Output supports branch managers, regional leaders, and executive teams making branch network decisions.

## When to Use

- Producing monthly or quarterly branch performance scorecards
- Evaluating branch profitability and contribution to the network
- Analyzing branch staffing models and productivity optimization
- Assessing CRA performance by assessment area for examination preparation
- Supporting branch opening, closing, or consolidation decisions
- Benchmarking branch performance across the network and against peers
- Identifying top-performing and underperforming branches for best practice sharing

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Financial data | Revenue, expenses, FTP credits/charges, fee income | Branch P&L |
| Balance data | Deposits, loans, AUM originated/held at branch | Balance reports |
| Transaction data | Teller transactions, ATM, platform interactions | Activity reports |
| Customer data | New accounts, closed accounts, households served | CIF/customer data |
| Staffing data | FTEs, roles, compensation, hours, turnover | HR/workforce data |
| Satisfaction data | NPS, CSAT, mystery shop scores, complaint counts | Survey/quality data |
| CRA data | Lending in assessment area, community development activities | CRA reporting |
| Market data | Demographics, competition, market share | Market analysis |

## Methodology

### Step 1: Establish the Branch Financial Profile

Calculate key financial metrics using funds transfer pricing (FTP):

| Metric | Calculation | Branch Value | Network Average |
|--------|------------|--------------|-----------------|
| **Net interest income (FTP-adjusted)** | FTP credit on deposits + FTP credit on loans - funding cost | [$X] | [$X] |
| **Non-interest income** | Fee income (service charges, NSF, interchange, wealth referrals) | [$X] | [$X] |
| **Direct expenses** | Compensation + occupancy + technology + supplies | [$X] | [$X] |
| **Allocated expenses** | Shared services, corporate overhead allocation | [$X] | [$X] |
| **Pre-tax net income** | Total revenue - total expenses | [$X] | [$X] |
| **Efficiency ratio** | Non-interest expense / total revenue | [X%] | [X%] |
| **ROA (branch)** | Net income / average assets attributed | [X%] | [X%] |

**Profitability tiers**:
- **Tier 1 (>120% of network average ROA)**: High performer — best practice extraction
- **Tier 2 (80-120% of average)**: Solid performer — maintain and optimize
- **Tier 3 (50-80% of average)**: Underperformer — improvement plan required
- **Tier 4 (<50% of average)**: Strategic review — evaluate viability or transformation

### Step 2: Analyze Operational Efficiency

Measure branch productivity across dimensions:

| Metric | Definition | Branch Value | Target | Peer Benchmark |
|--------|-----------|--------------|--------|----------------|
| Revenue per FTE | Total revenue / total FTEs | [$X] | [$X] | [$X] |
| Accounts per FTE | Total accounts serviced / FTEs | [N] | [N] | [N] |
| Transactions per teller hour | Teller transactions / teller hours | [N] | [N] | [N] |
| Platform productivity | New accounts + services / platform hours | [N] | [N] | [N] |
| Cross-sell ratio | Products per household | [X.X] | [X.X] | [X.X] |
| Digital adoption rate | % of customers using digital channels | [X%] | [X%] | [X%] |
| Lobby wait time | Average customer wait time | [X min] | [X min] | [X min] |
| Appointment utilization | Appointments scheduled / available slots | [X%] | [X%] | [X%] |

### Step 3: Evaluate Customer Metrics

Assess the branch's customer acquisition and retention performance:

**Acquisition**:
- New accounts opened (by product: checking, savings, CD, loan, LOC)
- New-to-bank households acquired
- Source of new customers (walk-in, referral, digital lead, campaign)
- Average new account initial deposit
- 90-day activation rate (% of new accounts that become active)

**Retention**:
- Account attrition rate (annualized)
- Deposit balance attrition (net outflows)
- Closed account reasons analysis
- At-risk household identification

**Satisfaction**:
- Net Promoter Score (NPS) by branch
- Customer satisfaction (CSAT) survey scores
- Mystery shop scores (service quality, compliance, sales practices)
- Complaint volume and resolution rate
- Google/Yelp ratings and review sentiment

### Step 4: Assess CRA Performance

Evaluate Community Reinvestment Act metrics for the branch's assessment area:

| CRA Component | Metric | Branch/AA Performance | Rating Benchmark |
|--------------|--------|----------------------|-----------------|
| **Lending Test** | % of loans in assessment area | [X%] | Outstanding: >75% |
| | % to LMI borrowers | [X%] | Outstanding: meets/exceeds demographic |
| | % to LMI geographies | [X%] | Outstanding: meets/exceeds demographic |
| | Small business lending (<$1M) | [$XM, N loans] | Peer comparison |
| **Investment Test** | Community development investments | [$XM] | Outstanding: significant |
| **Service Test** | Branch accessibility in LMI areas | [Yes/No] | Outstanding: accessible |
| | Products serving LMI needs | [Product list] | Outstanding: comprehensive |
| | Community development services | [Hours/activities] | Outstanding: significant |

### Step 5: Analyze Staffing Optimization

Evaluate staffing model efficiency:

**Staffing mix analysis**:
- Ratio of platform (sales/service) to teller (transaction) staff
- Manager span of control
- Specialist availability (mortgage, business banking, wealth)
- Part-time vs. full-time mix optimization

**Workload distribution**:
- Transaction volume by hour of day and day of week
- Peak staffing requirements vs. current schedule alignment
- Idle time analysis during low-traffic periods
- Queue analysis during peak periods

**Cost-per-interaction**:
- Teller transaction cost: [$X] (vs. ATM: [$X], mobile: [$X])
- Platform interaction cost: [$X] per account opened
- Overall cost per customer interaction by channel

### Step 6: Benchmark and Rank

Position the branch within the network and against external benchmarks:

**Internal ranking** (across all metrics):
- Financial performance percentile within the network
- Operational efficiency percentile
- Customer metrics percentile
- CRA performance percentile
- Overall composite score and rank

**External benchmarking** (where data is available):
- ABA branch benchmarking survey comparisons
- Federal Reserve Survey of Consumer Finances data
- FDIC Summary of Deposits market share analysis
- Peer group comparison (similar asset-size institutions in market)

### Step 7: Generate Strategic Recommendations

Based on the analysis, provide actionable recommendations:

**For high performers**: Document best practices, consider expansion or format replication
**For average performers**: Identify specific improvement levers (cross-sell, efficiency, acquisition)
**For underperformers**: Develop turnaround plan with milestones and accountability
**For strategic review**: Evaluate consolidation, format change (full-service to advisory), or transformation to digital-first with advisory specialists

Consider market factors:
- Competitive intensity and market share trajectory
- Demographic trends (population growth/decline, income shifts)
- Digital channel migration (is the branch's role shifting from transactional to advisory?)
- Lease/ownership terms and facility condition

## Output Specification

```markdown
# Branch Performance Analysis: [Branch Name/ID]

## Branch Profile
- **Location**: [Address]
- **Market**: [MSA/Assessment Area]
- **Format**: [Full-service / Express / Advisory]
- **Opened**: [Date]
- **Lease/Own**: [Status, expiration if lease]
- **FTEs**: [Count by role]

## Financial Performance
| Metric | Branch | Network Avg | Rank | Trend |
|--------|--------|-------------|------|-------|
| Net interest income | [$X] | [$X] | [#/N] | [↑↓→] |
| Non-interest income | [$X] | [$X] | [#/N] | [↑↓→] |
| Total revenue | [$X] | [$X] | [#/N] | [↑↓→] |
| Total expenses | [$X] | [$X] | [#/N] | [↑↓→] |
| Net income | [$X] | [$X] | [#/N] | [↑↓→] |
| Efficiency ratio | [X%] | [X%] | [#/N] | [↑↓→] |

**Profitability Tier**: [Tier 1/2/3/4]

## Operational Efficiency
[Productivity metrics with benchmarks]

## Customer Performance
[Acquisition, retention, and satisfaction metrics]

## CRA Performance
[Assessment area lending, investment, and service metrics]

## Staffing Analysis
[Staffing model efficiency and optimization opportunities]

## Network Ranking
- **Overall Rank**: [#] of [N] branches
- **Financial Rank**: [#] of [N]
- **Efficiency Rank**: [#] of [N]
- **Customer Rank**: [#] of [N]

## Recommendations
1. [Specific, actionable recommendation with expected impact]
2. [Specific, actionable recommendation with expected impact]
3. [Specific, actionable recommendation with expected impact]

## Action Items
| Action | Owner | Timeline | Expected Impact |
|--------|-------|----------|-----------------|
| [Action] | [Name] | [Date] | [Metric improvement] |
```

## Analysis Framework

### Branch Format Optimization

Evaluate whether the branch format matches its market role:
- **Full-service**: High traffic, complex product needs, strong transactional volume
- **Advisory/consultative**: Lower traffic, high-value relationships, appointment-driven
- **Express/micro**: High foot traffic location, basic transactions, digital enrollment
- **Digital-first with advisor**: Minimal teller, technology-forward, specialist staffing

### Market Share Analysis

Using FDIC Summary of Deposits data:
- Calculate branch deposit market share within the MSA
- Track market share trajectory (gaining, stable, losing)
- Identify competitive threats (new branch openings, digital competitors)
- Assess deposit concentration risk (over-reliance on single branches or customers)

## Examples

**Example 1 — Underperforming Branch**:
"Branch #0247 (Maple Avenue) ranks 78th of 82 branches (Tier 4). Pre-tax net income of -$125K (network average: +$340K). Root causes: (1) Deposit base declined 18% YoY due to loss of two commercial relationships ($8.2M) to competitor offering higher rates; (2) Teller transaction volume declined 35% over 3 years while staffing remained constant (6 FTEs); (3) New account production of 8 accounts/month is 65% below network average. Digital adoption is 42% vs. 68% network average. Recommendation: Transform to advisory format with 3 FTEs (1 manager, 1 platform specialist, 1 teller/universal banker), install ITMs for routine transactions, and reallocate 3 FTEs to growing branches. Expected impact: expense reduction of $195K, breakeven within 12 months."

**Example 2 — CRA Assessment**:
"Branch #0112 (Downtown) assessment area CRA performance: Lending test — 67% of mortgage originations to LMI borrowers/geographies (exceeds demographic benchmark of 52%); small business loans: 142 loans totaling $8.4M (12% above peer). Investment test: $2.1M in LIHTC investments in assessment area. Service test: branch is located in an LMI census tract, offers free checking with no minimum balance, and staff contributed 340 hours of financial literacy education. Overall assessment area performance supports an Outstanding rating. Recommendation: document community development activities more granularly for examiner review; strengthen service test narrative with specific impact metrics."

## Guidelines

- Use FTP-adjusted revenue to fairly compare branches with different balance sheet compositions
- Always contextualize financial performance with market demographics and competitive dynamics
- CRA analysis must align with the institution's assessment area delineation methodology
- Branch rankings should use composite scores, not single-metric rankings
- Staffing recommendations must consider labor market conditions and training investment
- Present trends (minimum 4 quarters) rather than single-point-in-time snapshots
- Account for branch maturity (new branches need 3-5 years to reach profitability)
- Consider impact on CRA obligations before recommending branch closures in LMI areas
- Benchmark against similar-format branches (don't compare micro-branches to flagship locations)
- Include both quantitative metrics and qualitative market intelligence in recommendations

## Validation Checklist

- [ ] Financial performance uses FTP-adjusted revenue for fair comparison
- [ ] All key metrics are compared to network average and peer benchmark
- [ ] Branch ranking methodology is consistent and uses composite scoring
- [ ] Customer metrics cover acquisition, retention, and satisfaction dimensions
- [ ] CRA performance is assessed against demographic benchmarks
- [ ] Staffing analysis considers workload distribution and cost-per-interaction
- [ ] Market context (demographics, competition, trends) informs recommendations
- [ ] Recommendations are specific, quantified, and actionable
- [ ] Trends are presented (minimum 4 quarters) to show trajectory
- [ ] Branch format and lifecycle stage are factored into performance assessment
