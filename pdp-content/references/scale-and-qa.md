# Catalog-Scale PDP Program: Workflow & QA

At thousands of SKUs, quality comes from the **system** (data, templates, checks, sampling), not from heroic editing. Fix problems at the source. When the same issue shows up across many SKUs, change the template, the prompt or the data. Don't patch pages one at a time.

## Phase 1 — Data readiness
- **Profile the data.** Check fill rate per attribute and per category, inconsistent units and values ("Blue", "blue", "BLU"), conflicting fields, and missing variant links.
- **Define the minimum attribute set per category** needed to write a compliant, useful PDP. SKUs below the minimum go to a **data-gap queue**, not to generation.
- **Load the approved claims list per category** and the banned-terms list.

## Phase 2 — Templates and golden set
- **Templates per category and channel:** which attributes feed the title formula, which bullet topics, description structure, required disclaimers.
- **Golden set:** about 10–30 SKUs covering each category, the edge cases (bundles, multipacks, regulated items, variants) and sparse data. Write or approve these by hand with merchandising, brand and legal. They become the reference examples for generation and for QA.
- **Pilot:**
  1. Generate the pilot set.
  2. Do a full human review.
  3. Record every correction by type.
  4. Update the templates and prompts until the pilot passes the hard gates with only minor edits.

## Phase 3 — Batch generation with automated checks
Run these checks on every SKU before human review:

| Check | Fails when |
|---|---|
| Attribute fidelity | Any number, unit, material, certification or compatibility claim in the copy isn't in the source attributes, or differs from them |
| Variant consistency | Copy mentions a size, color or count that doesn't match that SKU |
| Restricted claims | Copy contains terms from the category's restricted list without approved wording |
| Banned / promotional terms | Channel-prohibited language (price, shipping, "best seller", "sale", time-sensitive words) |
| Length and format limits | Any field exceeds the channel limit, or required fields are missing |
| Placeholders | `[ATTR NEEDED]`, `TBD`, `{…}`, leftover template text |
| Duplication | Near-duplicate copy across sibling SKUs or against the manufacturer's source text above an agreed threshold |
| Locale formatting | Wrong units, decimal separators or currency for the market |
| Readability | Walls of text, keyword lists, repeated phrases |

Blocked SKUs go back to the data queue or the template queue, depending on the cause.

## Phase 4 — Human review by risk
- **Sample** a share of each batch that passed the automated checks, stratified by category. Something like 5–10% is a reasonable starting point.
- **Review 100%** of regulated categories, new categories, high-revenue hero SKUs, and anything with a compliance flag.
- **Escalate the sample** if it shows errors. One error type found in a sample means checking every SKU produced by the same template.
- **Record the reviewer's decision and edits.** The edits feed template improvements.

## Phase 5 — Staged rollout and monitoring
- Publish in batches. Start with a subset and monitor before expanding.
- **Monitor:**
  - retailer suppressions and rejections
  - feed disapprovals
  - search impressions and rankings for the affected pages
  - conversion and add-to-cart rates
  - returns coded "not as described"
  - customer questions about facts that the copy should already have answered
- **Testing copy changes** (method: `b2b-content-and-campaigns/references/testing-and-diagnosis.md`): only with enough traffic and conversions for a valid test. Otherwise use before/after comparisons, clearly labeled directional, with seasonality and promotions noted.
- **Refresh triggers:**
  - attribute changes in the PIM, which must regenerate the affected copy
  - new claims approvals
  - retailer rule changes
  - persistent review themes

## Localization at scale
- **Translate** specs and factual content precisely. **Transcreate** titles and benefit lines for search behavior and culture. Use **legally required wording** for compliance text in each market.
- **Run locale-specific checks:** units, character expansion against field limits, required local elements, and the market's claims rules (EU environmental claims, for example).
- **Native-speaker review** for each new market and category during the pilot. After that, sample.

See the localization QA reference in `customer-facing-quality-gate`.

## Reporting to stakeholders
- **Coverage:** SKUs live / in review / blocked, by category and channel.
- **Quality:** hard-gate pass rate, sample error rate by type, trend over time.
- **Data health:** top missing attributes and the SKU count affected by each. This is often the most valuable output for the business.
- **Impact:** metrics measured honestly against baselines, with directional results labeled as such.
