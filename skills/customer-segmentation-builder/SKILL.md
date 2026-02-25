---
name: customer-segmentation-builder
description: >
  Builds actionable customer segments for CPG and retail e-commerce using RFM analysis,
  behavioral clustering, lifecycle staging, and value-based tiering. Use when a user needs
  to segment their customer base for targeted marketing, personalization, or strategic planning.
  Triggers on requests for customer segmentation, audience building, cohort analysis, customer
  profiling, or segment-specific marketing strategies.

metadata:
  display_name: "Customer Segmentation Builder"
  short_description: "Build customer segments using RFM and behavior data"
  default_prompt: "Optimize my customer segmentation builder and suggest the best next steps"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Customer Segmentation Builder

## Overview

This skill constructs multi-dimensional customer segments by combining transactional data (RFM), behavioral signals, lifecycle stage, and demographic attributes. It produces named, sized, and actionable segments with tailored marketing strategies, channel preferences, and expected value metrics for CPG and retail e-commerce contexts.

## When to Use

- Building or refreshing a customer segmentation model
- Identifying high-value customer cohorts for targeted campaigns
- Developing personalized marketing strategies per segment
- Analyzing customer base composition and health
- Informing product development, assortment planning, or pricing with segment insights
- Creating audience lists for paid media, email, and loyalty programs

## Required Inputs

| Input | Required | Description |
|---|---|---|
| Transaction Data | Yes | Customer-level purchase history: order date, order value, items, frequency |
| Customer Count | Yes | Total number of unique customers in the dataset |
| Time Period | Yes | Data range for analysis (minimum 12 months recommended) |
| Product Categories | Recommended | Category/subcategory taxonomy for purchase behavior analysis |
| Channel Data | Recommended | Acquisition source, purchase channel (web, app, marketplace, store) |
| Demographic Data | No | Age, gender, location, household composition |
| Engagement Data | No | Email opens/clicks, site visits, app sessions, loyalty status |
| Business Objectives | No | Specific goals (e.g., grow retention, reduce churn, increase AOV) |

## Methodology

### Step 1 — RFM Analysis Foundation

Calculate RFM scores for every customer:

**Recency (R)**: Days since last purchase
```
R Score 5: Purchased within 0–30 days
R Score 4: Purchased within 31–60 days
R Score 3: Purchased within 61–120 days
R Score 2: Purchased within 121–240 days
R Score 1: Purchased 241+ days ago
```

**Frequency (F)**: Total number of orders in the analysis period
```
F Score 5: Top 20% by order count
F Score 4: 60th–80th percentile
F Score 3: 40th–60th percentile
F Score 2: 20th–40th percentile
F Score 1: Bottom 20%
```

**Monetary (M)**: Total revenue from the customer
```
M Score 5: Top 20% by total spend
M Score 4: 60th–80th percentile
M Score 3: 40th–60th percentile
M Score 2: 20th–40th percentile
M Score 1: Bottom 20%
```

Composite RFM Score = concatenation of R, F, M (e.g., "555" = best customers).

### Step 2 — Lifecycle Stage Assignment

Map RFM scores to lifecycle stages:

| Lifecycle Stage | RFM Pattern | Description |
|---|---|---|
| **Champions** | R:5, F:4–5, M:4–5 | Best customers; buy often, spend high, recent |
| **Loyal Customers** | R:3–4, F:4–5, M:3–5 | Consistent buyers with high frequency |
| **Potential Loyalists** | R:4–5, F:2–3, M:2–3 | Recent buyers with growth potential |
| **Recent Customers** | R:5, F:1, M:1–2 | New first-time buyers |
| **Promising** | R:3–4, F:1–2, M:1–2 | Bought recently, low frequency — need nurturing |
| **Need Attention** | R:2–3, F:3–4, M:3–4 | Previously loyal, showing decline signals |
| **About to Sleep** | R:2, F:1–3, M:1–3 | Below average recency, at risk |
| **At Risk** | R:1–2, F:4–5, M:4–5 | Were high-value buyers, haven't returned |
| **Hibernating** | R:1, F:1–2, M:1–2 | Low across all dimensions, long inactive |
| **Lost** | R:1, F:1, M:1 | No activity for extended period |

### Step 3 — Behavioral Enrichment

Layer behavioral attributes onto lifecycle segments:

**Purchase Behavior Patterns**:
- **Category Loyalists**: >70% of purchases in one category
- **Cross-Category Shoppers**: Purchases across 3+ categories
- **Promotion-Sensitive**: >50% of orders include a discount code
- **Full-Price Buyers**: <20% of orders include a discount
- **Bulk Buyers**: AOV >2× average
- **Subscribe & Save**: Active subscription orders

**Channel Behavior**:
- **Digital-First**: >80% of purchases via web/app
- **Omnichannel**: Active across digital + physical (if applicable)
- **Marketplace-Dependent**: Primarily Amazon/Walmart.com purchasers
- **Social Commerce**: Purchases originating from social platforms

**Engagement Behavior**:
- **Email Engaged**: Opens >30%, clicks >5% of emails
- **App Active**: >4 app sessions/month
- **Loyalty Member**: Enrolled in loyalty/rewards program
- **Review Contributor**: Has left 1+ product reviews

### Step 4 — Value-Based Tiering

Apply value tiers using the Pareto principle:

| Tier | Definition | Typical % of Customers | Typical % of Revenue |
|---|---|---|---|
| **Platinum** | Top 5% by LTV | 5% | 25%–35% |
| **Gold** | 6th–20th percentile | 15% | 25%–30% |
| **Silver** | 21st–50th percentile | 30% | 20%–25% |
| **Bronze** | Bottom 50% | 50% | 10%–20% |

