---
name: Retailer Content Customizer
description: Tailor product content to meet the unique style guides, character limits, taxonomy rules, and merchandising requirements of each retail partner including Amazon, Walmart, Target, Kroger, and Instacart.

metadata:
  display_name: "Retailer Content Customizer"
  short_description: "Customize product content per retailer style guidelines"
  default_prompt: "Generate retailer content for my case with clear next steps"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Retailer Content Customizer

## Overview

This skill adapts a single source product content asset into retailer-specific variations that conform to each retail partner's content standards, character limits, taxonomy requirements, enhanced content templates, and merchandising expectations. A one-size-fits-all approach to retail content leaves 15-30% of conversion potential on the table — each retailer's algorithm, shopper behavior, and content display differs significantly.

The customizer maintains a central content master while producing channel-optimized variants that maximize search visibility and conversion within each retailer's ecosystem.

## When to Use

- Syndicating new product content across multiple retail partners.
- Onboarding to a new retailer channel with unique content requirements.
- Updating existing listings after retailer policy or template changes.
- Optimizing underperforming listings on specific retailer platforms.
- Preparing content for retailer-specific promotional events (Prime Day, Walmart+ Week, Target Circle Week).
- Submitting content through syndication platforms (Salsify, Syndigo, 1WorldSync).

## Required Inputs

| Input | Description | Example |
|---|---|---|
| `master_content` | Source-of-truth product content | Title, description, bullets, images, attributes |
| `target_retailers` | Retailers to customize for | `["Amazon", "Walmart", "Target", "Kroger", "Instacart"]` |
| `product_category` | Retailer-specific category/taxonomy | Category path per retailer |
| `brand_guidelines` | Brand voice and visual standards | Brand guide summary |
| `keywords_by_retailer` | Retailer-specific keyword research | Per-retailer keyword lists |
| `competitive_intel` | Top competitors per retailer | Competitor ASINs/listings |
| `enhanced_content_assets` | A+/Rich Media assets available | Image list, video URLs |
| `promotional_context` | Upcoming promotions or seasonal relevance | "Prime Day 2026", "Back to School" |

## Methodology

### Step 1 — Retailer Specification Mapping

Apply the content specification matrix for each target retailer:

**Amazon**:
| Field | Specification |
|---|---|
| Product Title | ≤ 200 chars; Brand + Line + Key Feature + Size/Count/Variant |
| Bullet Points | 5 bullets, ≤ 500 chars each (≤ 250 recommended for mobile) |
| Product Description | ≤ 2000 chars; HTML allowed (basic: `<b>`, `<br>`, `<ul>`) |
| Backend Search Terms | ≤ 250 bytes; no brand names, ASINs, or title duplicates |
| A+ Content | Standard: 5 modules; Premium: 7 modules with video |
| Image Requirements | Main: pure white background, ≥ 1000×1000px; 6-9 images total |
| Indexing Notes | Title, bullets, backend terms, and brand field are indexed for search |

**Walmart**:
| Field | Specification |
|---|---|
| Product Name | ≤ 75 chars (shelf title); ≤ 250 chars (long title) |
| Key Features | 3-10 bullets, ≤ 500 chars each |
| Shelf Description | ≤ 4000 chars; supports basic HTML |
| Rich Media | Walmart Rich Media modules via content providers |
| Image Requirements | Main: white background, ≥ 300×300px (1000×1000 recommended) |
| Search Optimization | Title, short description, and key features indexed |
| Unique Rules | Prop 65 warnings mandatory for CA; no competitor references |

**Target (Target+)**:
| Field | Specification |
|---|---|
| Product Title | ≤ 200 chars; emphasis on readability over keyword density |
| Description | Clean, scannable format; lifestyle-oriented |
| Specifications | Structured attribute table |
| Enhanced Content | Target+ enhanced content via Syndigo |
| Image Requirements | Lifestyle-first approach; in-context imagery preferred |
| Unique Rules | Target Circle integration; inclusive language requirements |

**Kroger / Instacart**:
| Field | Specification |
|---|---|
| Product Title | ≤ 100 chars typically |
| Description | Shorter format; ingredient-first for food/bev |
| Image | Pack shot on white; ≤ 4 images typical |
| Unique Rules | Nutritional attributes for search filters; dietary tags critical |

### Step 2 — Title Optimization per Retailer

Construct retailer-specific titles from the master content:

```
Master: "BrightClean Natural Dish Soap, Plant-Based Formula, Lemon Zest Scent, 28 fl oz"

Amazon:  "BrightClean Natural Dish Soap — Plant-Based, Biodegradable Formula — Lemon Zest Scent — Tough on Grease, Gentle on Hands — 28 fl oz"
Walmart: "BrightClean Natural Dish Soap Plant-Based Lemon Zest 28 fl oz"
Target:  "BrightClean Plant-Based Dish Soap - Lemon Zest - 28 fl oz"
Instacart: "BrightClean Dish Soap Lemon Zest 28oz"
```

Title optimization principles per retailer:
- **Amazon**: Front-load primary keyword; use separators (—, |); include key benefit differentiator.
- **Walmart**: Concise shelf title; save detail for key features; avoid special characters.
- **Target**: Clean, consumer-friendly; brand-first; dash separators; no keyword stuffing.
- **Instacart**: Ultra-concise; product type + variant + size; abbreviate units.

### Step 3 — Bullet / Feature Customization

Adapt the master bullet set to each retailer's style and priorities:

