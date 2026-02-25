---
name: assortment-gap-analysis
description: >
  Identifies gaps in a retailer's or e-commerce platform's product assortment by comparing the current catalog
  against market demand signals, competitor offerings, and consumer search behavior. Use when the user wants to
  find missing products, underserved segments, whitespace opportunities, or optimize category breadth and depth.
  Triggers on requests mentioning assortment gaps, catalog gaps, missing SKUs, whitespace analysis, or
  category coverage assessment.

metadata:
  display_name: "Assortment Gap Analysis"
  short_description: "Find product assortment gaps versus market demand signals"
  default_prompt: "Analyze my assortment gap and recommend clear next actions"
  version: "1.0.0"
  tags:
    - commerce-intelligence
    - assortment-gap-analysis
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Assortment Gap Analysis

## Overview

Assortment Gap Analysis systematically evaluates a retailer's product catalog to identify missing items, underrepresented segments, and whitespace opportunities that represent unmet consumer demand. This skill combines internal sales data with external demand signals—search queries, competitor catalogs, trend data—to produce a prioritized list of assortment gaps with revenue sizing and fill recommendations.

In CPG and retail, assortment optimization directly impacts category growth. Studies consistently show that 15–25% of category revenue potential is lost due to assortment gaps, while 10–20% of SKUs are redundant. This skill focuses on finding the missing revenue, not trimming the tail (see SKU Rationalization for that).

## When to Use

- A category manager asks what products are missing from their assortment
- The user provides sales data and wants to know where demand is unmet
- Competitive benchmarking reveals the catalog is thinner in specific segments
- Consumer search data shows high-volume queries with zero or low results
- A new market, channel, or store cluster needs an assortment built from scratch
- Annual or quarterly category review requires a gap assessment

## Required Inputs

| Input | Required | Description |
|---|---|---|
| Current catalog/assortment | Yes | SKU list with attributes (brand, size, flavor, price tier, segment) |
| Sales data | Yes | At least 12 weeks of unit and revenue data by SKU |
| Category taxonomy | Yes | Hierarchical structure (category > subcategory > segment > subsegment) |
| Consumer search/demand data | Recommended | Site search queries, Google Trends, keyword volumes |
| Competitor assortment | Recommended | Competitor SKU lists or shelf snapshots |
| Market/syndicated data | Optional | Nielsen, IRI/Circana, or Euromonitor category data |
| Store/channel attributes | Optional | Format, geography, demographic cluster |

## Methodology

### Step 1: Structure the Category Decision Tree

Build a hierarchical decision tree that represents how consumers navigate the category. Typical CPG dimensions:

- **Need state** (e.g., everyday cooking vs. premium entertaining)
- **Form/format** (e.g., liquid, powder, pod, fresh, frozen)
- **Brand tier** (national brand, premium, value, private label)
- **Size/pack** (single serve, family size, bulk/club)
- **Flavor/variant** (original, organic, sugar-free, seasonal)
- **Price tier** (opening price point, mid, premium, super-premium)

Map every current SKU onto this tree so empty cells become visible.

### Step 2: Demand Signal Analysis

Quantify demand for each node in the decision tree:

1. **Internal search signals**: Aggregate site search queries; identify high-volume terms with zero results or low click-through.
2. **External search signals**: Google Trends, Amazon search frequency rank, keyword volume for the category.
3. **Sales velocity benchmarks**: For populated nodes, compute $/TDP (Total Distribution Points) or $/store/week. Flag nodes where velocity far exceeds peers—indicating latent demand that more SKUs could capture.
4. **Market share vs. fair share**: Compare your revenue share per segment to market-level segment share (from syndicated data). A segment where your share is 5% but the market is 15% signals an assortment gap.

### Step 3: Competitive Coverage Mapping

For each decision-tree node, count SKUs offered by top 3–5 competitors. Compute a **Coverage Index**:

```
Coverage Index = (Your SKU count in segment / Avg competitor SKU count in segment) × 100
```

- **< 70**: Significant gap — likely losing shoppers
- **70–100**: Parity — evaluate quality of assortment
- **> 130**: Potential over-assortment — check for cannibalization

### Step 4: Gap Prioritization

Score each identified gap on a 2×2 matrix:

| | High Market Demand | Low Market Demand |
|---|---|---|
| **Easy to Fill** (existing suppliers, simple logistics) | **Priority 1 — Quick Win** | **Priority 3 — Monitor** |
| **Hard to Fill** (new supplier, cold chain, regulatory) | **Priority 2 — Strategic** | **Priority 4 — Deprioritize** |

For each Priority 1 and 2 gap, estimate incremental revenue:

```
Incremental Revenue = Market Size of Segment × Target Fair Share × (1 − Current Share / Fair Share)
```

