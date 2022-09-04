# Key Security Concepts and CIA

* [ ] Describe the CIA Triad and what is meant by confidentiality, integrity and availability in terms of cybersecurity.

## CIA Triad

![CIA](https://www.nissatech.com/wp-content/uploads/2017/05/Picture3.png)

### Confidentiality

Used to prevent any disclosure of data without prior authorization by the owner (privacy). Preserving unauthorized restriction on information access and disclosure, including means for protecting personal privacy and proprietary information.

* Loss of confidentiality is the unauthorized disclosure of information.
* Can force confidentiality with encryption.
* Elements such as authentication, access controls, physical security and permissions are normally used to enforce confidentiality.

### Integrity

Implemented to verify and validate if the information that we sent or received has not been modified by an unauthorized person of the system. Guarding against improper information modification or destruction, including ensuring information non-repudiation and authenticity.

* Integrity loss is the unauthorized modification or destruction of information.
* Can implement technical controls such as mathematical algorithms or hashes (MD5, SHA1, etc.)

### Availability

Timely and reliable access to information. The basic principle is to be sure that the information and data is always available when needed.

* Loss of availability is the disruption of access to an information system.

Technical implementations to make sure data is available:

* RAIDs
* Clusters
* ISP Redundancy
* Backups

## Non-Repudiation and CIA

Valid proof of the identity of the data sender or receiver is not altered.

Technical implementations:

* Digital signatures (on emails)
* Logs (email server)

### Authenticity and Accountability

**Authenticity:** Property of being genuine and verified.

**Accountability:** Mapping actions to an identity.
