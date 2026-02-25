---
name: Replenishment Recommendation
description: Generate optimal reorder quantities and timing using Economic Order Quantity, safety stock models, and demand-driven replenishment strategies, factoring in supplier constraints, MOQs, and working capital targets.

metadata:
  display_name: "Replenishment Recommendation"
  short_description: "Recommend optimal reorder quantities, timing, and safety stock"
  default_prompt: "Optimize my replenishment recommendation and suggest the best next steps"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Replenishment Recommendation

## Overview

This skill generates precise replenishment recommendations—what to order, how much, and when—for each SKU-location combination. It combines Economic Order Quantity (EOQ) optimization with demand-driven replenishment policies, respecting real-world constraints such as minimum order quantities (MOQs), supplier capacity, shelf life, warehouse capacity, and working capital budgets. The output is a prioritized, actionable order plan that balances service level targets against inventory investment.

## When to Use

- During regular replenishment review cycles (daily/weekly purchase order generation)
- When inventory drops below reorder point and automated triggers fire
- During pre-season build planning for seasonal categories
- When supplier lead times change and safety stock recalibration is needed
- When working capital constraints require prioritization of limited ordering budget
- After a stockout event to determine recovery order quantities

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `inventory_position` | On-hand + in-transit + on-order - backorders - allocated | Numeric per SKU-location |
| `demand_forecast` | Forward weekly demand forecast (minimum lead time + review period) | Numeric array |
| `lead_time` | Supplier lead time in days (average and standard deviation) | Numeric |
| `review_period` | Ordering frequency (days between order opportunities) | Numeric |
| `service_level_target` | Target fill rate or cycle service level (%) | Numeric |
| `cost_parameters` | Unit cost, ordering cost per PO, carrying cost rate (% p.a.) | Structured object |
| `supplier_constraints` | MOQ, case pack, pallet quantity, max order capacity | Structured object |
| `shelf_life` | Product shelf life in days (for perishables) | Numeric (optional) |
| `warehouse_capacity` | Available storage in units, cases, or pallets | Numeric (optional) |

## Methodology

### Step 1: Reorder Point Calculation

Compute the reorder point (ROP) that triggers a replenishment:

```
ROP = (Average_Daily_Demand × Lead_Time) + Safety_Stock
```

Where safety stock accounts for both demand and supply variability:

```
Safety_Stock = Z × √(LT × σ_d² + d_avg² × σ_LT²)
```

- `Z` = Z-score for target service level (1.28 for 90%, 1.65 for 95%, 2.33 for 99%)
- `LT` = average lead time in days
- `σ_d` = standard deviation of daily demand
- `d_avg` = average daily demand
- `σ_LT` = standard deviation of lead time in days

### Step 2: Economic Order Quantity (EOQ)

Calculate the cost-optimal order quantity:

```
EOQ = √(2 × D × S / H)
```

Where:
- `D` = annual demand in units
- `S` = fixed ordering cost per purchase order (administrative + freight setup)
- `H` = annual holding cost per unit = `Unit_Cost × Carrying_Cost_Rate`

Adjust EOQ for practical constraints:
```
Adjusted_EOQ = max(MOQ, round_up_to_case_pack(EOQ))
If Adjusted_EOQ > Warehouse_Capacity_Available: cap at capacity and flag
If Shelf_Life < (Adjusted_EOQ / Daily_Demand): reduce to shelf-life-safe quantity
```

### Step 3: Order-Up-To Level (for Periodic Review Systems)

For periodic review replenishment policies:

```
Order_Up_To = Demand_During_(LT + Review_Period) + Safety_Stock
Order_Qty = max(0, Order_Up_To - Inventory_Position)
```

Apply rounding to case pack or pallet quantities:
```
Final_Order_Qty = round_up_to_nearest(Order_Qty, Case_Pack_Size)
If Final_Order_Qty < MOQ and Order_Qty > 0: set Final_Order_Qty = MOQ
```

### Step 4: Multi-Constraint Optimization

When working capital or warehouse capacity is constrained, prioritize across SKUs:

**Priority Score** = `Service_Level_Gap × Revenue_Weight × Criticality_Factor`

Where:
- `Service_Level_Gap` = `Target_SL - Projected_SL_Without_Order`
- `Revenue_Weight` = SKU revenue share (A-class items weighted higher)
- `Criticality_Factor` = 2.0 for must-not-stock-out items, 1.0 for standard, 0.5 for long-tail

Allocate budget using greedy knapsack: order highest-priority SKUs first until budget or capacity is exhausted.

### Step 5: Order Consolidation & Timing

- **Vendor consolidation**: Group orders to same supplier to achieve freight breaks and volume discounts
- **Full truckload optimization**: Aggregate orders to hit FTL thresholds (e.g., 40,000 lbs or 2,500 cubic feet)
- **Order timing**: If projected stockout date > lead time + buffer, delay order to reduce carrying cost
- **Forward buy evaluation**: If a supplier offers temporary discount, compute break-even weeks of supply:
  ```
  Break_Even_WoS = Discount% / (Carrying_Cost_Rate / 52)
  ```
  Only forward buy if expected sell-through is within break-even window.

