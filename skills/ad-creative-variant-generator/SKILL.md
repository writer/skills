---
name: ad-creative-variant-generator
description: >
  Generates systematic ad creative variants across copy, visual direction, format, and audience angle
  for CPG and retail e-commerce campaigns. Use when a user needs multiple ad variations for testing,
  creative diversification, or multi-platform adaptation. Triggers on requests for ad copy, creative
  variants, A/B test assets, ad matrix generation, or platform-specific ad content.

metadata:
  display_name: "Ad Creative Variant Generator"
  short_description: "Create multi-format ad creative variations for CPG"
  default_prompt: "Generate ad creative variant for my case with clear next steps"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Ad Creative Variant Generator

## Overview

This skill produces a structured matrix of ad creative variants by systematically varying messaging angles, copy styles, visual treatments, CTAs, and format specifications across platforms. It applies direct-response and brand advertising best practices specific to CPG and retail categories to maximize test coverage while maintaining brand coherence.

## When to Use

- Launching a new ad campaign that requires multiple creative variants for testing
- Refreshing existing creatives to combat performance fatigue
- Adapting a hero concept across platforms (Meta, TikTok, Google, Pinterest, Amazon)
- Building a creative testing roadmap with hypothesis-driven variants
- Generating copy and concept variations for dynamic creative optimization (DCO)
- Scaling creative output for multi-SKU or multi-segment campaigns

## Required Inputs

| Input | Required | Description |
|---|---|---|
| Product / Offer | Yes | Product name, key benefits, pricing, and promotional offer if applicable |
| Target Audience | Yes | Primary audience segment with demographics and psychographics |
| Platform(s) | Yes | Channels where ads will run (Meta, TikTok, Google, Pinterest, Amazon, etc.) |
| Campaign Objective | Yes | Awareness, consideration, conversion, or retargeting |
| Brand Voice | No | Tone descriptors (e.g., playful, authoritative, warm). Defaults to category norms |
| Existing Top Performers | No | Current best-performing ad copy/concepts for iteration |
| Number of Variants | No | Desired quantity; defaults to 12 (3 angles × 2 copy styles × 2 CTAs) |
| Compliance Constraints | No | Regulated claims, required disclaimers, restricted language |

## Methodology

### Step 1 — Message Angle Mining

Identify 3–5 distinct messaging angles from product inputs:

| Angle Type | Description | CPG Example |
|---|---|---|
| Functional Benefit | What the product does | "Removes 99% of stains in one wash" |
| Emotional Benefit | How it makes you feel | "Confidence in every outfit" |
| Social Proof | Validation from others | "Rated #1 by 10,000+ parents" |
| Problem-Agitation | Pain point amplification | "Tired of detergents that irritate sensitive skin?" |
| Aspirational | Identity and lifestyle | "For families who choose clean living" |
| Value/Economic | Price and savings | "Premium clean at half the price" |
| Scarcity/Urgency | Time or stock pressure | "Limited edition — only 500 units" |

Select the top 3 angles based on objective alignment and audience resonance.

### Step 2 — Copy Framework Application

For each angle, generate copy using proven frameworks:

- **AIDA** (Attention → Interest → Desire → Action): Best for awareness and consideration
- **PAS** (Problem → Agitation → Solution): Best for conversion and retargeting
- **BAB** (Before → After → Bridge): Best for transformation narratives
- **4U** (Useful, Urgent, Unique, Ultra-specific): Best for direct response

Produce headline (5–8 words), body copy (15–30 words), and CTA (2–4 words) for each combination.

### Step 3 — CTA Variant Matrix

Generate CTA variants mapped to funnel stage:

| Funnel Stage | Soft CTAs | Hard CTAs |
|---|---|---|
| Awareness | "Learn More", "See How" | "Watch Now", "Discover" |
| Consideration | "Compare Options", "See Reviews" | "Try It Free", "Get Sample" |
| Conversion | "Add to Cart", "Shop Now" | "Buy Now — 20% Off", "Claim Your Deal" |
| Retargeting | "Still Thinking?", "Come Back" | "Complete Your Order", "Last Chance" |

### Step 4 — Platform-Specific Adaptation

Adapt each variant to platform specifications:

**Meta (Facebook/Instagram)**
- Primary text: 125 chars (above fold), up to 500 chars total
- Headline: 27 chars optimal, 40 max
- Formats: Single image (1080×1080), Carousel, Reels (9:16), Stories (9:16)
- Best practices: Lead with hook in first 3 seconds of video; UGC outperforms polished by 30%+

