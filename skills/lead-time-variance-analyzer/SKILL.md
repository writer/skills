---
name: Lead Time Variance Analyzer
description: Diagnose supply delays by decomposing lead time into constituent stages, identifying variance sources, quantifying downstream impact on inventory and service levels, and recommending corrective actions.

metadata:
  display_name: "Lead Time Variance Analyzer"
  short_description: "Diagnose supply chain lead time variances and delays"
  default_prompt: "Analyze my lead time variance and recommend clear next actions"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Lead Time Variance Analyzer

## Overview

This skill systematically decomposes end-to-end procurement lead time into its constituent stages—order processing, manufacturing, quality inspection, transportation, customs/clearance, and receiving—to identify where delays originate, quantify their frequency and severity, and assess downstream impact on safety stock, service levels, and working capital. It provides root-cause diagnosis using adapted Ishikawa (fishbone) analysis and recommends targeted interventions to reduce lead time mean and variability.

## When to Use

- When supplier lead times are longer or more variable than contractual terms
- When safety stock levels are inflated due to lead time uncertainty
- During supplier performance reviews to pinpoint specific delay stages
- When evaluating nearshoring or logistics lane changes
- After a stockout event where lead time variance was a contributing factor
- When onboarding new suppliers to establish baseline lead time expectations

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `purchase_orders` | PO-level data with key milestone timestamps (minimum 6 months) | Structured array |
| `milestone_timestamps` | Order placed, acknowledged, shipped, arrived at port, cleared customs, received at DC | DateTime per PO |
| `contractual_lead_times` | Agreed lead time by stage per supplier/product | Numeric (days) |
| `transportation_mode` | Ocean, air, rail, truck, intermodal | Enum per PO |
| `supplier_profile` | Supplier location, manufacturing type, capacity data | Structured object |
| `product_characteristics` | Weight, volume, hazmat classification, shelf life, customs classification | Structured object |
| `inventory_parameters` | Current safety stock, service level, demand rate | Structured object |

## Methodology

### Step 1: Lead Time Decomposition

Break total lead time into measurable stages with timestamps:

```
Total_Lead_Time = T_order_processing + T_manufacturing + T_quality_inspection 
                + T_packaging_dispatch + T_transportation + T_customs_clearance 
                + T_receiving_putaway
```

For each stage, compute:
```
Mean_Stage_i = Σ(Stage_Duration_i) / n
StdDev_Stage_i = √(Σ(Stage_Duration_i - Mean_i)² / (n-1))
CV_Stage_i = StdDev_i / Mean_i  [coefficient of variation]
```

### Step 2: Variance Contribution Analysis

Determine which stages contribute most to total lead time variability:

```
Variance_Contribution_i = σ_i² / Σ(σ_j²) × 100%
```

This identifies the highest-leverage stages for improvement. A stage contributing >40% of total variance is the primary target.

Also compute:
- **P90 Lead Time**: 90th percentile — the "worst reasonable case" for planning
- **P50 Lead Time**: Median — more robust than mean for skewed distributions
- **Range**: Max - Min — identifies extreme outliers
- **Skewness**: Positive skew (long right tail) indicates occasional severe delays

### Step 3: Trend & Seasonality Detection

Analyze lead time trends over time:

```
LT_Trend = linear regression slope of monthly average lead time
Seasonal_Pattern = month-over-month lead time index (normalized to annual average)
```

Common seasonal patterns:
- **Chinese New Year** (Jan-Feb): +2-4 weeks for Asia-sourced goods
- **Peak shipping season** (Aug-Oct): +1-2 weeks ocean transit due to congestion
- **Monsoon season** (Jun-Sep): Disruption to South/Southeast Asian suppliers
- **Year-end factory shutdowns** (Dec): European supplier delays

### Step 4: Root Cause Diagnosis (Ishikawa Framework)

For stages with high variance contribution, apply adapted fishbone analysis:

**Manufacturing Delays (T_manufacturing)**
- Capacity constraints (high utilization, competing orders)
- Raw material shortages at supplier
- Quality rework loops
- Equipment downtime / maintenance scheduling
- Workforce availability (holidays, labor disputes)

