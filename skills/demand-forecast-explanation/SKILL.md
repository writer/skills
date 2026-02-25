---
name: Demand Forecast Explanation
description: Explain forecast drivers and decomposition to demand planners, translating statistical models into actionable business narratives with accuracy metrics, bias analysis, and root-cause attribution for forecast deviations.

metadata:
  display_name: "Demand Forecast Explanation"
  short_description: "Explain demand forecast drivers, bias, and deviations"
  default_prompt: "Explain my demand forecast in simple words and next steps"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Demand Forecast Explanation

## Overview

This skill translates complex demand forecasting model outputs into clear, actionable explanations for demand planners and supply chain stakeholders. It decomposes forecasts into constituent drivers—baseline demand, trend, seasonality, promotions, price elasticity, and external factors—and attributes forecast error to specific causes. The goal is to bridge the gap between data science outputs and planner decision-making, enabling informed consensus adjustments.

## When to Use

- A demand planner asks why a forecast increased or decreased for a specific SKU/location
- Stakeholders need to understand what is driving demand for an upcoming planning cycle
- Forecast accuracy has degraded and leadership requires root-cause attribution
- During S&OP meetings when forecast assumptions need to be defended or challenged
- When comparing statistical forecast vs. consensus forecast to justify overrides
- Post-period forecast error review to improve future accuracy

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `sku_id` | Product identifier (SKU, GTIN, or internal ID) | String |
| `location_id` | Store, DC, or region identifier | String |
| `forecast_period` | Time horizon (weekly, monthly, quarterly) | ISO date range |
| `statistical_forecast` | Model-generated forecast values | Numeric array |
| `actuals` | Historical actual demand (minimum 52 weeks) | Numeric array |
| `promotion_calendar` | Planned and historical promotions | Structured object |
| `price_history` | Historical and planned price points | Numeric array |
| `external_signals` | Weather, events, macro indicators (optional) | Structured object |

## Methodology

### Step 1: Forecast Decomposition

Break the aggregate forecast into additive or multiplicative components:

```
Forecast = Baseline + Trend + Seasonality + Promo_Lift + Price_Effect + External_Factors + Residual
```

- **Baseline**: Deseasonalized, detrended average demand (rolling 12-week median)
- **Trend**: Linear or exponential growth/decline rate (units per period)
- **Seasonality**: Seasonal indices by period (e.g., week-of-year indices normalized to 1.0)
- **Promo Lift**: Incremental volume from promotions (calculated as promoted vs. non-promoted base)
- **Price Effect**: Price elasticity impact using `ΔQ/Q ÷ ΔP/P` coefficient
- **External Factors**: Weather sensitivity coefficients, event-driven demand spikes

### Step 2: Accuracy Metrics Computation

Calculate standard forecast accuracy KPIs:

- **MAPE** (Mean Absolute Percentage Error): `MAPE = (1/n) × Σ|Actual - Forecast| / Actual × 100`
- **Weighted MAPE**: Weight by revenue or volume to prioritize high-value SKUs
- **Bias**: `Bias = Σ(Forecast - Actual) / Σ(Actual) × 100` — positive = over-forecast, negative = under-forecast
- **Tracking Signal**: `TS = RSFE / MAD` — flag when |TS| > 4 for systematic bias
- **Forecast Value Added (FVA)**: Compare each step in the process (statistical → consensus → final) to naive forecast

### Step 3: Error Attribution

For each period where `|Actual - Forecast| / Actual > threshold` (default 20%):

1. **Promotion Attribution**: Did an unplanned promotion or cancelled promotion explain the gap?
2. **Distribution Gap**: Was the product available? Check in-stock rate and void scan data
3. **Cannibalization/Halo**: Did a related SKU promotion shift demand?
4. **External Shock**: Weather events, competitor actions, market disruption
5. **Model Drift**: Has the underlying demand pattern changed (structural break test)?

### Step 4: Narrative Generation

Construct a planner-friendly explanation following this template:

> "For [SKU] at [Location] during [Period], the forecast of [X units] was [Y%] [above/below] actual demand of [Z units]. The primary driver was [Driver 1] contributing [N units] of the deviation, followed by [Driver 2] at [M units]. The forecast [does/does not] show systematic bias (tracking signal = [TS])."

