---
name: retention-playbook-generator
description: >
  Generates comprehensive, lifecycle-stage-specific retention playbooks for CPG and retail
  e-commerce brands. Use when a user needs to design retention programs, build automated
  lifecycle marketing workflows, or improve repeat purchase rates and customer loyalty.
  Triggers on requests for retention strategy, lifecycle marketing, repeat purchase optimization,
  loyalty program design, or customer engagement playbooks.

metadata:
  display_name: "Retention Playbook Generator"
  short_description: "Build lifecycle retention playbooks for retail brands"
  default_prompt: "Optimize my lifecycle retention playbooks for retail brands and suggest the best next steps"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Retention Playbook Generator

## Overview

This skill produces an end-to-end retention playbook covering every stage of the post-acquisition customer lifecycle — from first purchase through advocacy. It specifies exact trigger conditions, communication sequences, channel strategies, offer structures, and success metrics for each lifecycle stage, calibrated to CPG and retail e-commerce purchase dynamics.

## When to Use

- Designing or overhauling a retention marketing program
- Building automated lifecycle email/SMS/push workflows
- Improving repeat purchase rate, customer retention, or LTV
- Launching or optimizing a loyalty or rewards program
- Creating win-back and reactivation campaigns
- Establishing retention KPIs and measurement frameworks

## Required Inputs

| Input | Required | Description |
|---|---|---|
| Product Category | Yes | CPG subcategory (food, beauty, supplements, household, etc.) |
| Average Repurchase Cycle | Yes | Typical time between repeat purchases (days) |
| Current Retention Metrics | Yes | Repeat purchase rate, retention rate, churn rate (if known) |
| Channels Available | Yes | Email, SMS, push notification, direct mail, in-app, loyalty program |
| AOV | Recommended | Average order value for offer calibration |
| Customer Base Size | Recommended | For volume estimates and cost projections |
| Current Lifecycle Flows | No | Existing automated sequences to audit and improve |
| Loyalty Program Details | No | Current program structure, tiers, rewards |
| Tech Stack | No | ESP, CRM, CDP, e-commerce platform for implementation guidance |

## Methodology

### Step 1 — Lifecycle Stage Definition

Define the customer lifecycle stages with transition criteria:

```
New Customer → Developing → Established → VIP → Champion
       ↓            ↓            ↓         ↓
    Lapsed      At Risk      Declining   Dormant → Lost
```

| Stage | Definition | Transition Trigger |
|---|---|---|
| **New** | First purchase, 0–30 days | Order #1 placed |
| **Developing** | 2nd purchase made, building habit | Order #2 within 2× repurchase cycle |
| **Established** | 3+ purchases, consistent buyer | Order #3+ with regular cadence |
| **VIP** | Top 10% by LTV or frequency | Crosses LTV/frequency threshold |
| **Champion** | VIP + advocacy behavior | Referrals, reviews, UGC, social mentions |
| **At Risk** | Purchase gap exceeding 1.5× cycle | Recency gap > 1.5× expected interval |
| **Lapsed** | No purchase for 2× cycle | Recency gap > 2× expected interval |
| **Dormant** | No purchase for 3× cycle | Recency gap > 3× expected interval |
| **Lost** | No purchase for 4× cycle + no engagement | Unresponsive to all reactivation attempts |

### Step 2 — Stage-Specific Playbook Construction

#### Stage: New Customer (First 30 Days)

**Objective**: Drive 2nd purchase; build brand relationship

**Flow: Post-Purchase Welcome Series**

| Touchpoint | Timing | Channel | Content | Goal |
|---|---|---|---|---|
| Order Confirmation | Immediate | Email | Order details + brand story intro | Set expectations |
| Shipping Notification | On ship | Email/SMS | Tracking + excitement builder | Anticipation |
| Delivery Follow-Up | Day 2 post-delivery | Email | Usage tips, how-to content | Product success |
| Review Request | Day 7 post-delivery | Email | Star rating + review prompt | Social proof |
| Education Content | Day 10 | Email | Brand values, ingredient story, behind-the-scenes | Emotional connection |
| Reorder Nudge | Day 14–21 (pre-repurchase cycle) | Email + SMS | "Running low?" + easy reorder | 2nd purchase |
| Subscription Pitch | Day 21 | Email | Subscribe & save value prop | Subscription conversion |
| Incentivized Reorder | Day 28 (if no 2nd order) | Email + SMS | 10% off 2nd order | Urgency |

**KPI Targets**:
- 2nd purchase rate within 60 days: 30%–40% (consumable CPG), 15%–25% (semi-durable)
- Welcome series email open rate: 50%+
- Subscription conversion (if applicable): 10%–15% of new customers

#### Stage: Developing Customer (Orders 2–3)

**Objective**: Build purchase habit; expand basket

**Flow: Habit-Building Series**

