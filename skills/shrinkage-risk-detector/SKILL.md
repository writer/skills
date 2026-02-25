---
name: Shrinkage Risk Detector
description: Flag theft, fraud, and process-failure risk patterns by analyzing inventory variance, transaction anomalies, POS exceptions, and loss concentration to identify high-risk locations, products, and time windows with severity-scored alerts.

metadata:
  display_name: "Shrinkage Risk Detector"
  short_description: "Detect retail shrinkage risk from inventory and POS data"
  default_prompt: "Review my shrinkage risk and highlight top risks and next actions"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Shrinkage Risk Detector

## Overview

This skill detects and prioritizes shrinkage risks—inventory losses from theft (internal and external), fraud, administrative errors, and vendor/supplier fraud—by analyzing multi-source data for anomalous patterns. It computes shrinkage rates against benchmarks, applies statistical anomaly detection to identify outlier locations and products, correlates POS exception data with known theft indicators, and generates severity-scored alerts with investigation recommendations. The National Retail Federation estimates retail shrink at 1.4-1.6% of sales; reducing it by even 10-20 basis points drives significant margin improvement.

## When to Use

- During regular loss prevention reviews (weekly exception analysis, monthly location ranking)
- After physical inventory counts reveal unexplained variance
- When a specific store or DC shows spiking shrinkage rates
- During high-shrink periods (holidays, back-to-school, seasonal transitions)
- When onboarding new associates and monitoring for internal theft patterns
- Before deploying loss prevention resources to maximize ROI on LP staffing
- When implementing or evaluating shrinkage reduction technology (RFID, EAS, computer vision)

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `inventory_counts` | Perpetual vs. physical inventory variance by SKU-location | Structured array |
| `pos_transaction_data` | Transaction-level POS data with exceptions (voids, refunds, discounts, no-sales) | Structured array |
| `receiving_data` | Vendor shipment data vs. received quantities (ASN vs. actual) | Structured array |
| `employee_data` | Associate ID, shift schedule, register assignment, tenure | Structured object |
| `product_attributes` | Category, price, size, concealability, EAS tag status | Structured object |
| `location_profiles` | Store format, security features, LP staffing, geographic risk | Structured object |
| `historical_incidents` | Known theft/fraud cases with resolution and root cause | Structured array |
| `refund_data` | Refund transactions with reason codes, tender type, receipt status | Structured array |

## Methodology

### Step 1: Shrinkage Rate Computation & Benchmarking

Calculate shrinkage at multiple levels:

```
Shrinkage_Rate = (Book_Inventory - Physical_Inventory) / Net_Sales × 100
Known_Shrinkage = Identified_Theft + Identified_Admin_Errors + Identified_Vendor_Fraud
Unknown_Shrinkage = Total_Shrinkage - Known_Shrinkage
```

Industry benchmarks (NRF / ECR):

| Source | Typical Share | Rate (% of Sales) |
|--------|-------------|-------------------|
| External theft (shoplifting, ORC) | 35-40% | 0.50-0.65% |
| Internal theft (employee) | 25-30% | 0.35-0.50% |
| Administrative / process error | 15-20% | 0.20-0.30% |
| Vendor / supplier fraud | 5-10% | 0.07-0.15% |
| Unknown / unresolvable | 5-10% | 0.07-0.15% |

Segment shrinkage by:
- **Location**: Store, DC, zone within store/DC
- **Category**: Department, subcategory, brand
- **Time period**: Month, week, day-of-week, shift
- **Source**: External, internal, process, vendor

### Step 2: Statistical Anomaly Detection

Identify outlier locations, categories, and time periods:

```
Z_Score_Location = (Shrinkage_Rate_i - Mean_Shrinkage) / StdDev_Shrinkage
If Z > 2.0: Flag as statistically significant outlier
```

Apply moving average anomaly detection for trend shifts:
```
Expected_Shrinkage_t = EMA(Shrinkage, 12 weeks)
Anomaly_Score = |Actual_t - Expected_t| / MAD(Shrinkage, 12 weeks)
If Anomaly_Score > 3.0: Significant deviation from historical pattern
```

Correlation analysis to identify root causes:
- Shrinkage rate vs. LP staffing hours (inverse correlation expected)
- Shrinkage rate vs. employee turnover (positive correlation = training gap)
- Shrinkage rate vs. EAS compliance (inverse correlation = tagging effectiveness)
- Shrinkage rate vs. self-checkout usage % (positive correlation in some formats)

### Step 3: POS Exception Analysis (Internal Theft Indicators)

Monitor POS exception patterns that correlate with internal theft:

