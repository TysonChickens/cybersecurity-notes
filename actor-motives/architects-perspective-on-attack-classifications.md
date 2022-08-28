# Architect's Perspective on Attack Classifications

* [ ] Describe the various attack classifications such as passive attacks and active attacks.
* [ ] Discuss the various types of security services and the technical implementation of security policies.
* [ ] Discuss the various types of security services and the technical implementation of security policies.
* [ ] Identify and classify the various forms of active and passive attacks.

***

There are two major types of attacks:

**Passive Attacks** are essentially eavesdropping styles of attacks.

* Benefits is not easy detectable so eavesdropping could occur for a long time.
  * There is no evidence messages or evidence is being intercepted or changed.
* Second class is traffic analysis.

**Active Attacks** are explicit interception and modification. The attacker attempts to alter or control data and/or the hardware it resides on.

* Several classes of these attacks exist.
  * _Masquerade_ - Imitating someone else's identity and using legitimate sources to carry out attacks in the victim's name.
  * _Replay_ - Intercept communications and then fraudulently delays or resend it to misdirect the receiver into doing what the hacker wants.
  * _Modification_ - Tampering with the asset or message.
  * _Denial of Service_ - Deny users to access information systems, devices, or other network resources.

***

## Security Services

_Security services_:

* A processing or communication service that is provided by a system.
* To give a specific kind of protection to a system resource.
* Security services implement security policies.
* Are implemented by security mechanisms.

_The purpose of a security service_:

* Enhance security data processing systems and information transfer of an organization.
* Intended to counter security attacks.
* Using one or more security mechanisms.
* Often replicates functions normally associated with physical documents.
  * For example, have signatures, dates; need protection from disclosure, tampering, or destruction; be notarized or witnessed; be recorded or licensed.

### _International Telecommunication Union (United Nations to maintain international standards for telecommunication)_

#### **X.800**

A service provided by a protocol layer of communicating open systems, which ensures adequate security of the systems or of data transfers.

* **Authentication** - Assurance that communicating entity is the one claimed.
  * Have both peer-entity & data origin authentication.
* **Access Control** - Prevention of the unauthorized use of a resource.
* **Data Confidentiality** - Protection of data from unauthorized disclosure.
* **Data Integrity** - Assurance that received is as sent by an authorized entity.
* **Non-Repudiation** - Protection against denial by one of the parties in a communication.
* **Availability** - Resource accessible/usable.

#### **RFC 2828**

A processing or communication service provided by a system to give a specific kind of protection to system resources.

***

## Security Mechanisms

Security mechanisms are:

* Combination of hardware, software, and processes.
* They implement a specific security policy.
  * Protocol suppression, ID and authentication, for example.
* Mechanisms use security services to enforce security policy.
* Business policy describes what to going to do - Not how they are doing it.

Security mechanisms from X.800:

* **Specific** security mechanisms:
  * Cryptography
  * Digital signatures
  * Access controls
  * Data integrity
  * Authentication exchange
  * Traffic padding
  * Routing control
  * Notarization
* **Pervasive** security mechanisms:
  * Trusted functionality
  * Security labels
  * Event detection
  * Security audit trails
  * Security recovery

***

## Network Security Model

![Network Security Model](https://binaryterms.com/wp-content/uploads/2020/05/Network-Security-Model.jpg)

This model requires us to:

1. Design a suitable algorithm for the security transformation.
2. Generate the secret information (keys) used by the algorithm.
3. Develop methods to distribute and share the secret information.
4. Specify a protocol enabling the principals to use the transformation and secret information for a security service.

### X.800 A.2.2 and A.2.3 - Security Architecture and Motivation

A.2.2 : The motivation for security in open systems.

CCITT has identified a need for a series of Recommendations to enhance security within the Open Systems Interconnection architecture:

* Society's increasing dependence on computers that are accessed by, or linked by, data communications and which require protection against various threats.
* The appearance in several countries of "data protection" legislation which obliges suppliers to demonstrate system integrity and privacy.
* The wish of various organizations to use OSI recommendations, enhanced as needed, for existing and future secure systems.

A.2.3 : What is to be protected?

In general, the following may require protection:

* _Information_ and _data_ (including software and passive data related to security measures such as passwords).
* Communication and data processing _services_.
* _Equipment_ and _facilities_.

***

## Organizational Threats

Threats to a data communication system include the following:

* **Destruction** of information and/or other resources;
* **Corruption** or **modification** of information;
* **Theft**, **removal** or **loss** of information and/or other resources;
* **Disclosure** of information; and
* **Interruption** of services.

More on threats:

* **Accidental** threats do not involve malicious intent.
* **Intentional** threats require human with intent to violate security.
  * If an intentional threat results in action, it becomes an **attack**.
* **Passive** threats do not involve any (non-trivial) change to a system.
* **Active** threats involve some significant change to a system.

## Attacks

An attack is an action by a human with intent to violate security. It does not matter if the attack succeeds. It is still considered an attack even if it fails.

### 2 Forms of Passive Attacks

* **Disclosure** (release of message contents) : The content of a message is revealed to the unauthorized parties. An attack on the _confidentiality_ of a message.
* **Traffic analysis** (or traffic flow analysis). Even if an opponent cannot read the message content, information about the message may be useful information to the opponent. Also an attack on the _confidentiality_ of the message.

### 4 Forms of Passive Attacks

* **Masquerade** : An opponent impersonates a known or authorized person or system. This is an attack on the _authentication_ of the authorized entity's _identity_. An attack on the _authentication_ of the _origin_ of the message.

## Security Architecture Attacks

**Replay** : A copy of legitimate message is captured by an opponent and re-transmitted. This is an attack on the _integrity_ of the system's data.

**Modification** : The content of a legitimate message is altered. This is an attack on the _integrity_ of the message.

**Denial of Service (DoS)** : An opponent prevents authorized users from accessing a system. This is an attack on the _availability_ of the system.

***

### Security Architecture-Attack Models

Normally, information flows directly from the source to the destination.

* The information never arrives at the destination = _Active Attack (denial of service)_.
* The information arrives but an opponent obtains a copy = _Passive attack (disclosure)._
* An opponent intercepts the original message and forwards a modified version that appears to come from the original source = _Active attack (masquerade)._
* An opponent creates a message which appears to have come from the legitimate source = _Active attack (masquerade, denial of service)._
* The message never arrives at the destination but an opponent obtains a copy = _Active attack (denial of service)._
