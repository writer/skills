---
name: Warehouse Slotting Optimizer
description: Recommend optimal product placement within warehouse zones and pick locations using velocity-based slotting, ergonomic analysis, product affinity grouping, and space utilization modeling to minimize travel time and maximize throughput.

metadata:
  display_name: "Warehouse Slotting Optimizer"
  short_description: "Optimize warehouse product slotting and pick placement"
  default_prompt: "Optimize my warehouse slotting and suggest the best next steps"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Warehouse Slotting Optimizer

## Overview

This skill generates optimal warehouse product placement recommendations by analyzing pick velocity, order affinity, product physical characteristics, and ergonomic factors. Effective slotting reduces picker travel time (typically 50-60% of pick labor), improves throughput, reduces errors, and maximizes cubic space utilization. The skill applies ABC velocity stratification, correlated product analysis, golden zone ergonomic principles, and simulation-based validation to produce actionable slot assignment plans.

## When to Use

- During periodic slotting reviews (recommended quarterly for fast-moving SKUs)
- After significant assortment changes (new product launches, discontinuations)
- When pick productivity (units per labor hour) is declining or below benchmark
- After warehouse layout changes (new racking, zone reconfiguration, expansion)
- Before peak season to optimize for anticipated demand profile shifts
- When pick error rates are elevated and mis-picks may be slotting-related
- During new warehouse setup or WMS implementation

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `pick_history` | SKU-level pick frequency, lines, and units over trailing 13 weeks | Structured array |
| `order_profiles` | Order composition showing which SKUs are frequently ordered together | Structured array |
| `product_dimensions` | Length, width, height, weight per unit and per case | Structured object per SKU |
| `warehouse_layout` | Zone definitions, aisle/bay/level structure, pick face dimensions | Structured object |
| `current_slotting` | Current SKU-to-location assignments | Mapping table |
| `storage_types` | Available location types (floor, shelf, carton flow, pallet rack, mezzanine) | Structured object |
| `labor_standards` | Travel time between zones, pick time per location type, replenishment time | Structured object |
| `ergonomic_constraints` | Max weight for golden zone, height restrictions, ADA requirements | Structured object |

## Methodology

### Step 1: Velocity Analysis (ABC Classification)

Classify SKUs by pick frequency using Pareto distribution:

```
Pick_Velocity = Total_Picks / Active_Days  [picks per day]
Cumulative_Pick_Share = Running_Sum(Picks_per_SKU) / Total_Picks
```

| Class | Cumulative Pick Share | Typical SKU % | Slot Zone |
|-------|----------------------|---------------|-----------|
| A+ (Super fast) | Top 5% of picks | 1-2% of SKUs | Prime forward pick, golden zone, carton flow |
| A (Fast) | 5-50% of picks | 3-8% of SKUs | Forward pick area, ergonomic height |
| B (Medium) | 50-85% of picks | 10-20% of SKUs | Standard pick area, mid-level |
| C (Slow) | 85-95% of picks | 20-30% of SKUs | Reserve area, higher/lower levels |
| D (Very slow) | 95-100% of picks | 40-60% of SKUs | Remote storage, pick on demand |

### Step 2: Affinity Analysis (Correlated Picks)

Identify products frequently ordered together to slot them in proximity:

```
Affinity_Score(SKU_i, SKU_j) = Co_occurrence_Count(i,j) / max(Pick_Count(i), Pick_Count(j))
```

Build an affinity matrix and apply clustering (hierarchical or k-means) to group correlated SKUs. Benefits:
- Reduces travel distance for multi-line orders
- Enables zone-based wave picking efficiency
- Reduces cross-zone picks per order

Prioritize affinity for A-class items; low-velocity items benefit less from proximity optimization.

### Step 3: Ergonomic Zone Assignment (Golden Zone Principle)

The "golden zone" is the ergonomically optimal pick height range (waist to shoulder, approximately 24"-54" from floor):

```
Ergonomic_Priority_Score = Pick_Velocity × Weight_Factor
```

