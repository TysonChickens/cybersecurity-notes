# Unified Kill Chain

The [Unified Kill Chain](https://www.unifiedkillchain.com/assets/The-Unified-Kill-Chain.pdf) published in 2017 aims to complement with other cybersecurity kill chain frameworks such as MITRE's ATT\&CK.

The UKC has 18 phases - modern and extremely detailed compared to traditional security kill chain frameworks:

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/6cdfd3aba41ee1b942b5a1537a1dc1ad.png" alt=""><figcaption></figcaption></figure>

| <p>Modern (released in 2017, updated in 2022).<br></p>                                                                                                                                                           | <p>Some frameworks, such as MITRE’s were released in 2013, when the cybersecurity landscape was very different.<br></p>           |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| <p>The UKC is extremely detailed (18 phases).<br></p>                                                                                                                                                            | <p>Other frameworks often have a small handful of phases.<br></p>                                                                 |
| <p>The UKC covers an entire attack - from reconnaissance, exploitation, post-exploitation and includes identifying an attacker's motivation.<br></p>                                                             | <p>Other frameworks cover a limited amount of phases.<br></p>                                                                     |
| <p>The UKC highlights a much more realistic attack scenario. Various stages will often re-occur. For example, after exploiting a machine, an attacker will begin reconnaissance to pivot another system.<br></p> | Other frameworks do not account for the fact that an attacker will go back and forth between the various phases during an attack. |

## Phase: In (Initial Foothold)

The main focus for this phase is a series of actions for an attacker to gain access to a system or network environment.

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/7b2d991f38d302d49b0d1898448e2be8.png" alt=""><figcaption></figcaption></figure>

### Reconnaissance ([MITRE Tactic TA0043](https://attack.mitre.org/tactics/TA0001/))

Describes techniques where an adversary gathers information relating to their target through active and passive reconnaissance.

Information gathered from this phase can include:

* Discovering what systems and services are running on the target.
* Finding contact lists or lists of employees that can be impersonated or used in either a social engineering or phishing attack.
* Looking for potential credentials that may be useful in later stages, such as pivoting or initial access.
* Understanding the network topology and other networked systems to pivot.

### Weaponization ([MITRE Tactic TA0001](https://attack.mitre.org/tactics/TA0001/))

Setting up the necessary infrastructure to perform the attack. An example could be setting up a command and control server, or a system capable of catching reverse shells and delivering payloads to the system.

### Social Engineering ([MITRE Tactic TA0001](https://attack.mitre.org/tactics/TA0001/))

Manipulate employees to perform actions that will aid in the adversaries attack.

* Getting a user to open a malicious document.
* Impersonating a web page and having the user enter their credentials.
* Calling or visiting the target and impersonating a user, or being able to gain access to areas of a site.

### Exploitation ([MITRE Tactic TA0002](https://attack.mitre.org/tactics/TA0002/))

How an attacker takes advantage of weaknesses or vulnerabilities present in a system. The UKC defines "Exploitation" as abuse of vulnerabilities to perform code execution.

* Uploading and executing a reverse shell to a web application.
* Interfering with an automated script on the system to execute code.
* Abusing a web application vulnerability to execute code.

### Persistence ([MITRE Tactic TA0003](https://attack.mitre.org/tactics/TA0002/))

Describes the techniques to maintain access to a system have gained access to.

* Creating a service on the target system that will allow the attacker to regain access.
* Adding the target system to a Command & Control server where commands can be executed remotely.
* Leaving other forms of backdoors to execute when a certain action occurs on the system.

### Defense Evasion ([MITRE Tactic TA0005](https://attack.mitre.org/tactics/TA0005/))

Understand techniques to evade defense measures place in the system or network.

* Web application firewalls
* Network firewalls
* Anti-virus systems on the target machine
* Intrusion detection systems

Helpful to analyze attacks to form better defense systems.

### Command & Control ([MITRE Tactic TA0011](https://attack.mitre.org/tactics/TA0011/))

Combines the efforts of an adversary made during the "weaponization" stage of the UKC to establish communications between the adversary and target system. An adversary can establish command and control of a target system to achieve action on its objectives.

* Execute commands
* Steal data, credentials, and other information
* Use the controlled server to pivot to another system on the network

### Pivoting ([MITRE Tactic TA0008](https://attack.mitre.org/tactics/TA0008/))

Reach other systems within a network that are not accessible or exposed to the internet. There are many systems in a network that are not directly reachable and often contain valuable data or have weaker security.

## Phase: Through (Network)

After a successful foothold being established on the network, look to gain additional access and privileges to systems and data to fulfill their goals.

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/5262ff6852376b58e4b82ffdaa70b3e1.png" alt=""><figcaption></figcaption></figure>

### Pivoting ([MITRE Tactic TA0008](https://attack.mitre.org/tactics/TA0008/))

Once the attacker has access to the system, it will be used as a staging site and a tunnel to the victim's network.

### **Discovery (**[**MITRE Tactic TA0007**](https://attack.mitre.org/tactics/TA0007/)**)**

Uncover information about the system and the network it is connected to. This stage, the knowledge base would be built from the active user accounts, the permissions granted, applications and software in use, web browser activity, files, directories and network shares, including system configurations.

### **Privilege Escalation (**[**MITRE Tactic TA0004**](https://attack.mitre.org/tactics/TA0004/)**)**

Leverage the information on the account present with vulnerabilities and misconfigurations found to elevate their access to one of the following superior levels:

* SYSTEM/ROOT
* Local Administrator
* A user account with admin-like access
* A user account with specific access or functions

### **Execution (**[**MITRE Tactic TA0002**](https://attack.mitre.org/tactics/TA0002/)**)**

The system would be used as the distribution point for all malware and backdoors once the attacker has access to the system. This stage would deploy malicious code to pivot system as their host - Remote Trojans, C2 scripts, malicious links and scheduled tasks are deployed and created to facilitate a presence on the system and upload their persistence.

### **Credential Access (**[**MITRE Tactic TA0006**](https://attack.mitre.org/tactics/TA0006/)**)**

Alongside the Privilege Escalation stage, the adversary would attempt to steal account names and passwords through various methods, such as keylogging and credential dumping.

### **Lateral Movement** ([MITRE Tactic TA0008](https://attack.mitre.org/tactics/TA0008/))

With the credentials and elevated privileges, seek to move through the network and jump onto other targeted systems to achieve their primary objective.

## Phase: Out (Action on Objectives)

These goals are usually geared toward compromising the confidentiality, integrity and availability (CIA) triad.

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/c7914400ef9c65e2d1d1cc9b27ffdcc3.png" alt=""><figcaption></figcaption></figure>

### **Collection MITRE Tactic (TA0009)**

After all the hunting for access and assets, seek to gather all the valuable data of interest - Compromises the confidentiality of the data. The main target sources includes drives, browsers, audio, video and email.

### **Exfiltration (**[**MITRE Tactic TA0010**](https://attack.mitre.org/tactics/TA0010/)**)**

To elevate compromise, seek to steal data using encryption measures and compression to avoid any detection.

### **Impact (**[**MITRE Tactic TA0040**](https://attack.mitre.org/tactics/TA0040/)**)**

To compromise the integrity and availability of the data assets, one would manipulate, interrupt or destroy these assets. The goal would to disrupt business and operational processes.

* Remove account access
* Disk wipes
* Data encryption such as ransomware
* Defacement
* Denial of Service (DoS) attacks

### **Objectives**

With access to the systems and networks, seek to achieve their strategic goal for the attack.

* Encrypt files and systems with ransomware for financial gain.
* Seek to damage business reputation to release private and confidential information to the public.
