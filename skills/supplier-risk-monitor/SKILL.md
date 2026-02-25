---
name: Supplier Risk Monitor
description: Identify and score supplier reliability risks across delivery performance, quality, financial stability, geographic concentration, and capacity constraints, generating early-warning alerts and contingency recommendations.

metadata:
  display_name: "Supplier Risk Monitor"
  short_description: "Score and monitor supplier reliability and delivery risks"
  default_prompt: "Review my supplier risk and highlight top risks and next actions"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Supplier Risk Monitor

## Overview

This skill continuously monitors supplier performance and external risk signals to identify reliability threats before they disrupt the supply chain. It evaluates suppliers across five risk dimensions—delivery performance, quality, financial health, geographic/geopolitical exposure, and capacity constraints—producing a composite risk score with severity-tiered alerts. The skill also recommends mitigation actions including dual-sourcing, safety stock adjustments, and supplier development interventions.

## When to Use

- During monthly supplier performance reviews and quarterly business reviews (QBRs)
- When a supplier misses delivery commitments or quality defects increase
- Before contract renewals to assess whether to consolidate, diversify, or exit
- When geopolitical events, natural disasters, or economic downturns affect sourcing regions
- During new product development to evaluate prospective suppliers
- When procurement needs to justify dual-sourcing investment to leadership

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `supplier_profile` | Supplier ID, name, location, categories supplied, contract terms | Structured object |
| `delivery_history` | PO-level on-time and in-full delivery records (minimum 12 months) | Structured array |
| `quality_records` | Defect rates, rejections, customer complaints traced to supplier | Structured array |
| `financial_indicators` | Credit rating, payment terms, public financial data (if available) | Structured object |
| `geographic_data` | Manufacturing locations, shipping lanes, regional risk indices | Structured object |
| `spend_data` | Annual spend, spend concentration, share of category volume | Numeric |
| `alternative_suppliers` | Qualified alternates for same materials/products | Structured array |
| `external_signals` | News sentiment, regulatory changes, weather/disaster alerts | Structured object (optional) |

## Methodology

### Step 1: Delivery Performance Scoring (Weight: 30%)

Calculate core delivery KPIs:

```
OTIF_Rate = (POs_Delivered_On_Time_AND_In_Full / Total_POs) × 100
On_Time_Rate = (POs_Delivered_Within_Window / Total_POs) × 100
In_Full_Rate = (POs_Delivered_Complete / Total_POs) × 100
Lead_Time_Reliability = 1 - (σ_LT / μ_LT)  [coefficient of variation inverse]
```

Scoring thresholds:
| OTIF Rate | Score | Risk Level |
|-----------|-------|------------|
| ≥ 95% | 0-10 | Low |
| 85-94% | 11-40 | Moderate |
| 70-84% | 41-70 | High |
| < 70% | 71-100 | Critical |

Apply trend adjustment: if OTIF has declined >5 percentage points over 3 months, add +15 to risk score.

### Step 2: Quality Risk Scoring (Weight: 25%)

```
Defect_Rate = (Defective_Units / Total_Units_Received) × 1,000,000  [PPM]
Complaint_Rate = (Customer_Complaints_Traced_to_Supplier / Total_Units_Sold) × 100,000
Lot_Rejection_Rate = (Rejected_Lots / Total_Lots_Inspected) × 100
```

Scoring thresholds:
| Defect Rate (PPM) | Score | Risk Level |
|-------------------|-------|------------|
| < 500 | 0-10 | Low |
| 500-2,000 | 11-40 | Moderate |
| 2,000-10,000 | 41-70 | High |
| > 10,000 | 71-100 | Critical |

Escalation trigger: Any single lot failure on critical quality attribute = immediate high-risk flag regardless of average PPM.

### Step 3: Financial Stability Scoring (Weight: 20%)

Evaluate using available financial signals:

