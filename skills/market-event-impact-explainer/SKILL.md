---
name: market-event-impact-explainer
description: Explain market event impact on client portfolios in plain language with actionable context. Use when significant market events occur (rate changes, geopolitical crises, sector selloffs, earnings shocks), clients ask about market headlines, advisors need rapid communication templates, or when proactive client outreach is needed during market volatility.

metadata:
  display_name: "Market Event Impact Explainer"
  short_description: "Explain market event impact on client portfolios clearly"
  default_prompt: "Explain my market event impact in simple words and next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Market Event Impact Explainer

## Overview

Translate market events into client-specific portfolio impact explanations. This skill connects macro events (rate decisions, geopolitical developments, sector rotations, economic data releases) to the actual holdings and allocation in a client's portfolio, producing clear explanations suitable for client conversations, emails, and review presentations. The goal is to reduce client anxiety, prevent panic-driven decisions, and reinforce long-term plan adherence.

## When to Use

- Major market events requiring proactive client communication (>5% market move)
- Client calls asking "what does [headline] mean for my portfolio?"
- Preparing talking points for market-event-driven client outreach campaigns
- Quarterly review context-setting during periods of elevated volatility
- Explaining sector, asset class, or geographic market events and portfolio exposure
- Documenting investment committee market commentary for distribution

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Market event | Description of the event and market reaction | News/data feed |
| Client portfolio | Current holdings with asset class, sector, geography | Custodian data |
| Performance impact | Portfolio and component returns during the event period | Performance data |
| Historical context | Prior similar events and market recovery patterns | Historical database |
| Client profile | Risk tolerance, time horizon, goals, communication preference | CRM data |
| Economic data | Relevant economic indicators and forecasts | Economic feeds |

## Methodology

### Step 1 — Event Classification and Severity Assessment

Classify the market event to determine response urgency and communication approach:

**Event categories:**
- **Monetary policy**: Rate decisions, QE/QT changes, forward guidance shifts
- **Geopolitical**: Conflicts, sanctions, trade policy, elections, regulatory changes
- **Economic data**: Employment, inflation, GDP, housing, consumer confidence surprises
- **Credit events**: Sovereign debt concerns, corporate defaults, bank stress
- **Sector-specific**: Industry disruption, regulatory action, earnings surprises
- **Market structure**: Flash crashes, liquidity events, correlation spikes

**Severity tiers:**
| Tier | Market Impact | Client Response | Communication Timeline |
|------|--------------|----------------|----------------------|
| 1 — Minor | <3% broad market move | Monitor only | Next scheduled contact |
| 2 — Notable | 3–7% broad market move | Prepare talking points | Within 1 week |
| 3 — Significant | 7–15% broad market move | Proactive outreach to top clients | Within 48 hours |
| 4 — Severe | >15% broad market move or crisis | All-client communication | Within 24 hours |

### Step 2 — Portfolio Exposure Mapping

Map the event to specific portfolio exposures:

- **Direct exposure**: Holdings directly affected (e.g., energy stocks during oil price shock)
- **Indirect exposure**: Holdings affected through second-order effects (e.g., airlines affected by energy costs)
- **Correlation exposure**: Asset classes that historically move together during this type of event
- **Hedge exposure**: Portfolio elements that should offset losses (e.g., Treasuries during equity selloff)

Quantify the exposure:
- Percentage of portfolio in directly affected holdings
- Dollar impact: Estimated gain/loss attributable to the event
- Attribution: How much of the portfolio's period return is explained by the event

### Step 3 — Plain-Language Impact Translation

Convert technical analysis into client-appropriate language:

**Framework for client explanation:**

1. **What happened** (1–2 sentences): State the event simply
   - "The Federal Reserve raised interest rates by 0.50% — more than the 0.25% markets expected"
   - "Military conflict in [region] caused global stock markets to decline sharply"

2. **How it affected your portfolio** (2–3 sentences): Specific impact with dollar amounts
   - "Your portfolio declined approximately $[X] (about X%) this week"
   - "Your bond holdings lost about $[X] because bond prices fall when interest rates rise"
   - "However, your [hedge/diversifier] gained $[X], partially offsetting the stock decline"

