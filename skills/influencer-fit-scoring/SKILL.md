---
name: influencer-fit-scoring
description: >
  Scores and ranks influencers for brand partnership fit using a multi-dimensional framework
  covering audience alignment, engagement quality, brand safety, content relevance, and commercial
  viability for CPG and retail e-commerce campaigns. Use when evaluating potential influencer
  partners, building shortlists, or comparing candidates. Triggers on requests for influencer
  evaluation, creator partnerships, influencer scoring, KOL assessment, or ambassador selection.

metadata:
  display_name: "Influencer Fit Scoring"
  short_description: "Score influencer-brand partnership fit and alignment"
  default_prompt: "Score my influencer fit and explain what to improve"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Influencer Fit Scoring

## Overview

This skill applies a weighted scoring model to evaluate influencer-brand fit across six dimensions: audience alignment, engagement authenticity, content relevance, brand safety, commercial potential, and cost efficiency. It produces a ranked shortlist with composite scores, risk flags, and partnership recommendations tailored to CPG and retail e-commerce objectives.

## When to Use

- Evaluating a list of potential influencer partners for a campaign
- Building a tiered influencer roster (mega, macro, micro, nano)
- Comparing influencer candidates for a specific product launch or promotion
- Assessing existing influencer partnerships for renewal decisions
- Vetting influencers for brand safety and audience authenticity
- Structuring an influencer marketing program from scratch

## Required Inputs

| Input | Required | Description |
|---|---|---|
| Influencer Profiles | Yes | Name, handle, platform, follower count, niche/category |
| Brand / Product | Yes | Brand identity, product category, target positioning |
| Campaign Objective | Yes | Awareness, engagement, conversion, content creation, or loyalty |
| Target Audience | Yes | Demographics, interests, geography of desired reach |
| Budget Range | No | Total influencer budget to inform tier recommendations |
| Engagement Metrics | Recommended | Average likes, comments, shares, saves, video views |
| Audience Demographics | Recommended | Follower age, gender, location breakdown (from analytics tools) |
| Past Collaboration Data | No | Previous brand deals, competitor partnerships, performance history |
| Brand Safety Requirements | No | Categories, topics, or associations to avoid |

## Methodology

### Step 1 — Tier Classification

Categorize each influencer by reach tier:

| Tier | Follower Range | Typical CPG Use Case | Avg. Engagement Rate |
|---|---|---|---|
| Nano | 1K–10K | Authentic advocacy, niche communities | 4%–8% |
| Micro | 10K–100K | Targeted reach, high engagement, UGC | 2%–5% |
| Mid-Tier | 100K–500K | Balanced reach and engagement | 1.5%–3% |
| Macro | 500K–1M | Broad awareness, trend-setting | 1%–2% |
| Mega | 1M+ | Mass awareness, celebrity association | 0.5%–1.5% |

### Step 2 — Six-Dimension Scoring Model

Score each influencer on a 0–100 scale across six dimensions:

**Dimension 1: Audience Alignment (Weight: 25%)**
- Demographic overlap with target audience (age, gender, location)
- Interest category alignment (beauty, food, fitness, parenting, etc.)
- Audience income level proxy (based on content, brand affinities)
- Geographic concentration in target markets

```
Score = (Demo Match % × 0.4) + (Interest Match % × 0.3) + (Geo Match % × 0.3) × 100
```

**Dimension 2: Engagement Quality (Weight: 20%)**
- Engagement rate vs. tier benchmark (above/at/below average)
- Comment quality ratio: meaningful comments ÷ total comments
- Saves and shares ratio (high-intent signals)
- Follower growth trajectory (organic vs. spike patterns)

```
Score = (ER Percentile × 0.4) + (Comment Quality × 0.3) + (Save/Share Ratio × 0.2) + (Growth Health × 0.1) × 100
```

**Dimension 3: Content Relevance (Weight: 20%)**
- Content category alignment with brand/product
- Content production quality (visual, audio, editing)
- Content format match with campaign needs (Reels, long-form, Stories, etc.)
- Organic product integration naturalness (does the creator authentically use similar products?)

