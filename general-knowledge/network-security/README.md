# Network Security and Traffic Analysis

A computer network is a group of computers and devices connected with each other. Network security focuses on protecting the security of these devices and the links connecting them. Traffic analysis or Network Traffic Analysis is a subdomain of the network security domain, its primary focus is to investigate the network data to identify problems and anomalies.

Network security consists of different hardware and software solutions to achieve the set of security goals for protecting data, applications, devices, and systems connected to the network. Hardware solutions refer to the devices you set up on a network to protect network security. Examples of hardware appliances:

* Firewall appliance: The firewall allows and blocks connections based on a predefined set of rules.
* Intrusion Detection System (IDS): Detects system and network intrusions and intrusion attempts to break into the network.
* Virtual Private Network (VPN): Ensures that the network traffic cannot be read nor altered by a third party. It protects the confidentiality (secrecy) and integrity of the sent data.

On the other hand, we have software security solutions:

* Antivirus software: Install on your computer or smartphone to detect malicious files and block them from executing.
* Host firewall: A program that ships as part of the operating system, or a program installed on the system.
  * MS Windows includes Windows Defender Firewall.
  * Apple macOS includes an application firewall.

According to the [Cost of a Data Breach Report 2021 by IBM Security](https://newsroom.ibm.com/2021-07-28-IBM-Report-Cost-of-a-Data-Breach-Hits-Record-High-During-Pandemic), a data breach in 2021 cost a company $4.24 million per incident on average, in comparison with $3.86 million in 2020. The average cost changes with the sector and the country. For example, the average total cost for a data breach was $9.23 million for the healthcare sector, while $3.79 million for the education sector.

## Network Security

Network security focuses on two core concepts: authentication and authorization. Network security operations contain three base control levels to ensure the maximum security management.

| Control Level      | Description                                                                                                 |
| ------------------ | ----------------------------------------------------------------------------------------------------------- |
| **Physical**       | Prevent unauthorized physical access to networking devices, cable boards, locks, and all linked components. |
| **Technical**      | Data security controls prevent access to network data like tunnels and implementing security layers.        |
| **Administrative** | Provide consistency in operations like creating policies, access levels and authentication processes.       |

The main approaches to network security operations:



| Access Control                                                          | Threat Control                                            |
| ----------------------------------------------------------------------- | --------------------------------------------------------- |
| Starting point for controls to ensure authentication and authorization. | Detecting/preventing malicious activities on the network. |

The key elements of Access Control:

| Access Controls                          | Description                                                                                                                                               |
| ---------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Firewall Protection**                  | Controls incoming and outgoing network traffic with predetermined security rules to block suspicious/malicious traffic while allowing legitimate traffic. |
| **Network Access Control (NAC)**         | Designed to verify device specifications and conditions are compliant before connecting to the network.                                                   |
| **Identity and Access Management (IAM)** | Control and manage the asset identity and user access to data systems and resources over the network.                                                     |
| **Load Balancing**                       | Control the resource usage to distribute (based on metrics) tasks over a set of resources and improve overall data flow.                                  |
| **Network Segmentation**                 | Creates and controls network ranges to isolate the users' access levels to improve the protection of internal devices/data in a safer network.            |
| **Virtual Private Networks (VPN)**       | Encrypted communication between devices (typically for secure remote access) over the network.                                                            |
| **Zero Trust Model**                     | Access and permissions at a minimum level to fulfill job responsibilities.                                                                                |

Key elements of Threat Control:

| Threat Controls                                               | Description                                                                                                                                                                                                                                          |
| ------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Intrusion Detection and Prevention (IDS/IPS)**              | Inspects traffic and creates alerts (IDS) or resets the connection (IPS) when detecting a threat.                                                                                                                                                    |
| **Data Loss Prevention (DLP)**                                | Inspects traffic (content inspection and contextual analysis) and blocks the extraction of sensitive data.                                                                                                                                           |
| **Endpoint Protection**                                       | Protect all kinds of endpoints and devices that connect to the network with multi-layer approach.                                                                                                                                                    |
| **Cloud Security**                                            | Protect cloud from threats and data by applying countermeasures like data encryption or a VPN.                                                                                                                                                       |
| **Security Information and Event Management (SIEM)**          | Tool to help find threats, compliance, and security incident-management, through available data logs and statistics by event and context analysis.                                                                                                   |
| **Security Orchestration Automation and Response (SOAR)**     | Tool to help coordinate and automate tasks between various people, tools, and data within a single platform to identify anomalies, threats, and vulnerabilities. Also supports vulnerability management, incident response, and security operations. |
| **Network Traffic Analysis & Network Detection and Response** | Inspect network traffic or traffic capture to identify anomalies and threats.                                                                                                                                                                        |

Typical network security management operation:

| Deployment                                                                                          | Configuration                                                                        | Management                                                                                                    | Monitoring                                                                                                                                  | Maintenance                                                                                                                           |
| --------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| <ul><li>Device and software installation</li><li>Initial configuration</li><li>Automation</li></ul> | <ul><li>Feature configuration</li><li>Initial network access configuration</li></ul> | <ul><li>Security policy implementation</li><li>NAT and VPN implementation</li><li>Threat mitigation</li></ul> | <ul><li>System monitoring</li><li>User activity monitoring</li><li>Threat monitoring<br></li><li>Log and traffic sample capturing</li></ul> | <ul><li>Upgrades</li><li>Security updates</li><li>Rule adjustments</li><li>License management</li><li>Configuration updates</li></ul> |

## Managed Security Services

Not every organization has enough resources to dedicate groups for specific security domains. Managed Security Services (MSS) fulfil the required effort to meet security needs.

* These are services have been outsourced to service providers callled Managed Security Service Providers (MSSPs).
* Most are time and cost effective.

| Network Penetration Testing  | Assessing network security by simulating external/internal attacker techniques to breach the network.                                                                                    |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Vulnerability Assessment     | Assessing network security by discovering and analyzing vulnerabilities in the environment.                                                                                              |
| <p>Incident Response<br></p> | An organized approach to addressing and managing a security breach. It contains a set of actions to identify, contain, and eliminate incidents.                                          |
| Behavioral Analysis          | An organized approach to addressing system and user behaviors, creating baselines and traffic profiles for specific patterns to detect anomalies, threats, vulnerabilities, and attacks. |

## Traffic/Network Analysis

Traffic analysis is a method of intercepting, recording/monitoring, and analyzing network data and communication patterns to detect and respond to anomalies and threats. There are two main techniques used in Traffic Analysis:

| Flow Analysis                                                                                                                                        | Packet Analysis                                                                                                 |
| ---------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| Collect data/evidence from network devices to provide statistical results through data summary without applying detailed packet-level investigation. | Collect all available network data to apply Deep Packet Inspection (DPI) to detect and block malicious packets. |
| Easy to collect and analyze                                                                                                                          | Provides full packet details to find the root cause.                                                            |
| Does not provide full packet details for the root cause.                                                                                             | Requires time and skill to analyze.                                                                             |

* Provides full network visibility.
* Helps comprehensive baseline for asset tracking.
* Helps to detect/respond to anomalies and threats.
