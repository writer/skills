---
name: churn-risk-detection
description: >
  Detects and scores customer churn risk for CPG and retail e-commerce brands using behavioral
  signals, purchase pattern analysis, and engagement decay metrics. Use when a user needs to
  identify at-risk customers, build churn prediction models, or design proactive retention
  interventions. Triggers on requests about churn analysis, customer attrition, retention risk,
  lapsed customer identification, or win-back targeting.

metadata:
  display_name: "Churn Risk Detection"
  short_description: "Score and predict customer churn risk for retail brands"
  default_prompt: "Review my churn risk and highlight top risks and next actions"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Churn Risk Detection

## Overview

This skill identifies customers exhibiting churn signals by analyzing purchase recency decay, frequency decline, engagement drop-off, and behavioral anomalies. It produces a risk-scored customer list with churn probability estimates, time-to-churn predictions, revenue-at-risk quantification, and prescribed intervention strategies. Designed for non-contractual CPG and retail contexts where churn is silent (customers simply stop buying).

## When to Use

- Proactively identifying customers likely to churn before they lapse
- Building retention trigger campaigns based on behavioral signals
- Quantifying revenue at risk from customer attrition
- Evaluating the health of a customer base over time
- Designing and prioritizing win-back campaigns
- Setting up automated churn prevention workflows in CRM/ESP

## Required Inputs

| Input | Required | Description |
|---|---|---|
| Transaction Data | Yes | Customer-level purchase history with dates, amounts, and order counts |
| Customer IDs | Yes | Unique identifiers for each customer |
| Analysis Date | Yes | Current date or reference date for recency calculations |
| Category Purchase Cycle | Recommended | Expected repurchase interval for product category (e.g., 30 days for coffee) |
| Engagement Data | Recommended | Email opens/clicks, site visits, app sessions over time |
| Subscription Status | No | Active, paused, cancelled subscription status (if applicable) |
| Customer Service Data | No | Support tickets, complaints, returns, refund history |
| Acquisition Channel | No | How the customer was acquired (organic, paid, referral, etc.) |

## Methodology

### Step 1 — Define Churn for the Business

In non-contractual settings, churn must be operationally defined:

**Category-Based Churn Definition**:
```
Churn Threshold = Expected Repurchase Cycle × Churn Multiplier

Recommended Multipliers:
  Consumables (coffee, supplements, cleaning): 2.0× → e.g., 30-day cycle → churn at 60 days
  Semi-durable (skincare, personal care): 2.5× → e.g., 60-day cycle → churn at 150 days
  Durable (cookware, appliances): 3.0× → e.g., 180-day cycle → churn at 540 days
  Grocery basket: 1.5× → e.g., 14-day cycle → churn at 21 days
```

If category cycle is unknown, calculate from data:
```
Median Inter-Purchase Interval (IPI) = Median of (Order Date N+1 - Order Date N) across all customers

Churn Threshold = Median IPI × 2.0 (or use 75th percentile IPI × 1.5)
```

### Step 2 — Behavioral Signal Extraction

Extract churn signals across multiple dimensions:

**Purchase Behavior Signals**:

| Signal | Calculation | Churn Indicator |
|---|---|---|
| Recency Gap | Days since last purchase ÷ Avg IPI | Ratio >1.5 indicates concern; >2.0 critical |
| Frequency Decline | Orders in last 90d vs. prior 90d | >30% decline is a strong churn signal |
| AOV Decline | AOV last 3 orders vs. lifetime AOV | >20% decline indicates reduced commitment |
| Basket Shrinkage | Items per order trending down | Reducing engagement with product range |
| Category Narrowing | # categories last 3 orders vs. historical | Down-trading to fewer categories |
| Promotion Dependency | % of recent orders with discount code | Increasing to >80% signals price-only loyalty |

**Engagement Signals**:

| Signal | Calculation | Churn Indicator |
|---|---|---|
| Email Open Decay | 30-day open rate vs. 90-day average | >40% decline |
| Click-through Decline | 30-day CTR vs. 90-day average | >50% decline |
| Site Visit Frequency | Sessions last 30d vs. prior 30d | >50% decline |
| App Uninstall | App removed or sessions dropped to zero | Strong churn signal |
| Loyalty Inactivity | Points earned last 60d = 0 (for loyalty members) | Disengagement signal |

