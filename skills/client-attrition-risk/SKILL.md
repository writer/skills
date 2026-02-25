---
name: client-attrition-risk
description: Predict client attrition risk for wealth management relationships using engagement, performance, service, and life-event signals. Use when building client retention programs, prioritizing advisor outreach, identifying at-risk relationships before departure, analyzing attrition patterns, or developing proactive retention strategies for high-value clients.

metadata:
  display_name: "Client Attrition Risk"
  short_description: "Predict wealth management client attrition risk signals"
  default_prompt: "Optimize my client attrition risk and suggest the best next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Client Attrition Risk Prediction

## Overview

Identify wealth management clients at elevated risk of leaving the relationship before they signal intent to transfer. This skill combines engagement analytics, portfolio performance relative to expectations, service quality indicators, life-event triggers, and competitive market factors to produce a client-level attrition probability score. Outputs enable proactive retention interventions, advisor capacity allocation, and strategic investment in relationships with the highest retention ROI.

## When to Use

- Building or refining client retention early warning systems
- Prioritizing advisor outreach to at-risk high-value relationships
- Analyzing root causes of historical client departures
- Designing segment-specific retention programs and playbooks
- Evaluating the impact of fee changes, service model changes, or advisor transitions on attrition risk
- Forecasting AUM attrition for business planning and budgeting

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Client demographics | Age, AUM tier, tenure, household composition | CRM data |
| Engagement data | Meeting frequency, login activity, email opens, calls | CRM/digital analytics |
| Performance data | Client returns vs. benchmark and expectations | Performance system |
| Service records | Service requests, complaints, resolution times | Service ticketing |
| Life events | Job changes, retirement, divorce, death, inheritance | CRM notes |
| Fee data | Fee rate, fee changes, fee competitiveness | Billing data |
| Historical attrition | Prior departures with reasons and characteristics | Historical records |
| Advisor data | Advisor tenure, team changes, service model | HR/CRM data |

## Methodology

### Step 1 — Engagement Signal Monitoring

Track behavioral signals that precede disengagement:

**Digital engagement indicators:**
- **Portal/app login frequency**: Declining trend over 3+ months (vs. client's own baseline)
- **Statement access**: Client stops downloading or viewing statements
- **Email engagement**: Open rates declining, unsubscribes from newsletters
- **Document completion**: Delayed or non-responsive to document requests
- **Digital tool usage**: Stopped using planning tools, calculators, or goal trackers

**Relationship engagement indicators:**
- **Meeting attendance**: Declined or cancelled recent meeting invitations
- **Meeting quality**: Shorter meetings, fewer questions, less engagement during reviews
- **Response time**: Increasing time to respond to advisor communications
- **Initiated contact**: Client stops initiating contact (previously proactive, now silent)
- **Referral activity**: Client who previously referred others has stopped

**Scoring**: Create an engagement score (0–100) based on weighted combination of indicators, compared to the client's own historical baseline (not population average — introverted clients may have lower baseline engagement without being at risk).

### Step 2 — Performance and Expectations Gap Analysis

Assess whether the client's experience meets their expectations:

- **Absolute performance**: Client's portfolio return for trailing 1Y, 3Y, since-inception
- **Relative performance**: Client's return vs. IPS benchmark and peer/target return
- **Expectations gap**: Difference between what the client expected and what was delivered
  - Clients rarely remember exact benchmarks — they remember whether they "did well" or "did poorly"
  - Compare against market headlines ("market was up 20%, but my portfolio only gained 12%")
- **Negative experience periods**: Count of quarters with negative returns in trailing 3 years
- **Drawdown impact**: Maximum portfolio decline experienced by the client and recovery status
- **Fee-adjusted return**: Net return after advisory fees — fee drag visibility

**Risk scoring:**
- Underperformance of >200 bps vs. benchmark for 4+ consecutive quarters: High risk
- Negative absolute return during a positive market year: High risk
- Client experienced drawdown >15% without proactive advisor communication: High risk

### Step 3 — Service Quality Assessment

Evaluate the service experience quality:

- **Response time**: Average time to respond to client inquiries (target: same business day)
- **Issue resolution**: First-contact resolution rate and average time-to-resolution
- **Complaint history**: Number and severity of complaints in trailing 24 months
- **Promise fulfillment**: Were action items from meetings completed on time?
- **Proactive outreach**: Is the advisor initiating contact or only responding?
- **Team continuity**: Has the client experienced advisor or team changes?
- **Service level match**: Is the service level appropriate for the client's AUM tier?

**Service quality score**: Composite rating based on objective metrics weighted by importance (complaint history most heavily weighted).

### Step 4 — Life Event and Transition Risk Factors

Identify life events that create relationship vulnerability:

| Life Event | Attrition Risk | Mechanism | Intervention Window |
|------------|---------------|-----------|-------------------|
| Retirement | Medium | Cash needs change, competitor approaches | 12 months pre/post |
| Spouse death | High | Surviving spouse may have different advisor preference | 3–12 months |
| Divorce | High | Account splits, one party may leave | During proceedings |
| Inheritance | Medium | Beneficiary has own advisor, consolidation decision | 6 months post |
| Job loss/change | Medium | Reduced income, may seek lower fees | 3 months post |
| Relocation | Medium | Local advisor preference, relationship disruption | Pre-move |
| Business sale | High | Large liquidity event attracts competitor solicitation | 6 months pre/post |
| Children aging out | Low-Med | Reduced planning complexity, fee sensitivity increases | Gradual |
| Health decline | Medium | POA/family involvement, relationship transfer | Variable |

### Step 5 — Competitive and Market Factors

Assess external pressures on the relationship:

- **Fee competitiveness**: Is the client's fee rate competitive for their AUM tier?
  - Industry average: 80–100 bps for <$1M, 60–80 bps for $1–5M, 40–60 bps for $5M+
  - If client's rate is >20 bps above market: elevated risk
- **Robo-advisor/digital threat**: Clients with simple needs and cost sensitivity may migrate to digital platforms
- **Competitive solicitation**: Wealth industry marketing spend in client's demographic/geography
- **Market environment**: Extended bull markets reduce switching costs; bear markets increase advisor dependency
- **Industry disruption**: Fee compression trends, commission-to-fee transition, consolidation

### Step 6 — Attrition Probability Scoring

Combine all factors into a composite attrition risk score:

**Model inputs and weights:**
| Factor Category | Weight | Client Score | Weighted Score |
|----------------|--------|-------------|----------------|
| Engagement decline | 30% | XX/100 | XX |
| Performance gap | 25% | XX/100 | XX |
| Service quality issues | 20% | XX/100 | XX |
| Life event risk | 15% | XX/100 | XX |
| Competitive/fee pressure | 10% | XX/100 | XX |
| **Composite attrition risk** | **100%** | | **XX/100** |

**Risk tier assignment:**
- **Low (0–25)**: Standard relationship management, no special intervention
- **Watch (26–50)**: Enhanced monitoring, include in next advisor touchpoint agenda
- **Elevated (51–75)**: Proactive outreach within 30 days, develop retention action plan
- **Critical (>75)**: Immediate advisor attention, retention intervention within 1 week

### Step 7 — Retention Strategy Recommendations

Map risk tiers to specific retention interventions:

**For Watch-tier clients:**
- Schedule a proactive check-in call (not a sales call — genuine relationship touch)
- Send personalized market commentary relevant to their portfolio
- Verify no outstanding action items or service issues

**For Elevated-tier clients:**
- Senior advisor or principal engagement within 30 days
- Performance review meeting with explicit expectations recalibration
- Fee review — proactively adjust if above-market for the AUM tier
- Service enhancement: upgrade meeting frequency, add digital access, provide enhanced reporting
- Address any specific life event with relevant planning expertise

**For Critical-tier clients:**
- Immediate senior leadership engagement (managing director, branch manager)
- Comprehensive relationship review: fees, performance, service, planning
- Proactive fee concession if competitiveness is a factor
- "Save" offer: Enhanced services, dedicated team, fee reduction — quantify the cost of save vs. cost of loss
- If departure is imminent: conduct a professional exit interview and maintain relationship for potential return

## Output Specification

```
## Client Attrition Risk Report — [Date]

### Risk Distribution
| Tier | Clients | AUM ($M) | Revenue ($K) | % of Total AUM |
|------|---------|---------|-------------|---------------|
| Low | XXX | $XXX | $X,XXX | XX% |
| Watch | XX | $XX | $XXX | XX% |
| Elevated | XX | $XX | $XXX | XX% |
| Critical | X | $X | $XX | XX% |

### Critical and Elevated Risk Clients
| Client | AUM ($M) | Revenue ($K) | Risk Score | Primary Driver | Recommended Action |
|--------|---------|-------------|-----------|----------------|-------------------|
| [Name] | $X.X | $XX | XX | [Driver] | [Action — timeline] |

### Risk Driver Analysis (Aggregate)
| Driver | % of At-Risk AUM | Trend |
|--------|-----------------|-------|
| Engagement decline | XX% | [↑↓→] |
| Performance gap | XX% | [↑↓→] |
| Service issues | XX% | [↑↓→] |
| Life events | XX% | [↑↓→] |
| Fee sensitivity | XX% | [↑↓→] |

### Retention ROI Analysis
- At-risk revenue (Elevated + Critical): $[X]
- Estimated retention rate with intervention: XX%
- Revenue saved: $[X]
- Cost of retention interventions: $[X]
- Retention ROI: [X]:1

### Trend Analysis
| Metric | Q-4 | Q-3 | Q-2 | Q-1 | Current |
|--------|-----|-----|-----|-----|---------|
| At-risk clients (Elevated+Critical) | XX | XX | XX | XX | XX |
| At-risk AUM ($M) | $XX | $XX | $XX | $XX | $XX |
| Actual departures | X | X | X | X | X |
| Model accuracy (predicted vs. actual) | XX% | XX% | XX% | XX% | — |
```

## Analysis Framework

Apply the **PULSE** framework:

- **P**atterns — Monitor engagement, performance, and service quality trends
- **U**nderlying causes — Identify the root drivers of dissatisfaction or disengagement
- **L**ife events — Track transition events that create relationship vulnerability
- **S**coring — Combine factors into actionable risk scores and tiers
- **E**ngagement — Deploy tier-appropriate retention interventions

## Examples

**Example 1 — Silent Disengagement Detection**

Client: $2.4M relationship, 6-year tenure. No complaints filed. No recent life events. Attrition score: 68 (Elevated). Why: Portal logins dropped from 12/quarter to 2/quarter over 6 months. Declined last two meeting invitations. Stopped opening quarterly performance emails. Performance: -1.2% vs. benchmark over trailing year. Assessment: Classic "silent disengager" — no dramatic event, just gradual withdrawal. Intervention: Senior advisor reaches out with personalized invitation to discuss year-end tax planning (high-value, time-sensitive topic). During conversation, address performance concerns and reaffirm value proposition. Outcome: Client revealed they had been approached by a competitor. After fee review and enhanced service commitment, client remained.

**Example 2 — Life-Event-Triggered Risk**

Client: $1.8M relationship, husband (primary contact) passed away 4 months ago. Wife (surviving spouse) has had minimal prior relationship with advisor. Attrition score: 72 (Elevated). Why: Surviving spouse has her own CPA who is recommending a different advisor. No proactive outreach from the advisor post-death beyond the initial condolence. Performance is fine; service quality is fine — the risk is purely relationship-driven. Intervention: Managing director and female senior advisor schedule an in-home meeting focused on the widow's needs and preferences. Present comprehensive widow-specific planning (retitling assets, Social Security survivor benefits, insurance review, estate settlement). Demonstrate that the team can serve HER needs, not just her late husband's relationship.

## Guidelines

- Score clients against their own engagement baseline, not population averages
- Weight AUM in prioritization — a critical-risk $5M client warrants more intervention than a critical-risk $200K client
- Distinguish controllable from uncontrollable attrition drivers in reporting
- Track model accuracy quarterly: compare predicted high-risk clients to actual departures
- Retrain the model at least annually using updated historical attrition data
- Conduct exit interviews for all departing clients to improve future prediction
- Ensure retention interventions are genuine value-adds, not desperate saves — clients can sense the difference
- Coordinate retention efforts across the team — avoid multiple uncoordinated contacts
- Document all retention interactions and outcomes for program effectiveness measurement

## Validation Checklist

- [ ] Engagement scoring uses client-specific baselines, not population averages
- [ ] Performance gap analysis accounts for client expectations, not just benchmark comparison
- [ ] Service quality metrics include both objective (response time) and subjective (complaint) measures
- [ ] Life event triggers are comprehensive and include appropriate risk windows
- [ ] Competitive/fee analysis uses current market benchmarking data
- [ ] Risk scoring model is weighted based on historical attrition driver analysis
- [ ] Retention interventions are differentiated by risk tier and primary driver
- [ ] ROI analysis accounts for both intervention cost and lifetime revenue at risk
- [ ] Model accuracy is tracked and the model is recalibrated periodically
- [ ] At-risk client list is reviewed and actioned within specified timeframes per tier
