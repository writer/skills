---
name: enterprise-risk-heatmap-narratives
description: Generate enterprise risk heatmap narratives for financial institutions. Use when preparing board risk reports, writing risk appetite commentary, creating risk trend narratives for ERM dashboards, explaining risk rating changes, or producing committee-ready enterprise risk assessments aligned with COSO ERM 2017 and OCC Heightened Standards.

metadata:
  display_name: "Enterprise Risk Heatmap Narratives"
  short_description: "Write enterprise risk heatmap narratives for bank boards"
  default_prompt: "Summarize my enterprise risk heatmap with key findings and next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Enterprise Risk Heatmap Narratives

## Overview

Generate clear, insightful narratives to accompany enterprise risk heatmaps and dashboards for board and senior management consumption. This skill applies the COSO Enterprise Risk Management Framework (2017), OCC Heightened Standards (12 CFR 30 Appendix D), and Basel Committee operational risk guidance to translate quantitative risk assessments into compelling, actionable narratives that support informed risk governance and strategic decision-making.

## When to Use

- Preparing enterprise risk heatmap narratives for board risk committee reports
- Writing risk appetite and tolerance commentary for quarterly risk dashboards
- Explaining risk rating changes (upgrades, downgrades) with supporting rationale
- Creating risk trend narratives for emerging and evolving risks
- Producing top and emerging risk narratives for senior management risk forums
- Developing risk interconnection narratives showing cascading risk relationships

## Required Inputs

- **Risk register**: Current risk inventory with categories, ratings, trends, and owners
- **Risk appetite framework**: Board-approved appetite statements, tolerance thresholds, capacity limits
- **Risk assessment data**: Inherent and residual ratings, likelihood/impact scores, velocity assessments
- **Key risk indicators (KRIs)**: Current values, thresholds, trend data
- **Risk event data**: Recent operational losses, near-misses, emerging risk triggers
- **Strategic context**: Business strategy, growth initiatives, market conditions

## Methodology

### Step 1: Risk Taxonomy and Heatmap Structure

Organize the heatmap using a risk taxonomy aligned with COSO ERM 2017: Credit Risk (lending, counterparty, concentration), Market Risk (interest rate, equity, FX), Liquidity Risk (funding, market, contingent), Operational Risk (process, people, systems, fraud), Compliance Risk (regulatory, legal, conduct, financial crimes), Strategic Risk (business model, competitive, M&A), Reputation Risk (customer trust, media, ESG), Technology Risk (cyber, data, infrastructure), Model Risk (development, validation, usage).

**Heatmap axes**: Likelihood (1-Rare to 5-Almost Certain) × Impact (1-Insignificant to 5-Severe), with Velocity overlay (Rapid <30 days, Moderate 1-6 months, Gradual >6 months). Color coding: Critical (Red, 20-25), High (Orange, 12-19), Medium (Yellow, 5-11), Low (Green, 1-4).

### Step 2: Individual Risk Narrative Development

For each risk, develop a structured narrative containing:

1. **Current state assessment** (2-3 sentences): Current risk level with specific KRI values and recent events
2. **Trend driver explanation** (2-3 sentences): Internal and external factors driving the trend
3. **Risk appetite comparison** (1-2 sentences): Position relative to board-approved appetite/tolerance
4. **Key controls and mitigants** (2-3 sentences): Primary controls and their operating effectiveness
5. **Forward-looking assessment** (2-3 sentences): Expected trajectory and emerging factors
6. **Management actions** (1-3 sentences): Actions underway or planned with timelines

Prefix each narrative with: Risk name/category, Rating (Inherent → Residual), Trend (↑→↓), Velocity, Risk Appetite Status (Within/Approaching/Exceeding).

### Step 3: Risk Trend and Movement Analysis

Document rating changes with: prior and current rating with effective date, specific evidence-based rationale, triggering events or KRI breaches, governance approval process, impact on overall risk profile, and consequential cascading effects on related risks.

### Step 4: Risk Appetite and Tolerance Commentary

For each risk category, provide: appetite statement in measurable terms, current position relative to appetite/tolerance/capacity, tolerance proximity quantification, and breach reporting with management response and remediation timeline.

Traffic light reporting: Green (within appetite, standard monitoring), Yellow (approaching tolerance, enhanced monitoring required), Orange (at/exceeding tolerance, immediate action and board notification), Red (exceeding tolerance approaching capacity, emergency response with board-approved remediation).

### Step 5: Risk Interconnection Narrative

