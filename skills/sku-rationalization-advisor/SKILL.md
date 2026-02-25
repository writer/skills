---
name: sku-rationalization-advisor
description: >
  Evaluates and recommends SKU-level actions (keep, delist, consolidate, replace) to optimize assortment
  efficiency, reduce complexity costs, and improve inventory productivity. Use when the user wants to reduce
  SKU count, identify underperforming items, streamline assortment, or conduct a portfolio pruning exercise.
  Triggers on requests about SKU rationalization, tail-SKU analysis, assortment pruning, delisting candidates,
  or long-tail optimization.

metadata:
  display_name: "SKU Rationalization Advisor"
  short_description: "Advise on SKU keep, delist, or consolidate actions"
  default_prompt: "Optimize my sku rationalization and suggest the best next steps"
  version: "1.0.0"
  tags:
    - commerce-intelligence
    - sku-rationalization-advisor
    - cpg-retail
  icon_path: "assets/icon.png"
---

# SKU Rationalization Advisor

## Overview

SKU Rationalization Advisor systematically evaluates every SKU in a category or portfolio against performance, strategic, and operational criteria to recommend keep/delist/consolidate/replace actions. The goal is to reduce complexity costs and free shelf space or warehouse capacity for higher-potential items without sacrificing meaningful consumer choice.

In CPG retail, the long tail is expensive. Industry analysis shows that the bottom 20% of SKUs typically contribute only 1–3% of revenue but consume 15–25% of inventory carrying costs, supply chain complexity, and shelf space. However, naive pruning destroys value—some low-velocity SKUs serve as strategic traffic drivers, assortment signals, or niche segment anchors. This skill applies a multi-criteria framework to distinguish truly unproductive SKUs from strategically necessary ones.

## When to Use

- Annual assortment reset or planogram reset cycle
- Warehouse or shelf-space capacity constraints require SKU reduction
- Category has grown to excessive SKU count through years of additions without removals
- Supply chain or procurement team flags complexity costs
- Preparing for private label expansion (need shelf space for new PL items)
- Post-acquisition portfolio integration requiring duplicate elimination
- User provides SKU-level data and asks which items to cut

## Required Inputs

| Input | Required | Description |
|---|---|---|
| SKU master list | Yes | Full catalog with attributes: brand, size, flavor, segment, pack, price |
| Sales data (12+ weeks) | Yes | Units, revenue, and ideally margin by SKU; 52 weeks preferred |
| Inventory data | Recommended | Average inventory $, turns, days of supply, stockout rate |
| Margin/cost data | Recommended | Gross margin $, gross margin %, COGS, landed cost |
| Distribution data | Recommended | Store count, %ACV, or warehouse allocation |
| Substitution/switching data | Optional | Which SKUs shoppers switch to when one is unavailable |
| Supplier/vendor data | Optional | Supplier dependencies, exclusive arrangements, MOQ requirements |
| Strategic item flags | Optional | Items with contractual obligations, brand commitments, or strategic role |

## Methodology

### Step 1: SKU Performance Scoring

Score every SKU on four dimensions (each 0–100):

**A. Revenue Contribution Score**
```
Revenue Score = (SKU Revenue / Category Revenue) × 10,000
```
Normalize to 0–100 scale. Pareto benchmark: top 20% of SKUs should score > 60.

**B. Profitability Score**
```
Profit Score = (SKU Gross Margin $ / Top-SKU Gross Margin $) × 100
```
If margin data unavailable, use ASP relative to category average as proxy.

**C. Velocity Score**
```
Velocity Score = (SKU Units per Store per Week / Category Avg Units per Store per Week) × 100
```
Cap at 100. Measures inventory productivity and consumer demand intensity.

**D. Trend Score**
```
Trend Score = 50 + (SKU YoY Growth Rate − Category YoY Growth Rate) × 5
```
Centered at 50; above 50 = outperforming category trend, below = underperforming. Cap at 0–100.

**Composite Score** (weighted):
```
Composite = (Revenue × 0.30) + (Profit × 0.30) + (Velocity × 0.25) + (Trend × 0.15)
```

### Step 2: Strategic Role Assessment

Assign each SKU a strategic role that may override pure performance scores:

| Role | Definition | Protection Level |
|---|---|---|
| **Traffic Driver** | Generates store/site visits; high search volume, destination item | High — keep even if margin is low |
| **Basket Builder** | High attach rate; frequently bought with other items | Medium-High |
| **Margin Anchor** | Above-average margin %; may have low velocity | Medium |
| **Assortment Signal** | Represents a segment that defines category credibility | Medium — keep at least 1 SKU |
| **Niche/Loyalty** | Small but fiercely loyal customer base; high repeat rate | Medium — evaluate switching risk |
| **Filler/Redundant** | No unique role; interchangeable with other SKUs | Low — primary delist candidate |

### Step 3: Redundancy & Cannibalization Analysis

Identify clusters of overlapping SKUs:

