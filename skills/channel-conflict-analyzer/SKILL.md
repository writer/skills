---
name: channel-conflict-analyzer
description: Identify and quantify channel cannibalization, pricing conflicts, and distribution overlap across CPG sales channels. Use when analyzing cross-channel interference, DTC vs retail conflict, marketplace pricing violations, or when optimizing channel strategy to minimize value destruction.

metadata:
  display_name: "Channel Conflict Analyzer"
  short_description: "Detect cross-channel pricing and distribution conflicts"
  default_prompt: "Analyze my channel conflict and recommend clear next actions"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Channel Conflict Analyzer

## Overview

Systematically identify, quantify, and resolve channel conflicts that erode CPG brand value, margin, and retailer relationships. This skill analyzes pricing inconsistencies, distribution overlap, promotional interference, and cannibalization patterns across all active channels — providing actionable resolution strategies that balance growth with channel harmony.

## When to Use

- Cross-channel pricing discrepancy investigations
- DTC vs retail channel conflict assessment
- Amazon/marketplace pricing compliance reviews
- New channel launch impact assessment (e.g., adding Dollar channel)
- Retailer complaints about pricing or distribution fairness
- Category review preparation — defending distribution strategy
- Annual channel strategy optimization

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Channel map | All active channels with revenue contribution | Channel list with $ and % |
| Pricing by channel | Shelf price, promoted price, net price by SKU/channel | Price matrix |
| Volume by channel | Units and revenue by SKU/channel over time | Time series data |
| Distribution strategy | Which SKUs are authorized for which channels | Authorization matrix |
| Promotional calendars | Promo events by channel with timing and depth | Calendar data |
| Channel economics | Margin structure, trade terms by channel | P&L by channel |
| Consumer overlap | Shopper profile overlap between channels | Demographic/behavioral data |

## Methodology

### Step 1: Channel Architecture Mapping

Map the complete channel ecosystem:

```
Channel Ecosystem:
├── Brick & Mortar
│   ├── Grocery (Kroger, Albertsons, etc.)
│   ├── Mass (Walmart, Target)
│   ├── Club (Costco, Sam's)
│   ├── Drug (CVS, Walgreens)
│   ├── Dollar (Dollar General, Dollar Tree)
│   ├── C-Store (7-Eleven, Circle K)
│   └── Natural/Specialty (Whole Foods, Sprouts)
├── E-Commerce
│   ├── Amazon (1P, 3P, Subscribe & Save)
│   ├── Retailer.com (Walmart.com, Kroger.com, Instacart)
│   ├── DTC (Brand website)
│   └── Other Marketplaces
└── Other
    ├── Foodservice/Away-from-Home
    ├── Club/Warehouse Direct
    └── International/Gray Market
```

For each channel, document: Revenue, Margin, Strategic Role (traffic, margin, brand building, trial).

### Step 2: Pricing Conflict Detection

Scan for pricing violations across the channel matrix:

**Price Consistency Analysis:**

| SKU | Grocery | Mass | Club (per unit) | Amazon | DTC | Conflict? |
|-----|---------|------|-----------------|--------|-----|-----------|
| A | $4.99 | $4.79 | $4.16 | $4.49 | $5.49 | Flag |

**Conflict Types:**

| Conflict Type | Definition | Severity |
|---------------|-----------|----------|
| Minimum Advertised Price (MAP) violation | Channel selling below MAP | Critical |
| Cross-channel undercutting | One channel consistently below others | High |
| Promotional collision | Same product promoted deeply in multiple channels simultaneously | Medium |
| Gray market / diversion | Product appears in unauthorized channels | Critical |
| Size/count arbitrage | Bulk/club sizes resold at unit-competitive prices | High |

**Price Deviation Score:**
```
For each SKU across channels:
  Mean Channel Price = Average of all channel prices
  Deviation Score = (Channel Price − Mean) / Mean × 100
  Flag: Any channel with |Deviation| > 10% from mean
```

### Step 3: Cannibalization Quantification

Measure actual cross-channel volume transfer:

**Time-Series Cannibalization Test:**
```
When Channel A adds a new promotional event or distribution:
  1. Measure Channel A volume change during event period
  2. Measure Channel B, C, D volume change during same period
  3. If Channel B declines while Channel A grows → possible cannibalization

Cannibalization Rate = |Channel B Volume Decline| / Channel A Volume Gain
  0-20%: Low cannibalization (mostly incremental)
  20-50%: Moderate cannibalization (mixed)
  >50%: High cannibalization (primarily shifted, not created)
```

**Category Expansion Test:**
```
Total Category Volume (all channels) during period:
  If Total Volume grew: Channel A generated net category expansion
  If Total Volume flat: Channel A primarily cannibalized
  If Total Volume declined: Channel A may have accelerated decline

Net Incrementality = Total Volume Change − Expected Baseline Growth
```

### Step 4: Consumer Overlap Analysis

Assess shopper duplication across channels:

**Overlap Matrix:**
| | Grocery | Mass | Amazon | DTC |
|---|---------|------|--------|-----|
| Grocery | 100% | 45% | 30% | 8% |
| Mass | — | 100% | 35% | 5% |
| Amazon | — | — | 100% | 15% |
| DTC | — | — | — | 100% |

High overlap (>40%) between channels selling the same SKU indicates high cannibalization risk. Low overlap (<15%) suggests channels serve distinct consumer segments.

**Channel Role Differentiation:**
- Channels with low consumer overlap can carry similar assortments (different shoppers)
- Channels with high overlap should carry differentiated assortments (same shoppers, different needs)

### Step 5: Margin Impact Assessment

Quantify the financial impact of channel conflicts:

```
Conflict Cost Analysis:

1. Price Erosion Cost
   = Units shifted to lower-price channel × Price difference per unit
   Example: 50K units shifted from Grocery ($4.99) to Amazon ($4.49) = $25K revenue loss

2. Margin Dilution Cost
   = Units shifted × Margin differential per unit
   Example: Grocery margin $2.10/unit vs Amazon margin $1.45/unit → $0.65/unit dilution

3. Trade Spend Inefficiency
   = Promotional spend in conflicting events that cannibalize rather than expand
   Example: Simultaneous Kroger TPR and Amazon Lightning Deal → $X wasted spend

4. Retailer Relationship Cost (qualitative)
   = Risk of delisting, reduced support, or punitive chargebacks
   Severity: Low / Medium / High / Critical

Total Quantified Conflict Cost = (1) + (2) + (3)
```

### Step 6: Channel Strategy Optimization

Develop conflict resolution strategies:

**Assortment Differentiation Strategy:**
| Strategy | Method | Example |
|----------|--------|---------|
| Exclusive SKUs | Unique products per channel | Club-exclusive multi-pack |
| Size/count variation | Different pack sizes by channel | Grocery: 12oz; C-Store: 8oz; Club: 36oz |
| Flavor/variant exclusives | Channel-exclusive flavors | Target-exclusive seasonal flavors |
| Bundling | Channel-specific bundles | DTC subscription bundles |
| Price pack architecture | Different price points by channel | Same product, different pack counts |

**Pricing Governance Framework:**
```
Pricing Guardrails:
1. MAP Policy: Minimum advertised price for all channels
2. Channel Price Floor: Minimum net price by channel tier
3. Promotional Depth Limits: Maximum discount % by channel
4. Temporal Separation: No overlapping deep promotions within X weeks
5. Cross-Channel Price Audit: Monthly automated check
```

**Channel Prioritization Matrix:**
| Channel | Revenue | Margin | Growth | Strategic Value | Priority |
|---------|---------|--------|--------|----------------|----------|
| Grocery | High | Medium | Low | Distribution breadth | Protect |
| DTC | Low | High | High | Data + margin | Invest |
| Amazon | Medium | Low | High | Discovery + reach | Manage |
| Club | High | Low | Medium | Volume + trial | Optimize |

## Output Specification

