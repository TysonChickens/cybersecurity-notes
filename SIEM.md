---
id: o9kgllk4dy29wx2figqoz1w
title: SIEM
desc: ''
updated: 1653197997879
created: 1653197985092
---

# SIEM Concepts

- [ ] Explore and understand the key terms of SIEM.
- [ ] Explore the role of a SIEM in the network.
- [ ] Understand the role of a SIEM in modern SOC.

- [ ] Explore different SIEM vendors and their components.

- [ ] Deep drive of QRadar from a Security Analysts point of view.

- [ ] Describe User Behavior Analytics (UBA) use cases.
---

## SIEM

SIEM (System Information Event Management)
: A data aggregator, search, and reporting system. SIEM gathers immense amounts of data from entire networked environment, consolidates and makes that data human accessible. With the data categorized and laid out, you can research data security breaches with as much detail as needed.

Key Terms:

- Log Collection
- Normalization
- Correlation
- Aggregation
- Reporting

1. A SIEM system collects logs and other security-related documentation for analysis.
2. The core function is to manage network security by monitoring flows and events.
3. It consolidates log events and network flow data from thousands of devices, endpoints and applications distributed throughout a network. It then uses an advanced Sense Analytics engine to normalize and correlate this data and identifies security offenses requiring investigation.
4. A SIEM system cane be ruled-based or employ a statistical correlation engine to establish relationships between event log entries.
5. Capture log event and network flow data in near real time and apply advanced analytics to reveal security offenses.
6. It can be available on premises and in a cloud environment.

### Events & Flows

Event
: Typically a log of a specific action such as a user login, or a FW permit, occurs at a specific time and the event is logged at that time.

Flows
: A record of network activity between two hosts that can last for seconds to days depending on the activity within the session.

- For example, a web request might download multiple files such as images, ads, video, and last for 5 to 10 seconds, or a user who watches a Netflix movie might be in a network session that last up to a few hours.

### Data Collection

Data Collection
: The process of collecting flows and logs from different sources into a common repository.

- It can be performed by sending data directly into the SIEM or an external device can collect log data from the source and move it into the SIEM system on demand or scheduled.
- Consider CPU, memory, storage capacity, license, and number of sources.

### Normalization

Normalization
: Process involves turning raw data into a format that has fields such as IP address that the SIEM can use.

- Normalization involves parsing raw event data and preparing the data to display readable information.
- Normalization allows for predictable and consistent storage for all records, and indexes those records for fast searching and sorting.

### License Throttling

License Throttling
: Monitors the number of incoming events to the system to mange input queues and EPS licensing.

### Coalescing

- Events are parsed and then coalesced based on common attributes across events.
  - QRadar: Event coalescing starts after three events have been found with matching properties within a 10 second period.
- Event data received by QRader is processed in to normalized fields, along with the original payload. Five properties are evaluated:
  - QID
  - Source IP
  - Destination IP
  - Destination port
  - Username

### Offenses

#### Event Correlation

- Logs
- IP Reputation
- Flows
- Geo Location

#### Activity Baseline & Anomaly Detection

- User Activity
- Database Activity
- Application Activity
- Network Activity

#### Offense Identification

- Credibility
- Severity

## SIEM Deployment

### Considerations

- Compliance
- Cost-Benefit
- Cybersecurity

### Events

Event Collector
: Collects event from local and remote log sources, and normalizes raw log source events to format for use by QRadar. The Event Collector bundles or coalesces identical events to conserve system usage and sends the data to the Event Processor.

- Can use bandwidth limiters and schedules to send events to the Event Processor to overcome WAN limitations such as intermittent connectivity.
- Bundles or coalesces identical events to conserve system usage and sends the data to the Event Processor.

Event Processor
: Processes events that are collected from one or more Event Collector components.

- Processes event by using the Custom Rules Engine (CRE).

### Flows

Flow Collector
: Generates flow data from raw packets that are collected from monitor ports such as SPANs, TAPs and monitor sessions, or from external flow sources such as netflow, sflow, jflow.

- Data is then converted to QRadar flow format and sent down the pipeline for processing.

#### Flow Processor

Flow De-duplication
: A process that removes duplicate flows when multiple Flow Collectors provide data to Flow Processors appliances.

Asymmetric Recombination
: Responsible for combining two sides of each flow when data is provided asymmetrically. This process can recognize flows from each side and combine them in to one record. However, sometimes only one side of the flow exists.

License Throttling
: Monitors the number of incoming flows to the system to manage input queues and licensing.

Forwarding
: Applies routing rules for the system, such as sending flow data to offsite targets, external Syslog systems, JSON systems, and other SIEMs.

