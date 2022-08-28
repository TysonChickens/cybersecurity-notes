---
id: tf7vn30fxe1zpo1bohdpmxt
title: Management
desc: ''
updated: 1653198294210
created: 1653198279063
---

# Overview of Incident Management Response

- [ ] Review the National Institute of Standards and Technology Incident Handling Guide.

- [ ] Understand the X-Force IRIS Cyberattack Framework.

- [ ] Define a breach and it's common characteristics.
- [ ] Discuss an organization's response to a breach.
---

## NIST Incident Response Lifecycle - Teams

### Computer Security Handling Guide

Recommendations from National Institute of Standards and Technology.

- Establish a formal incident response capability.
- Create an incident response policy.
- Develop an incident response plan based on the incident response policy.
- Develop incident response procedures.
- Establish policies and procedures regarding incident-related information sharing.
- Consider relevant factors when selecting an incident response team model.

#### Incident Response Team Structure

1. Team Model - A coordinating team is a group of the IT professionals that provides an organization with the services and support surrounding the prevention and management and coordination of potential cybersecurity related emergencies.
   - Small organizations with central incident response team.
   - Large organization has multiple teams on-site or geographically dispersed.
2. Team Model Selection - Cost vs. Use in-house employees or partially outsource incident response work to another organization. Common when organization needs a full-time incident response team but does not have enough available qualified employees.
3. Incident Response Personnel - Members of the incident response team should have good problem-solving skills and critical thinking abilities. It is not necessary for every team member to be a technical expert.
   - Teamwork
   - Communication
4. Incident Response Team Services

### Incident Response Lifecycle

