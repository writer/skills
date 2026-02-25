---
name: operational-resilience-planning
description: Conduct operational resilience planning and assessment for financial institutions. Use when defining important business services, setting impact tolerances, mapping critical resources, conducting scenario testing, or aligning with Basel Committee BCBS 548, OCC Heightened Standards, and FFIEC guidance on operational resilience.

metadata:
  display_name: "Operational Resilience Planning"
  short_description: "Plan operational resilience for financial institutions"
  default_prompt: "Optimize my operational resilience and suggest the best next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Operational Resilience Planning

## Overview

Plan and assess operational resilience for financial institutions by defining important business services, establishing impact tolerances, mapping interconnections and critical resources, and designing scenario testing programs. This skill applies the Basel Committee's Principles for Operational Resilience (BCBS 548), OCC Heightened Standards (12 CFR 30 Appendix D), FFIEC guidance, and NIST Cybersecurity Framework to ensure the institution can absorb, adapt to, and recover from disruptions.

## When to Use

- Establishing or maturing an operational resilience program
- Defining important business services and setting impact tolerances
- Mapping critical resources and interdependencies for important business services
- Designing and executing severe but plausible disruption scenarios
- Assessing the institution's ability to remain within impact tolerances
- Responding to regulatory expectations or examination findings on operational resilience

## Required Inputs

- **Business service inventory**: Customer-facing and internal services, descriptions, stakeholder mapping
- **Risk appetite framework**: Board-approved risk appetite statements, tolerance thresholds
- **Technology architecture**: System dependencies, infrastructure topology, cloud service mapping
- **Third-party relationships**: Critical vendor dependencies, fourth-party exposures
- **BCP/DR documentation**: Existing continuity plans, IT DR plans, RTO/RPO definitions
- **Incident history**: Prior disruption events, near-misses, lessons learned

## Methodology

### Step 1: Important Business Service Identification

Identify important business services (IBS) per BCBS 548 Principle 1 — services where disruption could pose a risk to financial stability, threaten safety and soundness, or cause customer harm.

Assess against: customer impact (number affected, segment vulnerability, alternatives), financial impact (revenue, penalties, capital, liquidity), regulatory impact (reporting obligations, systemic importance), market impact (payments, clearing, settlement roles), and reputational impact (media, trust, competitive positioning).

Categorize: **Critical** (disruption threatens viability), **Important** (significant impact, rapid restoration needed), **Standard** (manageable, extended recovery acceptable).

### Step 2: Impact Tolerance Setting

Establish impact tolerances per BCBS 548 Principle 3, measuring maximum tolerable disruption in: duration, data integrity loss, customer impact scope, financial loss, and regulatory compliance gaps.

Engage business leaders, risk management, and board committees in calibration. Set tolerances reflecting board risk appetite — not current capabilities. Document rationale including assumptions. Review annually or following significant operational changes.

### Step 3: Resource and Dependency Mapping

Map critical resources per BCBS 548 Principle 4 across: People (key roles, geographic distribution, succession, minimum staffing), Technology (applications, infrastructure, cloud, network), Data (stores, flows, backup, replication), Facilities (locations, alternatives), Third parties (vendor dependencies, substitutability), Financial resources (liquidity, insurance, capital reserves).

Produce dependency maps showing system-to-system dependencies, third-party single points of failure, geographic concentration risks, temporal dependencies, and cross-service data flows.

### Step 4: Vulnerability and Threat Assessment

Identify vulnerabilities across: technology failures (hardware, software, cloud, capacity), cyber threats (ransomware, DDoS, supply chain, insider — per NIST CSF), third-party failures (insolvency, degradation, fourth-party cascading), people risks (key-person, pandemic, labor), physical threats (disaster, utility, geographic concentration), and process failures (errors, failed changes, data corruption).

For each vulnerability: assess likelihood, impact on each IBS referencing tolerances, existing controls and effectiveness, and residual risk.

### Step 5: Scenario Design and Testing

Design severe but plausible scenarios per BCBS 548 Principle 6. Scenarios should test tolerance adherence, affect multiple services simultaneously, differ from historical incidents, and incorporate evolving threats.