| Retailer | Bullet Strategy |
|---|---|
| **Amazon** | Benefit-led, CAPS opening phrase, keyword-rich, 5 bullets, address common objections |
| **Walmart** | Feature-focused, straightforward language, 3-5 bullets, value-oriented messaging |
| **Target** | Lifestyle-oriented, inclusive tone, scannable, emphasize design and experience |
| **Kroger** | Ingredient transparency, dietary attributes (organic, gluten-free, vegan), nutritional benefits |
| **Instacart** | Short, attribute-driven, emphasize what shoppers verify at shelf (flavor, size, diet compatibility) |

### Step 4 — Enhanced Content / A+ Module Adaptation

Map available assets to each retailer's enhanced content template system:

1. **Amazon A+ Content**: Standard (Brand Story + 5 modules) or Premium A+ (interactive, video, hover).
   - Module selection strategy: Comparison Chart + Lifestyle Banner + Feature Highlights + Brand Story + FAQ.
2. **Walmart Rich Media**: Below-the-fold modules via approved content providers (Syndigo, Salsify).
3. **Target Enhanced Content**: Clean, editorial-style layout; less promotional than Amazon A+.
4. **Instacart Shoppable Display**: Limited enhanced content; focus on clear product imagery.

### Step 5 — Attribute & Taxonomy Alignment

Ensure product attributes map correctly to each retailer's taxonomy:

1. Map master attributes to retailer-specific attribute names (e.g., "Scent" on Amazon vs. "Fragrance" on Walmart).
2. Populate retailer-required attributes that may not exist in master content (e.g., Walmart's "Is Portable," Amazon's "Item Form").
3. Validate category placement — incorrect taxonomy causes search suppression and browse issues.
4. Enable all applicable search refinement filters (dietary, allergen, certification badges).

### Step 6 — Content Scorecard per Retailer

Score each retailer-specific listing on the **Retail Content Effectiveness Index**:

| Dimension | Weight | Criteria |
|---|---|---|
| Completeness | 25% | All required and recommended fields populated |
| Keyword Optimization | 25% | Retailer-specific keywords in indexed fields |
| Content Quality | 20% | Readability, persuasion, brand voice alignment |
| Enhanced Content | 15% | A+/Rich Media present and optimized |
| Image Compliance | 15% | Meets retailer image specs and best practices |

**Score**: 0-100 per retailer. Target ≥ 85 for all channels.

## Output Specification

```yaml
output:
  retailer_variants:
    - retailer: string
      title: string
      bullets: list[string]
      description: string
      backend_keywords: string       # If applicable
      attributes: dict               # Retailer-specific attributes
      enhanced_content_plan: string   # Module recommendations
      content_score: float           # 0-100
      warnings: list[string]        # Policy or optimization gaps
  master_to_variant_diff: dict       # Changes from master per retailer
  cross_retailer_consistency: float  # Brand consistency score across all variants
```

## Analysis Framework

**Channel Performance Benchmarking**: After deployment, track per-retailer content performance:

| Metric | Amazon Benchmark | Walmart Benchmark | Target Benchmark |
|---|---|---|---|
| Content Score (Salsify/Profitero) | ≥ 90 | ≥ 85 | ≥ 80 |
| Search Rank (primary keyword) | Page 1 | Page 1-2 | Page 1 |
| Conversion Rate | > 10% (cat avg) | > 5% | > 4% |
| Glance Views → Detail Page % | > 0.5% | > 0.3% | > 0.3% |

## Examples

**Scenario**: Launching a new organic baby food pouch across Amazon, Walmart, Target, and Instacart.

**Key Customizations**:
- **Amazon**: Heavy keyword optimization ("organic baby food stage 2," "baby puree"), 5 FAB bullets, A+ Content with comparison chart vs. own product line.
- **Walmart**: Shorter title, Prop 65 compliance, highlight WIC eligibility, value messaging.
- **Target**: Clean aesthetic, inclusive family imagery, sustainability story, Target Circle offer mention.
- **Instacart**: Ultra-concise title, flavor/stage/size front-and-center, dietary filters enabled (organic, no added sugar).

## Guidelines

- Maintain a single source of truth (master content) — never let retailer variants become the master.
- Retailer rules supersede brand preferences when they conflict (e.g., Amazon's CAPS bullet style vs. brand's lowercase preference).
- Update retailer specifications quarterly — policies change frequently, especially on Amazon and Walmart.
- Never copy competitor content, even if higher-ranking — create original content per retailer TOS.
- Use content syndication platforms (Salsify, Syndigo) for scale, but manually optimize hero SKUs.
- Track retailer-specific content scores using tools like Profitero, DataWeave, or Edge by Ascential.

## Validation Checklist

- [ ] Title meets character limits and format rules for each retailer.
- [ ] Bullet/feature content is adapted to each retailer's style and priorities.
- [ ] All required attributes are populated per retailer taxonomy.
- [ ] Backend/search terms are optimized per retailer (no title duplication on Amazon).
- [ ] Enhanced content plan is tailored to each retailer's template system.
- [ ] Images meet each retailer's technical specifications.
- [ ] Retailer-specific policies are applied (Prop 65 for Walmart CA, no competitor refs on Amazon).
- [ ] Content Effectiveness Index score ≥ 85 per retailer.
- [ ] Cross-retailer brand consistency is maintained (tone, claims, messaging hierarchy).
- [ ] Content is ready for syndication platform ingestion format.
