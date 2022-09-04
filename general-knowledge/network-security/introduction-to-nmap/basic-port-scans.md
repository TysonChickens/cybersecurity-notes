# Basic Port Scans

### TCP and UDP Ports

A TCP port or UDP port is used to identify a network service running on that host. A port is usually linked to a service using that specific port number.

* HTTP server = TCP port 80 by default.
  * HTTP/S server supports SSL/TLS = TCP port 443.

For oversimplification, we can classify ports in two states:

1. Open: A service listening on that port.
2. Closed: There is no service listening on that port.

In practical situations, we need to consider the impact of firewalls. A firewall might be blocking the packets and Nmap considers the following 6 states:

1. **Open**: Indicates that a service is still listening on that specified port.
2. **Closed**: No service is listening on the specified port, although the port is accessible. It is reachable and is not blocked by a firewall or other security appliances/programs.
3. **Filtered**: Nmap cannot determine if the port is open or closed because the port is not accessible. Usually due to a firewall preventing Nmap from reaching that port.
4. **Unfiltered**: Nmap cannot determine if the port is open or closed, although the port is accessible. Encountered when using an ACK scan `-sA`.
5. **Open|Filtered**: Nmap cannot determine whether the port is open or filtered.
6. **Closed|Filtered**: Nmap cannot decide whether a port is closed or filtered.

### TCP Flags

Nmap supports different types of TCP port scans. The TCP header is the first 24 bytes of a TCP segment. The following figure shows the TCP header as defined as [RFC 793](https://datatracker.ietf.org/doc/html/rfc793.html).

* In the first row is the source TCP port number and the destination port number.
  * The port number is allocated 16 bits (2 bytes).
* In the second and third rows, sequence number and the acknowledgement number.
  * Each row has 32 bits (4 bytes) allocated, with six rows total, making up 24 bytes. ![TCP-Header](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/79ca8e4acbd573a27cee413cde927769.png)

From left to right, the highlighted TCP flags in red - setting a flag bit means settings its value to 1. The TCP header flags are:

1. **URG**: Urgent pointer indicates that the incoming data is urgent, and a TCP segment with the URG flag set is processed immediately without consideration of having to wait on previously sent TCP segments.
2. **ACK**: Acknowledgement flag indicates that the acknowledgement of the receipt of a TCP segment.
3. **PSH**: Push flag asking TCP to pass the data to the application promptly.
4. **RST**: Reset flag is used to reset the connection. This flag is used when data is sent to a host and there is no service on the receiving end to answer.
5. **SYN**: Synchronize flag is used to initiate a TCP 3-way handshake and synchronize sequence numbers with the other host. The sequence number should be set randomly during TCP connection establishment.
6. **FIN**: The sender has no more data to send.

### TCP Connect Scan

TCP connect scan works by completing the TCP 3-way handshake. The client sends a TCP packet with SYN flag set, and the server responds with SYN/ACK if the port is open; the client completes the 3-way handshake by sending an ACK.

![3-way-handshake](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/8390020a13d6f22f49233833f6265de6.png)

Can choose to run TCP connect scan using `-sT` to avoid establishing a TCP connection by sending a RST/ACK.

![RST/ACK](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/514972cd54b3f58c83f951978ea9183e.png)

TCP connect scan is the only possible option to discover open TCP ports if you are not a privileged user (root or sudoer).

Option `-F` to enable fast mode and decrease the number of scanned ports from 1000 to 100 most common ports.

* Option `-r` can also be added to scan the ports in consecutive order instead of random order.

### TCP SYN Scan

Unprivileged users are limited to connect scan. However, the default scan mode is SYN scan, and it requires a privileged (root or sudoer) user to run it.

* SYN scan does not need to complete the 3-way handshake.
  * Breaks the connection once it receives a response from the server.
    * Since there is no established TCP connection, this decreases the chances of the scan being logged.
* Scan type using the `-sS` option. The figure below shows how the TCP SYN scan works without completing the TCP 3-way handshake. ![TCP-SYN](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/48e631fd3deba4a2b759ca48405fcc08.png)

### UDP Scan

UDP is a connection-less protocol and it does not require any handshake for connection establishment.

* Cannot guarantee that a service listening on UDP port would respond to our packets.
  * If a UDP packet is sent to a closed port, an ICMP port unreachable error (type 3, code 3) is returned.
* Use UDP scan option `-sU` and possible to combine it with another TCP scan. ![UDP](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/085088cd1b2b122312b1ee952c4aa0f7.png)

### Fine-Tuning Scope and Performance

Instead of the default 1000 ports, it is possible to specify the ports scanned:

* Port list: `-p22,80,443` will scan ports 22, 80, and 443.
* Port range: `-p1-1023` will scan all ports between 1 and 1023 inclusive.
* Scan all 65535 ports with `-p-`
  * TO scan the most common 100 ports, add `-F` and using `--top-ports 10` will check the ten most common ports.

Can also control the scan timing using `-T<0-5>`. `-T0` is the slowest (paranoid), while `-T5` is the fastest. According to Nmap manual page, there are 6 templates:

1. Paranoid (0) - Scans one port at a time and waits 5 minutes between sending each probe.
2. Sneaky (1)
3. Polite (2)
4. Normal (3)
5. Aggressive (4)
6. Insane (5)

To avoid IDS alerts, consider options `-T0` or `-T1`. If you do not specify any timing, Nmap uses normal `-T3`. Note that `-T5` is the most aggressive in terms of speed; this can affect the accuracy of the scan results due to the increased likelihood of packet loss.

Can alternatively control the packet rate using `--min-rate <number>` and \`--max-rate .

In addition, control probing parallelization using `--min-parallelism <numprobes>` and \`--max-parallelism . Nmap probes the targets to discover which hosts are live and which ports are open.

### Summary

3 types of scans:

| Port Scan Type | Example Command            |
| -------------- | -------------------------- |
| TCP Connect    | `nmap -sT MACHINE_IP`      |
| TCP SYN        | `sudo nmap -sS MACHINE_IP` |
| UDP            | `nmap -sU MACHINE_IP`      |

*   Scan type options to discover TCP and UDP services on a target host.

    | Option                  | Purpose                                  |
    | ----------------------- | ---------------------------------------- |
    | `-p-`                   | All ports                                |
    | `-p1-1023`              | Scan ports 1 to 1023                     |
    | `-F`                    | 100 most common ports                    |
    | `-r`                    | Scan ports in consecutive order          |
    | `T<0-5>`                | -T0 being the slowest and T5 the fastest |
    | `--max-rate 50`         | Rate does not exceed over 50 packets/sec |
    | `--min-rate 15`         | Minimum rate of at least 15 packets/sec  |
    | `--min-parallelism 100` | At least 100 probes in parallel          |
