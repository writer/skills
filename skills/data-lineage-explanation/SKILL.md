---
name: data-lineage-explanation
description: Explain data traceability and lineage for financial institution data assets. Use when documenting data flows for regulatory reporting, tracing data from source to consumption, assessing data quality risks, supporting model risk management, or responding to BCBS 239 and FFIEC data governance expectations.

metadata:
  display_name: "Data Lineage Explanation"
  short_description: "Explain data lineage and traceability for bank reporting"
  default_prompt: "Explain my data lineage in simple words and next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Data Lineage Explanation

## Overview

Document and explain data traceability and lineage across financial institution data ecosystems. This skill applies BCBS 239 (Principles for Effective Risk Data Aggregation and Risk Reporting), FFIEC IT Examination Handbook (Information Security and Operations booklets), and COSO Principle 13 (uses relevant, quality information) to produce clear, auditable data lineage documentation supporting regulatory reporting, model risk management, and data governance programs.

## When to Use

- Documenting data lineage for regulatory reports (Call Reports, FR Y-9C, CCAR/DFAST)
- Tracing data from source systems through transformations to consumption points
- Assessing data quality risks in critical data elements used for risk management
- Supporting model risk management with data provenance documentation (SR 11-7)
- Responding to regulatory findings on data governance or data quality
- Preparing for BCBS 239 compliance assessments
- Explaining data flows to non-technical stakeholders, auditors, or examiners

## Required Inputs

- **Data element(s)**: Specific data fields, metrics, or reports to trace
- **System inventory**: Source systems, data warehouses, ETL pipelines, reporting platforms
- **Transformation logic**: Business rules, calculations, aggregations, derivations
- **Data dictionaries**: Field definitions, data types, valid values, business glossary
- **Governance documentation**: Data ownership, stewardship assignments, quality thresholds
- **Regulatory context**: Applicable reporting requirements and submission deadlines

## Methodology

### Step 1: Scope and Critical Data Element Identification

Define the scope of the lineage documentation effort:

- Identify the target report, metric, or data asset requiring lineage documentation
- Enumerate the Critical Data Elements (CDEs) that comprise or feed into the target
- Classify each CDE by regulatory significance: Tier 1 (direct regulatory submission fields), Tier 2 (inputs to regulatory calculations), Tier 3 (operational data supporting risk management)
- Prioritize lineage documentation based on materiality, regulatory sensitivity, and known data quality issues
- Map CDEs to the institution's enterprise data model and business glossary

### Step 2: Source System Identification and Authoritative Source Designation

Trace each CDE to its system of origin:

- Identify the authoritative source (golden source) for each data element
- Document alternative sources and reconciliation requirements where multiple sources exist
- Capture source system metadata: platform, database, schema, table, field, data type, refresh frequency
- Assess source system reliability: uptime SLA, known data quality issues, change management processes
- Document manual data entry points and associated control risks
- Identify any third-party data feeds and their SLA/quality commitments

### Step 3: Transformation and Business Rule Documentation

Document every transformation between source and consumption:

- **Extraction**: How data is pulled from source systems (API, direct query, file transfer, CDC)
- **Transformation**: Business rules applied, calculations performed, data type conversions, field mappings
- **Loading**: Target system ingestion process, conflict resolution rules, historical preservation approach
- **Aggregation**: Summarization logic, grouping criteria, hierarchical roll-up rules
- **Derivation**: Calculated fields, proxy methodologies, estimation techniques
- **Filtering**: Inclusion/exclusion criteria, date range parameters, entity scope

For each transformation, document: unique ID, input and output fields, business rule (plain language), technical implementation reference, business and technical owners, and change control process.

### Step 4: Data Quality Control Point Mapping

Identify and document data quality controls along the lineage path:

- **Completeness checks**: Null/blank validation, mandatory field enforcement, record count reconciliation
- **Accuracy checks**: Reasonableness testing, cross-system reconciliation, historical trend comparison
- **Timeliness checks**: SLA monitoring, data freshness indicators, latency measurement
- **Consistency checks**: Cross-field validation, referential integrity, format standardization
- **Validity checks**: Domain validation, business rule compliance, regulatory code validation

Map each control to COSO Principle 13 requirements and BCBS 239 principles (accuracy, completeness, timeliness, adaptability).

### Step 5: Data Flow Visualization

Create layered documentation: **Level 1 — Conceptual** (major system boundaries for executive audiences), **Level 2 — Logical** (specific data elements, transformation points, quality gates for management/auditors), **Level 3 — Physical** (tables, fields, ETL jobs, scheduling for technology teams). Use consistent notation: rectangles for systems, diamonds for transformations, circles for quality checkpoints, labeled arrows for data flow direction.

### Step 6: BCBS 239 Compliance Assessment

Evaluate lineage completeness against BCBS 239 principles:

| Principle | Assessment Question |
|-----------|-------------------|
| Accuracy | Can the data be traced to authoritative sources with documented transformations? |
| Completeness | Does the lineage cover all CDEs with no undocumented transformations? |
| Timeliness | Are data freshness requirements documented with SLA monitoring? |
| Adaptability | Can the lineage accommodate ad-hoc reporting requests and stress scenarios? |
| Governance | Are data owners, stewards, and quality thresholds clearly assigned? |

