---
id: a5791pvdsfhjho9m09pm1a0
title: Concepts
desc: ''
updated: 1653055997250
created: 1653034586765
---

# Overview of Key Security Concepts

- [ ] Describe the CIA Triad and what is meant by confidentiality, integrity and availability in terms of cybersecurity.

---

## CIA Triad

![CIA](https://www.nissatech.com/wp-content/uploads/2017/05/Picture3.png)

### Confidentiality

Used to prevent any disclosure of data without prior authorization by the owner (privacy).

- Can force confidentiality with encryption.
- Elements such as authentication, access controls, physical security and permissions are normally used to enforce confidentiality.

### Integrity

Implemented to verify and validate if the information that we sent or received has not been modified by an unauthorized person of the system.

- Can implement technical controls such as mathematical algorithms or hashes (MD5, SHA1, etc.)

### Availability

The basic principle is to be sure that the information and data is always available when needed.

Technical implementations to make sure data is available:

- RAIDs
- Clusters
- ISP Redundancy
- Backups

## Non-Repudiation and CIA

Valid proof of the identity of the data sender or receiver is not altered.

Technical implementations:

- Digital signatures (on emails)
- Logs (email server)
