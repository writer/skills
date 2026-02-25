---
name: store-vs-online-mix-optimizer
description: >
  Analyzes and optimizes the allocation of products, inventory, promotions, and marketing spend between
  in-store and online (e-commerce) channels to maximize total revenue and margin. Use when the user wants
  to optimize channel mix, understand channel-specific performance differences, resolve channel conflicts,
  or plan omnichannel assortment and pricing strategy. Triggers on requests about store vs. online,
  channel mix, omnichannel optimization, e-commerce vs. brick-and-mortar, channel allocation, or online
  vs. offline strategy.

metadata:
  display_name: "Store vs. Online Mix Optimizer"
  short_description: "Optimize product allocation between store and e-commerce"
  default_prompt: "Optimize my store vs online mix and suggest the best next steps"
  version: "1.0.0"
  tags:
    - commerce-intelligence
    - store-vs-online-mix-optimizer
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Store vs. Online Mix Optimizer

## Overview

Store vs. Online Mix Optimizer provides a data-driven framework for allocating products, inventory, promotions, and resources across physical store and e-commerce channels. As omnichannel retail has matured, the naive approach of offering everything everywhere has proven suboptimal—each channel has distinct economics (cost-to-serve, basket dynamics, consumer behavior) that demand tailored strategies.

This skill addresses the core tension in omnichannel retail: maximizing total enterprise value while respecting the structural differences between channels. E-commerce typically has higher fulfillment costs but broader assortment capability; stores have lower last-mile costs but constrained shelf space. The optimal mix is rarely 50/50—it's category-specific, geography-specific, and consumer-segment-specific.

## When to Use

- Omnichannel assortment planning: deciding which products go where
- Channel P&L analysis: understanding true profitability by channel
- Inventory allocation between e-commerce fulfillment centers and store replenishment
- Pricing strategy: whether to maintain price parity across channels or differentiate
- Promotional calendar: allocating trade spend across in-store and digital channels
- New product launch: determining optimal channel entry strategy
- User asks about online vs. store performance, channel mix, or omnichannel optimization

## Required Inputs

| Input | Required | Description |
|---|---|---|
| Sales data by channel | Yes | Revenue, units, transactions split by in-store vs. online (e-commerce, click-and-collect, delivery) |
| Product catalog | Yes | Full SKU list with attributes; channel availability flags |
| Channel cost data | Recommended | Fulfillment cost, shipping cost, return rate, marketing cost per channel |
| Margin data by channel | Recommended | Gross margin and contribution margin by channel |
| Customer data | Recommended | Customer segments, cross-channel shopping behavior, channel preferences |
| Traffic data | Recommended | Store visits, site sessions, app sessions |
| Inventory data | Optional | Inventory levels by location (store, DC, e-commerce FC) |
| Competitor channel data | Optional | Competitor online vs. in-store presence and pricing |
| Geographic data | Optional | Store trade areas, delivery zones, demographic profiles |

## Methodology

### Step 1: Channel Performance Baseline

Build a comprehensive channel P&L to understand true economics:

| Metric | In-Store | E-Commerce | Click & Collect | Marketplace |
|---|---|---|---|---|
| Gross Revenue | — | — | — | — |
| Returns & Allowances | −1–3% | −15–30% | −5–10% | −10–20% |
| Net Revenue | — | — | — | — |
| COGS | — | — | — | — |
| Gross Margin | — | — | — | — |
| Fulfillment/Delivery Cost | Low ($0.50–$2/order) | High ($5–$15/order) | Medium ($3–$7/order) | Varies |
| Marketing/Acquisition Cost | Allocated | $2–$8/order | Shared | 15–25% commission |
| Technology/Platform Cost | Low | High | Medium | Low |
| Contribution Margin | — | — | — | — |

**Key insight**: Revenue share and profit share by channel often diverge significantly. E-commerce may be 20% of revenue but only 10% of profit due to higher costs.