![lifecycle](https://securitynotes.org/wp-content/uploads/2017/09/NIST-incident-response-lifecycle.png)

#### Preparation

Includes everything an organization does to get ready for incident response, such as putting in place the necessary tools and resources and training the team.

- Activities aimed at preventing incidents from occurring.

#### Detection & Analysis

Finding out what happened.

- The most important thing is to quickly determine the level of damage caused by the incident and pinpoint the source of the problem.
  - Signs of an incident are categorized as precursors and indicators.

Precursor
: A sign that an incident may occur in the future.

Indicator
: An incident may have occurred, or may be occurring now.

#### Containment, Eradication, and Recovery

After identifying the problem, an essential part of containment is decision-making and taking action.

- Incident response is about containing the incident by cutting off its source, eradicating it by eliminating all traces of it, and recovering to normal operations.

#### Post-Event Activity

A summary of what is learned from an incident to prevent similar incidents in the future.

- Collaborate with regulators or law enforcement agencies.
- Make necessary updates on new plan during an incident response.

## Cyberattack Frameworks

IBM X-Force Incident Response team have developed a comprehensive framework to address all actions attacker takes, empowering security analysts and threat-hunters with insight to narrow risk exposure and increasing cyberattacks.

### IBM X-Force IRIS Cyberattack Framework

![framework](https://securityintelligence.com/wp-content/uploads/2018/07/outside-attack-framework-v2.png)

![framework2](https://securityintelligence.com/wp-content/uploads/2018/08/execution-framework-v4-1.png)

#### Attack Beginnings: Bad Actor sets the Stage

To determine a target and prepare an attack, the preparation framework examines the steps that cyberattacks move through.

- Attacker determines objective and attacks.

This stage includes all the known methods that attackers use to advance from target selection to launching their attack to include:

- Conduct external reconnaissance.
- Align tactics, techniques and procedures (TTPs) to target.
- Prepare malware and software tools.
- Prepare attack infrastructure.

##### Defense Tips: Increase Network Security

- Build a threat profile of adversarial actors who are likely to target the company. When building the profile, ask:
  - Have threat actors targeted the organization?
  - What type of attacker would be interested in this organization?
  - Where are these threat groups?
  - What are the attackers' goals?
- Take steps to safeguard the assets attackers are likely to target, such as most critical data.
- Determine whether threat actors have interest in the organization and its assets, intellectual property, customers, or proprietary data.
- To prevent C&C servers from crafting domains that look legitimate to unsuspecting targets, purchase all the likely typo-changed domains associated with company name, and monitor suspicious domain registrations.

#### Launch and Execute Attack: The Compromise Begins

Launch Attack
: Once the attack infrastructure is ready, the attacker launches an attack gainst the target, either directly or indirectly, and defines the attack as successful or failed.

Examples of direct attacks:

- Stolen credentials.
- Phishing email with a malicious file or domain attached.

Examples of indirect attacks:

- Infection of a work laptop while connected to a home network.
- Compromise of a website or online advertisement.

Access Environment
: Once the attack is determined successful, the attacker will work quickly to establish a foothold.

Execute initial compromise
: The attacker gains access to at least one host on the network or has logged in to a user's account.

Establish Foothold
: The attacker ensures continued access to, and control of, at least one host or user account within the network.

##### More Defense Tips Network Security - Attack Continues / Expand Access

- Harden the attack surface and deter most attackers from viewing the organization as an easy target with methods such as efficient and timely patch management.
- Include patch management performance metrics in the system adminstration process and use automated checks for patches.
- Apply the concept of least privilege: Make sure users and systems only have access privileges that correspond with their role; remove excess privileges; and only allow users and systems to perform authorized tasks.
- To disrupt attacks, implement a strong endpoint detection and mitigation strategies.
- Employ a threat-hunting program to aid in threat identification and mitigation.
- Refine threat-hunting program.
  - As unknown threats are discovered, migrate associated threat indicators as signatures into detection and protection platforms to automatically identify any other instances.
- Invest in a centralized logging and analysis platform to automatically prioritize data and place it into tiers ranging from benign activities to those likely indicating maliciousness.
- Whitelist and create a baseline for normal activity, and perform frequency analysis.
- Enforce strong user password policies by enabling multi-factor authentication (MFA), restricting the ability to use the same password across systems, and storing password hashes in secured locations to prevent password-stealing methods.

#### Attack Gains Strength: Continuous Phases Occur

Some aspects of cyberattacks are continuously present during the attack lifecycle.

Operational Security
: Throughout attack preparation, operational security represents all the actions attackers take to hide their attack preparations from the victims or cybersecurity defenders.

Defense Evasion and Monitoring
: Attack activity exists throughout the execution cycle and reflects the efforts bad actors may use to evade detection. Tactics include the use of malicious software designed to disguise the attack presence and data masking.

Feedback Pipeline
: Exists from the time the attack preparation begins, all the way through the execution stage.

##### More Defense Tips from Attack

- Analyze all network traffic and endpoints, and search often for anomalous behavior to disrupt defense evasions and monitoring tactics.
- Set up a honeypot- a deceptive file or system designed to trick attackers into accessing it- to trigger an immediate alert to security teams with details regarding the activity on the honeypot, including user information and logged keystrokes.
- Monitor or restrict unusual data transfers, specifically:
  - Creation of RAR files, which can be used to exfiltrate information. Investigate spikes in emails to external addresses.
  - Creation of auto forward rules and new email delegates.
  - Excessive traffic leaving through file transfer protocol (FTP) or Domain Name Server (DNS).  

#### Attack Objective Execution: Attacker Completes the Mission

Execute Objective
: Once the execution phases are completed successfully, the attacker moves toward the final goal, which could include disruption through financial or data theft, ideological messaging, or industrial espionage.

##### Defense Tips for Security

- Build and train a dedicated team to respond to security incidents.
- Practice relevant attack scenarios using tabletop exercises or simulations that mimic a cyberattack.
- Thoroughly examine available forensics to understand attack details, establish mitigation priorities, provide data to law enforcement and plan risk reduction strategies.
- Consider an incident response retainer with trusted security partners.

## What is a Breach?

Breach
: A data breach is the result of another security incident, whether it's an attack by hackers, a careless or malicious insider, or even an accident involving faulty processes or procedures.

- A data breach involves data either belonging to the organization only but more often both inside and outside the organization.

### Organization Only

This type of breach will cause profits and new business.

### Data Inside and Outside of the Organization

Involve loss of business revenue and typically legal sanctions.

### Technical Aspects

Isolating network segments, removing malware and limiting system access to downed systems.

### Communications

Federal organization or law enforcement agencies with healthcare data and financial institutions.

### Who should be Involved?

- Management and Technical Incident Response Team
- Legal personnel
- Public relations

The team **MUST** be be defined in the Incident Response Strategy **PRIOR** to a data breach.