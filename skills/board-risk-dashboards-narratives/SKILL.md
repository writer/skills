---
name: board-risk-dashboards-narratives
description: Generate board-safe risk dashboard narratives covering credit, market, liquidity, operational, and strategic risk with traffic-light indicators and trend commentary. Use when preparing board risk committee materials, translating CRO dashboards into director-accessible language, or writing risk appetite statement compliance narratives.

metadata:
  display_name: "Board Risk Dashboards Narratives"
  short_description: "Write board-ready risk dashboard narratives for banks"
  default_prompt: "Summarize my board risk dashboards with key findings and next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Board Risk Dashboard Narratives

## Overview

Transforms detailed risk dashboards and CRO-level data into board-appropriate narratives that non-executive directors can readily understand and act upon. Combines quantitative risk metrics with qualitative context, trend analysis, traffic-light visualization, and clear escalation of items requiring board attention. Aligned with regulatory expectations for board risk oversight (OCC Heightened Standards, EBA Guidelines on Internal Governance).

## When to Use

- Preparing quarterly Board Risk Committee (BRC) meeting materials
- Translating CRO risk reports into director-accessible narratives
- Writing risk appetite statement (RAS) compliance commentary
- Documenting board risk oversight for regulatory examination readiness
- Generating ad-hoc board risk updates during heightened risk periods

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Risk appetite statement | Board-approved risk appetite metrics and thresholds | RAS framework |
| Credit risk data | NPL, provision coverage, concentration, migration, loss rates | Dashboard metrics |
| Market risk data | VaR, stress test losses, investment portfolio, rate sensitivity | Dashboard metrics |
| Liquidity risk data | LCR, NSFR, survival horizon, funding concentration | Dashboard metrics |
| Operational risk data | Loss events, KRIs, technology incidents, compliance issues | Event and KRI data |
| Capital adequacy | CET1, leverage, stress test capital trajectory | Capital metrics |
| Strategic/emerging risks | Cyber, climate, geopolitical, competitive, conduct risks | Qualitative assessments |
| Prior period data | Previous quarter dashboard for trend analysis | Same format |

## Methodology

### Step 1 — Establish the Risk Appetite Compliance Framework

Map every reported metric to the board-approved Risk Appetite Statement (RAS):

For each metric, define three zones:
- **Within appetite (Green)**: Metric comfortably within board-approved threshold
- **Approaching limit (Amber)**: Metric within 80-100% of threshold, or adverse trend for 2+ consecutive periods
- **Exceeding appetite (Red)**: Metric has breached board-approved threshold

Construct the **RAS Compliance Summary Table** showing every appetite metric with current level, threshold, trend direction, and traffic-light status. This table serves as the opening page of every board risk report.

### Step 2 — Narrate Credit Risk Position

Structure the credit risk narrative around these themes:

**Portfolio quality:**
- NPL ratio with trend (3-quarter rolling) and peer comparison
- Stage migration analysis: flows between Stage 1 (performing), Stage 2 (significant increase in credit risk), Stage 3 (credit-impaired) under IFRS 9
- Provision coverage ratio and adequacy assessment
- Net charge-off rate vs. historical average and through-the-cycle expectation

**Concentration risk:**
- Top 10 / Top 20 borrower exposure as % of CET1
- Sector concentration with traffic-light status (e.g., CRE office, leveraged lending)
- Geographic concentration and country risk exposures
- Connected-party exposure vs. regulatory limits

**Forward-looking indicators:**
- Watch list trend and expected NPL formations
- IFRS 9 / CECL forward-looking ECL model outputs
- Macro scenario probability weights and their impact on provisions

Board-appropriate language: Avoid technical jargon (PD, LGD, EAD) in favor of accessible terms ("probability of default" written out, "expected losses," "impaired loans").

### Step 3 — Narrate Market and Interest Rate Risk

Simplify market risk for non-specialist directors:

**Trading risk:**
- VaR as a percentage of its limit (not absolute, which is harder for directors to contextualize)
- Frequency of VaR exceptions (backtesting) with explanation of any breaches
- Largest individual position or desk contribution to risk

**Banking book interest rate risk:**
- NII sensitivity to +/- 100bps expressed as % of projected NII (relatable framing)
- EVE sensitivity as % of CET1 capital
- Direction of sensitivity: "If rates rise, earnings will [increase/decrease] by approximately $[X]M"
- Hedge program summary: "The bank has hedged approximately [X]% of its rate exposure"

**Investment portfolio:**
- Unrealized gains/losses with trend
- Duration of the portfolio and its strategic rationale
- Credit quality composition of the bond portfolio

### Step 4 — Narrate Liquidity and Funding Risk

Frame liquidity for board understanding:

**Regulatory metrics:**
- LCR and NSFR with headroom above minimums expressed in both percentage points and dollar equivalents
- Trend direction with brief explanation of drivers

**Funding profile:**
- Deposit stability: Core deposit ratio, largest depositor concentration
- Funding diversification: Number of funding sources, reliance on any single source >10%
- Maturity profile: Near-term wholesale maturities as % of total funding

**Stress resilience:**
- Survival horizon in plain language: "The bank can meet all obligations for [X] days without accessing wholesale markets"
- Contingency funding plan status: All triggers green / any triggers amber or red

### Step 5 — Narrate Operational and Non-Financial Risks

Cover operational risk themes relevant to board oversight:

**Operational losses:**
- Total operational losses (YTD) with comparison to prior year and provisioned amount
- Significant individual events (>$1M or reputational impact) with root cause and remediation status

**Technology and cyber:**
- System availability metrics (uptime %)
- Cyber incidents and attempted attacks (high-level, not technical detail)
- Status of key technology programs (core banking, cloud migration)