### Step 2: Category-Channel Fit Analysis

Not all categories perform equally across channels. Score each category on channel fit:

**In-Store Advantage Factors**:
- Sensory evaluation needed (produce, bakery, cosmetics): +20 store score
- Immediate consumption/need: +15
- Heavy/bulky relative to value (beverages, paper products): +15 (expensive to ship)
- Low price point / high shipping-to-value ratio: +10
- Impulse purchase driven: +10

**E-Commerce Advantage Factors**:
- Long-tail/niche products (specialty foods, dietary needs): +20 online score
- Research-intensive / high information need: +15
- Subscription/replenishment suitable (diapers, pet food, vitamins): +15
- Embarrassment factor (personal care, health): +10
- Heavy/bulky for consumer to carry (pet food, beverages, bulk items): +10
- Price-comparison intensive: +10

**Channel Fit Score**:
```
Channel Fit Index = (Online Score − In-Store Score + 50) / 100
```
- Index > 0.60: E-commerce-first category
- Index 0.40–0.60: True omnichannel category
- Index < 0.40: Store-first category

### Step 3: Assortment Optimization by Channel

Define channel-specific assortment strategy:

**In-Store Assortment** (constrained by shelf space):
- Focus on top-velocity SKUs (Pareto principle: top 20–30% of SKUs drive 80% of store sales)
- Must-carry KVIs (Key Value Items) for price image
- Impulse and cross-merchandising opportunities
- Private label core range

**E-Commerce Assortment** (broader, "endless aisle"):
- Full core assortment (matches store)
- Extended range: long-tail SKUs not viable in-store but viable online
- Exclusive online SKUs (larger sizes, variety packs, bundles)
- Marketplace/dropship for ultra-long-tail

**Assortment Overlap Analysis**:
```
Overlap Rate = SKUs Available in Both Channels / Total Unique SKUs × 100
```
Benchmark: 40–70% overlap is typical. 100% overlap is usually suboptimal (too many slow movers in-store; not enough online-only extension).

### Step 4: Pricing Strategy Across Channels

Evaluate and recommend pricing approach:

| Strategy | Description | When to Use | Risk |
|---|---|---|---|
| **Price Parity** | Same price online and in-store | When consumers freely cross-shop and compare | Margin compression online due to higher costs |
| **Channel-Adjusted** | Online prices reflect delivery cost | When consumers understand channel cost differences | Consumer perception of unfairness |
| **Dynamic Online** | Online prices adjust based on competitive and demand signals | When online competition is intense | In-store pricing appears static |
| **Subscription Discount** | Lower online price for recurring orders | High-replenishment categories (diapers, pet food) | Training consumers to wait for discounts |

**Price Parity Index**:
```
PPI = Average Online Price / Average In-Store Price × 100
```
- PPI 100: Full parity
- PPI 95–99: Slight online advantage (common in competitive e-commerce)
- PPI 101–105: Slight in-store advantage (covers some delivery cost)

### Step 5: Marketing and Promotion Allocation

Optimize trade spend and marketing investment across channels:

**Channel ROI Comparison**:
```
In-Store Promo ROI = Incremental In-Store Margin / In-Store Trade Spend
Online Promo ROI = Incremental Online Margin / Online Marketing Spend
```

**Allocation Framework**: Shift marginal dollars toward the channel with higher ROI until ROI equilibrium is reached.

**Channel-Specific Promotion Tactics**:

| Tactic | Best Channel | Expected ROI | Notes |
|---|---|---|---|
| Temporary price reduction | Both | Medium | Must maintain parity if both channels |
| Display/endcap | In-store only | High | No equivalent online |
| Digital coupon / promo code | Online (primarily) | High (targeted) | Can be omnichannel |
| Sponsored product/search | Online only | Varies | Critical for online visibility |
| Bundle/variety pack | Online (primarily) | Medium-High | Harder to execute in-store |
| Free shipping threshold | Online only | High | Drives basket size |
| In-store sampling | In-store only | High for trial | No online equivalent |