### Step 7: Lineage Documentation and Narrative Generation

Produce final documentation combining technical lineage with business-context narrative:

- Write plain-language explanations of each data flow segment for non-technical audiences
- Document assumptions, limitations, and known data quality risks
- Include attestation requirements for data owners and stewards
- Reference applicable regulatory requirements and examination expectations
- Provide maintenance and update procedures for keeping lineage current

## Output Specification

```markdown
# Data Lineage Report: [Report/Metric Name]

## Executive Summary
[Plain-language overview of the data flow, key systems, and governance structure]

## Critical Data Elements
| CDE | Business Definition | Authoritative Source | Regulatory Tier | Data Owner |
|-----|-------------------|---------------------|-----------------|------------|

## Data Flow Narrative
### Source Layer
[Description of originating systems and data capture]

### Transformation Layer
[Business rules, calculations, and aggregation logic in plain language]

### Consumption Layer
[Final reporting, dashboards, regulatory submissions]

## Data Flow Diagram
[Level 1 conceptual diagram description or reference]

## Transformation Inventory
| Step | Input | Transformation | Output | Business Rule | Owner |
|------|-------|---------------|--------|---------------|-------|

## Data Quality Controls
| Control Point | Type | Description | Threshold | Frequency | Owner |
|--------------|------|-------------|-----------|-----------|-------|

## BCBS 239 Compliance Assessment
| Principle | Status | Gaps | Remediation |
|-----------|--------|------|-------------|

## Known Limitations and Risks
[Documented gaps, manual interventions, single points of failure]

## Governance
| Role | Name | Responsibilities |
|------|------|-----------------|
| Data Owner | [name] | Accountable for data quality and fitness for purpose |
| Data Steward | [name] | Day-to-day data quality monitoring and issue resolution |
| Technical Owner | [name] | System and pipeline maintenance, change management |

## Maintenance Schedule
[Frequency and triggers for lineage documentation updates]
```

## Analysis Framework

Data lineage maturity assessment model:

| Maturity Level | Characteristics |
|---------------|----------------|
| Level 1 — Ad Hoc | Lineage is tribal knowledge, undocumented, person-dependent |
| Level 2 — Documented | Lineage documented manually, updated periodically, gaps remain |
| Level 3 — Managed | Lineage systematically maintained, quality controls in place, owner accountability |
| Level 4 — Automated | Lineage auto-discovered and maintained by tooling, integrated with data catalog |
| Level 5 — Optimized | Real-time lineage, impact analysis capabilities, proactive quality monitoring |

## Examples

**Example 1 — Regulatory Report Lineage**:
"The Tier 1 Capital Ratio reported on the FR Y-9C (Schedule HC-R) originates from three authoritative sources: (1) General Ledger (SAP) provides Common Equity Tier 1 capital components from GL accounts 3000-3199, aggregated through the Finance Data Warehouse using business rules documented in ETL Job FDW-CAP-001; (2) Risk-Weighted Assets are calculated by the credit risk engine (Moody's RiskAuthority) using exposure data from the loan origination system, with risk weights applied per Basel III standardized approach; (3) Regulatory adjustments are manually entered by the Capital Management team using a controlled spreadsheet with dual-approval workflow. All three data streams converge in the Regulatory Reporting Platform (AxiomSL) where final reconciliation occurs against the prior quarter submission with a ±2% variance threshold."

**Example 2 — Data Quality Risk Identification**:
"Lineage analysis of the allowance for credit losses (ACL) model reveals an undocumented manual override step between the model output and the final GL posting. The Portfolio Management team applies qualitative adjustment factors via an uncontrolled Excel spreadsheet that is not subject to the institution's model risk management framework (SR 11-7). This represents a data quality risk as: (1) the override logic is not version-controlled, (2) no reconciliation exists between the model output and adjusted values, (3) the qualitative factors lack documented methodology. Recommend: formalize the qualitative adjustment process within the model governance framework and implement automated reconciliation controls."

## Guidelines

- Always trace lineage from authoritative source to final consumption; never assume intermediate systems are well-documented
- Use plain language for business-context narratives; reserve technical detail for Level 3 documentation
- Explicitly document manual intervention points as they represent elevated data quality and operational risk
- Ensure lineage documentation is version-controlled and updated in response to system changes, regulatory updates, or data quality incidents
- Consider lineage for both batch and real-time data flows
- Engage data owners in validating lineage accuracy; technology teams alone cannot confirm business rule correctness
- Highlight any "dark data" — data flows that exist but are not governed, monitored, or documented

## Validation Checklist

- [ ] All critical data elements identified and traced to authoritative sources
- [ ] Transformation logic documented in both business and technical terms
- [ ] Data quality controls mapped along the lineage path
- [ ] Multi-level data flow diagrams created (conceptual, logical, physical)
- [ ] BCBS 239 compliance gaps identified with remediation plans
- [ ] Manual intervention points flagged with compensating controls assessed
- [ ] Data owners and stewards confirmed and accountability documented
- [ ] Known limitations and risks disclosed transparently
- [ ] Documentation maintained under version control with update triggers defined
- [ ] Narrative is accessible to non-technical audiences including examiners
