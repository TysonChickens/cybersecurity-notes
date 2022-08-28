---
id: pd3512leoloo1qll6fr2j0o
title: Incident Response
desc: ''
updated: 1653132363884
created: 1653132352687
---

# Incident Response Overview

- [ ] Describe the various phases of an incident response including preparation, detection, analysis, eradication, recovery, and post incident activities.
- [ ] Explain the importance of documentation in Incident Response.
- [ ] Be able to discuss the components of an incident response policy and how that can help members of a IR team.

- [ ] Learn about incident response policies.
- [ ] Review the resources needed for incident response teams to be successful.
- [ ] Learn about the recommended practices for securing networks, systems, and applications.
- [ ] Preparation Checklist.

- [ ] Learn the difference between Precursors and Indicators and their common sources.
- [ ] Learn about the different types of monitoring systems used for detection.
- [ ] Learn about the importance of prioritization and documentation.
- [ ] Review the possible communication channels needed.

- [ ] Learn what to take into consideration when selecting a containment strategy.
- [ ] Learn why backup and forensics are key for containment.
- [ ] Review goals of eradication and recovery.
- [ ] Review Sans Institute Checklist.

- [ ] Learn what a "Lessons Learned" review and meetings are.
- [ ] Review other situational activities.
---

## What is Incident Response?

Events
: An event can be something as benign and unremarkable as typing on a keyboard or receiving an email.

- In some cases, if there is an Intrusion Detection System (IDS), the alert can be considered an event until validated as a threat.

Incidents
: An event that negatively affects IT systems and impacts on the business. It is an unplanned interruption or reduction in quality of an IT service.

- An event can lead to an incident, but no the other way around.

### Importance of Incident Response

One of the benefits of having an incident response is that it support responding to incidents systematically so that the appropriate actions are taken, it helps personnel to minimize loss or theft of information and disruption of services caused by incidents, and to use information gained during incident handling to better prepare for handling future incidents.

## IR Team Models

- Central (small company)
- Distributed (large company with many resources)
- Coordinating (advice / assisting team)

### Coordinating Teams

Incidents do not occur in a vacuum and can have an impact on multiple parts of a business. Establish relationships with the following teams:

- Management &rarr; Information Assurance &rarr; IT Support &rarr; Legal &darr; Physical Security & Facilities Management
&darr; 
- Public Affairs & Media Relations &rarr; Human Resources &rarr; Business Continuity Planning &rarr; Physical Security & Facilities Management

## Common Vector Attacks

Organizations should be generally prepared to handle any incident but should focus on being prepared to handle incidents that use common attack vectors.

- External/Removable Media
- Intrusion
- Web
- Email
- Impersonation
- Loss or Theft of Equipment

## Baseline Questions

**Knowing the answers to these will help coordination with other teams and the media.**

- Who attacked you? Why?
- When did it happen? How did it happen?
- Did this happen because you have poor security processes?
- How widespread is the incident?
- What steps are you taking to determine what happened and to prevent future occurrences?
- What is the impact of the incident?
- Was any personally identifiable information exposed?
- What is the estimated cost of this incident?

## Incident Response Phases

### Preparation

#### Incident Response Policy

IR Team
: The composition of the incident response team within the organization.

Roles
: The role of each of the team members.

Means, Tools, Resources
: The technological means, tools, and resources that will be used to identify and recover compromised data.

Policy Testing
: The persons responsible for testing the policy.

Action Plan
: How to put the policy into action.

#### Resources

##### Incident Handler Communications and Facilities

- Contact information
- On-call information
- Incident reporting mechanisms
- Issue tracking system
- Smartphones
- Encryption software
- War room
- Secure storage facility

##### Incident Analysis Hardware and Software

- Digital forensic workstations and/or backup devices
- Laptops
- Spare workstations, servers, and networking equipment
- Blank removable media
- Portable printer
- Packet sniffers and protocol analyzers
- Digital forensic software
- Removable media
- Evidence gathering accessories

##### Incident Analysis Resources

- Port lists
- Documentation
- Network diagrams and lists of critical assets
- Current baselines
- Cryptographic hashes

#### The Best Offense

Keeping the number of incidents reasonably low is very important to protect the business processes of the organization. If security controls are insufficient, higher volumes of incidents may occur, overwhelming the incident response team.

Risk Assessment
: Periodic risk assessments of systems and apps should determine what risk are posed by combinations of threats and vulnerabilities.

Host Security
: All hosts should be hardened appropriately using standard configurations, adhere to strict ACLs, and be monitored continuously.

Network Security
: The network perimeter should be configured to deny all activity that is not expressly permitted.

Malware Prevention
: Software to detect and stop malware should be deployed throughout the organization.

User Awareness and Training
: Users should be made aware of policies and procedures regarding appropriate use of networks, systems, and applications.

#### Checklist

- Are all members aware of the security policies of the organization?
- Do all members of the Computer Incident Response Team know whom to contact?
- Do all incident responders have access to journals and access to incident response toolkit to perform the actual incident response process?
- Have all members participated in incident response drills to practice the incident response process and to improve overall proficiency on a regularly established basis?

### Detection & Analysis

#### Precursors & Indicators

Precursors
: A sign that an incident may occur in the future.

- Web server log entries that show the usage of a vulnerability scanner.
- An announcement of a new exploit that targets a vulnerability of the organization's mail server.
- A threat from a group stating that the group will attack the organization.

Indicators
: A sign that an incident may have occurred or may be occurring now.

