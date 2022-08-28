---
id: 6qcnpb0kgvgnegg7bf01tku
title: Active Reconnaissance
desc: ''
updated: 1659153063444
created: 1659076308516
---

# Introduction

Focus on active reconnaissance and the essential tools related to it. We learn to use a web browser to collect more information about our target - Using simple tools such as `ping`, `traceroute`, `telnet`, and `nc` to gather information about the network, system, and services.

Active reconnaissance requires to make some kind of contact with the target. Examples could be:

- Phone call or visit to the target company to gather more information in part of social engineering.
- Alternatively, a direct connection to the target system, visiting their website or checking if their firewall has an SSH port open.

## Web Browser

The web browser is a tool readily available on all systems to gather information about a target.

On the transport level, the browser connects to:

- TCP port 80 by default when the website is accessed over HTTP.
- TCP port 443 by default when the website is accessed over HTTPS.

Since the default ports for HTTP and HTTPS are not shown in the address bar, it is possible to custom ports to access a service.

While browsing a web page, you can use `CTRL+SHIFT+I` on PC or `OPTION+COMMAND+I` on a Mac to open the Developer Tools on Firefox. Similar shortcuts will also work with Google Chrome or Chromium browser.

- Developer tools allows to inspect many things the browser has received and exchanged with the remote server.
  - Can view and modify the JavaScript (JS) files, inspect cookies and discover the folder structure of the site content.

There are also plenty of add-ons for Firefox and Chrome that can help in penetration testing:

- FoxyProxy lets you quickly change the proxy server you are using to access the target website. Helpful using a tool such as Burp Suite or need to switch proxy servers regularly.
- User-Agent Switcher and Manager gives the ability to pretend to be accessing the webpage from a different operating system or different web browser.
- Wappalyzer provides insights about the technologies used on the visited websites.

## Ping

The primary purpose of ping is to check whether you can reach the remote system and that the remote system can reach you back. In simple terms, the ping command sends a packet to a remote system, and the remote system replies. This means the remote system is online and the network can communicate between the two systems.

The ping is a command that sends an ICMP Echo packet to a remote system. If the remote system is online, and the ping packet was correctly routed and not blocked by any firewall, the remote system should send back an ICMP Echo Reply. Similarly, the ping reply should reach the first system if appropriately routed and not blocked by any firewall.

- The objective of the command is to ensure that the target system is online before we spend time carrying out more detailed scans to discover the running operating system and services.
  - `ping MACHINE_IP` or `ping HOSTNAME`.
    - If you don't specify the count on a Linux system, you will need to hit `CTRL+C` to force it to stop.
    - `ping -c 10 MACHINE_IP` to send 10 packets.
- If the target computer is shut down, each ping will respond with "Destination Host Unreachable".
- Many possible reasons to not get a reply back.
  - Still booting up, turned off, or the OS has crashed.
  - Unplugged from the network, faulty network device across the path.
  - A firewall is configured to block such packets. The firewall might be apiece of software running on the system itself or a separate network appliance. MS Windows firewall blocks ping by default.

## Traceroute

The traceroute command _traces the route_ taken by the packets from your system to another host.

- Purpose is to find IP addresses of routers or hops that a packet traverses as it goes from your system to a target host. 
  - Also reveals the number of routers between the two systems. It is helpful as it indicates the number of hops(routers) between your system and the target host.
    - Route taken by the packets might change as many routers use dynamic routing protocols that adapt to network changes.

On Linux and macOS, the command to use is `traceroute MACHINE_IP`. On MS Windows, `tracert MACHINE_IP`.

There is no direct way to discover the path from your system to a target system. ICMP can 'trick' the routers into revealing the IP addresses by using a small Time to Live (TTL) in the IP header field.

- TTL indicates the maximum number of routers/hops that packet can pass through before being dropped; TTL is not a maximum number of time units.
  - When a router receives a packet, it decrements the TLL by one before passing it to the next router. Initially, it leaves the system with a TTL value of 64; it reaches the target system with a TTL value of 60 after passing through 4 routers.

![ttl](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/e82c42dcfae78ac592a8d7843465d2d6.png)


However, if the TTL reaches 0, it will be dropped, and an ICMP Time-to_live exceeded would be sent to the original sender. In the following figure, the system set TTL to 1 before sending it to the router. The first router on the path decrements the TTL by 1, resulting in a TTL of 0. This router will discard the packet and send an ICMP time exceeded in-transit error message. Note that some routers are configured not to send such ICMP messages when discarding a packet.

![ttl-0](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/948388c823b156813fa30225c2fa3f05.png)

On Linux, `traceroute` will start by sending UDP datagrams within IP packets of TTL being 1. Therefore, a TTL of 1 will reveal the IP address of the first router to you.

To summarize:

- The number of hops/routers between your system and the target system depends on the time running traceroute. There is no guarantee that packets will always follow the same route.
- Some routers return a public IP address.
- Some routers do not return a reply.

## Telnet

The TELNET (Teletype Network) protocol was developed in 1969 to communicate with a remote system via a command-line interface. The default port used by telnet is 23.

- Telnet sends all the data, including usernames and passwords, in cleartext. Sending in cleartext makes it easy for anyone, who has access to the communication channel, to steal the login credentials.
  - The secure alternative is SSH (Secure SHell) protocol.

Telnet relies on the TCP protocol and can be used to connect to any service and grab its banner. Using `telnet MACHINE_IP PORT`, can connect to any service running on TCP and exchange a few messages unless it uses encryption.

To discover more information about a web server, listening on port 80:

- Connect to server at port 80 using the HTTP protocol.
  - Issue `GET / HTTP/1.1`
  - To get a valid response, instead of an error, you need to input some value for the host host: example and hit enter twice. Executing these steps will provide the requested page.
- Can discover the type and version of the installed web server.

## Netcat

Netcat or simply `nc` has different applications that can support both TCP and UDP protocols. It can function as a client that connects to a listening port; alternatively, it can act as a server that listens on a port of your choice.

First, we can connect to a server similar to Telnet with `nc MACHINE_IP PORT` which is similar to telnet.

- `GET / HTTP/1.1` and might have to SHIFT+ENTER after the GET line.
- Can use netcat to listen on a TCP port and connect to a listening port on another system.
  - On the server system, where you want to open a port and listen on it, you can issue `nc -lp 1234` or `nc -lvnp 1234`. The exact order of the letters does not matter as long as port number is preceded directly by `-p`.

| Option | Meaning                                             |
| ------ | --------------------------------------------------- |
| `-l`   | Listen mode                                         |
| `-p`   | Specify the port number                             |
| `n`    | Numeric only; no resolution of hostnames via DNS    |
| `v`    | Verbose output (optional, helpful to discover bugs) |
| `vv`   | Very verbose (optional)                             |
| `k`    | Keep listening after client disconnects             |

- Port numbers less than 2014 require root privileges to listen on.
- Option `-n` will avoid DNS lookups and warnings.