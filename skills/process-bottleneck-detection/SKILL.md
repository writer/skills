---
name: process-bottleneck-detection
description: Identify and analyze operational bottlenecks in banking processes using Lean and Six Sigma methodologies. Use when investigating process slowdowns, cycle time degradation, throughput constraints, or capacity limitations across lending, payments, account servicing, and back-office operations.

metadata:
  display_name: "Process Bottleneck Detection"
  short_description: "Detect bottlenecks in banking operations processes"
  default_prompt: "Review my process bottleneck and highlight top risks and next actions"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Process Bottleneck Detection

## Overview

This skill produces structured bottleneck analyses for banking operations processes using Lean and Six Sigma methodologies. It covers value stream mapping, Theory of Constraints (TOC) application, cycle time analysis, WIP (work-in-progress) accumulation, and constraint identification. Output supports process improvement initiatives, capacity planning, and operational efficiency optimization across all banking functions.

## When to Use

- Investigating why a process is not meeting throughput or cycle time targets
- Conducting value stream mapping for process improvement initiatives
- Analyzing WIP accumulation patterns to identify constraint points
- Supporting Lean/Six Sigma DMAIC project define and measure phases
- Capacity planning when volume growth is straining current processes
- Evaluating the impact of process changes on end-to-end cycle time
- Preparing business cases for technology or staffing investments

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Process map | Current-state process flow with steps and handoffs | Process documentation |
| Cycle time data | Processing time at each step, wait time between steps | Time study data |
| Volume data | Input volume, output volume, WIP at each step | Operations metrics |
| Resource data | Staff, systems, capacity at each process step | Resource inventory |
| Quality data | Error rates, rework rates, first-pass yield at each step | Quality metrics |
| SLA/target | Expected cycle time and throughput targets | SLA definitions |
| Historical trends | Process performance over time | Trend data |

## Methodology

### Step 1: Map the Value Stream

Document the end-to-end process with Lean value stream mapping:

For each process step, capture:

| Step | Activity | Value/Non-Value | Cycle Time | Wait Time | Resources | WIP |
|------|----------|-----------------|------------|-----------|-----------|-----|
| 1 | [Activity] | [VA/NVA/BNVA] | [X min] | [X min] | [N FTEs] | [N items] |
| 2 | [Activity] | [VA/NVA/BNVA] | [X min] | [X min] | [N FTEs] | [N items] |

Classify each activity:
- **Value-Added (VA)**: Transforms the item in a way the customer values and is willing to pay for
- **Business Non-Value-Added (BNVA)**: Required by regulation, policy, or risk management but not customer-valued
- **Non-Value-Added (NVA)**: Pure waste — waiting, rework, unnecessary movement, over-processing

Calculate the **Process Cycle Efficiency (PCE)**:
PCE = Value-Added Time / Total Lead Time × 100%

Banking operations typically show PCE of 5-15%, indicating significant waste reduction opportunity.

### Step 2: Identify the Constraint (TOC)

Apply the Theory of Constraints to find the bottleneck:

**The bottleneck is the process step where**:
1. WIP accumulates in front of it (upstream queue growth)
2. Downstream steps are starved for work (waiting for input)
3. The step's cycle time × volume exceeds available capacity
4. The step has the lowest throughput rate in the process chain

**Bottleneck identification methods**:

| Method | How to Apply | Indicator |
|--------|-------------|-----------|
| **WIP analysis** | Find the step with the largest queue | Highest WIP count |
| **Utilization analysis** | Calculate utilization at each step | Step closest to 100% |
| **Throughput analysis** | Measure output rate at each step | Lowest output rate |
| **Wait time analysis** | Measure queue time before each step | Longest pre-step wait |
| **Capacity analysis** | Compare demand to capacity at each step | Smallest capacity margin |

### Step 3: Quantify the Bottleneck Impact

Measure the constraint's effect on the overall process:

- **Throughput limitation**: "The bottleneck limits overall process throughput to [X] items per day, while demand is [Y] items per day, creating a gap of [Z] items per day"
- **Cycle time extension**: "The bottleneck adds [X] hours of wait time, extending end-to-end cycle time from [ideal] to [actual]"
- **Quality impact**: "The bottleneck step has a [X%] error rate, causing [Y%] rework that consumes [Z] additional capacity hours"
- **Cost impact**: "The bottleneck drives [$X] in overtime, [$Y] in expediting costs, and [$Z] in SLA penalties per month"
- **Customer impact**: "[X%] of customers experience delays, generating [Y] complaints per month"

