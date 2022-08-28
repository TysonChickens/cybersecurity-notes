---
id: wcuptt9dpzdx06nt9l6myuv
title: Data Security
desc: ''
updated: 1653180786193
created: 1653180766235
---

# Data Security and Protection

- [ ] Describe the importance of data security and protection.

- [ ] Understand the Data Security top challenges.
- [ ] Understand common pitfalls.
- [ ] Describe the unique challenges for the following industries
  - [ ] Healthcare
  - [ ] Transportation
  - [ ] Financial Markets
  - [ ] Retail

- [ ] Discuss the Critical Data Protection capabilities.

- [ ] Understand the features of Guardium as an example of Data Protection solution.
- [ ] Describe the features of IBM Security Guardium Data Encryption.
- [ ] Describe the features of IBM Security Key Lifecycle Manager.
- [ ] View the Guardium portion of the IBM Security Learning Academy.

- [ ] Learn about the 2 major mobile operating systems and their differences.
- [ ] Understand the primary vulnerabilities, weak points, and back doors.
- [ ] Learn about security options available for mobile devices.
- [ ] Understand what mobile endpoint management entails day-to-day.

---

Data Security
: Data security is the process of protecting your most critical business assets, that is your data, against unauthorized or unwanted use.

Protecting:

- Confidentiality
- Integrity
- Availability

Protecting of data:

- In transit
- At rest
  - Databases
  - Unstructured data (files)
  - On endpoints

Data must be protected against deliberate and inadvertent or accidental attacks.

Deliberate:
- Hackers
- Denial of Service
  
Accidental:
- Operator error
- Natural disaster
- Component failure

## Data Security Top Challenges

- Explosive data growth.
  - Variety of data will need be protected.
- New privacy regulations.
  - Different areas and countries have different regulations.
- Operational complexity.
  - Moving to the cloud provides more stability and vulnerabilities.
  - Implementation of security strategies.
  - Resource intensive projects.
- Cybersecurity skills shortage.
  - Need more professional and people skills for cybersecurity.

### Data Security Common Pitfalls

- Failure to move beyond compliance.
  - Must stay ahead of the game and be proactive on threats.
- Failure to recognize the need for centralized data security.
  - Requires a dedicated team for cybersecurity strategies.
- Failure to define who owns responsibility for the data itself.
  - Specific person to protect data.
- Failure to address known vulnerabilities.
  - Vast majority of exploits use known vulnerabilities at least 6 months old.
- Failure to prioritize and leverage data activity monitoring.
  - Put measures in place to monitor privileged users, suspicious activities, and outliers.

### Healthcare

- Process and store combination of personal health information and payment card data.
- Subject to strict data privacy regulations such as HIPAA.
- May also be subject to financial standards and regulations.
- Highest cost per breach record.
- Data security critical for both business and regulatory compliance.

### Transportation

- A critical part of national infrastructure.
- Combines financially sensitive information and personal identification information
- Relies on distributed IT infrastructure and third party vendors.

### Financial and Insurance

- Most targeted industry: 19% of cyberattacks in 2018.
- Strong financial motivation for both external and internal attacks.
- Numerous industry-specific regulations require complex compliance measures.
  - FINRA
  - SOX
  - Basel framework for banks

### Retail

- Among most highly targeted groups for data breaches.
- Large number of access points in retail data lifecycle.
- Customers and associate access and share sensitive data in physical outlets, online, and mobile applications.

### Top 12 Critical Data Protection Capabilities of Data Protection

#### Data Discovery

- Determine where data resides and discover databases or file sources in your network that potentially contain sensitive or regulated data.
- To protect data, must know where data lives.

#### Data Classification

- Parse discovered data sources to determine the kind of data they contain, matching against a predefined set of patterns or keywords.
- Assign labels based on the data type to inform policies.
- Allows to determine what protective measures are necessary.
- Data may fall under multiple classifications.
- Standards and regulations (SOX, HIPAA, PCI, and so on) define classifications for data.

#### Vulnerability Assessment

- Scan data environments to detect vulnerabilities and exposures.
  - Missing patches.
  - Weak passwords.
  - Unauthorized access and changes.
  - Misconfigured privileges.
  - Account sharing.
  - Other behavioral vulnerabilities.
- Iterative process.
- Requires coordination across, centralized effort.

#### Data Risk Analysis

- Identify data sources with the greatest risk of exposure or audit failure and help security professionals prioritize where to focus first.
- Build on classification and vulnerability assessment.

#### Data and File Activity Monitoring

- Capture and record real-time data access activity, with visibility into transactions for platforms and protocols by users including database admins, developers, outsourced personnel and applications.
- Centralized policies.
- Resource intensive: Scanning many transactions for small number of suspicious transactions.

#### Real-time Alerting

- Detect abnormal activity to identify risk around sensitive data access, privileged user actions, change control, application user activities and security exceptions.

#### Blocking, Masking, and Quarantining

- Obscure data and/or blocking further action by risky users when activities deviate from regular baselines or pre-defined policies.
- Provide only level of access to data necessary.

#### Encryption

- Render sensitive data useless to cyber-criminals, unauthorized employees, and third-party service providers by encoding it in such a way that only authorized individuals can read it by decrypting the encoded data with a key.
- Protect data at rest and in transit.

#### Tokenization

- A special type format-preserving encryption that substitutes sensitive data with a token, which can be mapped to the original value.

