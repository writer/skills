---
name: clinical-workflow-optimization
description: Identify inefficiencies in clinical workflows through process analysis, bottleneck detection, and evidence-based improvement recommendations. Use when analyzing clinical operational processes, reducing documentation burden, optimizing care team task distribution, improving patient throughput, or supporting Lean/Six Sigma healthcare initiatives.

metadata:
  display_name: "Clinical Workflow Optimization"
  short_description: "Find and fix clinical workflow bottlenecks and waste"
  default_prompt: "Optimize my clinical workflow and suggest the best next steps"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Clinical Workflow Optimization

## Overview

Analyze clinical workflows to identify inefficiencies, bottlenecks, redundancies, and waste — then generate evidence-based recommendations for improvement. This skill applies Lean healthcare, Six Sigma, and human factors engineering principles to clinical operations including patient flow, documentation processes, care team coordination, order management, and communication pathways.

## When to Use

- Analyzing patient throughput bottlenecks in clinics, EDs, or inpatient units
- Reducing clinician documentation burden and EHR interaction time
- Optimizing care team task distribution (top-of-license practice)
- Improving order-to-completion turnaround times
- Supporting Lean/Six Sigma healthcare quality improvement projects
- Redesigning clinical workflows for new care models (telehealth, team-based care)

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Workflow description | Current-state process steps with roles and timing | Process map or narrative |
| Operational metrics | Cycle times, wait times, throughput, volumes | Numeric data |
| Stakeholder input | Pain points identified by clinicians and staff | Qualitative list |
| Technology environment | EHR system, tools, integrations in use | System inventory |
| Improvement goals | Target metrics or problem statements | Structured objectives |

## Methodology

### Step 1: Current-State Process Mapping

Document the existing workflow in detail:

**Process Elements to Capture:**
- Each step in the workflow with responsible role
- Decision points and branching logic
- Handoffs between team members or systems
- Wait times between steps
- Information inputs and outputs at each step
- Technology touchpoints (EHR, fax, phone, paper)

**Value Stream Classification:**
- Value-added (VA): Steps that directly contribute to patient care
- Non-value-added but necessary (NVAN): Required by regulation, safety, or policy
- Non-value-added waste (NVA): Pure waste — target for elimination

### Step 2: Waste Identification (8 Wastes of Healthcare - DOWNTIME)

Systematically identify waste in each category:

| Waste Type | Healthcare Example | Impact |
|-----------|-------------------|--------|
| **D**efects | Medication errors, wrong-site procedures, documentation errors | Patient safety, rework |
| **O**verproduction | Unnecessary tests, redundant documentation, over-ordering | Cost, patient burden |
| **W**aiting | Patient waiting for provider, lab results pending, prior auth delays | Throughput, satisfaction |
| **N**on-utilized talent | RNs doing clerical tasks, physicians doing data entry | Staff satisfaction, cost |
| **T**ransportation | Patient transfers for tests, specimen transport delays | Time, risk |
| **I**nventory | Expired supplies, excess stock, medication waste | Cost |
| **M**otion | Clinician walking between rooms, searching for equipment | Time, fatigue |
| **E**xtra processing | Duplicate data entry, redundant approvals, unnecessary clicks | Time, burnout |

### Step 3: Bottleneck Analysis

Identify and quantify process bottlenecks:

**Bottleneck Detection Methods:**
1. Capacity analysis: Where does demand exceed processing capacity?
2. Wait time accumulation: Where do the longest waits occur?
3. Queue length monitoring: Where do patient/task queues build up?
4. Constraint mapping: What single point, if improved, would increase overall throughput?

**Common Clinical Bottlenecks:**
- Provider-dependent order signing
- Prior authorization processing
- Lab/imaging result turnaround
- Discharge process (medication reconciliation, education, transport)
- Specialist referral and scheduling
- EHR documentation time

### Step 4: Root Cause Analysis

For each identified inefficiency, determine root causes:

**Analysis Tools:**
- 5 Whys: Ask "why" iteratively to reach the root cause
- Fishbone (Ishikawa) diagram: Categorize causes by People, Process, Technology, Environment, Policy
- Pareto analysis: Identify the 20% of causes creating 80% of the problem

### Step 5: Improvement Recommendations

Generate specific, actionable recommendations:

**Recommendation Framework:**
1. Quick wins (low effort, high impact): Implement within 1-2 weeks
2. Short-term improvements (moderate effort): Implement within 1-3 months
3. Strategic initiatives (high effort, transformational): Implement over 3-12 months