1. Group SKUs by attribute similarity (same brand + same segment + similar price ± 10%)
2. Within each cluster, calculate **Incremental Contribution**: revenue that would be lost if the SKU were removed (net of substitution to remaining SKUs)
3. Apply a **Substitution Rate** assumption: typically 40–65% for CPG (i.e., 40–65% of a delisted SKU's sales transfer to remaining items)

```
Net Revenue at Risk = SKU Revenue × (1 − Substitution Rate)
```

### Step 4: Action Classification

Based on Composite Score, Strategic Role, and Redundancy:

| Composite Score | Strategic Role | Redundancy | Recommended Action |
|---|---|---|---|
| > 60 | Any | Any | **Keep** — core performer |
| 40–60 | Traffic/Basket/Signal | Low | **Keep** — strategically important |
| 40–60 | Filler | High | **Consolidate** — merge with stronger variant |
| 20–40 | Any non-critical | High | **Replace** — swap for higher-potential alternative |
| < 20 | Filler/Redundant | Any | **Delist** — remove from assortment |
| < 20 | Niche/Loyalty | Low | **Review** — manual decision required |

### Step 5: Impact Simulation

Simulate the impact of recommended delistments:

```
Total Delist Revenue = Σ (Delisted SKU Revenue)
Retained Revenue = Σ (Delisted SKU Revenue × Substitution Rate)
Net Revenue Loss = Total Delist Revenue − Retained Revenue
Complexity Savings = # SKUs Removed × Cost per SKU (inventory carry + handling + space)
Net Impact = Complexity Savings − Net Revenue Loss
```

Industry benchmark: Cost per SKU ranges from $5,000–$50,000/year depending on category and supply chain complexity.

## Output Specification

### 1. SKU Action Summary

| SKU | Brand | Segment | Revenue | Composite Score | Strategic Role | Action | Net Revenue Risk | Substitute SKU |
|---|---|---|---|---|---|---|---|---|
| — | — | — | — | — | — | Keep/Delist/Consolidate/Replace | — | — |

### 2. Portfolio Impact Dashboard

- Total SKUs: current → proposed
- Revenue at risk (gross) and retained (net of substitution)
- Complexity cost savings
- Net margin improvement
- Shelf space / warehouse slots freed

### 3. Delist Candidate Detail Cards

For each delisted SKU:
- Performance scores breakdown
- Top 3 substitute SKUs and substitution rationale
- Customer impact assessment (loyalty segment affected)
- Supplier impact (any volume commitments or deductions at risk)
- Recommended exit timeline

### 4. Consolidation Recommendations

Clusters of SKUs to merge, with proposed surviving SKU and rationale.

## Analysis Framework

### Key Metrics

- **SKU Productivity**: Revenue per SKU (benchmark: top quartile > 2× category average)
- **Pareto Ratio**: % of revenue from top 20% of SKUs (benchmark: 75–85%)
- **Long-Tail Burden**: % of SKUs contributing < 0.1% of category revenue
- **Inventory Turns by SKU**: Turns < 4×/year in center store signals overstock or low demand
- **Incremental Contribution**: Revenue uniquely attributable to the SKU (not transferable)
- **Complexity Cost per SKU**: Fully loaded cost including procurement, warehousing, handling, shelf management
- **Customer Reach**: % of total buyers who purchased the SKU in the last 52 weeks

### Decision Thresholds

- Delist threshold: Bottom 15–25% of SKUs by composite score, unless strategically protected
- Minimum viable assortment: At least 1 SKU per decision-tree node that has demonstrated demand
- Maximum delist batch: Recommend no more than 15% of SKU count in a single reset to manage disruption
- Substitution rate validation: If observed switching data is available, use it; otherwise apply category-level default (50%)

## Examples

**Input**: "We have 1,200 SKUs in our Home Cleaning category. Management wants to reduce to 900 SKUs while maintaining at least 95% of current revenue. Here's our 52-week sales, margin, and inventory data."

**Output**:
1. **Scoring**: 1,200 SKUs scored; 187 score below 20 (delist zone), 124 score 20–40 (replace zone), remaining 889 score > 40
2. **Redundancy**: 93 SKU clusters identified with high overlap; 156 SKUs are redundant within clusters
3. **Recommendations**: Delist 168 SKUs, consolidate 84 into 42, replace 48 → net reduction of 258 SKUs (to 942)
4. **Impact**: Gross revenue at risk $4.2M (3.8%); estimated retained after substitution $2.9M; net loss $1.3M (1.2%). Complexity savings: $2.1M/year. Net benefit: +$0.8M/year.
5. **Top delist clusters**: 14 niche air freshener variants (0.3% of revenue, 1.2% of SKUs), 22 legacy packaging sizes in dish soap, 11 private label duplicates with identical formulations

## Guidelines

- Never recommend delisting the only SKU serving a valid consumer need state — that creates an assortment gap
- Apply a "buyer count" safety check: if a SKU has > 2% of category buyers, flag for manual review even if scores are low
- Consider seasonal SKUs separately — annualized metrics understate their in-season importance
- Respect contractual and promotional commitments; flag timing constraints for delistments
- Communicate delist recommendations with sensitivity: provide data-backed rationale, not just scores
- Stagger delistments over 2–3 reset windows rather than a single mass cut
- Monitor post-delist performance for 8–12 weeks; have contingency to relist if substitution doesn't materialize
- Always pair rationalization with gap-fill recommendations (use Assortment Gap Analysis skill) — rationalize and renovate simultaneously

## Validation Checklist

- [ ] Every SKU has been scored on all four dimensions
- [ ] Strategic roles are assigned and protection levels applied
- [ ] Redundancy analysis uses attribute-based clustering, not just performance data
- [ ] Substitution rates are documented and defensible
- [ ] Net revenue impact is calculated (not just gross delist revenue)
- [ ] Complexity cost savings are estimated
- [ ] No single-representative segments are left empty after delistments
- [ ] Seasonal SKUs are evaluated on in-season performance
- [ ] Supplier and contractual constraints are flagged
- [ ] Delist count stays within the recommended maximum per reset cycle
