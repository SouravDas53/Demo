# SAST Process Document (Checkmarx)

---

# Document Control

| Field | Value |
|---|---|
| Document Title | Static Application Security Testing (SAST) Process Document |
| Tooling Reference | Checkmarx SAST |
| Prepared For | LIFESTANCE HEALTH |
| Prepared By | Lalit kumar |
| Classification | Confidential |
| Version | 1.0 |
| Date | Feb 2026 |
| Review Cycle | Quarterly |

---

# 1. Purpose

This document defines the operational process for performing Static Application Security Testing (SAST) using Checkmarx within a healthcare environment.

The objective is to identify code-level security weaknesses early in the software development lifecycle, reduce the chance of PHI/ePHI exposure, and support compliance-ready evidence collection for security and privacy oversight.

---

# 2. Scope

This process applies to:

- Web applications
- APIs and microservices
- Mobile applications
- Backend services
- Shared libraries
- Infrastructure-related code where applicable
- Third-party code included in source repositories

This process applies to:

- New applications
- Enhancements
- Emergency fixes
- High-risk production changes
- Periodic re-scans of existing applications

---

# 3. Control Context

Healthcare organizations need secure development controls that protect PHI/ePHI and support auditability. SAST is used to find code-level weaknesses before release, and it is typically paired with threat modeling, code review, and other verification practices.

This process is aligned to secure software development and security-assurance expectations that emphasize early verification, traceability, remediation discipline, and evidence retention.

---

# 4. Roles and Responsibilities

| Role | Responsibility |
|---|---|
| Application Owner | Owns business risk and release priority |
| Engineering Lead | Ensures fixes are implemented |
| Developers | Remediate findings and follow secure coding standards |
| AppSec Lead | Maintains SAST standards and triage guidance |
| DevSecOps | Integrates scans into CI/CD |
| Security Architect | Defines risk thresholds and design expectations |
| Compliance / Risk | Validates evidence and exception handling |
| QA / Test Team | Verifies security fixes in test environments |

---

# 5. SAST Operating Model

## 5.1 High-Level Flow

1. Application is onboarded into Checkmarx.
2. Repository and branch mapping are configured.
3. Scan profiles and policies are assigned.
4. Automated scans run on pull request, merge, or scheduled basis.
5. Findings are triaged by severity and exploitability.
6. Developers remediate confirmed issues.
7. Security validates re-scan results.
8. Release gates are approved or blocked.
9. Evidence is retained for audit and compliance.

## 5.2 Process Entry Criteria

A codebase is eligible for SAST when:

- Source repository is accessible
- Build ownership is established
- Application criticality is defined
- Data classification is completed
- Scan policy is approved
- Exception process is defined

---

# 6. Technical Onboarding Requirements

## 6.1 Repository Information

