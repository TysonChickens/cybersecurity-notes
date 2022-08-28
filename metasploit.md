---
id: 9k9gs0zqcs40mq2fsi5nesj
title: Metasploit
desc: ''
updated: 1654728330205
created: 1654385766338
---

# Introduction to Metasploit

Metasploit in the most widely exploitation framework - A powerful tool that can support all phases of penetration testing, from information gathering to post-exploitation.

Two main versions:

1. **Metasploit Pro**: The commercial version that facilitates the automation and management of tasks.
2. **Metasploit Framework**: The open-source version that works from the command line.

The Metasploit Framework is a set of tools that allow information gathering, scanning, exploitation, exploit development, post-exploitation, and more.

The main components summarized below:

- **msfconsole**: The main command-line interface.
- **Modules**: Supporting modules such as exploits, scanners, payloads, etc.
- **Tools**: Stand-alone tools that will vulnerability research, vulnerability assessment, or penetration testing.

## Main Components of Metasploit

**Exploit**
: A piece of code that uses a vulnerability present on the target system.

**Vulnerability**
: A design, coding, or logic flaw affecting the target system.

**Payload**
: An exploit will take advantage of a vulnerability via a payload. Payloads are the code that will run on the target system.

### Auxiliary

Any supporting module, such as scanners, crawlers and fuzzers.

### Encoders

Allow to encode the exploit and payload in the hope that a signature-based antivirus solution may miss them.

Signature-based antivirus and security solutions have a database of known threats.

- They detect by comparing suspicious files to a database and raise an alert if there is a match.

### Evasion

While encoders will encode the payload, they should not be considered a direct attempt to evade antivirus software.

- 'Evasion' modules will try with more or less success.

### Exploits

Exploits neatly organized by the target system.

### NOPs (No OPeration)

Intel x86 CPU represented with 0x90, to tell the CPU do nothing for one cycle.

- Used as a buffer to achieve consistent payload sizes.

### Payloads

Code that will run on the target system. Examples could be:

- Getting a shell
- Loading a malware or backdoor
- Running a command

Running a command on the target system to allow Metasploit to send different payloads that can open shells on the target system.

#### Singles

Self-contained payloads (add user, launch notepad.exe, etc.) that do not need to download any additional component to run.

#### Stagers

Responsible for setting up a connection channel between Metasploit and the target system.

- Provides some advantages as the initial size of the payload will be relatively small compared to the the full payload sent at once.

#### Stages

Downloaded by the stager to allow larger sized payloads.

### Post

Post modules will be useful on the final stage of penetration testing process.

## Msfconsole

`msfconsole` command on terminal or any system with the Metasploit Framework is installed on to activate.

- The Metasploit console can be used just like a regular command-line shell.

### Working with Modules
