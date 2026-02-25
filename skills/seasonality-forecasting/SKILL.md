---
name: seasonality-forecasting
description: >
  Identifies, quantifies, and forecasts seasonal demand patterns for CPG and retail products to optimize
  inventory, promotions, and assortment timing. Use when the user wants to understand seasonal trends,
  build seasonal demand forecasts, plan seasonal inventory, or optimize the timing of product launches,
  promotions, and markdowns. Triggers on requests about seasonality, seasonal demand, seasonal planning,
  demand forecasting, or seasonal inventory optimization.

metadata:
  display_name: "Seasonality Forecasting"
  short_description: "Forecast seasonal demand patterns for inventory planning"
  default_prompt: "Optimize my seasonality forecasting and suggest the best next steps"
  version: "1.0.0"
  tags:
    - commerce-intelligence
    - seasonality-forecasting
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Seasonality Forecasting

## Overview

Seasonality Forecasting decomposes historical demand into trend, seasonal, and residual components to produce accurate forecasts that account for predictable demand fluctuations. In CPG and retail, seasonality is the most reliable and actionable demand signal—it repeats annually with high fidelity and can be planned for months in advance.

Failure to properly account for seasonality is the single largest source of preventable stockouts and overstock in retail. Seasonal peaks missed by 1–2 weeks result in lost sales; seasonal inventory not cleared by markdown timing erodes margin. This skill delivers precise seasonal profiles and actionable timing recommendations.

## When to Use

- Annual demand planning and open-to-buy budgeting
- Inventory pre-build decisions for seasonal peaks
- Promotion calendar timing aligned to seasonal demand cycles
- Seasonal assortment transitions (e.g., summer → fall planogram reset)
- New product launch timing optimization
- Markdown and clearance timing for seasonal inventory
- User provides historical sales data and asks about seasonal patterns

## Required Inputs

| Input | Required | Description |
|---|---|---|
| Historical sales data | Yes | Weekly or monthly units/revenue; minimum 2 full years (104 weeks), ideally 3+ years |
| Product hierarchy | Yes | Category, subcategory, brand, SKU for aggregation levels |
| Calendar data | Recommended | Holiday dates, promotional calendar, store events |
| Weather data | Optional | Regional temperature, precipitation for weather-sensitive categories |
| Macro indicators | Optional | Economic data, school calendars, cultural events for context |
| New product flags | Optional | Launch dates for items without full history |

## Methodology

### Step 1: Data Preparation and Cleaning

1. **Aggregate to appropriate level**: SKU-level for high-volume items, subcategory or brand level for slower-moving items (need ≥ 50 units/week for reliable SKU-level seasonality)
2. **Align to consistent calendar**: Convert to ISO weeks or 4-5-4 retail calendar for comparable periods
3. **Adjust for anomalies**: Remove or flag COVID-period data (2020-2021), extreme weather events, supply disruptions, stockout periods
4. **Normalize for distribution**: If store count changed, convert to per-store-per-week metrics before decomposition
5. **Handle holiday shifts**: Easter, Ramadan, Lunar New Year, and other movable holidays must be aligned by event, not calendar date

### Step 2: Time Series Decomposition

Decompose the demand signal into three components:

```
Y(t) = Trend(t) × Seasonal(t) × Residual(t)   [Multiplicative model]
Y(t) = Trend(t) + Seasonal(t) + Residual(t)    [Additive model]
```

**Choose multiplicative** when seasonal amplitude grows with trend (most CPG categories).
**Choose additive** when seasonal amplitude is constant regardless of trend level.

**Decomposition methods** (in order of recommendation):

1. **STL (Seasonal-Trend decomposition using LOESS)**: Robust, handles outliers, flexible seasonal period
2. **X-13ARIMA-SEATS**: Gold standard for official statistics; handles trading-day effects and holiday effects
3. **Classical decomposition**: Moving-average based; simple but less robust to outliers
4. **Prophet**: Bayesian approach; good with multiple seasonality (weekly + annual) and holiday effects

Extract the **Seasonal Index** for each period:

```
Seasonal Index(week w) = Average Seasonal Component(week w) / Grand Mean of Seasonal Component
```

An index of 1.20 means demand in that week is typically 20% above average.

### Step 3: Seasonal Profile Construction

Build a seasonal profile (52-week or 12-month index) for each product/category:

| Week | Seasonal Index | Classification | Planning Implication |
|---|---|---|---|
| W1–W4 (Jan) | 0.85 | Trough | Post-holiday clearance; lean inventory |
| W5–W8 (Feb) | 0.90 | Below average | Valentine's spike in confection/floral only |
| W18–W22 (May) | 1.15 | Shoulder | Pre-build for summer peak |
| W23–W35 (Jun-Aug) | 1.35 | Peak | Maximum inventory; increase promotional activity |
| W44–W48 (Nov) | 1.40 | Holiday peak | Thanksgiving/Black Friday; maximum coverage |
| W49–W52 (Dec) | 1.55 | Maximum peak | Holiday gifting; risk of overstock post-Dec 25 |

**Peak-to-Trough Ratio**: Measure of seasonality intensity:
```
PT Ratio = Max Seasonal Index / Min Seasonal Index
```
- PT < 1.3: Low seasonality (staples: paper towels, dish soap)
- PT 1.3–2.0: Moderate seasonality (most CPG food & beverage)
- PT 2.0–4.0: High seasonality (sunscreen, allergy meds, grilling)
- PT > 4.0: Extreme seasonality (holiday candy, pool chemicals, de-icer)

### Step 4: Demand Forecasting

Combine trend projection with seasonal profile:

```
Forecast(t) = Projected Trend(t) × Seasonal Index(t) × Adjustment Factors
```

**Trend projection methods**:
- Linear trend: Adequate for stable categories
- Exponential smoothing (Holt-Winters): Captures level and trend with adaptive weighting
- Growth curves: For categories in growth or decline phases

**Adjustment factors**:
- Planned promotional lifts (from promotion calendar)
- Distribution changes (new store openings, channel expansion)
- Known external events (Olympics, World Cup, elections)
- Macro-economic adjustments (inflation impact on volume)

**Forecast accuracy metrics**:
```
MAPE = (1/n) × Σ |Actual − Forecast| / Actual × 100
WMAPE = Σ |Actual − Forecast| / Σ Actual × 100
Bias = Σ (Forecast − Actual) / Σ Actual × 100
```

Target: MAPE < 15% at weekly category level; < 25% at weekly SKU level.

### Step 5: Inventory and Timing Recommendations

Translate the forecast into operational decisions:

**Safety Stock by Season**:
```
Safety Stock = z × σ_demand × √(Lead Time + Review Period)
```
Increase z-score (service level) during peak season to prevent stockouts on high-velocity items.

**Pre-Build Timing**: Start inventory build `Lead Time + 2 weeks` before the seasonal ramp begins.

**Markdown Timing**: Initiate seasonal clearance when:
```
Weeks of Supply > Remaining Weeks in Season × 1.5
```

**Assortment Transition Windows**: Recommend dates for:
- Seasonal set introduction (e.g., summer grilling set goes live Week 18)
- Core assortment flex (expand/contract shelf space to match seasonal index)
- End-of-season clearance start and target completion dates

### Step 6: Category-Specific Seasonal Drivers

Map external drivers to seasonal patterns for causal understanding:

| Driver | Affected Categories | Index Impact | Data Source |
|---|---|---|---|
| Temperature > 80°F | Beverages, ice cream, sunscreen | +25–60% | Weather API |
| Back-to-school (Aug) | Snacks, lunch items, school supplies | +15–30% | School calendar |
| Cold/flu season (Nov-Feb) | OTC medicine, tissues, soup | +40–80% | CDC flu data |
| Grilling season (May-Sep) | Charcoal, condiments, hot dogs, buns | +50–120% | Temperature data |
| Holiday baking (Nov-Dec) | Flour, sugar, butter, baking mixes | +80–200% | Calendar |
| Super Bowl (early Feb) | Chips, dips, beer, frozen appetizers | +100–300% (event week) | Event calendar |

## Output Specification

### 1. Seasonal Profile Report

52-week (or 12-month) seasonal index chart and table for each product/category analyzed.

### 2. Demand Forecast

Point forecast with prediction intervals (80% and 95%) for the planning horizon (typically 13–52 weeks).

### 3. Seasonal Classification

Categorization of each product/category by seasonality intensity (low/moderate/high/extreme) with peak-to-trough ratio.

### 4. Operational Calendar

| Event | Category | Timing | Action | Inventory Implication |
|---|---|---|---|---|
| Summer ramp begins | Beverages | Week 18 | Increase orders | +35% vs. baseline |
| Peak week | Sunscreen | Week 27 | Maximum coverage | 4 weeks forward cover |
| Markdown start | Summer seasonal | Week 34 | Begin clearance | Target 90% sell-through by W38 |

