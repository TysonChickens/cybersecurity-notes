---
id: 8ykaxd1qjsjfi1c6zsfq1eq
title: Cryptography Encryption
desc: ''
updated: 1653131984950
created: 1653131979939
---

# Introduction to Cryptography

- [ ] Define cryptography and encryption.
- [ ] Describe the related Open Web Application Security Project (OWASP) Top 10 project and SANS Institute Top 25 cryptographic weaknesses.
- Describe encryption and common types of encryption algorithms.
- Define cryptographic terms including hash function and digital signatures.

- [ ] Describe common pitfalls of cryptography.

- [ ] Describe the digital state of data: Data at Rest.

- [ ] Describe the digital state of data: Data in Use.

- [ ] Describe the digital state of data: Data in Transit.

---

Cryptography
: Encryption and related cryptographic mechanisms (hashing, digital signing) safeguard customer data and its integrity, and prevent unauthorized access to it.

## OWASP Top 10

- Missing and faulty crypto consistently appears on OWASP Top 10 list.

## SANS Top 25

- Cryptographic weaknesses feature prominently on SANS Top 25 list.

## Crypto Vulnerabilities in the News

- Crypto vulnerabilities frequently contribute to hacks and data leaks.
- [Bug in Twitter internal software led to passwords stored in plaintext.](https://www.bleepingcomputer.com/news/security/twitter-admits-recording-plaintext-passwords-in-internal-logs-just-like-github/)
- [Coplin Health Systems lost control of un-encrypted data of 43,000 patients when a laptop was stolen from an employee's car.](https://www.databreaches.net/coplin-health-systems-notifies-43000-patients-after-laptop-stolen-from-employees-car/)

---

## Cryptography Basics - Terminology

Encryption
: Process of encoding data in a way that only authorized parties can access it.

- Encryption provides *Confidentiality*, but not *Integrity*.
- Data can be encrypted
  - At rest
  - In use
  - In transit
- Sensitive business and personal data should be encrypted **at all times, everywhere.**
- Importance has risen dramatically in recent years.

### Common Encryption Algorithms

- Symmetric Key (AES, DES, IDEA, ...)
- Public Key (RSA, Elliptic Curve, DH, ...)

![encryption](https://1.bp.blogspot.com/-gyqO5PbitmM/WEMgAFfdMSI/AAAAAAAABD0/SbYlTPkRDEkiUe_Asvpsyst65RFgH6OHQCLcB/s1600/SymmKeyVsPubKey.jpg)

Hash Function
: Maps data of arbitrary size to data of a fixed size.

- Hashing provides *Integrity*, but not *Confidentiality*.
- Original data deliberately hard to reconstruct.
- Used for *integrity checking* and sensitive data storage (e.g. passwords).

Data Signature
: A mathematical scheme for verifying the authenticity of digital messages and documents.

- Uses hashing and public key encryption.
- Ensure *authentication, non-repudiation, and integrity*.

![signature](https://cdn.educba.com/academy/wp-content/uploads/2019/11/Digital-Signature-Cryptography-2.png)

---

## Cryptography Pitfalls

### Missing Encryption of Data and Communications

- Products handle sensitive business and personal data.
- Data is often the most valuable asset that the business has.
- When you store or transmit it in clear text, it can be easily leaked or stolen.
- Today, there is no excuse for not encrypting data that is stored or transmitted.
- Cryptographic technology is mature, tested, and is available for all environments.

**RECOMMENDATION** - Encrypt all sensitive data you are handling (and also ensure its integrity).

- Some product owners do not encrypt stored data because "*users don't have access to the file system*".
- There are plenty of vulnerabilities out there that may allow exposure of files stored on the file system.
- Physical machine running the application may be stolen, hard disk can then be accessed directly.

**RECOMMENDATION** - Have to assume that hte files containing sensitive information may be exposed and analyzed.

### Implementing Own Crypto

- Often, developers use Base64 encoding, simple xor encoding, and similar obfuscation schemes.
- Also, see products implement their own cryptographic algorithms.

**RECOMMENDATION** - Rely on proven cryptography, that was scrutinized by thousands of mathematicians and cryptographers. Follow recommendations of National Institute of Standards and Technology (NIST).

### Relying on Algorithms Being Secret

- "Attackers will never know our internal algorithms."
  - They can and will be discovered; only a question of motivation.
- A whole branch of hacking - **Reverse Engineering** - is devoted to discovering hidden algorithms and data.
- Application shipped only in compiled form can be "de-compiled".
  - Attackers may analyze trial/free versions of the product, or get copies on the Dark Web.

[The Clearswift-sponsored survey polled more than 500 internet technology decision makers and 4,000 employees in the United States, Europe, and Australia, and discovered that](https://www.clearswift.com/resources/press-releases/new-research-reveals-more-third-employees-willing-sell-private-company-data-and-proprietary):

    25 percent of employees would sell company data, risking both their jobs and criminal convictions, for less than $8000;
    3 percent of employees would sell private information for as little as $155;
    18 percent would accept an offer of $1550;
    35 percent of employees were open to bribes as the offer reached $77,500;
    65 percent of employees said they wouldn’t sell data for any price.

- "Security by obscurity" is not a good defense mechanism.
  - All algorithms that keep us safe today are open source and very well-studied: AES, RSA, SHA*, ...

**RECOMMENDATION** - Always assume that algorithms will be known the the adversary.

- Kerckhoff's Principle - *"A crypto-system should be secure even if everything about the system, except the key, is public knowledge."*

### Using Hardcoded/Predictable/Weak Keys

- Not safeguarding keys renders crypto mechanisms useless.
- When the passwords and keys hardcoded in the product or stored plaintext in the config file, they can be easily discovered by an attacker.
- An easily guessed key can be found by trying commonly used passwords.
- When keys are generated randomly, they have to be generated from cryptographically-secure source of randomness, not the regular RNG.

**RECOMMENDATION** - Rely on hard to guess, randomly generated keys and passwords that are stored securely.

### Ignoring Encryption Export Regulation Rules

- Encryption is export controlled.
- All code that...
  - **contains** encryption (closed or open-source).
  - **calls** encryption algorithms in another library or component.
  - **directs** encryption functionality in another product... must be classified for export __*before*__ being released.

---

## Encrypting Data at Rest

- The rule of thumb is to encrypt all sensitive data at rest: in files, config files, databases, backups.
- Symmetric key encryption is most commonly used.
- Follow NIST guidelines for selecting appropriate algorithm - Currently it is AES (with CBC mode) and Triple DES.

## Pitfalls and Recommendations

- Some algorithms are outdated and no longer considered secure.
  - Examples include DES, RC4, and others.
- Use hardcoded/easily guessed/insufficiently random keys.
  - Select cryptographically-random keys, do not reuse keys for different installs.
- Storing keys in a clear text in proximity to data they protect ("key under the doormat").
  - Store keys in secure keystores.
- Using initialization vectors (IVs) incorrectly.
  - Use a new *random* IV every time.
- Preferable to select the biggest key size you can handle (but watch out for export restrictions).

## Encrypting Data in Use

- Unfortunately a rarely-followed practice.
- Memory could be leaked by attacker.
  - Famous 2014 Heartbleed defect leaked memory of processes that used OpenSSL.
- The idea is to keep data encrypted up until it must be used.
- Decrypt data as needed, and then promptly erase it in memory after use.
- Keep all sensitive data (data, keys, passwords) encrypted except a brief moment of use.
- Consider __**Homomorphic encryption**__ if it can be applied to your application.

## Encrypting Data in Transit

- Today, there is no excuse for communicating in clear text.
- There is an industry consensus about; Firefox and Chrome now mark HTTP sites as insecure.
- Attackers can easily snoop on unprotected communications.
- All communications (not just HTTP) should be encrypted, including: RPC, database connections, and others.
- TLS/SSL is most commonly used protocol.
  - Public key crypto (RSA, DH) for authentication and key exchange; Symmetric key crypto to encrypt the data.
  - Server Digital Certificate references certificate authority (CA) and the public key.
- Sometimes just symmetric key encryption is employed (but requires pre-sharing of keys).

## Additional Pitfalls

### Using self-signed certificates

- Less problematic for internal communications but still dangerous.
- Use properly generated certificates verified by established CA.

### Accepting arbitrary certificates

- Attacker can issue their own certificate and snoop on communications (MitM attacks).
- Do not accept arbitrary certificates without verification.

### Not using certificate pinning

- Attacker may present a properly generated certificate and still snoop on communications.
- *Certificate pinning* can help - presented certificate is checked against a set of expected certificates.

### Using outdated versions of the protocol or insecure cipher suites

- Old versions of SSL/TLS are vulnerable (DROWN, POODLE, BEAST, CRIME, BREACH, and other attacks).
- **TLS v1.1-1.3 are safe to use (1.2 is recommended, with 1.3 coming).
- Review TLS support; there are tools to help you:
  - Nessus, Qualys SSL Server Test (external only), sslscan, sslyze.

### Allow TLS downgrade to insecure versions, or even to HTTP

- Lock down versions of TLS that you support and do not allow downgrade; disable HTTP support altogether.

### Not Safeguarding Private Keys

- Do not share private keys between different customers, store them in secure keystores.

#### Additional Recommendations

##### Consider Implementing Forward Secrecy

- Some cipher suites protect past sessions against future compromises of secret keys or passwords.

##### Do not use compression under TLS

- CRIME/BREACH attacks showed that using compression with TLS for changing resources may lead to sensitive data exposure.

##### Implement HTTP Strict Transport Security (HSTS)

- Implement Strict-Transport-Security header on all communications.

##### Stay Informed of Latest Security News

- A protocol or cipher suite that is secure today may be broken in the future.

