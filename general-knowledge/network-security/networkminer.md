---
description: >-
  How to use NetworkMiner to analyze traffic files and network forensic
  activities
---

# NetworkMiner

{% embed url="https://www.netresec.com/?page=NetworkMiner" %}

Official description:

> NetworkMiner is an [open source](https://www.netresec.com/?page=NetworkMinerSourceCode) network forensics tool that extracts artifacts, such as files, images, emails and passwords, from captured network traffic in PCAP files. NetworkMiner can also be used to capture live network traffic by sniffing a network interface. Detailed information about each IP address in the analyzed network traffic is aggregated to a network host inventory, which can be used for passive asset discovery as well as to get an overview of which devices that are communicating. NetworkMiner is primarily designed to run in Windows, but can also be used in [Linux](https://www.netresec.com/?page=Blog\&month=2014-02\&post=HowTo-install-NetworkMiner-in-Ubuntu-Fedora-and-Arch-Linux).
>
> NetworkMiner has, since the first release in 2007, become a popular tool among incident response teams as well as law enforcement. NetworkMiner is today used by companies and organizations all over the world.

## Features

| Capability                            | Description                                                                                                                                                                                             |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Traffic sniffing                      | Intercept the traffic, sniff it, and collect and log packets that pass through the network.                                                                                                             |
| <p>Parsing PCAP files<br></p>         | Parse pcap files and show the content of the packets in detail.                                                                                                                                         |
| <p>Protocol analysis<br></p>          | Identify the used protocols from the parsed pcap file.                                                                                                                                                  |
| <p>OS fingerprinting<br></p>          | <p>Identify the used OS by reading the pcap file. This feature strongly relies on<a href="https://github.com/xnih/satori/"> Satori </a>and <a href="https://lcamtuf.coredump.cx/p0f3/">p0f</a>.<br></p> |
| <p> File Extraction<br></p>           | <p>Extract images, HTML files and emails from the parsed pcap file.<br></p>                                                                                                                             |
| <p>Credential grabbing<br></p>        | <p>Extract credentials from the parsed pcap file.<br></p>                                                                                                                                               |
| <p>Clear text keyword parsing<br></p> | Extract clear-text keywords and strings from the parsed pcap file.                                                                                                                                      |

## Operating Modes

There are two main modes:

* Sniffer: Not intended to use as a sniffer and is available only on Windows. It is not a dedicated sniffer like Wireshark and tcpdump.
* Packet Parsing/Processing: Capture a quick overview and information on the investigated capture. This mode is used to grab the easy details before deep dive investigation.

## Pros and Cons

### Pros

* OS fingerprinting
* Easy file extraction
* Credential grabbing
* Clear text keyword parsing
* Overall overview

### Cons

* Not useful in active sniffing
* Not use for large pcap investigation
* Limited filtering
* Not built for manual traffic investigation

## Differences Wireshark and NetworkMiner

The best practice is to record the traffic for offline analysis, quickly overview the pcap with NetworkMiner and go deep with Wireshark for further investigation.

| Feature                     | NetworkMiner                                                    | Wireshark                    |
| --------------------------- | --------------------------------------------------------------- | ---------------------------- |
| Purpose                     | <p>Quick overview, traffic mapping, and data extraction<br></p> | <p>In-Depth analysis<br></p> |
| GUI                         | <p>✅<br></p>                                                    | <p>✅<br></p>                 |
| Sniffing                    | <p>✅<br></p>                                                    | <p>✅<br></p>                 |
| Handling PCAPS              | <p>✅<br></p>                                                    | <p>✅<br></p>                 |
| OS Fingerprinting           | <p>✅<br></p>                                                    | <p>❌<br></p>                 |
| Parameter/Keyword Discovery | <p>✅<br></p>                                                    | Manual                       |
| Credential Discovery        | <p>✅<br></p>                                                    | <p>✅<br></p>                 |
| File Extraction             | <p>✅<br></p>                                                    | <p>✅<br></p>                 |
| Filtering Options           | <p>Limited<br></p>                                              | <p>✅<br></p>                 |
| Packet Decoding             | <p>Limited<br></p>                                              | <p>✅<br></p>                 |
| Protocol Analysis           | <p>❌<br></p>                                                    | <p>✅<br></p>                 |
| Payload Analysis            | <p>❌<br></p>                                                    | <p>✅<br></p>                 |
| Statistical Analysis        | <p>❌<br></p>                                                    | <p>✅<br></p>                 |
| Cross-Platform Support      | <p>✅<br></p>                                                    | <p>✅<br></p>                 |
| Host Categorization         | <p>✅<br></p>                                                    | <p>❌<br></p>                 |
| Ease of Management          | <p>✅<br></p>                                                    | ✅                            |
