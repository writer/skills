---
name: bcp-readiness-analysis
description: Analyze business continuity planning readiness for financial institutions. Use when assessing BCP program maturity, evaluating business impact analyses, reviewing recovery strategies, testing disaster recovery plans, or responding to FFIEC BCP Handbook examination expectations and OCC Heightened Standards requirements.

metadata:
  display_name: "Bcp Readiness Analysis"
  short_description: "Assess bank business continuity and disaster readiness"
  default_prompt: "Optimize my bank business continuity and disaster and suggest the best next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Business Continuity Planning Readiness Analysis

## Overview

Assess business continuity planning (BCP) readiness across financial institution operations, technology, and third-party ecosystems. This skill applies the FFIEC Business Continuity Planning Handbook, OCC Heightened Standards (12 CFR 30 Appendix D), and NIST SP 800-34 (Contingency Planning Guide) to evaluate BCP program maturity, business impact analysis completeness, recovery strategy adequacy, and testing program effectiveness.

## When to Use

- Assessing overall BCP program maturity and examination readiness
- Evaluating business impact analysis (BIA) completeness and currency
- Reviewing IT disaster recovery plans and testing results
- Assessing pandemic, cyber resilience, and work-from-home continuity plans
- Preparing for FFIEC or OCC examinations focused on business continuity
- Evaluating third-party BCP capabilities for critical vendors

## Required Inputs

- **BCP program documentation**: BCP policy, program charter, governance structure, plan maintenance schedule
- **Business impact analyses**: BIA results by business unit, criticality tiers, RTO/RPO definitions
- **Recovery plans**: Business unit recovery plans, IT disaster recovery plans, crisis communication plans
- **Testing results**: Test schedules, exercise results, action item tracking, lessons learned
- **Third-party BCP**: Critical vendor BCP assessments, contractual BCP requirements
- **Incident history**: Prior activations, near-misses, pandemic response experience

## Methodology

### Step 1: BCP Governance and Program Assessment

Evaluate the BCP governance framework against FFIEC Handbook expectations:

- Board has approved BCP policy and receives regular program reporting
- Senior management has designated a BCP program owner with authority and resources
- BCP responsibilities are integrated into business line management accountability
- Policy defines scope, objectives, roles, and addresses FFIEC/OCC requirements
- Standards address minimum BIA requirements, testing frequency, and maintenance cycles

Assess all FFIEC program elements: Business Impact Analysis, Risk Assessment, Recovery Strategies, Plan Development, Testing, Maintenance, and Training/Awareness.

### Step 2: Business Impact Analysis (BIA) Evaluation

Assess the quality and completeness of the institution's BIA:

- **Scope**: All business functions and critical processes included
- **Criticality classification**: Clear tiering (Critical, Essential, Important, Non-Essential) with defined criteria
- **Recovery objectives**: RTO and RPO defined based on business impact, not technology capability
- **Dependencies**: Upstream and downstream process dependencies mapped
- **Resource requirements**: Minimum staffing, technology, facilities, and data specified
- **Financial impact**: Revenue loss, penalties, and reputational damage quantified at progressive intervals
- **Peak periods**: Seasonal dependencies identified (month-end, quarter-end, tax season)
- **Currency**: Updated within 12 months and validated by business owners

BIA quality scoring: Completeness of scope (20%), RTO/RPO appropriateness (25%), Dependency mapping (20%), Financial impact analysis (15%), Currency and validation (20%).

### Step 3: Recovery Strategy Assessment

Evaluate whether recovery strategies meet BIA-defined objectives across four dimensions:

**Technology**: Backup strategy (frequency, offsite, encryption), data replication (sync/async, RPO alignment), alternate processing (hot/warm/cold/cloud), network redundancy, application recovery sequencing.

**Business Operations**: Alternate work locations, remote work capacity, manual workaround procedures, vital records management.

**People and Communication**: Crisis management team with succession, mass notification system, customer communication templates, regulatory notification procedures with defined triggers.

**Third-Party**: Critical vendor BCP capabilities assessed, contractual BCP provisions, alternate vendor arrangements, fourth-party dependencies understood.

### Step 4: Testing Program Effectiveness Review

Assess the BCP testing program against FFIEC expectations:

| Plan Type | Minimum Frequency | Progressive Complexity |
|-----------|-------------------|----------------------|
| Enterprise crisis management | Annually | Tabletop → Simulation |
| IT disaster recovery | Semi-annually | Walkthrough → Failover |
| Business unit recovery | Annually | Checklist → Functional |
| Communication/notification | Quarterly | Call tree → Full notification |

