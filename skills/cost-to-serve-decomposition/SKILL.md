---
name: cost-to-serve-decomposition
description: Decompose customer service costs by channel, product, segment, and activity to identify cost optimization opportunities. Use when analyzing cost-to-serve by customer segment, building activity-based costing models, evaluating channel economics, or supporting pricing and profitability strategy in retail and commercial banking.

metadata:
  display_name: "Cost To Serve Decomposition"
  short_description: "Decompose banking cost-to-serve by channel and segment"
  default_prompt: "Analyze my cost to serve decomposition and recommend clear next actions"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Cost-to-Serve Decomposition

## Overview

This skill produces structured cost-to-serve analyses for banking operations, decomposing total service delivery costs by customer segment, channel, product, and activity. It applies activity-based costing (ABC) methodology to allocate direct and indirect costs to service activities, enabling profitability analysis at the customer level and identification of cost optimization opportunities. Output supports pricing strategy, channel optimization, customer segmentation, and operational efficiency initiatives.

## When to Use

- Building or refining activity-based costing models for banking operations
- Analyzing customer-level profitability by incorporating service costs
- Evaluating the economics of different service delivery channels
- Supporting pricing decisions with cost-to-serve intelligence
- Identifying high-cost activities for automation or process improvement
- Comparing cost-to-serve across customer segments for strategic differentiation
- Preparing business cases for technology or process investments

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Cost center data | Department-level expenses (compensation, occupancy, technology, supplies) | General ledger |
| Activity data | Staff time allocation by activity, transaction volumes | Time study/activity logs |
| Channel data | Interactions by channel (branch, call center, digital, ATM) | Channel reporting |
| Customer data | Segment, products held, transaction frequency, balance | CIF/customer analytics |
| Product data | Products and services with pricing and fee structure | Product catalog |
| Process data | Process maps with step-level effort estimates | Process documentation |
| FTE data | Headcount, compensation, roles, allocation | HR/workforce data |

## Methodology

### Step 1: Define the Cost Hierarchy

Establish the cost allocation structure:

```
Total Operating Cost
├── Direct Costs (attributable to specific activities)
│   ├── Compensation (by role and activity)
│   ├── Transaction processing costs
│   ├── Channel-specific costs (branch occupancy, ATM maintenance, platform fees)
│   └── Product-specific costs (loan origination, card production)
├── Indirect Costs (shared services requiring allocation)
│   ├── Technology infrastructure
│   ├── Compliance and risk management
│   ├── Corporate overhead (HR, finance, legal)
│   └── Marketing and customer acquisition
└── Unallocable Costs (excluded from CTS)
    ├── Strategic investments
    └── One-time restructuring charges
```

### Step 2: Identify and Catalog Activities

Map all customer-facing and support activities:

| Activity Category | Activities | Cost Driver | Unit Cost |
|-------------------|-----------|-------------|-----------|
| **Account servicing** | Account opening, maintenance, closure, statement generation | Per account/month | [$X.XX] |
| **Transaction processing** | Deposits, withdrawals, transfers, payments, wires | Per transaction | [$X.XX] |
| **Customer service** | Call center inquiries, branch inquiries, complaint resolution | Per interaction | [$X.XX] |
| **Lending operations** | Application processing, underwriting, closing, servicing | Per loan | [$X.XX] |
| **Compliance** | KYC/CDD, transaction monitoring, regulatory reporting | Per customer/year | [$X.XX] |
| **Collections** | Delinquency management, workout, recovery | Per delinquent account | [$X.XX] |
| **Dispute resolution** | Reg E claims, chargebacks, error resolution | Per dispute | [$X.XX] |
| **Onboarding** | Welcome, product activation, enrollment, initial training | Per new customer | [$X.XX] |

### Step 3: Allocate Costs Using ABC Methodology

Apply activity-based costing in four steps:

**Step 3a — Resource cost pools**: Group costs by department/cost center
**Step 3b — Resource drivers**: Allocate resource costs to activities based on time/effort
**Step 3c — Activity cost pools**: Aggregate costs for each defined activity
**Step 3d — Activity drivers**: Allocate activity costs to cost objects (customers, products, channels) based on consumption

| Cost Pool | Total Cost | Activity Driver | Driver Volume | Unit Cost |
|-----------|-----------|-----------------|---------------|-----------|
| Branch staffing | [$XM] | Staff-minutes per interaction type | [N minutes] | [$X.XX/min] |
| Call center | [$XM] | Calls handled by type | [N calls] | [$X.XX/call] |
| Digital platform | [$XM] | Active users + transactions | [N users] | [$X.XX/user/mo] |
| Loan operations | [$XM] | Applications processed | [N applications] | [$X.XX/app] |
| Compliance | [$XM] | Customers by risk tier | [N customers] | [$X.XX/cust/yr] |

### Step 4: Calculate Cost-to-Serve by Segment

Aggregate activity costs at the customer segment level:

