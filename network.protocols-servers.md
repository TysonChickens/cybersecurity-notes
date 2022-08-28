---
id: 7vbcm0m35nipg01gjxvwkw5
title: Protocols Servers
desc: ''
updated: 1660631777301
created: 1660282688970
---

# Introduction

Learn about common protocols such as HTTP, FTP, POP3, SMTP and IMAP, along with related insecurities.

- Understand each protocol and what happens on the low level that is usually hidden by an elegant GUI (Graphical User Interface).
- Protocols using a simple Telnet client to understand what the GUI client is doing under the hood.

## Telnet

The Telnet protocol is an application layer protocol used to connect to a virtual terminal of another computer.

- Using Telnet, a user can log into another computer and access its terminal (console) to run programs, start batch processes, and perform system administration tasks remotely.
  - When a user connects, they will be asked for a username and password. Upon correct authentication, the user will access the remote system's terminal.
    - Communication with Telnet is not encrypted and is an easy target for attackers.
- Telnet server uses the Telnet protocol to listen for incoming connections on port 23.
- Not a reliable protocol for remote administration as all data are sent in cleartext.

## HyperText Transfer Protocol (HTTP)

HyperText Transfer Protocol is the protocol used to transfer web pages. The web browser connects to the webserver and uses HTTP to request HTML pages and images among other files and submit forms and upload various files.

- Browsing the World Wide Web (WWW), we are certainly using the HTTP protocol.

![HTML](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/a23a13cef49ae7fff87bfd94f6a175dc.png)

The image shows a client requesting the HTML page `index.html`, which the webserver provides. Then the client requests an image, `logo.jpg`, and the server sends it.

- HTTP sends and receives data as cleartext (not encrypted); therefore, you can use a simple tool, such as Telnet (or Netcat) to communicate with a web server and act as a "web browser". The key difference is input HTTP-related commands instead of a web browser doing it automatically.
- Instead of a web request, use `telnet` to request a file from the web server.
  - Connect to port 80 using `telnet MACHINE_IP`.
  - Type `GET /index.html HTTP/1.1` to retrieve the page `index.html` or `GET / HTTP/1.1` to retrieve the default page.
  - Finally provide some value for the host file like `host: telnet` and hit the Enter/Return key twice.

We need an HTTP server (webserver) and an HTTP client (web browser) to use the HTTP protocol. THe web server will "serve" a specific set of files to the requesting web browser.

Popular choices for HTTP servers are:

