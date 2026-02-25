---
name: Returns Root Cause Analysis
description: Diagnose why product returns are happening by classifying return reasons, identifying systemic patterns across products, channels, and customer segments, quantifying financial impact, and recommending targeted reduction strategies.

metadata:
  display_name: "Returns Root Cause Analysis"
  short_description: "Diagnose root causes of product returns across channels"
  default_prompt: "Analyze my returns root cause and recommend clear next actions"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Returns Root Cause Analysis

## Overview

This skill performs systematic root cause analysis on product returns to identify actionable patterns and reduce return rates. It classifies returns into taxonomy-driven reason categories, applies statistical analysis to detect systemic issues versus random noise, quantifies financial impact including reverse logistics costs and lost margin, and recommends targeted interventions. The analysis spans product quality, content accuracy, fulfillment errors, customer behavior, and fraud, using adapted Ishikawa and Pareto frameworks.

## When to Use

- When overall return rate exceeds category benchmarks (e.g., >8% for apparel, >3% for grocery)
- During monthly/quarterly category reviews to identify return rate trends
- When a specific product or supplier shows spiking return rates
- Before scaling a new product or category to understand return risk profile
- When return processing costs are eroding profitability on specific items
- During vendor chargeback discussions to substantiate quality claims

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `return_transactions` | Return records with reason codes, timestamps, channel, customer | Structured array (6+ months) |
| `order_data` | Original orders linked to returns (product, price, channel, fulfillment method) | Structured array |
| `product_catalog` | Product attributes (category, size/fit info, images, description, supplier) | Structured object |
| `customer_reviews` | Product reviews and ratings mentioning returns or dissatisfaction | Text array |
| `quality_inspection` | Inspection results on returned items (condition, disposition) | Structured array |
| `customer_segments` | Customer return history, lifetime value, purchase frequency | Structured object |
| `competitor_benchmarks` | Industry return rate benchmarks by category (optional) | Numeric |

## Methodology

### Step 1: Return Rate Computation & Segmentation

Calculate return rates at multiple granularities:

```
Return_Rate = Units_Returned / Units_Sold × 100
Return_Rate_by_Revenue = Revenue_Returned / Gross_Revenue × 100
Net_Return_Rate = (Units_Returned - Exchanges) / Units_Sold × 100  [excludes size exchanges]
```

Segment return rates by:
- **Product**: SKU, product family, category, brand
- **Channel**: Online vs. in-store, marketplace vs. DTC
- **Fulfillment**: Ship-from-store, DC fulfillment, drop-ship, BOPIS
- **Customer**: New vs. returning, customer tier, geography
- **Time**: Day of week, seasonality, post-promotional periods

### Step 2: Reason Code Classification & Taxonomy

Map return reasons into a hierarchical taxonomy:

| L1 Category | L2 Sub-Category | Example Reason Codes | Typical Share |
|-------------|-----------------|---------------------|---------------|
| **Product Quality** | Defective/damaged | DOA, manufacturing defect, missing parts | 15-25% |
| | Performance | Doesn't work as expected, poor durability | 5-10% |
| **Fit & Sizing** | Too large/small | Size exchange needed, fit not as described | 20-35% (apparel) |
| | Style mismatch | Color different, style not as shown | 5-10% |
| **Content Accuracy** | Description mismatch | Product differs from listing, missing features | 10-15% |
| | Image mismatch | Actual appearance differs from photos | 5-8% |
| **Fulfillment Error** | Wrong item sent | Pick error, ship error | 3-5% |
| | Damaged in transit | Shipping damage, inadequate packaging | 5-10% |
| | Late delivery | Arrived after need-by date | 3-5% |
| **Customer Behavior** | Changed mind | No longer needed, found better alternative | 15-25% |
| | Bracketing | Ordered multiple sizes/styles intentionally | 5-15% (apparel) |
| **Fraud/Abuse** | Wardrobing | Used and returned (tags removed, worn) | 2-5% |
| | Return fraud | Empty box, counterfeit swap, receipt fraud | 1-3% |

### Step 3: Ishikawa (Fishbone) Root Cause Decomposition

For the top 3 return reason categories by volume, apply structured root cause analysis:

**Product Quality Returns — Fishbone Branches**
- **Materials**: Substandard raw materials, supplier quality escape
- **Manufacturing**: Process capability gaps, inadequate inspection
- **Design**: Design flaw, insufficient testing before launch
- **Packaging**: Inadequate protection during transit
- **Storage**: Warehouse damage, temperature excursion (perishables)

**Content Accuracy Returns — Fishbone Branches**
- **Photography**: Images don't represent actual color/size/texture
- **Copywriting**: Description overpromises or omits key details
- **Specifications**: Incorrect dimensions, weight, compatibility info
- **Translations**: Localization errors for international markets
- **Updates**: Product changed but listing not updated

**Fulfillment Error Returns — Fishbone Branches**
- **Pick accuracy**: Mis-picks from similar adjacent slots, barcode scan failures
- **Pack process**: Wrong item boxed, missing components
- **Ship process**: Mislabeling, wrong address, carrier damage
- **Inventory accuracy**: System shows stock but physical differs

### Step 4: Statistical Pattern Detection

Apply statistical tests to distinguish signal from noise:

```
Z_test = (Return_Rate_SKU - Return_Rate_Category) / √(p(1-p)/n)
If Z > 1.96 (95% confidence): SKU return rate is significantly above category average
```

Detect patterns:
- **Supplier correlation**: Do all products from supplier X have elevated defect returns?
- **Batch/lot correlation**: Is a specific production batch driving returns?
- **Temporal correlation**: Did return rate spike after a product change, listing update, or new fulfillment method?
- **Customer correlation**: Are specific customer cohorts returning at disproportionate rates?
- **Review-return correlation**: Does low review score predict high return rate? (leading indicator)

### Step 5: Financial Impact Quantification

Calculate the full cost of returns:

```
Gross_Return_Cost = Returned_Revenue  [top-line impact]
Net_Return_Cost = Lost_Margin + Reverse_Logistics + Processing_Labor + Restocking 
                + Markdown_on_Resale + Disposal_Cost + Customer_Service_Cost
```

Component estimates:
- **Reverse logistics**: $5-15 per return (shipping label + carrier pickup)
- **Processing labor**: $3-8 per return (receive, inspect, disposition)
- **Restocking**: $1-3 per return (repackage, re-slot, system update)
- **Markdown on resale**: 20-50% of original price for opened/used items
- **Disposal**: Full cost for unsalvageable returns (typically 5-15% of returns)

```
Cost_of_Returns_as_%_Revenue = Net_Return_Cost / Gross_Revenue × 100
Profit_Impact = Net_Return_Cost / Net_Profit × 100  [returns as % of profit erosion]
```

## Output Specification

```yaml
returns_analysis:
  period: "2025-08 to 2026-01"
  overall_return_rate: 11.2
  benchmark_return_rate: 8.0
  total_units_returned: 45600
  total_return_cost: 2850000
  return_rate_by_reason:
    product_quality: { rate: 2.8, pct_of_returns: 25, trend: "increasing" }
    fit_sizing: { rate: 3.4, pct_of_returns: 30, trend: "stable" }
    content_accuracy: { rate: 1.5, pct_of_returns: 13, trend: "decreasing" }
    fulfillment_error: { rate: 0.9, pct_of_returns: 8, trend: "stable" }
    customer_behavior: { rate: 2.0, pct_of_returns: 18, trend: "stable" }
    fraud_abuse: { rate: 0.6, pct_of_returns: 6, trend: "increasing" }
  top_problem_skus:
    - sku_id: "SKU-DRESS-4421"
      return_rate: 34.2
      category_benchmark: 12.0
      units_returned: 1240
      return_cost: 68200
      primary_reason: "Fit & Sizing (62% of returns)"
      root_cause: "Size chart inaccurate — runs 1.5 sizes small vs. industry standard"
      recommendation: "Update size chart, add fit notes ('runs small, order 1 size up'), implement virtual try-on"
      expected_rate_reduction: 12
  supplier_quality_issues:
    - supplier: "SUP-TEXTILEMAX"
      products_affected: 34
      avg_defect_return_rate: 6.8
      category_avg: 1.5
      root_cause: "Stitching quality failures concentrated in lots after machinery maintenance"
      recommendation: "Implement incoming quality inspection protocol, request SPC data from supplier"
  recommendations:
    - action: "Implement enhanced size guidance with fit predictor tool"
      target_reason: "Fit & Sizing"
      estimated_return_reduction: 4200
      estimated_annual_savings: 315000
    - action: "Tighten incoming quality inspection for SUP-TEXTILEMAX"
      target_reason: "Product Quality"
      estimated_return_reduction: 1800
      estimated_annual_savings: 198000
```

