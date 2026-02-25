---
name: exception-queue-prioritization
description: Prioritize and triage operations exception queues across banking functions. Use when managing work queues for payment exceptions, account servicing exceptions, lending exceptions, or compliance review queues, applying risk-based prioritization to optimize processing order and resource allocation.

metadata:
  display_name: "Exception Queue Prioritization"
  short_description: "Prioritize and triage banking operations exception queues"
  default_prompt: "Check my exception queue prioritization for gaps risks and required fixes"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Exception Queue Prioritization

## Overview

This skill produces structured prioritization frameworks for banking operations exception queues. It covers payment exceptions, account servicing exceptions, lending document exceptions, compliance review queues, and reconciliation breaks. The prioritization methodology balances regulatory deadlines, customer impact, financial exposure, and operational efficiency. Output supports queue managers, operations supervisors, and workforce management.

## When to Use

- Prioritizing daily exception queues when volume exceeds processing capacity
- Redesigning queue routing rules for improved efficiency
- Allocating staff across multiple exception queues based on risk and urgency
- Analyzing queue aging and bottleneck patterns
- Supporting regulatory compliance by ensuring deadline-driven items are processed first
- Balancing same-day processing requirements against backlog management
- Producing queue management reports for operations leadership

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Queue inventory | All active exception queues with current volumes | Queue management system |
| Item details | Exception type, amount, age, customer type, deadline | Queue item attributes |
| SLA targets | Processing time targets per exception type | SLA catalog |
| Regulatory deadlines | Reg E, Reg CC, NACHA, Fedwire cutoff times | Regulatory calendar |
| Staff availability | Available FTEs, skill levels, shift schedules | Workforce data |
| Historical throughput | Items processed per FTE per hour by type | Productivity metrics |
| Risk parameters | Financial exposure, customer tier, compliance risk | Risk assessment |

## Methodology

### Step 1: Inventory and Classify Exception Types

Catalog all exception types with their risk and urgency attributes:

| Exception Type | Regulatory Deadline | Financial Exposure | Customer Impact | Complexity |
|---------------|--------------------|--------------------|-----------------|------------|
| OFAC screening holds | Real-time/4 hours | Varies | High (payment delayed) | Medium |
| ACH returns | 2 banking days (RDFI) | Per item | Medium | Low |
| Wire repair (OFAC clear) | Same day (Fedwire hours) | High ($) | High | Medium |
| Reg E disputes | 10 business days (prov credit) | Per claim | High | High |
| NSF/overdraft decisions | Same day (before EOD posting) | Per item | High | Low |
| Unposted items | Same day | Varies | Medium | Medium |
| Loan document exceptions | Per pipeline SLA | Loan amount | Medium | High |
| Reconciliation breaks | T+1 | Break amount | Low (internal) | Medium |
| Account maintenance requests | Per SLA (24-48 hours) | Low | Medium | Low |
| Suspicious activity referrals | 30 days (SAR filing) | N/A | Low | High |

### Step 2: Apply the Risk-Based Prioritization Matrix

Score each exception item on four dimensions:

| Dimension | Weight | Score 1 (Low) | Score 3 (Medium) | Score 5 (High) |
|-----------|--------|--------------|------------------|----------------|
| **Regulatory urgency** | 35% | No regulatory deadline | Deadline >5 days | Deadline ≤2 days or today |
| **Financial exposure** | 25% | <$1,000 | $1,000-$50,000 | >$50,000 |
| **Customer impact** | 25% | Internal/back-office | Customer aware, low urgency | Customer waiting, complaint risk |
| **Aging** | 15% | <25% of SLA elapsed | 25-75% of SLA elapsed | >75% of SLA elapsed |

**Priority Score** = Σ (Weight × Score)

| Priority Tier | Score Range | Processing Order | Target Resolution |
|--------------|-------------|------------------|-------------------|
| **P1 — Critical** | 4.0-5.0 | Immediate, top of queue | Within 2 hours |
| **P2 — High** | 3.0-3.9 | Same day | Within 4 hours |
| **P3 — Medium** | 2.0-2.9 | Next business day | Within 24 hours |
| **P4 — Low** | 1.0-1.9 | Within SLA window | Within 48 hours |

