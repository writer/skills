---
name: campaign-brief-generator
description: >
  Generates comprehensive, execution-ready marketing campaign briefs for CPG and retail e-commerce brands.
  Use when a user needs to plan a new campaign, product launch, seasonal promotion, or brand awareness initiative.
  Triggers on requests involving campaign planning, marketing briefs, promotional strategy, launch plans,
  or go-to-market documentation.

metadata:
  display_name: "Campaign Brief Generator"
  short_description: "Generate execution-ready marketing campaign briefs"
  default_prompt: "Summarize my execution ready marketing campaign with key findings and next steps"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Campaign Brief Generator

## Overview

This skill produces structured, agency-grade campaign briefs that align business objectives with audience insights, channel strategy, creative direction, and measurable KPIs. It synthesizes brand context, competitive landscape, and budget parameters into a single actionable document ready for execution by internal teams or external agencies.

## When to Use

- Planning a new product launch or line extension campaign
- Building seasonal or tentpole promotional strategies (BFCM, Back-to-School, Holiday)
- Creating always-on brand awareness or consideration campaigns
- Briefing creative agencies, media buyers, or internal marketing teams
- Structuring influencer or co-marketing partnership campaigns
- Documenting campaign rationale for executive stakeholder approval

## Required Inputs

| Input | Required | Description |
|---|---|---|
| Brand / Product | Yes | Brand name, product line, and key product attributes or USPs |
| Campaign Objective | Yes | Primary goal: awareness, consideration, conversion, retention, or reactivation |
| Target Audience | Yes | Demographics, psychographics, or existing customer segments |
| Budget Range | Yes | Total budget or budget tier (e.g., $50K–$100K) |
| Timeline | Yes | Campaign duration, key dates, and hard deadlines |
| Channels | No | Preferred or required channels; if omitted, skill recommends optimal mix |
| Competitive Context | No | Key competitors, market positioning, or share-of-voice benchmarks |
| Past Performance Data | No | Historical campaign metrics to inform KPI targets |
| Brand Guidelines | No | Tone, visual identity, mandatory legal/compliance copy |

## Methodology

### Step 1 — Objective Alignment & KPI Definition

Map the stated campaign objective to a measurable KPI framework:

| Objective | Primary KPI | Secondary KPIs | CPG Benchmark |
|---|---|---|---|
| Awareness | Reach / Impressions | Brand lift, SOV | CPM $5–$12 |
| Consideration | Engagement rate, CTR | Video completion rate, site traffic | CTR 0.8%–1.5% |
| Conversion | ROAS, CPA | Conversion rate, AOV | ROAS 3:1–5:1 |
| Retention | Repeat purchase rate | CLV delta, email open rate | RPR 25%–40% |
| Reactivation | Win-back rate | Reactivation CPA, reorder rate | Win-back 5%–12% |

Set SMART targets using industry benchmarks adjusted for brand maturity and category.

### Step 2 — Audience Strategy

Build a layered audience framework:

1. **Core Segment**: Highest-value existing customers (top 20% by LTV)
2. **Growth Segment**: Lookalike or adjacent audiences with high propensity
3. **Conquest Segment**: Competitor customers or category switchers
4. **Exclusion List**: Recent purchasers (suppress for efficiency), existing subscribers

For each segment, define:
- Demographics (age, gender, HHI, geography)
- Behavioral signals (purchase frequency, browse behavior, cart abandonment)
- Psychographic profile (values, lifestyle, media consumption)
- Estimated audience size and CPM implications

### Step 3 — Channel Mix Recommendation

Apply a **Reach–Engage–Convert** funnel framework:

| Funnel Stage | Channels | Budget Allocation | Role |
|---|---|---|---|
| Reach | Programmatic display, CTV/OTT, YouTube, TikTok | 30%–40% | Broad awareness, frequency building |
| Engage | Social (Meta, Pinterest), influencer, content marketing | 25%–35% | Consideration, social proof, education |
| Convert | Paid search, shopping ads, retargeting, email/SMS | 25%–35% | Direct response, cart recovery |
| Retain | Email, SMS, loyalty program, direct mail | 5%–10% | Post-purchase nurture, repeat purchase |

Adjust allocation based on objective weighting. Awareness campaigns shift budget upward; conversion campaigns shift downward.

### Step 4 — Creative Requirements

Specify creative deliverables per channel:

- **Hero Assets**: Key visual, hero video (15s/30s/60s), product photography
- **Social Variants**: Platform-native formats (Reels, Stories, Carousels, Pins)
- **Performance Creative**: Dynamic product ads, UGC-style testimonials, benefit-led statics
- **Retail Media**: Sponsored product images, brand store assets, A+ content
- **Email/SMS**: Subject lines, preview text, modular templates, SMS character-limited copy

Include messaging hierarchy: headline > subhead > body > CTA, with A/B test recommendations.

### Step 5 — Budget Allocation & Media Plan Skeleton

Produce a channel-level budget table:

```
Channel          | Budget    | Impressions Est. | KPI Target
-----------------+-----------+------------------+------------
Meta Ads         | $XX,XXX   | X.XM             | ROAS X.X
Google Search    | $XX,XXX   | X.XM             | CPA $XX
TikTok           | $XX,XXX   | X.XM             | CPV $0.XX
Email/SMS        | $X,XXX    | XK sends         | Open XX%
Influencer       | $XX,XXX   | X.XM reach       | EMV $XX,XXX
```

### Step 6 — Timeline & Milestones

Build a phased execution timeline:

1. **Pre-Launch (T-4 to T-2 weeks)**: Creative production, audience build, platform setup
2. **Teaser Phase (T-1 week)**: Organic seeding, email teasers, influencer previews
3. **Launch (Day 1–7)**: Full media activation, PR push, site merchandising
4. **Sustain (Week 2–N)**: Optimization, creative refresh, retargeting ramp
5. **Post-Campaign (Week N+1–2)**: Reporting, learnings documentation, audience archival

### Step 7 — Measurement Plan

Define the measurement framework:

- **Attribution Model**: Last-click, linear, or data-driven (recommend data-driven for multi-channel)
- **Brand Lift Study**: Pre/post survey for awareness campaigns (minimum $50K spend threshold)
- **Incrementality Test**: Geo-holdout or PSA test for ROAS validation
- **Reporting Cadence**: Daily dashboards, weekly optimization reviews, final campaign report

## Output Specification

Deliver a structured campaign brief document with these sections:

1. **Executive Summary** (3–5 sentences)
2. **Campaign Objective & KPIs** (table format)
3. **Target Audience Profiles** (per segment)
4. **Channel Strategy & Budget Allocation** (table + rationale)
5. **Creative Brief** (messaging, formats, deliverable list)
6. **Timeline & Milestones** (Gantt-style or phased list)
7. **Measurement & Reporting Plan**
8. **Risks & Mitigation** (top 3 risks with contingency actions)
9. **Appendix**: Competitive references, historical benchmarks, brand guidelines summary

## Examples

**Input**: "Create a campaign brief for our new organic baby food line launching on DTC and Amazon. Budget is $150K over 8 weeks. Target: millennial parents, ages 25–40, HHI $75K+."

**Output**: A complete brief including awareness-heavy channel mix (40% upper funnel), influencer strategy with mommy-blogger partnerships, Amazon Sponsored Brands + DSP allocation, creative specs for unboxing videos and ingredient-transparency messaging, and a phased timeline from teaser to sustain.

**Input**: "We need a Black Friday campaign brief for our skincare brand. $80K budget, 2-week window, conversion-focused."

**Output**: A conversion-oriented brief with 60% budget in lower funnel (retargeting, search, shopping), promotional offer ladder (early access → doorbuster → extended sale), email/SMS drip sequence specs, and hourly monitoring plan for peak days.

## Guidelines

- Always tie every channel recommendation back to the stated objective and audience
- Use conservative benchmark estimates; overpromising erodes trust
- Flag when budget is insufficient for stated objectives (e.g., awareness on <$25K)
- Include a minimum of two A/B testing recommendations in creative strategy
- Respect brand safety and compliance requirements (FTC, FDA for CPG claims)
- Recommend creative refresh cadence to combat ad fatigue (every 2–3 weeks)
- For multi-market campaigns, note localization requirements per market
- If past performance data is provided, use it to calibrate KPI targets ±15% from historical

## Validation Checklist

- [ ] Campaign objective is clearly stated with SMART KPI targets
- [ ] Audience segments are specific, sized, and actionable
- [ ] Channel mix aligns with funnel stage and objective weighting
- [ ] Budget allocation sums to total budget with no unaccounted spend
- [ ] Creative deliverables are specified per channel with format dimensions
- [ ] Timeline includes all phases with realistic production lead times
- [ ] Measurement plan includes both performance and brand metrics
- [ ] At least 3 risks identified with mitigation strategies
- [ ] Brief is self-contained and executable without additional context
