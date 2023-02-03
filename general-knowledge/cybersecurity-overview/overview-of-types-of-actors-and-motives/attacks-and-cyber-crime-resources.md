# Defense and Cyber Crime Resources

* [ ] Describe how host insertions are used to compromise a network.
* [ ] Describe what measures can be taken to protect against unauthorized insertion of a new host on your network.
* [ ] Describe Social Engineering and how it is used as an effective method of cyber exploitation.
* [ ] Describe what is meant by cyberwar and the online resources available to understand the global picture.
* [ ] Describe various resources available to you to help your organization protect itself against cyber-crime and cyber-criminals.

## Cyber Kill Chain

Cyber Kill Chain : A security model that outlines the phases of a cyberattack from Lockheed Martin.

* Military concept related to the structure of an attack. It consists of target identification, decision and order to attack the target, and finally the target destruction.

![Kill Chain](https://images.idgesg.net/images/article/2017/11/cyber-kill-chain-infographic-100741032-large.jpg)

The Cyber Kill Chain will help understand and protect against ransomware attacks, security breaches as well as Advanced Persistent Threats (APTs) - Ability to recognize the intrusion attempts and understand the intruder's goals and objectives.&#x20;

1. **Reconnaissance**: Research, identification, and selection of targets. The process of discovering and collecting information on the system and the victim to plan the attack. **OSINT** (Open-Source Intelligence) is the first step an attacker needs to complete and to study the victim by collecting every available piece of information on the company and its employees to determine the best attack.
   * [theHarvester](https://github.com/laramies/theHarvester) - other than gathering emails, this tool is also capable of gathering names, subdomains, IPs, and URLs using multiple public data sources.
   * [Hunter.io](https://hunter.io/) - this is  an email hunting tool that will let you obtain contact information associated with the domain.
   * [OSINT Framework](https://osintframework.com/) - OSINT Framework provides the collection of OSINT tools based on various categories.
2. **Weaponization**: After reconnaissance, combines malware and exploit into a deliverable payload. Most attackers usually use automated tools to generate the malware or refer the DarkWeb to purchase the malware. An example is pairing remote access malware with exploit into a deliverable payload such as macros (e.g Adobe PDF and Microsoft Office files).
   * Malware is a program or software designed to damage, disrupt, or gain unauthorized access to a computer.
   * An exploit is a program or code that takes advantage of the vulnerability or flaw in the application or system.
   * A payload is a malicious code that attackers runs on the system.
3. **Delivery**: Transmission of weapon to target (e.g via email attachments, websites, or USB drives).
4. **Exploitation**: Once delivered, the weapon's code is triggered, exploiting vulnerable applications or systems. After gaining access to the system, the malicious actor could exploit software, system, or server-based vulnerabilities to escalate the privileges or move laterally through the network. These are examples of how an attacker carries out exploitation:
   * The victim triggers the exploit by opening the email attachment or clicking on a malicious link.
   * Using a zero-day exploit.
   * Exploit software, hardware, or even human vulnerabilities.&#x20;
   * An attacker triggers the exploit for server-based vulnerabilities.&#x20;
5. **Installation**: The weapon installs a backdoor on a target's system allowing persistent access.
6. **Command & Control**: Outside server communicates with the weapons providing "hands on keyboard access" inside the target's network. The most common C2 channels used by adversaries nowadays:
   * The protocols HTTP on port 80 and HTTPS on port 443 - this type of beaconing blends the malicious traffic with the legitimate traffic and can help the attacker evade firewalls. &#x20;
   * DNS (Domain Name Server). The infected machine makes constant DNS requests to the DNS server that belongs to an attacker, this type of C2 communication is also known as DNS Tunneling.
7. **Actions on Objectives**: The attacker works to achieve the objective of the intrusion, which can include exfiltration or destruction of data, or intrusion of another target. With hands-on keyboard access, the attacker can achieve the following:&#x20;
   * Collect the credentials from users.
   * Perform privilege escalation (gaining elevated access like domain administrator access from a workstation by exploiting the misconfiguration).
   * Internal reconnaissance (for example, an attacker gets to interact with internal software to find its vulnerabilities).
   * Lateral movement through the company's environment.
   * Collect and exfiltrate sensitive data.
   * Deleting the backups and shadow copies. Shadow Copy is a Microsoft technology that can create backup copies, snapshots of computer files, or volumes.&#x20;
   * Overwrite or corrupt data.

## Social Engineering

The use of humans for cyber purposes.

* Communicate the with the intended victim to extract useful information for an attack.
* Attacker will attempt to manipulate to encourage the victim to give away sensitive information.

### Phishing and Vishing

* Vishing utilize voice communication conducted over voice and phone calls.
  * VoIP allows caller identity to be spoofed.
* Phishing attacks use email or malicious websites to impetrate personal information by acting as a trustworthy organization.

## Cyberwarfare

Cyberwarfare : Use of computer technology to disrupt the activities of a state or organization, especially the purpose attacking of information systems for strategic or military purposes.

[List of significant cyber incidents since 2006.](https://www.csis.org/programs/strategic-technologies-program/significant-cyber-incidents)

## Cyber-crime Resources

### Cyber-crime Reports

* [IBM X-Force](https://www.ibm.com/security/xforce) - Offensive and defensive security services threat intelligence platform has reports for organizations to stay ahead of evolving threats.

### Personalized Reports

* [X-Force Exchange](https://exchange.xforce.ibmcloud.com/) - IBM® X-Force Exchange is a cloud-based, threat intelligence sharing platform that you can use to rapidly research the latest global security threats, aggregate actionable intelligence, consult with experts and collaborate with peers. IBM X-Force Exchange, supported by human- and machine-generated intelligence, leverages the scale of IBM X-Force to help users stay ahead of emerging threats.
* [https://www.ibm.com/security/data-breach](https://www.ibm.com/security/data-breach) - Cost of a data breach reports for the year.

## X-Force Research

As threats multiply and increase in sophistication, it is more important than ever that organizations maintain awareness of current security trends.

IBM X-Force Threat Intelligence research reports can help you keep pace with an evolving threat landscape and learn how to protect your networks and data from the latest threats and attack vectors. Current reports are available for download, using the links below.

In 2018, many organizations across all industries faced unmanageable levels of cyber threats brought on by the changing threat landscape, the risk of exposure, and an ever-growing attack surface. The optimum strategy to respond to this combination of factors is to make security an integral part of culture and overall structure. To help organizations better prepare for this landscape, IBM® Security has developed the X-Force® Threat Intelligence Index 2019 report to provide insight on cybersecurity issues, including what the most common types of attacks are and where they come from.

The IBM X-Force Threat Intelligence Index 2019 examined numerous cyber threats that shaped the threat landscape in 2018 and will continue to have an impact in 2019. According to the report, cyber-criminals are moving away from malware-based attacks and instead abusing operating system tools to achieve their goals.

Download the full IBM X-Force Threat Intelligence Index 2019 to discover how to keep pace with the changing threat landscape and:

```
- Analyze top targeted industries and changes year over year

- Explore how cyber criminals are using operating system tools to get control

- Uncover why cyber criminals are changing their techniques to gain illegal profits

- Determine what steps you can take to protect your organization against these threats
```

IBM Security analyzes data and insight derived from monitored security clients, incident response services and penetration testing engagements. X-Force also runs spam traps around the world and monitors tens of millions of spam and phishing attacks daily. It analyzes billions of web pages and images to detect fraudulent activity and brand abuse

Download the 2019 X-Force Threat Intelligence Index 2019 if you have not already done so from the resource section of a previous lesson. Read the report and keep as a reference guide throughout your Cybersecurity training.

[https://www.ibm.com/security/data-breach/threat-intelligence](https://www.ibm.com/security/data-breach/threat-intelligence)

Download and read two industry reports that interest you from X-Force Research to understand the attack threats and recommended mitigation for that industry as found by the subject matter experts.

[https://www.ibm.com/security/data-breach/mss-security-threat-research](https://www.ibm.com/security/data-breach/mss-security-threat-research)
