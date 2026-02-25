---
name: Customer Complaint Root Cause Analyzer
description: Identify systemic CX issues by analyzing customer complaint data across channels, applying root cause analysis frameworks to distinguish symptoms from underlying process, policy, or system failures driving repeat dissatisfaction.

metadata:
  display_name: "Customer Complaint Root Cause Analyzer"
  short_description: "Analyze customer complaints for systemic root causes"
  default_prompt: "Analyze my customer complaint root cause and recommend clear next actions"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Customer Complaint Root Cause Analyzer

## Overview

This skill moves beyond surface-level complaint categorization to uncover the systemic root causes behind customer dissatisfaction. Individual complaints are symptoms; this skill traces those symptoms back to underlying failures in processes, policies, systems, training, or vendor performance. By identifying and addressing root causes, retailers can eliminate entire classes of complaints rather than repeatedly treating individual occurrences.

## When to Use

- When complaint volumes spike in a category without an obvious trigger
- During quarterly or annual CX program reviews to identify systemic improvement priorities
- When specific stores, channels, or product categories show persistent complaint patterns
- After operational changes (new system launch, policy update, vendor switch) to detect unintended CX impacts
- To build the business case for process or system investments by quantifying complaint-driven costs
- When NPS or CSAT trends downward and the cause is unclear

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `complaint_records` | Full complaint dataset with timestamps, channel, category, verbatim text, resolution | Tabular with text fields |
| `complaint_taxonomy` | Hierarchical categorization scheme (L1/L2/L3 categories) | Reference data |
| `operational_events` | Log of system changes, policy updates, vendor changes, process modifications | Event log |
| `store_operations_data` | Store-level metrics (staffing, process compliance, training completion) | Tabular |
| `order_data` | Order details linked to complaints (product, fulfillment method, timeline) | Tabular |
| `system_incident_log` | IT system outages, errors, degraded performance events | Event log (optional) |
| `agent_resolution_data` | How complaints were resolved, by whom, time to resolution | Tabular (optional) |

## Methodology

### Step 1 — Complaint Data Normalization and Enrichment

Prepare the complaint dataset for analysis:

1. **Text Normalization**: Standardize verbatim complaint text — lowercase, remove PII, correct common misspellings, expand abbreviations.
2. **Category Validation**: Verify that complaint categorization is consistent. Use NLP-based reclassification to identify miscategorized complaints (agent-applied categories are wrong approximately 15-25% of the time).
3. **Enrichment Joins**: Link complaints to order data (product, fulfillment method, timeline), store data (region, format, staffing levels), and customer data (segment, tenure, lifetime value).
4. **Duplicate Detection**: Identify and consolidate complaints from the same customer about the same issue across channels (e.g., called and also emailed).

### Step 2 — Pattern Detection

Identify statistically significant complaint patterns:

1. **Volume Trend Analysis**: Time-series decomposition of complaint volumes by category. Separate trend, seasonality, and anomaly components. Flag categories with volume increases exceeding 2 standard deviations.
2. **Correlation Clustering**: Identify complaint categories that spike simultaneously — these often share a common root cause (e.g., "late delivery" and "wrong item" both spike when a warehouse is understaffed).
3. **Cohort Analysis**: Compare complaint rates across cohorts (new vs. returning customers, BOPIS vs. ship-to-home, store A vs. store B) to isolate variables.
4. **Text Mining**: Apply topic modeling (LDA or BERTopic) to complaint verbatims to discover complaint themes not captured by the existing taxonomy.

### Step 3 — Root Cause Tracing

For each significant complaint pattern, trace to the root cause using structured analysis:

1. **Five Whys Analysis**: Iteratively ask "why" to move from symptom to cause. Document each level.
   - Why are customers complaining about late delivery? Because orders are shipped 2 days after the promised date.
   - Why are orders shipped late? Because the warehouse is processing orders slower than target.
   - Why is processing slower? Because a new WMS module is requiring manual workarounds.
   - Why are manual workarounds needed? Because the WMS was deployed without integration to the cartonization system.
   - Why was integration skipped? Because the project timeline was compressed to hit a launch date.
   - Root cause: Incomplete system integration due to project timeline pressure.

2. **Ishikawa (Fishbone) Categorization**: Classify root causes into standard categories:
   - **Process**: Steps are missing, unclear, or poorly sequenced.
   - **Policy**: Rules create friction or are misaligned with customer expectations.
   - **People**: Training gaps, understaffing, or unclear role accountability.
   - **Technology**: System bugs, integration failures, or capability gaps.
   - **Vendor/Partner**: Third-party performance failures (carriers, suppliers, service providers).
   - **Product**: Design defects, quality issues, or misleading product information.

3. **Event Correlation**: Align complaint spikes with the operational event log to identify triggering changes. Use time-lagged correlation — process changes may take 1-4 weeks to manifest in complaints.

### Step 4 — Impact Quantification

Size the business impact of each root cause:

- **Complaint Volume**: Number of complaints attributable to this root cause (direct and estimated indirect).
- **Customer Impact**: Number of unique customers affected, segmented by value tier.
- **Cost of Complaints**: Agent handling time x cost per minute + appeasement costs (credits, coupons, replacements) + shipping costs for re-fulfillment.
- **Revenue Risk**: Estimated churn probability x customer lifetime value for affected customers. Use published retail churn rates (a customer who complains is 4x more likely to defect than one who does not).
- **Brand Impact**: Social media amplification — complaints shared publicly vs. resolved privately.

### Step 5 — Remediation Recommendations

Develop specific, actionable remediation plans:

1. **Quick Wins** (under 2 weeks): Policy clarifications, script updates, FAQ additions, agent empowerment expansions.
2. **Medium-Term Fixes** (2-8 weeks): Process redesigns, training programs, vendor SLA renegotiations, system configuration changes.
3. **Strategic Investments** (2-6 months): System replacements, organizational restructuring, capability building.

For each recommendation, specify: owner, timeline, success metric, and expected complaint volume reduction.

## Output Specification

Produce a root cause analysis report containing:

- `analysis_period`: Date range analyzed
- `total_complaints`: Total volume and period-over-period change
- `complaint_patterns`: Array of statistically significant patterns, each with category, volume, trend direction, severity, and affected segments
- `root_causes`: Array of identified root causes, each with:
  - `cause_id`: Unique identifier
  - `description`: Clear statement of the root cause
  - `category`: Ishikawa category (process, policy, people, technology, vendor, product)
  - `five_whys_chain`: Array showing the logical trace from symptom to root cause
  - `evidence`: Data points supporting the root cause identification
  - `complaints_attributed`: Number of complaints linked to this cause
  - `revenue_at_risk`: Estimated revenue impact
  - `cost_of_inaction`: Monthly ongoing cost if not addressed
- `remediation_plan`: Prioritized array of actions with owner, timeline, cost estimate, expected impact, and success metrics
- `monitoring_plan`: Metrics and thresholds to track post-remediation

## Analysis Framework

Apply the **Complaint Iceberg Model**:

- **Visible (5%)**: Formal complaints received through contact center, email, social media.
- **Semi-Visible (25%)**: Complaints expressed through low survey scores, negative reviews, or reduced purchase frequency.
- **Hidden (70%)**: Silent dissatisfaction — customers who experience the issue but do not complain. They simply reduce engagement or defect.

For every visible complaint, estimate the total affected population using industry ratios (1 complaint represents 20-50 similar experiences). Size recommendations based on the full iceberg, not just the visible tip.

## Examples

**Example Root Cause Analysis**:

Pattern: "Item Not As Described" complaints increased 340% in Home Decor category over 8 weeks.

Five Whys trace: (1) Customers say the product color does not match photos. (2) Product photos were recently reshot with new studio lighting. (3) New lighting setup was not color-calibrated to match in-home viewing conditions. (4) Photo studio vendor changed equipment without updating color profiles. (5) Vendor contract did not include color accuracy specifications.

Root cause: Vendor management gap — photo studio contract lacks color fidelity standards.

Impact: 1,240 complaints, estimated 24,800 affected customers (using 1:20 ratio), $186K in return shipping costs, $312K in revenue at risk from customer defection.

Remediation: (a) Immediate: add color calibration reference card to all photo shoots; re-photograph top 50 SKUs by complaint volume. (b) Medium-term: update vendor SOW with Delta E color accuracy requirements and acceptance testing protocol. (c) Strategic: implement automated color consistency checking in the digital asset pipeline.

## Guidelines

- Always validate root causes with multiple evidence sources — never rely on a single data point or anecdote.
- Distinguish between root causes and contributing factors. A root cause, if eliminated, prevents recurrence. A contributing factor increases severity but is not the origin.
- Avoid blame-oriented language. Frame root causes as system or process failures, not individual failures.
- Challenge existing complaint taxonomies — many taxonomies are agent-convenience-oriented, not analytically useful.
- Include the customer's voice by incorporating verbatim quotes (anonymized) that illustrate the lived experience behind the data.
- Account for complaint channel bias — certain demographics and issue types are overrepresented in certain channels.
- Consider seasonal context when analyzing trends — holiday period complaints about delivery speed are structurally different from off-peak complaints.
- Size the silent majority — the complaints you receive are the minority of affected customers.

## Validation Checklist

- [ ] Complaint data has been deduplicated across channels (same customer, same issue)
- [ ] NLP reclassification has been applied to validate agent-assigned categories
- [ ] Statistical significance testing applied to all identified patterns (chi-square or equivalent)
- [ ] Five Whys analysis reaches a true root cause (actionable, systemic) and not another symptom
- [ ] Ishikawa categorization is consistent and each root cause fits exactly one category
- [ ] Impact quantification includes both direct costs and estimated revenue risk
- [ ] Silent majority multiplier (1:20 or 1:50 ratio) is applied and stated explicitly
- [ ] Remediation plan includes quick wins, medium-term fixes, and strategic investments
- [ ] Each recommendation has a named owner role, timeline, and measurable success criterion
- [ ] Monitoring plan defines specific metrics and alert thresholds for post-remediation tracking
