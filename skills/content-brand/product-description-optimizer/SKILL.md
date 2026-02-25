---
name: Product Description Optimizer
description: Generate and optimize SEO-rich, conversion-focused product detail page (PDP) copy for CPG and retail e-commerce, leveraging keyword strategy, benefit-driven messaging, and structured content best practices.

metadata:
  display_name: "Product Description Optimizer"
  short_description: "Optimize product detail page copy for SEO and conversion"
  default_prompt: "Optimize my product description and suggest the best next steps"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Product Description Optimizer

## Overview

This skill produces high-converting product detail page copy that balances search engine visibility with persuasive consumer messaging. It applies CPG-specific SEO frameworks, benefit-ladder copywriting, and structured data alignment to maximize both organic traffic and on-page conversion rate.

The optimizer treats every PDP as a micro-landing page — each element (title, bullets, enhanced content) has a distinct job in the discovery-to-purchase funnel.

## When to Use

- Launching new SKUs on DTC or marketplace channels (Amazon, Walmart, Target+, Instacart).
- Refreshing existing listings that underperform on CTR (< 0.4%) or CVR (< 8% category avg).
- Expanding to new keywords or search verticals (e.g., "clean label," "keto-friendly").
- Migrating content across retailers with different character-limit and formatting rules.
- Preparing A+ / Enhanced Brand Content modules.

## Required Inputs

| Input | Description | Example |
|---|---|---|
| `product_name` | Full SKU name including variant | "BrightClean Dish Soap, Lemon Zest, 28 oz" |
| `product_attributes` | Key specs: size, scent, flavor, form factor, count | JSON or table |
| `target_keywords` | Primary (1-2) and secondary (3-7) keywords with search volume | `{ "primary": ["natural dish soap"], "secondary": ["plant-based dish soap", "eco dish soap"] }` |
| `category` | Retail taxonomy / browse node | "Health & Household > Cleaning Supplies > Dish Soap" |
| `brand_voice_guide` | Link or summary of tone, banned words, mandatory claims | Brand style guide excerpt |
| `channel` | Target retailer or DTC platform | "Amazon US", "Walmart.com", "Shopify DTC" |
| `competitive_set` | Top 3-5 competitor ASINs/URLs for gap analysis | List of URLs |
| `regulatory_claims` | Approved on-pack claims and certifications | "USDA Organic", "EPA Safer Choice" |

## Methodology

### Step 1 — Keyword & Search Intent Mapping

1. Classify each keyword by intent: **navigational** (brand search), **informational** (how-to), **transactional** (buy/best).
2. Map primary keyword to the product title; secondary keywords distributed across bullets and description.
3. Identify long-tail modifiers from auto-suggest, "Customers also searched," and Related Search terms.
4. Calculate a **Keyword Coverage Score**: (matched keywords / total target keywords) × 100. Target ≥ 85%.

### Step 2 — Title Construction

Apply the **CPG Title Formula**:

```
[Brand] + [Product Line] + [Key Differentiator] + [Primary Keyword] + [Size/Count] + [Variant]
```

- Amazon: ≤ 200 characters (80 chars mobile-visible).
- Walmart: ≤ 75 characters for title; extended title ≤ 250.
- Keep the first 60 characters front-loaded with primary keyword and core benefit.

### Step 3 — Benefit-Ladder Bullet Points

Use the **Feature → Advantage → Benefit (FAB)** framework for each bullet:

1. **Feature**: What it is (ingredient, technology, format).
2. **Advantage**: What it does better than alternatives.
3. **Benefit**: What the consumer gains (time saved, peace of mind, sensory delight).

Write 5 bullets (Amazon) or 3-4 key features (Walmart). Each bullet ≤ 250 characters. Lead with the benefit, not the feature. Naturally embed one secondary keyword per bullet without stuffing.

### Step 4 — Product Description / A+ Content