### Reasons to Add Event or Flow Collectors to All-in-One Deployment

- Data collection requirements exceed the collection capability of processor.
- Must collect events and flows at a different location than processor is installed.
- Monitoring packet-based flow sources.
- As deployment grows, the workload exceeds the processing capacity of the All-in-One appliance.
- Security operations center employs more analysts who do more concurrent searches.
- The types of monitored data, and the retention period for that data increases, which increases processing and storage requirements.
- As security analyst team grows, requires better search performance.

### Security Operations Center (SOC)

Triad of security operations: People, Process and Technology

![SOC](https://lh3.googleusercontent.com/XkV9_pyKmRnuXUzAFDdFggJIad1YDxzfoVf9grhfqKJNXEDqMttRH0792TeKZjEyP0ZLK_WOz-r8kNrjUBCgv5s1JvnvhoQ-9rZ_rdjcHkUkpjGBAACeS928xGryEycAV9POW8f8l8Ub4iFAvQ)

## SIEM Solutions - Vendors

> The security information and event management (SIEM) market is defined by customers' need to analyze security event data in real time, which supports the early detection of attacks and breaches. SIEM systems collect, store, investigate, support mitigation and report on security data for incident response, forensics and regulatory compliance. The vendors included in this Magic Quadrant have products designed for this purpose, which they actively market and sell to the security buying center. 
- 2020 Garter.com Magic Quadrant Report

### Gartner's Magic Quadrant (2022)

![quad](https://aware-commons.s3.ap-south-1.amazonaws.com/static-files/sf-website/news/magic-quadrant-graph.png)

### Deployment

#### Small

Gartner defines a small deployment as one with around 300 log sources and about 1500 EPS (events per second).

#### Medium

A midsize deployment is considered to have up to 1000 log sources and 7000 EPS.

#### Large

A large deployment generally covers more than 1000 log sources with approximately 15000 EPS.

### Important Concepts

SIEM
: Combines security information (SIM) and security event management (SEM) to provide real-time analysis of security alerts generated by network hardware and applications.

Rule
: A programmed procedure that attempts to correlate events and generates new events that report on correlation when it occurs.

Rule Threshold
: The point at which a rule is triggered and a correlation event generated.

Event Threshold
: The number of times the event must occur before triggering the rule threshold.

Rule Action
: An automatic procedure that occurs when all rule conditions and threshold settings have been met.

Trend
: A resource that defines how and over what time period data will be aggregated and evaluated for trends. A trend executes a specified query on a defined schedule and time duration.

Event
: A log of a specific action such as a user login, or a FW permit, occurs at a specific time and the event is logged at that time.

Flow
: A record of network activity that can last for seconds, minutes, hours, or days, depending on the activity within the session.

Data Collection
: The process of collecting flows and logs from different sources into a common repository.

Normalization
: Involves turning raw data into a format that has fields such as an IP address that the SIEM can use.

Licensing Throttling
: Monitors the number of incoming events to the system to manage EPS and FPS licensing.

Coalescing
: Events are grouped based on common attributes.

### IBM QRadar

- Year 2004-205, Q1 Labs entered into the SIEm market modifying their NBAD platform (QFLOW) and in 2012, IBM bought them.
- Proprietary based on Ariel Data store and probably Ariel Query Language (AQL).
- Log correlation, Network Forensics, Intelligence Feeds, Vulnerability Management, Risk Manager.

#### Vulnerability Manager

- IBM® QRadar® Vulnerability Manager is a network scanning platform that detects vulnerabilities within the applications, systems, and devices on your network or within your DMZ.

- QRadar Vulnerability Manager uses security intelligence to help you manage and prioritize your network vulnerabilities. 
  - For example, you can use QRadar Vulnerability Manager to continuously monitor vulnerabilities, improve resource configuration, and identify software patches. You can also, prioritize security gaps by correlating vulnerability data with network flows, log data, firewall, and intrusion prevention system (IPS) data.

#### User Behavior Analytics


- IBM® QRadar® User Behavior Analytics (UBA) analyzes user activity to detect malicious insiders and determine if a user’s credentials have been compromised. Security analysts can easily see risky users, view their anomalous activities and drill down into the underlying log and flow data that contributed to a user’s risk score.

- As an integrated component of the QRadar Security Intelligence Platform, UBA leverages out of the box behavioral rules and machine learning (ML) models to add user context to network, log, vulnerability and threat data to more quickly and accurately detect attacks.

#### Network Insights

- Analyzes network data in real-time to uncover an attacker's footprints and expose hidden security threats in many scenarios before they can damage your organization, including:
  - Phishing e-mails
  - Malware
  - Data Exfiltration
  - Lateral movement
  - DNS and other application abuse
  - Compliance gaps

### ArcSight ESM

ArcSight ESM is a Security Information and Event Management (SIEM) solution that combines event correlation and security analytics to identify and prioritize threats in real-time and remediate incidents early. It is able to concentrate, normalize, analyze, and report the results of its analysis of security event data generated by various Intrusion Detection System (IDS) sensors and scanners in the operational environment. ArcSight ESM allows users to monitor events in real-time, correlate events.

- ArcSight Manager
- CORR-Engine (Correlation Optimized Retention and Retrieval Engine)
- ArcSight Console
- ArcSight Command Center (ACC)
- ESM Service Layer APIs


### Splunk

Splunk software has been around since 2006 and the company has since grown to become and industry leader. Splunk's vision is to make machine data accessible, usable and valuable to everybody. The company offers a wide range of products to turn machine data into valuable information by monitoring and analyzing all activities. This is known as Operational Intelligence and is the unique value proposition of Splunk.

- Splunk offers many free technology add-ons that provides real value immediately.
  - For example, the Distributed Management Console (DMC) helps pull all the Splunk architecture management together in one set of dashboards.

### LogRhythm's Security Intelligence Platform

- Platform Manager (PM) supports centralized management and administration for the LogRhythm implementation.
- Data Processor (DP) performs log collection and management.
- Data Indexer (DX) indexes data and metadata.
- AI Engine (AI) provides correlation and analysis capabilities.
- All-In-One (XM) combines the PM, DP, DX, and AI components.
- Network Monitor (NM) specializes in deep analysis of network traffic contents.
- Data Collector (DC) collects log data from remote systems and prepares it for secure transfer to the centralized LogRhythm Security Intelligence Platform implementation.

## QRadar SIEM - Industry Example

Automated threat detection and prioritization and securing the cloud.

- Real-time correlation and behavioral anomaly detection.
- Threat intelligence and vulnerability insight.
- Machine learning, service and user profiling.

### Solve Challenges

- Protect any critical data.
- Effectively respond to incidents.
- Prove compliance.

### Automate Intelligence

- Apply automated analytics to detect, connect, prioritize and investigate threats with IBM Watson.

### See Everything

- Collect data across the entire environment.

### Deployment Models

- On PREM
  - HW, SW, VM
- AS A SERVICE
  - SaaS, Managed Service
- CLOUD
  - AWS, Azure, Google Cloud
- HYBRID
  - On-prem, SaaS, IaaS

## User Behavior Analytics

### Security Ecosystem

Detecting insider threat requires a 360 degree view of both logs and flows.

- Threat Intel
- Network
- Cloud
- Identity & access
- Data
- Apps
- Mobile
- Endpoint

### Advantages of IBM QRadar UBA

- Complete visibility across end point, network and cloud infrastructure with both log and flow data.
- Avoids reloading and curating data faster time to insights, lowers operating cost, frees valuable resources.
- Out-of-the-box analytic models that leverage and extend the security operations platform.
- Single Security operation processes with integration of workflow system and other security solutions.
- Easily extend to third-party analytic models including existing insider threats use cases already implemented.
- Leverage UBA insights in other integrated security analytics solutions.
- Get more from QRadar ecosystem.

#### IBM QRadar UBA

160+ rule and ML driven use cases addressing 3 major insider vector threats.

- Compromised or stolen credentials.
- Careless or malicious insiders.
- Malware takeover of user accounts.

#### Into User Behavioral Analytics

Getting started with:

- Log sources input; parsing properly
- LDAP setup: reference maps
- User ID coalescing
- KYC & Align with Biz needs
- Config and tune UC

Analytic Outcomes

1. Focus on accounts and access.
   1. Account anomalies
   2. Access deviations
2. Expand to user views with network & session data.
   1. Surface abnormal user behavior
3. Build and compare to peer group
   1. Detect users deviating from self or from peer groups

Data Intelligence

- LDAP, AD, Authentication Logs
- Proxy, Firewall, Web GW, VPN, IPDS, Flow
- Endpoint, SaaS Apps, Cloud

#### Value to SOC

##### Analyst Effectiveness

- Detect known and unknown threats.
- Reduce time to detection.
- Identify activities of interest quickly.

##### Analyst Efficiency

- Expedite investigations.
- Reduce time to respond.
- Reduce deep data expertise.

##### ROI

- Get more from investments.
- Leverage existing QRadar skills.
- Available at no charge.

##### Time to Value

- Easy to acquire.
- Quick to deploy and configure.
- Easy to tune.