Calculate per-tier metrics:
- Average LTV, AOV, purchase frequency, and retention rate
- Contribution margin (revenue minus acquisition and servicing costs)
- Growth trajectory (tier migration rate quarter-over-quarter)

### Step 5 — Segment Profile Construction

For each segment, build a comprehensive profile:

```
Segment: [Name]
├── Size: X,XXX customers (XX% of base)
├── Revenue Share: XX% of total revenue
├── Avg LTV: $XXX | Avg AOV: $XX | Avg Frequency: X.X orders/year
├── Retention Rate: XX%
├── Top Categories: Category A (XX%), Category B (XX%)
├── Channel Mix: Web XX%, App XX%, Marketplace XX%
├── Promotion Sensitivity: Low / Medium / High
├── Preferred Engagement: Email / SMS / Push / Social
├── Lifecycle Stage: [Stage]
├── Value Tier: [Tier]
└── Key Behavioral Tags: [Tag1], [Tag2], [Tag3]
```

### Step 6 — Segment Strategy Mapping

Assign tailored strategies per segment:

| Segment | Strategic Objective | Key Tactics | KPI Target |
|---|---|---|---|
| Champions | Maximize value, advocacy | Exclusive access, referral program, VIP perks | Increase AOV 10%, referral rate 15% |
| Loyal Customers | Deepen relationship | Cross-sell, loyalty tier upgrade, early access | Cross-sell rate 20%, retention 90%+ |
| Potential Loyalists | Accelerate 2nd/3rd purchase | Welcome series, incentivized reorder, bundle offers | 2nd purchase rate 40%+ within 60 days |
| Recent Customers | Convert to repeat | Post-purchase nurture, review request, subscription offer | 30-day repeat rate 25%+ |
| Need Attention | Re-engage before churn | Win-back email, special offer, survey | Reactivation rate 15%+ |
| At Risk | Prevent high-value loss | Personal outreach, exclusive discount, feedback request | Save rate 20%+ |
| Hibernating | Selective reactivation | Low-cost reactivation (email only), suppress from paid | Reactivation rate 5%+; suppress if no response |
| Lost | Suppress or sunset | Remove from active lists; reduce acquisition cost | List hygiene, deliverability improvement |

### Step 7 — Segment Sizing & Opportunity Analysis

Quantify the business opportunity per segment:

```
Revenue Uplift Potential = Segment Size × (Target Metric - Current Metric) × AOV

Example:
  Potential Loyalists: 5,000 customers
  Current 2nd purchase rate: 25%
  Target 2nd purchase rate: 40%
  AOV: $45
  Uplift = 5,000 × (0.40 - 0.25) × $45 = $33,750 potential revenue
```

Rank segments by uplift potential to prioritize investment.

## Output Specification

1. **Segment Summary Table**: All segments with size, revenue share, key metrics, and lifecycle stage
2. **Segment Profiles**: Detailed profile cards for each segment (per Step 5 format)
3. **Strategy Matrix**: Per-segment objectives, tactics, channels, and KPI targets
4. **Value Distribution Chart**: Description of Pareto curve showing customer value concentration
5. **Opportunity Sizing**: Revenue uplift potential per segment, ranked by priority
6. **Implementation Roadmap**: Phased plan for activating segments across marketing channels
7. **Migration Tracking**: Recommended quarterly segment migration analysis framework

## Examples

**Input**: "Build customer segments for our DTC supplements brand. 45,000 customers, 18 months of transaction data, 3 product categories (vitamins, protein, wellness). We have email engagement data."

**Output**: 8 named segments with full profiles. Champions (4% of base, 28% of revenue) are subscription-heavy, multi-category buyers. Potential Loyalists (18% of base) represent $180K uplift opportunity if 2nd purchase rate increases from 22% to 38%. At Risk segment (6% of base) identified as previously high-value subscription cancellers. Strategy matrix with email sequences, loyalty tier design, and paid media suppression rules.

**Input**: "Segment our grocery e-commerce customers for a new loyalty program design. 200K customers, want to understand who should be in each loyalty tier."

**Output**: Four-tier loyalty structure mapped to value tiers with qualifying thresholds. Platinum (top 3%, $2,000+ annual spend) gets free delivery + exclusive products. Gold (next 12%, $800+ annual spend) gets accelerated points. Silver earns standard rewards. Behavioral overlay identifies "deal hunters" within each tier for differentiated offer strategies.

## Guidelines

- Use at least 12 months of data to account for seasonal purchase patterns in CPG
- Adjust RFM thresholds to the specific business — a monthly consumable has different frequency benchmarks than a durable good
- Segments must be actionable: if you can't target them in a marketing channel, they're analytical curiosities, not segments
- Aim for 6–10 segments; fewer than 5 lacks granularity, more than 12 is operationally unmanageable
- Always include segment size and revenue share — strategy without sizing is incomplete
- For subscription businesses, factor subscription status as a primary behavioral dimension
- Recommend suppression strategies for unresponsive segments to improve overall marketing efficiency
- Update segments quarterly to capture lifecycle migration and seasonal shifts

## Validation Checklist

- [ ] RFM scores are calculated with business-appropriate thresholds
- [ ] Every customer is assigned to exactly one primary segment
- [ ] Segment sizes sum to 100% of the customer base
- [ ] Revenue shares are calculated and sum to 100%
- [ ] Each segment has a distinct strategic objective and tactic set
- [ ] Opportunity sizing is quantified with clear assumptions
- [ ] High-value at-risk segments are identified and prioritized
- [ ] Segments are platform-activatable (exportable to ESP, ad platforms, CRM)
- [ ] Migration tracking framework is defined for ongoing monitoring
