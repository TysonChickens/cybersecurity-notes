---
id: 06obwk18k40kw2ywrzqo68q
title: Quantum Computers
desc: ''
updated: 1653132217350
created: 1653132205274
---

# Impact of Quantum Computing

- [ ] Describe the impacts of quantum computing on cryptography.

---

Quantum computing
: Computing using quantum-mechanical phenomena.

- Still 10-15 years away from quantum computing having an effect on crypto.

## Risks

Existing crypto symmetric encryption (e.g. AES) will be weakened.
  
- To maintain current levels of security, double the encryption key size (go from 128-bit to 256-bit keys).

Public key encryption that relies on prime number factorization (RSA used in SSL/TLS, blockchain, digital signatures) will be broken.

- Plan on switching to quantum-resistant algorithms (Lattice-based Cryptography, Homomorphic Encryption).

Attacker can capture conversations now and decrypt them when quantum computing becomes available.

- Make encryption, hash, signing algorithms "replaceable", to exchange them for something more robust if a weakness is discovered.