| Cost Component | Mass Market | Mass Affluent | High Net Worth | Small Business | Commercial |
|---------------|-------------|---------------|----------------|----------------|------------|
| Account servicing | [$X/yr] | [$X/yr] | [$X/yr] | [$X/yr] | [$X/yr] |
| Transaction processing | [$X/yr] | [$X/yr] | [$X/yr] | [$X/yr] | [$X/yr] |
| Channel cost (branch) | [$X/yr] | [$X/yr] | [$X/yr] | [$X/yr] | [$X/yr] |
| Channel cost (digital) | [$X/yr] | [$X/yr] | [$X/yr] | [$X/yr] | [$X/yr] |
| Channel cost (call center) | [$X/yr] | [$X/yr] | [$X/yr] | [$X/yr] | [$X/yr] |
| Compliance cost | [$X/yr] | [$X/yr] | [$X/yr] | [$X/yr] | [$X/yr] |
| Allocated overhead | [$X/yr] | [$X/yr] | [$X/yr] | [$X/yr] | [$X/yr] |
| **Total CTS** | **[$X/yr]** | **[$X/yr]** | **[$X/yr]** | **[$X/yr]** | **[$X/yr]** |
| **Revenue** | **[$X/yr]** | **[$X/yr]** | **[$X/yr]** | **[$X/yr]** | **[$X/yr]** |
| **Net margin** | **[$X/yr]** | **[$X/yr]** | **[$X/yr]** | **[$X/yr]** | **[$X/yr]** |
| **Margin %** | **[X%]** | **[X%]** | **[X%]** | **[X%]** | **[X%]** |

### Step 5: Analyze Cost Drivers and Variation

Identify what drives cost differences between segments and customers:

**High-cost driver analysis**:
- Which activities consume the most cost per customer?
- Which segments have the highest cost-to-serve relative to revenue?
- What is the distribution of CTS within each segment (average vs. P90)?
- Are there specific customer behaviors that drive disproportionate cost?

**Cost variation drivers**:
| Driver | Impact on CTS | Controllable? |
|--------|--------------|---------------|
| Channel preference (branch-heavy vs. digital) | High | Partially (migration programs) |
| Transaction frequency | Medium | Low (customer behavior) |
| Product complexity | Medium | Partially (product design) |
| Service intensity (complaints, calls) | High | Partially (proactive service) |
| Risk tier (compliance cost) | Medium | Low (regulatory driven) |
| Exception frequency | High | Yes (error prevention) |

### Step 6: Identify Optimization Opportunities

Prioritize cost reduction initiatives by impact and feasibility:

| Opportunity | Current Cost | Target Cost | Savings | Feasibility | Priority |
|------------|-------------|-------------|---------|-------------|----------|
| Migrate branch transactions to digital | [$X/yr] | [$X/yr] | [$X/yr] | [H/M/L] | [1-5] |
| Automate routine call center inquiries | [$X/yr] | [$X/yr] | [$X/yr] | [H/M/L] | [1-5] |
| Reduce exception/rework processing | [$X/yr] | [$X/yr] | [$X/yr] | [H/M/L] | [1-5] |
| Optimize compliance cost by risk tier | [$X/yr] | [$X/yr] | [$X/yr] | [H/M/L] | [1-5] |
| Redesign onboarding to reduce activation cost | [$X/yr] | [$X/yr] | [$X/yr] | [H/M/L] | [1-5] |
| Streamline loan origination workflow | [$X/yr] | [$X/yr] | [$X/yr] | [H/M/L] | [1-5] |

### Step 7: Inform Pricing and Strategy

Connect cost-to-serve insights to strategic decisions:

**Pricing alignment**: Are fees and pricing adequate to cover CTS for each segment?
- Identify segments where CTS exceeds revenue (negative margin customers)
- Assess fee elasticity: would price increases cause unacceptable attrition?
- Evaluate tiered pricing models that incentivize low-cost behavior (digital usage, direct deposit)

**Segment strategy**: How should the institution serve each segment differently?
- Mass market: Maximize digital self-service, minimize high-cost channel usage
- Mass affluent: Balanced model with digital efficiency and relationship touchpoints
- High net worth: High-touch, advisor-led with premium CTS justified by relationship revenue
- Small business: Efficient digital platform with specialist access for complex needs

**Product design**: Are products designed for efficient delivery?
- Simplify product lineup to reduce servicing complexity
- Bundle features that encourage low-cost behavior
- Design products for straight-through processing

## Output Specification