### Step 6: Inventory Allocation Optimization

Optimize inventory placement across store network and e-commerce fulfillment:

```
Service Level by Channel = Fill Rate × (1 − Stockout Rate)
```

**Allocation Principles**:
1. **Demand-proportional baseline**: Allocate inventory proportional to each channel's historical demand
2. **Velocity-adjusted**: High-velocity items get safety stock priority; long-tail items shift to centralized e-commerce FC
3. **Ship-from-store**: Use stores as fulfillment nodes for e-commerce orders to improve delivery speed and reduce FC costs (but account for store inventory disruption)
4. **Last-mile cost optimization**: In markets with dense store coverage, prioritize click-and-collect over home delivery

**Ship-from-Store Viability**:
```
SFS Cost = Store Pick Cost + Pack Cost + Ship Cost − (FC Pick Cost + FC Ship Cost)
```
If SFS Cost < $0 (cheaper than fulfillment center), ship-from-store is viable for the order.

### Step 7: Channel Mix Optimization Model

Build an optimization model to maximize total contribution margin:

```
Maximize: Σ (Revenue_c × Margin_c) − Σ (Cost_c)
Subject to:
  - Σ Revenue_c ≥ Total Revenue Target
  - Inventory_store + Inventory_online ≤ Total Inventory Budget
  - Marketing_store + Marketing_online ≤ Total Marketing Budget
  - Service Level_c ≥ Minimum Service Level by Channel
```

Output: Optimal revenue mix, inventory allocation, and marketing spend split.

## Output Specification

### 1. Channel Performance Dashboard

Side-by-side comparison of in-store vs. online across all KPIs, with trend lines.

### 2. Category-Channel Fit Matrix

Heatmap showing each category's Channel Fit Index with recommended primary channel.

### 3. Assortment Recommendations

| Category | In-Store SKUs | Online-Only SKUs | Both Channels | Recommended Change |
|---|---|---|---|---|
| — | — | — | — | +/− X SKUs by channel |

### 4. Pricing Recommendation

Recommended pricing strategy by category with expected revenue and margin impact.

### 5. Investment Reallocation Plan

| Resource | Current Split (Store/Online) | Recommended Split | Expected Impact |
|---|---|---|---|
| Marketing spend | — | — | — |
| Inventory investment | — | — | — |
| Promotional funds | — | — | — |

### 6. Optimized Channel Mix Summary

| Metric | Current | Optimized | Improvement |
|---|---|---|---|
| Total Revenue | — | — | +X% |
| Total Margin $ | — | — | +$Y |
| Online Share of Revenue | — | — | — |
| Overall Service Level | — | — | — |

## Analysis Framework

### Key Metrics

- **Online Revenue Share**: E-commerce revenue / total revenue (benchmark: 10–25% for omnichannel grocery, 25–50% for general merchandise)
- **Channel Contribution Margin**: Profit after all channel-specific costs (critical for true comparison)
- **Cost-to-Serve by Channel**: Total fulfillment + delivery + marketing cost per order by channel
- **Cross-Channel Shopping Rate**: % of customers who shop both channels (typically 15–35%; these are the most valuable customers)
- **Channel Cannibalization Rate**: % of online sales that would have occurred in-store absent the online option
- **Online Share of Category**: Varies dramatically — 5–10% for produce, 30–50% for pet supplies and baby
- **Return Rate by Channel**: In-store 2–5%, online 15–30% (highly category-dependent)
- **Basket Size by Channel**: Online baskets typically 1.5–3× in-store baskets in grocery
- **Delivery/Fulfillment Cost as % of Revenue**: Target < 10% for profitability; varies by channel model

### Industry Benchmarks

