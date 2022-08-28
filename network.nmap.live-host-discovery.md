---
id: d31756c0ynv094m2imzqoow
title: Live Host Discovery
desc: ''
updated: 1659653940384
created: 1659162654098
---

# Introduction to Nmap Discovery

The first question about finding live computers and the second question about discovering running services that focuses on port scanning.

1. Nmap Live Host Discovery
2. Nmap Basic Port Scans
3. Nmap Advanced Port Scans
4. Nmap Post Port Scans

Here, we will explain the steps that Nmap carries out to discover the systems that are online before port-scanning. With live hosts, Nmap can:

- ARP scan: Uses ARP requests to discover live hosts.
- ICMP scan: ICMP requests to identify live hosts.
- TCP/UDP ping scan: Sends packets to TCP ports and UDP ports to determine live hosts.

Introduce two scanners, `arp-scan` and `masscan`, and explain how they overlap with part of Nmap's host discovery.

Nmap was created by Gordon Lyon (Fyodor), a network security expert and open source programmer. It was released in 1997 and Nmap is short for Network Mapper, a free, open-source software released under GPL license. Nmap is an industry-standard tool for mapping networks, identifying live hosts, and discovering running services. Nmap's scripting engine further extend its functionality, from fingerprinting services to exploiting vulnerabilities. A Nmap scan usually goes through the steps shown below and may depend on the command-line arguments provided.


![nmap-process](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/f1b4ede255e008646e425038d709c9b6.png)

## Subnetworks

Network segment is a group of computers connected using a shared medium. For instance, the medium can be the Ethernet switch or WiFi access point. In an IP network, a _subnetwork_ is the equivalent of one or more network segments connected together and configured to use the same router.

- The network segment refers to a physical connection, while a subnetwork refers to a logical connection.

![network-diagram](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/aa787518e856e0094cb40da8399be0f3.png)

In the diagram, there are 4 network segments or subnetworks. A subnetwork, or a subnet, has its own IP address range and is connected to a more extensive network via a router.

- Subnets with /16 = 255.255.0.0 and around 65,000 hosts.
- Subnets with /24 = 255.255.255.0 and 250 hosts.

If you are connected to the same subnet, expect the scanner to rely on ARP (Address Resolution Protocol) queries to discover live hosts. An ARP query aims to retrieve hardware MAC address so communication over the link-layer becomes possible.

- If in Network A, ARP will only discover the devices within that subnet (10.1.100.0/24).
- ARP is a link-layer protocol, and ARP packets are bound to their subnet.

## Enumerating Targets

We need to specify the targets we want to scan. You can provide a list, a range, or a subnet. Examples:

- List: `MACHINE_IP scanme.nmap.org example.com` will scan 3 IP addresses.
- Range: `10.11.12.15-20` will scan 6 IP addresses: `10.11.12.15`,... and `10.11.12.20`.
- Subnet: `MACHINE_IP/30` will scan 4 IP addresses.
- Provide a file as input list of targets: `nmap -sL list_of_hosts.txt`.

To check the list of hosts that Nmap will scan, use `nmap -sL TARGETS` to provide a detailed list of the hosts without scanning them.

- Nmap will attempt a reverse-DNS resolution on all the targets to obtain their names. Add `-n` option if do not want Nmap to the DNS server.

## Discovering Live Hosts

We will leverage the protocols to discover the live hosts. Starting from bottom to top, we can use:

- ARP from Link Layer
- ICMP from Network Layer
- TCP from Transport Layer
- UDP from Transport Layer

![layers-TCP/IP](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/745e0412b319d324352c7b29863b74f4.png)

