---
name: UGC Moderation Assistant
description: Screen, classify, and moderate user-generated content including product reviews, Q&A submissions, community posts, and uploaded media for CPG and retail e-commerce platforms.

metadata:
  display_name: "Ugc Moderation Assistant"
  short_description: "Moderate user-generated reviews and product content"
  default_prompt: "Help me with ugc moderation and give clear next steps"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# UGC Moderation Assistant

## Overview

This skill provides a structured moderation framework for user-generated content (UGC) across e-commerce platforms — product reviews, ratings, Q&A, community forums, and user-submitted photos/videos. It balances brand protection with authentic consumer voice, applying regulatory, legal, and brand-safety filters while preserving genuine feedback that drives conversion.

Authentic reviews increase conversion rates by 15-30%. The goal is not to suppress negative feedback but to ensure all published content is genuine, compliant, and safe.

## When to Use

- Processing incoming product reviews before publication on DTC or marketplace storefronts.
- Moderating Q&A submissions on product detail pages.
- Screening user-submitted photos and videos for brand safety.
- Auditing existing review corpuses for policy violations or fake review patterns.
- Generating moderation reports for brand and legal teams.
- Responding to or flagging reviews that require brand intervention.

## Required Inputs

| Input | Description | Example |
|---|---|---|
| `ugc_content` | The user-generated text, rating, and metadata | `{ "text": "...", "rating": 4, "author": "...", "date": "..." }` |
| `product_info` | Associated product name, category, and claims | Product record |
| `moderation_policy` | Brand-specific moderation rules and thresholds | Policy document |
| `channel` | Platform where UGC will appear | "DTC Shopify", "Amazon Vine", "Bazaarvoice" |
| `media_attachments` | URLs to any user-uploaded images or videos | List of URLs |
| `escalation_contacts` | Contacts for legal, PR, and customer service escalation | Email/Slack channels |
| `historical_patterns` | Known fake review patterns or repeat offenders | Pattern library |

## Methodology

### Step 1 — Content Classification

Classify each piece of UGC into a moderation category:

| Category | Definition | Default Action |
|---|---|---|
| **Approved** | Genuine, policy-compliant, and relevant | Publish |
| **Approved with Edit** | Minor issues (PII, formatting) that can be auto-corrected | Publish after edit |
| **Flagged for Review** | Ambiguous content requiring human judgment | Queue for manual review |
| **Rejected — Policy** | Violates moderation policy (profanity, hate speech, threats) | Block with reason code |
| **Rejected — Compliance** | Contains regulated claims or legal risk | Block and escalate |
| **Rejected — Authenticity** | Suspected fake, incentivized, or competitor-planted review | Block and log |

### Step 2 — Authenticity Assessment

Apply the **Review Authenticity Scorecard** to detect inauthentic content:

| Signal | Weight | Indicators |
|---|---|---|
| Linguistic Analysis | 25% | Generic language, excessive superlatives, template patterns, lack of product-specific detail |
| Behavioral Patterns | 25% | Review velocity (multiple reviews in minutes), reviewer history, geographic anomalies |
| Purchase Verification | 20% | Verified purchase flag, order-to-review timing (< 24hrs suspicious, > 90 days stale) |
| Sentiment-Rating Alignment | 15% | 5-star rating with negative text, or vice versa — indicates manipulation |
| Duplicate Detection | 15% | Near-duplicate text across products, accounts, or time periods |

**Authenticity Score**: 0-100. Content below 40 is auto-rejected. 40-65 is flagged for human review. Above 65 passes authenticity gate.

### Step 3 — Safety & Compliance Screening

Screen content against multiple safety layers:

**Legal Safety**:
- PII detection: email addresses, phone numbers, full names of non-public individuals, addresses.
- Defamation risk: false statements of fact about competitors or individuals.
- Intellectual property: copyrighted text, trademarked terms used inappropriately.

**Regulatory Compliance**:
- Health/medical claims in reviews: "This cured my diabetes" — flag for disclaimer or removal.
- Off-label use descriptions for regulated products.
- Adverse event reports (FDA-reportable for supplements, OTC drugs, cosmetics).

**Brand Safety**:
- Profanity and hate speech (zero tolerance).
- Violent or sexually explicit content.
- Competitor promotion or spam links.
- Politically divisive or discriminatory language.

### Step 4 — Adverse Event Detection (CPG-Specific)

For FDA-regulated categories (supplements, OTC, cosmetics, food), identify potential adverse event reports:

1. Scan for medical terminology: "allergic reaction," "rash," "hospitalized," "side effect."
2. Classify severity: mild (discomfort), moderate (required medical attention), serious (hospitalization, life-threatening).
3. Serious adverse events trigger **mandatory escalation** to regulatory affairs within 24 hours.
4. Log all adverse event mentions in the pharmacovigilance tracking system.

### Step 5 — Sentiment Analysis & Brand Intelligence

Extract actionable intelligence from approved UGC:

- **Sentiment Distribution**: Positive / neutral / negative ratio by product and time period.
- **Topic Clustering**: Group reviews by theme (packaging, taste, efficacy, value, shipping).
- **Emerging Issues**: Detect sudden spikes in negative sentiment on specific topics.
- **Competitive Mentions**: Track competitor name mentions and comparative sentiment.
- **Feature Requests**: Identify recurring requests for product improvements.

### Step 6 — Response Prioritization

Rank reviews requiring brand response by urgency:

| Priority | Criteria | Response SLA |
|---|---|---|
| **P0 — Crisis** | Safety issue, viral potential, adverse event | 2 hours |
| **P1 — Urgent** | 1-star verified purchase with specific product defect | 24 hours |
| **P2 — Important** | Detailed negative review with actionable feedback | 48 hours |
| **P3 — Standard** | Positive review warranting thank-you response | 72 hours |
| **P4 — Monitor** | Neutral review, no action needed | No response required |

## Output Specification

```yaml
output:
  moderation_decision: string        # "approved" | "approved_with_edit" | "flagged" | "rejected"
  rejection_reason: string           # Policy code if rejected
  authenticity_score: float          # 0-100
  safety_flags: list[string]        # Specific safety issues found
  adverse_event_detected: boolean
  adverse_event_severity: string     # "mild" | "moderate" | "serious" | null
  sentiment: string                  # "positive" | "neutral" | "negative"
  topics: list[string]              # Extracted themes
  response_priority: string          # P0-P4
  suggested_response: string         # Draft brand response if P0-P3
  edits_applied: list[string]       # Auto-corrections made (PII redaction, etc.)
  pii_redacted: boolean
```

## Analysis Framework

**UGC Health Dashboard Metrics** (aggregate across all moderated content):

| Metric | Healthy Range | Alert Threshold |
|---|---|---|
| Approval Rate | 85-95% | < 75% (overly restrictive) or > 98% (under-moderated) |
| Fake Review Rate | < 5% | > 10% |
| Avg Authenticity Score | > 75 | < 60 |
| Adverse Event Rate | < 0.1% | > 0.5% (potential product issue) |
| Avg Response Time (P0/P1) | < 12 hrs | > 24 hrs |
| Sentiment Trend | Stable or improving | 3+ consecutive weeks declining |

## Examples

**Input Review**: "TERRIBLE product!! Gave me a horrible rash all over my arms. Called my doctor and he said it was a chemical burn. DO NOT BUY. Contact me at jane.smith@email.com to join the lawsuit."

**Analysis**:
- **Moderation Decision**: Rejected — Compliance
- **Authenticity Score**: 78 (genuine language, specific details)
- **Safety Flags**: PII detected (email), potential legal threat
- **Adverse Event**: Detected — Severity: Moderate (required medical attention)
- **Response Priority**: P0 — Crisis
- **Actions**: (1) Redact email address. (2) Escalate adverse event to regulatory affairs immediately. (3) Escalate legal threat to legal team. (4) Draft empathetic response with customer service contact.

## Guidelines

- Never suppress genuine negative reviews — they build trust and provide product intelligence.
- Adverse event detection is a legal obligation for FDA-regulated products. Err on the side of over-reporting.
- PII must be redacted before publication, never after.
- Incentivized reviews (samples, discounts) must be disclosed per FTC guidelines.
- Maintain consistent moderation standards regardless of rating — do not apply stricter standards to negative reviews.
- All moderation decisions must be logged with timestamps and rationale for audit trails.

## Validation Checklist

- [ ] Content is classified into the correct moderation category.
- [ ] Authenticity score is calculated using all five signal dimensions.
- [ ] PII is detected and redacted before any publication decision.
- [ ] Adverse events are identified, classified by severity, and escalated per protocol.
- [ ] Safety screening covers legal, regulatory, and brand-safety layers.
- [ ] Response priority is assigned based on urgency criteria.
- [ ] Suggested brand response is drafted for P0-P3 reviews.
- [ ] Moderation decision is logged with full audit trail.
- [ ] Fake review patterns are cross-referenced against historical data.
- [ ] Aggregate moderation metrics fall within healthy ranges.
