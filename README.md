---
description: This is my place to store all my knowledge learning about cybersecurity.
cover: >-
  https://images.unsplash.com/photo-1550751827-4bd374c3f58b?crop=entropy&cs=tinysrgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHw0fHxzZWN1cml0eXxlbnwwfHx8fDE2NjE5ODk3Mzk&ixlib=rb-1.2.1&q=80
coverY: -624.2578456318914
---

# 💭 Welcome to Tyson's Cybersecurity World!

## Cybersecurity Journey

There is much to learn so click around and explore!

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}

### Today's Cybersecurity Challenges

* The current threats, alerts, and the needed knowledge are increasing. Meanwhile, the available analysts and time are trending down.
* By 2025, there will be 3.5 million unfulfilled cybersecurity jobs.

## Security Analyst and SOC

A security operation center is a team of IT security professionals monitoring a company's network and systems 24 hours a day, seven days a week.&#x20;

McAfee's Definition: _"Security operations teams are charged with monitoring and protecting many assets, such as intellectual property, personnel data, business systems, and brand integrity. As the implementation component of an organization's overall cybersecurity framework, security operations teams act as the central point of collaboration in coordinated efforts to monitor, assess, and defend against cyber attacks"._

* **Find vulnerabilities on the network**: A vulnerability is a weakness that an attacker can exploit to carry out things beyond their permission level.
  * The SOC might discover a set of MS Windows computers that must be patched against a specific published vulnerability.
  * Vulnerabilities are not necessarily the SOC’s responsibility; however, unfixed vulnerabilities affect the security level of the entire company.
* **Detect unauthorized activity**: It is crucial to detect any unauthorized activity quickly before it causes any damage.
* **Discover policy violations**: A security policy is a set of rules and procedures created to help protect a company against security threats and ensure compliance.
  * What is considered a violation would vary from one company to another; example include downloading pirated media files and sending confidential company files insecurely.
* Detect intrusions: Intrusions refer to system and network intrusions.
* **Support with the incident response**: An incident can be an observation, a policy violation, an intrusion attempt, or something more damaging such as a major breach.
  * Responding correctly to a severe incident is not an easy task. The SOC can support the incident response team handle the situation.

## Elements of Security Operations Center (SOC)

* Example data sources that the SOC relies on.
* The services that the SOC provides.
* An example scenario.
* Investigate monitor, prevent, respond to threats 24/7 clock.

## Responsibilities for the SOC

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/60c7fac321aca20049602d2b/room-content/ac6d125de72c99f799d13c1aaf0c55dd.PNG" alt=""><figcaption></figcaption></figure>

### Preparation and Prevention&#x20;

* Stay informed of current cybersecurity alerts.&#x20;
* Detect & hunt threats to work on security roadmap to protect the organization for worst-case scenario.&#x20;

Prevention methods:&#x20;

* Gather intelligence data on the latest threats, threat actors, TTPs.
* Maintenance procedures- Firewalls signatures, patch vulnerabilities, block-listing / safe-listing applications, email addresses and IPs.

### Monitoring & Investigation

SOC team proactively uses SIEM (Security Information Event Management and EDR (Endpoint Detection & Response) tools to monitor suspicious malicious network activities.&#x20;

Learn how to prioritize alerts based on their level:&#x20;

* Low
* Medium
* High
* Critical&#x20;

Junior Security Analysts are crucial roles in the investigation procedure.

* Perform triage ongoing alerts by exploring & understanding how an attack works.
* Ask "How and why?"&#x20;
* Security analysts find answers via data logs & alerts using open-source tools.

### Response

After investigation, SOC team takes actions on the compromised hosts from the network terminating processes, deleting files, and more.

## Data Sources

The SOC uses many data sources to monitor the network for signs of intrusions and to detect any malicious behavior.

* **Server logs**: There are many types of servers on a network, such as a mail server, web server, and domain controller on MS Windows networks.
  * Logs can contain information about various activities such as successful and failed login attempts, and more.
* **DNS activity**: DNS stands for Domain Name System, and it is the protocol responsible for converting a domain name to an IP address.
  * The SOC can gather information about domain names that internal systems are trying to communicate with by inspecting DNS queries.
* **Firewall logs**: A firewall is a device that controls network packets entering and leaving the network by letting them through or blocking them.
* **DHCP logs**: DHCP stands for Dynamic Host Configuration Protocol, and it is responsible for assigning an IP address to the systems that try to connect to a network.
  * Inspecting DHCP transactions can learn about the devices that joined the network.

## SOC Services

Services include reactive and proactive services in addition to other services.

Reactive services refer to tasks initiated after detecting an intrusion or a malicious event.

* **Monitor security posture**: The primary role of the SOC, and it includes monitoring the network and computers for security alerts and notifications and responding to them.
* **Vulnerability management**: Refers to finding vulnerabilities in the company systems and patching (fixing) them. The SOC can assist but not necessarily execute them.
* **Malware analysis**: The SOC might recover malicious programs that reached the network.
  * Can do basic analysis by executing it in a controlled environment.
* **Intrusion detection**: An IDS is used to detect and log intrusions and suspicious packets. The SOC's job is to main such a system, monitor its alerts, and go through its logs as the need dictates.

Proactive services refer to tasks handled by the SOC without any indicator of an intrusion.

* **Network security monitoring (NSM):** Focuses on monitoring the network data and analyzing the traffic to detect signs of intrusions.
* **Threat hunting**: The SOC assumes an intrusions has already taken place and begins its hunt to see if they can confirm this assumption.
* **Threat Intelligence**: Focuses on learning about potential adversaries and their tactics and techniques to improve the company's defenses.

Other services include cyber security training. Many data breaches and intrusions can be avoided by raising users' security awareness.

### Example Scenario

One role in a SOC is the SOC analyst. A SOC analyst is responsible for network security monitoring and log management.

* Notices a particular DNS query repeating every minute - a behavior unusual for normal user browsing the internet.
  * Discover a process (program) using DNS to communicate with a malicious server.
  * Found out the computer was infected after visiting a malicious website by reviewing the computer logs.
  * The laptop is cleaned, and threat hunting starts to ensure that no other computers are infected.

{% content-ref url="general-knowledge/ibm-guardium-data-security-and-protection/siem-concepts/" %}
[siem-concepts](general-knowledge/ibm-guardium-data-security-and-protection/siem-concepts/)
{% endcontent-ref %}

#### SOC Analyst Tasks

* Review security incidents in IBM QRadar Security Information and Event Management (SIEM).
* Review the data that comprise the incident (events / flows).
* Pivot data multiple ways to find outliers (such as unusual domains, IPs, file access)
* Expand search to capture more data around the incident.
* Decide which incident to focus on next.
* Identify the name of the malware.
* Take newly found Indicators of Compromise (IOCs) from the Internet and search from them back in SIEM.
* Find other Internal IPs are potentially infected with the same malware.
* Search Threat Feeds + Search Engine + Virus total + favorite tools for these outliers / indicators; Find new malware at play.
* Start another investigation around each of these IPs.
* Review the payload outlying events for anything interesting (domains, MD5s, etc.)
* Search more websites for IOC information that malware from the Internet.