Assignment rules:
| Zone Height | Zone Name | Assign To |
|-------------|-----------|-----------|
| 0-12" | Floor level | Heavy items (>40 lbs), full-case picks, pallet picks |
| 12-24" | Low zone | B/C items, moderate weight |
| 24-54" | Golden zone | A+/A items, highest velocity, any weight |
| 54-72" | Upper zone | B/C items, lightweight only (<15 lbs) |
| 72"+ | Top stock | D items, reserve replenishment, lightweight |

Ergonomic cost multipliers for non-golden-zone picks:
- Floor level: 1.3× pick time (bending)
- Upper zone: 1.2× pick time (reaching)
- Top stock: 1.5× pick time (ladder/equipment required)

### Step 4: Space & Container Optimization

Match product to optimal storage medium:

```
Space_Efficiency = (Product_Volume × Units_per_Face) / Location_Volume × 100
Replenishment_Frequency = Daily_Picks / Units_per_Face_Location
```

| Storage Type | Best For | Pick Speed | Space Efficiency |
|-------------|----------|------------|-----------------|
| Carton flow rack | A+/A eaches, consistent case size | Fastest | High |
| Shelf (bin) | Small items, A/B eaches | Fast | Medium |
| Pallet position | Full-case or pallet picks, B/C items | Medium | Highest |
| Floor stack | Very high volume, uniform pallets | Medium | High |
| Mezzanine | Slow movers, lightweight, overflow | Slow | High |
| Automated (AS/RS) | Varies by system | Variable | Very high |

Ensure pick face capacity covers at minimum one shift's demand to avoid mid-shift replenishment:
```
Min_Face_Qty = Peak_Shift_Picks × 1.2  [20% buffer]
If Min_Face_Qty > Location_Capacity: assign a larger location type or split across locations
```

### Step 5: Travel Path Optimization

Calculate expected travel time reduction from proposed slotting changes:

```
Current_Travel = Σ(Pick_i × Distance_to_Location_i × 2)  [round-trip to each pick]
Proposed_Travel = Σ(Pick_i × Distance_to_New_Location_i × 2)
Travel_Reduction = (Current_Travel - Proposed_Travel) / Current_Travel × 100
```

For batch/wave picking environments:
```
Batch_Travel = Tour_Distance(Locations_in_Batch)  [traveling salesman approximation]
```

Optimize for common pick path routing (serpentine, skip-aisle, or zone-based) rather than pure distance.

### Step 6: Slot Change Execution Planning

Generate a prioritized move plan:

```
Move_Priority = Travel_Savings × Pick_Frequency / Move_Effort
```

Where `Move_Effort` = labor time to relocate product (proportional to inventory on hand).

Best practices for execution:
- Execute slot changes during low-volume periods (weekends, early shifts)
- Move highest-impact A+ items first (top 50 SKUs may capture 60%+ of savings)
- Update WMS location assignments in real-time as physical moves complete
- Perform cycle counts on moved items to ensure inventory accuracy

## Output Specification

```yaml
slotting_recommendation:
  analysis_date: "2026-02-07"
  warehouse: "DC-EAST-02"
  skus_analyzed: 8500
  current_performance:
    avg_travel_per_order: 142  # feet
    picks_per_labor_hour: 95
    replenishment_frequency: 3.2  # per shift per zone
    golden_zone_utilization: 62  # percent of golden zone = A items
  proposed_performance:
    avg_travel_per_order: 98  # feet
    picks_per_labor_hour: 128
    replenishment_frequency: 2.1
    golden_zone_utilization: 91
  improvement_summary:
    travel_reduction_pct: 31
    productivity_increase_pct: 35
    annual_labor_savings: 420000
    moves_required: 1240
    move_labor_hours: 310
    move_cost: 9300
    payback_period_days: 8
  top_moves:
    - sku_id: "SKU-SOAP-001"
      current_location: "A-14-C-3"
      proposed_location: "A-02-B-2"
      reason: "A+ velocity (85 picks/day), currently in C-zone; move to golden zone carton flow"
      daily_travel_savings_ft: 2400
    - sku_id: "SKU-BATT-044"
      current_location: "A-03-B-1"
      proposed_location: "D-22-A-4"
      reason: "D velocity (0.3 picks/day) occupying prime golden zone location; relocate to reserve"
      freed_location_value: "Reassign to A+ SKU"
  affinity_clusters:
    - cluster_id: 1
      skus: ["SKU-PASTA-01", "SKU-SAUCE-07", "SKU-CHEESE-12"]
      co_occurrence_rate: 0.42
      recommended_zone: "Zone A, Aisle 3-4"
```

