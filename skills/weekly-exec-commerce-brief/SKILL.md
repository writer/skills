---
name: weekly-exec-commerce-brief
description: Auto-generate a weekly executive commerce brief with KPIs, trend analysis, and strategic commentary for CPG leadership. Use when the user needs a weekly business review, executive summary, commerce performance brief, or KPI dashboard narrative.

metadata:
  display_name: "Weekly Exec Commerce Brief"
  short_description: "Generate weekly CPG commerce executive briefs with KPIs"
  default_prompt: "Summarize my weekly exec commerce with key findings and next steps"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Weekly Executive Commerce Brief

## Overview

Generate a structured, board-ready weekly executive brief that synthesizes commerce performance data into strategic narratives. The brief covers revenue, margin, channel mix, inventory health, promotional effectiveness, and competitive positioning — formatted for C-suite consumption with minimal preparation time.

## When to Use

- Weekly business review preparation for VP/SVP/C-suite audiences
- Pre-meeting executive summary generation
- Cross-functional alignment briefs (Sales, Marketing, Finance, Supply Chain)
- Rapid commerce performance snapshots for investor or board pre-reads
- When stakeholders request a "state of the business" overview

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Revenue data | Weekly revenue by channel, brand, region | Table or CSV with period comparisons |
| Margin metrics | Gross margin %, contribution margin by SKU/brand | Numerical with YoY/WoW deltas |
| Channel performance | DTC, Amazon, Retail (by retailer), Wholesale | Revenue + units + growth rates |
| Inventory positions | Weeks of supply, stockout rate, fill rate | By SKU or category |
| Promotional calendar | Active promotions, planned launches | Dates, channels, expected lift |
| Competitive signals | Market share shifts, competitor actions | Optional — qualitative or syndicated data |

## Methodology

### Step 1: Data Intake and Normalization

Ingest all provided data and normalize to a common reporting period (ISO week). Reconcile any channel-level discrepancies by applying the following hierarchy: ERP data > retailer portal data > estimated data. Flag any data gaps explicitly.

### Step 2: KPI Computation

Calculate and present the following KPIs using a Balanced Scorecard framework:

**Financial Perspective:**
- Net Revenue (WoW, YoY, vs Plan)
- Gross Margin % and Contribution Margin $
- Trade Spend as % of Gross Revenue
- ROAS by channel (if media spend provided)

**Customer Perspective:**
- Customer Acquisition Cost (CAC) by channel
- Repeat Purchase Rate (DTC)
- Net Promoter Score trend (if available)

**Internal Process Perspective:**
- Order Fill Rate and OTIF %
- Inventory Weeks of Supply by top 20 SKUs
- Stockout incidents and estimated lost revenue

**Growth & Learning Perspective:**
- New SKU velocity (first 4 weeks indexed to benchmark)
- Channel expansion milestones
- Test-and-learn program status

### Step 3: Trend Analysis

Apply a 4-week rolling average to smooth volatility. Identify:
- Inflection points (>5% WoW change in any tier-1 KPI)
- Sustained trends (3+ consecutive weeks directional movement)
- Seasonal pattern deviations vs prior year
- Correlation flags (e.g., price increase followed by unit decline)

### Step 4: Executive Narrative Construction

Write each section using the SCR framework (Situation-Complication-Resolution):

1. **Situation**: State the metric and its current value
2. **Complication**: Identify what changed, why it matters, and the risk/opportunity
3. **Resolution**: Recommend an action or highlight a decision needed

### Step 5: Risk and Opportunity Callouts

Enumerate top 3 risks and top 3 opportunities with:
- Quantified impact range (low/mid/high scenarios)
- Owner/accountable function
- Recommended next step and timeline

### Step 6: Forward-Looking Indicators

Include a "Next Week Outlook" section with:
- Planned promotional activity and expected lift
- Known supply chain disruptions
- Competitor launch intelligence
- Macro/seasonal factors (weather, holidays, events)

## Output Specification

```markdown
# Weekly Commerce Brief — Week [XX], [YYYY]

## Executive Summary
[3-5 sentence overview: top-line performance, biggest win, biggest risk, key decision needed]

## Scorecard

| KPI | Actual | Plan | Variance | WoW Change | YoY Change | Status |
|-----|--------|------|----------|------------|------------|--------|
| Net Revenue | $X.XM | $X.XM | +X.X% | +X.X% | +X.X% | G/Y/R |
| Gross Margin % | XX.X% | XX.X% | ... | ... | ... | ... |

## Channel Performance
[Breakdown by DTC, Amazon, Retail, Wholesale with narrative]

## Promotional Effectiveness
[Active promo ROI, lift vs baseline, cannibalization notes]

## Inventory & Supply Chain Health
[Fill rate, stockouts, weeks of supply heatmap]

## Risks & Opportunities
### Top Risks
1. [Risk with quantified impact and owner]

### Top Opportunities
1. [Opportunity with quantified upside and next step]

## Decisions Needed
- [ ] [Decision with deadline and stakeholder]

## Next Week Outlook
[Forward-looking indicators and planned actions]
```

## Analysis Framework

Apply the **P&L Waterfall** to decompose revenue changes:
1. Volume effect (units x prior period ASP)
2. Price/mix effect (ASP change x current units)
3. Channel mix effect (shift between high/low-margin channels)
4. Promotional drag (discount depth x promoted volume)
5. New product contribution (incremental revenue from launches under 12 weeks old)

## Example

**Input**: "Revenue was $4.2M this week vs $4.0M plan. Amazon grew 12% WoW but DTC declined 3%. Two SKUs stocked out at Walmart. Trade spend was 18% of gross."

**Output narrative (Executive Summary excerpt)**:
> "Total commerce revenue of $4.2M exceeded plan by 5%, driven by Amazon momentum (+12% WoW) following Subscribe & Save enrollment gains. DTC softness (-3% WoW) reflects the conclusion of the January acquisition campaign; retargeting is live this week. Walmart stockouts on SKUs #1042 and #1087 represent ~$85K in estimated lost revenue; replenishment POs were expedited with a 2/14 delivery ETA. Trade spend at 18% of gross is 200bps above target — recommend pausing the BOGO on SKU #1042 post-restock to recapture margin."

## Guidelines

- Always lead with the "so what" — executives scan, not read
- Use traffic-light indicators (Green/Yellow/Red) with defined thresholds: Green = on/above plan; Yellow = 1-5% below plan; Red = >5% below plan
- Round currency to nearest $K or $M; percentages to one decimal
- Never present data without context (variance to plan, WoW, YoY)
- Attribute root causes — avoid "revenue was down" without explanation
- Keep the full brief under 2 pages when rendered
- Flag data quality issues transparently rather than hiding gaps

## Validation Checklist

- [ ] All tier-1 KPIs (Revenue, Margin, Fill Rate, CAC) are present with plan/prior comparisons
- [ ] Narrative uses SCR framework — no orphaned data points
- [ ] At least 3 risks and 3 opportunities with quantified impact
- [ ] Decisions section includes owners and deadlines
- [ ] Forward-looking section references next week's promotional calendar
- [ ] Data gaps are explicitly flagged with impact assessment
- [ ] Brief fits within 2-page executive format
- [ ] Traffic-light thresholds are consistently applied