| Category | Example Scenario |
|----------|-----------------|
| Technology | Complete data center loss with cloud region failure |
| Cyber | Ransomware with backup compromise |
| Third-party | Simultaneous failure of two critical vendors during peak |
| People | 40% workforce unavailability during month-end |
| Multi-factor | Cyberattack during severe weather with vendor disruption |

Testing methods (progressive maturity): tabletop exercises, walkthrough testing, simulation, live failover, unannounced testing.

### Step 6: Gap Analysis and Remediation Planning

For each IBS, determine if current capabilities meet impact tolerances. Identify gaps by category (technology, process, people, third-party, governance). Prioritize by tolerance breach magnitude, disruption likelihood, and regulatory urgency. Develop remediation plans with milestones and investment needs. Distinguish tactical quick wins from strategic investments.

### Step 7: Governance, Reporting, and Continuous Improvement

Align governance with OCC Heightened Standards and BCBS 548 Principle 7: board reviews IBS designations and tolerances annually, named executives accountable per IBS, Three Lines of Defense model applied (first line owns execution, second line provides oversight, third line audits), quarterly dashboards to management, semi-annual board reporting, and continuous improvement through incident and testing lessons learned.

## Output Specification

```markdown
# Operational Resilience Assessment

## Executive Summary
[Resilience maturity, key gaps, priorities]

## Important Business Services
| Service | Criticality | Impact Tolerance | Current Capability | Gap |

## Vulnerability Assessment
| Threat | Affected Services | Likelihood | Impact | Residual Risk |

## Scenario Testing Results
| Scenario | Services Tested | Within Tolerance? | Key Findings | Actions |

## Gap Analysis and Remediation Roadmap
| Gap | Affected Service | Priority | Remediation | Owner | Timeline | Investment |

## Regulatory Alignment
| Framework (BCBS 548 / OCC / FFIEC) | Requirement | Status | Evidence |
```

## Analysis Framework

| Level | Description |
|-------|-------------|
| 1 — Foundational | BCP/DR exists but resilience not formalized; no IBS defined |
| 2 — Developing | IBS identified, tolerances being established, initial mapping |
| 3 — Established | Tolerances set, mapping complete, scenario testing initiated |
| 4 — Advanced | Regular testing, gap remediation active, governance embedded |
| 5 — Leading | Continuous monitoring, adaptive response, proactive anticipation |

## Examples

**Example 1 — Impact Tolerance Gap**:
"The Consumer Payments Service (IBS-003) has a board-approved 4-hour maximum disruption tolerance. DR testing demonstrates a 12-hour recovery plus 2-hour reconciliation — a 10-hour gap exceeding tolerance by 250%. Recommend: (1) active-active architecture for payments (12-month, $4.2M), (2) interim manual procedures to reduce customer impact, (3) report tolerance breach to Board Risk Committee."

**Example 2 — Third-Party Dependency**:
"The Wholesale Lending Service (IBS-007) relies on a single credit bureau (Vendor X) with no failover. Vendor X had three outages in 12 months (avg 6 hours), exceeding the 2-hour tolerance. Recommend: (1) secondary credit bureau within 90 days, (2) cached data fallback for low-risk decisioning, (3) include Vendor X outage in next tabletop exercise."

## Guidelines

- Operational resilience focuses on outcomes (impact tolerances), not inputs (recovery plans)
- Impact tolerances should reflect board risk appetite, not current capabilities
- Scenario testing should challenge assumptions and test adaptability
- Consider cascading effects across interconnected services
- Engage all Three Lines of Defense in resilience governance
- Integrate with strategic planning, technology investment, and third-party risk management

## Validation Checklist

- [ ] Important business services identified and approved by senior management
- [ ] Impact tolerances set and approved by the board
- [ ] Resource and dependency mapping completed with single points of failure identified
- [ ] Severe but plausible scenarios designed and testing program established
- [ ] Gaps between tolerances and capabilities quantified
- [ ] Remediation roadmap prioritized with investment requirements
- [ ] Governance aligned with Three Lines of Defense and OCC Heightened Standards
- [ ] Regulatory alignment assessed against BCBS 548, OCC, and FFIEC
- [ ] Continuous improvement process established