- **Above the fold**: 50-80 word paragraph restating the core value proposition with primary keyword in the first sentence.
- **Storytelling module**: Brand origin or use-case scenario (150-200 words).
- **Comparison chart**: Feature matrix vs. own portfolio (not competitors, per Amazon TOS).
- **Lifestyle imagery alt text**: Keyword-enriched, descriptive alt text ≤ 125 characters.

### Step 5 — Structured Data & Backend Optimization

- Populate search terms / backend keywords with synonyms, abbreviations, and Spanish-language equivalents where relevant.
- Ensure `itemType`, `material`, `scent`, and custom attributes align with browse node expectations.
- Add schema.org Product markup for DTC (name, brand, sku, gtin, offers, aggregateRating).

### Step 6 — Readability & Conversion Audit

| Metric | Target |
|---|---|
| Flesch-Kincaid Grade Level | 6-8 (general CPG) |
| Avg sentence length | ≤ 20 words |
| Power words per bullet | ≥ 1 ("effortless," "clinically proven," "dermatologist tested") |
| CTA presence | At least 1 implicit CTA ("Try," "Discover," "Experience") |
| Scannability | No paragraph > 3 lines on mobile |

## Output Specification

```yaml
output:
  title: string              # Optimized product title
  bullets: list[string]      # 3-5 benefit-driven bullet points
  description_html: string   # Rich product description with HTML
  backend_keywords: string   # Space-separated, ≤ 250 bytes
  seo_score: float           # 0-100 composite score
  readability_grade: float   # Flesch-Kincaid grade level
  keyword_coverage: float    # Percentage of target keywords used
  warnings: list[string]     # Policy violations or optimization gaps
```

## Analysis Framework

Score each listing across five dimensions (20 points each, total 100):

1. **Keyword Relevance (20)**: Primary keyword in title & first bullet; secondary keywords distributed; no cannibalization.
2. **Persuasion Quality (20)**: FAB framework applied; emotional triggers present; objection handling (e.g., "no artificial dyes").
3. **Compliance (20)**: No banned claims; certifications substantiated; retailer policy adherence.
4. **Readability (20)**: Grade level, sentence length, scannable formatting.
5. **Technical SEO (20)**: Backend keywords populated; structured data complete; image alt text present.

## Examples

**Input snippet**:
- Product: "PureGlow Vitamin C Serum, 1 fl oz"
- Primary keyword: "vitamin c serum for face"
- Channel: Amazon US

**Optimized Title**:
"PureGlow Vitamin C Serum for Face — 20% L-Ascorbic Acid, Hyaluronic Acid & Vitamin E — Brightening & Anti-Aging Face Serum, 1 fl oz"

**Bullet 1 (FAB)**:
"VISIBLY BRIGHTER SKIN IN 14 DAYS — Our stabilized 20% L-Ascorbic Acid formula penetrates deeply to reduce dark spots and even skin tone, so you wake up to a radiant, lit-from-within glow."

## Guidelines

- Never make unsubstantiated health or efficacy claims; always tie claims to approved language from regulatory/legal.
- Avoid keyword stuffing — a keyword density > 3% in any content block triggers a warning.
- Do not reference competitors by name on Amazon or Walmart.
- Use sentence case for bullets on Amazon; title case for titles.
- Always run final copy through the **Claims Compliance Checker** skill before publishing.
- Preserve brand voice parameters: if the guide says "playful," do not write clinical copy.

## Validation Checklist

- [ ] Primary keyword appears in title, first bullet, and description opening.
- [ ] All bullets follow the FAB framework.
- [ ] Title length within channel-specific character limit.
- [ ] Backend keywords contain no duplicates of title/bullet words.
- [ ] Flesch-Kincaid grade level ≤ 8.
- [ ] No banned or unsubstantiated claims present.
- [ ] Structured data / schema markup is complete (DTC).
- [ ] Content passes retailer-specific style guide checks.
- [ ] Keyword coverage score ≥ 85%.
- [ ] At least one implicit CTA is present in the description.
