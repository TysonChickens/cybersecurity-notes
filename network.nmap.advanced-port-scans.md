---
id: kxheujncrxbvnhs0tlf1kd4
title: Advanced Port Scans
desc: ''
updated: 1659928811439
created: 1659750479376
---

# Introduction

Explains different advanced types of scans and scan options. Some of these scan types can be useful against specific systems, while others are useful in particular network types.

- Null Scan
- FIN Scan
- Xmas Scan
- Maimon Scan
- ACK Scan
- Window Scan
- Custom Scan

Cover the topics including:

- Spoofing IP
- Spoofing MAC
- Decoy Scan
- Fragmented Packets
- Idle/Zombie Scan

## TCP Null Scan, FIN Scan, and Xmas Scan

### Null Scan

The null scan does not set any flag; all six flag bits are set to zero. Use `-sN` option during a scan and a TCP packet with no flags will not trigger any response when it reaches an open port.

- A lack of reply in a null scan indicates that either the port is open or a firewall is blocking the packet.
![null](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/04b178a9cf7048c21256988b8b2343e3.png)

However, we expect the target server to respond with an RST packet if the port is closed. The lack of RST response to figure out ports that are not closed: open or filtered.

![null-RST](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/224e01a913a1ce7b0fb2b9290ff5e1c8.png)

Note that many Nmap options require root privileges.

### FIN Scan

The FIN scan needs a TCP packet with the FIN flag set. Use `-sF` option for this scan type. Similarly, no response will be sent if the TCP port is open.

![FIN](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/78eb3d6ba158542f2b3223184b032e64.png)

However, the target system should respond with an RST if the port is closed. Some firewalls will 'silently' drop the traffic without sending an RST.
![FIN-RST](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/74dc07da7351a5a7f258948ec59efccc.png)

### Xmas Scan

Xmas scan gets its name after Christmas tree lights. An Xmas scan sets the FIN, PSH, and URG flags simultaneously. The option `-sX` to use Xmas scan.

Like the Null and FIN scan, if an RST packet is received, it means that the port is closed. Otherwise, it will be reported as open|filtered.

![Xmas](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/4304eacbc3db1af21657f285bc16ebce.png)

- These scans can be efficient when scanning a target behind a stateless (non-stateful) firewall. A stateless firewall will check if the incoming packet has the SYN flag set to detect a connection attempt.
  - A stateful firewall will block all such crafted packets and render this kind of scan useless.

## TCP Maimon Scan

Uriel Maimon first described this scan in 1996 where the FIN and ACK bits are set. The target should send an RST packet as a response. The option `-sM` to use Maimon scan.

- BSD-derived systems drop the packet if it is an open port exposing the open ports.
- This scan will not work on most targets in a modern network.
- Most target systems respond with an RST packet regardless whether the TCP port is open - will not be able to discover the open ports.

![Maimon](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/8ca5e5e0f6e0a1843cebe11b5b0785b3.png)

## TCP ACK, Window, and Custom Scan

### TCP ACK Scan

An ACK scan will send a TCP packet with ACK flag set. Use the option `-sA`.

- The target would respond to the ACK with RST regardless of the state of the port. This happens because a TCP packet with the ACK flag set should be sent only in response a received TCP packet to acknowledge of some data.

![TCP-ACK](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/a991831cedbb2761dde1fe66012a7311.png)

- This scan would be helpful if there is a firewall in front of the target.
  - Based on which ACK packets resulted in responses, this will show which ports were not blocked by the firewall.
- Type of scan is more suitable to discover firewall rule sets and configuration.

### Window Scan

TCP Window scan is almost the same as the ACK scan; however, it examines the TCP Window field of the RST packets returned. Use the scan option `-sW`.

- We expect to get an RST packet in reply to our 'uninvited" ACK packets, regardless of whether the port is open or closed.
- Using a TCP Window scan against a server behind a firewall will show ports are detected as closed.
  - Indicates the firewall does not block them.
- In contrast with the ACK scan that labels ports as unfiltered.

### Custom Scan

Use `--scanflags` to experiment beyond built-in TCP scan types.

- To set SYN, RST, and FIN simultaneously, use `--scanflags RSTSYNFIN`

![Custom](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/d76c5020f14ac0d66e7ff3812bb0bec3.png)

- Important to understand how the different ports will behave to interpret the results in different scenarios.
- Essential to note that the ACK scan and the Window scan are very efficient at helping to map out the firewall rules. There is a possibility the firewall rules need to be updated to reflect recent service changes. ACK and Window scans are exposing the firewall rules, not the services.

## Spoofing and Decoys

In some network setups, you can scan a target system using a spoofed IP address or even a spoofed MAC address. This is only beneficial where you can guarantee to capture the response.

Use the command `nmap -S SPOOFED_IP MACHINE_IP`. The target machine will respnd to the incoming packets sending the replies to the destination IP address of the SPOOFED_IP.

- For this to work and receive accurate results, the attacker needs to monitor the network traffic to analyze the replies.

![SPOOF](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/45b982d501fd26deb2b381059b16f80c.png)

Scanning with a spoofed IP address:

1. Attacker sends a packet with a spoofed source IP address to the target machine.
2. Target machine replies to the spoofed IP address as the destination.
3. Attacker captures the replies to figure out open ports.

Specify the network interface using `-e` and disable ping scan with `-Pn`. Instead of `nmap -S SPOOFED_IP MACHINE_IP`, you will need to issue `nmap -e NET_INTERFACE -Pn -S SPOOFED_IP MACHINE_IP` to tell Nmap explicitly which network interface to use and not to expect to receive a ping reply.