- **Credit rating** (Dun & Bradstreet, Moody's): Map to 0-100 risk scale
- **Payment behavior**: Are they requesting early payment or extended terms? (distress signal)
- **Revenue concentration**: If >30% of supplier's revenue depends on your business, mutual risk exists
- **Public signals**: Layoff announcements, executive departures, litigation, covenant violations

```
Financial_Risk_Score = Σ(weighted_indicator_scores)
```

If financial data is unavailable, use proxy indicators:
- Declining responsiveness to RFQs
- Reduced willingness to hold buffer inventory
- Requests for price increases outside contract escalation clauses

### Step 4: Geographic & Geopolitical Risk Scoring (Weight: 15%)

Assess concentration and exposure:

```
Geographic_Concentration = Σ(Spend_from_Region_i²) / (Total_Spend²)  [Herfindahl index]
```

Risk factors by region:
- Political stability index (World Bank Governance Indicators)
- Natural disaster exposure (earthquake, flood, hurricane zones)
- Trade policy risk (tariff changes, sanctions, export controls)
- Infrastructure reliability (port congestion, power grid stability)
- Single-point-of-failure: Is there only one manufacturing site? One port of exit?

### Step 5: Capacity & Concentration Risk (Weight: 10%)

```
Capacity_Utilization_Risk = Supplier_Utilization_Rate / 100  [higher = riskier]
Concentration_Risk = Your_Share_of_Supplier_Capacity  [>40% = elevated risk]
Single_Source_Flag = 1 if no qualified alternative exists, 0 otherwise
```

### Step 6: Composite Risk Score & Alert Generation

```
Composite_Score = 0.30 × Delivery_Score + 0.25 × Quality_Score + 0.20 × Financial_Score 
                + 0.15 × Geographic_Score + 0.10 × Capacity_Score
```

Alert tiers:
| Composite Score | Tier | Action |
|----------------|------|--------|
| 0-25 | Green | Standard monitoring |
| 26-50 | Yellow | Increased monitoring, supplier development plan |
| 51-75 | Orange | Active mitigation: qualify alternates, increase safety stock |
| 76-100 | Red | Contingency activation: shift volume, emergency sourcing |

## Output Specification

```yaml
supplier_risk_report:
  report_date: "2026-02-07"
  suppliers_monitored: 85
  risk_distribution:
    green: 52
    yellow: 21
    orange: 9
    red: 3
  critical_alerts:
    - supplier_id: "SUP-JADE-MFG"
      supplier_name: "Jade Manufacturing Co."
      composite_score: 78
      tier: "red"
      risk_dimensions:
        delivery: { score: 72, otif: "68%", trend: "declining" }
        quality: { score: 55, defect_ppm: 4200, trend: "stable" }
        financial: { score: 85, signal: "credit downgrade + payment term extension request" }
        geographic: { score: 82, factor: "single facility in high-risk flood zone" }
        capacity: { score: 65, utilization: "92%", your_share: "38%" }
      spend_at_risk: 4200000
      skus_affected: 23
      mitigation_actions:
        - "Activate qualified alternate SUP-PEAK-IND for top 8 SKUs (60% volume coverage)"
        - "Increase safety stock by 2 weeks for remaining 15 SKUs (cost: $185,000)"
        - "Request financial disclosure and site risk assessment within 30 days"
        - "Begin supplier qualification for SUP-ATLAS-MFG as long-term replacement"
      review_deadline: "2026-02-21"
```

## Analysis Framework

### Supplier Segmentation (Kraljic Matrix Application)

| Quadrant | Supply Risk | Profit Impact | Strategy |
|----------|-----------|---------------|----------|
| Strategic | High | High | Partnership, joint risk mitigation, dual-source critical items |
| Bottleneck | High | Low | Secure supply, find alternatives, increase inventory buffers |
| Leverage | Low | High | Competitive bidding, consolidate volume for price advantage |
| Non-Critical | Low | Low | Simplify, automate ordering, reduce transaction costs |

### Early Warning Indicators

Monitor these leading indicators (vs. lagging OTIF metrics):

1. **Order acknowledgment delays** — increasing response time signals capacity stress
2. **Partial shipments increasing** — supplier is rationing capacity across customers
3. **Quality inspection yield declining** — process instability before major failures
4. **Key person departures** — loss of institutional knowledge at supplier
5. **Raw material price spikes** — supplier margin pressure may lead to shortcuts
6. **Port/logistics disruptions** — track shipping lane congestion indices

## Examples

**Example 1 — Delivery Degradation Alert**
> "Supplier Jade Manufacturing OTIF has declined from 94% to 68% over 3 months. Root cause analysis indicates they lost a key sub-tier supplier and are rationing capacity. 23 SKUs worth $4.2M annual spend are affected. Immediate action: shift 60% volume to qualified alternate Peak Industries while requesting a formal corrective action plan with 90-day performance milestones."

**Example 2 — Geographic Risk Escalation**
> "Supplier Coastal Packaging operates a single facility in Houston, TX (Hurricane zone, FEMA risk tier 3). Hurricane season begins June 1. Current geographic risk score: 82. No qualified alternate for their specialty packaging. Recommended: (1) Build 6-week pre-season inventory buffer by May 1 (incremental cost: $340,000 carrying), (2) Begin qualification of Midwest Packaging Co. as backup source (estimated 16-week qualification timeline), (3) Request supplier's business continuity plan and insurance coverage documentation."

## Guidelines

1. Weight risk dimensions differently based on category criticality — for food safety-critical suppliers, increase quality weight to 35%
2. Always assess the alternative supplier landscape before declaring a risk critical — risk without alternatives is an emergency
3. Distinguish between chronic underperformance (systemic issue) and acute disruption (recoverable event)
4. Update financial risk indicators quarterly; delivery and quality indicators monthly
5. For sole-source suppliers, automatically elevate risk tier by one level (Yellow → Orange minimum)
6. Include tier-2 supplier risks when the primary supplier depends heavily on a single sub-supplier
7. Track corrective action plan (CAP) adherence — if milestones are missed, auto-escalate
8. Quantify the cost of dual-sourcing vs. the cost of disruption to support business case decisions
9. Integrate external signals (news, weather, trade policy) for proactive rather than reactive alerting

## Validation Checklist

- [ ] OTIF calculations use a consistent delivery window definition (e.g., ±2 days from requested date)
- [ ] Quality defect data includes both incoming inspection results and field returns traced to supplier
- [ ] Financial risk signals are verified against at least two independent sources
- [ ] Geographic risk indices are updated with current-year data (disaster maps, political risk ratings)
- [ ] Spend data includes all cost components (unit cost + freight + duties + quality cost)
- [ ] Alternative supplier list reflects current qualification status (qualified, in-progress, not started)
- [ ] Composite weights sum to 1.0 and reflect the organization's risk appetite
- [ ] Mitigation actions include estimated cost, timeline, and responsible owner
- [ ] Historical risk scores are trended to validate that the model detects real deterioration
- [ ] Report has been reviewed with procurement category managers before distribution
