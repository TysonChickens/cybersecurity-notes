# Types of Network Attacks

Servers implementing these protocols are subject to different kinds of attacks such as:

* Sniffing Attack (Network Packet Capture)
* Man-in-the-Middle (MITM) Attack
* Password Attack (Authentication Attack)
* Vulnerabilities

We always need to think about what we aim to protect: Confidentiality, Integrity, and Availability (CIA).

**Confidentiality** : Keeping contents of the communications accessible to the intended parties.

**Integrity** : Assuring any data sent is accurate, consistent, and complete when reaching its destination.

**Availability** : Ability to access the service when we need it.

Different parties will put varying emphasis on each one.

![CIA](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/992438a051d1355cf1146705557b457d.png)

* An attack aims to cause Disclosure, Alternation, and Destruction (DAD).
* These attacks directly affect the security of the system.
  * For instance, a network packet capture violates confidentiality and leads to the disclosure of information.
  * Meanwhile, a Man-in-the-Middle (MITM) attack breaks the system's integrity as it can alter the communicated data.

Vulnerabilities and exploited vulnerabilities have different impacts on the target systems.

* DoS or Denial of Service vulnerability can affect the system's availability.
* A Remote Code Execution (RCE) vulnerability can lead to more severe damages.
* Important to note a vulnerability itself creates a risk; damage can occur only when the vulnerability is exploited.

## Sniffing Attack

Sniffing refers to using a network packet capture tool to collect information about the target. When a protocol communicates in cleartext, the data exchanged be captured by a third party to analyze. If the data is not encrypted in transit, a simple network packet capture can reveal information, such as the content of private messages and login credentials.

A sniffing attack can be conducted using an Ethernet (802.3) network card, provided the user has proper permissions (root permissions on Linux and administrator privileges on MS Windows). There are many programs available to capture network packets such as:

* Tcpdump is a free open source command-line interface (CLI) program that has been ported to work on many operating systems.
* Wireshark is a free open source graphical user interface (GUI) program available for several operating systems, including Linux, macOS, and MS Windows.
* Tshark is a CLI alternative to Wireshark.

For Tcpdump to capture the username and password, use `sudo tcpdump port 110 -A` on POP3. This attack requires access to the network traffic, via a wiretap or a switch with port mirroring.

* We need `sudo` as packet captures require root privileges.
* POP3 server uses port 110.
* ASCII format `-A`.

![wireshark](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/c1ec79277c1f02beeb20f7dc81df2fd3.png)

Wireshark window explicitly displays "USER frank", and the last packet reveals the password "PASS D2xc9CgD" and also filtered traffic by "pop".

Any protocol that uses cleartext communication is susceptible to this kind of attack. The only requirement for this attack to succeed is to have access to a system between the two communicating systems. This attack requires attention; the mitigation adding an encryption layer on top of any network protocol.

* Transport Layer Security (TLS) has been added to HTTP, FTP, SMTP, POP3, IMAP and many others.
* For remote access, Telnet has been replaced by the secure alternative Secure Shell (SSH).

## Man-in-the-Middle (MITM) Attack

Attack occurs when a victim (A) believes they are communicating with a legitimate destination (B), but is unknowingly communicating with an attacker (E).

![MITM](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/3cb0c4f9dde184bf8dcd6b3a45418a44.png)

* Computer A is requesting the transfer of $20 to Computer M; However, Computer E altered this message and replaced the original with a new one.
* Computer B received the modified messaged and acted on it.

This attack is relatively simple to carry out if the two parties do not confirm the authenticity and integrity of each message.

