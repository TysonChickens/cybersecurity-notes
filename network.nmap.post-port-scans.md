---
id: zattr5zxwz5ssprivbm7lq7
title: Post Port Scans
desc: ''
updated: 1660273949908
created: 1659932386199
---

# Introduction

Focus on how Nmap can be used to:

- Detect versions of running services (on all ports).
- Detect the OS based on any signs revealed by the target.
- Run Nmap's traceroute.
- Run select Nmap scripts.
- Save the scan results in various formats.

![nmap-progress](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/c9724491cb38c1ebcd83b5b98f13e1d9.png)

## Service Detection

Once Nmap discovers open ports, we can probe the available port to detect the running service.

- Adding `-sV` to Nmap command will collect and determine service and version information for the open ports.
- Can control the intensity with `--version-intensity LEVEL` where the level ranges between 0, the lightest, and 9, the most complete.
  - `-sV --version-light` has an intensity of 2.
  - `-sV --version-all` has an intensity of 9.

`-sV` will force Nmap to proceed with the TCP 3-way handshake and establish the connection. This is necessary because Nmap cannot discover the version without establishing a connection fully and communicating with the listening service.

- Stealth SYN scan `-sS` is not possible when `-sV` option is chosen.

## OS Detection and Traceroute

### OS Detection

Nmap can detect the Operating System (OS) based on its behavior and any signs in its responses.

- OS detection can be enabled using `-O` (`nmap -sS -O MACHINE_IP`).
- Many factors can affect its accuracy such as having at least one open and one closed port on the target.
  - OS fingerprints might get distorted due to the use of virtualization and similar technologies.

### Traceroute

Nmap can find the routers between you and the target using `--traceroute`. Nmap's traceroute works slightly different than the `traceroute` command found on Linux and macOS or `tracert` found on MS Windows.

- Standard `traceroute` starts with a packet of low TTL (Time to Live) and keeps increasing until it reaches the target.
- Nmap's traceroute starts with a packet of high TTL and keeps decreasing it.
- Many routers are configured not to send ICMP Time-to-Live exceeded, which would prevent us from discovering their IP addresses.

## Nmap Scripting Engine (NSE)

A script is a piece of code that does not need to be compiled. It remains in original human-readable form and does not need to be converted to machine language. Nmap provides support for scripts using the Lua language.

- Part of Nmap, Nmap Scripting Engine (NSE) is a Lua interpreter that allows Nmap to execute Nmap scripts written in Lua language. However, we do not need to learn Lua to make use of Nmap scripts.
- Nmap default installation can contain close to 600 scripts. The default installation at `/usr/share/nmap/scripts` and expect the number of installed scripts to increase with updates.
- Can specify to use any group of these installed scripts or install other user's scripts.
  - Choose to run the scripts in the default category using `--script=default` or adding `-sC`.
    - Can specify the script by name using `--script "SCRIPT-NAME"` or a pattern such as `--script "ftp"`.
  - Categories include auth, broadcast, brute, default, dos, exploit, external, fuzzer, intrusive, malware, safe, version, and vuln.

| Script Category | Description                                                            |
| --------------- | ---------------------------------------------------------------------- |
| auth            | Authentication related scripts                                         |
| broadcast       | Discover hosts by sending broadcast messages                           |
| brute           | Performs brute-force password auditing against logins                  |
| default         | Default scripts, same as `-sC`.                                        |
| discovery       | Retrieve accessible information, such as database tables and DNS names |
| dos             | Detects servers vulnerable to Denial of Service (DoS)                  |
| exploit         | Attempts to exploit various vulnerable services                        |
| external        | Checks using a third-party service, such as Geoplugin and Virustotal   |
| fuzzer          | Launch fuzzing attacks                                                 |
| intrusive       | Intrusive scripts such as brute-force attacks and exploitation         |
| malware         | Scans for backdoors                                                    |
| safe            | Safe scripts that won't crash the target                               |
| version         | Retrieve service versions                                              |
| vuln            | Checks for vulnerabilities or exploit vulnerable services              |

If you are unsure what a script does, open the script file with a text reader, such as `less`, or a text editor.

## Saving the Output

When you run an Nmap scan, it is possible to save the results in a file. The three main formats are:

1. Normal
2. Grepable (`grep` able)
3. XML

There is a fourth one called Script Kiddie that is not recommended.

### Normal

The normal format is similar to the output seen on the screen when scanning a target.

- Save the scan in normal format using `-oN FILENAME`; N stands for normal.

### Grepable

The grepable format has its name from the command `grep`; grep stands for Global Regular Expression Printer.

- Makes filtering the scan output for specific keywords or terms efficient.
- Save the scan in grepable format using `-oG FILENAME`

### XML

Save the results in XML format using `-oX FILENAME`. The XML format would be most convenient to process the output in other programs.

- Can save the output in all three formats using `-oA FILENAME` to combine for normal, grepable, and XML.

## Summary

- How to detect running services and their versions along with host operating systems.
- Enable traceroute and utilizing Nmap scripts to aid in penetration testing.
- Save output scans for future reference.

| Option                      | Meaning                                          |
| --------------------------- | ------------------------------------------------ |
| `-sV`                       | Determine service/version info on open ports     |
| `-sV --version-light`       | Try the most likely probes                       |
| `-sV --version-all`         | Try all available probes                         |
| `-O`                        | Detect OS                                        |
| `-traceroute`               | Run traceroute to the target                     |
| `--script=SCRIPTS`          | Nmap scripts to run                              |
| `-sC` or `--script=default` | Run default scripts                              |
| `-A`                        | Equivalent to `-sV -O -sC --traceroute`          |
| `-oN`                       | Save output in normal format                     |
| `-oG`                       | Save output in grepable format                   |
| `-oX`                       | Save output in XML format                        |
| `-oA`                       | Save output in normal, XML, and Grepable formats |