| Exception Type | Threshold (per associate per week) | Indicator |
|---------------|-----------------------------------|-----------|
| **Voids after tender** | > 3 | Sweethearting or skimming |
| **No-sale drawer opens** | > 10 | Cash theft, making change for personal transactions |
| **Manual price overrides** | > 5 | Unauthorized discounting for friends/family |
| **Refunds to cash** | > 5 (or >$200 total) | Fictitious return fraud |
| **Employee purchase %** | > 3% of shift sales | Excessive self-purchasing / pass-through |
| **Suspended transactions** | > 5 per shift | Bypassing items for retrieval after shift |
| **Line-item voids** | > 8% of items scanned | Selective scanning (skip-scanning) |

Composite internal risk score per associate:
```
Internal_Risk_Score = Σ(Exception_Type_i × Weight_i × (Actual_Rate / Threshold_Rate))
```

Weight by severity: refunds to cash (3.0), voids after tender (2.5), no-sales (2.0), overrides (1.5), suspended transactions (2.0)

### Step 4: External Theft Pattern Detection

Identify organized retail crime (ORC) and shoplifting patterns:

**High-risk product indicators** (concealability × desirability × value):
```
Product_Risk_Score = (Size_Concealability × 0.3) + (Resale_Value_Ratio × 0.3) 
                   + (Theft_History_Rate × 0.25) + (EAS_Coverage_Gap × 0.15)
```

Common ORC target categories: health & beauty, spirits, electronics accessories, premium food (meat, seafood, baby formula), over-the-counter pharmaceuticals, batteries, razor blades.

**Location-based external risk factors:**
- Proximity to highway on-ramp (fast getaway)
- Adjacent to fencing locations (pawn shops, flea markets)
- High crime rate ZIP code (FBI UCR data)
- Limited CCTV coverage areas within store
- Understaffed departments during high-traffic periods

**Temporal patterns:**
- Shift change periods (reduced surveillance continuity)
- Store opening/closing (reduced staffing)
- Holiday rush (distracted associates, crowded stores)
- First of month / paycheck dates (high traffic, diversion opportunities)

### Step 5: Vendor & Receiving Fraud Detection

Identify shrinkage originating in the supply chain:

```
Receiving_Variance = ASN_Quantity - Received_Quantity
Variance_Rate = |Receiving_Variance| / ASN_Quantity × 100
```

Flag when:
- Consistent short shipments from a specific vendor (>2% variance, >3 occurrences)
- Receiving associate accepts without count verification (process compliance gap)
- High-value substitutions (higher-cost item on ASN, lower-cost item delivered)
- Phantom shipments (PO received in system but no physical delivery confirmed)
- Trailer seal integrity issues (broken seals, mismatched seal numbers)

### Step 6: Risk Scoring & Alert Prioritization

Compute composite shrinkage risk score per location (0-100):

```
Location_Risk_Score = w1 × Shrinkage_Rate_Severity + w2 × Trend_Severity 
                    + w3 × POS_Exception_Score + w4 × External_Risk_Score 
                    + w5 × Receiving_Variance_Score
```

Weights: `w1=0.30, w2=0.20, w3=0.20, w4=0.15, w5=0.15`

Alert tiers:

| Score | Tier | Response |
|-------|------|----------|
| 0-25 | Low | Standard monitoring cadence |
| 26-50 | Moderate | Increased exception review frequency, targeted audits |
| 51-75 | High | LP investigation, covert surveillance, operational review |
| 76-100 | Critical | Immediate LP deployment, potential law enforcement engagement |

## Output Specification

```yaml
shrinkage_risk_report:
  report_period: "2026-01"
  portfolio_summary:
    total_locations: 320
    total_shrinkage_value: 4200000
    shrinkage_rate_pct: 1.52
    benchmark_pct: 1.40
    yoy_trend: "+0.12 pp"
    estimated_recoverable: 840000
  risk_distribution:
    low: 198
    moderate: 78
    high: 34
    critical: 10
  critical_alerts:
    - alert_id: "SHR-C-001"
      location_id: "STORE-1447"
      risk_score: 88
      shrinkage_rate: 3.8
      company_avg: 1.52
      shrinkage_value: 142000
      primary_indicators:
        - type: "POS Exceptions"
          detail: "Associate #A2241: 18 voids after tender in January (threshold: 12), $4,200 in cash refunds without receipts"
          confidence: "high"
        - type: "Inventory Variance"
          detail: "Health & beauty category variance 340% above store average, concentrated in premium skincare"
          confidence: "high"
        - type: "External Risk"
          detail: "3 ORC incidents reported at nearby stores in same chain; known fencing operation 2 miles away"
          confidence: "medium"
      recommended_actions:
        - "Deploy LP investigator for covert observation of Associate #A2241 (2-week assignment)"
        - "Implement locked case for premium skincare (top 15 high-theft SKUs)"
        - "Install additional CCTV coverage at health & beauty end-caps"
        - "Conduct exception-based interview with associate if covert confirms patterns"
      estimated_recovery: 85000
      investigation_priority: "immediate"
```

## Analysis Framework

### Shrinkage Root Cause Decision Tree