### Step 5: Recommendation Synthesis

Based on error patterns, recommend:
- Adjusting seasonal indices if seasonality has shifted
- Incorporating new causal variables if external factors are material
- Planner override guidelines with confidence intervals
- Segmentation changes (move SKU between A/B/C forecast tiers)

## Output Specification

```yaml
forecast_explanation:
  sku_id: "SKU-12345"
  location: "DC-WEST-01"
  period: "2026-W06 to 2026-W10"
  forecast_summary:
    statistical_forecast: 12500
    consensus_forecast: 13000
    actual: 11800
  decomposition:
    baseline: 9200
    trend: -150
    seasonality: 1800
    promo_lift: 1400
    price_effect: 250
    external: 0
  accuracy_metrics:
    mape: 10.2
    bias_pct: 5.8
    tracking_signal: 2.3
    fva_vs_naive: 12.5
  error_attribution:
    - driver: "Promo cancellation"
      impact_units: -800
      confidence: "high"
    - driver: "Seasonal index drift"
      impact_units: -350
      confidence: "medium"
  narrative: "..."
  recommendations:
    - "Recalibrate seasonal indices using 2025-2026 data"
    - "Flag promo calendar sync as upstream data quality issue"
```

## Analysis Framework

### ABC-XYZ Segmentation for Forecast Prioritization

| Segment | Volume (ABC) | Variability (XYZ) | Forecast Approach |
|---------|-------------|-------------------|-------------------|
| AX | High volume, low variability | Statistical auto-forecast, minimal planner touch |
| AY | High volume, moderate variability | Statistical + planner review of promotions |
| AZ | High volume, high variability | Planner-intensive, scenario-based forecasting |
| BX-CZ | Lower volume | Aggregate forecasting, safety stock buffers |

### Bias Pattern Detection

- **Persistent positive bias** (>3 consecutive periods): Model is systematically over-forecasting — investigate demand decline, distribution loss, or competitive entry
- **Persistent negative bias**: Model is under-forecasting — investigate organic growth, new distribution, or untracked promotions
- **Oscillating bias**: Model is chasing noise — consider dampening or longer smoothing windows

## Examples

**Example 1 — Seasonal Forecast Miss**
> "Sunscreen SPF-50 at Southeast DC forecast 45,000 units for June but actual was 38,200 (MAPE: 17.8%). Decomposition shows seasonal index was calibrated on 2023-2024 data when summer started earlier. Recommend recalibrating with 2025 weather-adjusted start dates. Bias is +15.2% indicating systematic over-forecast for this category."

**Example 2 — Promotion-Driven Variance**
> "Organic Pasta 16oz forecast 8,200 units during BOGO week but actual was 12,400. The promo lift model estimated 40% uplift based on prior TPRs, but BOGO events historically drive 80-120% uplift for this subcategory. FVA analysis shows consensus adjustment added 1,200 units but still fell short. Recommend a BOGO-specific uplift coefficient."

## Guidelines

1. Always present accuracy metrics in context — a 25% MAPE on a CZ item is acceptable; on an AX item it signals a problem
2. Distinguish between forecastable error (model improvement opportunity) and unforecastable error (random demand variation)
3. Quantify each driver's contribution in units, not just percentages, so planners can make tangible adjustments
4. Compare FVA at each process step to identify whether planner overrides are adding or destroying value
5. Use 52-week rolling windows for accuracy metrics to smooth out period-specific anomalies
6. Flag when sample sizes are too small for reliable decomposition (fewer than 13 periods of history)
7. Present recommendations ranked by expected impact on forecast accuracy improvement

## Validation Checklist

- [ ] Decomposition components sum to within 2% of the total forecast
- [ ] MAPE, bias, and tracking signal are computed on aligned actuals (same granularity, same periods)
- [ ] Promotion calendar is synchronized with the latest trade promotion management system export
- [ ] Error attribution drivers are mutually exclusive and collectively exhaustive
- [ ] Narrative is free of statistical jargon — uses business terms planners understand
- [ ] Recommendations include specific parameter changes, not just directional guidance
- [ ] FVA analysis includes naive benchmark (e.g., same period last year) as the baseline
- [ ] Seasonal index recalibration recommendation includes the proposed new indices
- [ ] Output YAML conforms to the specification schema and passes validation
