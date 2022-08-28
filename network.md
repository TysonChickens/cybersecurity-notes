---
id: bc8xy1i30goti97d9k956l9
title: Network
desc: ''
updated: 1656650129601
created: 1656572511638
---

# Network Security Introduction

A computer network is a group of computers and devices connected with each other. Network security focuses on protecting the security of these devices and the links connecting them.

Network security consists of different hardware and software solutions to achieve the set of security goals. Hardware solutions refer to the devices you set up on a network to protect network security. Examples of hardware appliances:

- Firewall appliance: The firewall allows and blocks connections based on a predefined set of rules.
- Intrusion Detection System (IDS): Detects system and network intrusions and intrusion attempts to break into the network.
- Virtual Private Network (VPN): Ensures that the network traffic cannot be read nor altered by a third party. It protects the confidentiality (secrecy) and integrity of the sent data.

On the other hand, we have software security solutions:

- Antivirus software: Install on your computer or smartphone to detect malicious files and block them from executing.
- Host firewall: A program that ships as part of the operating system, or a program installed on the system.
  - MS Windows includes Windows Defender Firewall.
  - Apple macOS includes an application firewall.

According to the [Cost of a Data Breach Report 2021 by IBM Security](https://newsroom.ibm.com/2021-07-28-IBM-Report-Cost-of-a-Data-Breach-Hits-Record-High-During-Pandemic), a data breach in 2021 cost a company $4.24 million per incident on average, in comparison with $3.86 million in 2020. The average cost changes with the sector and the country. For example, the average total cost for a data breach was $9.23 million for the healthcare sector, while $3.79 million for the education sector.

## Methodology of Attack

Every 'operation' requires some form of planning to achieve success against a target.

According to Lockheed Martin, the Cyber Kill Chain has 7 steps:

![kill-chain](https://www.lockheedmartin.com/content/dam/lockheed-martin/rms/photo/cyber/THE-CYBER-KILL-CHAIN-body.png.pc-adaptive.1920.medium.png)

1. Recon: Short for reconnaissance, refers to where the attacker tries to learn as much as possible about the target. Information such as the types of servers, operating system, IP addresses, name of users, and email addresses.
2. Weaponization: Preparing a file with a malicious component, for example, to provide the attacker with remote access.
3. Delivery: Delivering the 'weaponized' file to the target via any method, such as email or USB flash memory.
4. Exploitation: When the user opens the malicious file, their system executes the malicious component.
5. Installation: The previous step should install the malware on the target system.
6. Command & Control (C2): The successful installation of the malware provides the attacker with a command and control ability over the target system.
7. Actions on Objectives: After gaining control over the target system, the attacker has achieved their objectives (stealing data).

