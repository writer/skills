---
name: retailer-negotiation-prep
description: Prepare structured negotiation talking points, BATNA analysis, and trade term strategies for CPG-retailer negotiations. Use when preparing for JBP sessions, annual line reviews, trade term negotiations, slotting discussions, or any retailer commercial meeting.

metadata:
  display_name: "Retailer Negotiation Prep"
  short_description: "Prepare CPG-retailer negotiation strategy and trade terms"
  default_prompt: "Analyze my retailer negotiation prep and recommend clear next actions"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Retailer Negotiation Prep

## Overview

Build a comprehensive negotiation preparation package for CPG-retailer commercial discussions. This skill produces structured talking points, BATNA (Best Alternative to a Negotiated Agreement) analysis, trade term modeling, concession strategies, and value-creation frameworks tailored to the specific retailer relationship and negotiation context.

## When to Use

- Annual Joint Business Planning (JBP) sessions
- Line review and assortment negotiations
- Trade term and promotional calendar negotiations
- Slotting fee and new item discussions
- Pricing and cost-increase pass-through conversations
- Deduction and chargeback dispute resolution
- Category captaincy proposals

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Retailer profile | Name, channel, format, geographic footprint | Text summary |
| Relationship history | Prior agreements, YTD performance, open issues | Summary or table |
| Negotiation objective | What you want to achieve (e.g., shelf expansion, cost pass-through) | Clear objective statement |
| Your data | Brand performance at retailer: sales, share, velocity, margins | Numerical data |
| Category data | Category performance, trends, competitive share | Syndicated data summary |
| Current trade terms | Existing terms: slotting, MDF, OI, scan, freight, payment terms | Term sheet or summary |
| Constraints | Non-negotiables, budget limits, internal mandates | List |

## Methodology

### Step 1: Stakeholder and Power Analysis

Map the negotiation landscape:

**Retailer Buyer Profile:**
- Decision-making authority level (category manager, DMM, VP)
- Known priorities (margin, traffic, differentiation, private label growth)
- Negotiation style (collaborative vs. positional)
- Performance metrics they are measured on (category $ growth, margin %, inventory turns)

**Power Balance Assessment:**
| Factor | Your Position | Retailer Position | Net Power |
|--------|--------------|-------------------|-----------|
| Brand strength / consumer pull | 1-5 | — | ←/→ |
| % of category revenue at retailer | — | 1-5 | ←/→ |
| Alternative channel options | 1-5 | — | ←/→ |
| Private label threat | — | 1-5 | ←/→ |
| Switching cost for retailer | 1-5 | — | ←/→ |

### Step 2: BATNA Development

Define your walk-away position and alternatives:

**Your BATNA:**
- What happens if no agreement is reached?
- Alternative retailers/channels available
- Revenue at risk and timeline to replace
- Cost of no-deal (inventory, capacity, brand impact)

**Retailer's BATNA (estimated):**
- Can they replace your brand? With what?
- Consumer switching behavior if delisted
- Category performance impact without your brand
- Private label readiness in your segment

**ZOPA (Zone of Possible Agreement):**
- Your reservation point (minimum acceptable outcome)
- Estimated retailer reservation point
- Overlap range = negotiation space

### Step 3: Value Creation Framework

Identify tradeable value beyond price/trade spend:

| Value Lever | Your Cost | Retailer's Perceived Value | Trade Ratio |
|-------------|-----------|---------------------------|-------------|
| Exclusive SKU/flavor | Low (existing capability) | High (differentiation) | Favorable |
| Early access to innovation | Low | Medium | Favorable |
| Category insights/data sharing | Low | High | Very Favorable |
| Joint demand forecasting | Medium | High | Favorable |
| Display/merchandising investment | Medium | Medium | Neutral |
| Extended payment terms | High (working capital) | High | Neutral |

Prioritize levers with favorable trade ratios — low cost to you, high value to retailer.

### Step 4: Concession Strategy

Design a planned concession sequence:

**Concession Rules:**
1. Never concede without getting something in return
2. Make concessions progressively smaller to signal approaching your limit
3. Start with low-cost/high-value items (from Step 3)
4. Reserve high-cost concessions for final rounds only
5. Always have a "pocket" concession ready for closing

**Concession Map:**
```
Round 1 (Opening): Offer [Value Lever A] in exchange for [Priority Ask 1]
Round 2 (Middle):  Offer [Value Lever B] in exchange for [Priority Ask 2]
Round 3 (Close):   Offer [Pocket concession] in exchange for [Final terms]

Hard No Items (non-negotiable):
- [Item 1 — reason]
- [Item 2 — reason]
```

