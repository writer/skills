---
name: Inventory Risk Alerting
description: Flag overstock and stockout risks across the inventory portfolio by computing weeks of supply, service level projections, and excess/obsolescence exposure, with severity-tiered alerts and recommended corrective actions.

metadata:
  display_name: "Inventory Risk Alerting"
  short_description: "Alert on overstock and stockout inventory risks by severity"
  default_prompt: "Review my inventory risk alerting and highlight top risks and next actions"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Inventory Risk Alerting

## Overview

This skill continuously evaluates inventory positions across SKU-location combinations to identify and classify overstock and stockout risks before they impact customer service or working capital. It computes forward-looking weeks of supply against demand forecasts, evaluates service level probability, and quantifies financial exposure from excess, slow-moving, and obsolete (SLOB) inventory. Alerts are severity-tiered and paired with specific corrective actions.

## When to Use

- Daily or weekly inventory health review across distribution network
- When fill rate drops below target or customer complaints about availability spike
- During monthly S&OP to highlight portfolio-level inventory risks
- When new product launches require cannibalization risk monitoring on existing SKUs
- Before seasonal peaks to ensure forward coverage meets demand surge
- When CFO requests working capital exposure analysis on excess inventory

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `inventory_snapshot` | Current on-hand, in-transit, and on-order quantities by SKU-location | Structured object |
| `demand_forecast` | Forward demand forecast (weekly, 12+ weeks) | Numeric array per SKU-location |
| `safety_stock_params` | Target service level, demand variability, lead time variability | Structured object |
| `lead_times` | Supplier and replenishment lead times by SKU | Numeric (days) |
| `product_lifecycle` | Product status (active, end-of-life, seasonal, new launch) | Enum |
| `cost_data` | Unit cost, carrying cost rate (% of COGS per annum) | Numeric |
| `sales_velocity` | Trailing 4-week and 13-week average daily sales | Numeric |

## Methodology

### Step 1: Weeks of Supply Calculation

```
Weeks_of_Supply = (On_Hand + In_Transit + On_Order - Backorders) / Weekly_Demand_Forecast
```

Classify against category-specific targets:

| Risk Zone | WoS vs. Target | Classification |
|-----------|---------------|----------------|
| Critical Stockout | < 1 week | Immediate action required |
| Stockout Risk | < Safety Stock coverage | Elevated risk |
| Healthy | Within target range (±20%) | No action |
| Overstock Warning | > 1.5× target | Monitor and reduce |
| Critical Overstock | > 2.5× target or > 26 weeks | Markdown/liquidation candidate |

### Step 2: Safety Stock & Service Level Projection

Calculate safety stock using the standard formula:

```
Safety_Stock = Z × √(LT × σ_d² + d² × σ_LT²)
```

Where:
- `Z` = service level Z-score (e.g., 1.65 for 95%, 2.33 for 99%)
- `LT` = average lead time in days
- `σ_d` = standard deviation of daily demand
- `d` = average daily demand
- `σ_LT` = standard deviation of lead time

Project forward service level:
```
Projected_Fill_Rate = P(Demand ≤ Available_Inventory) over review period
```

Flag when projected fill rate drops below target service level within the lead time horizon.

### Step 3: Excess & Obsolescence (E&O) Exposure

Quantify financial risk from overstocked inventory:

```
Excess_Qty = max(0, On_Hand - (Forecast_Demand × Forward_Weeks + Safety_Stock))
Excess_Value = Excess_Qty × Unit_Cost
Carrying_Cost_Exposure = Excess_Value × (Carrying_Cost_Rate / 52) × Estimated_Weeks_to_Clear
```

Apply aging buckets:
- **0-30 days excess**: Manageable through demand pull-forward or transfer
- **31-90 days excess**: Consider promotional markdowns
- **91-180 days excess**: Aggressive markdown or secondary channel liquidation
- **180+ days excess**: Write-off candidate, provision in financial reserves

### Step 4: Velocity-Based Risk Scoring

Compute a composite risk score (0-100) per SKU-location:

```
Risk_Score = w1 × Stockout_Probability + w2 × Excess_Severity + w3 × Lifecycle_Risk + w4 × Demand_Volatility
```

Default weights: `w1=0.35, w2=0.25, w3=0.20, w4=0.20`

Lifecycle risk multipliers:
- End-of-life SKU with >8 WoS: 2.0× multiplier on excess severity
- New launch SKU with <2 WoS: 1.5× multiplier on stockout probability
- Seasonal SKU past peak: 1.8× multiplier on excess severity

### Step 5: Alert Generation & Prioritization

Generate alerts prioritized by:
1. **Revenue at risk** (stockout alerts): `Lost_Sales = Unmet_Demand × Selling_Price × Fill_Rate_Gap`
2. **Capital at risk** (overstock alerts): `Excess_Value + Projected_Carrying_Cost + Markdown_Exposure`
3. **Customer impact**: A-class SKUs and key accounts prioritized

