---
id: 1mkrfedhrewayxy0j3hs899
title: AAA
desc: ''
updated: 1653097621095
created: 1653097334047
---

# Authentication and Access Control

- [ ] Discuss the terms Identification and AA in the context of cybersecurity.
- [ ] Discuss the 3 types of Authentication and the use of controls.

- [ ] Discuss the major Access Control methods, including MAC, DAC, RBAC and other methods such as Centralized and Decentralized
- [ ] Discuss Access Control best practices such as Least Privilege, Separation of Duties and Rotation of Duties.

- [ ] Discuss various common physical access control methods.
- [ ] Discuss various common logical access control methods.
- [ ] Discuss monitoring and access control processes such as IDS, IPS, Host IDS and IPS, HoneyPot and Sniffers.

---

## Authentication and AAA

![Identification](https://www.researchgate.net/profile/Hosam_Alamleh/publication/341297307/figure/download/fig2/AS:890081132965894@1589223287448/3-Identification-authentication-and-authorization-in-the-proposed-LBAC.png)

1. Identification
2. Authentication
3. Authorization
   - Resource
4. Accountability

## Authentication Methods

- Something you know (username/password)
- Something you have (smart-card, token)
- Something you are (fingerprints, biometric signatures, retina scanners)
  - Most secure authentication methods.

## Controls

### Types

Administrative
: Security awareness education, security framework compliance training, and incident response plans and procedures in place.

Technical
: Common controls such as multi-factor user authentication at login, and also granting internal access to a system on a need-to-know basis.

Physical
: Restrictions on physical access such as security guards at building entrances, locks, close circuit cameras, and perimeter fences.

#### Each Control Type

Corrective
: Use backups after a cybersecurity incident to minimize data loss and damage to information systems; and to restore information systems as quickly as possible.

Preventive
: Address weaknesses in information systems identified by risk management team before a cybersecurity incident.

Detective
: Detect unauthorized activity or security incidents such as alerts.

Compensatory
: Safeguard or countermeasure employed in the low, moderate, or high baselines that provides equivalent or comparable protection for an information systems.

---

## Access Control Methods

Only who has the rights to access or utilize the resource can use them.

### MAC - Mandatory Access Control

- Constrains the ability of a subject or initiator to access or generally perform some sort of operation on an object or target.
- Use labels to regulate the access.
- Military use.

### DAC - Discretionary Access Control

- Each object (folder or file) has an owner and the owner defines the rights and privilege.

### Role Based Access Control

The rights are configured based on the user roles.

- Separate roles for sales group, management group, etc.

### Centralized

- SSO (Single Sign On)
- Provide the 3 A's
- Unified system for all locations.

### Decentralized

- Independent access control methods
- Local power
- Normally the military forces the use of these methods on the battle fields.
- Multiple support desks, departments and locations to support.

## Best Practices for Access Control Field

These concepts are deeply integrated with the access control methodologies and must be followed by the organization in order of the policies and procedures.

### Least Privilege

- Information access limit.

### Separation of Duties

- Verify employee activity.

### Rotation of Duties

- Tracking and control.

---

## Physical and Logical

### Physical Methods

- Perimeters / Barriers
- Building
- Work areas
- Server and networks

#### Technical use Physical Security Controls

- ID badges
- List and logs
- Door access and control systems
- Tokens
- Proximity sensors
- Tramps
- Physical block
- Cameras

### Logical Methods

- ACL (Routers)
- GPO's
  - Password policies
  - Device policies
  - Day and time restrictions
- Accounts
  - Centralized
  - Decentralized
  - Expiration
- BYOD (Bring Your Own Device)
  - Popular concept modern times for individuals has opportunity to bring their own device to the work environment.
    - Strict policy and understanding.
    - Use of technical control MDM.
    - Training
    - Strong perimeter controls.

#### Monitoring Access Control

IDS - Intrusion Detection System
: Network security technology for detecting vulnerability exploits against a target or computer.

IPS - Intrusion Prevention System
: Works to detect and prevent identified threats by continuously monitoring system networks, looking for possible malicious incidents and capturing information.

HOST IDS and IPS
: Host-based systems that can monitor the host for unexpected behavior or drastic changes from their baseline.

HoneyPot
: Security tool to lure attackers away from the action network where they can be monitored safely. Can be software or malicious programs, hardware decoys, or entire domain works (HoneyNets).

Sniffers
: Device known as packet analyzers that can monitor network communications either on the wire or on the wireless network.