Document risk interconnections and cascading effects: identify primary interconnections (e.g., cyber → operational → reputation → strategic), describe plausible cascading scenarios, assess whether risk management accounts for interconnections or operates in silos, and highlight concentration risks spanning multiple categories.

### Step 6: Emerging and Top Risk Narratives

For emerging risks: description and relevance, horizon (near/medium/long-term), potential impact, monitoring indicators, preparedness assessment, and recommended actions. For top risks: rank top 10 with clear methodology, include full narrative elements, articulate board-level actions required, and compare to prior period.

### Step 7: Executive Summary and Board-Ready Compilation

Compile: executive summary (1 page with overall posture, key changes, board action items), risk appetite dashboard with traffic lights, top risks with brief narratives, emerging risks, rating changes summary, interconnection scenarios, and management action status.

## Output Specification

```markdown
# Enterprise Risk Report — [Reporting Period]

## Executive Summary
[1-page overview: enterprise risk posture, key themes, items for board action]

## Risk Appetite Dashboard
| Risk Category | Appetite | Current Position | Status | Trend |

## Top Risks
### 1. [Risk Name]
**Rating**: [Inherent] → [Residual] | **Trend**: [↑↓→] | **Velocity**: [speed]
[Full narrative per Step 2 structure]

## Risk Rating Changes
| Risk | Prior | Current | Direction | Driver | Governance Approval |

## Emerging Risks
[Narrative per Step 6 structure]

## Risk Interconnections
[Cascading scenarios and aggregate exposure assessment]

## Management Actions Summary
| Risk | Action | Owner | Status | Target Date |
```

## Analysis Framework

| Dimension | Strong Narrative | Weak Narrative |
|-----------|-----------------|----------------|
| Specificity | Data-driven with KRI references | Vague generalizations |
| Actionability | Clear actions with owners and timelines | Descriptive only, no accountability |
| Forward-looking | Emerging trends, trajectory forecast | Backward-looking, current state only |
| Interconnection | Cascading relationships, aggregate impacts | Each risk treated in isolation |
| Board relevance | Strategic implications, decisions needed | Operational detail inappropriate for board |
| Consistency | Uniform terminology and methodology | Inconsistent ratings, undefined terms |

## Examples

**Example 1 — Risk Narrative (Cyber Risk)**:
"**Technology Risk — Cyber Security**: Residual risk remains **High** (L:4, I:5, Score:20), unchanged from Q3 with an **increasing** trend and **rapid** velocity. The institution detected a 47% increase in sophisticated phishing attempts in Q4; threat intelligence indicates elevated state-sponsored activity targeting financial services. KRI CYB-003 (Mean Time to Detect) breached the yellow threshold at 18 hours vs. 12-hour target. Risk appetite: **Approaching tolerance**. Controls: 24/7 SOC, EDR, quarterly penetration testing (last test: two critical findings under remediation). Actions: (1) SOC staffing augmentation by Q1-end, (2) EDR upgrade targeted for [Date], (3) $2.3M zero-trust architecture investment over 18 months."

**Example 2 — Risk Rating Change**:
"**Compliance Risk — Regulatory Change**: Downgraded from **High** (16) to **Medium** (12), effective [Date], approved by Enterprise Risk Committee. Rationale: completed implementation of revised CRA rule ahead of deadline — system enhancements, process redesign, and staff training. Three validation tests confirmed compliance. KRI COMP-007 (Regulatory Change Backlog) decreased from 14 to 3 items, all low priority. Trend now **stable**; monitoring focused on anticipated CFPB examination in Q2."

## Guidelines

- Write for board-level audience: strategic, concise, focused on decisions needed
- Every narrative must be evidence-based with specific data points, KRI values, or events
- Risk appetite commentary is mandatory for every risk category
- Distinguish clearly between inherent risk and residual risk
- Use consistent risk taxonomy and rating methodology across all narratives
- Emerging risk narratives should be genuinely forward-looking, not repackaged current risks
- Risk interconnection analysis is increasingly expected by regulators; do not present risks in silos
- Ensure the executive summary can stand alone for time-constrained board members

## Validation Checklist

- [ ] All enterprise risks have corresponding heatmap placement and narratives
- [ ] Risk appetite status documented for every category with supporting metrics
- [ ] Risk rating changes explained with evidence and governance approval
- [ ] Top risks ranked with full narratives and management actions
- [ ] Emerging risks identified with horizon, indicators, and preparedness
- [ ] Risk interconnections documented with cascading scenario analysis
- [ ] KRI references are current and accurately cited
- [ ] Narratives consistent in terminology, methodology, and rating scale
- [ ] Executive summary highlights items requiring board action
- [ ] Report suitable for regulatory examination review
