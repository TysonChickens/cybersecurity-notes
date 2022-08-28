---
id: l9xnppid7xhd6dbt1uus1dj
title: Operations
desc: ''
updated: 1657351706582
created: 1656743430201
---

# Security Operations Center (SOC)

A security operation center is a team of IT security professionals monitoring a company's network and systems 24 hours a day, seven days a week.

- **Find vulnerabilities on the network**: A vulnerability is a weakness that an attacker can exploit to carry out things beyond their permission level. 
  - The SOC might discover a set of MS Windows computers that must be patched against a specific published vulnerability.
  - Vulnerabilities are not necessarily the SOC’s responsibility; however, unfixed vulnerabilities affect the security level of the entire company.
- **Detect unauthorized activity**: It is crucial to detect any unauthorized activity quickly before it causes any damage.
- **Discover policy violations**: A security policy is a set of rules and procedures created to help protect a company against security threats and ensure compliance.
  - What is considered a violation would vary from one company to another; example include downloading pirated media files and sending confidential company files insecurely.
- Detect intrusions: Intrusions refer to system and network intrusions.
- **Support with the incident response**: An incident can be an observation, a policy violation, an intrusion attempt, or something more damaging such as a major breach.
  - Responding correctly to a severe incident is not an easy task. The SOC can support the incident response team handle the situation.

## Elements of Security Operations

- Example data sources that the SOC relies on.
- The services that the SOC provides.
- An example scenario.

### Data Sources

The SOC uses many data sources to monitor the network for signs of intrusions and to detect any malicious behavior.

- **Server logs**: There are many types of servers on a network, such as a mail server, web server, and domain controller on MS Windows networks.
  - Logs can contain information about various activities such as successful and failed login attempts, and more.
- **DNS activity**: DNS stands for Domain Name System, and it is the protocol responsible for converting a domain name to an IP address.
  - The SOC can gather information about domain names that internal systems are trying to communicate with by inspecting DNS queries.
- **Firewall logs**: A firewall is a device that controls network packets entering and leaving the network by letting them through or blocking them.
- **DHCP logs**: DHCP stands for Dynamic Host Configuration Protocol, and it is responsible for assigning an IP address to the systems that try to connect to a network.
  - Inspecting DHCP transactions can learn about the devices that joined the network.

### SOC Services

Services include reactive and proactive services in addition to other services.

Reactive services refer to tasks initiated after detecting an intrusion or a malicious event.

- **Monitor security posture**: The primary role of the SOC, and it includes monitoring the network and computers for security alerts and notifications and responding to them.
- **Vulnerability management**: Refers to finding vulnerabilities in the company systems and patching (fixing) them. The SOC can assist but not necessarily execute them.
- **Malware analysis**: The SOC might recover malicious programs that reached the network.
  - Can do basic analysis by executing it in a controlled environment.
- **Intrusion detection**: An IDS is used to detect and log intrusions and suspicious packets. The SOC's job is to main such a system, monitor its alerts, and go through its logs as the need dictates.

Proactive services refer to tasks handled by the SOC without any indicator of an intrusion.

- **Network security monitoring (NSM):** Focuses on monitoring the network data and analyzing the traffic to detect signs of intrusions.
- **Threat hunting**: The SOC assumes an intrusions has already taken place and begins its hunt to see if they can confirm this assumption.
- **Threat Intelligence**: Focuses on learning about potential adversaries and their tactics and techniques to improve the company's defenses.

Other services include cyber security training. Many data breaches and intrusions can be avoided by raising users' security awareness.

### Example Scenario

One role in a SOC is the SOC analyst. A SOC analyst is responsible for network security monitoring and log management.

- Notices a particular DNS query repeating every minute - a behavior unusual for normal user browsing the internet.
  - Discover a process (program) using DNS to communicate with a malicious server.
  - Found out the computer was infected after visiting a malicious website by reviewing the computer logs.
  - The laptop is cleaned, and threat hunting starts to ensure that no other computers are infected.

### [[More information about SOC and SIEM|SIEM#SIEM]]