---
name: data-sharing-risk-review
description: Review and assess risks of data sharing arrangements between CPG brands and retail partners, including POS data, shopper data, clean room partnerships, and joint analytics. Use when evaluating retailer data agreements, assessing privacy risks (CCPA/GDPR), reviewing data clean room proposals, or auditing existing data sharing practices.

metadata:
  display_name: "Data Sharing Risk Review"
  short_description: "Review CPG-retailer data sharing privacy and compliance risks"
  default_prompt: "Check my data sharing risk for gaps risks and required fixes"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Data Sharing Risk Review

## Overview

Evaluate the risks inherent in CPG-retailer data sharing arrangements across legal, privacy, competitive, and operational dimensions. This skill assesses data flow architectures, privacy compliance requirements, competitive exposure risks, and contractual protections to produce a risk-rated assessment with specific mitigation recommendations.

## When to Use

- Evaluating a new retailer data sharing agreement or partnership proposal
- Reviewing data clean room arrangements (e.g., Walmart Luminate, Kroger 84.51°, Amazon Marketing Cloud)
- Assessing CCPA, CPRA, or GDPR compliance of data sharing practices
- Auditing existing data sharing arrangements for risk exposure
- Negotiating data clauses in JBP or trade agreements
- Evaluating third-party data partnerships (syndicated data, panel data)
- Due diligence on data practices during M&A

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Data sharing arrangement | Description of proposed or existing data exchange | Agreement summary or proposal |
| Data types involved | POS, loyalty, shopper-level, demographic, purchase history | Data dictionary or description |
| Data flow direction | One-way, two-way, or mutual exchange | Flow diagram or description |
| Partner identity | Retailer, data broker, technology provider | Partner profile |
| Geographic scope | US, EU, global | Market list |
| Technical architecture | API, flat file, clean room, direct access | Technical description |
| Existing agreements | Current data sharing contracts and terms | Contract excerpts |
| Purpose/use cases | How the data will be used by each party | Use case documentation |

## Methodology

### Step 1: Data Classification and Sensitivity Assessment

Classify all data elements in the sharing arrangement:

| Sensitivity Tier | Data Types | Risk Level | Handling Requirements |
|-----------------|-----------|-----------|---------------------|
| Tier 1: Restricted | Individual-level PII (name, email, device ID) | Critical | Explicit consent, encryption, strict access controls |
| Tier 2: Confidential | Pseudonymized shopper data, purchase history | High | Legitimate purpose, de-identification standards |
| Tier 3: Internal | Aggregated POS data, category-level analytics | Medium | Contractual protections, use restrictions |
| Tier 4: General | Published market data, syndicated reports | Low | Standard business terms |

**Data Element Inventory:**
For each data element shared, document:
- Field name and description
- Sensitivity tier
- Direction of flow (inbound, outbound, bidirectional)
- Granularity (individual, household, store, market, national)
- Frequency of sharing
- Retention period

### Step 2: Privacy Regulatory Compliance Assessment

**CCPA/CPRA (California):**
| Requirement | Assessment | Status |
|-------------|-----------|--------|
| Is personal information being "sold" or "shared" under CCPA definition? | Selling = exchange for monetary/valuable consideration; Sharing = cross-context behavioral advertising | ✓/✗ |
| Opt-out mechanism provided (Do Not Sell/Share)? | Required if data qualifies as sale/share | ✓/✗ |
| Service provider vs third party classification? | Service provider has limited use; third party triggers additional obligations | ✓/✗ |
| Data Processing Agreement (DPA) in place? | Required for service provider classification | ✓/✗ |
| Right to delete honored in shared data? | Must cascade deletion to data recipients | ✓/✗ |
| Privacy notice updated to disclose sharing? | Must list categories of PI shared and purposes | ✓/✗ |

**GDPR (if EU data involved):**
| Requirement | Assessment | Status |
|-------------|-----------|--------|
| Lawful basis identified (Art. 6)? | Consent, legitimate interest, contractual necessity | ✓/✗ |
| Joint controller or controller-processor relationship? | Determines responsibility allocation | ✓/✗ |
| Data Protection Impact Assessment (DPIA) conducted? | Required for high-risk processing | ✓/✗ |
| Data transfer mechanism (if cross-border)? | SCCs, adequacy decision, or BCRs | ✓/✗ |
| Data subject rights mechanisms? | Access, deletion, portability, objection | ✓/✗ |