**Conduct and compliance:**
- Regulatory compliance breaches or findings
- Customer complaints trend and significant complaint themes
- AML/KYC alert volumes and suspicious activity report trends

**Emerging risks:**
- Climate risk: Physical and transition risk exposure assessment
- Geopolitical risk: Country and sanction exposure relevant to current events
- AI/model risk: Use of AI models and validation status
- Third-party risk: Concentration in critical vendors

### Step 6 — Summarize Capital and Stress Test Position

Present capital in the context of resilience:
- Current CET1 vs. board target vs. regulatory minimum (visualized as a bar or waterfall)
- Distance to MDA restriction in percentage points and absolute dollars
- Stress test results: "Under a severe recession scenario, the bank's capital ratio would decline from [X]% to [Y]%, remaining [above/below] all regulatory minimums"
- Capital actions: Dividends, buybacks, and their impact on forward capital trajectory

### Step 7 — Compose the Board Narrative

Assemble with board communication best practices:
1. **Executive summary** (half page): Overall risk posture in 3-5 sentences with any red-flag items
2. **RAS compliance table**: One-page traffic-light dashboard
3. **Risk-by-risk narrative** (1 page each): Credit, market, liquidity, operational, capital — each following the structure: current position → trend → peer context → outlook → action items
4. **Emerging risks** (half page): New or evolving risks not yet in the RAS but warranting board awareness
5. **Appendix**: Supporting data tables for directors who want deeper detail

Total length target: 8-12 pages including tables and charts.

## Output Specification

```markdown
# Board Risk Dashboard — Q[X] [Year]

## Executive Risk Summary
Overall risk posture: [Stable / Elevated / Improving]
[3-5 sentence summary of the quarter's risk developments and board-attention items]

## Risk Appetite Compliance
| Risk Category | Metric | Current | Appetite | Trend | Status |
|---------------|--------|---------|----------|-------|--------|
| Credit | NPL Ratio | | | ↑↓→ | 🟢🟡🔴 |
| Credit | Concentration (Top 20) | | | | |
| Market | NII Sensitivity ±100bps | | | | |
| Liquidity | LCR | | | | |
| Liquidity | Survival Horizon | | | | |
| Capital | CET1 Ratio | | | | |
| Operational | Loss Ratio | | | | |

## Credit Risk
[Narrative covering quality, concentration, forward indicators]

## Market & Interest Rate Risk
[Narrative covering trading risk, banking book sensitivity, investment portfolio]

## Liquidity & Funding Risk
[Narrative covering LCR/NSFR, funding profile, stress resilience]

## Operational Risk
[Narrative covering losses, technology, cyber, compliance]

## Capital Adequacy & Stress Testing
[Narrative covering current ratios, stress trajectory, capital actions]

## Emerging & Strategic Risks
[Narrative covering new/evolving risks warranting board awareness]

## Items Requiring Board Decision
1. [Decision item with recommendation]

## Appendix
[Supporting data tables]
```

## Analysis Framework

Apply the **Board Risk Communication Pyramid**:
1. **Apex (What should we worry about?)**: Red and amber items, new risks, trend deterioration
2. **Middle (Where do we stand?)**: RAS compliance dashboard, key metrics vs. targets
3. **Base (Why?)**: Detailed supporting data and analysis in the appendix

Directors read top-down; the most critical information must appear first. Most directors will read the executive summary and RAS table; fewer will read the full narrative; only the most engaged will consult the appendix.

## Examples

**Example — Board-Appropriate Credit Narrative:**
"Credit quality remained stable, with the NPL ratio at 1.42%, within the board appetite of 2.0% and marginally improved from 1.48% last quarter. However, the commercial real estate office portfolio continues to show stress, with $87M in new watch list additions during the quarter, bringing total CRE office exposure on watch to $412M (2.1% of the CRE book). Management has proactively increased specific provisions by $23M and restricted new CRE office originations to existing relationship renewals only. The board is asked to note the enhanced monitoring framework and approve the updated CRE sector limit of $8.5B (reduced from $9.2B)."

**Example — Board-Appropriate Liquidity Narrative:**
"The bank maintains a strong liquidity position with LCR at 142%, well above the 100% regulatory minimum and 125% board appetite. In practical terms, the bank holds $4.8B more high-quality liquid assets than required, providing substantial capacity to absorb unexpected outflows. Under our most severe stress scenario, the bank can meet all obligations for 134 days without accessing wholesale funding markets, exceeding our 90-day internal minimum."

## Guidelines

- Write for an audience that is financially literate but not banking specialists
- Define technical terms on first use, then use consistently thereafter
- Express risk metrics in relatable terms ("X days of survival" vs. "LCR 142%")
- Always provide peer or historical context for every metric
- Limit each risk section to one page — depth goes in the appendix
- Use traffic-light indicators consistently across all risk categories
- Separate information items from decision items clearly
- Include "no change" commentary only for material metrics — silence implies stability
- Never present risk data without a forward-looking view or action implication

## Validation Checklist

- [ ] Every RAS metric mapped with current value, threshold, trend, and traffic-light status
- [ ] Traffic-light methodology consistent (green/amber/red thresholds documented)
- [ ] Credit narrative covers quality, concentration, and forward indicators
- [ ] Technical jargon eliminated or defined on first use
- [ ] Risk metrics accompanied by peer or historical context
- [ ] Stress test results stated in plain language with clear pass/fail indication
- [ ] Emerging risks section reflects current environment (not boilerplate)
- [ ] Decision items separated from information items with clear recommendations
- [ ] Total brief does not exceed 12 pages including appendix
- [ ] Executive summary captures all red/amber items and key board-attention matters
