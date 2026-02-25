---
name: Store Performance Narratives
description: Auto-generate executive-ready store performance insights by synthesizing KPIs across sales, traffic, labor, and merchandising into coherent analytical narratives with root-cause commentary and recommended actions.

metadata:
  display_name: "Store Performance Narratives"
  short_description: "Generate executive-ready store performance narratives"
  default_prompt: "Summarize my store performance with key findings and next steps"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Store Performance Narratives

## Overview

This skill transforms raw store-level performance data into structured, executive-ready analytical narratives. Rather than presenting dashboards of disconnected metrics, it synthesizes KPIs across sales productivity, customer conversion, labor efficiency, and merchandising effectiveness into coherent stories that explain why performance shifted and what actions to take. The output mirrors the analytical rigor of a seasoned district manager's weekly store review.

## When to Use

- Weekly or monthly store performance review cycles
- District and regional roll-up reporting for field leadership
- Comparable-store (comp) performance deviation analysis
- Pre-visit briefing documents for store walks
- Board-level retail operations summaries
- Identifying underperforming locations requiring intervention plans
- Post-promotion or post-event performance recaps

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `store_id` | Unique store identifier or list of stores | String or array |
| `reporting_period` | Date range for analysis (current period) | ISO date range |
| `comparison_period` | Benchmark period (prior year, prior period, plan) | ISO date range or label |
| `sales_data` | Gross sales, net sales, returns, discounts by department | Tabular (CSV/JSON) |
| `traffic_data` | Door counts, unique visitors, bounce rate | Tabular |
| `transaction_data` | Transaction count, UPT, ATV | Tabular |
| `labor_data` | Scheduled hours, actual hours, payroll cost, headcount | Tabular |
| `inventory_data` | Sell-through rate, weeks of supply, stockout incidents | Tabular (optional) |
| `store_profile` | Square footage, format, region, cluster, age | Reference data |

## Methodology

### Step 1 - Metric Computation and Normalization

Calculate the core KPI set for each store and period:

- **Sales per Square Foot**: Net sales divided by selling square footage. Normalize by store format (flagship, mall, strip, outlet).
- **Conversion Rate**: Transactions divided by traffic. Flag stores below cluster median.
- **Units per Transaction (UPT)**: Total units sold divided by transaction count. Indicator of cross-sell and attach effectiveness.
- **Average Transaction Value (ATV)**: Net sales divided by transaction count. Decompose into UPT multiplied by average unit retail (AUR).
- **Labor Productivity**: Net sales divided by labor hours. Benchmark against plan and cluster average.
- **Sell-Through Rate**: Units sold divided by (beginning inventory plus receipts). By department or category.
- **Payroll-to-Sales Ratio**: Total payroll cost divided by net sales. Flag deviation greater than 200 bps from plan.

### Step 2 - Variance Decomposition

For every KPI deviation from benchmark, decompose into contributing factors:

1. **Traffic vs. Conversion**: Sales change equals (traffic change times base conversion times base ATV) plus (base traffic times conversion change times base ATV) plus interaction term.
2. **Price vs. Volume**: Revenue change equals (unit change times base AUR) plus (base units times AUR change).
3. **Mix Shift**: Identify category-level mix changes that moved blended AUR or margin.
4. **Calendar Effects**: Adjust for trading day differences, holiday shifts, weather disruptions.

### Step 3 - Contextual Enrichment

Layer external and operational context onto each variance:

- **Weather impact**: Match store zip to weather data; flag days with greater than 20% deviation from normal conditions.
- **Local events**: Identify nearby events, construction, competitor openings or closings.
- **Promotional calendar**: Map promotional windows, markdowns, loyalty events to traffic and conversion spikes or dips.
- **Staffing anomalies**: Correlate conversion drops with understaffing (actual hours below 90% of scheduled).
- **Inventory gaps**: Link stockout incidents to missed sales estimates using attachment rate models.

### Step 4 - Narrative Generation

Construct the narrative following this structure:

1. **Headline**: One-sentence performance summary with directional indicator (e.g., "Store 4521 posted a +3.2% comp driven by conversion gains despite a -5% traffic headwind").
2. **Key Drivers**: Top 3 factors explaining the variance, ordered by magnitude of impact.
3. **Risk Signals**: Metrics trending in a concerning direction even if current period is on-plan.
4. **Bright Spots**: Areas of outperformance to replicate across the cluster.
5. **Recommended Actions**: Specific, time-bound actions tied to the identified drivers.

