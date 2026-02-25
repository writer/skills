---
name: upsell-timing-optimizer
description: >
  Determines the optimal timing, trigger conditions, and offer structure for upsell opportunities
  across the customer lifecycle in CPG and retail e-commerce. Use when a user needs to increase
  AOV through premium upgrades, size-ups, subscription conversions, or tier migrations without
  increasing churn. Triggers on requests for upsell strategy, upgrade timing, AOV optimization,
  subscription conversion, premium migration, or size-up campaigns.

metadata:
  display_name: "Upsell Timing Optimizer"
  short_description: "Optimize upsell timing, triggers, and offer structure"
  default_prompt: "Optimize my upsell timing and suggest the best next steps"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Upsell Timing Optimizer

## Overview

This skill analyzes customer purchase patterns, engagement signals, and lifecycle stage to identify the precise moment when upsell offers have the highest conversion probability and lowest churn risk. It maps upsell paths (size-up, premium tier, subscription, frequency increase) to customer readiness signals and produces a timing-optimized upsell calendar with offer specifications and expected revenue impact.

## When to Use

- Identifying when to offer premium product upgrades to existing customers
- Optimizing subscription upgrade or conversion timing
- Determining the right moment for size-up offers (trial → full size, single → multi-pack)
- Planning loyalty tier upgrade campaigns
- Increasing AOV without increasing promotional discounting
- Designing automated upsell trigger workflows in CRM/ESP

## Required Inputs

| Input | Required | Description |
|---|---|---|
| Transaction Data | Yes | Customer-level: order dates, products, quantities, revenue, product tiers |
| Product Hierarchy | Yes | Product tiers/levels: standard vs. premium, sizes, subscription vs. one-time |
| Current AOV | Yes | Baseline AOV for impact measurement |
| Customer Lifecycle Data | Recommended | Segment, lifecycle stage, LTV, tenure, order count |
| Engagement Data | Recommended | Email engagement, site visits, app usage, loyalty status |
| Subscription Data | No | One-time vs. subscriber status, subscription frequency, skip history |
| Price Point Map | No | Price ladder across product tiers for margin analysis |
| Historical Upsell Data | No | Past upsell campaign results (conversion rates, churn impact) |

## Methodology

### Step 1 — Upsell Path Definition

Map all available upsell paths in the product portfolio:

| Upsell Type | Description | Example | Typical AOV Lift |
|---|---|---|---|
| **Size-Up** | Larger quantity or size | 8oz → 16oz, 30-count → 60-count | 30%–60% |
| **Premium Upgrade** | Higher-quality tier | Standard → organic, basic → pro | 25%–50% |
| **Bundle Up** | Single item → curated set | Individual serum → full routine | 40%–80% |
| **Frequency Increase** | More frequent delivery | Monthly → bi-weekly subscription | 50%–100% |
| **Subscription Conversion** | One-time → auto-ship | Single purchase → subscribe & save | 15%–25% (per-order discount offset by LTV) |
| **Tier Migration** | Loyalty tier upgrade | Silver → Gold membership | Indirect (drives engagement + frequency) |
| **Add-On** | Supplementary premium feature | Standard shipping → express, basic → gift wrap | 10%–20% |

### Step 2 — Customer Readiness Signal Identification

Define behavioral signals that indicate upsell receptivity:

**High-Readiness Signals** (strong upsell indicators):

| Signal | Measurement | Why It Indicates Readiness |
|---|---|---|
| Consistent reorder | 3+ consecutive on-time reorders | Habitual buyer; product-market fit established |
| High engagement | Top 25% email open + click rate | Active relationship with brand |
| Full-price buyer | <20% of orders discounted | Not price-anchored; values quality |
| Category explorer | Purchased from 2+ categories | Expanding brand relationship |
| Increasing basket | AOV trending up over last 3 orders | Naturally upgrading spending |
| Product page browsing | Viewed premium product pages | Active consideration of upgrade |
| Review leaver | Left positive review (4–5 stars) | High satisfaction; advocacy signal |
| Loyalty active | Earning and redeeming points regularly | Invested in brand ecosystem |

**Low-Readiness Signals** (defer upsell):

| Signal | Risk |
|---|---|
| Recent complaint or return | Upsell will feel tone-deaf; fix experience first |
| Declining purchase frequency | Customer is pulling away; retention focus needed |
| Promotion-dependent | Only buys on discount; upsell will fail without incentive |
| New customer (<2 orders) | Relationship not established; 2nd purchase is the priority |
| Recent price increase exposure | Price sensitivity is elevated; avoid stacking |
| Subscription skip or pause | Satisfaction concern; address before upselling |

### Step 3 — Optimal Timing Windows

Identify the highest-conversion upsell moments based on lifecycle timing:

**Lifecycle-Based Timing Matrix**:

| Customer Stage | Upsell Type | Optimal Timing | Rationale |
|---|---|---|---|
| Post-2nd purchase | Subscription conversion | Day 3–7 after order 2 | Habit forming; convenience pitch resonates |
| Post-3rd purchase | Size-up | Day 1 after order 3 | Usage pattern confirmed; volume saves money |
| 60-day tenure | Premium upgrade | Day 60–75 | Brand trust established; ready for investment |
| Post-positive review | Bundle up | Day 1–3 after review | Peak satisfaction moment; emotional high |
| Pre-reorder window | Frequency increase | 3–5 days before expected reorder | Natural decision point; "never run out" message |
| Loyalty milestone | Tier migration | On point threshold approach | Gamification; "you're almost there" motivation |
| Seasonal peak | Gift/premium bundles | 2–3 weeks pre-holiday | Gifting and self-treat mindset |
| Post-price-browsing | Premium upgrade | Within 24 hours of page view | Active consideration; strike while warm |

**Optimal Day & Time**:
- Best days for upsell emails: Tuesday, Wednesday, Thursday
- Best time: 10 AM–12 PM local time (decision-making window)
- Avoid: Mondays (inbox overload), Fridays (weekend mindset), evenings (lower conversion)
- SMS upsell: 11 AM–1 PM or 6–8 PM (higher engagement windows)

### Step 4 — Upsell Offer Structure

Design the offer to maximize conversion while protecting margin:

**Value Framing Strategies**:

| Strategy | Structure | When to Use | Example |
|---|---|---|---|
| **Per-Unit Savings** | Show cost-per-unit reduction | Size-up offers | "$0.50/bar vs. $0.65/bar — save 23%" |
| **Percentage Upgrade** | Show % more product | Size/quantity increases | "Get 50% more for just 30% more" |
| **Feature Anchoring** | Highlight premium-exclusive features | Tier upgrades | "Unlock free shipping + exclusive access" |
| **Social Proof** | Show what top customers choose | Any upsell | "80% of our regulars choose the 24-pack" |
| **Risk Reversal** | Remove downside risk | Premium/subscription | "Try premium risk-free; downgrade anytime" |
| **Calculated Savings** | Show annual savings | Subscription conversion | "Subscribe and save $72/year" |

**Discount Rules for Upsell**:
```
Upsell offers should NOT rely on deep discounts. Target structure:

  Size-up: Show per-unit savings (inherent value, no coupon needed)
  Premium: First-order-at-standard-price guarantee (risk reversal)
  Subscription: 10%–15% ongoing discount (industry standard)
  Bundle: 10%–15% vs. à la carte (perceived value, margin-protected)
  Tier: Points bonus, not price discount (preserve tier economics)

If conversion rate is <5% without discount → test 10% introductory offer
If conversion rate is 5%–15% without discount → no discount needed
If conversion rate is >15% → increase price or reduce offer
```

### Step 5 — Channel & Trigger Orchestration

Map each upsell to its optimal delivery channel and trigger:

**Automated Trigger Flows**:

```
Trigger: 3rd order delivered
  → Wait 3 days
  → Check: Is customer a full-price buyer? (yes/no)
  → YES: Send "Upgrade to Premium" email (no discount)
  → NO: Send "Try Premium at your current price" email (introductory offer)
  → Wait 5 days
  → If no conversion: SMS reminder with social proof
  → Wait 7 days  
  → If no conversion: Suppress; retry in 60 days
```

**Channel Selection by Upsell Type**:

| Upsell Type | Primary Channel | Secondary | Trigger |
|---|---|---|---|
| Subscription conversion | Email | In-cart prompt | Post 2nd or 3rd purchase |
| Size-up | On-site (cart/PDP) | Email | Cart addition of standard size |
| Premium upgrade | Email | SMS | Lifecycle milestone (order 3+, day 60+) |
| Bundle up | On-site + email | Ads (retargeting) | Category browse behavior |
| Frequency increase | Email | In-app notification | Subscription management page visit |
| Tier migration | Email + in-app | Push notification | Points milestone approach |

### Step 6 — Churn Risk Guardrails

Protect against upsell-induced churn:

**Anti-Churn Rules**:
1. **Cooling period**: No upsell within 14 days of a complaint, return, or negative feedback
2. **Frequency cap**: Maximum 1 upsell attempt per 30-day period per customer
3. **Decline respect**: If customer declines upsell 2× consecutively, suppress for 90 days
4. **Satisfaction gate**: Only upsell customers with implied satisfaction (positive review, consistent reorder, no returns)
5. **Easy downgrade**: Always communicate that downgrade/cancellation is frictionless
6. **Price sensitivity check**: If customer's last order used a discount code, defer premium upsells
7. **New customer protection**: No upsell attempts before order #2 is placed

