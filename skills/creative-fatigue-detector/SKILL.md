---
name: creative-fatigue-detector
description: >
  Analyzes ad performance data to detect creative fatigue signals and recommends refresh strategies
  for CPG and retail e-commerce campaigns. Use when a user observes declining ad performance,
  increasing CPAs, or needs to establish creative refresh cadences. Triggers on requests about
  ad fatigue, declining ROAS, creative refresh timing, or performance degradation analysis.

metadata:
  display_name: "Creative Fatigue Detector"
  short_description: "Detect ad creative fatigue and recommend refresh timing"
  default_prompt: "Review my creative fatigue and highlight top risks and next actions"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Creative Fatigue Detector

## Overview

This skill diagnoses creative fatigue by analyzing performance trend data against statistical thresholds, identifies which specific creatives are fatigued versus underperforming for other reasons, and prescribes targeted refresh strategies. It distinguishes between true creative fatigue, audience saturation, seasonal effects, and market-level shifts to prevent premature creative kills.

## When to Use

- Ad performance metrics are declining over consecutive days or weeks
- CPA is rising while CTR and engagement are dropping simultaneously
- Frequency metrics are exceeding platform-recommended thresholds
- Planning proactive creative refresh schedules for evergreen campaigns
- Auditing a creative library to identify stale vs. still-performing assets
- Investigating whether poor performance is creative-driven or systemic

## Required Inputs

| Input | Required | Description |
|---|---|---|
| Performance Data | Yes | Daily or weekly metrics per creative: impressions, clicks, CTR, CPA, ROAS, conversions |
| Time Range | Yes | Minimum 14 days of data; 30–90 days preferred for trend analysis |
| Creative Identifiers | Yes | Creative/ad IDs, names, or descriptions to differentiate assets |
| Frequency Data | Recommended | Average frequency per creative or ad set over the analysis period |
| Platform | Recommended | Meta, Google, TikTok, etc. — fatigue thresholds vary by platform |
| Audience Size | No | Estimated audience pool size to calculate saturation metrics |
| Benchmark KPIs | No | Historical or target benchmarks for comparison |

## Methodology

### Step 1 — Data Normalization & Baseline Establishment

1. Calculate the **baseline performance window**: first 7 days of delivery (or first 25% of data)
2. Compute baseline averages for CTR, CPA, ROAS, conversion rate, and CPM
3. Normalize data for spend fluctuations — use rate metrics (CTR, CPA) not absolute volumes
4. Flag and exclude anomalous days (>2σ deviations from mean due to external factors)
5. Adjust for day-of-week effects using 7-day rolling averages

### Step 2 — Fatigue Signal Detection

Apply the following diagnostic tests to each creative:

**Primary Fatigue Indicators** (must show 2+ to confirm fatigue):

| Metric | Fatigue Signal | Threshold |
|---|---|---|
| CTR | Sustained decline | >20% drop from baseline over 7+ days |
| CPA | Sustained increase | >25% increase from baseline over 7+ days |
| Frequency | Over-saturation | >3.0 (prospecting) or >8.0 (retargeting) on Meta |
| CPM | Auction competitiveness drop | >30% increase without seasonal cause |
| Conversion Rate | Declining efficiency | >15% drop from baseline, sustained 5+ days |

**Secondary Fatigue Indicators** (supporting evidence):

| Metric | Signal | Threshold |
|---|---|---|
| Video completion rate | Attention decline | >25% drop in ThruPlay or 75% VCR |
| Engagement rate | Audience disinterest | >30% drop in likes, comments, shares |
| Negative feedback | Active rejection | >2× increase in "Hide Ad" or negative reactions |
| Impression share decay | Algorithmic deprioritization | >20% drop in delivery share within ad set |

### Step 3 — Fatigue Classification

Classify each creative into a fatigue category:

| Category | Criteria | Recommended Action |
|---|---|---|
| **Healthy** | All metrics within ±10% of baseline | Continue running; monitor weekly |
| **Early Fatigue** | 1 primary indicator triggered | Alert; prepare replacement creative |
| **Confirmed Fatigue** | 2+ primary indicators triggered | Reduce spend; begin creative swap |
| **Exhausted** | 3+ primary + secondary indicators | Pause immediately; replace creative |
| **Audience Saturated** | High frequency + stable CTR but rising CPM | Expand audience; creative may be fine |
| **Systemic Decline** | All creatives declining uniformly | Investigate external factors, not creative |

### Step 4 — Root Cause Differentiation

Distinguish creative fatigue from confounding factors:

- **Seasonal Effects**: Compare YoY data; check industry CPM indices (Q4 CPMs rise 30–60%)
- **Audience Exhaustion**: If frequency is high but creative is fresh, the audience pool is too small
- **Market Saturation**: If all competitors show similar trends (use auction insights if available)
- **Landing Page Issues**: If CTR is stable but CPA rises, investigate post-click experience
- **Algorithm Changes**: If CPM spikes without frequency change, suspect platform auction dynamics
- **Budget Scaling**: If budget increased >20% recently, expect efficiency decline (not fatigue)

