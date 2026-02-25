---
name: hipaa-risk-review
description: Identify and assess privacy and security risks under HIPAA Privacy Rule (45 CFR 160/164 Subpart E), Security Rule (45 CFR 164 Subpart C), and Breach Notification Rule by conducting systematic risk analyses of PHI handling practices, technical safeguards, and administrative controls. Use when performing HIPAA risk assessments, preparing for OCR audits, investigating potential breaches, evaluating new system implementations, or remediating compliance gaps.

metadata:
  display_name: "Hipaa Risk Review"
  short_description: "Assess HIPAA privacy and security compliance risks"
  default_prompt: "Check my hipaa risk for gaps risks and required fixes"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# HIPAA Risk Review

## Overview

Conduct systematic risk analysis of protected health information (PHI) handling practices across administrative, physical, and technical safeguard domains as required by the HIPAA Security Rule (45 CFR 164.308(a)(1)(ii)(A)). The Security Rule requires covered entities and business associates to conduct an accurate and thorough assessment of potential risks and vulnerabilities to the confidentiality, integrity, and availability of ePHI. This skill evaluates current controls against HIPAA requirements, identifies gaps, quantifies risk levels, and produces remediation plans aligned with OCR enforcement priorities and the NIST Cybersecurity Framework for healthcare.

## When to Use

- Conducting the required annual HIPAA Security Rule risk analysis
- Preparing for OCR (Office for Civil Rights) audit or investigation
- Evaluating HIPAA compliance of a new system, application, or workflow
- Investigating a potential breach or privacy incident
- Assessing business associate compliance and BAA adequacy
- Remediating findings from a previous audit or risk assessment
- Onboarding new workforce members who handle PHI
- Evaluating telehealth, mobile health, or cloud platform HIPAA compliance

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `phi_inventory` | Systems, applications, and locations where PHI is created, stored, transmitted, or disposed | Structured inventory |
| `current_controls` | Existing administrative, physical, and technical safeguards | Structured object |
| `policies_procedures` | HIPAA policies and procedures documentation | Document references |
| `workforce_data` | Workforce roles, access levels, and training completion | Structured object |
| `incident_history` | Prior privacy/security incidents and breach reports | Array of records |
| `business_associates` | BA list with BAA status and compliance assessment dates | Structured array |
| `technical_environment` | Network architecture, encryption status, access control systems | Structured object |

## Methodology

### Step 1: PHI Asset Inventory and Data Flow Mapping

Identify all PHI touchpoints across the organization:

- **Electronic PHI (ePHI)**: EHR systems, billing platforms, patient portals, email, cloud storage, mobile devices, medical devices
- **Paper PHI**: Medical records, printed reports, faxes, prescription pads, sign-in sheets
- **Oral PHI**: Provider-patient conversations, phone calls, voicemails, dictation
- **PHI in transit**: HL7/FHIR interfaces, claims transmissions, referral communications, telehealth sessions

**Data Flow Mapping:**
- Document how PHI enters the organization (patient intake, referrals, HIE)
- Track PHI movement between systems (EHR → billing → clearinghouse → payer)
- Identify PHI exit points (patient portal, discharge documents, external referrals)
- Map PHI disposal processes (secure shredding, media sanitization, record retention)

### Step 2: Threat and Vulnerability Identification

Identify threats to PHI confidentiality, integrity, and availability:

**Threat Categories:**

| Category | Examples | Likelihood Assessment |
|----------|----------|----------------------|
| External attacks | Ransomware, phishing, hacking, social engineering | Based on industry threat intelligence |
| Internal threats | Unauthorized access, snooping, insider theft | Based on workforce size and access controls |
| Environmental | Natural disaster, power failure, hardware failure | Based on geographic and infrastructure risk |
| Human error | Misdirected email/fax, lost devices, improper disposal | Based on incident history and training levels |
| Business associate | BA breach, unauthorized use, inadequate safeguards | Based on BA risk assessments |

**Vulnerability Assessment Areas:**
- Unencrypted ePHI at rest or in transit
- Weak or shared authentication credentials
- Insufficient access controls (excessive access rights)
- Inadequate audit logging or log review
- Missing or outdated patches and security updates
- Lack of workforce HIPAA training
- Absent or incomplete business associate agreements
- Inadequate physical security for PHI locations
- No or insufficient backup and disaster recovery

### Step 3: Control Assessment Against HIPAA Requirements

Evaluate existing controls against the Security Rule specification:

**Administrative Safeguards (45 CFR 164.308):**