**State Privacy Laws (Emerging):**
Check applicability of: Colorado Privacy Act, Virginia CDPA, Connecticut Data Privacy Act, and other state-specific requirements based on data subjects' locations.

### Step 3: Competitive Risk Assessment

Evaluate competitive exposure created by data sharing:

| Risk Area | Assessment Questions | Risk Rating |
|-----------|---------------------|-------------|
| Competitive intelligence leakage | Could the retailer share your data insights with competitors? | Critical/High/Med/Low |
| Benchmarking exposure | Can the retailer benchmark your performance against competitors? | Critical/High/Med/Low |
| Private label intelligence | Does shared data reveal innovation pipeline, pricing strategy, or margin structure? | Critical/High/Med/Low |
| Negotiation leverage shift | Does data access give the retailer disproportionate negotiation power? | Critical/High/Med/Low |
| Data aggregation risk | Combined with other manufacturers' data, does yours reveal market strategy? | Critical/High/Med/Low |

**Competitive Firewall Assessment:**
```
Questions to verify:
1. Does the agreement prohibit sharing your data with competing manufacturers?
2. Are there Chinese wall provisions between retailer's buying team and data analytics team?
3. Is your data used in aggregate (lower risk) or brand-specific (higher risk) analysis?
4. Can the retailer use insights derived from your data for private label development?
5. Is there a non-compete clause on data-derived insights?
```

### Step 4: Contractual Protection Review

Assess the legal protections in the data sharing agreement:

| Clause | What to Look For | Risk if Missing |
|--------|-----------------|----------------|
| Purpose limitation | Data used only for stated purposes | Data repurposed against your interests |
| Use restrictions | Prohibit sharing with third parties, competitors | Competitive exposure |
| Retention limits | Data deleted after agreed period | Indefinite retention of sensitive data |
| Audit rights | Right to audit partner's data practices | No visibility into compliance |
| Breach notification | Timely notification of data incidents | Unknown exposure after breach |
| Termination provisions | Data return/destruction upon termination | Post-termination data retention |
| IP and derived data | Who owns insights derived from shared data? | Loss of analytical IP |
| Indemnification | Liability for privacy violations | Financial exposure from partner's actions |
| Exclusivity restrictions | Required to share with specific partners only | Loss of negotiating flexibility |

### Step 5: Technical Architecture Risk Assessment

Evaluate the security of the data sharing mechanism:

| Architecture | Risk Profile | Mitigation |
|-------------|-------------|-----------|
| Flat file transfer (FTP/SFTP) | High — data at rest, in transit, broad access | Encryption, access controls, watermarking |
| API integration | Medium — controlled access but persistent connection | API key management, rate limiting, logging |
| Data clean room | Lower — no raw data leaves the environment | Verify differential privacy, output controls |
| Direct database access | Very High — broad query capability | Avoid; use API or clean room instead |
| Retailer portal access | Medium — controlled but retailer-managed | Least privilege, session monitoring |

**Data Clean Room Specific Assessment:**
```
1. Is differential privacy applied to query outputs?
2. Are minimum aggregation thresholds enforced (e.g., k-anonymity)?
3. Can query patterns reveal individual records even if outputs are aggregated?
4. Who controls the clean room environment — neutral third party?
5. Are query logs available for audit?
6. Can you control which queries are permitted against your data?
```

### Step 6: Risk Scoring and Prioritization

Compile a composite risk assessment:

```
Risk Score Calculation:
  Privacy Risk (0-25):     Tier classification × regulatory exposure × data volume
  Competitive Risk (0-25): Intelligence exposure × firewall adequacy × partner intent
  Contractual Risk (0-25): Missing clauses × enforceability × partnership maturity
  Technical Risk (0-25):   Architecture vulnerability × security controls × breach probability

Composite Risk Score (0-100):
  0-25:  Low Risk — proceed with standard monitoring
  26-50: Moderate Risk — proceed with enhanced protections
  51-75: High Risk — proceed only with significant mitigations
  76-100: Critical Risk — do not proceed without fundamental restructuring
```