**Service Signals**:

| Signal | Churn Indicator |
|---|---|
| Recent complaint (unresolved) | 2× churn risk elevation |
| Multiple returns (3+ in 90 days) | 3× churn risk elevation |
| Negative review or rating | 1.5× churn risk elevation |
| Subscription downgrade or pause | Immediate intervention needed |
| Delivery failure or late shipment | 1.5× churn risk elevation (compounding) |

### Step 3 — Churn Risk Scoring Model

Build a composite churn risk score (0–100):

**Weighted Signal Model**:
```
Churn Risk Score = 
    (Recency Gap Score × 0.30) +
    (Frequency Decline Score × 0.25) +
    (Engagement Decay Score × 0.20) +
    (AOV/Basket Decline Score × 0.10) +
    (Service Issue Score × 0.10) +
    (Promotion Dependency Score × 0.05)

Each component scored 0–100:
  Recency Gap Score = min(100, (Days Since Purchase ÷ Churn Threshold) × 100)
  Frequency Decline Score = min(100, max(0, (1 - Recent Freq ÷ Historical Freq) × 100))
  ...etc.
```

**Risk Tier Classification**:

| Tier | Score Range | Estimated Churn Probability | Urgency |
|---|---|---|---|
| Low Risk | 0–25 | <10% | Monitor quarterly |
| Moderate Risk | 26–50 | 10%–30% | Monitor monthly; soft engagement |
| High Risk | 51–75 | 30%–60% | Active intervention within 2 weeks |
| Critical Risk | 76–100 | >60% | Immediate intervention; likely churning now |

### Step 4 — Revenue-at-Risk Quantification

Calculate the financial impact of potential churn:

```
Revenue at Risk (per customer) = Predicted Annual Revenue × Churn Probability

Where Predicted Annual Revenue = Historical AOV × Historical Annual Frequency

Aggregate Revenue at Risk = Σ (Revenue at Risk per customer) for all customers with score >50
```

**Segment-Level Risk Summary**:
```
Segment        | Customers at Risk | Avg Churn Score | Revenue at Risk | % of Total Revenue
Champions      | XX                | XX              | $XX,XXX         | X%
Loyal          | XXX               | XX              | $XXX,XXX        | XX%
At Risk        | X,XXX             | XX              | $XXX,XXX        | XX%
Total          | X,XXX             | --              | $X,XXX,XXX      | XX%
```

### Step 5 — Churn Driver Analysis

Identify the primary churn drivers in the customer base:

1. **Recency-driven churn**: Customers simply haven't returned — no engagement decline, just inactivity
2. **Experience-driven churn**: Customers had negative experiences (returns, complaints, delivery issues)
3. **Value-driven churn**: Customers only buy on promotion; churn when discounts stop
4. **Competition-driven churn**: Cross-shopping signals (declining share of wallet)
5. **Lifecycle-driven churn**: Natural category exit (e.g., baby products as children age out)
6. **Subscription fatigue**: Active subscription cancellations or skip frequency increasing

Map each at-risk customer to their primary churn driver for targeted intervention.

### Step 6 — Intervention Prescription

Prescribe actions based on risk tier and churn driver:

| Risk Tier | Driver | Intervention | Channel | Timing |
|---|---|---|---|---|
| High | Recency | "We miss you" + incentive | Email + SMS | Day 1 of high-risk classification |
| High | Experience | Service recovery outreach | Personal email or phone | Within 48 hours |
| High | Value | Exclusive loyalty offer (not discount) | Email | Day 3 |
| Critical | Recency | Escalated offer + free shipping | SMS + push | Immediate |
| Critical | Subscription | Pause option + downsell offer | Email + in-app | Pre-cancellation trigger |
| Moderate | Recency | Content re-engagement (new products, tips) | Email | Weekly cadence |
| Moderate | Value | Bundle offer or subscribe-and-save pitch | Email | Next promotional window |