### Step 3: Apply Priority Overrides

Certain conditions automatically elevate priority:

| Override Condition | Automatic Priority | Rationale |
|-------------------|-------------------|-----------|
| OFAC/sanctions hold | P1 | Regulatory blocking obligation |
| Reg E provisional credit deadline (day 8+) | P1 | Regulatory timeline, penalties |
| Fedwire same-day cutoff approaching | P1 | Irrevocable payment deadline |
| Executive/board member account | P1 | Reputation risk |
| Legal/subpoena response | P1 | Court-ordered deadline |
| ACH return deadline (midnight day 2) | P2 | NACHA rules, financial exposure |
| Customer complaint linked | P2 | UDAAP, complaint management |
| High-value item (>$500K) | P2 (minimum) | Financial exposure |

### Step 4: Allocate Resources to Queues

Match staffing to queue demands:

1. **Calculate demand**: Count items in each priority tier × average processing time per item
2. **Assess capacity**: Available FTEs × productive hours × items-per-hour by exception type
3. **Identify gaps**: Where demand exceeds capacity at each priority level
4. **Reallocate**: Shift resources from lower-priority queues to cover critical gaps
5. **Escalate**: When P1/P2 demand exceeds total capacity, escalate for management action (overtime, cross-training, temporary staff)

**Staffing allocation principle**: Never leave P1 items unprocessed while working P3 or P4 items. Dynamic reallocation during the day as queue compositions change.

### Step 5: Monitor Queue Health Metrics

Track real-time and daily queue performance:

| Metric | Definition | Target | Alert Threshold |
|--------|-----------|--------|-----------------|
| Queue depth | Total items pending | Varies by type | >120% of daily average |
| Aging rate | % of items >50% of SLA | <10% | >20% |
| P1 clearance time | Time from arrival to resolution for P1 items | <2 hours | >3 hours |
| Items per FTE/hour | Throughput productivity metric | Varies by type | <80% of benchmark |
| Inflow vs. outflow | New items arriving vs. items resolved | Outflow > inflow | Sustained inflow > outflow |
| Same-day clearance rate | % of items resolved on arrival day | >90% (P1/P2) | <85% |

### Step 6: Identify and Resolve Bottlenecks

Common queue bottlenecks and resolution strategies:

| Bottleneck | Indicator | Resolution |
|-----------|-----------|------------|
| Approval dependency | Items aging in "pending approval" status | Delegate approval authority, implement tiered limits |
| Information gaps | Items in "pending information" with no follow-up | Automated reminders, escalation timers |
| Skill mismatch | Complex items assigned to junior staff | Skill-based routing, tiered queue assignment |
| System limitations | Manual rekeying, multiple system lookups | System integration, single-screen resolution |
| Volume spikes | Predictable surges (month-end, payroll dates) | Flex staffing, pre-processing, automation |

### Step 7: Continuous Improvement

Use queue data to drive process improvement:

- **Root cause exceptions**: Why are items entering the exception queue? Can the root cause be eliminated?
- **Automation candidates**: Which exception types follow deterministic logic suitable for automation?
- **Straight-through processing**: What percentage of items could be auto-resolved with rule-based logic?
- **Prevention**: Can upstream controls prevent items from becoming exceptions?
- **Queue elimination**: Can process redesign eliminate entire exception categories?

## Output Specification

```markdown
# Exception Queue Prioritization Report: [Date]

## Queue Summary
| Queue | Total Items | P1 | P2 | P3 | P4 | Oldest Item | Staff Assigned |
|-------|-------------|----|----|----|----|-------------|----------------|
| [Queue] | [N] | [N] | [N] | [N] | [N] | [Age] | [N FTEs] |

## P1 Critical Items
| Item ID | Type | Amount | Deadline | Assigned To | Status |
|---------|------|--------|----------|-------------|--------|
| [ID] | [Type] | [$Amount] | [Time] | [Name] | [Working/Pending] |

## Resource Allocation
| Queue | Demand (hours) | Capacity (hours) | Gap | Action |
|-------|---------------|------------------|-----|--------|
| [Queue] | [X] | [X] | [+/-X] | [Reallocation details] |

## Queue Health
| Metric | Current | Target | Status |
|--------|---------|--------|--------|
| P1 clearance time | [X hrs] | <2 hrs | [Green/Amber/Red] |
| Same-day clearance | [X%] | >90% | [Green/Amber/Red] |
| Queue aging (>50% SLA) | [X%] | <10% | [Green/Amber/Red] |

## Bottlenecks and Actions
- [Bottleneck identified with resolution plan]

## Recommendations
- [Queue optimization recommendations]
```

