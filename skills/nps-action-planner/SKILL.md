---
name: NPS Action Planner
description: Recommend targeted actions from Net Promoter Score data by segmenting promoters, passives, and detractors, analyzing their feedback drivers, and generating prioritized intervention plans to shift customers up the loyalty spectrum.

metadata:
  display_name: "Nps Action Planner"
  short_description: "Turn NPS feedback into prioritized improvement actions"
  default_prompt: "Optimize my nps action and suggest the best next steps"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# NPS Action Planner

## Overview

This skill transforms Net Promoter Score data from a backward-looking metric into a forward-looking action plan. It segments respondents into promoters (9-10), passives (7-8), and detractors (0-6), analyzes the specific drivers behind each group's scores, and generates targeted intervention plans designed to convert detractors to passives, passives to promoters, and activate promoters as brand advocates. Each recommendation is sized by expected NPS point impact and business value.

## When to Use

- After each NPS survey wave to develop the response action plan
- When NPS trends downward and leadership requires a recovery roadmap
- When NPS varies significantly across segments, channels, or touchpoints and requires tailored strategies
- To design closed-loop feedback programs that address individual detractor concerns
- When building the business case for CX investments by linking NPS to financial outcomes
- To develop promoter activation strategies (referral programs, review solicitation, advocacy programs)

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `nps_responses` | Individual survey responses with score (0-10), timestamp, customer ID | Tabular |
| `respondent_attributes` | Customer segment, tenure, lifetime value, channel preference, recency | Tabular |
| `verbatim_feedback` | Open-ended text from NPS survey ("What is the primary reason for your score?") | Text field |
| `transaction_history` | Purchase history for respondents (frequency, recency, monetary value) | Tabular |
| `touchpoint_nps` | NPS collected at specific touchpoints (post-purchase, post-support, post-delivery) | Tabular (optional) |
| `historical_nps` | At least 4 quarters of historical NPS data for trend analysis | Time series |
| `competitive_nps` | Industry and competitor NPS benchmarks | Reference data (optional) |
| `financial_data` | Revenue, margin, and retention rates by NPS segment | Tabular (optional) |

## Methodology

### Step 1 — NPS Decomposition and Segmentation

Analyze the NPS score structure:

1. **Score Distribution Analysis**: Plot the full 0-10 distribution, not just the NPS number. Two brands can have the same NPS with very different distributions — a bimodal distribution (many 9-10s and many 0-3s) requires different actions than a concentrated distribution (mostly 7-8s).
2. **Segment-Level NPS**: Calculate NPS for each meaningful customer segment (by value tier, tenure cohort, acquisition channel, geography, product category purchased).
3. **Touchpoint NPS**: If available, compare NPS collected at different journey stages. Identify which touchpoints create the most detractors and which create the most promoters.
4. **Trend Analysis**: Decompose NPS trend into promoter rate change, detractor rate change, and passive rate change. Identify which movement is driving the overall NPS trend.
5. **Financial Linkage**: Calculate the revenue and margin differential between promoters, passives, and detractors. Quantify the lifetime value gap to make the business case for score improvement.

### Step 2 — Driver Analysis by NPS Group

Understand what drives each group's score:

1. **Detractor Driver Analysis**:
   - Apply topic modeling to detractor verbatims to identify primary pain themes.
   - Rank themes by prevalence and sentiment intensity.
   - Cross-reference with operational data to identify the specific experience failures.
   - Categorize detractors: "Recoverable" (had a fixable bad experience) vs. "Structural" (fundamental misalignment with brand/product).

2. **Passive Driver Analysis**:
   - Passives are the most actionable group — they are satisfied but not loyal.
   - Analyze what differentiates passives who later become promoters from those who become detractors.
   - Identify the "missing delight" — what promoters mention that passives do not.
   - Look for unmet expectations rather than failed expectations.

3. **Promoter Driver Analysis**:
   - Identify the primary reasons for promoter enthusiasm from verbatims.
   - Segment promoters by activation potential (do they actually refer, review, or repurchase at higher rates?).
   - Identify "vulnerable promoters" — those whose scores are declining over successive surveys.