**Incentive Ladder** (escalating offers for non-responsive at-risk customers):
```
Day 0: Personalized product recommendation (no incentive)
Day 7: 10% off next order
Day 14: 15% off + free shipping
Day 21: 20% off + free gift with purchase
Day 30: Final win-back: 25% off "last chance" offer
Day 45: Move to suppression list; reduce marketing spend
```

### Step 7 — Monitoring & Alert System Design

Define ongoing churn monitoring:

- **Daily scan**: Flag newly critical-risk customers for immediate action
- **Weekly digest**: Summary of risk tier migration (how many moved from moderate to high?)
- **Monthly review**: Churn rate trend, intervention effectiveness, revenue-at-risk dashboard
- **Quarterly recalibration**: Adjust scoring weights based on observed churn vs. predicted churn

**Alert Triggers**:
- Customer crosses from moderate to high risk → trigger retention workflow
- High-value customer (top 10% LTV) enters high risk → alert customer success team
- Churn rate exceeds baseline by >20% → flag systemic issue for investigation
- Subscription cancellation initiated → trigger save flow

## Output Specification

1. **Churn Risk Scorecard**: Every customer scored with risk tier, probability, and primary driver
2. **Revenue-at-Risk Summary**: Aggregate and segment-level revenue exposure
3. **Top 50 At-Risk Customers**: Prioritized list of highest-value customers at greatest risk
4. **Churn Driver Distribution**: Breakdown of primary churn causes across the at-risk population
5. **Intervention Playbook**: Per-tier, per-driver recommended actions with channel and timing
6. **Monitoring Dashboard Spec**: Metrics, thresholds, and alert rules for ongoing churn tracking

## Examples

**Input**: "Identify churn risk for our pet food DTC brand. 25,000 customers, average repurchase cycle is 28 days. We've noticed a spike in subscription cancellations."

**Output**: 3,200 customers (13%) classified as high or critical risk, representing $420K in annual revenue at risk. Subscription cancellers (800 customers) are the highest-risk cohort; primary driver is subscription fatigue (average tenure 8 months). Recommendation: introduce "pause" option, flexible delivery frequency, and surprise-and-delight program at month 6. Non-subscription at-risk customers show recency-driven patterns; prescribe a 4-step incentive ladder.

**Input**: "Our beauty brand has 60% first-year churn. Help us understand why and who's most at risk."

**Output**: Churn analysis reveals 42% of first-year churn happens before the 2nd purchase (within 60 days). Primary driver: post-purchase disengagement (no email engagement after order confirmation). High-risk new customers identified by: no email open within 14 days, no site revisit within 30 days, and single-SKU first order. Intervention: redesigned post-purchase nurture sequence with education content, usage tips, and day-45 reorder incentive.

## Guidelines

- Non-contractual churn (CPG/retail) requires probabilistic estimation — there is no single "churn event"
- Always define churn threshold relative to category purchase cycle, not arbitrary time periods
- Combine behavioral signals; no single metric reliably predicts churn alone
- High-value customers warrant more aggressive (and more expensive) retention interventions
- For low-value, high-churn segments, it may be more efficient to let them churn than to invest in retention
- Distinguish between addressable churn (can be prevented) and structural churn (lifecycle exit)
- Track intervention effectiveness: what % of high-risk customers were retained after intervention?
- Avoid "discount addiction" — escalate non-monetary value (exclusive access, content, community) before discounts
- For subscription businesses, monitor skip rate and frequency changes as early warning signals

## Validation Checklist

- [ ] Churn is operationally defined with category-appropriate thresholds
- [ ] Multiple behavioral signals are combined (not relying on recency alone)
- [ ] Risk scores are calibrated against observed churn rates
- [ ] Revenue at risk is quantified at customer and segment level
- [ ] Churn drivers are identified and mapped to specific interventions
- [ ] High-value at-risk customers are prioritized for immediate action
- [ ] Intervention playbook includes escalation ladder and channel recommendations
- [ ] Monitoring system includes automated alert triggers
- [ ] False positive rate is assessed (customers flagged but didn't actually churn)
