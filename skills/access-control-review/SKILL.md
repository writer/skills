---
name: access-control-review
description: Review access control risks and segregation of duties in financial institutions. Use when evaluating user access provisioning, reviewing privileged access, assessing SoD conflicts, analyzing access certification results, or responding to FFIEC IT Examination Handbook and SOX control requirements related to logical access.

metadata:
  display_name: "Access Control Review"
  short_description: "Review access controls and segregation of duties for banks"
  default_prompt: "Check my access control for gaps risks and required fixes"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Access Control Review

## Overview

Evaluate access control risks including user access management, privileged access governance, segregation of duties (SoD) conflicts, and access certification effectiveness. This skill applies the FFIEC IT Examination Handbook (Information Security booklet), NIST Cybersecurity Framework (PR.AC), SOX Section 302/404 requirements for IT general controls, and COSO Principle 11 (general controls over technology) to assess the adequacy of logical access controls in financial institutions.

## When to Use

- Reviewing user access provisioning and de-provisioning processes
- Assessing privileged access management programs (PAM)
- Identifying and remediating segregation of duties conflicts
- Evaluating access certification/recertification campaigns
- Analyzing access-related audit findings or regulatory examination results
- Assessing access controls as IT general controls (ITGCs) supporting SOX-relevant applications

## Required Inputs

- **Access data**: User access listings, role assignments, entitlement details, privileged account inventories
- **SoD matrix**: Defined conflict rules, toxic combinations, mitigating controls
- **Application inventory**: In-scope applications, criticality classification, SOX relevance
- **Process documentation**: Access provisioning workflows, approval chains, certification procedures
- **Audit/exam findings**: Prior access-related findings, remediation status, MRA/MRIA tracking
- **Organizational data**: Org charts, job descriptions, reporting hierarchies, recent transfers/terminations

## Methodology

### Step 1: Access Governance Framework Assessment

Evaluate governance against FFIEC and NIST expectations: policy framework comprehensiveness, RBAC implementation with roles aligned to job functions, least privilege enforcement, application and data owner accountability, risk committee reporting, and alignment to NIST CSF PR.AC subcategories (PR.AC-1 through PR.AC-7).

### Step 2: Access Lifecycle Management Review

Assess the end-to-end access lifecycle:

**Provisioning**: Documented business justification, application/data owner approval, role-based grants (not ad-hoc), automated provisioning where feasible, and pre-grant SoD conflict checking.

**Modification**: Role changes trigger access reviews, accumulated access from prior roles reviewed and revoked (access creep prevention), temporary/emergency access has defined expiration.

**De-provisioning**: Termination triggers same-day revocation, HR system feeds drive automated de-provisioning, shared accounts transferred or disabled, contractor access revoked on engagement end.

Key KPIs: Provisioning ≤3 days, termination revocation same-day, orphan accounts 0%, transfer completion ≤5 days.

### Step 3: Privileged Access Management (PAM) Assessment

Evaluate per FFIEC and NIST SP 800-53 (AC-6): complete privileged account inventory and classification, documented justification and ownership, MFA and session recording requirements, activity logging with anomaly detection, quarterly review frequency, service account password rotation, and documented break-glass procedures with post-use review.

### Step 4: Segregation of Duties (SoD) Analysis

Define toxic combinations for key processes:

| Process | Conflicting Functions |
|---------|---------------------|
| Accounts Payable | Vendor master maintenance + Payment approval |
| General Ledger | Journal entry creation + Journal entry approval |
| Wire Transfers | Wire initiation + Wire release |
| Lending | Loan origination + Credit approval |
| User Administration | Access provisioning + Access approval |
| Treasury | Trade execution + Trade settlement + Trade recording |

Extract entitlements, map to SoD rules, identify cross-application conflicts, assess compensating controls, and quantify conflicts by severity (Critical=no controls, High=weak, Medium=adequate, Low=strong).

### Step 5: Access Certification Review

