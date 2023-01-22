---
description: Adversary, Infrastructure, capability and victim
---

# Diamond Model

The Diamond Model of Intrusion Analysis was developed by cybersecurity professionals - Sergio Caltagirone, Andrew Pendergast, and Christopher Betz in 2013.

The four core features are edge connected representing their relationships in a shape of a diamond: adversary, infrastructure, capability, victim, and establishes the element of any intrusion activity.

* Can help explain to other people about what happened during an event or any valuable information on the malicious threat actor.

## Adversary

An adversary is known as an attacker, enemy, cyber threat actor, or hacker - the person who stands behind the cyberattack.

It is difficult to identify an adversary during the first stages of a cyberattack. We can utilize data collected from an incident or breach, signatures, and other relevant information can help determine who the adversary might be.

* **Adversary Operator** is the "hacker" or person(s) conducting the intrusion activity.
* **Adversary Customer** is the one to benefit from the activity conducted. It may be the same person who stands behind the adversary operator, or it may be a separate person or group.

## Victim

The victim is the target of the adversary. A victim can be an organization, person, target email address, IP address, domain ,etc. There is always a victim in every cyberattack.

**Victim Personae** are the people and organizations being targeted and whose assets are being attacked and exploited.

* Organization names
* People's names
* Industries
* Job roles
* Interests

**Victim Assets** are the attack surface and include the set of systems, networks, email addresses, hosts, IP addresses, social networking accounts where the adversary will direct their capabilities.

## Capability

Capability is also known as the skill, tools, and techniques used by the adversary - highlights TTPs. Includes all techniques used to attack the victims from less sophisticated methods to complicated methods.

**Capability Capacity** is all of the vulnerabilities and exposures that the individual capability can use.

**Adversary Arsenal** is a set of capabilities that belong to an adversary. An adversary must have the required capabilities that can be malware and phishing email development skills or access to malware or ransomware as a service.

## Infrastructure

Known as software or hardware can be physical or logical interconnections to deliver a capability or maintain control of capabilities.

The infrastructure can also be IP addresses, domain names, email addresses, or a malicious USB device found in the street.

**Type 1 Infrastructure** is controlled or owned by the adversary.

**Type 2 Infrastructure** is controlled by an intermediary. It has the purpose to obfuscate the source and attribution of the activity - Includes malware staging servers, malicious domain names, compromised email accounts, etc.

**Service Providers** are organizations that provide services considered critical for the adversary available of Type 1 and Type 2 infrastructures (ISPs, domain registrars, and webmail providers).

## Event Meta Features

Meta-Features are not required but add some valuable information or intelligence.&#x20;

**Timestamp**: Date and time for an event - Helpful to determine patterns & group the malicious activity.&#x20;

**Phase**: Phases of an intrusion, attack, or breach "Every malicious activity contains two or more phases which must be successfully executed in succession to achieve the desired result." - Diamond Model Creators & Axiom 4

**Results:** Event results can be "success", "failure! or "unknown! Can be related to the CIA being compromised&#x20;

* Also document all post-conditions resulting from the event.
* Important to capture results and post-conditions of adversary's operations.&#x20;

**Directions:** Describe host-based & network-based events represent the direction of the intrusion attack:&#x20;

* Victim-Infrastructure&#x20;
* Infrastructure-Victim
* Infrastructure-Infrastructure
* Adversary-Infrastructure
* Infrastructure- Adversary
* Bidirectional
* Unknown&#x20;

**Methodology**: Describe the general classification of intrusion. Examples:

* Phishing
* DDoS breach
* Port scan
* etc.&#x20;

**Resources**: Every event needs one or more external sources to be satisfied to succeed. Examples:&#x20;

* _Software_ - OS, virtualization software or Metasploit framework
* _Knowledge_ - How to use Metasploit to execute the attack and run&#x20;
* _Information_ - Username /Password&#x20;
* _Hardcore_ - servers workstations, routers&#x20;
* _Funds -_ Money to purchase tools/software&#x20;
* _Facilities_ - Electricity & shelter&#x20;
* _Access_ - Network path source host to victim/vice-versa or network from an ISP.

## Social - Political Component

Describes the needs and intent:&#x20;

* Financial Gain&#x20;
* Acceptance in the community&#x20;
* Hacktivism&#x20;
* Espionage

## Technology Component

Highlights the relationship between: capability & infrastructure.

* How the adversary operates & communicates.
  * Example of watering hole attack (methodology) and compromise legitimate websites targeted victims will visit.