## Analysis Framework

### Queue Aging Distribution

Analyze the age distribution within each queue:
- 0-25% of SLA: "Green zone" — on track
- 25-50% of SLA: "Yellow zone" — monitor
- 50-75% of SLA: "Orange zone" — expedite
- 75-100% of SLA: "Red zone" — critical, risk of breach
- >100% of SLA: "Breached" — immediate management attention

### Predictive Queue Management

Use historical data to forecast queue volumes:
- Day-of-week patterns (Monday volume spike, Friday wind-down)
- Calendar effects (month-end, quarter-end, holidays, tax dates)
- Correlation with transaction volumes (ACH batch processing, wire activity)
- Leading indicators (loan pipeline for doc exception forecasting)

## Examples

**Example 1 — Morning Queue Triage**:
"Queue triage 2025-10-20 08:30 AM: Total exceptions pending: 347 across 6 queues. P1 items: 12 (4 OFAC holds from overnight batch, 5 Reg E claims at day 9 of 10, 3 high-value wire repairs). Assigned 3 senior analysts to P1 items with target clearance by 10:30 AM. P2 items: 48 (32 ACH returns due by midnight, 16 customer-linked exceptions). Allocated 4 analysts to P2 queue. P3/P4: 287 items with same-day-or-next-day SLAs. Remaining 8 analysts assigned to P3/P4 processing. Capacity assessment: P1/P2 demand = 22 staff-hours, capacity = 28 staff-hours (adequate). P3/P4 demand = 48 staff-hours, capacity = 32 staff-hours (gap of 16 hours). Recommendation: authorize 2 hours overtime for 4 analysts to reduce backlog, or defer 50 P4 items to tomorrow."

**Example 2 — Bottleneck Resolution**:
"Analysis of the loan document exception queue reveals average aging of 4.2 days against a 3-day SLA (breach rate: 38%). Bottleneck identified: 67% of exceptions are 'pending title company response' with no automated follow-up. Average time in this status: 2.8 days. Resolution: (1) Implement automated escalation email to title company at 24-hour mark (IT, 2 weeks); (2) Establish backup title company relationships for SLA-sensitive transactions (Vendor Management, 30 days); (3) Add 'pending external' exception status with separate SLA clock to improve measurement accuracy (Operations, 1 week)."

## Guidelines

- Regulatory-deadline items must always be processed before discretionary items
- Never batch P1 items for "efficient processing later"; process immediately upon identification
- Maintain audit trail of priority assignments, especially for overrides
- Staff allocation should be reviewed at minimum twice daily (morning and mid-day)
- Cross-train staff on multiple exception types to enable flexible resource allocation
- Track and report queue management decisions to operations leadership daily
- Use queue data for capacity planning and staffing model updates monthly
- Automate priority scoring where possible to remove subjectivity from triage
- Escalate capacity shortfalls before SLA breaches occur, not after

## Validation Checklist

- [ ] All exception types are inventoried with regulatory deadlines identified
- [ ] Priority scoring matrix weights reflect institutional risk appetite
- [ ] Override conditions are documented and consistently applied
- [ ] Resource allocation balances demand against available capacity
- [ ] P1 items have individual tracking with assigned analyst and target time
- [ ] Queue health metrics are monitored in real-time during business hours
- [ ] Bottlenecks are identified with specific resolution plans
- [ ] Aging distribution is analyzed to prevent SLA breaches
- [ ] Continuous improvement recommendations target root cause elimination
- [ ] Queue management decisions are documented for audit trail