```markdown
# Channel Conflict Analysis — [Brand/Portfolio]

## Executive Summary
[Key conflicts identified, total quantified cost, top 3 resolution priorities]

## Channel Architecture
[Channel map with revenue, margin, and strategic role]

## Conflict Inventory

| # | Conflict Type | Channels | SKUs Affected | Quantified Impact | Severity |
|---|--------------|----------|---------------|-------------------|----------|
| 1 | [Type] | [A vs B] | [SKU list] | $XK/year | Critical/High/Med |
| 2 | ... | ... | ... | ... | ... |

## Pricing Conflict Heat Map
[SKU × Channel matrix with price deviation scores flagged]

## Cannibalization Analysis
[Volume transfer measurements with category expansion test results]

## Financial Impact
- Price Erosion Cost: $XK
- Margin Dilution Cost: $XK
- Trade Spend Waste: $XK
- **Total Quantified Conflict Cost: $XK**

## Resolution Recommendations
### Priority 1: [Highest-impact resolution]
- Action: [Specific action]
- Expected impact: $XK recovered
- Timeline: [Implementation timeline]
- Owner: [Function/role]

### Priority 2-3: [Additional resolutions]

## Governance Framework
[Pricing guardrails and monitoring cadence]

## Monitoring Dashboard Metrics
[KPIs to track ongoing channel health]
```

## Analysis Framework

**Channel Profitability Waterfall:**
```
Gross Revenue by Channel
  − Trade Spend (channel-specific)
  − Channel-specific costs (marketplace fees, shipping, broker)
  = Channel Contribution I
  − Allocated overhead (sales team, marketing)
  = Channel Contribution II
  − Cannibalization adjustment
  = True Channel Value
```

## Example

**Input**: "Our protein bar is sold at Grocery ($3.49), Amazon ($2.99), and our DTC site ($3.99/bar, $2.79/bar on subscription). Amazon unit share growing 15% QoQ. Grocery buyer called about the price gap."

**Analysis excerpt**:
> "A $0.50 (14.3%) price gap between Grocery ($3.49) and Amazon ($2.99) exceeds the 10% conflict threshold and is eroding the retailer relationship. The DTC subscription price ($2.79) undercuts all channels including Amazon, creating a cascading pricing floor. **Quantified impact**: At current Amazon growth rates (+15% QoQ), an estimated 22K units/quarter are shifting from Grocery to Amazon, representing $24K in revenue erosion and $14K in margin dilution (Grocery CM: $1.42/unit vs Amazon CM: $0.78/unit after referral fees). **Resolution**: (1) Implement MAP policy at $3.29 across all channels — Amazon price increases to $3.29; (2) Convert DTC subscription to a unique bundle (4-bar variety pack at $10.99 = $2.75/bar) to differentiate from single-bar channels; (3) Offer Grocery retailer a 60-day exclusive on the new Salted Caramel SKU as a relationship repair gesture."

## Guidelines

- Quantify every conflict in dollars — qualitative assessments alone don't drive action
- Always assess consumer overlap before labeling volume shifts as cannibalization
- Distinguish between healthy channel competition and destructive conflict
- MAP policies must be legally compliant (consult legal on resale price maintenance rules)
- Consider the retailer's perspective — they monitor competitor pricing too
- Channel conflicts are symptoms; root causes are often unclear assortment or pricing strategies
- Monitor gray market and unauthorized sellers quarterly

## Validation Checklist

- [ ] All active channels mapped with revenue, margin, and strategic role
- [ ] Price deviation scores calculated across full SKU × Channel matrix
- [ ] At least 3 conflict types assessed (pricing, cannibalization, promotional)
- [ ] Cannibalization quantified using time-series analysis
- [ ] Consumer overlap assessed between conflicting channels
- [ ] Financial impact quantified: price erosion + margin dilution + trade waste
- [ ] Resolution strategies include assortment, pricing, and governance elements
- [ ] Pricing governance framework defined with guardrails
- [ ] Monitoring KPIs and cadence established
- [ ] Legal considerations flagged for MAP/pricing policies