### Step 5: Fill Recommendations

For each gap, recommend:

- Specific product attributes needed (brand tier, size, price point, flavor)
- Whether to fill via national brand listing, private label development, or exclusive
- Estimated number of SKUs to add
- Cannibalization risk to existing SKUs (substitution ratio estimate)
- Supplier or brand candidates if known

## Output Specification

Deliver the following structured output:

### 1. Assortment Gap Summary Table

| Gap ID | Segment | Gap Description | Market Demand Score (1-10) | Fill Difficulty (1-5) | Priority | Est. Incremental Revenue | Recommended Action |
|---|---|---|---|---|---|---|---|
| G-001 | Organic Snack Bars / Single Serve | No organic option under $2.00 | 8 | 2 | Quick Win | $1.2M/yr | List 2 national brand SKUs |

### 2. Category Decision Tree Heatmap

Visual or tabular representation of the decision tree with cells color-coded:
- Green: Well-covered, strong velocity
- Yellow: Present but underperforming vs. market
- Red: Empty or severely under-indexed
- Blue: Over-assorted vs. market

### 3. Search Demand Gap Report

Top 20 unmatched or under-matched search terms with monthly volume, current catalog match rate, and recommended products.

### 4. Competitive Coverage Scorecard

Coverage Index by segment vs. each key competitor with overall weighted average.

### 5. Revenue Sizing Summary

Total addressable gap revenue, broken into Priority 1–4 buckets, with confidence intervals.

## Analysis Framework

### Key Metrics

- **Assortment Breadth Index**: Number of unique subsegments covered / total subsegments in market
- **Assortment Depth Score**: Average SKUs per subsegment vs. market average
- **Fair Share Index**: Your segment revenue share / market segment revenue share (target ≥ 1.0)
- **Search-to-Shelf Ratio**: % of top 100 search terms that have a matching SKU in catalog
- **New Item Opportunity Score**: Composite of demand signal strength, competitive gap, and fill feasibility
- **Substitution Risk Rate**: Estimated % of new SKU revenue that cannibalizes existing SKUs (benchmark: 20–35% in CPG)

### Industry Benchmarks

- Top-quartile retailers cover 85%+ of consumer decision-tree nodes
- Average e-commerce catalog has 12–18% redundant SKUs and 8–14% missing critical segments
- Search null-result rate should be below 5% for a well-assorted catalog
- Private label should represent 20–30% of SKU count and 15–25% of category revenue in mature categories

## Examples

**Input**: "Analyze gaps in our Snacking category. We carry 340 SKUs across bars, chips, crackers, nuts, and fruit snacks. Here is our sales data and the competitor assortment from Target and Walmart."

**Output**: The agent produces:
1. A decision tree with 48 nodes; 7 nodes are empty (red), 11 are under-indexed (yellow)
2. Top gaps: (a) No keto/low-carb bars under $2 — $3.4M opportunity, (b) No organic cheese crackers — $1.1M opportunity, (c) Missing single-serve nut mixes in 1oz format — $0.8M opportunity
3. Total addressable gap revenue: $8.7M across 7 Priority 1 and 4 Priority 2 gaps
4. Coverage Index vs. Target: 74 (gaps in better-for-you and premium tiers)
5. Top unmatched search terms: "keto snack bar" (14K/mo), "organic goldfish crackers" (8K/mo)

## Guidelines

- Always build the decision tree before scanning for gaps — structure prevents overlooking non-obvious segments
- Use at least two independent demand signals to validate a gap (e.g., search data + competitor presence)
- Distinguish between assortment gaps (missing segments) and distribution gaps (listed but not available in all stores/regions)
- Account for private label potential: if the gap is in a commoditized segment, recommend PL before national brand
- Never recommend adding SKUs without estimating cannibalization impact on existing items
- Flag regulatory or supply-chain constraints (e.g., CBD products, allergen requirements, cold chain)
- Segment analysis by channel (online vs. in-store) since optimal assortment differs
- Consider planogram and shelf-space constraints for brick-and-mortar recommendations
- Size recommendations proportionally: don't suggest 50 SKUs for a segment that warrants 3

## Validation Checklist

- [ ] Every gap is mapped to a specific node in the category decision tree
- [ ] Demand is validated by at least two signals (search, syndicated, competitor, trend)
- [ ] Revenue estimates include methodology and assumptions
- [ ] Cannibalization risk is assessed for each recommendation
- [ ] Gaps are prioritized using the demand × feasibility matrix
- [ ] Competitive coverage index is calculated against at least 2 competitors
- [ ] Private label vs. national brand fill strategy is specified
- [ ] Output includes both quick wins (< 90 days) and strategic plays (6–12 months)
- [ ] Channel-specific considerations are noted where relevant
