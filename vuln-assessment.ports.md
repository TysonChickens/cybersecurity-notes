---
id: g5iofppe4yv4diis8es1q9t
title: Ports
desc: ''
updated: 1653180875870
created: 1653180871962
---

# Port Scanning

- [ ] Describe what port scanning is.
- [ ] Learn what information can be gained from port scanning.
- [ ] Learn about NMAP and ZenMap port scanning applications.

---

> Network port and service identification involves using a port scanner to identify network ports and services operating on active hosts - such as FTP and HTTP - and the application that is running each identified service, such as Microsoft Internet Information Server (ISS) or Apache for the HTTP service... All basic scanners can help identify active hosts and open ports, but some scanners are also able to provide additional information on the scanned hosts.

## What is a Port?

Port
: Computer ports are the central docking point for the flow of information from a program or the internet to a device or another computer in the network and vice versa. It is the parking spot for the data to be exchanged through electronic, software, or programming-related mechanisms.

- Port 20 (UDP) File Transfer Protocol (FTP) used for data transfer.
- Port 22 (TCP) Secure Shell (SSH) protocol for secure logins, ftp, and port forwarding.
- Port 53 (UDP) Domain Name System (DNS) which translates names to IP addresses.
- Port 80 (TCP) World Wide Web HTTP.

## Responses

A port scanner is a simple computer program that checks all of those doors - start calling ports - and responds with one of three possible responses:

- Open, Accepted
- Closed, Not Listening
- Filtered, Dropped, Blocked

## Types of Scans

Port scanning is a method of determining which ports on a network are open and could be receiving or sending data. It is also a process for sending packets to specific ports on a host and analyzing responses to identify vulnerabilities.

- **Ping** - Simplest port scan sending ICMP echo requests to see who is responding.
- **TCP/Half Open** - A popular, deceptive scan also known as SYN scan.
  - It notes the connection and leaves the target hanging.
- **TCP Connect** - Completing the TCP connection and makes it slower and noisier than half open.
- **UDP** - Send an empty packet or a packet that has a different payload per port, and will only get a response if the port is closed.
  - Faster than TCP but doesn't contain as much data.
- **Stealth** - TCP scans are quieter than the other options and can get past firewalls. They will still get picked up by the most recent IDS.

## Tools

### NMAP

Nmap ("Network Mapper") is an open source tool for network exploration and security auditing.

- Designed to rapidly scan large networks, and works fine against single hosts.
- Nmap uses raw IP packets in novel ways to determine what hosts are available on the network. 
  - Services (application name and version) those hosts are offering.
  - Type of packet filters/firewalls are in use.
  - Dozens of other characteristics...
- Commonly used for security audits.
  - Also good for many systems and network administrators for routine tasks such as network inventory, managing service upgrade schedules, and monitoring host or service uptime.