## Analysis Framework

### Return Rate Benchmarks by Category (E-Commerce)

| Category | Typical Return Rate | Best-in-Class | Primary Driver |
|----------|-------------------|---------------|----------------|
| Apparel | 20-30% | 12-15% | Fit & sizing |
| Footwear | 15-25% | 10-12% | Fit & comfort |
| Electronics | 8-12% | 4-6% | Functionality & expectations |
| Home & Garden | 8-12% | 5-7% | Size/appearance mismatch |
| Beauty & Personal Care | 3-5% | 1-2% | Allergic reaction, shade mismatch |
| Grocery / CPG | 1-3% | <1% | Damage, freshness |

### Fraud Detection Indicators

Flag for fraud investigation when:
- Customer has returned >50% of purchases in trailing 12 months
- Return condition doesn't match customer-stated reason
- Serial returner pattern: buy → use briefly → return before window closes
- Empty box or weight mismatch on returned package
- High-value item swapped with counterfeit or lower-value substitute

## Examples

**Example 1 — Sizing Root Cause**
> "Women's Dress SKU-4421 has a 34.2% return rate (category benchmark: 12%). 62% of returns cite 'too small' or 'sizing issue.' Customer reviews corroborate: 'runs at least 1.5 sizes small.' Root cause: size chart uses brand-specific sizing that differs from industry standard. Recommendation: (1) update product listing with 'runs small, order 1-2 sizes up' alert, (2) implement ML-based fit predictor using customer body measurements and purchase history, (3) add customer review size feedback to listing. Expected return rate reduction: 12 percentage points, saving $68K in return costs for this SKU alone."

**Example 2 — Supplier Quality Pattern**
> "34 products from supplier TextileMax show an average defect-related return rate of 6.8% vs. category average of 1.5%. Defects are concentrated in stitching failures. Lot analysis reveals defects spike in production lots immediately following scheduled machinery maintenance — suggesting improper machine calibration post-maintenance. Recommendation: (1) require supplier to provide first-article inspection results post-maintenance, (2) implement incoming quality sampling at DC (AQL 2.5, Level II), (3) issue vendor chargeback of $198K for quality-related return costs."

## Guidelines

1. Treat return reason codes with skepticism — customers often select the easiest option, not the true reason
2. Cross-reference stated reason with inspection condition to validate (e.g., "defective" claim but item is in perfect condition = likely buyer's remorse)
3. Analyze returns at the SKU level, not just category — a few high-return SKUs can skew category metrics
4. Separate first-time returns from repeat returns on the same order (bracketing behavior)
5. Calculate return rate on a cohort basis (returns from orders placed in period X) not just calendar returns
6. Weight financial impact by net margin, not revenue — a high-return but low-margin item may be less critical than a moderate-return high-margin item
7. Track return rate trajectory for new product launches — early weeks predict long-term rate
8. Include customer service contact data — returns preceded by a support call often indicate a solvable issue
9. Benchmark against competitors using industry reports, not just internal targets

## Validation Checklist

- [ ] Return reason codes are mapped to the standardized taxonomy (not raw free-text only)
- [ ] Return rate denominators use units sold in the corresponding origination period, not the return period
- [ ] Quality inspection data covers a representative sample of returns (minimum 20% inspected)
- [ ] Financial impact includes all cost components (reverse logistics, processing, markdown, disposal)
- [ ] Statistical significance is confirmed before flagging SKUs or suppliers as outliers
- [ ] Customer segment analysis complies with privacy regulations (no PII in outputs)
- [ ] Fraud detection flags are validated by the loss prevention team before action
- [ ] Supplier root causes are verified with supplier quality data, not just assumed from return patterns
- [ ] Recommendations include implementation cost and expected timeline to impact
- [ ] Analysis excludes warranty claims and recalls, which are tracked separately
