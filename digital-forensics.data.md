---
id: 2tx6kae8dfako6nl9lbcyup
title: Data
desc: ''
updated: 1656764538094
created: 1653180168836
---

# Data Files

- [ ] Learn about the different file systems.
- [ ] Learn what method are used for gathering and preserving the integrity of files.
- [ ] Learn about what metadata from files can be useful.
- [ ] Learn what techniques forensic tool-kits can perform for data analysis.

- [ ] Learn about the different volatile and non-volatile data in Operating Systems.
- [ ] Learn about the different Operating Systems.
- [ ] Learn about what log information may be useful.

- [ ] Learn about the different components of an application and how they are meaningful to a forensic analyst.
- [ ] Learn about the different types of applications that provide meaningful forensic data.
- [ ] Learn what considerations are taken when collecting application data.

- [ ] Review TCP/IP basics and how it relates to forensics.
- [ ] Learn about the different sources of network traffic.
- [ ] Learn about examining and analyzing network traffic.


---

A file can be of many data types, including a document, an image, a video, or an application. Successful forensic processing computer media depends on the ability to collect, examine, and analyze the files that reside on the media. - *NIST 800-86*

## File Systems

A file system defines the way that files are named, stored, organized, and accessed on logical volumes.

### Windows

Windows is a widely used OS designed by Microsoft. The file systems used by Windows:

- FAT
  - 12
  - 16
  - 32
- NTFS
- ReFS

Investigators can search out evidence by analyzing the following important locations of Windows:

- Recycle Bin
- Registry
- Thumbs.db
- Files
- Browser History
- Print Spooling

### UNIX

- EXT
  - 2
  - 3
  - 4
- ReiserFS
- XFS
- JFS
- Btrfs

### macOS

Mac OS X is the UNIX-based operating system that contains a Mach 3 micro-kernel and a FreeBSD based subsystem. Its user interface is Apple like, whereas the underlying architecture is UNIX like.

- Mac OS X offers a novel technique to create a forensic duplicate. To do so, the perpetrator's computer should be placed into a "Target Disk Mode." Using this mode, the forensic examiner creates a forensic duplicate of perpetrator's hard disk with the help of a FireWire cable connection between the two PCs.

- HFS+
- APFS

### Linux

Linux is an open source, UNIX-like, ad elegantly designed operating system that is compatible with personal computers, supercomputers, server, mobile devices, netbooks, and laptops.

- Unlike other OSs, Linux holds many file systems of the ext family, including ext2, ext3, and ext4.
- Linux can provide an empirical evidence if the Linux embedded machine is recovered from a crime scene. In this  case, forensic investigators should analyze the following folders and directories.
  - `/etc[%SystemRoot%/System32/config]` contains system configurations directory that holds separate configuration files for each application.
  - `/var/log` directory contains application logs and security logs (kept for 4-5 weeks).
  - `/home/$USER` holds user data and configuration information.
  - `/etc/passwd` has user account information.

### What is not There

- **Deleted files** - When a file is deleted, it is typically not erased from the media; instead, the information in the directory's data structure that points to the location of the file is marked as deleted.
- **Slack Space** - If a file requires less space than the file allocation unit size, an entire file allocation unit is still reserved for the file.
 - **Free Space** - Free space is the area on media that is not allocated to any partition. The free space may still contain pieces of data.
 - **MAC Data** - Important to know as much information about relevant files as possible. Recording the Modification, Access, and Creation times of files allows analysts to help establish a timeline of the incident.
    1. Modification Time
    2. Access Time
    3. Creation Time

## Logical Backup

A logical backup copies the directories and files of a logical volume. It does not capture other data that may be present on the media, such as deleted files or residual data stored in slack space.
- Can be used on live system if using a standard backup software.
- May be resource intensive.

## Imaging

Generates a bit-for-bit copy of the original media, including free space and slack space. Bit stream images require more storage space and take longer to perform logical backups.
- If evidence is needed for legal or HR reasons, a full bit stream image should be taken, and all analysis done on the duplicate.
- Disk-to-Disk vs Disk-to-File
- Should not be used on a live system since data is always changing.

## Tools for Techniques

Many forensic products allow the analyst to perform a wide range of processes to analyze files and application, as well as collecting files, reading disk images, and extracting data from files.

1. File Viewers
2. Un-compressing files
3. GUI for Data Structures
4. Identifying Known Files
5. String Searches & Pattern Matches
6. Metadata

## Operating System Data

> OS data exists in both non-volatile and volatile states. Non-volatile data refers to data that persists even after a computer is powered down, such as a filesystem stored on a hard drive. Volatile data refers to data on a live system that is lost after a computer is powered down, such as the current network connections to and from the system. - *NIST 800-86*

### Volatile

- Slack Space
- Free Space
- Networking Configuration/Connections
- Running Processes
- Open Files
- Login Sessions
- Operating System Time

#### Collection & Prioritization of Volatile Data