```
High Shrinkage Detected
├── Known vs. Unknown?
│   ├── Known Source → Address directly (prosecution, process fix, vendor chargeback)
│   └── Unknown Source → Investigate further
│       ├── Concentrated in specific categories?
│       │   ├── Yes → High-theft product profile? → Likely external theft → EAS/locked case
│       │   └── No → Systemic issue → Process audit, receiving review
│       ├── Concentrated in specific locations?
│       │   ├── Yes → Check POS exceptions → Internal theft indicators? → LP investigation
│       │   └── No → Company-wide process issue → Policy review
│       ├── Concentrated in specific time periods?
│       │   ├── Yes → Correlate with staffing → Coverage gap? → Schedule optimization
│       │   └── No → Consistent pattern → Structural vulnerability
│       └── Correlated with specific associates?
│           ├── Yes → High POS exceptions → Exception-based investigation
│           └── No → External or process-driven
```

### Loss Prevention ROI Framework

Calculate return on LP investment:
```
LP_ROI = (Shrinkage_Reduction_Value - LP_Investment_Cost) / LP_Investment_Cost × 100
```

Typical ROI by intervention:
| Intervention | Cost | Expected Shrinkage Reduction | Typical ROI |
|-------------|------|----------------------------|-------------|
| Exception-based reporting software | $50-100K/year | 10-15% of internal theft | 300-500% |
| EAS tagging (source or in-store) | $0.05-0.15/item | 20-30% of external theft | 200-400% |
| RFID inventory accuracy | $0.03-0.10/item | 15-25% (process error reduction) | 150-300% |
| LP officer deployment | $60-80K/year/officer | $200-400K recoveries per officer | 200-500% |
| CCTV / computer vision | $20-50K per store | 10-20% of external theft | 100-250% |

## Examples

**Example 1 — Internal Theft Pattern**
> "Store 1447 Associate #A2241 flagged with risk score 88. January exceptions: 18 voids after tender (3× threshold), $4,200 in cash refunds without receipts (2.1× threshold), and 14 manual price overrides. These exceptions cluster during closing shifts when supervision is minimal. Concurrent inventory pattern: premium skincare shrinkage is 340% above store average. Hypothesis: associate is processing fictitious refunds and/or sweethearting products to accomplices. Recommendation: 2-week covert LP observation, followed by exception-based interview. Estimated recoverable loss: $85,000 annualized."

**Example 2 — Organized Retail Crime Alert**
> "Cluster of 5 stores in the metro region showing simultaneous spikes in razor blade, baby formula, and premium liquor shrinkage (+45% MoM). Pattern matches known ORC sweep tactics: rapid clearance of high-value, easily fenced merchandise across multiple locations in a short window. Local LP intelligence confirms a new fencing operation opened within the trade area. Recommendation: (1) Implement keeper/locked case on top 20 ORC-target SKUs across all 5 stores, (2) Coordinate with regional organized crime task force, (3) Deploy plain-clothes LP for 4-week deterrence sweep, (4) Enhance entrance/exit CCTV with facial recognition capable systems."

## Guidelines

1. Always distinguish between high-shrinkage (actual loss) and high-variance (may be counting/process error) — investigate before concluding theft
2. POS exception analysis requires minimum 4 weeks of data per associate to avoid false positives from training periods
3. Never share individual associate risk scores outside of LP and HR — these are investigative leads, not accusations
4. Weight recent incidents more heavily than historical — a reformed pattern should not permanently flag a location
5. Account for legitimate reasons for exceptions — some departments (e.g., produce, deli) have inherently higher void rates
6. Separate markdown/damage write-offs from true shrinkage in calculations
7. For DC/warehouse shrinkage, focus on receiving accuracy, cycle count variance, and shipping accuracy
8. Cross-reference shrinkage patterns with employee schedules — correlation with specific shifts is a strong indicator
9. Use physical inventory count results to calibrate perpetual inventory accuracy — trust physical over system data
10. Include opportunity cost in shrinkage impact: a $10 stolen item costs ~$30 in lost revenue to recover margin (at 33% margin)

## Validation Checklist

- [ ] Shrinkage rate denominator uses net sales (consistent with industry standard)
- [ ] Physical inventory counts are audited for accuracy (double-count procedures, blind counts)
- [ ] POS exception thresholds are calibrated to the specific store format and department
- [ ] Employee data is handled in compliance with HR policies and applicable labor laws
- [ ] External risk factors use current crime data (updated at least annually)
- [ ] Vendor fraud detection accounts for legitimate receiving variances (damage, partial shipments)
- [ ] Alert deduplication prevents repeated alerts for known, actively investigated issues
- [ ] Financial impact calculations use retail value (not cost) for revenue loss perspective
- [ ] Recommended actions are proportionate to the evidence level and risk score
- [ ] All investigation recommendations comply with company policy and applicable laws (surveillance, interviews)
- [ ] Report access is restricted to authorized LP, HR, and store management personnel
