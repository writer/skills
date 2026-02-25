---
name: cross-sell-opportunity-engine
description: >
  Identifies and prioritizes cross-sell opportunities by analyzing product affinity, purchase
  sequences, basket composition, and customer segment behavior for CPG and retail e-commerce.
  Use when a user needs to increase basket size, improve category penetration, design product
  bundles, or build recommendation strategies. Triggers on requests for cross-sell analysis,
  product affinity, bundle optimization, recommendation engine design, or category expansion.

metadata:
  display_name: "Cross Sell Opportunity Engine"
  short_description: "Identify cross-sell opportunities via product affinity"
  default_prompt: "Optimize my cross sell opportunity and suggest the best next steps"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Cross-Sell Opportunity Engine

## Overview

This skill discovers high-probability cross-sell opportunities by mining transactional data for product co-purchase patterns, sequential purchase paths, and segment-level category gaps. It produces ranked product pair recommendations, bundle designs, and channel-specific activation strategies to grow AOV and customer category penetration in CPG and retail e-commerce.

## When to Use

- Identifying which products to recommend alongside or after a purchase
- Designing product bundles or kits with data-driven composition
- Building personalized recommendation strategies for email, site, or ads
- Analyzing category penetration gaps across customer segments
- Planning cross-category marketing campaigns
- Optimizing product page "Frequently Bought Together" sections
- Increasing AOV through strategic product pairing

## Required Inputs

| Input | Required | Description |
|---|---|---|
| Transaction Data | Yes | Order-level data: customer ID, order ID, products purchased, categories, revenue |
| Product Catalog | Yes | Product names, categories, subcategories, price points, margin |
| Time Period | Yes | Analysis window (minimum 6 months; 12+ months preferred) |
| Customer Segments | Recommended | Pre-defined segments for segment-specific analysis |
| Product Margin Data | Recommended | Gross margin per product/category for profitability-weighted recommendations |
| Browse/Search Data | No | Product page views, searches, add-to-cart without purchase |
| Return Data | No | Product return rates (to avoid recommending high-return combinations) |

## Methodology

### Step 1 — Market Basket Analysis (Association Rules)

Apply association rule mining to discover product co-purchase patterns:

**Key Metrics**:

```
Support(A→B) = Transactions containing both A and B ÷ Total transactions
  Minimum threshold: 1% (for large catalogs) to 5% (for small catalogs)

Confidence(A→B) = Transactions containing both A and B ÷ Transactions containing A
  Minimum threshold: 20%
  Interpretation: "Of customers who bought A, XX% also bought B"

Lift(A→B) = Confidence(A→B) ÷ Support(B)
  Minimum threshold: 1.5
  Interpretation: >1 means A and B are bought together more than random chance
  Lift of 2.0 means customers are 2× more likely to buy B when they buy A
```

**Output: Product Affinity Matrix**:
```
Product A          | Product B          | Support | Confidence | Lift  | Avg Joint AOV
Facial Cleanser    | Moisturizer        | 12%     | 45%        | 3.2   | $58
Protein Powder     | Shaker Bottle      | 8%      | 62%        | 5.1   | $72
Coffee Beans       | Coffee Filters     | 15%     | 38%        | 2.8   | $42
Baby Formula       | Baby Wipes         | 11%     | 55%        | 3.5   | $65
```

### Step 2 — Sequential Purchase Path Analysis

Identify products commonly purchased in sequence (not same basket):

```
Sequence Analysis:
  For each customer, order products by purchase date
  Identify frequent transitions: Product A (order N) → Product B (order N+1)

Sequence Probability = P(B follows A) = Count(A→B sequences) ÷ Count(A purchases)

Time-to-Next: Median days between purchase of A and subsequent purchase of B
```

**Output: Purchase Sequence Map**:
```
Step 1 Product    | Step 2 Product     | Seq. Probability | Median Gap | Revenue Opportunity
Starter Kit       | Full-Size Product  | 42%              | 18 days    | $35/customer
Shampoo           | Conditioner        | 38%              | 25 days    | $18/customer
Face Serum        | Eye Cream          | 29%              | 35 days    | $42/customer
Dog Food          | Dog Treats         | 51%              | 12 days    | $15/customer
```