## Output Specification

```markdown
# Data Sharing Risk Review — [Partnership/Arrangement Name]

## Executive Summary
**Overall Risk Rating**: [Critical / High / Moderate / Low]
**Composite Score**: [X/100]
**Recommendation**: [Proceed / Proceed with Conditions / Restructure / Do Not Proceed]

## Data Flow Summary
[Description of what data flows, in which direction, at what granularity]

## Risk Assessment

### Privacy & Regulatory Risk: [X/25]
[CCPA/GDPR compliance findings with specific gaps identified]

### Competitive Risk: [X/25]
[Competitive exposure assessment with firewall evaluation]

### Contractual Risk: [X/25]
[Missing or inadequate clauses with specific remediation]

### Technical Risk: [X/25]
[Architecture vulnerabilities and security assessment]

## Critical Findings
| # | Finding | Risk | Regulation/Standard | Remediation |
|---|---------|------|-------------------|-------------|
| 1 | [Finding] | Critical/High | [Reference] | [Action] |

## Required Mitigations (Before Proceeding)
1. [Mitigation with owner and timeline]
2. [Mitigation with owner and timeline]

## Recommended Contract Modifications
[Specific clause language recommendations]

## Monitoring Plan
[Ongoing monitoring cadence, audit rights exercise schedule, compliance reviews]
```

## Analysis Framework

**Data Sharing Decision Matrix:**
| Data Sensitivity | High Partner Trust | Low Partner Trust |
|-----------------|-------------------|------------------|
| Tier 1 (PII) | Proceed with full protections | Do Not Share |
| Tier 2 (Pseudonymized) | Proceed with clean room | Proceed with aggregation only |
| Tier 3 (Aggregated) | Proceed with standard terms | Proceed with use restrictions |
| Tier 4 (Public) | Proceed | Proceed |

## Example

**Input**: "Retailer X proposes accessing our shopper-level purchase data from their loyalty program for joint analytics. They want to combine it with our CRM data in their analytics platform to build co-branded audience segments for media targeting."

**Analysis excerpt**:
> "**Composite Risk Score: 68/100 — HIGH.** This arrangement involves bidirectional sharing of Tier 1 (PII from CRM) and Tier 2 (pseudonymized loyalty data) in the retailer's owned environment, creating significant privacy and competitive exposure. **Privacy risk (20/25)**: Combining CRM data with loyalty purchase history likely constitutes 'sharing' under CCPA for cross-context behavioral advertising, triggering opt-out rights and GPC signal compliance. No evidence of a DPIA despite high-risk profiling activity under GDPR (if EU consumers included). **Competitive risk (18/25)**: Retailer's analytics platform lacks demonstrated Chinese wall between the analytics team and buying team, creating a vector for margin and pricing intelligence leakage to the private label team. **Recommendation**: Restructure to a neutral data clean room with (1) differential privacy thresholds, (2) query-level access controls, (3) contractual prohibition on private label use, and (4) CCPA opt-out mechanism integration before proceeding."

## Guidelines

- Always classify data before assessing risk — sensitivity tier determines the entire framework
- "Anonymized" data is rarely truly anonymous — assess re-identification risk
- Clean rooms reduce but do not eliminate risk — evaluate their specific controls
- Competitive risk is often underweighted — a retailer is both a customer and a potential competitor
- Contractual protections are only as good as their enforceability and your ability to audit
- Privacy regulations are evolving rapidly — check for new state laws quarterly
- This review assesses risk, not legal compliance — recommend privacy counsel for Critical findings

## Validation Checklist

- [ ] All data elements inventoried with sensitivity classification
- [ ] CCPA/CPRA compliance assessed (sale/share, opt-out, DPA, deletion)
- [ ] GDPR compliance assessed if EU data involved (basis, DPIA, transfers)
- [ ] Competitive risk assessed across 5 dimensions
- [ ] Competitive firewall evaluated with specific questions answered
- [ ] Contractual protections reviewed against 9 key clauses
- [ ] Technical architecture risk assessed with security controls evaluated
- [ ] Clean room specific assessment completed (if applicable)
- [ ] Composite risk score calculated (0-100)
- [ ] Critical findings listed with specific remediation actions
- [ ] Monitoring plan established with audit cadence
