---
name: market-sizing
description: "Produces defensible market size estimates for a specified market or opportunity. Clarifies scope before sizing, chooses a method (top-down, bottom-up, or value-based), researches and cites public sources, separates facts from assumptions, builds a full calculation chain with sensitivity ranges, and rates overall confidence. Use this skill whenever a market size, TAM/SAM/SOM, spend pool, or expansion upside estimate is needed."
metadata:
  display_name: "Market Sizing"
  short_description: "Produce defensible market size estimates with cited sources and sensitivity ranges"
  default_prompt: "Size the market for [product/category] in [geography] over [time horizon]"
  icon_path: "assets/icon.png"
---

# Market Sizing

## Goal

Produce a defensible market size estimate for a market or opportunity the user specifies. The estimate is built on cited public sources, shows the full calculation chain, separates facts from assumptions, and comes with a sensitivity range and confidence rating. No fabricated numbers — every input traces to a source or a clearly labeled assumption.

## When to Use

Activate this skill when any of the following apply:

- A user asks to "size the market" or "estimate the TAM" for a product, category, workflow, use case, or problem area
- A user needs a TAM, SAM, SOM, spend pool, expansion upside, or unit volume estimate
- A user wants a bottom-up or top-down market model with cited inputs
- A user asks "how big is the market for [X]" or "what's the opportunity size for [Y]"
- A user needs a defensible market figure for a business case, pitch deck, or investment memo

Relevant input types:
- A product category, workflow, use case, or problem area description
- Optional scope parameters (geography, segment, time horizon, unit, answer type)
- The user may provide some or none of these — the skill asks for the gaps

## How to Use

The user invokes:

- `/market-sizing <market or opportunity description>`

Interpret the input as:
- The market, product category, workflow, use case, or problem area to size
- Any scope parameters the user already specified alongside it
- If the user hasn't provided enough to begin, ask for the missing parameters (see Step 1)

## Steps (STRICT)

### 1. CLARIFY BEFORE YOU SIZE

Before estimating, confirm these parameters. If the user hasn't specified any, ask them to fill them in. If they've already provided some, skip those and only ask for the gaps. Use `ask_form` to collect all missing parameters at once.

Required parameters:
- **What am I sizing?** (product category, workflow, use case, problem area)
- **Geography and segment scope** (global, US only, enterprise vs SMB, etc.)
- **Time horizon** (current year, 5-year projection, etc.)
- **What unit should the answer be in?** (revenue, spend pool, unit volume, population count)
- **What kind of answer do I need?** (TAM/SAM/SOM, spend pool, expansion upside, other)

### 2. CHOOSE YOUR METHOD

Pick the simplest defensible approach:

| Method | When to Use |
|--------|-------------|
| **Top-down** | Reliable published market data exists — start from aggregate and narrow down |
| **Bottom-up** | Build from observable units (number of buyers × price × frequency) |
| **Value-based** | Start from the value created or problem solved, then translate to spend |

State which method you're using and why. If more than one fits, use the second to cross-check the first.

### 3. RESEARCH AND CITE

Use reliable public web sources for every external input. Acceptable source types:
- Market reports (Gartner, IDC, Forrester, Statista, etc.)
- Government statistics (Census Bureau, BLS, Eurostat, etc.)
- Industry associations
- Public company filings (10-K, S-1, annual reports)
- Census and demographic data
- Analyst estimates

For each input:
- Cite the source by name
- Note the year of the data
- Link to the source when available

Do not fabricate numbers. If a key input can't be sourced, label it as a **stated assumption** with a confidence level (high / medium / low).

### 4. SEPARATE FACTS FROM ASSUMPTIONS

In the output, keep these visually distinct:

| Category | Definition | How to Label |
|----------|------------|--------------|
| **Facts** | Sourced numbers with citations | Source name + year in the input table |
| **Estimates** | Derived calculations from facts and assumptions | Show the formula in the calculation chain |
| **Assumptions** | Judgment calls with rationale and confidence level | Mark as "Assumption" with confidence (high/medium/low) |

### 5. BUILD THE MODEL

Show the full calculation chain. Every derived number must trace back to a formula, not a hardcoded output. Structure the output as:

