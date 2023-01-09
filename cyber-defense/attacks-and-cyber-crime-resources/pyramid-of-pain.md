# Pyramid of Pain

<figure><img src="https://i.ibb.co/QYWXRSh/pop2.png" alt=""><figcaption></figcaption></figure>

### Hash Values (Trivial)

A hash value is a numeric value of a fixed length that uniquely identifies data from a hashing algorithm. The most common hashing algorithms:

* **MD5** (Message Digest, defined by [RFC 1321](https://www.ietf.org/rfc/rfc1321.txt))  - was designed by Ron Rivest in 1992 and is a widely used cryptographic hash function with 128-bit hash value. Not considered cryptographically secure due to a number of attacks against MD5 hashes, including hash collision.
* **SHA-1 (Secure Hash Algorithm 1,** defined by [RFC 3174](https://tools.ietf.org/html/rfc3174)) - Invented by the United States National Security Agency in 1995. SHA-1 takes an input and produces a 160-bit hash value string as a 40 digit hexadecimal number.
  * [NIST deprecated the use of SHA-1 in 2011](https://csrc.nist.gov/news/2017/research-results-on-sha-1-collisions) and banned its use for digital signatures at the end of 2013 being susceptible to brute-force attacks. NIST recommends to stronger hash algorithms such as SHA-2 and SHA-3 families.
* **SHA-2 (Secure Hash Algorithm 2)** - Designed by the National Institute of Standards and Technology (NIST) and the National Security Agency (NSA) in 2001 to replace SHA-1. The most common is SHA-256 algorithm that returns a hash value of 256-bits as a 64 digit hexadecimal number.

A hash is not considered to be secure if two files have the same hash value or digest. Security professionals use the hash value to gain insight into a specific malware sample, a malicious or a suspicious file, as a way to uniquely identify and reference the malicious artifact.

Various online tools can be used to do hash look-ups like [VirusTotal](https://www.virustotal.com/gui/) and [Metadefender Cloud - OPSWAT](https://metadefender.opswat.com/?lang=en).

## Pyramid of Pain

This concept is being applied to cybersecurity solutions like Cisco Security, SentinelOne, and SOCRadar to improve the effectiveness of CTI (Cyber Threat Intelligence), threat hunting, and incident response exercises.

### Hash Values (Trivial)

A hash value is a numeric value of a fixed length that uniquely identifies data from a hashing algorithm. The most common hashing algorithms:

* **MD5** (Message Digest, defined by [RFC 1321](https://www.ietf.org/rfc/rfc1321.txt))  - was designed by Ron Rivest in 1992 and is a widely used cryptographic hash function with 128-bit hash value. Not considered cryptographically secure due to a number of attacks against MD5 hashes, including hash collision.
* **SHA-1 (Secure Hash Algorithm 1,** defined by [RFC 3174](https://tools.ietf.org/html/rfc3174)) - Invented by the United States National Security Agency in 1995. SHA-1 takes an input and produces a 160-bit hash value string as a 40 digit hexadecimal number.
  * [NIST deprecated the use of SHA-1 in 2011](https://csrc.nist.gov/news/2017/research-results-on-sha-1-collisions) and banned its use for digital signatures at the end of 2013 being susceptible to brute-force attacks. NIST recommends to stronger hash algorithms such as SHA-2 and SHA-3 families.
* **SHA-2 (Secure Hash Algorithm 2)** - Designed by the National Institute of Standards and Technology (NIST) and the National Security Agency (NSA) in 2001 to replace SHA-1. The most common is SHA-256 algorithm that returns a hash value of 256-bits as a 64 digit hexadecimal number.

A hash is not considered to be secure if two files have the same hash value or digest. Security professionals use the hash value to gain insight into a specific malware sample, a malicious or a suspicious file, as a way to uniquely identify and reference the malicious artifact.

Various online tools can be used to do hash look-ups like [VirusTotal](https://www.virustotal.com/gui/) and [Metadefender Cloud - OPSWAT](https://metadefender.opswat.com/?lang=en).

### IP Address (Easy)

An IP address is used to identify any device connected to the network and rely to send and receive information over the network.

A common defense tactic is to block, drop, or deny inbound requests from IP addresses on the firewall. This tactic is not often not bulletproof as an adversary can use a new public IP address.

* Fast Flux is used, according to [Akamai](https://blogs.akamai.com/2017/10/digging-deeper-an-in-depth-analysis-of-a-fast-flux-network-part-one.html), Fast Flux is a DNS technique used by botnets to hide phishing, web proxying, malware delivery, and malware communication activities behind compromised hosts acting as proxies.

### Domain Names (Simple)

Domain names are a mapping an IP address to a string of text. A domain name can contain a top-level domain or sub-domain followed by a domain and top-level domain.

Attackers can purchase a domain, register it and modify DNS records. For defenders, many DNS providers have loose standards and provide APIs to make it easier for the attacker to change the domain.

Punycode attack used by the attackers to redirect users to a malicious domain that seems legitimate at first glance.

* As per [Wandera](https://www.wandera.com/punycode-attacks/), "Punycode is a way of converting words that cannot be written in ASCII, into a Unicode ASCII encoding."

To detect the malicious domains, proxy logs or web server logs can be used.

Malicious domains are usually hidden using URL shorteners. A URL shortener creates a short and unique URL that will redirect to the specific website specified during the initial setup of setting up the URL shortener link.&#x20;

Attackers use the following URL Shortening services to generate malicious links:&#x20;

* bit.ly
* goo.gl
* ow.ly
* s.id
* smarturl.it
* tiny.pl
* tinyurl.com
* x.co

### Host Artifacts (Annoying)

The attacker will feel a little more annoyed and frustrated if you can detect the attack. It will force the attacker to change is attack tools and methodologies.

Host artifacts are the traces that attackers leave on the system, such as registry values, suspicious process execution, attack patterns or IOCs (Indicators of Compromise), files dropped by malicious applications, or anything related to the current threat.

### Network Artifacts (Annoying)

If you can detect and respond to the threat, the attacker would need more time to go back and change their tactics or modify the tools, providing more time to respond and detect the upcoming threats.

Network artifact = User string C2 information, URI patterns followed by HTTP POST Requests.&#x20;

* Artifacts detected by Wireshark PCAPs by using a network protocol analyzer such as Tshark or explore IDS logging source such as Snort. The User-Agent defined by RFC 2616 as the request-header field contains information about the user originating request.

These are the most common User-Agent strings found for the [Emotet Downloader Trojan](https://www.mcafee.com/blogs/other-blogs/mcafee-labs/emotet-downloader-trojan-returns-in-force/).

### Tools (Challenging)

The attacker would most likely give up trying to break into network or build new tools that serves the same purpose.&#x20;

Attackers use utilities to create malicious documents (maldocs) for spear phishing attempts, backdoor to establish C2. any custom. EXE, DLL files, payloads, or password crackers.&#x20;

Antivirus signatures, detection rules, and YARA rules to use against attackers.

[MalwareBazaar ](https://bazaar.abuse.ch/)and [Malshare](https://malshare.com/) = Resources to samples, malicious feeds, and YARA rules.

* Helpful for threat hunting and incident response.

Detection rules -[ SOC Prime Threat Detection Marketplace](https://tdm.socprime.com/) are for professionals to share detection rules of CVE threats.&#x20;

Fuzzy Hashing helps perform similarity analysis - match two files with minor differences based on fuzzy hash values.

* SSDeep website for complete explanation for fuzzy hashing.

### TTPs (Tough)

• TTPs = Tactics, Techniques & Procedures. Includes the whole [MITRE ](https://attack.mitre.org/)[ATT\&CK Matrix](https://attack.mitre.org/) to achieve their goal.

Detect and respond to TTPs quickly leaves adversaries little chance to fight back.