| Metric | Grocery | General Merchandise | Health & Beauty |
|---|---|---|---|
| Online revenue share | 10–15% | 25–40% | 15–25% |
| Online basket size | $80–$150 | $40–$80 | $35–$60 |
| In-store basket size | $35–$65 | $25–$50 | $20–$40 |
| Online return rate | 3–5% | 20–35% | 10–15% |
| Fulfillment cost / order | $8–$15 | $5–$10 | $4–$8 |
| Click-and-collect share of online | 40–60% | 30–50% | 20–40% |

## Examples

**Input**: "Our grocery business does $2.1B total, with $280M online (13.3% share). Online is growing at 18% YoY but our online contribution margin is only 2.1% vs. 6.8% in-store. Help us optimize the channel mix to improve total profitability without sacrificing growth."

**Output**:
1. **Diagnosis**: Online profitability is dragged down by three factors: (a) High delivery cost at $12.50/order (above benchmark), (b) Deep promotional discounts online to drive trial (avg 15% off vs. 8% in-store), (c) Over-assortment online — 4,200 online SKUs vs. 2,800 in-store; the extra 1,400 generate only $8M but add $1.2M in warehousing cost.
2. **Category-Channel Fit**: Produce, bakery, deli = strong in-store (Channel Fit < 0.35). Pet food, baby, household bulk = strong online (Channel Fit > 0.65). Center-store grocery = true omnichannel (0.40–0.55).
3. **Recommendations**:
   - (a) Push click-and-collect vs. delivery: shift C&C from 35% to 55% of online orders. Saves $4.20/order × 200K orders = $840K/year.
   - (b) Rationalize online-only assortment: delist 600 low-velocity online-only SKUs generating < $5/week. Saves $480K in warehousing, loses only $3.2M gross revenue (60% of which transfers to remaining SKUs).
   - (c) Align online promo depth with in-store: reducing online promo gap from 15% to 10% improves margin by $2.1M with estimated 3% online volume impact.
   - (d) Implement $35 minimum order for free delivery (currently $25). Increases avg basket by $6 and reduces unprofitable small orders.
4. **Projected Impact**: Online contribution margin improves from 2.1% to 4.4%. Total enterprise margin improves by $4.8M annually. Online growth moderates from 18% to 14% but on a healthier base.

## Guidelines

- Always analyze contribution margin by channel, not just revenue — a fast-growing unprofitable channel destroys value
- Recognize that cross-channel customers are 2–3× more valuable than single-channel customers; don't optimize one channel at the expense of the other
- Account for channel cannibalization: not all online growth is incremental; estimate what portion would have been in-store purchases
- Price parity decisions are strategic, not just economic — consumer trust and brand consistency matter
- Ship-from-store sounds appealing but has hidden costs: in-store shopper disruption, inventory accuracy requirements, and labor complexity
- Return rates differ dramatically by channel; factor return costs into channel profitability
- Don't apply one-size-fits-all: the optimal channel strategy varies by category, geography, and customer segment
- Consider the halo effect: online presence drives store traffic (and vice versa) through increased brand awareness
- Delivery economics change with density: urban markets can support delivery profitably; rural markets may not
- The fastest-growing segment is often hybrid models (click-and-collect, curbside, same-day delivery from store); optimize for these, not just "store vs. online"
- Test channel-specific strategies in pilot markets before scaling nationally

## Validation Checklist

- [ ] Channel P&L includes all relevant costs (fulfillment, delivery, returns, marketing, technology)
- [ ] Category-channel fit is assessed using both demand data and structural factors
- [ ] Cross-channel customer behavior is analyzed (not just channel-level aggregates)
- [ ] Price parity strategy is explicitly defined and justified
- [ ] Assortment recommendations differ by channel (not simply "offer everything everywhere")
- [ ] Inventory allocation considers both service level and cost-to-serve
- [ ] Marketing spend allocation is based on channel-specific ROI
- [ ] Cannibalization effects are estimated and accounted for
- [ ] Recommendations include impact on both online and in-store performance (total enterprise view)
- [ ] Implementation plan addresses operational requirements (systems, labor, process changes)