```markdown
# Cost-to-Serve Analysis: [Period]

## Executive Summary
[Key findings: overall CTS trends, segment profitability insights, optimization opportunities]

## Cost Hierarchy
[Total operating cost decomposition into direct, indirect, and unallocable]

## Activity Cost Catalog
| Activity | Total Cost | Driver | Volume | Unit Cost |
|----------|-----------|--------|--------|-----------|
| [Activity] | [$X] | [Driver] | [N] | [$X.XX] |

## Segment Cost-to-Serve
[Segment-level CTS with revenue, margin, and benchmarks]

## Cost Driver Analysis
[Key drivers of cost variation with quantified impact]

## Customer Profitability Distribution
- **Profitable customers**: [N] ([X%] of base), contributing [$XM] net margin
- **Break-even customers**: [N] ([X%] of base)
- **Unprofitable customers**: [N] ([X%] of base), absorbing [$XM] in negative margin

## Optimization Opportunities
[Prioritized list with savings estimates and feasibility]

## Strategic Recommendations
[Pricing, segmentation, product, and channel recommendations]
```

## Analysis Framework

### Customer Profitability Distribution (Pareto Analysis)

Apply the 80/20 rule to banking customer profitability:
- Typically 20-30% of customers generate 100%+ of profit
- 50-60% of customers are marginally profitable or break-even
- 10-20% of customers are unprofitable (CTS exceeds revenue)
- The top decile often subsidizes the bottom two deciles

### Channel Cost Benchmarking

Compare unit costs to industry benchmarks:

| Channel | Institution | Industry Low | Industry Median | Industry High |
|---------|-----------|-------------|-----------------|---------------|
| Branch (teller) | [$X] | $3.50 | $4.25 | $5.50 |
| Call center (live) | [$X] | $3.00 | $4.50 | $6.00 |
| ATM | [$X] | $0.50 | $0.70 | $1.00 |
| Online | [$X] | $0.10 | $0.20 | $0.35 |
| Mobile | [$X] | $0.05 | $0.12 | $0.20 |

### Cost-to-Serve Maturity Model

Assess the sophistication of the institution's CTS capability:
- **Level 1**: Aggregate cost ratios (total expenses / total customers)
- **Level 2**: Channel-level costing (cost per transaction by channel)
- **Level 3**: Activity-based costing (unit costs by activity)
- **Level 4**: Customer-level profitability (CTS at individual customer level)
- **Level 5**: Predictive CTS (forecast future CTS based on behavior models)

## Examples

**Example 1 — Segment CTS Comparison**:
"Cost-to-serve analysis reveals mass market checking accounts have an average CTS of $285/year against average revenue of $195/year, generating negative margin of -$90/customer. Primary cost drivers: 4.2 branch visits/year ($18.90 per visit = $79), 8.3 call center contacts ($4.50/contact = $37), and 2.1 overdraft-related service interactions ($12/interaction = $25). In contrast, mass affluent checking has CTS of $340/year against revenue of $890/year (+$550 margin). Strategy recommendation: for mass market, implement digital-first service model with incentives for digital adoption (fee waiver for paperless + direct deposit), projected to reduce CTS by $75/customer through channel migration. Expected ROI: $3.2M annually across 42,500 mass market accounts."

**Example 2 — Activity Cost Drill-Down**:
"Dispute resolution activity costs $187 per dispute on average. Decomposition: intake and documentation (25 minutes, $18), investigation (45 minutes, $42), provisional credit processing (10 minutes, $8), system research and documentation (35 minutes, $28), customer communication (3 touchpoints × $4.50 = $14), management review (15 minutes, $15), final resolution processing (20 minutes, $16), regulatory compliance documentation (20 minutes, $18), allocated compliance overhead ($28). Total: $187. High-cost drivers: investigation and system research require toggling between 4 systems. Recommendation: implement unified dispute management platform to reduce investigation time by 40% and system research by 50%, reducing per-dispute cost to $128 (32% reduction). At 8,400 disputes/year, annual savings: $495K."

## Guidelines

- Use activity-based costing, not simple allocation methods (headcount or balance-based pro-rata)
- Validate time allocations through time studies or time-tracking data, not manager estimates alone
- Include both direct and allocated costs, but clearly separate them in reporting
- Present cost-to-serve alongside revenue to show margin, not cost in isolation
- Account for customer lifecycle stage (new customers cost more due to onboarding)
- Distinguish between fixed costs (occupancy, infrastructure) and variable costs (per-transaction)
- Be cautious with cost allocation for shared resources; allocation method significantly affects results
- Update ABC models at least annually to reflect process and volume changes
- Cost-to-serve analysis should inform strategy, not dictate customer treatment (avoid "firing" customers)
- Consider the lifetime value of currently unprofitable customers (students, young professionals)

## Validation Checklist

- [ ] Cost hierarchy captures all material operating costs
- [ ] Activities are comprehensive and represent actual work performed
- [ ] Activity drivers reflect true consumption patterns, not proxies
- [ ] Cost-to-serve is calculated at the segment level with per-customer averages
- [ ] Revenue data is paired with cost data to show net margin
- [ ] Cost driver analysis identifies controllable vs. uncontrollable drivers
- [ ] Customer profitability distribution is analyzed (Pareto/decile analysis)
- [ ] Optimization opportunities are prioritized with estimated savings and feasibility
- [ ] Channel cost benchmarks provide external context
- [ ] Strategic recommendations connect cost insights to pricing, product, and channel decisions
