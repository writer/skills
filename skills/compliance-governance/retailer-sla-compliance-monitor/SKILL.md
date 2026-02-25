---
name: retailer-sla-compliance-monitor
description: Track and report on SLA adherence across CPG-retailer relationships including fill rates, on-time delivery, labeling compliance, and chargeback metrics. Use when monitoring operational SLAs, preparing compliance reports, analyzing chargeback trends, disputing penalties, or conducting supplier scorecard reviews.

metadata:
  display_name: "Retailer Sla Compliance Monitor"
  short_description: "Monitor CPG-retailer SLA compliance and chargebacks"
  default_prompt: "Check my retailer sla compliance for gaps risks and required fixes"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Retailer SLA Compliance Monitor

## Overview

Systematically track, analyze, and report on Service Level Agreement compliance across CPG-retailer relationships. This skill monitors operational KPIs (fill rate, OTIF, labeling, EDI accuracy), identifies compliance trends and root causes, quantifies financial impact of non-compliance (chargebacks and penalties), and produces actionable improvement plans aligned with retailer scorecard frameworks.

## When to Use

- Monthly/quarterly SLA compliance reporting
- Retailer supplier scorecard preparation
- Chargeback dispute analysis and remediation
- OTIF (On-Time In-Full) performance deep-dives
- Labeling and packaging compliance audits
- Pre-line-review compliance status preparation
- Corrective action plan development after compliance failures
- Benchmarking SLA performance across retailers

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| SLA requirements | Contractual KPIs and thresholds by retailer | SLA terms document |
| Performance data | Actual performance metrics (fill rate, OTIF, etc.) | Operational data |
| Chargeback history | Deduction detail by type, amount, date | Chargeback log |
| Order/shipment data | PO detail, shipment dates, quantities, ASN accuracy | Transaction data |
| Retailer scorecards | Published supplier performance reports | Scorecard documents |
| Root cause data | Known causes of compliance failures | Incident log or notes |
| Improvement actions | Active corrective actions and their status | Action tracker |

## Methodology

### Step 1: SLA Landscape Mapping

Document all active SLAs across retailer relationships:

**Major Retailer SLA Frameworks:**

| Retailer | Key Program | Critical KPIs | Penalty Structure |
|----------|------------|---------------|-------------------|
| Walmart | OTIF Scorecard | On-Time ≥87%, In-Full ≥95% | 3% of COGS fine per infraction |
| Target | Vendor Compliance | Ship window accuracy, PO fill rate | $ per occurrence by violation type |
| Kroger | Supplier Performance | Fill rate ≥98%, ASN accuracy ≥95% | Deductions per case short |
| Amazon | Vendor Central Metrics | PO fill rate, ASN accuracy, prep compliance | Chargebacks + potential suppression |
| Costco | Supplier Requirements | On-time delivery, quality standards | Non-compliance fees + potential delisting |

**SLA KPI Universe:**
```
Delivery Performance:
├── On-Time Delivery Rate (% of POs delivered within window)
├── In-Full Rate (% of PO units delivered complete)
├── OTIF Combined (On-Time AND In-Full — most stringent)
├── Must Arrive By Date (MABD) compliance
└── Appointment scheduling compliance

Order Accuracy:
├── PO Fill Rate (units shipped / units ordered)
├── ASN (Advance Ship Notice) accuracy and timeliness
├── Invoice accuracy (match to PO and ASN)
├── EDI compliance (transaction set accuracy)
└── Labeling/barcode accuracy

Quality & Compliance:
├── Product quality incidents (damage, defect rate)
├── Packaging compliance (case pack, pallet configuration)
├── Labeling compliance (GS1, retailer-specific requirements)
├── Recall response time
└── Documentation completeness (COA, SDS as required)
```

### Step 2: Performance Measurement and Trending

Calculate current compliance metrics against each SLA:

**OTIF Calculation (Walmart methodology):**
```
On-Time Rate:
  = Orders delivered within the delivery window / Total orders
  Window: Typically ±1 day of requested delivery date
  Threshold: ≥87% (as of current program)

In-Full Rate:
  = Cases delivered complete / Cases ordered
  Threshold: ≥95% (measured at case level)

OTIF Combined:
  = Orders that are BOTH on-time AND in-full / Total orders
  This is multiplicative — must meet BOTH criteria for each order
```

**Trend Analysis:**
- Calculate rolling 4-week and 13-week performance averages
- Identify trends: improving, stable, or deteriorating
- Flag any metric that has declined for 3+ consecutive periods
- Compare against prior year same period (seasonality adjustment)

**Performance vs. Threshold Heat Map:**

| KPI | Threshold | 4-Week Avg | 13-Week Avg | YoY Trend | Status |
|-----|-----------|-----------|-------------|-----------|--------|
| On-Time | ≥87% | XX.X% | XX.X% | +/-Xpp | 🟢/🟡/🔴 |
| In-Full | ≥95% | XX.X% | XX.X% | +/-Xpp | 🟢/🟡/🔴 |
| ASN Accuracy | ≥95% | XX.X% | XX.X% | +/-Xpp | 🟢/🟡/🔴 |

