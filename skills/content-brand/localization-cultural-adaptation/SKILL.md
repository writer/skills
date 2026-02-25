---
name: Localization & Cultural Adaptation
description: Adapt CPG and retail e-commerce content for target markets with culturally resonant messaging, locale-specific regulatory compliance, and linguistic quality assurance beyond simple translation.

metadata:
  display_name: "Localization & Cultural Adaptation"
  short_description: "Localize retail content with cultural adaptation and QA"
  default_prompt: "Check my localization cultural adaptation for gaps risks and required fixes"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Localization & Cultural Adaptation

## Overview

This skill transforms source-market content into culturally adapted, market-ready copy for international CPG and retail expansion. It goes far beyond translation — applying cultural insight, local regulatory requirements, consumer behavior research, and market-specific SEO to produce content that resonates as if it were created natively in the target market.

Poorly localized content reduces purchase intent by up to 40%. This skill treats localization as a strategic revenue lever, not a cost center.

## When to Use

- Expanding product listings to new country marketplaces (Amazon.de, Rakuten, MercadoLibre).
- Adapting DTC website content for international storefronts.
- Localizing packaging copy for regulatory compliance in new markets.
- Creating market-specific advertising and social media campaigns.
- Auditing existing localized content for quality and cultural fit.
- Adapting US English content to UK English, Canadian French, Latin American Spanish, etc.

## Required Inputs

| Input | Description | Example |
|---|---|---|
| `source_content` | Original content in source language | English PDP copy, ad creative |
| `source_market` | Origin market and locale | "en-US" |
| `target_markets` | Destination markets and locales | `["de-DE", "ja-JP", "es-MX", "fr-CA"]` |
| `product_category` | Product type for regulatory context | "organic snack food", "skincare" |
| `brand_voice_guide` | Brand voice parameters (adapts per market) | Voice document |
| `local_competitors` | Key competitors in target market | List of brands/URLs |
| `target_keywords` | Local SEO keywords per market | Per-locale keyword lists |
| `regulatory_requirements` | Market-specific labeling and claims rules | Regulatory summary per market |
| `cultural_briefing` | Any known sensitivities or preferences | Cultural notes |

## Methodology

### Step 1 — Market Intelligence Gathering

Build a **Cultural Context Profile** for each target market:

1. **Consumer Behavior**: Purchase drivers, price sensitivity, channel preferences, decision-making style (individual vs. family/community).
2. **Category Norms**: How the product category is perceived locally (e.g., supplements as medicine in Germany vs. wellness in the US).
3. **Communication Style**: Direct vs. indirect, humor tolerance, formality expectations, preferred narrative structures.
4. **Visual & Aesthetic Preferences**: Color associations (white = purity in West, mourning in East Asia), imagery norms, layout conventions (RTL for Arabic/Hebrew).
5. **Taboos & Sensitivities**: Religious considerations (halal/kosher), political sensitivities, culturally inappropriate imagery or metaphors.

### Step 2 — Linguistic Adaptation (Beyond Translation)

Apply the **Transcreation Framework** — a spectrum from translation to full creative adaptation:

| Level | When to Use | Example |
|---|---|---|
| **Translation** | Legal text, ingredient lists, technical specs | Direct equivalent |
| **Localization** | Product descriptions, UI elements | "16 oz" → "473 ml" |
| **Transcreation** | Headlines, taglines, emotional copy | "Got Milk?" → "¿Y la leche?" (culturally adapted) |
| **Creation** | Market-specific campaigns with no source equivalent | New content from brief |

For each content block, determine the appropriate adaptation level. Functional content (specs, ingredients) gets translated; emotional content (headlines, benefits) gets transcreated.

### Step 3 — Locale-Specific SEO Optimization

1. **Keyword Research**: Use local search tools (not translated US keywords) to identify actual search behavior in the target language.
2. **Search Intent Mapping**: The same product may have different search intents by market (informational in emerging markets vs. transactional in mature markets).
3. **Title & Bullet Localization**: Apply local marketplace title formulas and character limits.
4. **Backend Keywords**: Populate with local synonyms, colloquialisms, and alternate spellings (e.g., "colour" vs. "color" for UK).

### Step 4 — Regulatory & Legal Adaptation

