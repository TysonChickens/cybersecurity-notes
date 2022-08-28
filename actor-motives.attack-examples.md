---
id: u78aaokg3hlvee6vixocu29
title: Attack Examples
desc: ''
updated: 1653034458600
created: 1653034451929
---

# Additional Attack Examples Today

- [ ] Describe how network mapping, or "casing the joint" is used by bad actors, what commands are used and what information is commonly gathered.
- [ ] Describe the countermeasures that can be used against mapping threats.
- [ ] Describe packet sniffing and how it can be used to gather information about your network.
- [ ] Describe the countermeasures you can deploy to safeguard against packet sniffers.

- [ ] Describe how IP Spoofing can be used by attackers.
- [ ] Describe how ingress filtering can be used as a countermeasure to safeguard against IP Spoofing and its level of effectiveness.

- [ ] Describe how Denial of Service (DoS) and Distributed Denial of Service (DDoS) attacks are carried out.
- [ ] Describe how packet filtering and traceback can be used to help counter DoS attacks and the shortcoming of these measures.

- [ ] Describe how host insertions are used to compromise a network.
- [ ] Describe what measures can be taken to protect against unauthorized insertion of a new host on your network.

## Internet Security Threats

### Mapping

- Before attacking - "case the joint" to find out what services are implemented on the network.
- Use `ping` to determine what hosts have addresses on the network.
- Port-scanning to attempt to establish TCP connection to each port in sequence (see what happens).
- *nmap* mapper (network exploration and security auditing).
  
#### Mapping Countermeasures

- Record traffic entering network.
- Look for suspicious activity (IP addresses, ports being scanned sequentially).
- Use a host scanner and keep a good inventory of hosts on the network.
  - Be wary of an unexpected "computer" appears on the network.

---

### Packet Sniffing

- Broadcast media
- Promiscuous NIC reads all packets passing by.
- Can read all unencrypted data (e.g passwords).
- Computer C sniffs Computer B packets.

#### Countermeasures - Packet Sniffing

- All hosts in organization run software that checks periodically if host interface in promiscuous mode.
- One host per segment of broadcast media (switched Ethernet at hub).

---

### IP Spoofing

- Can generate "raw" IP packets directly from application, putting any value into IP source address field.
- Receiver can't tell if source is spoofed.
- e.g: C pretends to be B.

#### Countermeasures - IP Spoofing

**Ingress filtering**:

- Routers should not forward outgoing packets with invalid source addresses (datagram source address not in router's network).
- Downside is can not be mandated for all networks.

---

### Denial of Service

- Flood of maliciously generated packets "swamp" receiver.
- Distributed DOS (DDoS): Multiple coordinated sources of packets to target the user.

#### Countermeasures - Denial of Service

- *Filter out* flooded packets (e.g SYN) before reaching host (throw out good with bad).
- *Traceback* to source of floods (most likely an innocent, compromised machine).

---

### Host Insertions

- Generally an insider threat, a computer "host" with malicious intent is inserted in sleeper mode on the network.
  
#### Countermeasures - Host Insertions

- Maintain an accurate inventory of computer hosts by MAC address.
- Use a host scanning capability to match discoverable hosts against known inventory.
- Missing hosts are okay.
- New hosts are bad news.

#### Threats

- Rogue software processes
- Inserted onto a host intentionally
- Other source is a good processes co-opted for bad purposes
- Possible usage:
  - Network traffic monitoring
  - Extract sensitive data:
    - Crypto keys
    - Plaintext documents