- ARP has one purpose: Sending a frame to the broadcast address on the network segment and asking the computer with a specific IP address to respond by providing its MAC (hardware) address.
- ICMP has [many types](https://www.iana.org/assignments/icmp-parameters/icmp-parameters.xhtml). ICMP ping uses Type 8 (Echo) and Type 0 (Echo Reply).

### Nmap Using ARP

There are various ways to discover online hosts. When no host discovery options are provided, Nmap:

1. When a privileged user tries to scan targets on a local network (Ethernet), Nmap uses ARP requests. A privileged user is root or a user who belongs to sudoers and can run sudo.
2. WHen a privileged user tries to scan targets outside the local network, Nmap uses ICMP echo requests, TCP ACK (Acknowledge) to port 80, TCP SYN (Synchronize) to port 443, and ICMP timestamp request.
3. When an unprivileged user tries to scan targets outside the local network, Nmap resorts to a TCP 3-way handshake by sending SYN packets to ports 80 and 443.

Nmap, by default, uses a ping scan to find live hosts, then proceeds to scan live hosts only.

- Issue `nmap -sn TARGETS` to only discover online hosts without port-scanning the live systems.

ARP scan is possible only if you are on the same subnet as the target systems.

- If you only want Nmap to perform an ARP scan without port-scanning, use `nmap -PR -sn TARGETS`, where `-PR` indicates only an ARP scan.
- The host with the IP address we are asking about will send an ARP reply with its MAC address to tell it is online.

With ARP scans, there is a scanner built around ARP queries: `arp-scan`; provides many options to customize scan.

- A popular command is `arp-scan --localnet` or `arp-scan -l` to send ARP queries to all valid IP addresses on your local networks.
- Similarly, the command `arp-scan` will generate many ARP queries that we can see using tcpdump, Wireshark, or a similar tool.

### Nmap Using ICMP

It is possible to ping every IP address on a target network with `ping` (ICMP Type 8/Echo) requests with a ping reply (ICMP Type 0). This approach is not always reliable as many firewalls block ICMP echo requests.

To use ICMP echo request to discover live hosts, add the option `-PE` (remember to add `-sn` if do not want a port scan).

![ICMP](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/25fb5fd5d2009cf69d7aae40e8fde2ec.png)

- Can scan target's subnet using `nmap -PE -sn MACHINE_IP/24` and will send ICMP echo packets to every IP address, and expect live hosts to reply.
- MAC addresses of the targets do not show unless they are on the same subnet as our system scan.
  - Attempting a scan from a system that belongs to a different subnet will show similar results without the MAC addresses.

Since ICMP echo requests tend to be blocked, might also consider ICMP Timestamp or ICMP Address Mask requests to tell if a system is online. Nmap uses timestamp request (ICMP Type 13) and checks whether it will get a Timestamp reply (ICMP Type 14).

- Adding the `-PP` option tells Nmap to use ICMP timestamp requests.

![ICMP-timestamp](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/06443faaa41a349ff46732d60e2e3bcd.png)

Nmap can also use address mask queries (ICMP Type 17) and checks whether it gets an address mask reply (ICMP Type 18). This scan can be enabled with the option `-PM`.

![ICMP-mask-queries](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/14c31c66e002e2f50b0f8525c8d8e456.png)

### Nmap Using TCP and UDP

#### TCP SYN Ping

Send a packet with the SYN (Synchronize) flag set to a TCP port, 80 by default, and wait for a response.

- An open port should reply with a SYN/ACK(Acknowledge); a closed port would result in an RST (Reset).
  - Below is a reminder of how a TCP 3-way handshake works:
![3-way handshake](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/23e7f481f78de8d3e89ef845b747002d.png)

- Use the option `-PS` followed by the port number, range, list or a combination of them. For example, `-PS21` will target port 21, while `-PS21-25` will target ports 21, 22, 23, 24, and 25.
![TCP-SYN](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/168d48701c5f872cf1930e08b32bcd6f.png)

#### TCP ACK Ping

Sends a packet with an ACK flag set. By default, port 80 is used. The syntax is similar to TCP SYN ping with `-PA`.

- Must be running Nmap as a privileged user to able to accomplish this. As an unprivileged user, Nmap will attempt a 3-way handshake.
  - Privileged users (root and sudoers) can send TCP SYN packets and do not need complete the TCP 3-way handshake even if the port is open. Unprivileged users have no choice but to complete the 3-way handshake if the port is open.
  - The target responds with the RST flag set because the TCP packet with the ACK flag is not part of any ongoing connection. The expected response is used to detect if the target host is up.
    ![TCP-ACK](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/db5ab44a8c700c4ab0603e85e456040d.png)

#### UDP Ping

Contrary to TCP SYN ping, sending a UDP packet to an open port is not expected to lead to any reply. However, if we send a UDP packet packet to a closed UDP port, we expect to get an ICMP port unreachable packet - Indicates that the target system is up and available.

![UDP-ping](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/1b827ef60c39619e281c4ca51a6d57b6.png)

- The syntax to specify the ports is similar to TCP SYN ping and TCP ACK ping; Nmap uses `-PU` for UDP

#### Masscan

Masscan uses a similar approach to discover available systems. Masscan is aggressive with the rate of packets it generates.

- The syntax is quite similar with `-p` followed by a port number, list, or range.
  - `masscan MACHINE_IP/24 -p443`
  - `masscan MACHINE_IP/24 -p80,443`
  - `masscan MACHINE_IP/24 -22-25`
  - `masscan MACHINE_IP/24 --top-ports 100`

### Reverse-DNS Lookup

Nmap’s default behavior is to use reverse-DNS online hosts as hostnames can reveal a lot.

- Can skip DNS queries with `-n`.
- By default, Nmap will look up online hosts; however, can use the option `-R` to query the DNS server even for for offline hosts.
  - To specify DNS server, add the `--dns-servers DNS_SERVER` option.

## Summary

ARP, ICMP, and UDP can detect live hosts - Any response from a host is an indication that it is online. Below is a quick summary of the command-line options:

| Scan Type         | Example Command                             |
| ----------------- | ------------------------------------------- |
| ARP               | `sudo nmap -PR -sn MACHINE_IP/24`           |
| ICMP Echo         | `sudo nmap -PE -sn MACHINE_IP/24`           |
| ICMP Timestamp    | `sudo nmap -PP -sn MACHINE_IP/24`           |
| ICMP Address Mask | `sudo nmap -PM -sn MACHINE_IP/24`           |
| TCP SYN Ping      | `sudo nmap -PS22,80,443 -sn MACHINE_IP/30`  |
| TCP ACK Ping      | `sudo nmap -PA22,80,443 -sn MACHINE_IP/30`  |
| UDP Ping          | `sudo nmap -PU53,161,162 -sn MACHINE_IP/30` |

- Remember `-sn` option is only interested in host discovery without port-scanning.

| Option | Purpose                          |
| ------ | -------------------------------- |
| `-n`   | No DNS lookup                    |
| `-R`   | Reverse-DNS lookup for all hosts |
| `-sn`  | Host discovery only              |