**Common Optimization Strategies:**
- Standardize: Create standard work protocols for repeatable processes
- Automate: Use EHR tools, order sets, templates, and clinical rules
- Delegate: Move tasks to appropriate team members (top-of-license)
- Parallelize: Perform independent tasks simultaneously rather than sequentially
- Eliminate: Remove unnecessary steps, approvals, or documentation
- Simplify: Reduce complexity, clicks, and decision points

## Output Specification

The output includes:

**workflow_analysis**: workflow_name, scope, current_state_summary, total_cycle_time, value_added_ratio, total_steps, waste_steps

**waste_inventory**: waste items categorized by DOWNTIME type, each with description, location_in_process, estimated_time_impact, estimated_cost_impact, root_cause

**bottlenecks**: bottleneck_location, description, capacity_vs_demand, average_wait_time, downstream_impact, root_cause

**recommendations**: recommendation, category (quick-win/short-term/strategic), target_waste_or_bottleneck, expected_improvement (time savings, cost reduction, quality impact), implementation_effort, responsible_role, dependencies

**future_state_metrics**: projected_cycle_time, projected_value_added_ratio, projected_throughput_improvement, projected_cost_savings

**implementation_roadmap**: phased timeline with milestones, owners, and success metrics

## Analysis Framework

### Clinical Documentation Burden Analysis

Documentation is often the largest source of clinician time waste:

| Metric | Benchmark | Action if Exceeded |
|--------|-----------|-------------------|
| EHR time per patient | Less than 16 minutes | Template optimization, scribes, ambient AI |
| Documentation after hours | Less than 30 min/day | Workflow redesign, note templates |
| Clicks per order | Less than 5 | Order set optimization |
| Inbox messages per day | Less than 50 | Triage protocols, team-based management |
| Copy-forward rate | Less than 30% | CDI review, template improvement |

### Patient Throughput Metrics

| Metric | ED Target | Clinic Target | Inpatient Target |
|--------|-----------|---------------|-----------------|
| Door-to-provider | Less than 30 min | Less than 15 min | N/A |
| Door-to-disposition | Less than 4 hours | N/A | N/A |
| Cycle time (arrival to departure) | Less than 4.5 hours | Less than 60 min | N/A |
| Discharge order to departure | N/A | N/A | Less than 3 hours |
| Bed turnover time | N/A | N/A | Less than 60 min |

## Examples

**Input**: Primary care clinic with 45-minute average visit cycle time (target: 30 minutes). Providers spending 18 minutes per visit on EHR documentation. MAs performing rooming in 5 minutes but then idle for 10 minutes while provider finishes previous visit note.

**Analysis (abbreviated)**:
- Bottleneck: Provider documentation between visits creating cascade delays
- Waste identified: Waiting (MA idle 10 min), Extra processing (18 min EHR time exceeds benchmark), Non-utilized talent (MA idle time)
- Root causes: No documentation templates for common visits, provider completing notes sequentially rather than in parallel with MA rooming
- Recommendations:
  1. Quick win: Create smart-phrase templates for top 10 visit types (save 5 min/visit)
  2. Quick win: MA performs HPI intake using structured questionnaire during idle time
  3. Short-term: Implement team documentation model (MA documents vitals/HPI, provider reviews and completes)
  4. Strategic: Evaluate ambient AI documentation tools for note generation

## Guidelines

1. **Observe before recommending** — base analysis on actual workflow data, not assumptions
2. **Involve frontline staff** — clinicians and staff closest to the work identify issues best
3. **Measure before and after** — quantify improvements with data
4. **Avoid burdenshifting** — ensure optimization does not simply move burden to another role or step
5. **Maintain safety** — never optimize away safety-critical steps (double-checks, timeouts, reconciliation)

## Validation Checklist

- [ ] Current-state process is accurately mapped with times and roles
- [ ] All eight waste categories (DOWNTIME) are systematically evaluated
- [ ] Bottlenecks are identified with quantitative impact data
- [ ] Root causes are identified (not just symptoms)
- [ ] Recommendations are specific, actionable, and assigned to responsible roles
- [ ] Expected improvements are quantified with realistic projections
- [ ] Safety-critical steps are preserved in all optimization recommendations

## HIPAA Compliance Notes

- Workflow data often includes patient volumes, timing, and operational PHI
- Process improvement observations in clinical areas must not compromise patient privacy
- Video or time-motion studies require appropriate consent and IRB review if applicable
- Workflow optimization data shared with consultants requires BAA
- EHR usage analytics (click tracking, time studies) may contain identifiable user data requiring privacy protections
