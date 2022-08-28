---
id: nuj3aqp0hv7sf09tj7fr9qf
title: Response
desc: ''
updated: 1659049996192
created: 1653034622726
---

# Access Management and Incident Response

- [ ] Describe the access management and incident response processes.
- [ ] Describe the management process of Incident Response, how it is implemented, and why it is important to an overall security schema.

- [ ] Describe the key concepts of Incident Response:
  - [ ] E-Discovery
  - [ ] Use of automated systems
  - [ ] Business Continuity Planning and Disaster Recovery
  - [ ] Post-incident activities

- [ ] Describe the cyber security incident response processes and the 3 phases of Prepare, Respond and Follow up.

---

## Access Management

Authorization is the process of allowing somebody to access a specific object.

- Access criteria
  - Groups
  - Time frame and specific dates
  - Physical location
  - Transaction type

- "Need to know" only access information needed for the role.
- Single Sign-on (SSO)

### Authentication Concepts

- Identity proof
- Kerberos (SSO)
- Mutual authentication
  - MS-CHAP V2
- SID's vs DACL's
  - Security ID (Active Directory)
  - Discretionary Access Control List

---

## Incident Response

A breach of security is known as an incident. Despite all threat models and secure system designs, incidents do happen. Actions taken to resolve and remediate the threat are known as Incident Response (IR) and are a whole career path in cybersecurity.

Incidents are classified using a rating of urgency and impact. Urgency will be determined by the type of attack, where the impact will be determined by the affected system and what impact that has on business operations.

![urgency-impact](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/ab0cc8478b0bce9a400187f559d36dd6.png)

An incident is responded to by a Computer Security Incident Response Team (CSIRT), which is a group of employees with technical knowledge about the systems and/or current incident.

Incident Management
: Computer security incident management involves the monitoring and detection of security events on a computer or a computer network and the execution of proper resources to those events. Means the information security or the incident management team will regularly check and monitor the security events occurring on a computer or in our network.

### Key Components

Events
: An observed change to the normal behavior of a system, environment, process, workflow, or person. Examples: router, ACLs were updated, firewall policy was pushed.

Incident
:  An event that negatively effects the confidentiality, integrity, and/or availability (CIA) at an organization in a way that impacts the business.

Response team - Computer Security Incident Response Team
: A team that receives reports of security breaches, conducts analyses of the reports and responds to the senders. A CSIRT may be an established group or an ad hoc assembly.

Investigation
: The investigation seeks to determine the circumstances of the incident. Every incident will warrant or require an investigation. Collect evidence and keep in mind the chain of custody.

### Key Concepts

E-Discovery
: Data inventory helps to understand the current tech status, data classification, data management, use automated systems. Understand how to control data retention and backup.

Automated Systems
: Using SIEM, SOA, UBA, big data analysis, honeypots/honey-tokens, artificial intelligence or other technologies could enhance the mechanism to detect and control incidents that could compromise the tech environment.

BCP (Business Continuity Plan) & Disaster Recovery
: Understand the company in order to prepare the BCP. A BIA (Business Impact Analysis) is also good to have a clear understanding of the critical business areas. Also indicate if a security incident will trigger the BCP or the disaster recovery.

Post-Incident
: Root-cause analysis, understand the difference between error, problem and isolated incident. Lessons learned and reports are key.

### Incident Response Process

#### 1. Prepare

The first phase about setting up appropriate procedures with the right tools before the occurrence of an incident.

1. Conduct a criticality assessment for the organization.
2. Carry out a cyber security threat analysis, supported by realistic scenarios.
3. Consider the implications of people, process, technology and information.
4. Create an appropriate control framework.
5. Review your state of readiness in cyber security incident response.

#### 2. Respond

Identification of the actual incident to look at the affected areas of the network or the system.

1. Identify cyber security incident.
2. Define objectives and investigate situation.
3. Take appropriate action.
4. Recover systems, data, and connectivity.

#### 3. Follow Up

1. Investigate incident more thoroughly.
2. Report incident to relevant stakeholders.
3. Carry out a post incident review.
4. Communicate and build on lessons learned.
5. Update key information, controls and processes.
6. Perform trend analysis.

![[incident-response]]
