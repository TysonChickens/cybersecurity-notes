---
id: s4pb2fsqnhn3juvfg31nlx4
title: Digital Signatures
desc: ''
updated: 1653132149394
created: 1653132135898
---

# Digital Signatures

- [ ] Describe recommended uses of digital signatures.

- [ ] Describe how to safeguard encryption keys.
- [ ] Describe how to secure the Key Encryption Key (KEK).

---

Digital Signatures
: Ensure that messages and documents come from an *authentic source* and were *not maliciously modified* in transit.

- Some recommended uses of digital signatures include verifying integrity if:
  - Data exchanged between nodes in the product.
  - Code transmitted over network for execution at client side (e.g. JavaScript).
  - Service- and fix packs installed by customer.
  - Data temporarily saved to customer machine (e.g. backups).
- Digital signatures must be verified to be useful.

---

## Safeguard Encryption Keys

Encryption is futile if the encryption keys are not safeguarded.

- **DO NOT STORE** them in your code, in plaintext config files, in databases.
- Proper way to store keys and certificates is in secure cryptographic storage, e.g. keystores.
  - For example, in Java, you can use Java KeyStore (JKS).
- **There is a tricky problem of securing Key Encrypting Key (KEK)**
  - A key used to encrypt the keystore.

### Securing KEK

- Use Hardware Secure Modules (HSM).
- Use Virtual HSM (Unbound vHSM).
- Derive KEK from user-entered password.
  - Can be seen in Symantec Encryption Desktop software securing our laptops.
- Derive KEK from data unique to the machine product is running on.
  - Could be file system metadata (random file names, file timestamps).
  - Attacker that downloads the database or the keystore will not be able to as easily obtain this information.