| Market | Key Regulatory Considerations |
|---|---|
| **EU** | EC 1169/2011 (food labeling), EC 1223/2009 (cosmetics), GPSR, mandatory allergen declarations in bold |
| **UK** | Post-Brexit divergence from EU; UK-specific MHRA for health products |
| **Canada** | Bilingual labeling (English + French) mandatory; CFIA food regulations; NHP regulations |
| **Japan** | FOSHU system for health claims; JFSL compliance; ingredient name translation to INCI Japanese |
| **Germany** | HWG (Heilmittelwerbegesetz) restricts health advertising; strong consumer protection (Wettbewerbsrecht) |
| **Mexico** | NOM labeling standards; front-of-pack warning labels for sugar/sodium/calories |
| **Australia** | TGA for therapeutics; FSANZ for food standards; mandatory country-of-origin labeling |

### Step 5 — Cultural Quality Scoring

Evaluate localized content using the **Multidimensional Quality Metrics (MQM)** framework adapted for CPG:

| Dimension | Weight | Scoring Criteria |
|---|---|---|
| Accuracy | 25% | Factual correctness, no meaning shifts, claim preservation |
| Fluency | 25% | Reads naturally in target language; no translationese |
| Cultural Appropriateness | 20% | No cultural faux pas; locally resonant imagery and metaphors |
| Terminology | 15% | Correct industry and regulatory terminology for the locale |
| SEO Effectiveness | 15% | Local keywords integrated; search visibility potential |

**Quality Score**: 0-100. Minimum threshold for publication: 80.

### Step 6 — In-Market Validation

Before full launch, recommend validation steps:

1. **Native Speaker Review**: At least one in-market native speaker reviews all transcreated content.
2. **Back-Translation Check**: Translate back to source language to catch meaning drift.
3. **Cultural Sensitivity Panel**: For markets with significant cultural distance, run content by a local focus group.
4. **A/B Testing**: Test localized vs. direct-translated content for CTR/CVR differences in first 30 days.

## Output Specification

```yaml
output:
  localized_content:
    title: string
    bullets: list[string]
    description: string
    backend_keywords: string
  locale: string                    # Target locale code
  adaptation_level: string          # "translation" | "localization" | "transcreation" | "creation"
  quality_score: float              # MQM score 0-100
  dimension_scores:
    accuracy: float
    fluency: float
    cultural_appropriateness: float
    terminology: float
    seo_effectiveness: float
  regulatory_compliance: boolean
  regulatory_notes: list[string]
  cultural_adaptations: list[string]  # Log of cultural changes made
  warnings: list[string]             # Potential issues for human review
  back_translation: string           # English back-translation for verification
```

## Analysis Framework

**Localization ROI Assessment**: Track the business impact of localization quality:

- **Content Quality vs. Conversion**: Correlate MQM scores with in-market CVR.
- **Localization Depth vs. Revenue**: Compare transcreated listings against translated-only for revenue per session.
- **Time-to-Market**: Measure days from source content availability to localized go-live.
- **Cost-per-Locale**: Track localization investment per market vs. revenue contribution.

## Examples

**Source (en-US)**: "Our farm-fresh granola is loaded with crunchy clusters and real berries — the perfect way to start your morning!"

**de-DE (Transcreation)**: "Unser knuspriges Granola mit echten Beeren bringt natürlichen Genuss in jeden Morgen — sorgfältig ausgewählt, wie vom Wochenmarkt."
- *Cultural note*: "Farm-fresh" doesn't resonate in German market; adapted to "Wochenmarkt" (weekly market) which carries similar connotations of quality and freshness.

**ja-JP (Transcreation)**: "農場から届いたような新鮮さ。本物のベリーとカリカリクラスターで、毎朝を特別なひとときに。"
- *Cultural note*: Emphasis shifted to the "special moment" framing, which resonates with Japanese breakfast culture of mindful eating.

## Guidelines

- Never assume a US keyword simply translates — always research local search behavior.
- Measurements, currencies, date formats, and number formatting must match target locale conventions.
- Colors, animals, and hand gestures in imagery must be reviewed for cultural meaning.
- Humor rarely translates — default to benefit-driven messaging if uncertain.
- For bilingual markets (Canada, Belgium, Switzerland), ensure both languages receive equal creative quality.
- Preserve all regulatory claims verbatim as approved for the target market — do not transcreate legal language.

## Validation Checklist

- [ ] Cultural Context Profile is complete for each target market.
- [ ] Adaptation level (translation/localization/transcreation/creation) is assigned per content block.
- [ ] Local keyword research is conducted (not just translated from source).
- [ ] All measurements, currencies, and formats follow target locale conventions.
- [ ] Regulatory requirements for the target market are applied.
- [ ] MQM quality score ≥ 80 across all dimensions.
- [ ] Back-translation confirms no meaning drift for critical claims.
- [ ] Cultural sensitivities are reviewed and documented.
- [ ] Content reads naturally with no translationese.
- [ ] In-market validation plan is defined before launch.
