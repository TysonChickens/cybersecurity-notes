---
id: dx2a2d32xn75x5h37zt99s7
title: SOC
desc: ''
updated: 1653130539140
created: 1653130531896
---

# System and Organization Controls Report (SOC) Overview

- [ ] Describe the differences between SOC1, SOC2, SOC3 Controls.
- [ ] Describe the benefits of SOC Reports.

- [ ] Describe the Audit process for SOC Reporting.

## SOC Reports

- Some industry/jurisdictions require SOC2 or local compliance audit.
- Many organizations who know compliance, know SOC2 Type 2 consider it a stronger statement of operational effectiveness than ISO 27001 (continuous testing).
- Many organization's clients will accept SOC2 in lieu of the right-to-audit.

### Compared with ISO 27001

![Compare](https://advisera.com/wp-content/uploads/sites/5/2021/02/soc-2-vs-iso-27001-what-are-the-differences.png)

### SOC 1 vs. SOC 2 vs. SOC 3

![SOC](https://www.otava.com/wp-content/uploads/SOC-report-comparison-table.jpg)

SOC 1
: Used for situations where the systems are being used for financial reporting.

- Also referenced as Statement on Standards for Attestation Engagements (SSAE) 18 AT-C 320 (formerly SSAE 16 or AT 801).

SOC 2
: Addresses a service organization's controls that are relevant to their operations and compliance, more generally than SOC 1.

- Restricted use report contains substantial detail on the system, security practices, testing methodology and results.
- Also SSAE 18 standard, sections AT-C 105 and AT-C 205.

SOC 3
: General use report to provide interested parties with a CPA's opinion about same controls in SOC 2.

### Type 1 vs. Type 2

Type 1 Report
: Service auditor expresses an opinion on whether the description of the service organization's systems is fairly presented and whether the controls included in the description are **suitably designed** to meet the applicable Trust Service criteria as of a point in time.

Type 2 Report
: Service auditor's report contains the same opinions express in a Type 1 report, but also includes an opinion on the **operating effectiveness** of the service organization's controls for a period of time. Includes description of the service auditor's *tests of operating effectiveness and test results*.

- Proof you are maintaining effectiveness over time.
- Renewed every 6 months or yearly.
- SOC1 and SOC2 each available as Type 1 and Type 2.

### SOC 2 Principles

![SOC2_Principles](https://storage.googleapis.com/website-production/uploads/2019/11/soc-2-compliance-principles-certification.jpg)

Security
: The system is protected against unauthorized access (both physical and logical). Controls related to user provisioning, user revalidation, change management, etc.

Availability
: The system is available for operation and use as committed or agreed. Controls related to virus prevention, system back-ups, disaster recovery, etc.

Confidentiality
: Information designated as confidential is protected by the system as committed or agreed.

Processing Integrity
: System processing is complete, accurate, timely, and authorized.

Privacy
: Personal information is collected, used, retained, disclosed, and destroyed in conformity with the commitments in the entity's privacy notice and with criteria set forth in generally accepted privacy principles (GAPP) issued by the AICPA and CICA.

---

## SOC Reports - Auditor Process Overview

Auditors are looking for:

Accuracy
: Controls results being assessed for pass/fail.

Completeness
: Do controls implementation cover the entire offering; e.g. no gaps in inventory, personnel, etc.

Timeliness
: Controls are performed on time (or early) with no gaps in coverage.

- If a control cannot be performed on time, are there appropriate assessment (risk) approvals **BEFORE** the control is considered 'late'.

with Resilience notice
: Checks/Balances in place such that if a control does fail.

Consistency
: Shifting control implementation raises concerns about above, plus increase testing.

## Continuous Monitoring Between Audits

### Purpose

- Ensure controls are operating as designed.
- Identify control weaknesses and failure outside an audit setting.
- Communicate results to appropriate stakeholders.

### Scope

All production devices and controls will be tested for operating effectiveness over time focusing on:

- Execution against the defined security policies.
- Execution evidence maintenance/availability.
- Timely deviation from policy documentation.
- Timely temporary failures of a control or loss of evidence documentation and communication.