**Dimension 4: Brand Safety (Weight: 15%)**
- Controversial content history scan (political, offensive, polarizing)
- Competitor partnership conflicts (exclusivity concerns)
- FTC compliance history (proper #ad disclosure)
- Audience bot/fake follower percentage (flag if >15%)
- Content tone alignment with brand values

```
Score = 100 - (Controversy Penalty + Competitor Conflict Penalty + Compliance Risk Penalty + Bot Penalty)
```

**Dimension 5: Commercial Viability (Weight: 10%)**
- Previous sponsored content performance (vs. organic benchmarks)
- Product-tagging and link-in-bio utilization (shoppability)
- Track record of driving measurable actions (site traffic, sales, codes redeemed)
- Professional responsiveness and reliability (if data available)

**Dimension 6: Cost Efficiency (Weight: 10%)**
- Estimated CPM: (Influencer Fee ÷ Estimated Impressions) × 1,000
- Estimated CPE: Influencer Fee ÷ Estimated Engagements
- Benchmarked against tier and platform norms

| Platform | Tier | CPM Benchmark | CPE Benchmark |
|---|---|---|---|
| Instagram | Micro | $8–$15 | $0.15–$0.40 |
| Instagram | Macro | $12–$25 | $0.30–$0.80 |
| TikTok | Micro | $5–$12 | $0.05–$0.20 |
| TikTok | Macro | $10–$20 | $0.10–$0.35 |
| YouTube | Micro | $15–$30 | $0.25–$0.60 |
| YouTube | Macro | $20–$40 | $0.40–$1.00 |

### Step 3 — Composite Score Calculation

```
Composite Score = (Audience × 0.25) + (Engagement × 0.20) + (Content × 0.20) 
                + (Safety × 0.15) + (Commercial × 0.10) + (Cost × 0.10)
```

Adjust weights based on campaign objective:
- **Awareness campaigns**: Increase Audience Alignment to 30%, reduce Cost Efficiency to 5%
- **Conversion campaigns**: Increase Commercial Viability to 20%, reduce Content Relevance to 15%
- **Content creation campaigns**: Increase Content Relevance to 30%, reduce Audience Alignment to 15%

### Step 4 — Risk Flag Assessment

Flag influencers with critical risk indicators:

| Risk Flag | Trigger | Severity |
|---|---|---|
| 🔴 Bot Audience | >20% fake/bot followers | Disqualifying |
| 🔴 Competitor Exclusive | Active deal with direct competitor | Disqualifying |
| 🟡 Controversy History | Past 12 months controversial content | Review Required |
| 🟡 Engagement Anomaly | ER >3× tier average (potential manipulation) | Investigate |
| 🟡 Audience Mismatch | <40% demo overlap with target | Low Priority |
| 🟢 Rate Premium | CPM >2× benchmark | Negotiate |

### Step 5 — Shortlist & Tier Recommendation

Rank influencers by composite score and organize into partnership tiers:

- **Tier A — Anchor Partners** (Top 10%): Long-term ambassadorships, exclusive deals, co-creation
- **Tier B — Campaign Partners** (Top 11–30%): Campaign-specific collaborations, multi-post packages
- **Tier C — Amplification Partners** (Top 31–60%): One-off posts, product seeding, affiliate programs
- **Below Threshold** (Bottom 40%): Not recommended; document reasons

## Output Specification

1. **Scored Roster Table**: All influencers ranked by composite score with per-dimension breakdowns
2. **Risk Flag Summary**: Flagged influencers with risk type, severity, and recommended action
3. **Top 10 Shortlist**: Recommended partners with rationale and suggested partnership tier
4. **Partnership Structure Recommendations**: Deliverables, compensation model, and timeline per tier
5. **Budget Allocation**: Recommended spend distribution across influencer tiers
6. **Competitive Intelligence**: Notable competitor influencer partnerships observed

## Examples

**Input**: "Score these 15 food bloggers for our organic snack brand launch on Instagram. Target audience is health-conscious millennials in the US. Budget $50K."

**Output**: Ranked roster with composite scores. Top 5 micro-influencers (25K–80K followers) score highest due to strong audience alignment (82% health/wellness interest match) and above-average engagement. Two macro influencers flagged for competitor conflict (active partnerships with competing snack brands). Budget allocation: 60% micro (8 creators), 30% mid-tier (3 creators), 10% content licensing.

**Input**: "Evaluate these 8 TikTok creators for our Gen Z skincare line. We need high conversion potential."

**Output**: Scoring with Commercial Viability weighted at 20%. Top 3 creators identified with proven affiliate sales history, active TikTok Shop integration, and product-review content style. Two creators flagged for engagement anomalies suggesting potential bot activity. Recommended: 3-creator program with affiliate commission structure + flat fee hybrid.

## Guidelines

- Always verify engagement authenticity — inflated metrics waste budget and distort ROI
- Weight dimensions differently based on campaign objective; one size does not fit all
- For CPG, prioritize creators who show organic product usage in their content (not just paid posts)
- Consider content repurposing rights in partnership structure (whitelisting, paid amplification)
- Evaluate audience overlap between shortlisted creators to avoid redundant reach
- For regulated CPG categories (food, supplements), verify creator compliance with FTC/FDA guidelines
- Nano and micro creators typically deliver 3–5× the engagement rate of macro at lower CPMs
- Always check for audience geographic concentration — a US brand needs US-majority audiences
- Recommend a mix of tiers: anchors for credibility, micro for engagement and conversion

## Validation Checklist

- [ ] All six scoring dimensions are evaluated with documented rationale
- [ ] Composite scores use appropriate objective-based weight adjustments
- [ ] Risk flags are assigned and disqualifying risks result in removal
- [ ] Shortlist includes clear tier assignments with partnership recommendations
- [ ] Cost efficiency benchmarks are platform- and tier-specific
- [ ] Audience overlap analysis is performed across shortlisted creators
- [ ] Budget allocation is realistic and sums to provided budget
- [ ] FTC/compliance considerations are addressed for regulated categories