## Output Specification

```yaml
inventory_risk_report:
  generated_at: "2026-02-07T08:00:00Z"
  portfolio_summary:
    total_skus_monitored: 4500
    stockout_risk_count: 127
    overstock_risk_count: 342
    healthy_count: 4031
    total_excess_value: 2450000
    projected_lost_sales: 890000
  critical_alerts:
    - alert_id: "STOCK-001"
      severity: "critical"
      type: "stockout_imminent"
      sku_id: "SKU-78901"
      location: "DC-EAST-02"
      weeks_of_supply: 0.4
      projected_stockout_date: "2026-02-10"
      revenue_at_risk: 125000
      recommended_action: "Expedite PO-44521 (ETA 2/12) or transfer 500 units from DC-WEST-01 (3-day transit)"
      root_cause: "Demand spike from competitor OOS driving substitution"
    - alert_id: "EXCESS-001"
      severity: "high"
      type: "overstock"
      sku_id: "SKU-34567"
      location: "DC-CENTRAL-01"
      weeks_of_supply: 34.2
      excess_value: 89000
      carrying_cost_monthly: 1480
      recommended_action: "Initiate 20% markdown via promotional calendar or transfer to high-velocity locations"
      root_cause: "Forecast over-bias of +40% during Q4 promo that underperformed"
```

## Analysis Framework

### ABC Classification for Alert Thresholds

| Class | Revenue Share | Stockout Threshold | Overstock Threshold | Review Frequency |
|-------|-------------|-------------------|---------------------|-----------------|
| A | Top 80% revenue | < 2 WoS | > 8 WoS | Daily |
| B | Next 15% revenue | < 1.5 WoS | > 12 WoS | Weekly |
| C | Bottom 5% revenue | < 1 WoS | > 16 WoS | Bi-weekly |

### Key Performance Indicators

- **Inventory Turns**: `COGS / Average_Inventory_Value` — target varies by category (grocery: 15-25, general merch: 4-8)
- **GMROI**: `Gross_Margin / Average_Inventory_Cost` — target > 2.0 for healthy ROI
- **Days of Supply**: `Average_Inventory / Average_Daily_COGS` — complement to WoS for financial view
- **Fill Rate**: `Units_Shipped / Units_Ordered` — target 95-98.5% for A-class items
- **Perfect Order Rate**: Orders delivered on-time, in-full, undamaged, with correct documentation

## Examples

**Example 1 — Stockout Risk Alert**
> "ALERT [CRITICAL]: SKU-78901 (Premium Coffee 12oz) at DC-EAST-02 has 0.4 weeks of supply remaining with weekly demand of 1,200 units. No open POs. Revenue at risk: $125,000 over next 3 weeks. Action: Place emergency PO for 5,000 units with expedited shipping, estimated 4-day lead time. Alternative: Transfer 2,000 units from DC-WEST-01 where WoS = 6.8."

**Example 2 — Overstock Alert with E&O Quantification**
> "ALERT [HIGH]: SKU-34567 (Seasonal Sunscreen SPF-30) at DC-CENTRAL-01 has 34.2 WoS (target: 8 WoS). Excess quantity: 8,900 units valued at $89,000. Monthly carrying cost: $1,480. Product is post-season with declining demand. If not actioned within 60 days, projected markdown loss is $44,500 (50% of excess value). Recommend immediate 20% promotional markdown and cross-DC rebalancing."

## Guidelines

1. Run stockout risk detection daily for A-class items; weekly for B/C-class
2. Always include the financial impact in alerts — units alone do not drive executive action
3. Factor in in-transit and on-order inventory to avoid false stockout alerts
4. For seasonal items, use seasonal demand forecast (not trailing average) for WoS calculations
5. Distinguish between planned promotional overstock (intentional forward buy) and unplanned excess
6. Cross-reference stockout alerts with substitution availability — if a direct substitute is in stock, lower severity
7. Account for minimum order quantities (MOQs) when recommending reorder actions
8. Include lead time in stockout horizon — alert must fire before lead time window closes
9. Track alert-to-action conversion rate to calibrate thresholds and reduce alert fatigue

## Validation Checklist

- [ ] Inventory snapshot is current (within 24 hours for daily alerts)
- [ ] Demand forecast aligns with the latest consensus forecast from S&OP
- [ ] Safety stock parameters reflect current service level targets by category
- [ ] Lead times are updated to reflect actual recent supplier performance, not contractual
- [ ] E&O calculations use current standard cost, not historical purchase price
- [ ] Seasonal classification is current — items are flagged pre-season, in-season, and post-season
- [ ] Alert deduplication logic prevents repeated alerts for the same SKU-location-risk within the suppression window
- [ ] Financial exposure totals reconcile with inventory valuation reports from finance
- [ ] Recommended actions are feasible (check supplier capacity, transfer lane availability, markdown approval authority)