### Step 5 — Fatigue Velocity Scoring

Calculate the rate of performance decay to prioritize action:

```
Fatigue Velocity = (Baseline CPA - Current CPA) / (Baseline CPA × Days Since Baseline)

Interpretation:
  FV < 0.5%/day  → Slow burn; 2-3 weeks before critical
  FV 0.5-1.0%/day → Moderate; prepare refresh within 1-2 weeks
  FV > 1.0%/day  → Rapid; refresh immediately
```

Estimate **Days to Exhaustion** (DTE):

```
DTE = (CPA Ceiling - Current CPA) / (Daily CPA Increase Rate)

Where CPA Ceiling = Baseline CPA × 1.5 (or max acceptable CPA)
```

### Step 6 — Refresh Strategy Prescription

Based on fatigue classification, recommend specific actions:

**For Early Fatigue**:
- Introduce 2–3 new variants of the same winning angle
- Adjust visual treatment (color, layout, talent) while keeping message
- Test new format (static → video, or carousel → Reel)

**For Confirmed Fatigue**:
- Launch entirely new messaging angle
- Rotate to different creative framework (AIDA → PAS)
- Introduce new audience segments to reduce frequency pressure
- Test UGC or creator content if currently using branded

**For Exhausted Creatives**:
- Full creative replacement — new angle, format, and visual treatment
- Archive learnings: document what worked in baseline period
- Consider concept evolution rather than complete departure from brand

**Proactive Refresh Cadence** (CPG/retail benchmarks):
- Prospecting: Refresh every 2–3 weeks
- Retargeting: Refresh every 1–2 weeks (smaller audiences fatigue faster)
- Seasonal campaigns: Build 3× creative volume upfront; rotate weekly
- Always-on: Maintain 5–8 active variants per ad set; rotate bottom 2 every 2 weeks

## Output Specification

1. **Fatigue Dashboard**: Per-creative summary with classification, fatigue velocity, and DTE
2. **Trend Visualizations**: Described data visualization specs for CTR, CPA, and frequency over time
3. **Root Cause Analysis**: For each fatigued creative, the diagnosed cause and confidence level
4. **Action Plan**: Prioritized list of creatives to pause, refresh, or continue with timelines
5. **Refresh Recommendations**: Specific creative direction for replacement assets
6. **Monitoring Cadence**: Ongoing fatigue-check schedule and alert thresholds

## Examples

**Input**: "Our Meta prospecting campaign has 6 creatives running for 4 weeks. CTR dropped from 1.8% to 1.1%, CPA went from $18 to $28. Frequency is at 4.2. Help diagnose."

**Output**: Classification of each creative into fatigue categories; identification that 3 creatives are exhausted (FV >1.2%/day), 2 are confirmed fatigued, and 1 remains healthy. Root cause: audience over-saturation (frequency 4.2) compounding creative fatigue. Action plan: pause 3 exhausted creatives immediately, expand lookalike audience from 1% to 3%, introduce 4 new variants with UGC angle, implement weekly fatigue monitoring.

**Input**: "All our ads across Google and Meta are showing rising CPAs over the last 10 days. Is it creative fatigue or something else?"

**Output**: Systemic decline diagnosis — uniform CPA increase across platforms and creatives suggests external factor. Analysis points to Q4 CPM inflation (industry-wide 35% CPM increase in this period). Recommendation: hold creative constant, adjust CPA targets for seasonal benchmarks, increase bids, and revisit in January when auction pressure normalizes.

## Guidelines

- Never diagnose fatigue with fewer than 14 days of data — early fluctuations are noise
- Always check frequency before blaming the creative; high frequency is often the root cause
- Distinguish between absolute metric declines and relative (rate-based) declines
- Account for spend changes — doubling budget will naturally raise CPA 10–20%
- For small-audience retargeting, fatigue thresholds should be more aggressive (lower frequency caps)
- Recommend creative diversification, not just replacement — maintain learnings from winners
- Platform-specific thresholds matter: TikTok creatives fatigue faster (7–14 days) than Meta (14–28 days)
- For CPG, seasonal purchase cycles affect conversion rates independent of creative quality

## Validation Checklist

- [ ] Minimum 14 days of data analyzed per creative
- [ ] Baseline period is clearly defined and reasonable
- [ ] All primary and secondary fatigue indicators are evaluated
- [ ] Each creative receives a fatigue classification with supporting evidence
- [ ] Root cause analysis differentiates creative fatigue from confounding factors
- [ ] Fatigue velocity and DTE are calculated for actionable prioritization
- [ ] Refresh recommendations are specific and actionable (not generic)
- [ ] Monitoring cadence is established for ongoing fatigue prevention
