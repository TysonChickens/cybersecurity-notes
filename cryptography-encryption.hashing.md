---
id: 0fne3cpmfljfulwoqcenf7k
title: Hashing
desc: ''
updated: 1653132086144
created: 1653132070213
---

# Hashing

- [ ] Describe hashing and its purpose in encryption.
- [ ] Describe common pitfalls of using hashing.
- [ ] Describe additional considerations when using hashing.
- [ ] Define Message Authentication Codes (MACs).

---

Hashing is used for a variety of purposes:

- Validating passwords (salted hashes).
- Verifying data/code *integrity* (message authentication codes and keyed hashes).
- Verifying data/code *integrity* and *authenticity* (digital signatures).
- Use secure hash functions (follow NIST recommendations):
  - **SHA-2 (SHA-256, SHA-384, SHA-512, etc) and SHA-3**.

## Pitfalls

### Using Weak or Obsolete Functions

- Hash functions for which it is practical to generate *collisions* (two or more different inputs that correspond to the same hash value) are not considered robust.
- **MD5** has been known to be broken for more than 10 years, collisions are fairly easily generated.
- **SHA-1** was recently proven to be unreliable.
  - [Google proof of SHA-1 collisions.](https://security.googleblog.com/2017/02/announcing-first-sha1-collision.html)

### Using Predictable Plaintext

- Not quite a cryptography problem, but password can be discovered through brute-forcing.

### Using Unsalted Hashes when Validating Passwords

- Even for large problem spaces, rainbow tables can be used to crack hashes.
- When *salt* (a random byte sequence, at least 8 bytes recommended) is added to the plaintext the resulting hash is completely different, and rainbow tables will no longer help.
  - Use *key stretching functions* with a large number of iterations.
    - Deliberately slow (controlled by number of iterations) in order to make brute-forcing attacks impractical, both online and offline (aim for 750ms to complete the operation).
  - Future proof hashes - include an algorithm identifier to allow seamless upgrade in the future if the current algorithm becomes obsolete.

![salt](https://cdn.guidingtech.com/media/assets/WordPress-Import/2016/10/HASH_AND_SALT.png)

## Message Authentication Codes (MACs)

![MACs](https://www.computertechreviews.com/wp-content/uploads/2019/12/maxresdefault-2.jpg)

- MACs confirm that the data block came from the stated sender and has not been changed.
- Hash-based MACs (HMACs) are based on crypto hash functions (e.g. HMAC-SHA256 or HMAC-SHA3).
- They generate a hash of the message with the help of the secret key.
  - If the key is not known, attacker cannot alter the message and be able to generate another valid HMAC.
- HMACs help when data may be maliciously altered while under temporary attacker's control (e.g. cookies, or transmitted messages).
- Even encrypted data should be protected by HMACs to avoid *bit-flipping attacks*.