Status: 🟢 = ≥threshold; 🟡 = within 2pp of threshold; 🔴 = >2pp below threshold

### Step 3: Chargeback Analysis and Financial Impact

Quantify the financial impact of SLA non-compliance:

**Chargeback Taxonomy:**
| Category | Common Types | Typical Cost |
|----------|-------------|-------------|
| Delivery | Late/early shipment, missed appointment | $200-$500 per occurrence |
| Quantity | Short ship, over ship, unauthorized substitution | % of shorted value |
| Documentation | Missing/inaccurate ASN, BOL, packing slip | $100-$300 per occurrence |
| Labeling | Wrong UPC, missing GS1-128, pallet label errors | $100-$500 per occurrence |
| Packaging | Wrong case pack, pallet configuration, damage | $200-$1,000+ per occurrence |
| Compliance | OTIF fines (Walmart: 3% of COGS) | Variable by program |

**Financial Summary:**
```
Total Chargebacks (period):         $XXX,XXX
  Delivery-related:                 $XX,XXX  (XX%)
  Quantity-related:                 $XX,XXX  (XX%)
  Documentation-related:            $XX,XXX  (XX%)
  Labeling-related:                 $XX,XXX  (XX%)
  Packaging-related:                $XX,XXX  (XX%)
  Compliance fines:                 $XX,XXX  (XX%)

Chargebacks as % of Net Revenue:    X.X%
  Benchmark: <0.5% is healthy; >1.0% requires immediate action

Successfully disputed:              $XX,XXX  (XX% of total)
Dispute success rate:               XX%
Open disputes:                      $XX,XXX
```

### Step 4: Root Cause Analysis

Apply the Five Whys and Pareto analysis to compliance failures:

**Pareto Analysis:**
Rank failure modes by frequency and financial impact. Focus corrective actions on the top 3-5 root causes that account for 80% of chargebacks.

**Root Cause Categories:**
| Category | Examples | Resolution Owner |
|----------|---------|-----------------|
| Demand planning | Poor forecast accuracy → shorts | Demand Planning |
| Supply reliability | Supplier delays → late shipments | Procurement |
| Warehouse operations | Pick errors, wrong labels, late dispatch | Logistics/3PL |
| Transportation | Carrier delays, missed appointments | Logistics |
| System/EDI | ASN errors, PO processing failures | IT/Operations |
| Quality | Product defects, packaging failures | Quality Assurance |
| Capacity | Insufficient production to fill orders | Manufacturing |

**Root Cause Deep-Dive Template:**
```
Failure: [Specific failure description]
Impact: $XX,XXX in chargebacks; XX POs affected
Root Cause (5 Whys):
  Why 1: [Surface symptom]
  Why 2: [Contributing factor]
  Why 3: [Process failure]
  Why 4: [System/structural cause]
  Why 5: [Root cause]
Corrective Action: [Specific fix addressing root cause]
Preventive Action: [System/process change to prevent recurrence]
Owner: [Name/function]
Due Date: [Date]
Expected Impact: [Estimated chargeback reduction]
```

### Step 5: Dispute Management

Identify chargebacks eligible for dispute:

**Dispute Eligibility Criteria:**
| Dispute Basis | Evidence Required | Success Probability |
|--------------|-------------------|-------------------|
| POD (Proof of Delivery) contradicts | Signed BOL, carrier tracking | High (70-90%) |
| ASN was sent on time (system proof) | EDI transmission log with timestamp | High (70-85%) |
| Quantity discrepancy (retailer counting error) | BOL, packing slip, warehouse scan logs | Medium (50-70%) |
| Duplicate chargeback | Prior deduction for same event | High (80-95%) |
| Program interpretation disagreement | Contract language, program guide citation | Low-Medium (30-50%) |
| Force majeure event | Weather, carrier force majeure declaration | Low (20-40%) |

**Dispute ROI Analysis:**
```
Chargebacks eligible for dispute:     $XX,XXX
Expected success rate:                XX%
Expected recovery:                    $XX,XXX
Cost to dispute (labor + admin):      $X,XXX
Dispute ROI:                          X.Xx
Prioritize disputes with ROI > 3.0x
```

### Step 6: Corrective Action Plan

Develop a structured improvement plan:

```
Corrective Action Plan (CAP)
Target: Improve [KPI] from [current] to [target] within [timeline]

Initiative 1: [Name]
  Action: [Specific operational change]
  Owner: [Name/function]
  Timeline: [Start-End]
  Investment: $X
  Expected Impact: +Xpp on [KPI], -$XK in chargebacks
  Milestone 1: [Date — what should be true]
  Milestone 2: [Date — what should be true]

Initiative 2: [Name]
  [Same structure]

Monitoring:
  Weekly: [Leading indicators to track]
  Monthly: [SLA performance review]
  Quarterly: [Retailer scorecard review]
```

