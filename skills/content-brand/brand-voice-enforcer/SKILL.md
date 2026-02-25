---
name: Brand Voice Enforcer
description: Analyze and rewrite content to strict brand voice guidelines, scoring adherence across tone, vocabulary, syntax patterns, and persona alignment for CPG and retail brands.

metadata:
  display_name: "Brand Voice Enforcer"
  short_description: "Enforce brand voice consistency across all content types"
  default_prompt: "Score my brand voice enforcer and explain what to improve"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Brand Voice Enforcer

## Overview

This skill enforces brand voice consistency across all consumer-facing content — PDP copy, social posts, email campaigns, packaging copy, and customer service templates. It ingests a brand's voice framework, builds a scoring rubric, and rewrites non-conforming content while preserving factual accuracy and SEO value.

Brand voice is treated as a measurable system, not a subjective opinion. Every piece of content receives a quantified Voice Adherence Score (VAS) against the brand's defined personality dimensions.

## When to Use

- Onboarding new copywriters or agencies who need guardrails.
- Auditing existing content libraries for voice drift after rebrands or acquisitions.
- Adapting content across channels (packaging → digital, US → international) while preserving voice.
- Reviewing AI-generated or user-submitted content before publication.
- Building or updating a brand voice scoring model for automated QA pipelines.

## Required Inputs

| Input | Description | Example |
|---|---|---|
| `brand_voice_guide` | The complete brand voice document or structured summary | PDF, markdown, or JSON |
| `voice_dimensions` | 3-5 personality axes with definitions | `["Warm & Approachable", "Expert but Accessible", "Playfully Confident"]` |
| `vocabulary_rules` | Preferred terms, banned words, and substitutions | `{ "preferred": {"utilize": "use"}, "banned": ["cheap", "chemical-free"] }` |
| `content_samples` | 3-5 exemplar pieces that embody the ideal voice | URLs or text blocks |
| `input_content` | The content to be evaluated and rewritten | Raw text or HTML |
| `channel` | Target channel for format-specific norms | "Instagram caption", "PDP bullet", "email subject" |
| `audience_segment` | Primary audience persona | "Millennial parents, health-conscious" |

## Methodology

### Step 1 — Voice Profile Construction

Parse the brand voice guide into a structured **Voice DNA Model**:

1. **Personality Dimensions**: Map each dimension to a 1-5 scale with behavioral anchors.
   - Example: *Warmth* — 1 (clinical/detached) → 5 (conversational/intimate).
2. **Sentence Patterns**: Identify preferred syntax — short declarative vs. compound; active vs. passive; question leads vs. statement leads.
3. **Lexical Fingerprint**: Build a preferred vocabulary set (200-500 words) and a banned vocabulary set from the guide and exemplar content.
4. **Punctuation & Formatting Style**: Em dashes vs. parentheses, exclamation point frequency, emoji policy, capitalization rules.
5. **Persona Guardrails**: Define what the brand *is* and *is not* (e.g., "expert but never condescending").

### Step 2 — Content Analysis & Scoring

Evaluate input content against the Voice DNA Model using the **Voice Adherence Scorecard**:

| Dimension | Weight | Scoring Criteria |
|---|---|---|
| Tone Alignment | 25% | Does emotional register match target dimensions? |
| Vocabulary Compliance | 25% | Preferred terms used; banned terms absent; jargon level appropriate |
| Syntax Pattern Match | 20% | Sentence length, structure, and rhythm match exemplars |
| Persona Consistency | 15% | Content sounds like the defined brand persona throughout |
| Channel Fit | 15% | Tone and format norms match the target channel |

Calculate a composite **Voice Adherence Score (VAS)** from 0-100:
- **90-100**: Publication-ready. Minor polish only.
- **70-89**: Acceptable with targeted edits. Flag specific deviations.
- **50-69**: Significant rewrite needed. Multiple dimension failures.
- **Below 50**: Full rewrite. Content is off-brand.

### Step 3 — Deviation Identification

For each deviation detected, produce a structured finding:

```yaml
deviation:
  location: "Bullet 3, sentence 2"
  dimension: "Tone Alignment"
  severity: "major"       # minor | moderate | major
  original: "This product eliminates germs using powerful chemicals."
  issue: "Word 'chemicals' is banned; tone is clinical rather than warm."
  suggestion: "This formula wipes out 99.9% of germs with plant-powered ingredients."
```

### Step 4 — Guided Rewrite

1. Preserve all factual claims, keywords, and regulatory language from the original.
2. Apply voice transformations in priority order: banned word removal → tone adjustment → syntax alignment → persona tuning.
3. Maintain or improve readability scores (never increase grade level by more than 1).
4. Re-score the rewritten content to confirm VAS ≥ 85.

### Step 5 — Cross-Channel Adaptation

When adapting across channels, apply channel-specific voice modulations:

| Channel | Modulation |
|---|---|
| PDP (Amazon/Walmart) | More functional, keyword-aware; caps-led bullets |
| Social (Instagram/TikTok) | Shorter sentences, emoji-permitted, conversational hooks |
| Email | Personalized, benefit-first subject lines, CTA-driven body |
| Packaging | Concise, legal-reviewed, regulatory claim format |
| Customer Service | Empathetic, solution-oriented, first-person plural ("we") |

## Output Specification

```yaml
output:
  voice_adherence_score: float          # 0-100 composite VAS
  dimension_scores:
    tone_alignment: float
    vocabulary_compliance: float
    syntax_pattern_match: float
    persona_consistency: float
    channel_fit: float
  deviations: list[Deviation]           # Structured deviation findings
  rewritten_content: string             # Voice-corrected content
  rewrite_changelog: list[string]       # Summary of changes made
  confidence: float                     # Model confidence in rewrite quality
```

## Analysis Framework

The **Brand Voice Consistency Matrix** evaluates voice across three layers:

1. **Surface Layer** (vocabulary, punctuation, formatting) — easiest to enforce, most commonly violated.
2. **Structural Layer** (sentence patterns, paragraph rhythm, information hierarchy) — requires syntactic analysis.
3. **Semantic Layer** (emotional tone, persona expression, cultural resonance) — requires contextual understanding.

Enforcement priority: Surface → Structural → Semantic. Surface violations are auto-corrected; structural issues are flagged with suggestions; semantic misalignments require human review.

## Examples

**Brand Voice Profile**: "Sunny Kitchen" — a natural food brand.
- Dimensions: Warm (5), Playful (4), Expert (3), Premium (2).
- Banned words: "artificial," "processed," "cheap," "stuff."
- Preferred: "wholesome," "real ingredients," "kitchen-crafted."

**Input**: "Our product is manufactured using all-natural processes and contains no artificial ingredients."

**Analysis**: VAS = 42. "Manufactured" is clinical (Warmth violation). "All-natural" is an FDA-flagged term. Passive voice mismatches playful dimension.

**Rewrite**: "We craft every jar in small batches with real, wholesome ingredients — nothing artificial, ever."

**New VAS**: 91.

## Guidelines

- Never sacrifice regulatory accuracy for voice. Approved claims must remain verbatim even if they sound off-brand.
- Flag any rewrite that alters a factual claim for human review.
- When brand guides conflict with channel requirements (e.g., Amazon caps style vs. brand's lowercase preference), channel rules take precedence with a logged exception.
- Update the Voice DNA Model quarterly or after any brand refresh.
- Treat voice dimensions as a spectrum, not a binary — partial adherence is scored proportionally.

## Validation Checklist

- [ ] Voice DNA Model is built from the provided brand guide and exemplars.
- [ ] All five VAS dimensions are scored independently.
- [ ] Every deviation is logged with location, severity, and a concrete suggestion.
- [ ] Rewritten content scores ≥ 85 VAS.
- [ ] No factual claims, certifications, or regulatory language was altered.
- [ ] Banned vocabulary is fully removed.
- [ ] Readability grade level did not increase by more than 1.
- [ ] Channel-specific formatting rules are applied.
- [ ] Rewrite changelog is complete and auditable.
- [ ] Final output reviewed against brand "is / is not" persona guardrails.
