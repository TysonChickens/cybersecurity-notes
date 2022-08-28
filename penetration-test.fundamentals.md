---
id: bjsh4qgh9mn5m4y6pyinjce
title: Fundamentals
desc: ''
updated: 1658532149239
created: 1658363672548
---

# What is Penetration Testing?

The importance an relevancy of cybersecurity are increasing and be in every walk of life. Cybersecurity is relevant to all people in the modern world, including a strong password policy to protect emails or to businesses and other organizations needing to protect both devices and data from damages.

- A penetration test or pentest is ethically-driven attempt to test and analyze the security defenses to protect these assets and pieces of information. A penetration test involves using the same tools, techniques, and methodologies that someone with malicious intent would use and is similar to an audit.
- According to [Security Magazine](https://www.securitymagazine.com/articles/87787-hackers-attack-every-39-seconds), a cybersecurity industry magazine, there are over 2,200 cyber attacks every day - 1 attack every 39 seconds.

## Ethics

A penetration test is an **authorized audit** of a computer system's security and defenses as agreed by the owners of the systems. Anything that falls outside of the agreement is deemed unauthorized. Before a penetration test starts, a formal discussion occurs between the penetration tester and the system owner. The discussion forms the scope of the penetration testing agreement and will determine the course the penetration test takes.

Companies that provide penetration testing services are held against legal frameworks and industry accreditation. For example, the National Cyber Security Centre (NCSC) has the CHECK accreditation scheme in the UK. This check means that only _"CHECK approved companies can conduct authorized penetration tests of public sector and CNI systems and networks."_ (NCSC).

Penetration testers will often be faced with potentially morally questionable decisions during a penetration test. Ethics is the moral debate between right and wrong; where an action may be legal; it may go against an individual's belief system of right and wrong.

Hackers are sorted into three hats, where their ethics and motivations behind their actions determine what hat category they are placed into.


| Hat Category | Description                                                                                                    | Example                                                                         |
| ------------ | -------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| White Hat    | Considered 'good' people. They remain within the law and use their skills to benefit others.                   | Performing an authorized engagement on a company.                               |
| Grey Hat     | Use their skills to benefits others; they do not respect/follow the law or ethical standards at all times.     | Someone taking down a scamming site.                                            |
| Black Hat    | Criminals and often seek to damage organizations or gain some form of financial benefit at the cost of others. | Ransomware authors infect devices with malicious code and hold data for ransom. |

### Rules of Engagement (ROE)

The ROE is a document that is created at the initial stages of a penetration testing engagement - responsible for deciding how the engagement is carried out.


| Section    | Description                                                                                                                                                                            |
| ---------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Permission | Document gives explicit permission for the engagement to be carried out. This permission is essential to legally protect individuals and organizations for the activities carried out. |
| Test Scope | Annotate specific targets to which the engagement should apply. The test may only apply to certain servers or applications but not the entire network.                                 |
| Rules      | Define exactly the techniques that are permitted during the engagement. May specifically state that techniques such as phishing attacks are prohibited, but MITM attacks are okay.     |

## Penetration Testing Methodologies

Penetration tests can have a wide variety of objectives and targets within scope. No penetration test is the same, and there are no one-case fits all.

The steps a penetration tester takes during an engagement is known as the methodology. There are general theme of the following stages:

| Stage                 | Description                                                                                                                                          |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| Information Gathering | Involves collecting as much public accessible information about a target/organization as possible (Does not involve scanning any systems).           |
| Enumeration/Scanning  | Involves discovering applications and services running on the systems.                                                                               |
| Exploitation          | Leveraging vulnerabilities discovered on a system or application. This stage can involve the use of public exploits or exploiting application logic. |
| Privilege Escalation  | Once exploited, this stage is the attempt to expand your access to a system. Can escalate horizontally and vertically.                               |
| Post-exploitation     | What other hosts can be targeted, additional information can we gather from the host, covering tracks and reporting                                  |

![[penetration-test.pentest-forensics#pen-test-Methodologies]]


### OSSTMM

The [Open Source Security Testing Methodology Manual](https://www.isecom.org/OSSTMM.3.pdf) provides a detailed framework of testing strategies for systems, software, applications, communications and the human aspect of cybersecurity.

The methodology focuses primarily on how these systems, applications communicate, so it includes methodology for:

- Telecommunications (phones, VoIP, etc.)
- Wired networks
- Wireless communications

| Advantages                                                                                                                     | Disadvantages                                                                                 |
| ------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------- |
| Covers various testing strategies in-depth                                                                                     | The framework is difficult to understand, very detailed, and tends to use unique definitions. |
| Includes testing strategies for specific targets                                                                               |
| The framework is flexible depending upon the organization's needs.                                                             |
| A set of standard for systems and applications, meaning a universal methodology can be used in a penetration testing scenario. |

### OWASP

The "[Open Web Application Security Project"](https://owasp.org/) framework is a community-driven and frequently updated framework used solely to test the security of web applications and services.

- The foundation regularly writes reports stating the top ten security vulnerabilities a web application may have, the testing approach, and remediation.

| Advantages                                                                       | Disadvantages                                                                     |
| -------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| Easy to pick up and understand                                                   | May not be clear what type of vulnerability a web application has (often overlap) |
| Actively maintained and is frequently updated                                    | OWASP does not make suggestions to any specific software development life cycles  |
| It covers all stages of an engagement: from testing to reporting and remediation | The framework does not hold any accreditation such as CHECK                       |
| Specializes in web applications and services                                     |

### NIST Cybersecurity Framework 1.1

The NIST Cybersecurity Framework is a popular framework used to improve an organizations cybersecurity standards and manage the risk of cyber threats.

The framework provides guidelines on security controls & benchmarks for success for organizations from critical infrastructure (power plants, etc.) all through to commercial. There is a limited section on a standard guideline for the methodology a penetration tester should take.

| Advantages                                                                                                                | Disadvantages                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| The NIST Framework is estimated to be used by 50% of American organizations by 2020.                                      | NIST has many iterations of frameworks, so it may be difficult to decide which one applies to your organization. |
| The framework is extremely detailed in setting standards to help organizations mitigate the threat posed by cyber threats | The NIST framework has weak auditing policies, making it difficult to determine how a breach occurred.           |
| The framework is frequently updated                                                                                       | The framework does not consider cloud computing, which is quickly becoming increasing popular for organizations. |
| NIST provides accreditation for organizations that use this framework                                                     |
| NIST framework is designed to be implemented alongside other frameworks                                                   |

### NCSC CAF

The [Cyber Assessment Framework (CAF)](https://www.ncsc.gov.uk/collection/caf/caf-principles-and-guidance) is an extensive framework of fourteen principles used to assess the risk of cyber threats and an organization's defenses against these.

The framework applies to organizations considered to perform "vitally important services and activities" such as critical infrastructure, banking, and more. The framework mainly focuses on and assesses the following topics:

- Data security
- System security
- Identity and access control
- Resiliency
- Monitoring
- Response and recovery planning

| Advantages                                                 | Disadvantages                                                                               |
| ---------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| Backed by a government cybersecurity agency                | Still new in the industry - organizations have not made necessary changes suitable for it.  |
| Framework provides accreditation                           | Based on principles and ideas and is not as direct having rules like some other frameworks. |
| Covers 14 principles which range from security to response |

## Black box, White box, Grey box Penetration Testing

![[security.application#black-box-testing]]
![[security.application#white-box-testing]]
![[security.application#gray-box-testing]]