1. **Market definition** — one paragraph defining what's being sized
2. **Method and approach** — 2-3 sentences on the chosen method and why
3. **Input table** — each input, its value, source, and whether it's a fact or assumption
4. **Calculation chain** — step by step, with formulas
5. **Base case estimate** — the point estimate from the calculation
6. **Sensitivity range** — how the estimate changes when the top 2-3 assumptions move up or down

### 6. STATE CONFIDENCE AND NEXT STEPS

- Give a **point estimate and a range** (low / base / high)
- Name the **2-3 assumptions** that most move the number
- State what **source or data** would most improve confidence
- Rate **overall confidence** (high / medium / low) and explain why

## Output Format (STRICT)

Format the output in structured sections with tables. Do not write prose paragraphs — use numbered lists, tables, and formulas.

```
## 1. MARKET DEFINITION
[One paragraph]

## 2. METHOD AND APPROACH
[2-3 sentences]

## 3. INPUT TABLE

| # | Input | Value | Source | Year | Type |
|---|-------|-------|--------|------|------|
| 1 | [input name] | [value] | [source] | [year] | Fact / Assumption |

## 4. CALCULATION CHAIN
1. [Step 1 formula] = [result]
2. [Step 2 formula] = [result]
3. [Step 3 formula] = [result]

## 5. BASE CASE ESTIMATE
[Point estimate with unit]

## 6. SENSITIVITY RANGE

| Scenario | Assumption Changed | New Value | Estimate |
|----------|--------------------|-----------|----------|
| Low | [assumption] [down] | [value] | [estimate] |
| Base | — | — | [estimate] |
| High | [assumption] [up] | [value] | [estimate] |

## 7. CONFIDENCE AND NEXT STEPS
- **Point estimate:** [value]
- **Range:** [low] – [high]
- **Key swing assumptions:**
  1. [assumption 1]
  2. [assumption 2]
  3. [assumption 3]
- **Data that would most improve confidence:** [source or data type]
- **Overall confidence:** [high/medium/low] — [explanation]
```

## Constraints

- **Don't fabricate numbers.** Every external input must come from a cited public source or be explicitly labeled as a stated assumption with a confidence level.
- **Show the full chain.** Every derived number must trace to a formula. No black-box outputs.
- **Clarify before sizing.** Never start estimating until scope parameters are confirmed. Ask for gaps, don't guess them.
- **Separate facts, estimates, and assumptions.** Keep them visually distinct in the output. Don't blur the line between a sourced number and a judgment call.
- **Cite the year.** Market data goes stale — always note the year of each sourced input.
- **Sensitivity is mandatory.** The base case alone isn't enough. Show how the top 2-3 assumptions move the number.
- **No prose paragraphs.** Use numbered lists, tables, and formulas. Structured output only.
- **Cross-check when possible.** If two methods fit, use the second to sanity-check the first and note any divergence.
- **Be conservative.** When in doubt, round down rather than up. A defensible underestimate beats an inflated one.

## Failure Handling

- If the user's description is too vague to size even after clarification (e.g., "the internet market"), ask them to narrow the scope.
- If no reliable public data exists for a key input, label it as a stated assumption with a confidence level and proceed — but flag it clearly in the confidence section.
- If the estimate range is so wide it's not useful (e.g., low and high differ by more than 10x), say so and identify what data would narrow it.
- If the user provides contradictory scope parameters, point out the contradiction and ask them to resolve it.

## Examples

**Example 1**
User: /market-sizing US enterprise market for AI-powered contract review software

Expected output: After confirming scope (or using the provided parameters), the skill researches the number of US enterprises, contract review software pricing, adoption rates, and growth projections. Produces a structured 7-section output with an input table, calculation chain, base case estimate, sensitivity range, and confidence rating.

**Example 2**
User: /market-sizing global spend pool for developer tools, 5-year projection

Expected output: Confirms geography (global), unit (spend pool), and time horizon (5-year). Researches global developer population, tool spending per developer, and growth rates. Builds a bottom-up model with cited inputs, shows the calculation chain, and provides a sensitivity range around adoption and pricing assumptions.
