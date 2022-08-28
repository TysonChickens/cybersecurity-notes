---
id: iulpmov883qv6tpqkgvbno8
title: Dev Sec Ops
desc: ''
updated: 1653181446313
created: 1653181426195
---

# DevSecOps & Security Automation

- [ ] Understand the concept of DevOps and Automation and its effect on Application Security.

---

DevOps became a development for teams primarily focused on producing new systems, applications. functionality, and making them available to consumers as quickly as possible.

- Both DevOps and security engineers want easily deployable, vulnerability free releases.

DevSecOps is now integrated, automated, continuous security: always.

![dev](https://image.slidesharecdn.com/securityintodevops-differentviewsjul182017-170718191437/95/integrate-security-into-devops-secdevops-19-638.jpg?cb=1500405759)

## Define Operating and Governance Model

- Define strategy up front & apply it throughout.
- Consider any data sovereignty requirements.
- Address any audit & compliance requirements.
- Establish your risk management process.
- Automated checks for continuous assurance.

## People & Culture

A successful program starts with the people & culture.

- Training & awareness.
- Explain & embrace new ways of working.
- Equip teams & individuals with the right level of ownership & tools.

## Learning

Continuous improvement and feedback.

- Lessons learned.
- Coding & tooling best practices level-set.
- Ongoing collaboration.
- Blameless post-mortem.

## Develop Securely: Plan

Use tools and techniques to ensure security is integral to the design, development and operation of all systems.

- **Threat Modeling & Risk Analysis** - Model the threats with experimentation & validation. Analyze risks to your system.
  - Validate
  - Experiment
  - Analysis
  - Treatment
  - Data Protection
  - Privacy Design
- **Security Backlog** - Produce security epics informed by abuse cases. Add to to project backlog.
  - Common Abuse Cases (e.g OWASP)
  - Context Abuse cases
  - Compliance Requirements
- **Architecture & Design** - Informed architecture & design with security at its core.
  - Layered Protection
  - Integrated Security

### Code & Build

Apply the model to Everything-as-Code:

- Containers
- Apps
- Platform
- Machines

Detect issues & fix them, earlier in the lifecycle.

- **Secure Application Code** - Secure coding best practice guidance. Real-time code feedback. Catch before commit.
- **Secure Infrastructure Config** - Secure infrastructure configuration best practice guidance. Image hardening.
- **OSS / COTS Validation** - Vulnerability & license scanning. Remedial guidance before commit.

## Test

- **Internal / External Testing** - Integrate & automate security testing seamlessly with DevOps activities.
- **Continuous Assurance** - Automated checks to ensure systems are always protected and conform with requirements.
- **Compliance Checking** - Address industry-specific accreditation.

## DevSecOps Deployment - Release, Deploy & Decommission

- **Continuous Component Control** - Monitor and act on changes to component security. Block vulnerable component deployment.
- **App and Infra Orchestration** - Orchestrate and automate the deployment of secure application and underlying infrastructure.
- **Data Cleansing & Retention** - Build data cleansing into decommissioning activities.

### Release

- Continuous component controls.
- Versioning of infrastructure.

### Deploy

- Cloud provider security patches IAM policies, encryption, inventory.
- CI/CD Toolchain is sole deployment mechanism.
- Repeatable, parameterized infra-as-code patterns for environment creation.
- Immutable images (containers, virtual machines).
- Centralized Key-Value & secret stores.
- Data sovereignty.

### Decommission

- Pets vs. Cattle; Destroy & create again.
- Infrastructure-as-code tools manage removal of compute instance & persistent storage.
- De-registration to update inventory and ensure clean removal of secrets.
- IAM controls to regulate authorization.
- SaaS data removal requests & policies.
- Data backup cleansing.
- Crypto-shredding.

## Operate & Monitor

If you don't detect it, you can't fix it.

- **Detect and Visualize** - Visualization of environments add context & clarity.
- **Respond & Recover** - Playbooks drive response and recovery efforts.

### Detect & Visualize

- Catalogue
- Inventory
- Compliance
- User Behavior Analytics
- RASP
- Configuration Monitoring
- Continuous scanning of container, infrastructure and network

### Respond

- Virtual patching
- Automated remediation
- Reporting
- Feedback loop from production to engineering
- Blue vs Red team game days

### Recover

- Maximize service
- Root cause analysis
- Attack-driven defense
- Shift from MTBF to MTTR
- Chaos engineering


## Why DevSecOps

- Reduce risk & cost
- Increase quality - Continuous monitoring & scanning.
- Improve team synergy - Increase collaboration & productivity.
- Enhance visibility - Threat management integration.
- Meet compliance - Address critical compliance requirements.
- Accelerate development - Security automation integrated into CI/CD pipeline.
- Secure, rapid innovation - Satisfy DevOps and CISO requirements.