| Touchpoint | Timing | Channel | Content | Goal |
|---|---|---|---|---|
| Thank You + Cross-Sell | Day 1 post 2nd order | Email | Thank you + complementary product recommendation | Basket expansion |
| Loyalty Enrollment | Day 3 post 2nd order | Email + in-app | Loyalty program invitation with bonus points | Program enrollment |
| Category Education | Day 10 | Email | "Customers also love..." content + social proof | Cross-category awareness |
| Reorder Reminder | Pre-repurchase cycle | Email + SMS | Personalized reorder based on purchase history | 3rd purchase |
| Bundle Offer | If 3rd order delayed | Email | Curated bundle at 10%–15% discount | Conversion + AOV growth |

**KPI Targets**:
- 3rd purchase rate: 55%–65% of those who made 2nd purchase
- Cross-sell acceptance: 15%–20%
- Loyalty enrollment: 40%–50% of 2nd-time buyers

#### Stage: Established Customer (3+ Orders)

**Objective**: Maintain cadence; increase AOV and share of wallet

**Flow: Relationship Deepening**

| Touchpoint | Frequency | Channel | Content | Goal |
|---|---|---|---|---|
| Personalized Recommendations | Monthly | Email | ML-driven product suggestions based on purchase history | Cross-sell, AOV |
| New Product Announcements | On launch | Email + push | First-to-know access for new products | Engagement, AOV |
| Loyalty Status Update | Monthly | Email + in-app | Points balance, tier progress, rewards available | Loyalty engagement |
| Replenishment Reminders | Cycle-based | SMS + push | Smart reorder based on estimated consumption rate | Repeat purchase |
| Seasonal Campaigns | Quarterly | Email | Seasonal product bundles, gift sets | AOV, category expansion |
| Feedback & Co-Creation | Quarterly | Email + survey | Product preferences, new flavor/scent votes | Emotional investment |

**KPI Targets**:
- Annual retention rate: 70%–80%
- AOV growth: 5%–10% YoY
- Category penetration: expand from avg 1.5 to 2.5 categories

#### Stage: VIP Customer (Top 10%)

**Objective**: Maximize lifetime value; cultivate advocacy

**Flow: VIP Experience**

| Touchpoint | Frequency | Channel | Content |
|---|---|---|---|
| VIP Welcome | On qualification | Email + direct mail | VIP kit: handwritten note, exclusive samples, tier benefits |
| Early Access | On product launch | Email + SMS | 48-hour exclusive early access to new products |
| Birthday/Anniversary | Annual | Email + SMS + gift | Free product gift + personalized message |
| Exclusive Events | Quarterly | Email | Virtual or IRL brand experiences, tastings, workshops |
| Concierge Service | Always-on | Dedicated support | Priority support, personal recommendations |
| Referral Program | Ongoing | Email + in-app | Enhanced referral rewards (give $15, get $15) |

**KPI Targets**:
- VIP retention rate: 85%–95%
- VIP referral rate: 15%–25%
- VIP AOV premium vs. average: 2×–3×

#### Stage: At Risk → Lapsed → Dormant

**Objective**: Prevent churn and reactivate

**Flow: Win-Back Ladder**

| Stage | Timing | Touchpoint | Offer | Channel |
|---|---|---|---|---|
| At Risk | 1.5× cycle | "We noticed you've been away" | Personalized recommendation (no discount) | Email |
| At Risk | 1.75× cycle | Soft incentive | Free shipping on next order | Email + SMS |
| Lapsed | 2× cycle | Win-back offer | 15% off + free shipping | Email + SMS |
| Lapsed | 2.5× cycle | Escalated offer | 20% off + bonus loyalty points | Email + SMS + push |
| Dormant | 3× cycle | Final attempt | 25% off or free product | Email + direct mail |
| Dormant | 3.5× cycle | Feedback request | "Help us improve" survey (no hard sell) | Email |
| Lost | 4× cycle | Sunset | Suppress from active campaigns; archive | System |

**KPI Targets**:
- At-risk save rate: 25%–35%
- Lapsed win-back rate: 10%–18%
- Dormant reactivation rate: 3%–8%

### Step 3 — Channel Strategy

Define channel orchestration rules:

**Email**: Primary lifecycle channel; used for all stages
- Frequency cap: 3–4 emails/week maximum
- Personalization: product history, name, preferences, browse behavior
- Best send times: Tuesday–Thursday, 9–11 AM and 7–9 PM local time

**SMS**: High-urgency, high-value moments
- Frequency cap: 4–6 SMS/month maximum
- Use for: reorder reminders, flash sales, shipping updates, win-back offers
- Always include opt-out; comply with TCPA
- Expected CTR: 15%–25% (significantly higher than email)

**Push Notifications**: Engagement and real-time triggers
- Use for: price drops on browsed items, back-in-stock, loyalty milestones
- Frequency cap: 1–2/day maximum
- Personalize with product imagery

**Direct Mail**: High-value moments and premium customers
- Use for: VIP welcome kits, dormant win-back (final attempt), holiday catalogs
- Cost: $2–$5/piece; reserve for LTV > $200 customers
- Expected response rate: 2%–5% (higher than digital for lapsed audiences)

### Step 4 — Offer Architecture

Structure offers to protect margin while driving action:

**Offer Hierarchy** (escalate only as needed):
1. Value-add (no margin impact): Free content, exclusive access, early launch
2. Shipping incentive: Free or expedited shipping ($5–$8 cost)
3. Points bonus: 2× or 3× loyalty points (deferred cost)
4. Percentage discount: 10% → 15% → 20% (escalating ladder)
5. Dollar-off: $10 off $50+ (protects AOV with minimum)
6. Free gift: GWP with purchase (inventory cost, perceived high value)
7. Bundle discount: 15% off curated bundle (AOV protective)

**Rules**:
- Never lead with maximum discount; always start with value-add
- Cap escalation at 25% off; beyond that, the customer is discount-dependent
- Track discount depth per customer; flag those requiring >15% to convert
- Exclude full-price loyal customers from discount flows (they don't need them)

### Step 5 — Measurement Framework

**Primary Retention KPIs**:

| Metric | Calculation | CPG Benchmark |
|---|---|---|
| 30-day repeat rate | Customers with 2+ orders in 30 days ÷ total customers | 15%–25% |
| 90-day repeat rate | Customers with 2+ orders in 90 days ÷ total | 25%–40% |
| Annual retention rate | Customers purchasing in Year 2 ÷ Year 1 customers | 30%–50% |
| Revenue retention rate | Revenue from retained customers ÷ prior year revenue | 80%–120% (net) |
| Cohort LTV curve | Cumulative revenue per customer by acquisition cohort | Category-dependent |

**Flow-Level KPIs**:
- Open rate, click rate, conversion rate per touchpoint
- Revenue attributed to each lifecycle flow
- Unsubscribe rate per flow (flag if >0.5% per send)
- Time-to-next-purchase after each flow trigger

## Output Specification

1. **Lifecycle Stage Map**: Visual stage definitions with transition criteria
2. **Stage Playbooks**: For each stage — trigger, flow, touchpoints, content, offers, channels, timing
3. **Channel Strategy**: Frequency caps, best practices, orchestration rules
4. **Offer Architecture**: Escalation ladder with margin impact estimates
5. **KPI Dashboard**: Retention metrics with benchmarks and targets
6. **Implementation Roadmap**: Phased rollout plan with priority ranking
7. **Tech Requirements**: ESP/CRM flow configurations, data triggers, integration needs

## Examples

**Input**: "Build a retention playbook for our DTC protein bar brand. Repurchase cycle is 21 days. Current repeat rate is 22% (goal: 35%). We use Klaviyo for email and Attentive for SMS."

**Output**: Complete 7-stage playbook with Klaviyo flow specifications. Post-purchase sequence with day 0–28 touchpoints driving 2nd purchase. Subscription push at day 14 with "never run out" messaging. Win-back ladder starting at day 42. Implementation roadmap: Phase 1 (weeks 1–2) — post-purchase welcome, Phase 2 (weeks 3–4) — reorder reminders, Phase 3 (weeks 5–6) — win-back flows. Projected repeat rate improvement from 22% to 32% within 90 days based on benchmarks.

**Input**: "Our skincare brand has high first-purchase-to-second drop-off (70% churn before order 2). Design a retention program focused on the first 60 days."

**Output**: Intensive first-60-day playbook with 12-touch post-purchase sequence. Day 1: order confirmation with routine-builder content. Day 3: ingredient education video. Day 7: "How's your skin feeling?" check-in with usage tips. Day 14: review request + before/after gallery. Day 21: personalized routine expansion recommendation. Day 30: subscribe & save with 15% off. Day 45: "Results take time" reassurance content. Day 60: reorder nudge with 10% off if no 2nd purchase. Projected: reduce 60-day churn from 70% to 55%.

## Guidelines

- The post-purchase-to-second-purchase window is the most critical retention moment; invest disproportionately here
- Different product categories require different timing — don't apply a one-size-fits-all cadence
- Always segment VIPs out of discount flows; they devalue the brand relationship for your best customers
- SMS is powerful but consent-dependent; never assume SMS opt-in
- Measure incrementality of retention programs, not just attributed revenue
- For subscription brands, retention playbook should include pause/skip optimization (not just cancel prevention)
- Direct mail has a resurgence in DTC — use it selectively for high-value moments
- Avoid over-communicating; respect frequency caps aggressively — unsubscribes are irreversible
- Test one variable at a time in lifecycle flows; multi-variable changes make attribution impossible

## Validation Checklist

- [ ] All lifecycle stages are defined with clear transition criteria
- [ ] Each stage has a specified trigger, flow, and touchpoint sequence
- [ ] Channel selection is appropriate for each touchpoint with frequency caps
- [ ] Offer architecture escalates gradually and protects margin
- [ ] KPI targets are set per stage with realistic benchmarks
- [ ] Post-purchase to 2nd purchase flow is comprehensive (minimum 6 touchpoints)
- [ ] Win-back ladder includes at least 4 escalation steps before sunset
- [ ] VIP program includes non-monetary value (access, experience, recognition)
- [ ] Implementation is phased with clear priority ordering
- [ ] Measurement plan includes incrementality testing approach