- Antivirus software alerts when it detects that a host is infected with malware.
- A system administrator sees a filename with unusual characters.
- A host records auditing configuration change in its log.
- An application logs multiple failed login attempts from an unfamiliar remote system.
- An email administrator sees a large number of bounced emails with suspicious content.
- A network administrator notices an unusual deviation from typical network traffic flows.

#### Monitoring Systems

- Monitoring systems are crucial for early detection of threats.
- These systems are not mutually exclusive and still require an IR team to document and analyze the data.

IDS vs IPS
: Intrusion Detection Systems (IDS) and Intrusion Prevention Systems (IPS) are both parts of the network infrastructure. The main difference between them is that IDS is a monitoring system, while IPS is a control system.

DLP
: Data loss prevention (DLP) is a set of tools and processes used to ensure that sensitive data is not lost, misused, or accessed by unauthorized users.

SIEM
: Security Information and Event Management solutions combine Security Event Management (SEM) - which carries out analysis of event and log data in real-time with Security Information Management (SIM).



#### Documentation

Regardless of the monitoring system, highly detailed, thorough documentation is needed for the current and future incidents.

1. The current status of the incident.
2. A summary of the incident.
3. Indicators related to the incident.
4. Other incidents related to this incident.
5. Actions taken by all incident handlers on this incident.
6. Chain of custody, if applicable.
7. Impact assessments related to the incident.
8. Contact information for other involved parties.
9. A list of evidence gathered during the incident investigation.
10. Comments from incident handlers.
11. Next steps to be taken (e.g. rebuild the host, upgrade an application).

##### Functional Impact Categories

None
: No effect to the organization's ability to provide all services to all users.

Low
: Minimal effect; the organization can still provide all critical services to all users but has lost efficiency.

Medium
: Organization has lost the ability to provide a critical service to a subset of system users.

High
: Organization is no longer able to provide some critical services to any users.

##### Information Impact Categories

None
: No information was exfiltrated, changed, deleted, or otherwise compromised.

Privacy Breach
: Sensitive personally identifiable information (PII) of taxpayers, employees, beneficiaries, etc. was access or exfiltrated.

Proprietary Breach
: Unclassified proprietary information, such as protected critical infrastructure information (PCII), was accessed or exfiltrated.

Integrity Loss
: Sensitive or proprietary information was changed or deleted.

##### Recoverability Effort Categories

Regular
: Time to recovery is predictable with existing resources.

Supplemented
: Time to recovery is predictable with additional resources.

Extended
: Time to recovery is unpredictable; additional resources and outside help are needed.

Not Recoverable
: Recovery from the incident is not possible (e.g, sensitive data exfiltrated and posted publicly); launch investigation.

##### Notifications

Alert anyone that is possibly involved with incident.

- CIO
- Local and Head of information security
- Other incident response teams within the organization
- External incident response teams (if appropriate)
- System owner
- Human resources
- Public affairs
- Legal department
- Law enforcement (if appropriate)

### Containment, Eradication & Recovery

Containment is important before an incident overwhelms resources or increases damage. Containment strategies vary based on the type of incident. For example. the strategy for containing an email-born malware infection is quite different from that of a network-based DDoS attack.

An essential part of containment is decision-making. Such decisions are much easier to make if there are predetermined strategies and procedures for containing the incident.

1. Potential damage to and theft of resources.
2. Need for evidence preservation.
3. Service availability.
4. Time and resources needed to implement the strategy.
5. Duration of the solution.

#### Forensics in Incident Response

Evidence should be collected according to procedures that meet all applicable laws and regulations that have been developed from previous discussions with legal staff and appropriate law enforcement agencies so that any evidence can be admissible in court. - NIST 800-61

1. Capture a backup image of the system as-is.
2. Gather evidence.
3. Follow Chain of Custody protocols.

#### Eradication & Recovery

1. After an incident has been contained, eradication may be necessary to eliminate components of the incident, such as deleting malware and disabling breached user accounts, as well as identifying and mitigating all vulnerabilities that were exploited.
2. Recovery may involve such actions such as restoring systems from clean backups, rebuilding systems from scratch, replacing compromised files with clean versions, installing patches, changing passwords, and tightening network perimeter security (e.g., firewall rule sets, boundary router access control lists).
3. High level of testing and monitoring are often deployed to ensure restored systems are no longer impacted by the incident. This could take weeks or months depending on how long it takes to bring back compromised systems into production.

#### Checklist

- Can the problem be isolated? Are all affected systems isolated from non-affected systems? Have forensics copies of affected systems been created for further analysis?
- If possible, can the system be re-imaged and then hardened with patches and/or other countermeasures to prevent or reduce the risk of attacks? Have all malware and other artifacts left behind by the attackers been removed and the affected systems hardened against further attacks?
- What tools are you going to use to test, monitor, and verify that the systems being restored to productions are not compromised by the same methods that cause the original incident?

https://learn.saylor.org/mod/book/tool/print/index.php?id=29706

### Post-Incident Activity

#### Lessons Learned

- Exactly what happened, and at what times?
- How well did staff and management perform in dealing with the incident? Were the documented procedures followed? Were they adequate?
- What information was needed sooner?
- Were any steps or actions taken that might have inhibited the recovery?
- What would the staff and management do differently the next time a similar incident occurs?
- How could information sharing with other organizations have been improved?
- What corrective actions can prevent similar incidents in the future?
- What precursors or indicators should be watched for in the future to detect similar incidents?

#### Utilizing data collected
#### Evidence retention
#### Documentation