### Step 4: Analyze Root Causes of the Bottleneck

Determine why the constraint exists:

| Root Cause Category | Banking Examples |
|--------------------|-----------------|
| **Capacity constraint** | Insufficient staff for loan underwriting volume; system processing limit reached |
| **Dependency constraint** | Waiting for appraisal, title search, or third-party verification |
| **Batching constraint** | Items accumulated for batch processing instead of continuous flow |
| **Approval constraint** | Manual approval required from limited-availability personnel |
| **System constraint** | Legacy system throughput limits, manual data entry between systems |
| **Skill constraint** | Complex exceptions requiring specialized expertise in short supply |
| **Policy constraint** | Policy requires sequential review steps that could be parallelized |
| **Quality constraint** | High rework rate consuming capacity that should serve new items |

### Step 5: Apply the Five Focusing Steps (TOC)

Follow Goldratt's Theory of Constraints methodology:

1. **IDENTIFY** the constraint: Pinpoint the single step limiting throughput
2. **EXPLOIT** the constraint: Maximize output from the constraint without adding resources
   - Eliminate non-productive time at the bottleneck step
   - Ensure the constraint never waits for work (buffer inventory upstream)
   - Remove non-essential tasks from the constraint resource
   - Improve quality at upstream steps to prevent defective items reaching the constraint
3. **SUBORDINATE** everything else: Align non-constraint steps to serve the constraint
   - Pace upstream steps to the constraint's throughput (don't overproduce WIP)
   - Ensure downstream steps process constraint output immediately
4. **ELEVATE** the constraint: Add capacity at the constraint
   - Add staff, extend hours, or automate
   - Invest in technology to increase throughput
   - Outsource or cross-train to increase skilled capacity
5. **REPEAT**: After elevating, the bottleneck may shift — find the new constraint

### Step 6: Design the Improvement

Propose specific improvements based on Lean principles:

| Lean Principle | Application | Expected Impact |
|---------------|-------------|-----------------|
| **Eliminate waste** | Remove NVA steps (unnecessary reviews, duplicate data entry) | [X% cycle time reduction] |
| **Reduce batch sizes** | Process items individually rather than in batches | [X% wait time reduction] |
| **Create flow** | Redesign handoffs to enable continuous processing | [X% lead time reduction] |
| **Pull system** | Downstream steps signal readiness rather than push from upstream | [X% WIP reduction] |
| **Error-proofing (poka-yoke)** | Add validation to prevent errors at source | [X% rework reduction] |
| **Standardize work** | Document best practices to reduce variation | [X% consistency improvement] |
| **Cross-train** | Multi-skill staff to flex across constraint and non-constraint steps | [X% capacity flexibility] |

### Step 7: Validate and Monitor

Establish metrics to confirm improvement and sustain gains:

- **Lead time**: End-to-end process time (target: [X%] reduction)
- **Throughput**: Items completed per day (target: [X] items)
- **WIP**: Work-in-progress at each step (target: [X%] reduction)
- **PCE**: Process cycle efficiency (target: [X%] improvement)
- **First-pass yield**: Items completed without rework (target: [X%])
- **Customer wait time**: Time customer experiences delay (target: [X] reduction)

Implement control charts (X-bar/R or I-MR) to monitor for regression.

## Output Specification

```markdown
# Process Bottleneck Analysis: [Process Name]

## Process Overview
- **Process**: [Name and description]
- **Scope**: [Start point to end point]
- **Current Volume**: [X items/day]
- **Target Cycle Time**: [X hours/days]
- **Actual Cycle Time**: [X hours/days]
- **Process Cycle Efficiency**: [X%]

## Value Stream Summary
| Step | Activity | Type | Cycle Time | Wait Time | WIP | Utilization |
|------|----------|------|------------|-----------|-----|-------------|
| [#] | [Activity] | [VA/NVA/BNVA] | [Time] | [Time] | [N] | [X%] |

## Bottleneck Identification
- **Constraint Step**: [Step name and number]
- **Evidence**: [WIP accumulation, utilization, throughput data]
- **Root Cause**: [Why this step is the constraint]
- **Capacity**: [Current capacity vs. demand]

## Impact Quantification
| Metric | With Bottleneck | Without Bottleneck | Gap |
|--------|----------------|-------------------|-----|
| Throughput | [X/day] | [X/day] | [X/day] |
| Cycle time | [X hours] | [X hours] | [X hours] |
| Cost | [$X/month] | [$X/month] | [$X/month] |

## Improvement Recommendations
| # | Recommendation | Type | Expected Impact | Investment | Payback |
|---|---------------|------|-----------------|------------|---------|
| 1 | [Recommendation] | [Exploit/Elevate] | [Quantified impact] | [$X] | [X months] |

## Monitoring Plan
[Metrics, control charts, and review cadence for sustained improvement]
```

