---
name: Omnichannel Journey Mapper
description: Map and analyze customer journeys across digital and physical retail channels, identifying moments of truth, friction points, and channel-transition breakdowns to optimize end-to-end omnichannel experience.

metadata:
  display_name: "Omnichannel Journey Mapper"
  short_description: "Map omnichannel customer journeys and friction points"
  default_prompt: "Map my omnichannel journey and show key friction points and improvements"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Omnichannel Journey Mapper

## Overview

This skill constructs detailed customer journey maps that span all retail touchpoints — web, mobile app, social, email, contact center, and physical store — to reveal how customers actually navigate across channels. It identifies moments of truth (high-impact interactions), friction points (where customers struggle or abandon), and channel-transition failures (where context is lost between touchpoints). The output enables retailers to prioritize CX investments where they will have maximum impact on conversion, retention, and lifetime value.

## When to Use

- Designing or redesigning omnichannel customer experiences
- Diagnosing why customers drop off during cross-channel journeys (e.g., browse online, abandon in-store)
- Evaluating the effectiveness of BOPIS (buy online, pick up in-store), ship-from-store, or curbside programs
- Preparing for omnichannel capability investments and building business cases
- Understanding post-purchase journey gaps (returns, exchanges, support)
- Benchmarking journey quality against competitive or best-in-class standards

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `customer_events` | Timestamped interaction events across channels with session/customer ID | Event stream (JSON/CSV) |
| `channel_definitions` | List of channels with attributes (digital/physical, owned/earned) | Reference data |
| `transaction_data` | Purchase records linked to customer ID and originating channel | Tabular |
| `support_interactions` | Contact center, chat, and in-store service desk records | Tabular |
| `digital_analytics` | Page views, clicks, search queries, cart actions from web/app | Event stream |
| `customer_segments` | Segment definitions with behavioral and demographic attributes | Reference data |
| `nps_csat_data` | Survey responses linked to journey stage or touchpoint | Tabular (optional) |
| `store_experience_data` | Mystery shop scores, wait times, associate interactions | Tabular (optional) |

## Methodology

### Step 1 — Journey Event Stitching

Unify customer interactions across channels into coherent journey sequences:

1. **Identity Resolution**: Link events using customer ID, loyalty ID, device fingerprint, email, and cookie graphs. Apply probabilistic matching where deterministic links are unavailable, with confidence thresholds.
2. **Session Construction**: Group events into sessions by channel with 30-minute inactivity timeout for digital and visit-level grouping for physical stores.
3. **Journey Threading**: Connect sessions into end-to-end journeys using intent signals (search queries, category browsing patterns, wishlist activity) to identify journeys pursuing the same purchase intent.
4. **Timeline Assembly**: Arrange all events chronologically with channel labels, creating the raw journey timeline.

### Step 2 — Journey Pattern Mining

Identify the most common and most impactful journey patterns:

1. **Sequence Analysis**: Use sequential pattern mining to find the most frequent channel sequences (e.g., Social Ad > Mobile Browse > Desktop Cart > Store Purchase).
2. **Journey Clustering**: Group journeys by shape (number of touchpoints, channel diversity, duration) using k-means or hierarchical clustering.
3. **Conversion Path Analysis**: Identify which journey patterns have the highest and lowest conversion rates, controlling for purchase intent strength.
4. **Channel Attribution**: Apply data-driven attribution (Shapley value or Markov chain) to determine each channel's contribution to conversion.

### Step 3 — Moment of Truth Identification

Pinpoint the interactions that disproportionately determine journey outcomes:

- **Statistical Impact Analysis**: For each touchpoint type, compare conversion rates of journeys that include it vs. those that do not. Control for journey length and customer segment.
- **Emotion Mapping**: Overlay CSAT/NPS data collected at specific touchpoints to identify where emotional highs and lows occur.
- **Failure Point Detection**: Identify touchpoints where more than 30% of journeys terminate without conversion — these are primary friction points.
- **Moment Categories**:
  - **Discovery Moments**: First meaningful engagement that creates purchase consideration.
  - **Evaluation Moments**: Product comparison, review reading, in-store trial that builds confidence.
  - **Commitment Moments**: Add-to-cart, checkout initiation, or associate-assisted sale closure.
  - **Fulfillment Moments**: Order confirmation, pickup/delivery, unboxing experience.
  - **Advocacy Moments**: Post-purchase review, social sharing, referral actions.

### Step 4 — Channel Transition Analysis

Evaluate how effectively the experience maintains continuity across channel switches:

1. **Context Persistence Score**: Measure whether customer context (cart contents, browsing history, loyalty status) is maintained when switching channels. Score from 0 (no context transferred) to 100 (full context continuity).
2. **Transition Friction Index**: Calculate the abandonment rate at each channel transition point. High-friction transitions include: mobile to desktop (cart not synced), online to store (no visibility into online browsing), store to contact center (no interaction history available).
3. **Handoff Quality**: For assisted transitions (e.g., online chat transfers to phone, digital lead to in-store appointment), measure whether the receiving channel had the information needed to continue seamlessly.
4. **Recovery Analysis**: When a journey encounters friction at a transition, identify whether the customer recovered (continued the journey) or abandoned, and what factors predicted recovery.