- [Apache](https://www.apache.org/)
- [Internet Information Services (IIS)](https://www.iis.net/)
- [nginx](https://nginx.org/)

There are many web browsers available. Currently, the most popular web browsers are:

- Chrome by Google
- Edge by Microsoft
- Firefox by Mozilla
- Safari by Apple

## File Transfer Protocol (FTP)

File Transfer Protocol (FTP) was developed to make the transfer of files between different computers with different systems efficient.

- FTP sends and receives data as cleartext; therefore, we can use Telnet (or Netcat) to communicate with an FTP server and act as an FTP client.
- Connect to an FTP server using a Telnet client. FTP servers listen on port 21 by default.
- The command `TYPE A` switches the file transfer mode to ASCII and `TYPE I` switches the file transfer mode to binary.
- Use FTP client to download a text file:
  - `ls` to the list files.
  - `ascii` to switch mode since it is a text file.
  - `get FILENAME` for client and server to establish a connection for file transfer.

There are two modes for FTP:

- Active: Data is sent over a separate originating from the FTP server's port 20.
- Passive: Data is sent over a separate originating from an FTP client's port above port number 1023.

FTP servers and FTP clients user the FTP protocol. There are various FTP server software that can select from if you want to hose FTP file server. Examples of FTP server software include:

- vsftpd
- ProFTPD
- uFTP

FTP clients, in addition to the console FTP client commonly found on Linux systems. Can also use an FTP client with GUI such as FileZilla and some web browsers also support FTP protocol.

- Because FTP sends the login credentials along with the commands and files in cleartext, FTP traffic can be an easy target for attackers.

## Simple Mail Transfer Protocol (SMTP)

Email is one of the most used services on the Internet. There are various configurations for email servers and is possible to set up an email system to allow local users to exchange emails with each other with no access to the internet. Email delivery over the Internet requires the following components:

1. Mail Submission Agent (MSA)
2. Mail Transfer Agent (MTA)
3. Mail Delivery Agent (MDA)
4. Mail User Agent (MUA)

![email](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/822a449fd569c16c875a13ca2487b714.png)

Shows the steps that an email needs to go through to reach the recipient's inbox:

1. Mail User Agent (MUA), or simply an email client, has an email message to be sent. The MUA connects to a Mail Submission Agent (MSA) to send its message.
2. The MSA receives the message, checks for any errors before transferring it to the Mail Transfer Agent (MTA) server, commonly hosted on the same server.
3. The MTA will send the email message to the MTA of the recipient. The MTA can also function as a Mail Submission Agent (MSA).
4. A typical setup would have the MTA server also functioning as a Mail Delivery Agent (MDA).
5. The recipient will collect its email from the MDA using their email client.

Simplified analogy:

1. You (MUA) want to send postal mail.
2. The post office employee (MSA) checks the postal mail for any issues before your local post office (MTA) accepts it.
3. The local post office checks the mail destination and sends it to the post office (MTA) in the correct country.
4. The post office (MTA) delivers the mail to the recipient mailbox (MDA).
5. The recipient (MUA) regularly checks the mailbox for new mail. They notice the new mail, and they take it.

In the same way, we need to follow a protocol to communicate with an HTTP server, and we need to rely on email protocols to talk with an MTA and an MDA protocols are:

1. Simple Mail Transfer Protocol (SMTP)
2. Post Office Protocol version 3 (POP3) or Internet Message Access Protocol (IMAP)

SMTP is used to communicate with an MTA server. Since SMTP uses cleartext, all commands are sent without encryption and use a basic Telnet client to connect to an SMTP server and act as am email client (MUA) sending a message.

- SMTP server listens on port 25 by default.
- Once connected, issue `helo hostname` and start typing our email.
  - After `helo`, issue `mail from:`, `rcpt to:` to indicate the sender and the recipient.
  - When sending email message, issue the command `data` and type the message.

## Post Office Protocol 3 (POP3)

The Post Office Protocol version 3 (POP3) is a protocol used to download the email messages from a Mail Delivery Agent (MDA) server. The mail client connects to the POP3 server, authenticates, downloads the new email messages before (optional) deleting them.

![pop3](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/ed910ad418376edc846846fc2a0dd3f6.png)

- POP3 server default port is 110.
- Authentication is required to access the email messages.
- Using the `STAT` command, a reply "+OK 1 179" has the format `+OK nn mm`, where __nn__ is the number of email messages in the inbox, and the __mm__ is the size of the inbox in octets (byte).
- The command `LIST` provides a list of new messages on the server. `RETR 1` retrieves the first message in the list.

## Internet Message Access Protocol (IMAP)

Internet Message Access Protocol (IMAP) is more sophisticated than POP3. IMAP makes it possible to keep your email synchronized across multiple devices (and mail clients).

- Use Telnet to connect to IMAP server's default port 143 and then authenticate using `LOGIN username password`.
- IMAP requires each command to be preceded by a random string to be able to track the reply.
- List mail folders using `LIST "" "*"`, before checking any new messages in the inbox using `EXAMINE INBOX`.

## Summary

Common protocols and default port numbers:

| Protocol | TCP Port | Application(s) | Data Security |
| -------- | -------- | -------------- | ------------- |
| FTP      | 21       | File Transfer  | Cleartext     |
| HTTP     | 80       | Worldwide Web  | Cleartext     |
| IMAP     | 143      | Email (MDA)    | Cleartext     |
| POP3     | 110      | Email (MDA)    | Cleartext     |
| SMTP     | 25       | Email (MTA)    | Cleartext     |
| Telnet   | 23       | Remote Access  | Cleartext     |