Use sequence timing to determine optimal cross-sell trigger timing in lifecycle flows.

### Step 3 — Category Penetration Gap Analysis

Analyze what percentage of customers purchase across multiple categories:

```
Category Penetration Rate = Customers who purchased in Category X ÷ Total customers

Cross-Category Rate = Customers purchasing in 2+ categories ÷ Total customers
```

**Category Penetration Matrix**:
```
                    | Bought Skincare | Bought Haircare | Bought Body | Bought Supplements
Skincare Buyers     | 100%            | 28%             | 35%         | 12%
Haircare Buyers     | 32%             | 100%            | 22%         | 8%
Body Care Buyers    | 40%             | 19%             | 100%        | 15%
Supplement Buyers   | 18%             | 9%              | 21%         | 100%
```

**Gap Opportunity Sizing**:
```
Opportunity = (Target Penetration - Current Penetration) × Segment Size × Category AOV

Example:
  Skincare buyers into Haircare: (40% target - 28% current) × 10,000 × $32 = $38,400
```

### Step 4 — Profitability-Weighted Scoring

Not all cross-sells are equally valuable. Score by incremental profit:

```
Cross-Sell Score = Lift × Confidence × Margin Contribution × (1 - Return Rate)

Where:
  Lift: From association rules (>1.5)
  Confidence: Probability of co-purchase (0–1)
  Margin Contribution: Gross margin $ of the cross-sell product
  Return Rate: Historical return rate of the product pair
```

Rank all product pairs by Cross-Sell Score to prioritize high-value, high-probability, low-risk recommendations.

### Step 5 — Segment-Specific Cross-Sell Mapping

Different segments have different cross-sell propensities:

```
Segment             | Top Cross-Sell          | Confidence | Best Channel  | Offer Needed?
New (1st order)     | Complementary accessory | 35%        | Post-purchase email | Yes (10% off)
Developing (2-3)    | Adjacent category entry  | 28%        | Personalized email  | Bundle discount
Established (4+)    | Premium/upgrade product  | 22%        | On-site reco  | No (relationship)
VIP                 | New product / exclusive  | 40%        | Early access email  | No (access)
Price-Sensitive      | Value bundle             | 45%        | Promotion email     | Yes (bundle %)
```

### Step 6 — Bundle Design & Optimization

Create data-driven bundles from cross-sell analysis:

**Bundle Types**:

| Type | Logic | Example | Discount Strategy |
|---|---|---|---|
| **Complementary** | High-lift product pairs | Cleanser + Moisturizer | 10%–15% vs. separate |
| **Starter Kit** | Entry products for new customers | 3 best-sellers mini sizes | 20%–25% value |
| **Replenishment** | Regular-use items at volume | 3-pack protein bars | 10% + free shipping |
| **Discovery** | Low-penetration categories | "Try our haircare" sample set | 30%+ value (trial size) |
| **Gift Set** | Seasonal/gifting occasions | Holiday collection | Premium packaging, 10% |
| **Subscribe & Save** | Recurring need items | Monthly essentials box | 15% ongoing discount |

**Bundle Pricing Framework**:
```
Bundle Price = Σ(Individual Prices) × (1 - Bundle Discount %)

Target Bundle Margin = Individual Product Margin - (Bundle Discount × Revenue) 
  Ensure bundle margin remains >40% of individual margin

Cannibalization Check: Will the bundle reduce full-price individual sales?
  - If >30% of bundle buyers would have bought items separately → flag risk
  - Mitigate: limit bundle availability, make it new-customer exclusive
```

### Step 7 — Activation Strategy

Deploy cross-sell recommendations across channels:

**On-Site**:
- Product page: "Frequently Bought Together" (top 3 by lift)
- Cart page: "Complete Your Routine" (complementary items not in cart)
- Post-purchase page: "Customers Also Bought" (sequential purchase products)
- Search results: Boost cross-sell products when primary product is queried

