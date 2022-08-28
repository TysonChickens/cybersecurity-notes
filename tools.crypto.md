---
id: zlio56gb9b3584pqbluv2hm
title: Crypto
desc: ''
updated: 1653041861040
created: 1653041855092
---

# Introduction to Cryptography

- [ ] Explain the role of cryptography in cybersecurity, how it is used and how it can be attacked.

- [ ] Describe the purpose or use of cryptography in cybersecurity.
- [ ] Describe how cryptography is used to assure the key cybersecurity tenants of confidentiality, integrity, authentication and non-repudiation.

- [ ] Describe the three encryption types used in modern cryptography, including typical uses and advantages of each:
  - [ ] Symmetric
  - [ ] Asymmetric
  - [ ] Hash

- [ ] Describe the 5 common forms of cryptographic attacks:
  - [ ] Brute force
  - [ ] Rainbow tables
  - [ ] Social engineering
  - [ ] Known plaintext
  - [ ] Known ciphertext

- [ ] Describe important cryptography terms such as:
  - [ ] Plaintext
  - [ ] Ciphertext
  - [ ] Symmetric key
  - [ ] Public key
  - [ ] Substitution cipher
  - [ ] DES: Data Encryption Standard

---

- Cryptography is secret writing.
- Secure communication that may be understood by the intended recipient only.
- There is data in motion and data at rest. Both need to be secured.
- Been used for thousands of years by Egyptians Hieroglyphics, Spartan Scytale, Caesar Cipher, are examples of ancient cryptography.

## Key Concepts

Confidentiality
: Process of assuring that only the intended parties can read and understand the message.

Integrity
: Process of detecting if the message has been changed, where the message should not be altered in any way in the process of being transmitted.

Authentication
: Process of identifying are authenticated with someone or something it is actually to do something.

Non-repudiation
: Process of detecting if something or someone has done something, and that someone cannot deny that action or that message which was sent by him or her.

Cryptoanalysis
: Process of analyzing ciphers in cryptographic algorithms. Allows scientists and mathematicians to determine if a cryptographic algorithm is secure or not.

Cipher
: An algorithm that encrypts a message.

Plaintext
: Basic text that is human readable.

Ciphertext
: Plaintext gone through the cipher, which is basically the cipher has been applied to a plaintext and ciphertext is not humanly readable.

Encryption
: Process of transforming plaintext into ciphertext.

Decryption
: Process of transforming the ciphertext into a plaintext using the cipher.

## Cryptographic Strength

- Relies on math, not secrecy.
- Ciphers that have stood the test of time are public algorithms.
- Mono-alphabetic < Poly-alphabetic Ciphers
- Modern ciphers use Modular math.
- Exclusive Or (XOR) is the "secret sauce" behind modern encryption.
    ![XOR table](https://img.phemex.com/wp-content/uploads/2021/07/19091947/xor.jpg)

## Stream Cipher and Block Cipher

Stream Cipher
: Encrypt or decrypt bit per bit.

Block Cipher
: Encrypt or decrypt in blocks or several sizes, depending on the algorithm.

---

## Types of Cryptography

There are three primary types for modern encryption:

- Symmetric
- Asymmetric
- Hash

### Symmetric Encryption

- Use the same key to encrypt and decrypt.
- Security depends on keeping the key secret at all times.
- Strengths include speed and cryptographic strength  per bit of key.
- The bigger the key, the stronger the algorithm.
- Key need to be shared using a secure, out-of-band method.
- DES, Triples DES, AES are examples of symmetric encryption.

### Asymmetric Encryption

- Whitfield Diffie and Martin Hellman are pioneers of asymmetric encryption, created the Diffie-Hellman.
- Uses two keys.
- One key can be made public, called *public key*. The other one needs to be kept private, called *private key*.
- One for encryption and one for decryption.
- Used in digital certificates, Public Key Infrastructure - PKI.
- Uses "one-way" algorithms to generate the two keys.
- Slower than symmetric encryption.

### Hash Functions

- A hash function provides encryption using an algorithm and no key.
- A variable-length plaintext is "hashed" into a fixed-length hash value, often called a "message digest" or simply a "hash".
- If the hash of a plaintext changes, the plaintext itself has changed = Provides integrity verification.
- SHA-1, MD5, older algorithms prone to collisions (two different plaintext having the same hash)/
- SHA-2 is the newer and recommended alternative.

---

## Cryptographic Attacks

Brute force
: Attack based on trial and error through submission of many passwords to guess correctly.

Rainbow tables
: Similar to brute force, but they use a limited amount of information or entity, or files, and they contain three hash passwords to check against hash customers to make attacks a lot faster.

Social engineering
: Non-technical methods to obtain a user information or password.

Known Plaintext
: Having only plain text and doing analysis based on the plain text to understand how the cipher works.

Known ciphertext
: Process of having only ciphertext. Similar to plaintext attack but only have ciphertext to defer the key used in the cipher to encrypt and decrypt information.

---

## A Different Perspective from a Security Architect

![The Language of Cryptography](https://in.element14.com/wcsstore/ExtendedSitesCatalogAssetStore/cms/asset/images/common/campaign/internet_of_things/the-language.png)

### Symmetric Encryption Visual

![Symmetric Cryptography](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/symmetric-key-what-is-cryptography-edureka.png)

### Asymmetric Encryption Visual

![Asymmetric Cryptography](https://sectigostore.com/blog/wp-content/uploads/2020/11/asymmetric-encryption.png)

#### DES (Data Encryption Standard)

- US encryption standard [NIST 1993]
- 56-bit symmetric key, 64-bit plaintext input.
  - 56-bit-key-encrypted phrase ("Strong cryptography makes the world a safer place") decrypted (brute force) in 4 months.
  - No known "backdoor" decryption approach.
  - DES MORE SECURE:
    - Use three keys sequentially (3-DES) on each datum.
    - Use cipher-block chaining.

![DES](https://assets.omscs.io/notes/5CC2B27E-728F-44B1-871D-3CBDC4BAE48F.png)

### Substitution Cipher

Substitution Cipher
: Substituting one thing for another.
    *Monoalphabetic cipher*: Substitute one letter for another.

![Monoalphabetic cipher](https://www.researchgate.net/profile/Ahtisham-Hashmi/publication/323081658/figure/download/fig2/AS:592450070532097@1518262512719/Mono-Alphabetic-Substitution-Cipher.png)

### AES: Advanced Encryption Standard

- New (November 2001) symmetric-key NIST standard, replacing DES.
- Processes data in 128 bit blocks.
- 128, 192, or 256 bit keys.
- Brute force decryption (try each key) taking 1 sec on DES, takes 149 trillion years for AES.