Evaluate certification effectiveness: scope covers all in-scope and SOX-relevant applications, frequency commensurate with risk (critical=quarterly, standard=semi-annual), certifiers are application/data owners, certifiers receive sufficient information (entitlements in business terms, last login dates), rubber-stamping indicators analyzed (100% approval, minimal review time), revocation follow-through confirmed, and results retained for audit.

### Step 6: SOX ITGC Access Control Assessment

Evaluate: all SOX-relevant applications in scope, separation of dev/test/production access, direct database access controls and monitoring, administrator OS access review, design adequacy testing, and operating effectiveness test results for provisioning, de-provisioning, and certification controls.

### Step 7: Findings, Risk Rating, and Recommendations

Classify findings by severity, map to regulatory requirements (FFIEC, NIST, SOX), provide actionable recommendations with effort estimates, distinguish quick wins from strategic improvements, and estimate residual risk from unmitigated gaps.

## Output Specification

```markdown
# Access Control Review Report

## Executive Summary
[Maturity assessment, key findings, critical recommendations]

## Access Governance Maturity
| Domain | Maturity (1-5) | Key Gaps |

## Detailed Findings
[Critical, High, Medium/Low findings with risk impact, regulatory reference, remediation]

## SoD Conflict Summary
| Process | Conflicts Identified | With Compensating Controls | Unmitigated |

## Privileged Access Summary
| Account Type | Count | Compliant | Non-Compliant | Key Issues |

## Access Certification Effectiveness
| Application | Certification Rate | Revocation Rate | Rubber-Stamp Indicators |

## Remediation Roadmap
| Finding | Priority | Remediation | Owner | Target Date | Effort |
```

## Analysis Framework

| Level | Description |
|-------|-------------|
| 1 — Initial | Ad-hoc access management, no formal processes, pervasive SoD conflicts |
| 2 — Developing | Basic provisioning/de-provisioning, partial RBAC |
| 3 — Defined | RBAC implemented, SoD rules defined, periodic certifications |
| 4 — Managed | Automated lifecycle, continuous SoD monitoring, PAM deployed |
| 5 — Optimized | Risk-adaptive controls, real-time analytics, zero-trust architecture |

## Examples

**Example 1 — SoD Conflict Finding**:
"Analysis of SAP entitlements identified 23 users in Finance with concurrent access to FB01 (Post Journal Entry), FB02 (Change Journal Entry), and FBRA (Reset Cleared Items) — allowing a single user to create, modify, and reverse journal entries without approval. 18 of 23 users have no compensating controls. This represents a significant deficiency in COSO Principle 10 and a SOX ITGC gap. Recommend: immediate remediation for unmitigated users, compensating detective controls (daily exception report reviewed by Controller) for those requiring dual access with documented justification."

**Example 2 — Privileged Access Finding**:
"The core banking platform (FIS Horizon) has 47 system admin accounts: 12 are shared/generic without individual accountability, and 3 belong to employees terminated 30-90 days ago. No session recording or just-in-time elevation is implemented. Recommend: (1) deactivate orphaned accounts immediately, (2) eliminate shared accounts within 60 days, (3) deploy PAM solution within 180 days."

## Guidelines

- Prioritize systems processing customer PII and financial data
- Consider cross-application SoD conflicts, not just within-application entitlements
- 100% SoD elimination may not be feasible; focus on adequate compensating controls
- Consider system integration and SSO impacts on access control boundaries
- Evaluate service account proliferation as a growing attack vector
- Document assessments for regulatory examination readiness

## Validation Checklist

- [ ] Access governance assessed against FFIEC and NIST requirements
- [ ] Full access lifecycle evaluated: provisioning, modification, de-provisioning
- [ ] Privileged account inventory complete with ownership and justification
- [ ] SoD analysis performed for all critical business processes
- [ ] Compensating controls assessed for effectiveness
- [ ] Certification effectiveness analyzed with rubber-stamping indicators
- [ ] SOX ITGC access controls assessed for design and operating effectiveness
- [ ] Findings mapped to regulatory requirements and COSO principles
- [ ] Remediation roadmap includes priorities, owners, timelines, and effort