### Step 5 — Journey Map Visualization and Recommendations

Produce the final journey map with actionable insights:

1. **Swim Lane Diagram**: Channels as horizontal lanes, journey stages as vertical columns, with customer flow volume shown by line thickness.
2. **Friction Heat Map**: Overlay a heat map showing where abandonment and negative sentiment concentrate.
3. **Opportunity Sizing**: For each friction point, estimate the revenue impact of fixing it based on the volume of affected journeys and the average order value at stake.
4. **Prioritized Recommendations**: Rank improvements by (revenue impact x feasibility) / implementation cost.

## Output Specification

Produce a journey analysis object containing:

- `journey_patterns`: Array of discovered journey types, each with sequence of touchpoints, frequency count, conversion rate, average duration, and average order value
- `moments_of_truth`: Array of high-impact touchpoints, each with touchpoint name, channel, journey stage, impact score (correlation with conversion), current satisfaction score, and volume of journeys affected
- `friction_points`: Array of identified friction areas, each with location in journey, abandonment rate, primary cause, estimated revenue at risk, and recommended fix
- `channel_transitions`: Array of transition points between channels, each with from-channel, to-channel, volume, context persistence score, friction index, and recommended improvement
- `segment_variations`: Object showing how journey patterns differ across customer segments
- `recommendations`: Prioritized array of improvement actions with expected impact, effort estimate, and implementation dependencies

## Analysis Framework

Apply the **5E Journey Framework**:

1. **Entice**: How does the customer become aware and interested? Channels: paid media, social, search, email, word-of-mouth.
2. **Enter**: How does the customer begin actively engaging? Touchpoints: site landing, app open, store entry, catalog browse.
3. **Engage**: How does the customer evaluate and build purchase intent? Interactions: product pages, reviews, fitting rooms, associate conversations, comparison tools.
4. **Exit**: How does the customer complete the transaction? Checkout: online payment, POS transaction, BOPIS order, phone order.
5. **Extend**: How does the relationship continue post-purchase? Follow-up: delivery tracking, returns process, loyalty program, replenishment, reviews.

Map every touchpoint to one of the 5Es, then analyze each stage for completeness, quality, and cross-channel continuity.

## Examples

**Example Journey Pattern Analysis**:

Pattern: "Research Online, Buy In-Store" (ROPO) — 23% of all journeys.

Typical sequence: Google Search > Product Page (Mobile) > Store Locator > In-Store Visit > POS Purchase. Average duration: 4.2 days. Conversion rate: 34% (vs. 12% for pure digital). Average order value: $127 (vs. $89 online-only).

Key friction point: Store Locator to In-Store Visit transition shows 58% drop-off. Root cause analysis reveals: (1) inventory availability not shown on store locator (customers arrive to find item out of stock), (2) no mechanism to save the online research to recall in-store.

Recommendation: Implement real-time inventory visibility on product pages and store locator. Enable "Save to My Store" feature that sends browsing history to store associate's clienteling tool. Estimated impact: +8% conversion on ROPO journeys, representing $2.4M incremental annual revenue.

## Guidelines

- Always ground journey maps in actual behavioral data, not assumed or idealized journeys. Aspirational journeys are a separate exercise.
- Ensure identity resolution methodology is documented and privacy-compliant (GDPR, CCPA). Use anonymized customer IDs in outputs.
- Weight journey patterns by revenue contribution, not just frequency. A rare high-value journey may deserve more attention than a common low-value one.
- Acknowledge data gaps honestly. If in-store behavior is poorly instrumented, note the gap rather than inferring behavior.
- Separate journey analysis by customer segment — new vs. returning, high-value vs. occasional, digital-native vs. store-first.
- Include emotional states alongside behavioral data where survey data supports it. Behavior tells you what happened; emotion tells you why.
- Validate journey maps with frontline staff (store associates, contact center agents) who observe customer behavior firsthand.
- Do not conflate correlation with causation when identifying moments of truth — use controlled experiments where possible.

## Validation Checklist

- [ ] Identity resolution covers at least 70% of multi-channel journeys with high-confidence matches
- [ ] Journey patterns account for at least 80% of total journey volume
- [ ] Moments of truth are validated with statistical significance testing (p < 0.05)
- [ ] Friction points include both quantitative (abandonment rate) and qualitative (satisfaction) evidence
- [ ] Channel transitions are scored for context persistence using actual data, not assumptions
- [ ] Revenue impact estimates use conservative assumptions with stated confidence intervals
- [ ] Recommendations are prioritized by impact-to-effort ratio with implementation dependencies noted
- [ ] Privacy compliance is confirmed — no PII in journey map outputs
- [ ] Segment-level variations are analyzed for at least the top 3 customer segments
- [ ] Journey maps have been cross-referenced with frontline qualitative feedback
