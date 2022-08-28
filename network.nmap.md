---
id: zegnyfq64amprq2yq9rnu3e
title: Nmap
desc: ''
updated: 1655599671365
created: 1654835317617
---

# Introduction to Nmap

When it comes to hacking, knowledge is power. The more knowledge about a target system or network, the more options are available.

- 'Map' or landscape is called port scanning.
  - When a computer runs a network service, it opens a networking construct called a 'port' to receive the connection. Ports are necessary for making multiple network requests or having multiple services available.
- Network connections are made between two ports - an open port listening on the server and a randomly selected port on your own computer.
  - When you connect to a web page, your computer may open port 49534 to connect to the server's port 443.
- ![ports](https://i.imgur.com/3XAfRpI.png)

Every computer has a total of 65535 available ports; however, many of these are registered as standard ports.

- For example, a HTTP web service can nearly always be found on port 80 of the server.
- HTTPS web service on port 443.
- Windows NETBIOS on port 139 and SMB on port 445.

We begin any attack with a port scan using a tool called nmap. Nmap will connect to each port of the target in turn. Depending on how the port responds, it can be determined as being open, closed, or filtered (usually by a firewall).

- nmap is the industry standard and is a powerful tool with its scripting engine which can be used to scan for vulnerabilities, and some perform exploit directly.

## Nmap Parameters

- `-sS` = Syn scan
- `-sU` = UDP scan
- `-O` = Detect operating system
- `-sV` = Detect version of the services running
- `-v` = Increase verbosity level 1
- `-vv` = Verbosity level 2
- `-oA` = Save the nmap results in three major formats
- `-oN` = Save nmap results in a 'normal' format
    - `-oG` = A useful output to save results in a 'grepable' format
- `-A` = Aggressive mode to activate service detection, operating system detection, traceroute and common script scanning.
- `-T5` = Set timing template to increase the speed scans run at to level 5.
- `-p 80` = Scan only port 80
- `-p 1000-1500` = Scan ports 1000-1500
- `-p-` = Scan all ports
- `--script` = Activate a script from the nmap scripting library
- `--script=vuln` = Activate all the scripts in the 'vuln' category

## Scan Types Overview

Three basics scan types when port scanning with Nmap:

1. TCP Connect Scans (`-sT`)
2. SYN 'Half-open' Scans (`-sS`)
3. UDP Scans (`-sU`)

Additionally, there are several less common port scans:

- TCP Null Scans (`-sN`)
- TCP FIN Scans (`sF`)
- TCP Xmas Scans (`sX`)

Most of these are used for very similar purposes but differs between each scan.

### TCP Connect Scans

Understanding the TCP three-way handshake when doing TCP Connect scans `-sT`.

1. The attacking machine sends a TCP request to the target server with the SYN flag set.
2. The server acknowledges this packet with a TCP response containing the SYN flag, as well as the ACK flag.
3. Completes the handshake by sending a TCP request with the ACK flag set.

![handshake](https://muirlandoracle.co.uk/wp-content/uploads/2020/03/image-2.png)

If the port is closed, the target server will respond with a TCP packet with the _RST (Reset)_ flag set.

- Many firewalls are configured to drop incoming packets. Nmap sends a TCP SYN request, and receives nothing back. This indicates the port is being protected by a firewall and the port is considered to be _filtered_ - if the port is open and hidden behind a firewall


### SYN Scans

SYN scans are sometimes referred to as 'half-open' or 'stealth' scans.

TCP scans perform a full three-way-handshake with the target and SYN scans sends back a RST TCP packet after receiving SYN/ACK from the server.

#### Advantages

- Bypass older Intrusion Detection systems as they look for a full three-way-handshake.
  - No longer the case with modern IDS solutions.
  - SYN scans are often not logged by applications listening on open ports, as standard practice is to log a connection once it has been fully established.
- Scans are significantly faster than a standard TCP Connect scan.

#### Disadvantages

- Require sudo permissions to work correctly in Linux. SYN scans require the ability to create raw packets (opposed to the full TCP handshake).
- Unstable services are sometimes brought down by SYN scans - problematic if a client is a production environment.

All the pros outweigh the cons since SYN scans are the default scans used by Nmap _if run with sudo permissions_.

### UDP Scans

Unlike TCP, UDP connections are _stateless_. UDP connections rely on sending packets to a target port and essentially hoping they make it.

- UDP is best for connections which rely on speed over quality (e.g. video sharing) but the lack of acknowledgement makes more difficult and slower to scan.

When a packet is sent to an open UDP port, there should be no response. Nmap refers to the port as being `open|filtered`.

When a packet is sent to a closed UDP port, the target should respond with an ICMP (ping) packet containing a message that the port is unreachable.

### ICMP Network Scanning

Purpose to see which IP addresses contain active hosts, and which do not.

Nmap can perform a "ping sweep" to send ICMP packet to each possible IP address for the specified network.

- When it receives a response, it marks the IP address that responded as being alive.
- Perform a ping sweep with `nmap -sn 192.168.0.1-254` on IP ranges specified with a hyphen or CIDR notation.
  - `-sn` tells Nmap not to scan any ports - forcing it to only ICMP echo packets to identify targets.

## NSE Scripts Overview

The Nmap Scripting Engine (NSE) is an incredible powerful addition to Nmap. NSE scripts are written in the Lua programming language, and can be used for a variety of things: scanning for vulnerabilities, to automating exploits for them. NSE is useful for reconnaissance and includes many categories:

- `safe` - Will not affect the target
- `intrusive` - Not safe: likely to affect the target
- `vuln` - Scan for vulnerabilities
- `exploit` - Attempt to exploit a vulnerability
- `auth` - Attempt to bypass authentication for running services
- `brute` - Attempt to brute force credentials for running services
- `discovery` - Attempt to query running services for further information about the network

A more detailed list can be found [here](https://nmap.org/book/nse-usage.html).

### Working with the NSE

- `--script=safe` will run any applicable safe scripts against the target or any specified category.
- To run a specific script, we would use `--script=<script-name>`.
  - Multiple scripts can be run simultaneously by separating them by a comma.

A full list of scripts and example use cases can be found [here](https://nmap.org/nsedoc/).

### Searching for Scripts

All of the official scripts on Linux at `/usr/share/nmap/scripts`.

- Use grep to look for scripts: `grep 'ftp' /usr/share/nmap/scripts/script.db`
- Use `ls`: `ls -l /usr/share/nmap/scripts/*ftp*`

### Installing New Scripts

It is possible to install the scripts manually by downloading the script from Nmap (`sudo wget -O /usr/share/nmap/scripts/<script-name>.nse https://svn.nmap.org/nmap/scripts/<script-name>.nse`)

- This must be followed up with `nmap --script-updatedb` which updates the _script.db_ file to contain the new downloaded script.