**TikTok**
- Copy overlay: 100 chars max on-screen
- Format: 9:16 vertical video, 15–60s
- Best practices: Native-feel content, trending audio, text-on-screen hooks, creator-style delivery
- Hook formula: "POV:", "Wait for it", "Things I wish I knew about..."

**Google (Search/Display/YouTube)**
- Search: Headline 30 chars × 3, Description 90 chars × 2
- Display: 1200×628, 300×250, 728×90, responsive display
- YouTube: 6s bumper, 15s non-skip, 30s skippable
- Best practices: Keyword insertion in headlines, benefit-led descriptions

**Pinterest**
- Title: 100 chars, Description: 500 chars
- Format: Standard pin (2:3), Idea pin, Video pin
- Best practices: Lifestyle imagery, text overlay with clear benefit, seasonal relevance

**Amazon (Sponsored Brands/DSP)**
- Headline: 50 chars, Custom image: 1200×628
- Best practices: Star rating inclusion, Prime badge, competitive pricing callout

### Step 5 — Variant Matrix Assembly

Assemble the full matrix:

```
Variant ID | Angle          | Framework | CTA Style | Platform | Format
V001       | Functional     | AIDA      | Hard      | Meta     | Static 1:1
V002       | Functional     | AIDA      | Soft      | Meta     | Carousel
V003       | Emotional      | BAB       | Hard      | Meta     | Reel 9:16
V004       | Social Proof   | PAS       | Hard      | TikTok   | Video 9:16
V005       | Problem-Agit.  | PAS       | Soft      | Google   | RSA
...
```

### Step 6 — Testing Roadmap

Structure variants into a phased testing plan:

- **Phase 1 (Week 1–2)**: Test 3 angles with consistent CTA → identify winning angle
- **Phase 2 (Week 3–4)**: Test 3 copy frameworks within winning angle → identify winning framework
- **Phase 3 (Week 5–6)**: Test CTA and format variants within winning angle+framework
- **Statistical rigor**: Minimum 1,000 impressions per variant, 95% confidence threshold, 7-day conversion windows

## Output Specification

1. **Variant Matrix Table**: All variants with ID, angle, framework, CTA, platform, format
2. **Full Copy Blocks**: For each variant — headline, body, CTA, character counts
3. **Visual Direction Notes**: Per variant — image/video concept, mood, composition guidance
4. **Platform Spec Sheet**: Dimensions, file types, character limits per platform
5. **Testing Roadmap**: Phased test plan with success criteria and decision rules
6. **Naming Convention**: Standardized UTM and ad naming taxonomy

## Examples

**Input**: "Generate ad variants for our new collagen protein powder. Target: women 28–45, health-conscious. Platforms: Meta and TikTok. Conversion-focused."

**Output**: 12-variant matrix across 3 angles (beauty-from-within, clean ingredients, daily ritual), PAS and AIDA frameworks, hard CTAs, with 6 Meta variants (3 static, 2 carousel, 1 Reel) and 6 TikTok variants (creator-style UGC scripts), plus a 6-week testing roadmap.

**Input**: "Refresh our laundry detergent ads — current winners are benefit-focused statics on Meta. Need new variants to fight fatigue."

**Output**: 8 iteration variants branching from the winning functional angle into emotional and social proof angles, introducing carousel and video formats, with A/B test structure preserving the control ad.

## Guidelines

- Every variant must be clearly differentiated — no near-duplicates that waste test budget
- Maintain brand voice consistency across variants; vary message, not personality
- Flag any copy that requires legal/compliance review (health claims, "free" offers, comparative claims)
- For CPG, always consider product-in-use imagery over product-only shots
- Include at least one UGC-style variant per platform — typically outperforms branded creative
- Never exceed platform character limits; provide exact character counts
- For regulated categories (supplements, food, beauty), include required disclaimer placement guidance
- Recommend minimum 3 variants per ad set for Meta's machine learning optimization

## Validation Checklist

- [ ] Minimum 3 distinct messaging angles represented
- [ ] Each variant has complete copy (headline, body, CTA) with character counts
- [ ] All platform specifications are accurate and current
- [ ] Visual direction is described for every variant
- [ ] No two variants are identical in angle + framework + CTA combination
- [ ] Testing roadmap includes sample size requirements and success criteria
- [ ] Naming convention is consistent and UTM-trackable
- [ ] Compliance-sensitive copy is flagged for review