## Output Specification

```markdown
# SLA Compliance Report — [Retailer] [Period]

## Executive Summary
**Overall Compliance Status**: 🟢 Compliant / 🟡 At Risk / 🔴 Non-Compliant
**Financial Impact**: $XK in chargebacks (X.X% of revenue)
**Top Issue**: [Most impactful compliance failure]
**Trend**: Improving / Stable / Deteriorating

## Performance Dashboard

| KPI | Threshold | Current | Prior Period | Trend | Status |
|-----|-----------|---------|-------------|-------|--------|
| OTIF | ≥XX% | XX.X% | XX.X% | ↑/→/↓ | 🟢/🟡/🔴 |
| Fill Rate | ≥XX% | XX.X% | XX.X% | ↑/→/↓ | 🟢/🟡/🔴 |
| ASN Accuracy | ≥XX% | XX.X% | XX.X% | ↑/→/↓ | 🟢/🟡/🔴 |

## Chargeback Summary
| Category | Amount | % of Total | Trend | Top Root Cause |
|----------|--------|-----------|-------|---------------|
| Delivery | $XK | XX% | ↑/→/↓ | [Cause] |
| Quantity | $XK | XX% | ↑/→/↓ | [Cause] |

## Root Cause Analysis
[Pareto chart of top failure modes with 5-Why deep-dive on #1 issue]

## Dispute Status
- Open: $XK across X disputes
- Recovered YTD: $XK (XX% success rate)
- Pending: $XK

## Corrective Action Plan
[Active initiatives with status, owner, timeline, expected impact]

## Cross-Retailer Benchmark
[Performance comparison across retailers to identify systemic vs retailer-specific issues]
```

## Analysis Framework

**SLA Compliance Maturity Model:**
| Level | Description | Characteristics |
|-------|------------|----------------|
| 1 - Reactive | Fire-fighting compliance failures | No trend monitoring, high chargebacks |
| 2 - Measured | Tracking KPIs but not acting proactively | Dashboards exist, but root cause analysis is ad hoc |
| 3 - Managed | Root cause analysis drives improvement | Corrective actions active, chargeback declining |
| 4 - Optimized | Predictive monitoring prevents failures | Leading indicators trigger preemptive action |
| 5 - Best-in-Class | Compliance is a competitive advantage | Strategic supplier status, preferred partner programs |

## Example

**Input**: "Walmart OTIF last 4 weeks: 82%, 84%, 81%, 83%. Threshold is 87%. Total OTIF fines YTD: $420K. Main issue is late deliveries from our West Coast DC."

**Analysis excerpt**:
> "**Status: 🔴 NON-COMPLIANT.** Rolling 4-week OTIF average of 82.5% is 450bps below the 87% threshold, generating an estimated $35K/week in OTIF fines (3% of COGS on non-compliant POs). YTD fines of $420K represent 1.8% of Walmart net revenue — well above the 0.5% healthy benchmark. **Root cause**: Pareto analysis shows 68% of late deliveries originate from the West Coast DC, with carrier appointment scheduling as the #1 failure mode. Five-Why analysis traces this to a manual appointment booking process that doesn't account for Walmart's 30-minute delivery windows. **Corrective Action Plan**: (1) Immediate: Pre-book carrier appointments 72 hours in advance (vs current 24 hours), target: +3pp OTIF within 4 weeks. (2) Short-term: Implement automated appointment scheduling integration with Walmart's Luminate platform, target: +5pp within 8 weeks. (3) Medium-term: Evaluate adding a Southwest regional DC to reduce transit distance and variability. Expected full recovery to 87%+ within 12 weeks, preventing ~$180K in additional fines."

## Guidelines

- Always lead with financial impact — compliance metrics alone don't drive urgency
- Track at the most granular level possible (DC, carrier, SKU) to identify true root causes
- Benchmark performance across retailers to distinguish systemic vs retailer-specific issues
- Dispute eligible chargebacks aggressively — recovered deductions improve the bottom line
- Chargebacks as % of net revenue is the KPI that gets executive attention
- Corrective actions must have owners, dates, and measurable outcomes
- SLA requirements change — re-map the landscape annually

## Validation Checklist

- [ ] All active SLAs mapped with thresholds by retailer
- [ ] Performance metrics calculated with rolling averages (4-week, 13-week)
- [ ] Heat map shows status vs threshold for every KPI
- [ ] Chargebacks classified by taxonomy and quantified
- [ ] Chargebacks as % of net revenue calculated and benchmarked
- [ ] Root cause analysis applied with Pareto and Five Whys
- [ ] Dispute-eligible chargebacks identified with expected recovery
- [ ] Corrective action plan includes specific initiatives with owners and timelines
- [ ] Cross-retailer benchmark identifies systemic issues
- [ ] Trend analysis covers at least 13 weeks of historical data