## Analysis Framework

### Little's Law Application

Apply Little's Law to validate bottleneck analysis:
**Lead Time = WIP / Throughput**

If WIP = 45 items and Throughput = 15 items/day, then Lead Time = 3 days.
To reduce lead time to 2 days at the same throughput: reduce WIP to 30 items.
To reduce lead time to 2 days at the same WIP: increase throughput to 22.5 items/day.

### Takt Time Calculation

Calculate the pace needed to meet demand:
**Takt Time = Available Time / Customer Demand**

Example: 8 hours available, 40 items demand → Takt time = 12 minutes per item.
Any step with cycle time exceeding takt time is a potential bottleneck.

### Process Capability Assessment

For variable cycle times, assess capability:
- Calculate Cp and Cpk for each step against SLA specification
- Cp < 1.0 indicates the process is not capable of meeting SLA
- Steps with low Cpk are variation-driven bottlenecks requiring standardization

## Examples

**Example 1 — Loan Origination Bottleneck**:
"Value stream analysis of the mortgage origination process (application to closing) reveals a 45-day average cycle time against a 30-day target. Bottleneck identified: underwriting review (Step 7 of 12). Evidence: WIP of 127 files in the underwriting queue vs. <20 at all other steps; underwriter utilization at 97%; upstream steps (processing, appraisal ordering) have capacity surplus. Root cause: 4 underwriters each process 6 files/day (24/day capacity) against an average inflow of 28 files/day, creating a 4-file daily deficit accumulating as queue growth. Exploit: eliminate non-underwriting tasks currently performed by underwriters (condition tracking, document chasing) — estimated capacity recovery of 15%. Elevate: hire 1 additional underwriter (6 files/day capacity addition, reducing utilization to 82%). Combined impact: reduce underwriting queue from 127 to <30 files, cutting cycle time from 45 to 32 days."

**Example 2 — Account Opening Bottleneck**:
"Digital account opening process analysis shows 72-hour average completion time against a same-day target for 80% of applications. Bottleneck: manual identity verification queue (Step 3). Of 150 daily applications, 45 (30%) fail automated CIP verification and route to manual review. Manual review capacity: 4 analysts × 8 items/hour = 32 items/day, creating a daily shortfall of 13 items. Additionally, manual review has a 15% rework rate due to incomplete customer outreach. Recommendations: (1) Implement document upload with OCR to resolve 40% of manual verifications automatically (reduce manual queue to 27/day); (2) Improve automated CIP matching algorithm to reduce fallout rate from 30% to 20% (reduce manual queue to 30/day before OCR); (3) Combined impact: manual queue reduced to 18/day, within current capacity of 32/day, enabling same-day processing for 95%+ of applications."

## Guidelines

- Always measure actual cycle times; do not rely on process documentation alone
- Distinguish between processing time (value-added work) and wait/queue time (waste)
- Focus improvement efforts on the single constraint; improving non-constraint steps yields no throughput gain
- Validate bottleneck identification with data, not assumptions or anecdotal reports
- Include both time and quality dimensions in the analysis
- Calculate financial impact to support investment business cases
- Apply Little's Law as a sanity check on cycle time and WIP relationships
- Present improvement recommendations with expected impact quantified
- Monitor for bottleneck migration after implementing improvements
- Use control charts to distinguish common-cause variation from special-cause events

## Validation Checklist

- [ ] End-to-end process is mapped with all steps, handoffs, and decision points
- [ ] Each step is classified as VA, NVA, or BNVA
- [ ] Cycle time and wait time are measured at each step with actual data
- [ ] WIP is measured at each step to identify accumulation points
- [ ] Bottleneck is identified with multiple supporting evidence (WIP, utilization, throughput)
- [ ] Root cause of the bottleneck is analyzed beyond the surface constraint
- [ ] Impact is quantified in throughput, cycle time, cost, and customer experience terms
- [ ] Improvement recommendations follow TOC five focusing steps
- [ ] Financial business case supports proposed investments
- [ ] Monitoring plan includes specific metrics, targets, and control chart methodology