| Standard | Key Requirements | Assessment |
|----------|-----------------|------------|
| Risk Analysis (a)(1)(ii)(A) | Accurate, thorough risk assessment | Current/outdated/absent |
| Risk Management (a)(1)(ii)(B) | Implement measures to reduce risk | Documented plan with progress |
| Workforce Security (a)(3) | Authorization and supervision | Role-based access, termination procedures |
| Information Access (a)(4) | Access authorization policies | Minimum necessary implemented |
| Security Awareness (a)(5) | Training program | Annual training, phishing tests |
| Incident Procedures (a)(6) | Incident response plan | Documented, tested, exercised |
| Contingency Plan (a)(7) | Backup, recovery, emergency mode | Tested within 12 months |
| Evaluation (a)(8) | Periodic compliance evaluation | Scheduled and documented |
| BAA Management (b)(1) | Business associate agreements | Current for all BAs |

**Physical Safeguards (45 CFR 164.310):**

| Standard | Key Requirements | Assessment |
|----------|-----------------|------------|
| Facility Access (a) | Access controls, visitor logs, restricted areas | Implemented/gaps |
| Workstation Use (b) | Policies for workstation use and positioning | Documented/enforced |
| Workstation Security (c) | Physical safeguards for workstations | Screen locks, privacy screens |
| Device and Media (d) | Disposal, re-use, media tracking | Documented procedures, certificates |

**Technical Safeguards (45 CFR 164.312):**

| Standard | Key Requirements | Assessment |
|----------|-----------------|------------|
| Access Control (a) | Unique user ID, emergency access, auto-logoff, encryption | Implemented per standard |
| Audit Controls (b) | Record and examine system activity | Logging enabled, reviewed |
| Integrity (c) | Protect ePHI from improper alteration | Integrity controls in place |
| Authentication (d) | Verify person or entity identity | MFA implemented where appropriate |
| Transmission Security (e) | Encryption for ePHI in transit | TLS 1.2+, encrypted email |

### Step 4: Risk Scoring and Prioritization

Score each identified risk using likelihood and impact assessment:

**Likelihood Scale:**
- 1 (Very Low): Unlikely to occur given current controls
- 2 (Low): Could occur but controls significantly mitigate
- 3 (Medium): Reasonably likely to occur
- 4 (High): Likely to occur within the assessment period
- 5 (Very High): Expected to occur or has recently occurred

**Impact Scale:**
- 1 (Negligible): Minimal impact, no PHI exposure
- 2 (Low): Limited PHI exposure, few individuals affected
- 3 (Medium): Moderate PHI exposure, potential OCR interest
- 4 (High): Significant PHI exposure, likely reportable breach
- 5 (Critical): Large-scale breach, substantial harm, regulatory action expected

**Risk Score:** Likelihood × Impact (1-25 scale)

| Risk Level | Score | Action Required |
|------------|-------|-----------------|
| Critical | 20-25 | Immediate remediation required |
| High | 12-19 | Remediation within 30 days |
| Medium | 6-11 | Remediation within 90 days |
| Low | 2-5 | Address in next review cycle |
| Minimal | 1 | Accept risk with documentation |

### Step 5: Breach Risk Assessment

For identified vulnerabilities, assess breach notification implications:

- **Does the scenario involve unsecured PHI?** (not encrypted per NIST guidelines)
- **Does the HIPAA Breach Notification Rule apply?** (45 CFR 164.402-414)
- **Apply the four-factor breach risk assessment:**
  1. Nature and extent of PHI involved (types and identifiers)
  2. Unauthorized person who used or received the PHI
  3. Whether PHI was actually acquired or viewed
  4. Extent to which risk has been mitigated
- **Notification requirements**: Individual (without unreasonable delay, within 60 days), HHS (annually if under 500; within 60 days if 500+), media (if 500+ in a jurisdiction)

### Step 6: Remediation Planning

Develop prioritized remediation plans for identified risks:

- **Immediate actions**: Address critical and high risks within defined timeframes
- **Policy updates**: Revise policies and procedures to address gaps
- **Technical controls**: Implement encryption, access controls, audit logging
- **Training**: Targeted workforce education on identified vulnerabilities
- **Vendor management**: Update BAAs, request BA compliance attestations
- **Documentation**: Ensure all risk decisions are documented (including accepted risks)

### Step 7: Ongoing Monitoring Framework

Establish continuous compliance monitoring:

- Quarterly access reviews and audit log analysis
- Annual comprehensive risk analysis update
- Continuous vulnerability scanning for ePHI systems
- Monthly review of security incident trends
- Bi-annual workforce training assessments
- Annual BA compliance review cycle
- Tracking of OCR enforcement actions and guidance updates

