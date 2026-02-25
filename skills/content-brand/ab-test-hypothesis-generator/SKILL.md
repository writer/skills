---
name: A/B Test Hypothesis Generator
description: Generate statistically rigorous, testable hypotheses for e-commerce content optimization experiments across PDP copy, imagery, pricing presentation, enhanced content, and promotional messaging.

metadata:
  display_name: "A/b Test Hypothesis Generator"
  short_description: "Generate A/B test hypotheses for e-commerce content"
  default_prompt: "Generate a b test hypothesis for my case"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# A/B Test Hypothesis Generator

## Overview

This skill produces structured, testable hypotheses for content A/B tests on e-commerce platforms. It goes beyond "let's try a different headline" — generating hypotheses grounded in consumer psychology frameworks, competitive gap analysis, and statistical rigor. Each hypothesis includes the rationale, expected effect size, required sample size, and measurement plan.

Undisciplined testing wastes traffic and delays learning. This skill ensures every test has a clear thesis, a measurable outcome, and a path to statistically valid conclusions.

## When to Use

- Building a quarterly content testing roadmap for key SKUs or category pages.
- Diagnosing underperforming PDPs and generating optimization hypotheses.
- Evaluating the impact of brand voice, claim hierarchy, or imagery changes.
- Testing pricing presentation, promotional messaging, or urgency tactics.
- Validating localized content effectiveness in new markets.
- Prioritizing a backlog of potential tests by expected impact and effort.

## Required Inputs

| Input | Description | Example |
|---|---|---|
| `current_content` | Existing content (control variant) | Title, bullets, images, A+ |
| `performance_data` | Current metrics for the content | `{ "impressions": 50000, "clicks": 2000, "orders": 180, "ctr": 0.04, "cvr": 0.09 }` |
| `product_category` | Category benchmarks for context | "Oral Care", "Plant-Based Snacks" |
| `competitive_analysis` | Top competitor content and positioning | Competitor listing screenshots/text |
| `customer_insights` | Review themes, Q&A patterns, search terms | Aggregated customer feedback |
| `brand_constraints` | Non-negotiable brand elements | "Must include brand tagline", "No price anchoring" |
| `testing_platform` | Platform capabilities and limitations | "Amazon Manage Your Experiments", "Optimizely", "Google Optimize" |
| `traffic_volume` | Daily/weekly sessions for the test page | "~500 sessions/day" |
| `business_objectives` | Primary KPI to optimize | "Increase CVR", "Reduce return rate", "Improve AOV" |

## Methodology

### Step 1 — Performance Diagnostic

Analyze current content performance to identify optimization opportunities:

1. **Funnel Analysis**: Map the impression → click → detail page view → add-to-cart → purchase funnel. Identify the largest drop-off point.
2. **Benchmark Comparison**: Compare CTR and CVR against category averages and top performers.
3. **Heuristic Audit**: Score current content on the **Content Effectiveness Heuristic** (10 dimensions):
   - Relevance to search query | Visual hierarchy | Benefit clarity | Trust signals | Social proof | Urgency/scarcity | Differentiation | Readability | Mobile optimization | CTA strength
4. **Voice of Customer Mining**: Extract themes from reviews, Q&A, and search queries that reveal unmet information needs.

### Step 2 — Hypothesis Framework Construction

Every hypothesis must follow the **ICE-formatted hypothesis statement**:

```
IF we [change variable],
THEN [expected outcome] will [increase/decrease] by [estimated magnitude],
BECAUSE [behavioral or psychological rationale].
```

**Variable Categories**:

| Category | Testable Variables | Psychological Basis |
|---|---|---|
| **Title** | Keyword order, benefit-first vs. brand-first, specificity level | Anchoring effect, information scent |
| **Bullets** | FAB order, social proof inclusion, negative framing vs. positive | Loss aversion, social validation |
| **Description** | Story-driven vs. specification-driven, length, format | Narrative transportation, cognitive load |
| **Images** | Hero image angle, lifestyle vs. pack shot, infographic inclusion | Visual salience, mental simulation |
| **A+ Content** | Module order, comparison chart presence, video vs. static | Cognitive fluency, information architecture |
| **Pricing Display** | Per-unit pricing, subscribe & save prominence, bundle framing | Price anchoring, decoy effect |
| **Social Proof** | Review count display, UGC integration, expert endorsement | Bandwagon effect, authority bias |
| **Urgency** | Stock level indicators, limited-time offers, seasonal framing | Scarcity principle, FOMO |

### Step 3 — Hypothesis Generation Engine

Generate hypotheses using a systematic process:

1. **Gap Hypotheses**: Derived from the performance diagnostic — what's underperforming and why?
2. **Competitive Hypotheses**: Derived from competitor analysis — what are top performers doing differently?
3. **Customer-Driven Hypotheses**: Derived from VOC data — what information are shoppers seeking that we're not providing?
4. **Framework Hypotheses**: Derived from behavioral science principles applied to the specific product context.

For each hypothesis, document:

```yaml
hypothesis:
  id: "H-001"
  statement: "IF we lead bullet 1 with the clinical study result ('87% saw results in 2 weeks') instead of the ingredient feature ('Contains 20% Vitamin C'), THEN CVR will increase by 8-15%, BECAUSE social proof and outcome framing reduce perceived risk for first-time buyers."
  variable: "Bullet 1 — Opening phrase"
  control: "Current ingredient-led bullet"
  variant: "Clinical result-led bullet"
  primary_kpi: "CVR (unit session percentage)"
  secondary_kpis: ["Add-to-cart rate", "Glance views to detail page"]
  expected_effect: "+8-15% CVR"
  confidence: "medium"
  psychological_basis: "Social proof, outcome framing, risk reduction"
  evidence: "Review analysis shows 34% of shoppers ask about efficacy timeline"
```

### Step 4 — Statistical Design Specification

For each hypothesis, calculate the experimental design parameters:

1. **Minimum Detectable Effect (MDE)**: The smallest improvement worth detecting. Typically 5-15% relative lift for e-commerce content tests.
2. **Required Sample Size**: Based on baseline conversion rate, MDE, significance level (α = 0.05), and power (1-β = 0.80).

**Sample Size Formula** (two-proportion z-test):

```
n = (Z_α/2 + Z_β)² × [p1(1-p1) + p2(1-p2)] / (p1 - p2)²

Where:
  p1 = baseline conversion rate
  p2 = expected conversion rate (p1 × (1 + MDE))
  Z_α/2 = 1.96 (for α = 0.05)
  Z_β = 0.84 (for power = 0.80)
```

3. **Estimated Duration**: sample_size / daily_traffic. Add 1-2 full business weeks to account for day-of-week effects.
4. **Traffic Allocation**: Default 50/50 split. Consider 70/30 or 80/20 for high-risk tests to limit downside exposure.
5. **Stopping Rules**: Do not peek at results before minimum sample size is reached. Use sequential testing methods (e.g., always-valid p-values) if interim checks are needed.

### Step 5 — Prioritization (ICE Scoring)

Rank all generated hypotheses using the **ICE Framework**:

| Factor | Score (1-10) | Definition |
|---|---|---|
| **Impact** | 1-10 | Expected effect size × revenue potential |
| **Confidence** | 1-10 | Strength of supporting evidence and rationale |
| **Ease** | 1-10 | Implementation complexity and resource requirement |

**ICE Score** = (Impact + Confidence + Ease) / 3. Run highest-scoring hypotheses first.

### Step 6 — Test Execution Guardrails

Define pre-registration criteria for each test:

1. **Primary metric**: One and only one primary KPI for the statistical test.
2. **Secondary metrics**: Additional metrics tracked but not used for win/loss decisions.
3. **Guardrail metrics**: Metrics that must not degrade (e.g., return rate, customer satisfaction).
4. **Decision framework**: Pre-define what constitutes a winner, loser, or inconclusive result.
   - Winner: Primary KPI improves with p < 0.05 and no guardrail metric degradation.
   - Loser: Primary KPI degrades with p < 0.05.
   - Inconclusive: p ≥ 0.05 after full duration — log learnings, generate follow-up hypothesis.

## Output Specification

```yaml
output:
  hypotheses: list[Hypothesis]
  prioritized_ranking: list[string]    # Hypothesis IDs ranked by ICE score
  testing_roadmap:
    - quarter: string
      tests: list[string]             # Hypothesis IDs to run
  total_hypotheses_generated: int
  estimated_total_test_duration: string # "8-12 weeks for top 5 tests"
  traffic_feasibility: string          # "sufficient" | "marginal" | "insufficient"
  sample_size_calculations: dict       # Per-hypothesis sample requirements
  expected_cumulative_lift: string     # Estimated total CVR improvement if winners found
```

## Analysis Framework

**Testing Maturity Model**:

| Level | Practice | Typical Organization |
|---|---|---|
| **Level 1 — Ad Hoc** | Random tests, no documentation, results not tracked | Small brand, 1 person team |
| **Level 2 — Structured** | Hypotheses documented, basic statistical rigor | Growing brand, dedicated content person |
| **Level 3 — Programmatic** | Testing roadmap, ICE prioritization, learning repository | Mid-market brand, CRO function |
| **Level 4 — Optimized** | Continuous testing, Bayesian methods, personalization | Enterprise, dedicated experimentation team |

This skill targets Level 2-3 maturity for most CPG brands.

## Examples

**Scenario**: Organic protein powder on Amazon. Current CVR: 8.2%. Category avg: 11.5%.

**Generated Hypotheses (Top 3)**:

1. **H-001**: IF we add "30-Day Money-Back Guarantee" as bullet 5, THEN CVR will increase by 10-20%, BECAUSE 28% of negative reviews cite taste concerns, and risk reversal addresses purchase hesitation. ICE: 8.7.

2. **H-002**: IF we change the hero image from pack shot to lifestyle (person mixing shake post-workout), THEN CTR will increase by 5-12%, BECAUSE mental simulation of product use increases purchase intent. ICE: 7.3.

3. **H-003**: IF we restructure A+ Content to lead with a comparison chart (our 3 flavors side-by-side) instead of brand story, THEN CVR will increase by 5-10%, BECAUSE shoppers in consideration phase need help choosing a variant. ICE: 7.0.

## Guidelines

- Never test more than one variable at a time unless running a proper multivariate test with adequate traffic.
- Respect statistical significance — a test with p = 0.08 is NOT a winner. Log the learning and move on.
- Account for novelty effects — new content may spike initially then regress. Run tests for a minimum of 2 full weeks.
- Not everything needs a test — obvious improvements (fixing typos, adding missing info) should be deployed directly.
- Build a **learning repository** — even failed tests generate valuable insights for future hypotheses.
- Consider downstream metrics — a CVR increase means nothing if return rate spikes proportionally.

## Validation Checklist

- [ ] Every hypothesis follows the IF/THEN/BECAUSE format with specific variables.
- [ ] Psychological or behavioral rationale is cited for each hypothesis.
- [ ] Sample size calculations are provided with stated assumptions (α, β, MDE).
- [ ] Estimated test duration accounts for day-of-week effects and minimum run time.
- [ ] ICE scores are calculated and hypotheses are prioritized.
- [ ] Primary KPI, secondary metrics, and guardrail metrics are defined per test.
- [ ] Decision framework (winner/loser/inconclusive criteria) is pre-registered.
- [ ] Traffic feasibility is assessed — sufficient daily volume to reach significance in reasonable time.
- [ ] Testing roadmap sequences tests to avoid conflicts and maximize learning velocity.
- [ ] Stopping rules prevent premature peeking and false positive conclusions.