## Analysis Framework

### Slotting Effectiveness KPIs

| KPI | Definition | Target |
|-----|-----------|--------|
| Picks per labor hour | Total picks / direct labor hours | 100-150 (manual), 200+ (semi-automated) |
| Travel time % | Travel time / total productive time | < 40% (good), < 30% (excellent) |
| Golden zone A-item % | A items in golden zone / total A items | > 85% |
| Replenishment trips per shift | Forward area replenishments per shift | < 2 per zone per shift |
| Pick accuracy | Correct picks / total picks | > 99.8% |
| Cube utilization | Used cubic feet / available cubic feet | 75-85% (allows movement) |

### Slot Profile Matching Matrix

| Product Velocity | Product Size | Product Weight | Recommended Slot |
|-----------------|-------------|---------------|-----------------|
| A+ | Small | Light | Carton flow, golden zone center of aisle |
| A+ | Large/Heavy | Heavy | Floor-level pallet, close to shipping |
| A | Medium | Medium | Shelf pick, golden zone |
| B | Any | Any | Standard shelf, mid-level |
| C/D | Small | Light | High shelf, mezzanine |
| C/D | Large | Heavy | Reserve pallet rack, remote |

## Examples

**Example 1 — Velocity-Based Reslotting**
> "DC-EAST-02 analysis shows only 62% of golden zone locations contain A/A+ velocity items. 340 golden zone positions are occupied by C/D items (< 1 pick/day). Proposed reslotting moves 340 slow movers to upper/remote locations and fills golden zone with top 340 velocity SKUs. Expected impact: 31% travel reduction, picks per labor hour improves from 95 to 128, annual labor savings of $420,000. Total move effort: 310 labor hours ($9,300). Payback: 8 days."

**Example 2 — Affinity-Based Zone Clustering**
> "Order analysis reveals pasta, sauce, and cheese SKUs appear together in 42% of orders. Currently slotted across 3 different zones requiring cross-zone travel. Clustering these 15 SKUs into Zone A, Aisles 3-4 reduces average multi-line order travel by 85 feet (22%). For 1,200 multi-line orders per day, this saves approximately 28 labor hours daily."

## Guidelines

1. Re-slot A+ and A items quarterly; B/C/D items semi-annually unless velocity changes significantly
2. Never slot purely by velocity — always incorporate product dimensions, weight, and ergonomic constraints
3. Maintain 10-15% of locations as flex/overflow to accommodate promotional inventory and new launches
4. Slot promotional items in forward pick areas 1-2 weeks before promotion start date
5. Consider pick path routing when assigning locations — mirror slotting to routing algorithm (serpentine, skip-aisle)
6. Don't split a single SKU across multiple pick faces unless demand exceeds any single location's capacity
7. Account for replenishment accessibility — floor-level carton flow is easy to replenish; upper shelves require equipment
8. For cold chain or hazmat products, slot within compliant zones first, then optimize within those constraints
9. Validate slotting changes with floor supervisors — picker tribal knowledge often identifies practical constraints not in data

## Validation Checklist

- [ ] Pick history covers at least 13 weeks to smooth out promotional and seasonal noise
- [ ] Product dimensions and weights are verified against physical measurements, not just catalog data
- [ ] Warehouse layout data reflects current configuration (recent layout changes captured)
- [ ] Current slotting assignments in WMS match physical reality (verified by cycle counts)
- [ ] Golden zone height range is calibrated to the actual workforce (not theoretical)
- [ ] Affinity analysis uses order-level co-occurrence, not just category assumptions
- [ ] Proposed slotting respects storage type constraints (temperature, hazmat, weight limits per shelf)
- [ ] Replenishment frequency calculations use peak demand, not average demand
- [ ] Move plan is sequenced to avoid blocking aisles or creating temporary out-of-stock in active pick faces
- [ ] ROI calculation includes move labor cost and any temporary productivity dip during transition