- Scan will be useless if the attacker system cannot monitor the network for responses.
- When on the same subnet as the target machine, you would be able to spoof MAC address as well.
  - Specify the source MAC address using `--spoof-mac SPOOFED_MAC`. This address spoofing is only possible if the attacker and the target machine are on the same Ethernet (802.3) network or same WiFi(802.11).

Spoofing only works in a few number of cases where certain conditions are met. The concept is to make the scan appear to be coming from many IP addresses so that the attacker's IP address would be lost among them.

![Decoy](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/754fc455556a424ca83f512665beaf7d.png)

Launch a decoy scan by providing a specific or random IP address after `-D`.

## Fragmented Packets

**Firewall**
: A piece of software or hardware that permits packets to pass through or blocks them. It functions based on firewall rules, summarized as blocking all traffic with exceptions or allowing all traffic with exceptions. A traditional firewall inspects the IP header and the transport layer header. A more sophisticated firewall would also try to examine the data carried by the transport layer.

**IDS**
: An intrusion detection system (IDS) inspects network packets for select patterns or specific content signatures. It raises an alert whenever a malicious rule is met. In addition to the IP header and transport layer header, an IDS would inspect the data contents in the transport layer and check matches for any malicious patterns.

**Fragmented Packets**
: Nmap provides the option `-f` to fragment packets. The IP data will be divided into 8 bytes or less. Adding another `-f` (`-ff`) will split the data into 16 byte-fragments instead of 8.

![fragment](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/5e55834e2638ba7ec9e84a0900b68ccb.png)

The data we will fragment across multiple packets is highlighted in red. IP uses the identification (ID) and fragment offset, shown in the second row aid in reassembly on the recipient side.

## Idle/Zombie Scan

Spoofing the source IP address can be a good approach to scanning stealthily but only works in specific network setups.

- Requires to be in a position to monitor the traffic.

Meanwhile, the idle scan, or zombie scan requires an idle system connected to the network that can communicate with.

- Nmap will make each probe appear as if coming from the idle (zombie) host, then check for indicators whether the idle (zombie) host received any response to the spoofed probe.
  - Run an idle scan using `-nmap -sI ZOMBIE_IP MACHINE_IP`.
- The idle (zombie) scan requires the follow steps to discover whether a port is open:
  - Trigger the idle host to respond to record the current IP ID on the idle host.
  - Send a SYN packet to a TCP port on the target. The packet should be spoofed to appear as if it was coming from the idle host (zombie) IP address.
  - Trigger the idle machine again to respond and compare the new IP ID with the one received earlier.

![idle](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/a93e181f0effe000554a8b307448bbb2.png)

The attacker will send a SYN packet to the TCP port they want to check on the target machine. However, this packet will use the idle host (zombie) IP address as the source. The TCP port below is closed; therefore, the target machine responds to the idle host with an RST packet and the idle host does not respond.

![zombie-IP](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/8e28bf940936ddbc2367b193ea3550b8.png)

Below scenario, the TCP port is open, so the target machine responds with a SYN/ACK to the idle host (zombie). The idle host responds to this unexpected packet with an RST packet.

![zombie-open](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/2b0de492e2154a30760852e07cebae0e.png)

This scan is called an idle scan because choosing an idle host is indispensable for the accuracy of the scan. If the "idle host" is busy, all the returned IP IDs would be useless.

## Getting More Details

Consider adding `--reason` if want Nmap to provide more details regarding its conclusions.

- The flag gives us the explicit reason why Nmap concluded the system is up or a particular port is open.
- For more detailed output, consider using `-v` for verbose output or `-vv` for even more verbosity.
  - Use `-d` for debugging details or `-dd` for even more details on output that extends beyond a single screen.

## Summary

| Port Scan Type                 | Example Command                                       |
| ------------------------------ | ----------------------------------------------------- |
| TCP Null                       | `sudo nmap -sN MACHINE_IP`                            |
| TCP FIN                        | `sudo nmap -sF MACHINE_IP`                            |
| TCP Xmas                       | `sudo nmap -sX MACHINE_IP`                            |
| TCP Maimon                     | `sudo nmap -sM MACHINE_IP`                            |
| TCP ACK                        | `sudo nmap -sA MACHINE_IP`                            |
| TCP Window                     | `sudo nmap -sW MACHINE_IP`                            |
| Custom TCP                     | `sudo nmap --scanflags URGACKPSHRSTSYNFIN MACHINE_IP` |
| Spoofed Source IP              | `sudo nmap -S SPOOFED_IP MACHINE_IP`                  |
| Spoofed MAC Address            | `--spoof-mac SPOOFED_MAC`                             |
| Decoy                          | `nmap -D DECOY_IP,ME MACHINE_IP`                      |
| Idle (Zombie)                  | `sudo nmap -sI ZOMBIE_IP MACHINE_IP`                  |
| Fragment IP data into 8 bytes  | `-f`                                                  |
| Fragment IP data into 16 bytes | `-ff`                                                 |

  
| Option                   | Purpose                                  |
| ------------------------ | ---------------------------------------- |
| `--source-port PORT_NUM` | Specify source port number               |
| `--data-length NUM`      | Append random data to reach given length |

These scan types rely on setting TCP flags in unexpected ways to prompt ports for a reply. Null, FIN, and Xmas scan provoke a response from closed ports, while Maimon, ACK, and Window scans provoke a response from open and closed ports.

| Option     | Purpose                               |
| ---------- | ------------------------------------- |
| `--reason` | Explains how Nmap made its conclusion |
| `-v`       | Verbose                               |
| `-vv`      | Very verbose                          |
| `-d`       | Debugging                             |
| `-dd`      | More details for debugging            |