**Transportation Delays (T_transportation)**
- Carrier capacity shortages (peak season, equipment imbalance)
- Port congestion (vessel waiting time, berth availability)
- Route disruptions (weather, canal closures, infrastructure failures)
- Mode selection mismatch (ocean vs. air trade-off not optimized)
- Consolidation delays (waiting for full container loads)

**Customs & Clearance Delays (T_customs_clearance)**
- Incomplete or incorrect documentation
- Regulatory inspections (random or triggered by classification)
- Tariff classification disputes
- Trade compliance holds (sanctions, restricted entities)
- Broker processing capacity

**Receiving Delays (T_receiving_putaway)**
- Dock scheduling conflicts
- Labor shortages at DC
- Quality inspection backlogs
- System receiving errors (ASN mismatch)
- Seasonal volume surge exceeding receiving capacity

### Step 5: Downstream Impact Quantification

Calculate the impact of lead time variance on inventory and service:

```
Safety_Stock_Current = Z × √(LT_mean × σ_d² + d_avg² × σ_LT²)
Safety_Stock_If_LT_Reduced = Z × √(LT_target × σ_d² + d_avg² × σ_LT_target²)
SS_Reduction_Units = Safety_Stock_Current - Safety_Stock_If_LT_Reduced
SS_Reduction_Value = SS_Reduction_Units × Unit_Cost
Working_Capital_Freed = SS_Reduction_Value  [one-time inventory reduction]
Annual_Carrying_Savings = SS_Reduction_Value × Carrying_Cost_Rate
```

Service level impact:
```
Current_SL = Φ((Inventory_Position - Demand_During_LT) / σ_Demand_During_LT)
SL_at_P90_LT = Φ((Inventory_Position - Demand_During_P90_LT) / σ_Demand_During_P90_LT)
SL_Gap = Current_SL - SL_at_P90_LT  [service level erosion during long lead times]
```

## Output Specification

```yaml
lead_time_analysis:
  supplier: "SUP-ORIENT-MFG"
  analysis_period: "2025-08 to 2026-01"
  sample_size: 156
  total_lead_time:
    contractual_days: 42
    actual_mean: 51.3
    actual_median: 48
    actual_p90: 67
    actual_stddev: 11.4
    cv: 0.22
    trend: "+1.2 days/month"
  stage_decomposition:
    - stage: "Order Processing"
      mean_days: 3.2
      stddev: 1.1
      variance_contribution_pct: 4
      contractual: 2
    - stage: "Manufacturing"
      mean_days: 18.5
      stddev: 6.8
      variance_contribution_pct: 42
      contractual: 14
      root_causes:
        - "Raw material delays from tier-2 supplier (38% of late POs)"
        - "Capacity contention with higher-priority customer (25% of late POs)"
    - stage: "Ocean Transportation"
      mean_days: 22.1
      stddev: 5.2
      variance_contribution_pct: 31
      contractual: 21
    - stage: "Customs Clearance"
      mean_days: 4.8
      stddev: 3.9
      variance_contribution_pct: 18
      contractual: 3
    - stage: "Receiving & Putaway"
      mean_days: 2.7
      stddev: 1.4
      variance_contribution_pct: 5
      contractual: 2
  downstream_impact:
    current_safety_stock_units: 12400
    target_safety_stock_units: 7800
    potential_ss_reduction_value: 230000
    annual_carrying_cost_savings: 57500
    service_level_erosion_at_p90: "2.8 percentage points"
  recommendations:
    - priority: "high"
      action: "Negotiate tier-2 raw material buffer stock with supplier"
      expected_lt_reduction_days: 4
      expected_variance_reduction_pct: 25
    - priority: "medium"
      action: "Switch to direct-ship ocean routing (bypass transshipment port)"
      expected_lt_reduction_days: 3
      expected_variance_reduction_pct: 15
```

## Analysis Framework

### Lead Time Maturity Model