### 5. Forecast Accuracy Assessment

Backtesting results showing MAPE, bias, and hit rate for prior-year seasonal forecasts.

## Analysis Framework

### Key Metrics

- **Seasonal Index**: Ratio of expected demand in a period to average demand (1.0 = average)
- **Peak-to-Trough Ratio**: Measures seasonality amplitude
- **MAPE / WMAPE**: Forecast accuracy
- **Forecast Bias**: Systematic over/under-forecasting tendency
- **In-Stock Rate During Peak**: Target ≥ 98% for top seasonal items
- **Seasonal Sell-Through Rate**: % of seasonal inventory sold at full price (target: ≥ 75%)
- **Markdown Depth on Seasonal**: Average markdown % required to clear (lower is better; target: < 30%)
- **Lost Sales Rate**: Estimated revenue lost due to seasonal stockouts (target: < 2% of peak revenue)

### Forecasting Accuracy Benchmarks

| Level | Good | Acceptable | Needs Improvement |
|---|---|---|---|
| Monthly, category | < 8% MAPE | 8–15% | > 15% |
| Weekly, category | < 15% MAPE | 15–25% | > 25% |
| Weekly, SKU | < 25% MAPE | 25–40% | > 40% |
| Event weeks (holidays) | < 12% MAPE | 12–20% | > 20% |

## Examples

**Input**: "Analyze seasonal patterns for our Grilling & Outdoor Cooking subcategory. We have 3 years of weekly POS data for 85 SKUs across charcoal, lighter fluid, grilling sauces, and outdoor cooking accessories. Build a seasonal forecast for the next 12 months."

**Output**:
1. **Seasonal Profile**: Extreme seasonality (PT Ratio 5.2). Season runs Week 14–Week 38 (early April through late September). Peak: Week 26–28 (early July, around July 4th). Secondary peak: Week 22 (Memorial Day).
2. **Seasonal Indices**: Jan 0.18, Feb 0.22, Mar 0.55, Apr 1.05, May 1.65, Jun 1.85, Jul 2.10, Aug 1.45, Sep 0.90, Oct 0.45, Nov 0.25, Dec 0.15
3. **Forecast**: Total category forecast $14.2M (+3.8% vs. prior year driven by trend growth in premium grilling sauces). Peak month July: $2.98M. MAPE on backtested 2024 forecast: 11.4%.
4. **Calendar**: Pre-build starts Week 10 (early March) with initial orders for charcoal. Full seasonal set in-store by Week 14. First markdown Week 34 (late August) for accessories; charcoal clearance Week 36. Target 85% sell-through before Week 38.
5. **Weather risk**: If average June temperature is > 5°F above normal, add 8–12% to June-July forecast.

## Guidelines

- Minimum 2 full years of data for basic seasonal patterns; 3+ years for reliable indices and confidence intervals
- At the SKU level, aggregate very low-volume items to subcategory level before decomposition—noise overwhelms signal below ~50 units/week
- Always check for structural breaks: consumer behavior shifts (e.g., year-round demand for formerly seasonal products), new competitors, or category redefinition
- Movable holidays (Easter, Ramadan, Diwali, Chinese New Year) must be event-aligned, not calendar-aligned, for accurate seasonal indices
- Separate the promotional signal from the seasonal signal — a promotion during peak season inflates the seasonal index if not controlled
- Consider climate change trends for weather-sensitive categories; historical averages may understate warming trends
- For new products without history, inherit the seasonal profile from the most similar existing product or subcategory
- Cross-validate forecasts by comparing top-down (category level) with bottom-up (sum of SKU forecasts); reconcile differences
- Flag any year used in the seasonal average that had material disruptions (COVID, supply chain, weather extremes)
- Include prediction intervals in forecasts — point estimates alone are insufficient for inventory planning

## Validation Checklist

- [ ] Minimum 2 full years of clean, comparable data are used
- [ ] Decomposition method is appropriate (multiplicative vs. additive) and stated
- [ ] Anomalous periods are identified and handled (excluded or adjusted)
- [ ] Seasonal indices sum/average to approximately 1.0 over a full year
- [ ] Peak-to-trough ratio is calculated and seasonality is classified
- [ ] Holiday and event effects are separately identified and aligned
- [ ] Forecast accuracy is backtested against at least one holdout year
- [ ] MAPE and bias are within acceptable ranges for the aggregation level
- [ ] Operational recommendations include specific dates and inventory implications
- [ ] Weather and external driver sensitivities are addressed for weather-sensitive categories