1. Network Connections
2. Login Sessions
3. Contents of Memory
4. Running Processes
5. Open Files
6. Network Configuration
7. Operating System Time

### Non-Volatile

- Configuration Files
- Logs
- Application files
- Data Files
- Swap Files
- Dump Files
- Hibernation Files
- Temporary Files

#### Collecting Non-Volatile Data

1. Consider Power-Down Options
2. File System Data Collected
3. Users and Groups
4. Passwords
5. Network Shares
6. Logs
   - Other logs can be collected depending on the incident under analysis.
     1. Network Hack - Collect logs of all the network devices lying in the route of the hacked device and the perimeter router (ISP router). firewall rule base may also be required in this case.
     2. Unauthorized Access - Save the web server logs, application server logs, application logs, router or switch logs, firewall logs, database logs, IDS logs etc.
     3. Trojan / Virus / Worm Attack - Save the antivirus logs apart from the event logs (pertaining to the antivirus).

## Application Data

> OSs, files and networks are all needed to support applications" OSs to run the applications, networks to send application data between systems, and files to store application data, configuration settings, and logs. From a forensic perspective, applications bring together files, OSs, and networks. - NIST 800-86

### Application Components

- Config Settings
  - Configuration File
  - Runtime Options
  - Added to Source Code
- Authentication
  - External Authentication
  - Proprietary Authentication
  - Pass-through Authentication
  - Host/User Environment
- Logs
  - Event
  - Audit
  - Error
  - Installation
  - Debugging
- Data
  - Can live temporarily in memory and/or permanently in files.
  - File format may be generic or proprietary.
  - Data may be stored in databases.
  - Some applications create temp files during session or improper shut down.
- Supporting Files
  - Documentation
  - Links
  - Graphics
- App Architecture
  - Local
  - Client/Server
  - Peer-to-Peer

### Types of Applications

Certain types of applications are more likely to be the focus of forensic analysis, including e-mail, web usage, interactive messaging, file sharing, document usage, security applications, and data concealment tools.

- Email: From end-to-end, information regarding a single e-mail message may be recorded in several places - the sender's system, each email server that handles the message, and the recipient's system, as well as the antivirus, spam, and content filtering servers." - *NIST 800-45*

- Web usage
  - Web data from Host: Typically, the richest sources of information regarding Web usage the hosts running the Web Browsers.
    - Favorite websites
    - History with time stamps of websites visited
    - Cached web data files
    - Cookies
  - Web data from Server: Another good source of web usage information is web servers, which typically keep logs of the requests they receive.
    - Timestamps
    - IP addresses
    - Web browser version
    - Type of request
    - Resource requested
- Interactive Communications
  - Group Chat: Typically uses a client/server architecture. The most popular standard group chat protocol for simple text-based communication is Internet Relay Chat (IRC).
  - Instant Messaging Applications: IM application configuration settings may contain user information, lists of users that the user has communicated with, file transfer information, and archived messages or chat sessions.
  - Audio & Video:
    - Technologies such as Voice over IP (VoIP) permit people to conduct telephone conversations over networks such as the Internet.
- File Sharing
- Document Usage
- Security Applications
- Data Concealment Tools

#### Collecting Application Data

- Filesystem
- Volatile OS Data
- Network Traffic

## Network Data

> Analysis can use data from network traffic to reconstruct and analyze network-based attacks and inappropriate network usage, as well as to troubleshoot various types of operational problems... The term network traffic refers to computer network communications that are carried over wired or wireless networks between hosts. - *NIST 800-86*

### TCP/IP

Application Layer
: Sends and receives data for particular applications, such as Domain Name System (DNS), Hypertext Transfer Protocol (HTTP), and Simple Mail Transfer Protocol (SMTP).

Transport Layer
: Provides connection-oriented or connection-less services for transporting application layer services between networks. The transport layer can optionally ensure the reliability of communications. TCP and UDP are commonly used transport layer protocols.

Internet Protocol Layer (also known as Network Layer)
: Routes packets across network as IP is the fundamental network layer protocol for TCP/IP. Other commonly used protocols at the network layer are Internet Control Message Protocol (ICMP) and Internet Group Management Protocol (IGMP).

Hardware Layer (also known as Data Link Layer)
: Handles communications on the physical network components. The best known data link layer protocol is Ethernet.

#### Sources of Network Data

These sources collectively capture important data from all four TCP/IP layers.

- Firewalls & Routers
- Packet Sniffers & Protocol Analyzers
- Intrusion Detection System
- Security Event Management Software
- Network Forensic Analysis Tools
- Remote Access

### Attacker Identification

- Contact IP Address Owner - Can help identify who is responsible for an IP address. Usually an escalation.
- Seek ISP Assistance - Requires court order and is only done to assist in the most serious attacks.
- Send Network Traffic - Not recommended for organizations.
- History of IP address - Can look for trends of suspicious activity.
- Application Content - Data packets could contain information about the attacker's identity.
