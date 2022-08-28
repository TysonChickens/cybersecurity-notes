---
id: gjixtopfgi2e35xn8tjx0zn
title: Net Analyzer
desc: ''
updated: 1653180954767
created: 1653180937836
---

# Network Protocol Analyzers

- [ ] Learn what network protocol analyzers are.
- [ ] Learn about Wireshark as the predominate network protocol analyzer.
- [ ] Understand the packet capture file format.

---

> A protocol analyzer (also known as sniffer, packet analyzer, network analyzer, or traffic analyzer) can capture data in transit for the purpose of analysis and review. Sniffers allow an attacker to inject themselves in a conversation between a digital source and destination in hopes of capturing useful data.

## Sniffers

Sniffers operate at the data link layer of the OSI model.

- They do not have to play by the same rules as the applications and services that reside further up the stack.
- Sniffers can capture everything on the wire and record it for later review.
- Allow user to see all of the data contained in the packet.

![osi](https://s7280.pcdn.co/wp-content/uploads/2018/06/osi-model-7-layers-1.png)

### WireShark

Wireshark intercepts traffic and converts that binary traffic into human-readable format.

- Makes it easy to identify what traffic is crossing your network.
  - Amount of data
  - Frequency
  - Latency between hops and so on.
- Network administrators use it to trouble network problems.
- Network security engineers use it to examine security problems.
- QA engineers use it to verify network applications.
- Developers use it to debug protocol implementations.
- People use it to learn network protocol internals.

#### Features

- Deep inspection of hundreds of protocols, with more being added all the time.
- Live capture and offline analysis.
- Standard three-pane packet browser.
- Multi-platform: Runs on Windows, Linux, OS X, FreeBSD, NetBSD, etc.
- Captured network data can be browsed via a GUI, or via the TTY-mode TShark utility.
- The most powerful display filters in the industry.
- Rich VOIP analysis.
- Read/write many different capture file formats.
- Capture files compressed with gzip can be decompressed on the fly.
- Live data can be read from many media sources.
- Decryption support for many protocols, including IPsec, ISAKMP, Kerberos, SNMPv3, SSL/TLS, WEP, and WPA/WPA2.
- Coloring rules can be applied to the packet list for quick, intuitive analysis.
- Output can be exported to XML, PostScript*, CSV, or plain text.

### Packet Capture (PCAP)

PCAP is a valuable resource for file analysis and to monitor your network traffic. Packet collection tools like Wireshark allow you to collect network traffic and translate it into a format that is human-readable.

- Most common for monitoring bandwidth usage...
  - Identify rogue DHCP servers
  - Detecting malware
  - DNS resolution
  - Incident response

Wireshark uses .pcap files to record packet data that has been pulled from a network scan. Packet data is recorded in files with the .pcap file extension and can be used to find performance problems and cyberattacks on the network.

- Libpcap
- WinPcap
- PCapng
- Npcap