## Output Specification

```yaml
hipaa_risk_review:
  assessment_date: string
  scope: string
  assessor: string
  phi_inventory_summary:
    total_systems: number
    ephi_systems: number
    ba_count: number
  risk_summary:
    total_risks_identified: number
    critical: number
    high: number
    medium: number
    low: number
  findings:
    - finding_id: string
      category: string  # administrative, physical, technical
      hipaa_reference: string  # 45 CFR citation
      description: string
      current_controls: string
      gap: string
      likelihood: number
      impact: number
      risk_score: number
      risk_level: string
      remediation:
        action: string
        responsible_party: string
        deadline: string
        estimated_cost: string
  breach_risk_scenarios: array
  remediation_plan_summary:
    total_actions: number
    estimated_timeline: string
    estimated_budget: string
  next_review_date: string
```

## Analysis Framework

### OCR Enforcement Priority Areas

Focus assessment on areas most frequently cited in OCR enforcement actions:

| Priority Area | OCR Finding Frequency | HIPAA Reference |
|--------------|----------------------|-----------------|
| Risk analysis not conducted | Very High | 164.308(a)(1)(ii)(A) |
| Insufficient access controls | High | 164.312(a) |
| Lack of encryption | High | 164.312(a)(2)(iv) |
| Missing BAAs | High | 164.502(e) |
| Inadequate audit controls | Medium | 164.312(b) |
| Insufficient training | Medium | 164.308(a)(5) |
| No contingency plan | Medium | 164.308(a)(7) |

## Examples

**Example: Mid-Size Clinic HIPAA Risk Assessment**

- Scope: 15-provider multispecialty clinic, cloud-based EHR, 3 physical locations
- PHI systems identified: 12 (EHR, billing, patient portal, fax server, email, 7 ancillary systems)
- Critical finding: Legacy fax server stores PHI without encryption — risk score 20 (Critical)
- High finding: 3 business associates without current BAAs — risk score 16 (High)
- High finding: No multi-factor authentication on EHR remote access — risk score 15 (High)
- Medium finding: Audit log review not performed regularly — risk score 9 (Medium)
- Total risks: 23 identified (2 critical, 5 high, 9 medium, 7 low)
- Remediation plan: 90-day timeline, estimated budget $45,000 for encryption and MFA deployment
- Breach risk: Legacy fax server scenario would constitute reportable breach if compromised (unencrypted PHI)

## Guidelines

1. **Risk analysis is required, not optional** — OCR has issued more enforcement actions for missing risk analysis than any other HIPAA violation
2. **Document everything** — HIPAA requires documentation of risk analysis and management decisions
3. **Addressable does not mean optional** — addressable implementation specifications must be implemented or have documented alternative measures
4. **Include all ePHI** — risk analysis must cover all systems creating, receiving, maintaining, or transmitting ePHI
5. **Update annually at minimum** — risk analysis must be updated when significant changes occur and at least annually
6. **Involve leadership** — risk management decisions require senior management awareness and resource allocation
7. **This analysis is not legal advice** — always consult with qualified HIPAA legal counsel for compliance determinations

## Validation Checklist

- [ ] Complete PHI asset inventory covering all systems, locations, and formats
- [ ] Data flow mapping documents PHI creation, storage, transmission, and disposal
- [ ] Threats and vulnerabilities identified across administrative, physical, and technical domains
- [ ] Controls assessed against all Security Rule standards and implementation specifications
- [ ] Risk scores calculated using documented likelihood and impact methodology
- [ ] Breach notification risk assessed for high-risk scenarios
- [ ] Remediation plan prioritized with responsible parties and deadlines
- [ ] Accepted risks documented with business justification
- [ ] Ongoing monitoring framework established
- [ ] Assessment documented per 45 CFR 164.316 requirements

## HIPAA Compliance Notes

- This risk review itself constitutes the risk analysis required by 45 CFR 164.308(a)(1)(ii)(A)
- Documentation must be retained for 6 years per 45 CFR 164.316(b)(2)(i)
- Risk analysis findings may be subject to discovery in litigation — consult legal counsel on privilege protections
- Engagement of external assessors requires a BAA if they will access PHI during the assessment
- OCR has published guidance on risk analysis methodology (HHS.gov/hipaa) — align with official guidance
- State laws may impose additional privacy and security requirements beyond HIPAA (e.g., state breach notification laws with shorter timelines)