| Attribute | Example Data |
|---|---|
| Application Name | Patient Portal |
| Repository URL | Git-based source repository |
| Branches In Scope | main, release/*, hotfix/* |
| Language Stack | Java, JavaScript, Python, C# |
| Hosting Model | Cloud / on-prem / hybrid |
| Data Sensitivity | PHI / ePHI |
| App Criticality | High |

## 6.2 Scan Configuration Inputs

Typical configuration fields to define during onboarding:

- Application name
- Business unit
- System owner
- Repository path
- Scan frequency
- Branch trigger rules
- Severity thresholds
- Policy profile
- Email / ticket routing
- Exception approver
- Evidence retention location

---

# 7. Checkmarx Scan Setup Standards

## 7.1 Recommended Baseline Setup

- Enable full repository scanning for initial baseline
- Enable incremental scans for pull requests or changed files
- Run scheduled full scans on a defined cadence
- Store scan configuration as code where possible
- Restrict scan policy changes to AppSec or platform administrators
- Route findings to the correct product team automatically

## 7.2 Scan Cadence

| Event | Required Action |
|---|---|
| Pull request | Incremental SAST scan |
| Merge to main branch | Policy-based SAST scan |
| Release candidate | Full scan and triage |
| Monthly / quarterly | Re-baseline scan |
| Post-remediation | Validation scan |
| High-risk change | Immediate ad hoc scan |

---

# 8. Severity and Risk Triage

## 8.1 Triage Principles

Each finding should be reviewed for:

- True positive vs false positive
- Reachability
- Data sensitivity
- Exposure path
- Business criticality
- Compensating controls
- Remediation effort

## 8.2 Severity Model

| Severity | Interpretation | Example Action |
|---|---|---|
| Critical | Likely exploitable with major impact | Block release |
| High | Serious weakness with meaningful risk | Remediate before release or formally accept risk |
| Medium | Important issue requiring planned fix | Remediate in sprint backlog |
| Low | Limited security impact | Track for remediation or accept per policy |
|
| Informational | Advisory only | Review and document |

## 8.3 Triage Ownership

- Developers confirm code context
- AppSec validates security relevance
- Security Architect resolves disputed findings
- Risk Owner approves exceptions where needed

---

# 9. Healthcare-Specific Technical Focus Areas

The SAST process should pay special attention to code that handles:

- Patient registration and identity data
- Clinical records
- Billing and claims data
- Prescriptions and treatment data
- API tokens and service credentials
- Encryption and key handling
- Session management
- File uploads and downloads
- Audit logging and consent records
- Report generation and exports

## 9.1 Priority Vulnerability Classes

- Injection flaws
- Broken access control
- Authentication bypass
- Hardcoded secrets
- Unsafe deserialization
- Sensitive data exposure
- Insecure crypto usage
- Path traversal
- SSRF-style issues
- Weak input validation

---

# 10. Development Lifecycle Integration

## 10.1 Pull Request Workflow

1. Developer creates branch
2. Code is committed with secure coding checks
3. Pull request is opened
4. Automated SAST scan runs
5. Findings are reviewed
6. Merge is blocked if policy threshold is exceeded
7. Developer remediates issues
8. Re-scan validates fix
9. PR is merged after approval

## 10.2 Release Workflow

1. Release candidate is tagged
2. Full SAST scan is executed
3. Scan results are reviewed by AppSec
4. Blockers are resolved or accepted via exception
5. Evidence is attached to the release record
6. Production deployment is approved

---

# 11. Policy Thresholds

## 11.1 Example Release Gate Policy

| Condition | Decision |
|---|---|
| Critical finding present | Block |
| High findings above threshold | Block |
| Open findings without owner | Block |
| Stale scan older than policy window | Block |
| Exception approved with expiry | Allow with risk acceptance |
| No findings above threshold | Allow |

## 11.2 Sample Thresholds

| Metric | Default Value |
|---|---|
| Critical findings allowed in release | 0 |
| High findings allowed in release | 0 unless risk accepted |
| Maximum scan age for release | 30 days |
| Maximum exception duration | 90 days |
| Re-test SLA after remediation | 5 business days |

---

# 12. Remediation Workflow

## 12.1 Standard Remediation Steps

1. Confirm finding validity
2. Assign issue to owner
3. Determine fix approach
4. Code remediation
5. Peer review of fix
6. Re-run SAST scan
7. Validate closure
8. Update tracking ticket
9. Retain evidence

## 12.2 Ticket Fields

Each issue ticket should include:

- Application name
- Repository name
- Scan ID
- Rule / query identifier
- Severity
- File path
- Line number
- Business impact
- Owner
- Due date
- Status
- Exception reference if applicable

---

# 13. Technical Data Fields for the Report

The following technical data should appear in the SAST report or dashboard:

- Total applications onboarded
- Scan success rate
- Number of findings by severity
- Open findings aging
- Mean time to remediate
- False-positive rate
- Reopened issue rate
- Release blocks triggered
- Exception count and expiry dates
- Scan coverage by repository and branch

## 13.1 Sample Dashboard View

| Metric | Example Value |
|---|---|
| Applications onboarded | 42 |
| Active repositories | 58 |
| Critical findings open | 3 |
| High findings open | 19 |
| Medium findings open | 74 |
| Mean time to remediate high findings | 8 days |
| PR scan coverage | 93% |
| Re-test completion rate | 96% |

---

+--------------------------------------------------+
| SECURITY POSTURE DASHBOARD                       |
+--------------------------------------------------+

[42]
Applications Onboarded

[58]
Active Repositories

[3]     [19]      [74]
Critical High      Medium

PR Scan Coverage
███████████████████ 93%

Re-Test Completion
████████████████████ 96%

---

# 14. Evidence and Audit Requirements

The following artifacts should be retained:

- Scan configuration approval
- Initial baseline scan report
- Triage notes
- False-positive justification where applicable
- Remediation ticket history
- Re-scan evidence
- Release approval record
- Exception approval record
- Metrics dashboard export

## 14.1 Evidence Retention Rules

- Store evidence in the approved compliance repository
- Retain according to policy and regulatory requirements
- Make evidence searchable by application, release, and date
- Preserve the full chain from finding to closure

---

# 15. Exception Management

Exceptions should be used only when remediation is not immediately feasible.

## Required Fields

- Reason for exception
- Business justification
- Risk owner
- Compensating controls
- Expiry date
- Revalidation date
- Approval signature

## Exception Conditions

- No open Critical findings should be excepted without executive approval
- High-risk exceptions require documented compensating controls
- All exceptions must expire and be reviewed

---

# 16. Example SAST Control Checklist

| Control | Status |
|---|---|
| Repository onboarded | Yes / No |
| Scan profile approved | Yes / No |
| Branch scanning enabled | Yes / No |
| PR scan enabled | Yes / No |
| Severity thresholds defined | Yes / No |
| Triage owner assigned | Yes / No |
| Release gate enforced | Yes / No |
| Re-scan validation required | Yes / No |
| Evidence retained | Yes / No |
| Exception workflow active | Yes / No |

---

# 17. Suggested Report Language for Leadership

The organization should adopt SAST as a mandatory preventive control for all in-scope healthcare applications. Checkmarx should be used to identify security weaknesses early, prioritize remediation based on business risk, and provide release evidence for compliance and audit purposes.

The program should be measured not only by scan volume, but by reduction in open high-risk findings, remediation speed, and release gate effectiveness.

---

# 18. Implementation Roadmap

## Phase 1 – Foundation

- Approve SAST policy
- Define roles and thresholds
- Identify pilot applications
- Establish evidence templates

## Phase 2 – Tool Integration

- Connect repositories
- Enable automated scans
- Configure routing and alerts
- Define release gates

## Phase 3 – Operationalize

- Train developers and reviewers
- Begin regular triage meetings
- Track remediation SLAs
- Report metrics to leadership

## Phase 4 – Optimize

- Reduce false positives
- Tune policies by application criticality
- Add trend analysis and dashboards
- Integrate with broader AppSec controls

---

# 19. Conclusion

A well-governed SAST process helps a healthcare organization find code defects before they become privacy incidents, compliance failures, or production vulnerabilities.

When Checkmarx is integrated into the SDLC with clear ownership, consistent thresholds, and strong evidence retention, it becomes a practical control for secure development and audit readiness.

---

# Appendix A – Sample SAST Report Header

| Field | Example |
|---|---|
| Application | Patient Portal |
| Scan Type | Full Repository Scan |
| Branch | release/2026.05 |
| Scan Date | 2026-05-20 |
| Findings | 96 |
| Critical | 0 |
| High | 4 |
| Medium | 21 |
| Low | 71 |

---

# Appendix B – Sample Triage Notes Template

- Finding ID
- File and line number
- Description
- Root cause
- Business impact
- Verification notes
- Fix owner
- Target fix date
- Closure evidence

---

# End of Document