### Step 5 - Aggregation for Roll-Up Reporting

When generating district or regional narratives:

- Weight store narratives by sales volume contribution.
- Identify systemic patterns (e.g., "7 of 12 stores saw conversion decline correlated with reduced floor coverage").
- Separate macro trends from store-specific issues.
- Rank stores by improvement opportunity (gap to cluster best-in-class multiplied by sales volume).

## Output Specification

Produce a structured narrative object per store containing:

- `store_id`: Store identifier
- `period`: Reporting period label
- `headline`: One-sentence performance summary
- `comp_sales_pct`: Comparable sales percentage change
- `kpi_summary`: Object containing each KPI with actual, benchmark, and variance percentage including sales_per_sqft, conversion_rate, upt, atv, labor_productivity
- `drivers`: Array of top contributing factors, each with factor name, impact in basis points, and contextual explanation
- `risk_signals`: Array of metrics with concerning trends, each with metric name, 4-week directional trend, and severity (low, medium, high)
- `actions`: Array of recommended actions, each with action description, responsible role, execution timeframe, and expected impact

## Analysis Framework

Apply the **Retail Performance Pyramid**:

- **Level 1 (Apex)**: Net Sales Growth - the ultimate output metric.
- **Level 2 (Traffic Layer)**: Traffic x Conversion - demand generation vs. in-store execution.
- **Level 3 (Basket Layer)**: UPT x AUR - cross-sell effectiveness and pricing power.
- **Level 4 (Levers)**: Marketing (awareness, campaigns, local marketing) | Experience (staffing, visual merchandising, service level) | Assortment (breadth, depth, newness) | Pricing (full-price sell-through, markdown cadence, promotional mix).

Each branch of the pyramid should be evaluated and referenced in the narrative when relevant. Walk down the pyramid from the apex to identify which lever is the primary driver of variance.

## Examples

**Example Input Context**: Store 4521, Week 48, Mall format, 8200 sqft

**Example Narrative Output**:

Store 4521 delivered a -2.1% comp, underperforming the district average of +0.8%. The shortfall was driven primarily by a 6.7% decline in conversion rate (18.2% vs. 19.5% PY), which offset gains in basket-building (+4.3% UPT) and ATV (+2.6%).

Key Drivers: (1) Traffic was flat (-0.3%), ruling out top-of-funnel issues. (2) Conversion dropped 130 bps versus the prior 4-week trend, coinciding with a 15% reduction in floor hours due to two associate call-outs on peak days (Thursday and Saturday). (3) Womens Apparel sell-through lagged at 38% vs. cluster benchmark of 52%, suggesting assortment misalignment.

Actions: (a) Backfill open associate position by Week 50 - estimated +80 bps conversion recovery. (b) Execute markdown acceleration on slow-moving Womens styles - target 48% sell-through by Week 51. (c) Schedule store walk with VM team to audit fixture flow and size representation.

## Guidelines

- Always lead with the "so what" - executives need the conclusion first, details second.
- Quantify every claim; avoid vague language like "slightly below" without a number attached.
- Distinguish between controllable factors (staffing, merchandising) and uncontrollable factors (weather, construction) explicitly.
- Use comp-store methodology: exclude stores open fewer than 14 months from comp base.
- Apply statistical significance thresholds - do not narrate noise. Flag variances below 2x standard deviation as "within normal range."
- Maintain consistent tone: objective, analytical, action-oriented. Avoid superlatives.
- For multi-store roll-ups, do not average percentages - use weighted calculations based on sales volume.
- Protect confidential data - never expose associate names, only reference role titles.
- When comparing stores, always control for format type, store age, and trade area demographics.

## Validation Checklist

- [ ] All KPIs calculated correctly with matching denominators (sqft is selling area, not total)
- [ ] Variance decomposition sums to total variance (no unexplained residual greater than 5%)
- [ ] Comparison period aligns correctly (PY week matches by day-of-week, not calendar date)
- [ ] Calendar adjustments applied for trading day differences
- [ ] Narrative claims are each supported by specific data points
- [ ] Actions are specific, measurable, and assigned to a responsible role
- [ ] Risk signals include trend direction over at least 4 periods
- [ ] Store profile context (format, age, cluster) factored into benchmarks
- [ ] Roll-up narratives use volume-weighted metrics, not simple averages
- [ ] No personally identifiable associate information included in output