## Output Specification

```yaml
replenishment_plan:
  generated_at: "2026-02-07T06:00:00Z"
  planning_horizon: "2026-02-07 to 2026-03-07"
  summary:
    total_order_lines: 245
    total_order_value: 1850000
    total_units: 128500
    orders_by_priority:
      critical: 18
      high: 67
      standard: 160
  orders:
    - sku_id: "SKU-11234"
      location: "DC-EAST-02"
      supplier: "SUP-ACME-01"
      recommended_qty: 2400
      unit_cost: 4.50
      order_value: 10800
      order_type: "standard_replenishment"
      priority: "critical"
      reorder_point: 1800
      current_position: 450
      safety_stock: 620
      eoq: 2200
      adjusted_reason: "Rounded up to pallet quantity (2400 = 4 pallets × 600)"
      projected_wos_after_receipt: 6.2
      recommended_order_date: "2026-02-07"
      expected_receipt_date: "2026-02-17"
      projected_stockout_date_without_order: "2026-02-11"
```

## Analysis Framework

### Replenishment Policy Selection Guide

| Demand Pattern | Variability | Recommended Policy | Review Cycle |
|---------------|-------------|-------------------|--------------|
| Steady, predictable (AX) | Low CoV (<0.3) | Continuous review (s,Q) with EOQ | Event-driven |
| Moderate variability (AY) | Medium CoV (0.3-0.7) | Periodic review (R,S) with dynamic SS | Weekly |
| Highly variable (AZ) | High CoV (>0.7) | Min-max with demand sensing | Daily |
| Slow-moving (CX/CY) | Low/Medium | (s,S) with aggregate ordering | Bi-weekly |
| Intermittent/lumpy (CZ) | Very high | Poisson or Croston's method for SS | Monthly + event triggers |

### Key Metrics to Track

- **Inventory Turns**: `Annual_COGS / Average_Inventory` — higher = more efficient capital use
- **Fill Rate**: `Line_Items_Fulfilled_Complete / Total_Line_Items_Ordered`
- **Purchase Order Cycle Time**: Days from PO creation to goods receipt
- **Supplier OTIF**: On-Time In-Full delivery performance by supplier
- **Working Capital Efficiency**: `Inventory_Value / Monthly_Revenue` — target < 1.0 for fast-turning CPG

## Examples

**Example 1 — Standard EOQ Replenishment**
> "SKU-11234 (Paper Towels 8-pack) at DC-EAST-02: Current position is 450 units with ROP at 1,800. Weekly demand forecast: 580 units. EOQ calculates to 2,200 units but rounded to 2,400 (full pallet = 600 units × 4). Order value: $10,800. If ordered today, receipt expected Feb 17. Without order, projected stockout Feb 11. Priority: CRITICAL."

**Example 2 — Constrained Budget Allocation**
> "Weekly ordering budget is $500,000 against $850,000 in recommended orders. Applying priority scoring: 18 critical orders ($145,000) fully funded, 67 high-priority orders ($310,000) fully funded, remaining $45,000 allocated to top 12 standard orders by service-level gap. 148 standard orders deferred to next cycle. Projected portfolio fill rate with this allocation: 96.2% (vs. 98.5% if fully funded)."

## Guidelines

1. Never recommend an order quantity below the supplier MOQ — either order MOQ or defer
2. For perishable goods, cap order quantity at `Daily_Demand × (Shelf_Life - Lead_Time - Buffer_Days)`
3. Always show the projected weeks of supply after receipt so planners can validate reasonableness
4. Flag when EOQ suggests a quantity that exceeds 12 weeks of supply — challenge the ordering cost assumption
5. Include in-transit inventory in position calculations to avoid double-ordering
6. When multiple DCs can source from the same supplier, consolidate at the PO level for freight optimization
7. For new product launches without demand history, use analogous product demand with a 1.5× safety factor
8. Recalculate safety stock monthly or when demand CV or lead time CV changes by more than 15%
9. Present the incremental carrying cost of ordering above EOQ so planners understand the trade-off

## Validation Checklist

- [ ] Inventory positions are net of allocations, holds, and quality quarantine
- [ ] Demand forecast reflects the latest consensus numbers including promotions
- [ ] Lead times use actual supplier performance data (not contractual lead times)
- [ ] Safety stock Z-score matches the agreed service level policy for each SKU class
- [ ] MOQ and case pack constraints are current per latest supplier agreements
- [ ] Working capital budget, if constrained, is provided by finance for the planning period
- [ ] Shelf-life constraint is applied for all perishable and limited-life SKUs
- [ ] Freight consolidation logic checks actual shipment routing, not assumed lanes
- [ ] Recommended order dates account for supplier order windows and cutoff times
- [ ] Total order value reconciles with unit costs from the latest supplier price file
