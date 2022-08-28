---
id: e77elhqi5fhnpz5kdvxeudb
title: Industry Standards
desc: ''
updated: 1653130585450
created: 1653130423955
---

# Industry Standards

- [ ] Define the three rules established as standards for the Health Insurance Portability and Accountability Act (HIPAA).
- [ ]  Describe why HIPAA compliance is so important to an organization.
- [ ]  Describe key HIPAA terms.

- [ ] Describe the Payment Card Industry Data Security Standard (PCI DSS)
- [ ] Describe the goals and requirements of PCI DSS.
- [ ] Describe the scope of PCI DSS as it relates to PEople, Process and Technology.
- [ ] Highlight new and key requirements for PCI DSS.

---

## Health Insurance Portability and Accountability Act (HIPAA)

Healthcare organizations use cloud services to achieve more than savings and scalability.

- Foster virtual collaboration across care environments.
- Leverage full potential of existing patient data.
- Address challenges in analyzing patient needs.
- Provide platforms for care innovation.
- Expand delivery network.
- Reduce response time in the case of emergencies.
- Integrate data silos and optimizes information flow.
- Increase resource utilization.
- Simplify processes, reducing administration cost.

### What is HIPAA-HITECH?

- The U.S Federal laws and regulations that define the control of most personal healthcare information (PHI) for companies responsible for managing such data:
  - Health Insurance Portability and Accountability (HIPAA)
  - Health Information Technology for Economic Clinical Health Act (HITECH)

- The HIPAA Privacy Rule establishes standards to protect individuals' medical records and other personal health information and applies ot health plans, health care clearinghouses, and those health care providers who conduct certain health care transactions electronically.
- The HIPAA Security Rule establishes a set of security standards for protecting certain health information that is held or transferred in electronic form. The Security Rule operational the protections contained in the Privacy Rule by addressing the technical and non-technical safeguards that **must** be put in place to secure individuals' electronic protected health information (e-PHI).

#### HIPAA Definitions

U.S Department of Health & Human Services (HHS) Office of Civil Rights (OCR)
: Governing entity for HIPAA.

Covered Entity
: HHS-OCR define companies that manage healthcare data for their customers as a Covered Entity.

Business Associate
: Any vendor company that supports the Covered Entity.

Protected Health Information (PHI)
: Any information about health status, provision of health care, or payment for health care that is maintained by a Covered Entity (or a Business Associate of a Covered Entity), and can be linked to a specific individual.

HHS-OCR "Wall of Shame"
: Breach Portal: Notice to the Secretary of HHS Breach of Unsecured Protected Health Information.

### Why Compliance is Essential

- U.S Law states that all individuals have the right to expect that their private health information be kept private and only be used to help assure their health.
- There are significant enforcement penalties if a Covered Entity / Business Associate is found in violation.
- HHS-OCR can do unannounced audits on the (**CE** + **BA**) or just the **BA**.

HIPAA is a U.S Regulation.

- Other countries have similar regulations / laws.
  - Canada - Personal Information Protection and Electronic Documents Act.
  - European Union (EU) Data Protection Directive (GDPR).
- Many US states address patient privacy issues and are more strict than those set forth in HIPAA and therefore supersedes the US regulations.
- Some international companies will require HIPAA compliance for a either a measure of confidence, or because they intend to do business with US data.

### HIPAA Security Rule

The Security Rule requires covered entities to maintain reasonable and appropriate **administrative**, **technical**, and **physical safeguards** for protecting **"electronic protected health information" (e-PHI)**.

Covered Entities must:

- Ensure the confidentiality, integrity, and availability of all e-PHI they create, receive, maintain or transmit.
- Identify and protect against reasonably anticipated threats to the security or integrity of the information.
- Protect against reasonably anticipated, impermissible uses or disclosures.
- Ensure compliance by their workforce.

### Administrative Safeguards

The Administrative Safeguards provisions in the Security Rule require covered entities to perform risk analysis as part of their security management processes.

- Security Management Process
- Security Personnel
- Information Access Management
- Workforce Training and Management
- Evaluation

### Technical Safeguards

- Access Control
- Audit Controls
- Integrity Controls
- Transmission Security

### Physical Safeguards

- Facility Access and Control
- Workstation and Device Security

---

## Payment Card Industry Data Security Standard (PCI DSS)

![PCI-DSS](http://cdn2.hubspot.net/hub/41683/hubfs/images/PCI_Data_Security_Standard.png?t=1464053240772&width=487)

- The Payment Card Industry Data Security Standard (PCI DSS) was introduced in 2004 by American Express, Discover, MasterCard and Visa in response to security breaches and financial losses within the credit card industry.
- Since 2006, the standard has been evolved and maintained by the PCI Security Standards Council, a "global organization, maintains, evolves and promotes Payment Card Industry standards for the safety of cardholder data across the globe."
- The PCI Security Standards Council is now comprised of American Express, Discover, JCB International, MasterCard and Visa Inc.
  - Applies to all entities that store, process, and/or transmit cardholder data.
  - Covers technical and operational practices for system components included in or connected to environments with cardholder data.
- PCI DSS 3.2 includes a total of 264 requirements grouped under 12 main requirements.

### Scope

The Cardholder Data Environment (CDE)
: People, processes and technology that store, process or transmits cardholder data or sensitive authentication data.

- Primary Account Number (PAN)
- PAN plus any of the following:
  - Cardholder name
  - Expiration date and/or service code

Sensitive Authentication Data
: Security-related information (including but not limited to card validation codes/values, full track data (from the magnetic stripe or equivalent on a chip), PINs, and PIN blocks) used to authenticate cardholders and/or authorize payment card transactions.

Sensitive Areas
: Anything that accepts, processes, transmits or store cardholder data and houses systems that contain cardholder data.

### PCI Requirements

Highlight new and key requirements.

- Approved Scanning Vendor (ASV) scans (quarterly, external, third-party).
- USE PCI scan policy in Nessus for internal vulnerability scans.
- File Integrity Monitoring (FIM).
- Firewall review frequency every 6 months.
- Automated logoff of idle session after 15 minutes.
- Responsibility Matrix