### Step 3 — Action Plan Development

Create targeted interventions for each group:

1. **Detractor Recovery Program**:
   - **Closed-Loop Follow-Up**: Design outreach protocol for detractors within 48 hours. Script empathetic outreach, provide resolution authority, and track recovery rate (percentage of detractors who improve their score on re-survey).
   - **Systemic Fix**: For the top 3 detractor themes, develop process or policy changes that prevent recurrence.
   - **Recovery Target**: Aim to recover 30-40% of detractors to passive or promoter status within 90 days.

2. **Passive Conversion Program**:
   - **Delight Injection**: Identify 2-3 low-cost, high-impact experience enhancements that would differentiate the brand experience for passives.
   - **Personalization**: Use purchase and preference data to deliver more relevant communications, offers, and experiences.
   - **Engagement Deepening**: Encourage passives to engage with more brand touchpoints (loyalty program, app, events) — multi-touchpoint customers are 3-4x more likely to be promoters.
   - **Conversion Target**: Aim to convert 15-20% of passives to promoters within 6 months.

3. **Promoter Activation Program**:
   - **Referral Mechanics**: Design or optimize referral programs that make it easy for promoters to share (pre-written messages, unique referral codes, mutual incentives).
   - **Review Solicitation**: Trigger review requests to promoters at the right moment (post-delivery confirmation, after repeat purchase).
   - **Advocacy Community**: Invite high-value promoters into VIP or ambassador programs.
   - **Activation Target**: Aim for 25%+ of promoters to take at least one advocacy action within 90 days.

### Step 4 — Impact Modeling

Estimate the NPS and financial impact of each action:

1. **NPS Point Impact**: Model the NPS change if X% of detractors are recovered and Y% of passives are converted, using the formula: NPS = %Promoters - %Detractors.
2. **Revenue Impact**: Apply the lifetime value differential between NPS groups to the expected group migration. Include incremental referral revenue from activated promoters.
3. **Cost-Benefit Analysis**: Compare intervention costs against expected financial returns. Prioritize actions with the highest NPS-point-per-dollar-invested ratio.
4. **Scenario Modeling**: Present conservative, moderate, and aggressive scenarios with different conversion rate assumptions.

### Step 5 — Monitoring and Iteration

Define the ongoing measurement framework:

- **Leading Indicators** (weekly): Closed-loop contact rate, detractor response rate, referral program enrollment, review submission rate.
- **Lagging Indicators** (quarterly): NPS score movement, segment migration rates, retention rate changes, referral revenue.
- **Feedback Loop**: After each survey wave, update driver analysis, recalibrate action priorities, and document what worked.

## Output Specification

Produce an NPS action plan containing:

- `current_nps`: Overall NPS with promoter, passive, and detractor percentages
- `nps_trend`: Quarterly NPS trend with decomposition into promoter/passive/detractor rate changes
- `financial_linkage`: Revenue and lifetime value by NPS group with total addressable opportunity
- `detractor_analysis`: Top themes, prevalence, severity, recoverability assessment, and specific verbatim examples
- `passive_analysis`: Differentiators from promoters, missing delight factors, and conversion opportunity sizing
- `promoter_analysis`: Enthusiasm drivers, activation potential, and vulnerable promoter identification
- `action_plan`: Prioritized array of interventions, each with target group, action description, owner role, timeline, estimated NPS point impact, estimated financial impact, and implementation cost
- `scenario_models`: Conservative, moderate, and aggressive impact projections with assumptions stated
- `monitoring_dashboard`: Leading and lagging KPIs with targets and measurement cadence

## Analysis Framework

Apply the **NPS Loyalty Spectrum** model:

- **Score 0-3 (Hostile Detractors)**: Actively warning others away. Priority: damage containment and root cause elimination. Low recovery probability — focus on preventing new customers from reaching this state.
- **Score 4-6 (Disappointed Detractors)**: Dissatisfied but not hostile. Priority: closed-loop recovery. Moderate recovery probability if outreach is swift and empathetic.
- **Score 7 (Low Passives)**: Satisfied but with unresolved friction. One bad experience away from becoming a detractor. Priority: friction removal.
- **Score 8 (High Passives)**: Satisfied and open to deeper engagement. Closest to the promoter threshold. Priority: delight injection and engagement deepening.
- **Score 9 (Moderate Promoters)**: Loyal and willing to recommend if asked, but unlikely to proactively advocate. Priority: make advocacy easy and rewarding.
- **Score 10 (Enthusiastic Promoters)**: Actively advocating. Priority: amplify their voice, protect their experience, and recognize their loyalty.

Each score band requires a differentiated strategy. Treating all detractors or all promoters the same wastes resources.

## Examples

**Example NPS Action Plan Summary**:

Current NPS: +32 (Promoters 48%, Passives 36%, Detractors 16%). Down from +38 last quarter.

Decline driver: Detractor rate increased from 12% to 16%, concentrated in ship-to-home customers (detractor rate 22% vs. 8% in-store). Primary detractor theme: "Delivery took much longer than promised" (mentioned in 43% of detractor verbatims).

Action Plan Priority 1 — Detractor Recovery: Implement 48-hour closed-loop callback for all delivery-related detractors. Estimated recovery rate: 35%. Impact: -2.2 percentage points on detractor rate, contributing +2.2 NPS points.

Action Plan Priority 2 — Passive Conversion: Launch post-purchase personalized recommendation emails for score-8 passives. Promote loyalty program enrollment with exclusive early access benefit. Estimated conversion: 18% of high passives to promoter. Impact: +1.8 NPS points.

Action Plan Priority 3 — Promoter Activation: Deploy one-click review solicitation SMS to promoters 3 days post-delivery. Include dual-sided referral incentive ($10 for referrer, $10 for friend). Estimated activation: 28% of promoters take one action. Revenue impact: $340K incremental annual referral revenue.

Combined scenario (moderate): NPS improvement from +32 to +36 over 2 quarters.

## Guidelines

- NPS is a relationship metric, not a transactional one. Interpret it in the context of overall brand perception, not just the last transaction.
- Always report NPS with the underlying score distribution, not just the headline number. Two identical NPS scores can require completely different strategies.
- Apply minimum sample sizes: overall NPS requires n >= 200 for reliability; segment-level NPS requires n >= 50 per segment.
- Closed-loop follow-up with detractors should happen within 48 hours. Recovery rates decline sharply after 72 hours.
- Do not incentivize survey completion in ways that bias scores upward (e.g., "rate us 10 and get a coupon"). This corrupts the data.
- Link NPS actions to financial outcomes — NPS improvement without revenue or retention improvement is not valuable.
- Passives deserve as much strategic attention as detractors. They are the swing vote in NPS and often represent the largest group.
- Protect promoter experience fiercely — losing a promoter costs more than gaining one, because they take their advocacy network with them.
- Update driver analysis each survey wave — the drivers of NPS shift over time as issues are resolved and new ones emerge.

## Validation Checklist

- [ ] NPS calculated correctly using standard methodology (% Promoters minus % Detractors)
- [ ] Sample size is adequate for overall and segment-level analysis (minimum thresholds documented)
- [ ] Score distribution is reported alongside the headline NPS number
- [ ] Driver analysis covers all three groups (detractors, passives, promoters) with differentiated insights
- [ ] Verbatim analysis uses systematic topic modeling, not manual cherry-picking
- [ ] Financial linkage quantifies the LTV differential between NPS groups
- [ ] Action plan includes interventions for all three groups with specific owners and timelines
- [ ] Impact estimates use conservative assumptions and state conversion rate sources
- [ ] Scenario modeling presents at least two scenarios (conservative and moderate)
- [ ] Monitoring plan includes both leading and lagging indicators with measurement cadence