| Level | Mean Adherence | CV | Characteristic |
|-------|---------------|-----|---------------|
| 1 - Reactive | >120% of contract | >0.40 | No visibility, frequent surprises |
| 2 - Measured | 110-120% of contract | 0.30-0.40 | Tracked but not managed |
| 3 - Managed | 100-110% of contract | 0.20-0.30 | Active supplier management, improving |
| 4 - Optimized | 95-100% of contract | 0.10-0.20 | Predictable, buffer-minimized |
| 5 - Synchronized | ≤95% of contract | <0.10 | Demand-synchronized, VMI-level integration |

### 5 Whys Adaptation for Lead Time Delays

Apply structured 5 Whys to the top variance-contributing stage:

1. **Why** was the shipment late? → Manufacturing completed 8 days behind schedule
2. **Why** was manufacturing late? → Key raw material was not available
3. **Why** was the raw material unavailable? → Tier-2 supplier had a quality rejection on their batch
4. **Why** did the tier-2 quality issue occur? → Incoming material spec was changed without notification
5. **Why** was the spec change not communicated? → No formal engineering change management process between tier-1 and tier-2

**Root Cause**: Lack of tier-2 supplier change management process
**Systemic Fix**: Implement ECN (Engineering Change Notice) protocol in supplier quality agreement

## Examples

**Example 1 — Manufacturing Variance Diagnosis**
> "Supplier Orient Manufacturing shows mean lead time of 51.3 days vs. 42-day contract (122% adherence). Manufacturing stage contributes 42% of total variance (σ = 6.8 days). Analysis of 156 POs reveals two root causes: tier-2 raw material delays affecting 38% of late orders, and capacity contention during Q4 peak affecting 25%. Recommended: negotiate 2-week raw material buffer stock at supplier site (estimated cost: $45,000, expected lead time reduction: 4 days, variance reduction: 25%)."

**Example 2 — Transportation & Customs Compound Delay**
> "Import lead time from Vietnam has increased by 1.2 days/month over 6 months. Ocean transit variance spiked during Aug-Oct due to vessel schedule reliability dropping to 58% on the Asia-West Coast route. Customs clearance shows high skewness (mean 4.8 days, P90: 12 days) driven by random FDA inspections on food-contact materials. Combined impact: safety stock is 59% higher than needed if lead times matched contract. Recommend: (1) diversify to two carrier alliances, (2) pre-file customs documentation 5 days before vessel arrival, (3) obtain C-TPAT certification to reduce inspection frequency."

## Guidelines

1. Require minimum 30 PO observations per supplier for statistically meaningful variance analysis
2. Exclude known force majeure events from trend analysis but report them separately
3. Use median (P50) rather than mean for skewed lead time distributions
4. Always pair lead time reduction recommendations with expected safety stock savings to build the ROI case
5. Differentiate between lead time mean reduction (faster) and variance reduction (more predictable) — variance reduction often has higher ROI
6. Track lead time by product family, not just supplier, since different products may have different manufacturing complexity
7. For international suppliers, separate pre-customs and post-customs lead time to isolate logistics from trade compliance issues
8. Update lead time parameters in the replenishment system whenever the analysis shows a >10% change
9. Compare actual lead times against the parameters currently used in inventory planning — misalignment is a common source of stockouts

## Validation Checklist

- [ ] PO milestone timestamps are complete — no missing stages that would bias analysis
- [ ] Contractual lead times reflect current agreements, not expired contracts
- [ ] Transportation mode is correctly tagged (ocean vs. air can differ by 3-5 weeks)
- [ ] Outlier POs are investigated, not just excluded — they often reveal systemic risks
- [ ] Variance contribution percentages sum to 100%
- [ ] Safety stock impact calculations use the same demand data as the replenishment system
- [ ] Seasonal patterns are identified and separated from trend analysis
- [ ] Root cause analysis goes beyond the supplier to include tier-2 and logistics provider factors
- [ ] Recommendations include estimated cost, timeline, and expected quantified benefit
- [ ] Analysis has been validated with the supplier to confirm root causes before action plans are finalized