3. **Why it matters (or doesn't)** (2–3 sentences): Context and perspective
   - "This type of event has occurred [N] times in the past 30 years. Markets recovered within [X] months on average"
   - "Your portfolio is designed to weather periods like this — the diversification across stocks, bonds, and alternatives is working as intended"

4. **What we're doing** (1–2 sentences): Active management response
   - "We are monitoring the situation closely and will rebalance if opportunities emerge"
   - "No changes are needed to your long-term plan at this time"

5. **What you should do** (1 sentence): Clear client guidance
   - "Continue with your regular contributions — investing during downturns has historically been beneficial"
   - "If your financial situation has changed, please let us know so we can adjust your plan"

### Step 4 — Historical Context and Recovery Analysis

Provide perspective through historical comparison:

- Identify the 3–5 most comparable historical events
- Document market decline magnitude and recovery timeline for each:

| Event | Market Decline | Recovery Time | 1Y After | 3Y After |
|-------|---------------|--------------|----------|----------|
| [Event 1] | -XX% | X months | +XX% | +XX% |
| [Event 2] | -XX% | X months | +XX% | +XX% |
| [Event 3] | -XX% | X months | +XX% | +XX% |

- Calculate the cost of panic-selling during each historical event:
  "An investor who sold at the bottom of [event] and waited 6 months to reinvest would have missed $[X] in gains per $100,000 invested"
- Note any differences between the current event and historical comparisons

### Step 5 — Scenario-Based Forward Analysis

Present possible outcomes without making predictions:

**Scenario A — Quick resolution:**
- Event resolves favorably within [timeframe]
- Expected portfolio impact: recovery of [X–Y]% within [timeframe]
- Probability assessment: [Low / Moderate / High]

**Scenario B — Extended impact:**
- Event persists for [timeframe]
- Expected portfolio impact: continued volatility, possible additional [X]% downside
- Probability assessment: [Low / Moderate / High]

**Scenario C — Escalation:**
- Event worsens significantly
- Expected portfolio impact: potential [X]% additional decline
- Probability assessment: [Low / Moderate / High]
- Portfolio protection elements: [Diversification, hedges, cash reserves that provide cushion]

### Step 6 — Communication Channel Optimization

Tailor the message format to the communication channel:

- **Phone call script**: 3-minute talking points for advisor calls to top clients
- **Email template**: 3-paragraph email suitable for mass distribution with personalization fields
- **Text/SMS**: 2-sentence summary with offer to schedule a call
- **Social media/blog**: Educational content suitable for public posting (no specific client data)
- **Meeting presentation**: 2–3 slides for incorporation into review meetings

### Step 7 — Follow-Up and Documentation

Complete the communication cycle:

- Log all client contacts and responses in CRM
- Document any client requests to change strategy (and whether acted upon or dissuaded)
- Schedule follow-up communication for [1 week / 1 month] post-event
- Update client-facing materials (market commentary, FAQ) on website/portal
- Track client retention and satisfaction following the event communication

## Output Specification

```
## Market Event Impact Report — [Event Name]

### Event Summary
- Event: [Plain-language description]
- Date: [Event date]
- Market reaction: [Key index movements]
- Severity: Tier [1–4]

### Portfolio Impact — [Client Name]
- Portfolio value change: $[X] ([X.X%])
- Directly affected holdings: [List with individual impact]
- Diversification benefit: $[X] offset from [hedges/diversifiers]
- Net impact vs. broad market: [Better/Worse/In line] by [X%]

### Client-Facing Explanation
[5-part narrative: what happened, your portfolio impact, context, our response, your action]

### Historical Perspective
[Comparable events table with recovery timelines]

### Communication Recommendation
- Priority: [Proactive outreach / Respond if contacted / Next scheduled meeting]
- Channel: [Phone / Email / Text]
- Template: [Pre-drafted communication]

### Advisor Talking Points
1. [Key point with supporting data]
2. [Key point with supporting data]
3. [Key point with supporting data]
- Anticipated client question: "[Question]" → Response: "[Answer]"
```

## Analysis Framework

Apply the **CALM** framework:

- **C**ontext — Classify the event and assess severity objectively
- **A**ssess — Map portfolio exposure and quantify specific impact
- **L**anguage — Translate analysis into clear, client-appropriate communication
- **M**onitor — Establish follow-up protocol and track client response

## Examples

**Example 1 — Fed Rate Hike Impact**

Event: Fed raises rates 50 bps (market expected 25 bps). Client portfolio impact: Equity sleeve down 3.1%, bond sleeve down 1.8%, total portfolio down 2.4% ($38,400 on $1.6M portfolio). Client message: "The Federal Reserve raised interest rates more than expected this week, which caused both stocks and bonds to decline temporarily. Your portfolio declined about $38,000 (2.4%), which is less than the broad market's 3.5% decline because your bond allocation is positioned with shorter maturities that are less sensitive to rate changes. Over the past 40 years, there have been 8 surprise rate hikes of this magnitude — stocks recovered fully within an average of 4 months. Your plan accounts for periods like this. No changes are recommended."

**Example 2 — Geopolitical Crisis Communication**

Event: Military escalation in Eastern Europe, oil prices spike 30%, markets down 8% in 3 days. Severity: Tier 3 — proactive outreach to all Tier 1 clients within 48 hours. Client portfolio impact: Down 5.2% (less than market due to energy overweight gaining 12% and Treasury allocation gaining 2%). Phone script: "I'm calling because I want you to hear from me directly during this volatile period. Your portfolio is down about 5% this week, which is actually better than the overall market decline of 8%. Your energy investments have gained significantly, and your Treasury bonds have provided stability — exactly the role they're designed to play in your portfolio. Based on historical geopolitical events, markets have typically recovered within 3–6 months. We are not recommending any changes to your allocation at this time."

## Guidelines

- Respond within the timeline appropriate for the severity tier — timeliness matters
- Never predict outcomes — present scenarios with historical context instead
- Personalize communications with the client's specific portfolio impact and dollar amounts
- Avoid minimizing legitimate concerns ("don't worry" is dismissive) — acknowledge and contextualize
- Emphasize the plan and its design for resilience, not market-timing decisions
- Document all communications for compliance records
- Coordinate messaging across the advisory team for consistency
- Include a call-to-action in every communication (schedule a review, maintain contributions, contact us)
- Never send mass communications without compliance review during significant events

## Validation Checklist

- [ ] Event correctly classified by category and severity tier
- [ ] Portfolio exposure mapped with specific holdings and dollar impact
- [ ] Client explanation uses plain language (no jargon, no acronyms without definition)
- [ ] Historical context includes at least 3 comparable events with recovery data
- [ ] Scenarios present a range of outcomes without making predictions
- [ ] Communication channel and timing appropriate for the severity tier
- [ ] Talking points address likely client questions with prepared responses
- [ ] All communications reviewed by compliance before distribution
- [ ] Follow-up schedule established for post-event monitoring
- [ ] CRM updated with communication log and client responses
