---
name: Voice of Customer Summarizer
description: Summarize customer feedback at scale across surveys, reviews, social media, and support interactions using NLP-driven theme extraction to produce actionable executive summaries with quantified sentiment trends.

metadata:
  display_name: "Voice Of Customer Summarizer"
  short_description: "Summarize customer feedback across all channels at scale"
  default_prompt: "Help me with voice of customer summarizer and give clear next steps"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Voice of Customer Summarizer

## Overview

This skill processes large volumes of unstructured customer feedback from multiple sources — surveys, product reviews, social media mentions, contact center transcripts, chat logs, and community forums — and distills them into structured, quantified summaries that surface the most important themes, sentiment shifts, and emerging issues. It replaces hours of manual review with systematic, reproducible analysis that ensures no critical signal is lost in the noise.

## When to Use

- Monthly or quarterly Voice of Customer (VoC) reporting cycles
- After product launches, campaigns, or operational changes to assess customer reaction
- When leadership asks "what are customers saying?" and needs a data-backed answer
- To monitor emerging issues before they become full-blown crises
- When comparing customer sentiment across brands, product lines, or regions
- To feed customer insights into product development, merchandising, or service design teams
- When consolidating feedback from multiple channels into a unified view

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `survey_verbatims` | Open-ended responses from CSAT, NPS, and post-transaction surveys | Text with metadata |
| `product_reviews` | Customer reviews from owned site, marketplace platforms (Amazon, etc.) | Text with star rating |
| `social_mentions` | Brand mentions from Twitter/X, Instagram, Facebook, Reddit, TikTok | Text with engagement metrics |
| `support_transcripts` | Contact center call transcripts and chat logs | Text with resolution data |
| `community_posts` | Customer forum or community board posts | Text with thread metadata |
| `source_metadata` | Channel, timestamp, customer segment, product/category reference for each piece of feedback | Structured metadata |
| `prior_period_summary` | Previous VoC summary for trend comparison | Prior output (optional) |

## Methodology

### Step 1 — Data Ingestion and Normalization

Prepare feedback from all sources for unified analysis:

1. **Text Cleaning**: Remove HTML tags, URLs, excessive punctuation, and bot-generated content. Preserve emojis as sentiment signals (map to sentiment labels).
2. **Language Detection**: Identify language; translate non-primary-language feedback for inclusion or analyze separately if volume warrants.
3. **Deduplication**: Identify cross-posted feedback (same customer posting the same review on multiple platforms) using fuzzy text matching.
4. **Source Weighting**: Assign analytical weight by source reliability and reach. Public reviews and social posts carry brand impact weight; private survey responses carry individual sentiment weight. Document the weighting scheme applied.
5. **PII Removal**: Strip names, email addresses, phone numbers, order IDs, and other personally identifiable information from all text before analysis.

### Step 2 — Theme Extraction

Identify the dominant topics in customer feedback:

1. **Topic Modeling**: Apply BERTopic, LDA, or similar to discover natural topic clusters in the corpus. Optimal topic count typically ranges from 15-40 for a retail brand's full feedback corpus.
2. **Theme Labeling**: Assign human-readable labels to each topic cluster based on representative terms and documents. Use a consistent taxonomy aligned with business functions (product quality, delivery experience, pricing/value, customer service, website/app experience, store experience, returns process).
3. **Theme Hierarchy**: Organize themes into a two-level hierarchy — Level 1 (broad category) and Level 2 (specific sub-theme). Example: L1 = "Delivery Experience", L2 = "Late Delivery", "Damaged Package", "Missing Items", "Tracking Accuracy".
4. **Theme Prevalence**: Calculate the percentage of feedback mentioning each theme. Track changes from the prior period.

### Step 3 — Sentiment Analysis

Quantify the emotional tone of feedback within each theme:

1. **Document-Level Sentiment**: Score each piece of feedback as positive, negative, neutral, or mixed using a fine-tuned sentiment model (not just keyword matching).
2. **Aspect-Based Sentiment**: Where feedback mentions multiple themes, assign sentiment per theme rather than a single document score. "Love the product but delivery was terrible" should register positive for product and negative for delivery.
3. **Sentiment Intensity**: Beyond polarity, measure intensity on a scale (e.g., 1-5) to distinguish mild dissatisfaction from outrage.
4. **Sentiment Trend**: Compare current period sentiment distribution against prior period for each theme. Flag themes with sentiment shifts exceeding 10 percentage points.
5. **Emotion Classification**: Where useful, classify emotions more granularly: frustration, delight, confusion, trust, anxiety. This adds nuance beyond positive/negative.

### Step 4 — Signal Detection

Identify emerging issues and noteworthy patterns:

1. **Emerging Themes**: Detect themes that are new or rapidly growing in prevalence (volume increase exceeding 50% period-over-period with minimum volume threshold).
2. **Viral Risk Assessment**: Flag negative feedback with high engagement metrics (retweets, shares, review upvotes) that could amplify into a brand crisis.
3. **Correlation with Operations**: Cross-reference emerging themes with known operational events (product recalls, system outages, policy changes, competitor actions).
4. **Geographic Clustering**: Identify themes concentrated in specific regions or stores — these may indicate local operational issues rather than brand-wide problems.
5. **Segment Patterns**: Detect themes disproportionately affecting specific customer segments (new customers, loyalty members, high-value customers).

### Step 5 — Executive Summary Generation

Produce the final VoC summary:

1. **Headline Findings**: Top 3-5 insights that require executive attention, ordered by business impact.
2. **Theme Dashboard**: All themes with prevalence, sentiment, trend direction, and business function owner.
3. **Verbatim Showcase**: 2-3 representative (anonymized) customer quotes per major theme to humanize the data.
4. **Emerging Issues Alert**: Any new or rapidly growing themes that require immediate investigation.
5. **Recommended Actions**: For each headline finding, a specific recommended next step with suggested owner.
6. **Trend Comparison**: How this period's VoC compares to the prior period — what improved, what worsened, what is new.

## Output Specification

Produce a VoC summary report containing:

- `period`: Analysis period
- `total_feedback_volume`: Count of feedback items analyzed, broken down by source
- `headline_insights`: Array of top 3-5 findings, each with insight statement, supporting data, business impact assessment, and recommended action
- `theme_summary`: Array of themes, each with:
  - `theme_name`: Human-readable label
  - `level_1_category`: Broad category
  - `level_2_subcategory`: Specific sub-theme
  - `prevalence_pct`: Percentage of feedback mentioning this theme
  - `prevalence_change`: Period-over-period change in prevalence
  - `sentiment_distribution`: Percentage positive, negative, neutral, mixed
  - `sentiment_trend`: Direction and magnitude of sentiment shift
  - `representative_quotes`: 2-3 anonymized customer quotes
  - `business_owner`: Suggested functional owner
- `emerging_issues`: Array of newly detected or rapidly growing themes with velocity metrics and risk assessment
- `viral_risks`: Any high-engagement negative content requiring immediate attention
- `segment_insights`: Themes that disproportionately affect specific customer segments
- `period_comparison`: Summary of improvements, deteriorations, and new themes vs. prior period

## Analysis Framework

Apply the **Feedback Signal Pyramid**:

1. **Volume** (base): How much are customers talking about this topic? High volume = widespread relevance.
2. **Sentiment**: Of those talking, what is the emotional tone? Negative sentiment on a high-volume topic = urgent issue.
3. **Intensity**: How strongly do customers feel? High-intensity negative sentiment = potential brand damage.
4. **Velocity**: Is the topic growing or shrinking? Rapid growth = emerging issue needing fast response.
5. **Impact** (apex): What is the business consequence? Link to churn, revenue, or acquisition metrics where possible.

Prioritize themes that score high across multiple pyramid levels. A low-volume, high-intensity, high-velocity negative theme (e.g., a product safety concern) may be more urgent than a high-volume, moderate-intensity, stable theme (e.g., general pricing perception).

## Examples

**Example VoC Executive Summary**:

Period: Q4 2025. Total feedback analyzed: 47,832 items across 5 channels.

Headline 1: "Size accuracy" emerged as a new top-5 theme (8.2% prevalence, up from 2.1% in Q3) with 78% negative sentiment. Root cause: New vendor for Women's Denim is running 1.5 sizes smaller than legacy vendor. Impact: Return rate for affected SKUs is 34% vs. category average of 12%. Recommendation: Add prominent "runs small, size up" guidance to PDPs for affected SKUs immediately; initiate vendor quality conversation.

Headline 2: Sentiment toward "delivery speed" improved from 41% positive to 67% positive following the carrier network expansion in October. Positive mentions specifically cite same-day and next-day options. Recommendation: Expand same-day eligibility to 15 additional metros by Q1.

Headline 3: "Loyalty program" theme shows growing frustration (negative sentiment up 22 points) concentrated among tier-2 members. Verbatim analysis reveals dissatisfaction with the recent point devaluation. Quote: "It now takes twice as many points for the same reward. Feels like a bait and switch." Recommendation: Loyalty team to present mitigation plan (grandfathering, transition period, enhanced earn rates) within 2 weeks.

## Guidelines

- Process ALL available feedback, not just a convenience sample. Sampling introduces bias, especially for emerging issues that may have low absolute volume.
- Maintain source-channel attribution throughout the analysis. Do not blend social media sentiment with survey sentiment without noting the methodological differences.
- Weight feedback by source appropriately — a single viral tweet with 10K retweets has different brand impact than 10K individual survey responses saying the same thing.
- Always anonymize customer information before including verbatims in summaries. Remove names, locations, order numbers, and any identifying details.
- Validate topic model outputs by reviewing representative documents for each cluster. Auto-generated topics sometimes merge unrelated themes or split a single theme.
- Be cautious with automated sentiment analysis accuracy — test against human-labeled benchmarks. Most sentiment models achieve 75-85% accuracy; acknowledge this margin of error.
- Flag sarcasm and irony risks in sentiment analysis. "Great, another delayed delivery" is negative, but naive models may score it positive.
- Include positive themes alongside negative ones. Leadership needs to know what is working and what to protect, not just what to fix.
- Ensure the summary is actionable — every headline finding should point to a specific next step, not just describe a situation.

## Validation Checklist

- [ ] All feedback sources are represented in the analysis with volume counts per source
- [ ] Text cleaning preserved meaningful content and did not strip sentiment signals (like emojis)
- [ ] PII has been completely removed from all verbatims in the output
- [ ] Topic model quality validated (coherent themes, no garbage clusters, appropriate granularity)
- [ ] Sentiment model accuracy benchmarked against human labels (target over 80% agreement)
- [ ] Aspect-based sentiment applied where feedback mentions multiple themes
- [ ] Emerging issues defined with clear thresholds (volume growth rate and minimum volume)
- [ ] Viral risk assessment includes engagement metrics, not just content sentiment
- [ ] Period-over-period comparison uses consistent methodology across both periods
- [ ] Recommendations are specific, assigned to a business function, and actionable without further analysis