* Any time browse over HTTP, is susceptible to a MITM attack, and will not be able to recognize it. Many tools aid in carrying out such an attack, such as [Ettercap](https://www.ettercap-project.org/) and [Bettercap](https://www.bettercap.org/).
* MITM can also affect other cleartext protocols such as FTP, SMTP, and POP3.
  * Mitigation against this attack requires the use of cryptography. The solution relies on proper authentication along with encryption or signing of the exchanged messages - Public Key Infrastructure (PKI) and trusted root certificates, Transport Layer Security (TLS) protects from MITM attacks.

## Transport Layer Security (TLS)

Can protect confidentiality and integrity against password sniffing and MITM attacks.

SSL (Secure Sockets Layer) started when the world wide web started to see new applications, such as online shopping and sending payment information.

* Netscape introduced SSL in 1994, with SSL 3.0 being released in 1996.
* More security was needed and TLS (Transport Layer Security) protocol was introduced in 1999.

![ISO/OSI-model](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/9d265987c58331f6fd2f664837f85380.png)

TLS is more secure than SSL, and it has practically replaced SSL. SSL is still in wide use and expect all modern servers be using TLS.

* We can use TLS to upgrade HTTP, FTP, SMTP, POP3, and IMAP. Here is a following table lists the protocols before and after encryption via SSL/TLS:

| Protocol | Default Port | Secured Protocol | Default Port with TLS |
| -------- | ------------ | ---------------- | --------------------- |
| HTTP     | 80           | HTTPS            | 443                   |
| FTP      | 21           | FTPS             | 990                   |
| SMTP     | 25           | SMTPS            | 465                   |
| POP3     | 110          | POP3S            | 995                   |
| IMAP     | 143          | IMAPS            | 993                   |

With HTTP, to retrieve a web page, the web browser would need at least perform the following steps:

1. Establish a TCP connection with the remote server.
2. Send HTTP requests to the web server, such as `GET` and `POST` requests.

HTTPS requires an additional step to encrypt the traffic:

1. Establish a TCP connection.
2. Establish SSL/TLS connection.
3. Send HTTP requests to the web server.

To establish an SSL/TLS connection, the client needs to perform the proper handshake with the server. Based on [RFC 6101](https://datatracker.ietf.org/doc/html/rfc6101), the SSL connection establishment will look like the figure below.

![SSL-Handshake](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/ea654470ae699d10e9c07bd11a8320ac.png)

Once an SSL/TLS handshake has been established, HTTP requests and exchanged data won't be accessible to anyone watching the communication channel.

* For SSL/TLS to be effective when browsing the web over HTTPS, we rely on public certificates signed by certificate authorities trusted by our systems.

## Secure Shell (SSH)

Secure Shell (SSH) was created to provide a secure way for remote system administration.

1. Confirm the identity of the remote server.
2. Exchanged messages are encrypted and can only be decrypted by the intended recipient.
3. Both sides can detect any modification in the messages.

To use SSH, you need an SSH server and an SSH client. The SSH server listens on port 22 by default. The SSH client can authenticate using:

* Username and password
* Private and public key (after the SSH server is configured to recognize the corresponding key).
* Use the command `ssh username@MACHINE_IP`.
  * If this is the first time connecting to the system, we will need to confirm the fingerprint of the SSH server's public key to avoid man-in-the-middle (MITM) attacks.
  * In the case of SSH, we usually do not have a third party to check if the public key is valid, so we need to manually.
* SSH can transfer files using SCP (Secure Copy Protocol) based on the SSH protocol: `scp username@MACHINE_IP:/home/username/archive.tar.gz ~`
  * Alternative syntax: `scp backup.tar.bz2 username@MACHINE_IP:/home/username/`. This will copy the file from the local system to the directory on the remote system.

FTP could be secured using SSL/TLS by using the FTPS protocol which uses port 990. It is worth mentioning that FTP can also be secured using the SSH protocol which is the SFTP protocol. By default, this service listen on port 22, just like SSH.

## Password Attack

Many protocols require to authenticate - proving who you claim to be before accessing a service. Authentication can be achieved through one of the following, or a combination:

1. Something you _know_, such as password and PIN code.
2. Something you _have_, such as SIM card, RFID card, and USB dongle.
3. Something you _are_, such as fingerprint and iris.

Based on the 150 million usernames and passwords leaked from the Adobe breach in 2013, the top ten passwords are:

1. 123456
2. 123456789
3. password
4. adobe123
5. 12345678
6. qwerty
7. 1234567
8. 111111
9. photoshop
10. 123123

Attack against these passwords are usually carried out by:

1. Password Guessing: Guessing a password requires some knowledge of the target, such as their pet's name and birth year.
2. Dictionary Attack: This approach expands on password guessing and attempts to include all valid words in a dictionary or a wordlist.
3. Brute Force Attack: This attack is the most exhaustive and time-consuming where an attack can go as far trying all possible character combinations.

With dictionary attacks, hackers have compiled list after list containing leaked passwords from data breaches. An example is RockYou's list of breached passwords.

An automated way to try the common passwords or the entries from a word list is THC Hydra. Hydra supports many protocols, including FTP, POP3, IMAP, SMTP, SSH and all methods related to HTTP. The general command-line syntax is: `hydra -l username -P wordlist.txt server service`.

* `-l username` = Login name of the target.
* `-P wordlist.txt` = wordlist.txt file, which is a text file containing the list of passwords you want to try with the provided username.
* `server` = Hostname or IP address of the target server.
* `service` = Indicates the service trying to launch the dictionary attack.

Extra optional arguments to add:

* `-s PORT` = Specify a non-default port for the service.
* `-V` or `-vV`, for verbose makes Hydra show the username and password combinations that are being tried.
* `-t n` = Where n is the number of parallel connections to the target.
* `-d` = Debugging to get more detailed information about what is going on.

In summary, attacks against login systems can be carried out efficiently using a tool, such as THC Hydra combined with a suitable word list. Mitigation against such attacks can be sophisticated and depends on the target system.

* Password Policy: Enforces minimum complexity constraints on the passwords set by the user.
* Account Lockout: Locks the account after a certain number of failed attempts.
* Throttling Authentication Attempts: Delays the response to a login attempt against automated tools.
* Using CAPTCHA: Requires solving a question difficult for machines (Completely Automated Public Turing Test to tell Computers and Humans Apart).
* Require the use of a public certificate for authentication.

## Summary

Here is a default port number for common protocols in a table:

| Protocol | TCP Port | Application(s)                  | Data Security |
| -------- | -------- | ------------------------------- | ------------- |
| FTP      | 21       | File Transfer                   | Cleartext     |
| FTPS     | 990      | File Transfer                   | Encrypted     |
| HTTP     | 80       | Worldwide Web                   | Cleartext     |
| HTTPS    | 443      | Worldwide Web                   | Encrypted     |
| IMAP     | 143      | Email (MDA)                     | Cleartext     |
| IMAPS    | 993      | Email (MDA)                     | Encrypted     |
| POP3     | 110      | Email (MDA)                     | Cleartext     |
| POP3S    | 995      | Email (MDA)                     | Encrypted     |
| SFTP     | 22       | File Transfer                   | Encrypted     |
| SSH      | 22       | Remote Access and File Transfer | Encrypted     |
| SMTP     | 25       | Email (MTA)                     | Cleartext     |
| SMTPS    | 465      | Email (MTA)                     | Encrypted     |
| Telnet   | 23       | Remote Access                   | Cleartext     |

Hydra options for attacking different passwords:

| Option            | Explanation                                                   |
| ----------------- | ------------------------------------------------------------- |
| `-l username`     | Provide login name                                            |
| `-P WordList.txt` | Specify the password list to use                              |
| `server service`  | Set the server address and service to attack                  |
| `-s PORT`         | Use in case of non-default service port number                |
| `-V` or `-vV`     | Show the username and password combinations being tried       |
| `-d`              | Display debugging output if the verbose output is not helping |