![tokenization](http://cdn.differencebetween.net/wp-content/uploads/2020/11/Difference-Between-Tokenization-and-Masking.png)

#### Key Management

- Securely distribute keys across complex encryption landscape.
- Centralized key management.
- Enable organized, secure key management that keeps data private and compliant.

#### Automated Compliance Support

- Pre-built capabilities mapped to specific regulations such as GDPR, HIPAA, PCI-DSS, CCPA and so on.
  - Audit workflows to streamline approval processes.
  - Out-of-the-box reports.
  - Pre-built classification patterns for regulated data.
  - Tamper-proof audit repository.

### Data Protection Example

IBM Guardium supports data protection:

- Comprehensive data protection - Dynamic blocking, alerting, quarantine, encryption, and integration with security intelligence.
- Sensitive data recovery - Perform vulnerability assessment, discovery, and classification.
- Address data privacy - Find and address personally identifiable information (PII), determine who is reading data, leverage masking.
- Expand platform coverage - Big data platforms, file systems, or other platforms also require monitoring, blocking, reporting.
- Acute compliance need - Database monitoring focused on changed data and automated reporting.

Allows to protect all data against unauthorized access and to enable organizations to comply with government regulations and industry standards.

1. Prevent data breaches - Prevent disclosure or leakages of sensitive data.
2. Ensure data privacy - Prevent unauthorized changes to data.
3. Reduce the cost of compliance - Automate and centralize controls across diverse regulations and heterogenous environments.
4. Identify risk - Discover sensitive information, identify dormant data, assess configuration gaps and vulnerabilities.

Guardium provides a complete monitoring solution.

- Minimal resource utilization (3 to 5% CPU utilization).
- DBAs have no access to Guardium, unless provided by a Guardium administrator.
- Collects database traffic from heterogenous environments and standardizes it, allowing one system to monitor multiple database types.
- External agent for monitoring cloud-based databases as services, running on Kubernetes.

IBM Security Guardium Data Encryption integrates a suite of highly-scalable products built on a common infrastructure.

- Provide encryption, tokenization and key management capabilities.
- Secure assets residing in cloud, virtual, big data and on-premise environments.
- Address compliance with government and industry regulations, including GDPR, CCPA, PCI-DSS and HIPAA.

Security key lifecycle manager centralizes, simplifies and automates the encryption key management process.

- Secure, robust key storage.
- Key serving and key lifecycle management for IBM and non-IBM storage solutions.
- Uses OASIS Key Management Interoperability Protocol (KMIP)
- Helps meet regulations such as PCI DSS, Sarbanes-Oxley, HIPAA.

## Mobile Endpoint Protection

Android and iOS are two major mobile operating systems.

**Android**

- Android Inc. was a small team working on an alternative to Symbian and Windows Mobile OS.
- Purchased by Google in 2005 - the Linux kernel became the base of the Android OS. Now developed primarily by Google and a consortium known as Open Handset Alliance.
- First public release in 2008 - Currently on version 10.
- ~86% of smartphones and ~39% of tablets run some form of Android.
- MDM capabilities since Android 2.2.

**iOS**

- Developed by Apple exclusively for their products.
- Launched in 2007 - Currently on version 15.
- Despite early proliferation and pop culture appeal, Apple smartphones only make up about 13% of devices (based on usage).
- ~60% of tablets worldwide run iOS/iPadOS.
- MDM Capabilities available since iOS 6.

### How Mobile Endpoints Differ from Traditional Endpoints

- Users do not interface directly with the OS.
- A series of applications act as a broker between the user and the OS.
- OS stability can be easily monitored and any anomalies reported that present risk.
- Anti-virus software can "see" the apps that are installed on a device, and read certain signatures, but can not peek inside at their contents.

### Primary Threats to Mobile Endpoints

#### System-Based

- Jail-breaking and rooting exploit vulnerabilities to provide root access to the system.
- Systems that were previously read-only can be altered in malicious ways.
- One primary function is gain access to apps that are not approved or bootleg.
- Vulnerabilities and exploits in the core code can open devices to remove attacks that provide root access.

#### App-Based Threats

- Primarily comes in the form of Phishing scams - via SMS or Email.
- Malicious code can infect even public apps. Be wary of granted apps access to sensitive data.
- Apps may request access to hardware features irrelevant to their functionality.
- Web content in mobile browsers, especially those that prompt for app installations, can be the root cause of many attacks.

### External

- Network-based attacks may collect sensitive data.
- Vulnerabilities can be exploited by tethering devices to external media.
- Social engineering is often used to gain unauthorized access to mobile devices.

### Protecting Mobile Assets

#### MDM

Control the content allowed on devices and restrict access to extraneous, potentially hazardous features. Lock devices down so they are inaccessible if lost or stolen.

- Mobile devices require constant monitoring as they are generally in use all day long.

#### App Security

Report on the health and reliability of applications, often times before they even make it on to devices.

- Any number of systems can be used to monitor as much or as little information as possible.

#### User Training

Educating users on the threats that can impact them is the number one line of defense. This is important for BYOD scenarios where prohibitive management isn't possible.

- Many times there will be gaps that can not be addressed due to system limitations (monitoring iCloud messages, for example).

### Day-to-Day Operations

- Monitor device OS versions
- Monitor app installs and versions
- Monitor and enforce encryption
- Distribute secure payloads
- Automate compliance actions
- Ensure proper NAC policies are enforced
- Educate users regularly
- Update contingency plans