**Email**:
- Post-purchase (Day 2): "Pair it with..." recommendation (top affinity product)
- Replenishment (pre-cycle): "Add to your reorder" with cross-sell suggestion
- Monthly digest: Personalized "recommended for you" based on purchase history
- Category introduction: "Discover our [new category]" for low-penetration segments

**Paid Media**:
- Dynamic product ads: Cross-sell catalog to past purchasers of complement products
- Retargeting: Show cross-sell products to recent single-category buyers
- Lookalike audiences built from multi-category buyers (highest LTV proxy)

**In-App / SMS**:
- Push notification: "Your [product] pairs perfectly with [cross-sell]" 
- SMS: Flash cross-sell offers for time-sensitive bundles

## Output Specification

1. **Product Affinity Matrix**: Top 20+ product pairs ranked by cross-sell score
2. **Sequential Purchase Map**: Top purchase paths with timing and probability
3. **Category Penetration Analysis**: Cross-category rates with gap opportunities sized in revenue
4. **Segment Cross-Sell Recommendations**: Per-segment top cross-sell products and channels
5. **Bundle Recommendations**: 3–5 bundle designs with pricing, margin analysis, and use case
6. **Activation Playbook**: Channel-specific deployment plan for top cross-sell opportunities
7. **Revenue Opportunity Summary**: Total addressable cross-sell revenue by priority tier

## Examples

**Input**: "Analyze cross-sell opportunities for our natural skincare brand. 5 product categories (cleanser, serum, moisturizer, SPF, eye cream), 20,000 customers, 12 months of data."

**Output**: Affinity matrix reveals cleanser→moisturizer (lift 3.8, confidence 52%) and serum→eye cream (lift 2.9, confidence 31%) as top pairs. Category penetration shows only 18% of cleanser buyers have tried SPF — $95K revenue gap. Recommended "Complete Your Routine" bundle (cleanser + serum + moisturizer) at 15% off, projected 12% attachment rate. Sequential analysis: SPF is purchased on average 45 days after first skincare purchase — trigger email at day 30 post-first-order.

**Input**: "We sell pet food and accessories. How do we increase basket size? Current AOV is $38, goal is $48."

**Output**: Top cross-sell: dog food → treats (lift 4.2), cat food → litter (lift 3.1), any food → toy/accessory (lift 1.8). Bundle design: "Monthly Essentials" (food + treats + dental chew) at 12% discount, projected AOV $52. Activation: add "Complete Your Pet's Order" module to cart page, post-purchase email with treat recommendation at day 5. Estimated AOV lift: $38 → $47 through on-site cross-sell (70% of impact) and email (30%).

## Guidelines

- Minimum support threshold of 1% — product pairs below this lack statistical reliability
- Always check lift, not just confidence — high confidence on a popular product may have low lift
- Exclude product pairs with high combined return rates (>15%) from recommendations
- Account for cannibalization: bundles shouldn't just discount what customers would buy anyway
- Segment-specific recommendations outperform one-size-fits-all by 2–3× in conversion rate
- For CPG consumables, sequence timing is critical — recommend before the customer needs to reorder
- Test bundle pricing sensitivity: some customers prefer "save $X" framing over "X% off"
- On-site recommendations should be limited to 3–4 products to avoid decision paralysis
- Track cross-sell attribution carefully: distinguish incremental purchases from planned multi-item orders
- Refresh affinity analysis quarterly as product catalog and customer behavior evolve

## Validation Checklist

- [ ] Association rules meet minimum support (>1%), confidence (>20%), and lift (>1.5) thresholds
- [ ] Cross-sell score incorporates both probability and profitability
- [ ] Sequential purchase timing is analyzed with median gap days
- [ ] Category penetration gaps are sized in revenue opportunity
- [ ] Bundle designs include margin analysis and cannibalization assessment
- [ ] Recommendations are segment-specific, not generic
- [ ] Activation strategy covers on-site, email, and paid channels
- [ ] High-return product combinations are excluded or flagged
- [ ] Revenue opportunity is quantified with clear assumptions
- [ ] Refresh cadence for affinity analysis is established
