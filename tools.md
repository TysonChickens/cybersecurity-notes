---
id: d9ibeadgk68z3q2qjgsqida
title: Tools
desc: ''
updated: 1653038754656
created: 1653038741994
---

# Introduction to Firewalls

- [ ] Describe the purpose, function, and types of firewall.

- [ ] Describe what packet filtering is and how packet filtering firewalls work.

- [ ] Describe application gateways and how these differ from standard packet filtering firewalls.
- [ ] Describe the limitations of application gateways.

- [ ] Describe what an XML gateway is and why it is used.

- [ ] Describe the difference between a stateful and a stateless firewall.
- [ ] Describe the tradeoffs when moving from a stateless to a stateful firewall.

---

Firewalls
: Isolates organization's internal net from larger Internet, allowing some packets to pass, blocking others.

## Purpose

- Prevent denial of service attacks
  - **SYN flooding**: Attacker establishes many bogus TCP connections, no resources left for "real" connections.
- Prevent illegal modification/access of internal data.
  - Attacker replaces CIA's homepage with something else.
- Allow only authorized access to inside network (set of authenticated users/hosts)
- **2 types of firewalls**:
  - Application-level
  - Packet-filtering

Packet Filtering
: Firewall technique used to control network access by monitoring outgoing and incoming packets and allowing them to pass or halt based on the source and destination Internet Protocol (IP) addresses, protocols and ports.

- Internal network connected to Internet via **router firewall**.
- Router **filters packet-by-packet**, decision to forward/drop packet based on:
  - Source IP address, destination IP address.
  - TCP/UDP source source and destination port numbers.
  - ICMP message type.
  - TCP SYN and ACK bits.

*Example 1: Block incoming and outgoing datagrams with IP protocol field = 17 and with either source or dest prot = 23.*

- All incoming and outgoing UDP flows and telnet connections are blocked.

*Example 2: Block inbound TCP segments with ACK=0.*

- Prevents external clients from making TCP connections with internal clients, but allows internal clients to connect to outside.

## Application Gateway

- Filters packets on application data as well on IP/TCP/UDP fields.
- *Example: Allow select internal users to telnet outside.*
  1. Require all telnet users to telnet through gateway.
  2. For authorized users, gateway sets up telnet connection to destination host. Gateway relays data between 2 connections.
  3. Router filter blocks all telnet connections not originating from gateway.

### Limitations of Firewalls and Gateways

- **IP spoofing** - Router can't know if data "really" comes from claimed source.
- If multiple apps need special treatment, each has own app gateway.
- Client software must know how to contact gateway (e.g. must set IP address of proxy in web browser).
- Filters often use all or nothing policy for UDP.
- *Tradeoff: Degree of communication with outside world, level of security.*
- Many highly protected sites still suffer from attacks.

## XML Gateway

- XML traffic passes thorough a conventional firewall without inspection (all across normal web ports).
- An XML gateway examines the payload of the XML message.
  - Well formed (meaning to spec) payload.
  - No executable code.
  - Target IP address makes sense.
  - Source IP is known.

## Stateless and Stateful

- Filter traffic between networks.
- They handle packets differently.
- They are multi-homed: Multiple NICs connected to different networks
- There are different types of firewalls. Stateless and Stateful are the most common ones.

### Stateless Firewalls

- No concept of "state".
- Also called Packet Filter.
- Filter packets based on Layer 3 and 4 information (IP and port).
- Lack of state makes it less secure.

### Stateful Firewalls

- Have state tables that allow the firewall to compare current packets with previous packets.
- Could be slower than packet filters but far more secure.
- Application Firewalls can make decisions based on Layer 7 information.

### Proxy Firewalls

- Proxy Firewall acts as intermediary servers.
- Proxies terminate connections and initiate new ones, like MITM.
- There are two 3-way handshakes to between two devices.