Tests must use realistic scenarios, define measurable objectives and success criteria, validate actual RTO/RPO achievement, include cross-functional dependencies, and formally document results with gap action items tracked to remediation.

### Step 5: Cyber Resilience Integration

Assess BCP and cybersecurity integration per FFIEC and NIST CSF: cyber scenarios in BCP testing (ransomware, data destruction), recovery plans for compromised backups, immutable backup strategies, coordinated incident response and BCP escalation, evidence preservation procedures, and breach notification requirements.

### Step 6: Pandemic and Extended Disruption Readiness

Evaluate preparedness for prolonged disruptions: remote work infrastructure for sustained (>30 day) operations, essential function staffing with geographic distribution and cross-training, supply chain continuity, customer service resilience, employee health protocols, and integration of prior pandemic lessons learned.

### Step 7: Readiness Scoring and Remediation Planning

Score each BCP component against a maturity model, identify gaps between readiness and regulatory expectations, prioritize remediation by risk exposure and regulatory urgency, develop a multi-year maturity roadmap, and prepare examination-ready evidence packages.

## Output Specification

```markdown
# BCP Readiness Assessment Report

## Executive Summary
[Overall readiness rating, key strengths, critical gaps, strategic recommendations]

## BCP Program Maturity Scorecard
| Component | Maturity (1-5) | FFIEC Alignment | Key Gaps |
|-----------|---------------|-----------------|----------|

## BIA Assessment
[Completeness evaluation, RTO/RPO analysis, dependency mapping adequacy]

## Recovery Strategy Analysis
| Critical Function | RTO Target | RTO Capability | RPO Target | RPO Capability | Gap |

## Testing Program Review
| Test Type | Last Conducted | Result | Open Actions | Next Scheduled |

## Remediation Roadmap
| Gap | Priority | Remediation | Owner | Timeline | Investment |
```

## Analysis Framework

BCP maturity model aligned with FFIEC expectations:

| Level | Description |
|-------|-------------|
| 1 — Initial | Informal plans, no structured program, limited testing |
| 2 — Developing | BIA completed, basic plans documented, annual testing initiated |
| 3 — Defined | Comprehensive program with governance, regular testing, maintenance cycle |
| 4 — Managed | Integrated program with metrics, progressive testing, continuous improvement |
| 5 — Optimized | Resilience-focused, real-time monitoring, adaptive planning, industry-leading |

## Examples

**Example 1 — RTO/RPO Gap Finding**:
"The Commercial Lending division's BIA defines a 4-hour RTO for the loan origination system. IT DR testing demonstrated a 14-hour recovery time (8hr database restore + 4hr reconfiguration + 2hr reconciliation). The RPO of 24 hours (daily backup) also exceeds the BIA-defined 4-hour RPO. Recommend: implement database replication (reducing RPO to <1hr and RTO to <2hrs), estimated $350K with 6-month implementation."

**Example 2 — Testing Program Deficiency**:
"The institution has not performed a full functional recovery test of the core banking platform in 28 months. The last payments DR failover (18 months ago) failed to restore within RTO — the remediation action item remains open. Per FFIEC BCP Handbook, testing should demonstrate recovery within established timeframes. Recommend: (1) conduct DR failover for core banking and payments within 60 days, (2) resolve open failed-test action items immediately, (3) establish semi-annual DR testing for all Tier 1 systems."

## Guidelines

- Assess BCP holistically, not just at the technology disaster recovery level
- BIA-defined RTOs/RPOs should drive recovery strategy investment, not the reverse
- Testing is the most critical element; untested plans provide false confidence
- Consider interdependencies between business units during recovery
- Integrate pandemic and cyber resilience into the core BCP program
- Third-party BCP assessment is a regulatory expectation, not optional

## Validation Checklist

- [ ] BCP governance assessed against FFIEC Handbook and OCC expectations
- [ ] BIA evaluated for completeness, currency, and business-owner validation
- [ ] RTO/RPO targets compared against demonstrated recovery capabilities
- [ ] Recovery strategies assessed for technology, operations, people, and third parties
- [ ] Testing program evaluated for frequency, scope, realism, and action follow-through
- [ ] Cyber resilience integration assessed including immutable backup strategies
- [ ] Pandemic and extended disruption readiness validated
- [ ] Readiness scores mapped to FFIEC maturity expectations
- [ ] Remediation roadmap prioritized with owners, timelines, and investment
