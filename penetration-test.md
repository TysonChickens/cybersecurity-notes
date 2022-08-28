---
id: btat806wf3v71jpa11klryx
title: Penetration Test
desc: ''
updated: 1653132326262
created: 1653132297591
---

# Introduction to Penetration Testing

- [ ] Learn what pentesting (penetration testing) is and why it's important.
- [ ] Understand the different types of pentesting.
- [ ] Review the different approaches to pentesting.

- [ ] Understanding the planning phase of penetration testing.
- [ ] Consider the ramifications of a real attack.
  
- [ ] Learn what vulnerability analysis is and its role in pentesting.
- [ ] Learn about different methods of gathering information.
- [ ] Understand what role social engineering plays in discovering information.
- [ ] Learn about different scanning tools.

- [ ] Learn about different methods of gaining access to a system:
  - [ ] Passive
  - [ ] Active
  - [ ] Offline
  - [ ] Without technology

- [ ] Understand the phases of a pentest attack.
- [ ] Learn what types of vulnerabilities are exploited.

- [ ] Learn about the Executive Summary and what information it details.
- [ ] Learn about the Technical Report and its benefits.

- [ ] What are the industry-leading tools used for penetration testing?

## What is Penetration Testing?

Penetration Testing
: Security testing in which assessors mimic real-world attacks to identify methods for circumventing the security features of an application, system, or network. It often involves launching real attacks on real systems and data that use tools and techniques commonly used by attackers.

### What is the Importance of Pentesting?

With cyber attacks becoming the norm, it is more important than ever to undertake regular vulnerability scans and penetration testing to identify vulnerabilities and ensure the cyber controls are working.

### Operating Systems

Desktop
- Windows
- Unix
- Linux
- MacOS
- Chrome
- Ubuntu

Mobile
- iOS
- Android
- Blackberry OS
- Windows Mobile
- WebOS
- Symbian OS

### Approaches

No two penetration tests are going to be the same because each company uses different tools, systems, and applications.

- Internal vs. external.
- Web & mobile application assessments.
- Social engineering.
- Wireless network, embedded device & IoT.
- ICS penetration.

### Penetration Testing Phases

1. Planning
2. Discovery
3. Attack
4. Report

#### Planning

- Setting objectives
  - What are the goals of the pentest?
  - What are your targets?
- Establishing boundaries
  - There are legal and ethical ramifications to consider.
  - Since the attacks are real they have the potential to interrupt availability of key functions and services.
- Informing Need-to-know employees.
  - Since there will always be some social engineering, it might be wise to inform local security so no one is arrested during the test.

#### Discovery

Vulnerability Analysis
: Vulnerability scanning can help identify outdated software versions, missing patches, and missing patches, and misconfigurations, and validate compliance with or deviations from an organization's security policy. This is done by identifying the operating systems and major software applications running on the hosts and matching them with information on known vulnerabilities stored in the scanners' vulnerability databases.

##### Google Dorks

A Google Dork query, sometimes referred to as dork, is a search string that uses advanced search operators to find information that is not readily available on a website.

Data can be found using Google Dorks:

- Admin login pages
- Username and passwords
- Vulnerable entities
- Sensitive documents
- Government/military data
- Email lists
- Bank account details and lots more...

##### Passive vs. Active

- Monitoring employees.
- Listening to network traffic.
- Network mapping.
- Port scanning.
- Password cracking.

**Passive-Online**

Wire Sniffing
: Capturing data packet across the computer network.

Man in the Middle
: Hijacking a session in real-time to obtain access.

Replay Attack
: A valid data transmission is maliciously or fraudulently repeated or delayed.

**Active-Online**

Password Guessing
: Also known as "brute force attack".

Trojan/Spyware/Keyloggers
: A spy software which collects different types of data from the session.

Hash Injection
: Authenticate to a remote server or service using the underlying NTLM or LanMan hash of a user's password.

Phishing
: Users are tricked into clicking a malicious link, which can lead to the installation of malware, a ransomware attack, or disclosure of information.

**Offline Attacks**

Pre-Computed Hashes
: Data structure that uses a hash function to store, order and/or access data in an array.

Distributed Network Attack (DNA)
: A password cracking system sold by AccessData. DNA can perform brute-force cracking of 40-bit RC2/RC4 keys. For longer keys, DNA can attempt password cracking.

- Computationally infeasible to attempt a brute-force attack on a 128-bit key.
- DNA can mine suspects hard drive for potential passwords.

Rainbow
: A table is precomputed table for reversing cryptographic hash functions, usually for cracking password hashes.

**Tech-less Discovery**

Social Engineering
: A general term related to the act of deceiving the user to surrender enough information to obtain access and/or data.

Shoulder Surfing
: Active spying by obtaining Optic access to the premises and view the access input.

Dumpster Diving
: Retrieval of information by examining the trash in search of discarded but not destroyed information.

#### Attack Phases

1. Discovery Phase
2. Gaining Access
   - Enough data has been gathered in the discovery phase to make an informed attempt to access the target.
3. Escalating Privileges
   -  If only user-level access was the obtained in the last step, the tester will now seek to gain complete control of the system (administrator-level access). 
4. System Browsing
   - The information gathering process begins again to identify mechanisms to gain access to additional systems.
5. Install Additional Tools
   -  Additional penetration. Testing tools are installed to gain additional information or access it through a combination of both.

##### Exploited Vulnerabilities

Categorized by the National Institute of Standards and technology. These are the categories that most vulnerabilities can be broken down. 

- Misconfigurations 
- Kernel Flaws
- Insufficient iInput Validations
- Symbolic Links
- File Descriptor Attacks
- Race Conditions
- Buffer Overflows
- Incorrect file and directory permissions

#### Reporting

##### Executive Summary

Communicate to the reader the specific goals of the penetration testing and the high level findings of the testing exercise.

1. Background
2. Overall Posture
3. Risk Ranking
4. General Findings
5. Recommendations
6. Road map

##### Technical Review

###### Introduction
###### Scope
###### Vulnerability Assessment
###### Vulnerability Confirmation
###### Post Exploitation
###### Risk / Exposure

## Writing a Penetration Testing Report

https://www.sans.org/white-papers/33343/

## Tools

ibm.biz/kalilinux
ibz.biz/nmap-org
ibm.biz/JTRipper
ibm.biz/metasploit
ibm.biz/wireshark
ibm.biz/hackthebox
ibm.biz/lamewalkthrough
