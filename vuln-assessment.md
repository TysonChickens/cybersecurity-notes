---
id: woqkmy53oegpxi1ia3jl833
title: Vuln Assessment
desc: ''
updated: 1661035022911
created: 1653180840220
---

# Vulnerability Assessment Tools

- [ ] Discuss various types of vulnerability assessment scanners.
- [ ] Discuss the Common Vulnerability Scoring System and how scores are assigned to vulnerabilities.
- [ ] Describe the use of A Security Technical Implementation Guide to enhance the overall security posture.
- [ ] Describe how to use the Center for Internet Security Benchmark hardening/vulnerability checklists.

---

> Vulnerability scanning identifies hosts and host attributes (e.g. operating systems, applications, open ports), but it also attempts to identify vulnerabilities rather than relying on human interpretation of the scanning results... Vulnerability scanning can help identify outdated software versions, missing patches, and misconfigurations, and validate compliance with or deviations from an organization's security policy. - NIST-SP 800-115

## Vulnerability Scanner

- Keeping an up-to-date database of vulnerabilities.
- Detection of genuine vulnerabilities without an excessive number of false positives.
- Ability to conduct multiple scans at the same time.
- Ability to perform trend analyses and create clear reports of the results.
- Provide recommendations for effective countermeasures to eliminate discovered vulnerabilities.

### Components of Vulnerability Scanners

There are 4 main components of most scanners:

Engine Scanner
: Performs security checks according to its installed plug-ins, identifying system information, and vulnerabilities.

Database
: Stores vulnerability information, scan results, and other data used by the scanner.

Report Module
: Provides scan result reporting such as technical reports for system administrators, summary reports for security managers, and high-level graph and trend reports for corporate executives' leadership.

User Interface
: Allows the administrator to operate the scanner. It may be either a Graphical User Interface (GUI), or just a command line interface.

### Host & Network

#### Internal

- It can be through Malware or virus that is downloaded onto a network through internet or USB.
- It can be a disgruntled employee who has the internal network access.
- It can be through the outside attacker who has gained the access to the internal network.
- The internal scan is done by running the vulnerability scanner on the critical components of the network from a machine which is a part of the network. This important component may include core router, switches, workstations, web server, database,etc.

#### External

- External scan is important as it is required to detect the vulnerabilities to those internet facing assets through which an attacker can gain internal access.
  - Running a vulnerability scanner on the host from the internet.
- Always a good idea to eliminate the open issues/loopholes before it can be used and exploited by a malicious user or an attacker.

### Common Vulnerability Scoring System (CVSS)

First introduced in 2005, the Common Vulnerability Scoring System (or CVSS) is a very popular framework for vulnerability scoring and has three major iterations. The current version is CVSSv3.1 (with version 4.0 in draft) a score is essentially determined by some of the following factors and many more:

1. How easy it to exploit the vulnerability?
2. Do exploits exist for this?
3. How does this vulnerability interfere with the CIA triad?

There are so many variables, a [calculator](https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator) is used to figure out the score using this framework.

A method of assigning severity rankings to computer system vulnerabilities, ranging from zero (least severe) to 10 (most severe).

- Provides a standardized vulnerability score across the industry, helping critical information flow more effectively between sections within an organization and between organizations.
- The formula for determining the score is public and freely distributed, providing transparency.
- Helps prioritize risk - CVSS rankings provide both a general score and more specific metrics.
- A vulnerability is given a classification (out of five) depending on the score that is assigned.

| Rating   | Score      |
| -------- | ---------- |
| None     | 0          |
| Low      | 0.1 - 3.9  |
| Medium   | 4.0 - 6.9  |
| High     | 7.0 - 8.9  |
| Critical | 9.0 - 10.0 |

- CVSS is not a magic bullet and has its advantages and disadvantages:

| Advantages                                                               | Disadvantages                                                                                                                     |
| ------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------- |
| CVSS has been around for a long time.                                    | Never designed to help prioritize vulnerabilities, instead, just assign a value of severity.                                      |
| Popular in organizations.                                                | Heavily assess vulnerabilities on an exploit being available. However, only 20% of all vulnerabilities have an exploit available. |
| A free framework to adopt and recommended by organizations such as NIST. | Vulnerabilities rarely change scoring after assessment despite after new developments may be found.                               |

#### Score Breakdown

Base-Exploit score
: Gives an idea of how easy it is to exploit the vulnerability and how much damage an exploit targeting that vulnerability could inflict.
- Attack vector
- Attack complexity
- Privileges required
- User interaction


Temporal score
: Ranks how aware people are of the vulnerability, what remedial steps are being taken, and whether threat actors are targeting it.
- Exploit code maturity
- Remediation level
- Report confidence


Environmental score
: Provides a more customized metric specific to an organization or work environment.
- Security requirements
- Impact score

### Security Technical Implementation Guides (STIGs)

- Defense Information Systems Agency (DISA) is the entity responsible for maintaining the security posture of the Department of Defense (DoD) IT infrastructure.
- Default configurations for many applications are inadequate in terms of security, and developing a security standard for applications would allow various DoD agencies to utilize the same standard across all application instances that exist.
- STIGs exist for a variety of software packages including Operating Systems, Database Applications, Open Source Software, Network Devices, Wireless Devices, Virtual Software, and the list continues to grow including mobile operating systems.

### Center for Internet Security (CIS)

#### Benchmarks

- CIS Benchmarks are the only consensus-based, best-practice security configuration guides both developed and accepted by government, business, industry, and academia.

#### Controls

CIS Controls are prioritized set of actions that collectively form a defense-in-depth set of best practices that mitigate the most common attacks against systems and networks.

- CIS Controls are developed by a community of IT experts who apply their first-hand experience as cyber defenders to create these globally accepted security best practices.

5 critical tenets of an effective cyber defense system in the CIS Controls:

- Offense informs defense
- Prioritization
- Measurements and Metrics
- Continuous diagnostics and mitigation
- Automation

##### CIS Control Groups

![groups](https://broadviewnetworks.ca/wp-content/uploads/2020/11/CIS-Control-Groups.png)