### Step 5: Talking Points Construction

Build structured talking points using the SPIN framework:

**Situation Questions** (establish common ground):
- "Your category grew X% last quarter — we see similar momentum in the channel..."
- "We understand inventory turns are a priority for the department..."

**Problem Questions** (surface retailer pain points):
- "We've noticed the premium segment is under-spaced relative to its growth rate..."
- "Promotional ROI in the category has been declining — we've seen similar trends..."

**Implication Questions** (amplify urgency):
- "If the premium segment continues under-indexed, the category risks losing shoppers to [competitor retailer]..."
- "Without corrective action, we estimate $Xm in category value is at risk over the next 12 months..."

**Need-Payoff Questions** (position your solution):
- "If we could demonstrate a planogram reset delivers +X% category growth, would that support a shelf expansion discussion?"
- "Our shopper data shows a loyalty program collaboration could increase basket size by $X..."

### Step 6: Scenario Rehearsal

Prepare for three negotiation scenarios:

| Scenario | Retailer's Likely Position | Your Response Strategy |
|----------|--------------------------|----------------------|
| Best case | Agrees to primary ask with minor pushback | Secure additional secondary objectives |
| Base case | Pushes back on primary, open to alternatives | Deploy concession Round 1-2, pivot to value creation |
| Worst case | Hardline rejection, threatens delisting/reduction | Invoke BATNA, propose pilot/test, request time to regroup |

## Output Specification

```markdown
# Negotiation Prep — [Retailer] [Meeting Type]
**Date**: [Meeting date]
**Objective**: [Primary negotiation objective]

## Power Analysis Summary
[Net power assessment with key leverage points]

## BATNA Analysis
| | Your BATNA | Retailer's BATNA |
|---|-----------|-----------------|
| Best alternative | ... | ... |
| Cost of no-deal | $X | $Y |
| ZOPA range | [Your floor] to [Retailer floor estimate] |

## Value Creation Menu
[Prioritized list of tradeable value items with trade ratios]

## Talking Points
### Opening (Situation/Problem)
1. [Point with supporting data]
2. [Point with supporting data]

### Building Urgency (Implication)
1. [Point with quantified risk/opportunity]

### Proposing Solutions (Need-Payoff)
1. [Proposal with expected retailer benefit]

## Concession Strategy
[Sequenced concession map with hard-no items]

## Scenario Responses
[Best/Base/Worst case playbook]

## Pre-Meeting Checklist
- [ ] Materials printed/loaded
- [ ] Data verified and sourced
- [ ] Internal alignment confirmed (Sales, Finance, Marketing)
- [ ] Backup proposals prepared
```

## Analysis Framework

**Trade Spend ROI for Each Proposed Term:**
```
Incremental Revenue from Term = Estimated Lift × Duration × ASP
Cost of Term = Direct Cost + Opportunity Cost
ROI = (Incremental Revenue − Cost) / Cost
Threshold: ROI > 2.0x for standard terms; > 3.0x for new/unproven terms
```

## Example

**Input**: "Preparing for Kroger JBP. Goal: expand shelf space from 3 to 5 facings. Our brand is #2 in category with 18% share. Category grew 6% but our brand grew 12%."

**Key talking point generated**:
> "Your snacking category delivered 6% growth in the Kroger banner this year, and our brand outpaced the category at 12%, contributing disproportionate growth per linear foot. With 18% value share on 3 facings (5% of section), our brand is significantly under-spaced relative to contribution. Our analysis shows that expanding to 5 facings would generate an estimated $X incremental weekly revenue per store based on velocity uplift seen in comparable resets at [peer retailer]. We're prepared to support the transition with a [merchandising commitment] and [exclusive Kroger SKU] to drive incremental basket trips."

## Guidelines

- Ground every talking point in data — assertions without data erode credibility
- Never disparage competitors by name — focus on category opportunity
- Quantify every proposal's benefit to the retailer, not just to your brand
- Prepare for objections before they're raised — every talking point needs an "if they push back" counter
- Maintain a collaborative tone — JBP is joint value creation, not zero-sum
- Always have a "next step" proposal ready regardless of outcome

## Validation Checklist

- [ ] Power analysis completed with at least 5 factors assessed
- [ ] BATNA defined for both sides with quantified cost of no-deal
- [ ] ZOPA range identified
- [ ] At least 5 value creation levers identified with trade ratios
- [ ] Concession strategy sequenced with hard-no items listed
- [ ] Talking points use SPIN framework structure
- [ ] All data points sourced and verified
- [ ] Three scenarios (best/base/worst) prepared with response strategies
- [ ] Internal alignment confirmed across Sales, Finance, Marketing