**Monitor Post-Upsell Metrics**:
```
Post-Upsell Churn Rate = Customers who churned within 60 days of upsell ÷ Customers who accepted upsell

Healthy: <5% post-upsell churn (lower than baseline churn)
Warning: 5%–10% post-upsell churn (investigate offer/product fit)
Critical: >10% post-upsell churn (pause upsell program; diagnose)
```

### Step 7 — Revenue Impact Modeling

Project the revenue impact of the upsell program:

```
Upsell Revenue = Eligible Customers × Upsell Conversion Rate × Incremental Revenue Per Upsell

Example:
  Eligible for subscription conversion: 8,000 customers (3+ orders, non-subscribers)
  Expected conversion rate: 12%
  Incremental annual revenue per subscriber: $85 (higher frequency + retention)
  Projected revenue: 8,000 × 0.12 × $85 = $81,600/year

Total Program Impact = Σ (Revenue per upsell path) - Cannibalization - Churn Cost
```

**AOV Impact Forecast**:
```
New AOV = (Current AOV × Non-Upsell %) + (Upsell AOV × Upsell %)

Example:
  Current AOV: $42
  Upsell AOV (size-up): $62
  Upsell adoption rate: 15%
  New Blended AOV: ($42 × 0.85) + ($62 × 0.15) = $35.70 + $9.30 = $45.00
  AOV Lift: +$3.00 (+7.1%)
```

## Output Specification

1. **Upsell Path Map**: All available upsell paths with type, products, and expected AOV lift
2. **Readiness Scoring Model**: Signal-based customer readiness assessment framework
3. **Timing Calendar**: Optimal upsell moments mapped to lifecycle stage and behavior triggers
4. **Offer Specifications**: Per-path offer structure, framing, and discount rules
5. **Channel & Trigger Flows**: Automated workflow designs with decision logic
6. **Churn Guardrails**: Anti-churn rules and monitoring thresholds
7. **Revenue Impact Model**: Projected revenue by upsell path with assumptions
8. **Testing Roadmap**: A/B test plan for timing, offer, and channel optimization

## Examples

**Input**: "Optimize upsell timing for our supplement brand. We have standard and premium lines (premium is 40% more expensive). Current premium penetration is 12%. 35,000 customers."

**Output**: Readiness analysis identifies 8,200 customers as high-readiness for premium upgrade (3+ orders, full-price history, high engagement). Optimal timing: day 5 after 3rd order delivery with "Upgrade Your Routine" email. Offer: first premium order at standard price (risk reversal). Projected premium penetration: 12% → 19% over 6 months, adding $142K in annual revenue. Churn guardrails: no premium pitch to customers with returns or declining frequency.

**Input**: "We want to convert more one-time buyers to subscribers for our coffee brand. Current subscription rate is 18%. Repurchase cycle is 21 days."

**Output**: Subscription conversion timing optimized to day 3 after 2nd order (habit-forming moment). Three-variant test: (A) "Never run out" convenience framing, (B) "Save 15% every order" savings framing, (C) "Join 50,000+ subscribers" social proof framing. Channel: email with SMS follow-up at day 8 for non-converters. Projected: conversion rate 14% of eligible, moving subscription penetration from 18% to 24%. Anti-churn: easy pause/skip messaging included; monitor 60-day post-conversion churn.

## Guidelines

- Timing is the single biggest lever in upsell success — the same offer converts 3–5× better at the right moment
- Never upsell a customer who hasn't demonstrated product satisfaction first
- Frame upsells as value-adds, not sales pitches — "you've earned this" > "buy more"
- Per-unit economics framing outperforms percentage discounts for size-up offers
- Subscription conversion should always emphasize flexibility (pause, skip, cancel anytime)
- Monitor cannibalization: if premium upsells are acquired mostly by customers who would have upgraded naturally, the program has limited incrementality
- Test timing windows before offer variations — timing has 2–3× more impact than offer wording
- For CPG, consumption rate data (if available) is the most powerful timing signal
- Always pair upsell with easy downgrade path to reduce perceived risk
- VIP customers respond to exclusivity and access; avoid discounting for this segment

## Validation Checklist

- [ ] All upsell paths are identified with clear product mapping and AOV lift
- [ ] Readiness signals are defined with both positive and negative indicators
- [ ] Timing windows are specific (day ranges, trigger events) not vague
- [ ] Offer structure varies by upsell type with appropriate framing
- [ ] Channel and trigger flows include decision logic and fallback sequences
- [ ] Churn guardrails are explicit with frequency caps and cooling periods
- [ ] Revenue impact is modeled with conservative conversion assumptions
- [ ] Cannibalization risk is assessed for each upsell path
- [ ] Post-upsell churn monitoring thresholds are defined
- [ ] Testing roadmap prioritizes timing tests before offer tests
