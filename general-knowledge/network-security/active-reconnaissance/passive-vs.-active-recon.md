# Passive vs. Active Recon

Reconnaissance (recon) can be defined as a preliminary survey to gather information about a target. It is the first step in the [Unified Kill Chain](https://www.unifiedkillchain.com/) to gain an initial foothold on a system.

* Rely on public available knowledge and resources without directly engaging with the target.
* Activities include:
  * Looking up DNS records of a domain from a public DNS server.
  * Checking jobs ads related to the target website.
  * Reading news articles about the target company.

On the other hand, \[\[active reconnaissance|network.active-reconnaissance]] cannot be achieved so discreetly and requires direct engagement with the target. Examples of active reconnaissance activities include:

* Connecting to one of the company servers such as HTTP, FTP, and SMTP.
* Calling the company in an attempt to get information (social engineering).
* Entering company premises pretending to be a repairman.

## WHOIS

WHOIS is a request and response protocol that follows the [RFC 3912](https://www.ietf.org/rfc/rfc3912.txt) specification. WHOIS server listens on TCP port 43 for incoming requests. The domain registrar is responsible for maintaining the WHOIS records for the domain names it is leasing.

* **Registrar**: Which registrar was the domain name registered?
* **Contact info of registrant**: Name, organization, address, phone, among other things (unless made hidden via privacy service).
* **Creation, update, and expiration dates**: When was the domain name first registered? When was it last updated? And when does it need to be renewed?
* **Name Server**: Which server to ask to resolve the domain name?

To retrieve this information, the command `whois` client or online service. The syntax is `whois DOMAIN_NAME`.

## nslookup and dig

Find the IP address of a domain name using `nslookup`, which stands for Name Server Look Up. The syntax for the command is `nslookup DOMAIN_NAME`. In general, you can use `nslookup OPTIONS DOMAIN_NAME SERVER`.

* OPTIONS contains the query type shown in the table below.
* DOMAIN\_NAME is the domain name you are looking up.
* SERVER is the DNS server that you want to query. Can choose any local or public DNS server to query such as Cloudflare (1.1.1.1, 1.0.0.1) or Google (8.8.8.8, 8.8.4.4).

| Query Type | Result             |
| ---------- | ------------------ |
| A          | IPv4 addresses     |
| AAAA       | IPv6 addresses     |
| CNAME      | Canonical Name     |
| MX         | Mail servers       |
| SOA        | Start of Authority |
| TXT        | TXT Records        |

* A and AAAA records are used to return IPv4 and IPv6 addresses. Helpful to check during penetration testing to further check IP addresses for insecurities.
* To learn about the email servers and configurations for a particular domain with `nslookup -type=MX tryhackme.com`. Could potentially find vulnerable server versions.

For more advanced DNS queries and additional functionality, we can use `dig @SERVER DOMAIN_NAME TYPE` or `dig DOMAIN_NAME TYPE` ("Domain Information Groper") to look up the MX records and compare them to `nslookup`.

* SERVER is the DNS server that you want to query.
* DOMAIN\_NAME is the domain name looking up.
* TYPE contains the DNS record type shown in the table.

## DNSDumpster

DNS lookup tools, such as nslookup and dig, cannot find subdomains on their own. There is a possibility that a subdomain is not updated regularly leading to vulnerable services.

To avoid time-consuming search with brute-forcing queries, an online service that offers detailed answers to DNS queries, such as [DNSDumpster](https://dnsdumpster.com/).

* DNSDumpster will return the collected DNS information in easy-to-read tables and a graph. DNSDumpster will also provide any collected information about listening servers.
  * List of DNS servers for the domain.
  * Resolve domain names to IP addresses and geolocate them.
  * Mail exchange servers and provide more information about the owner and location.
  * TXT records.

## Shodan.io

When tasked to run a penetration test against specific targets, a service like [Shodan.io](https://www.shodan.io/) can be helpful to learn various pieces of information about the client's network, without actively connecting to it. On the defensive side, you can use different services from Shodan.io to learn about connected and exposed devices belonging to the organization.

![shodan.io](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/a8ac6c22a64b8413ee8d02c2224eddac.png)

Record shows a web server. Shodan.io collects information related to any device it can find connected online. We learn:

* IP address
* Hosting company
* Geographic location
* Server type and version

## Summary

The power of such tools to collect information about targets without directly connecting to them.

| Purpose                      | Command-line Example                      |
| ---------------------------- | ----------------------------------------- |
| WHOIS record                 | `whois tryhackme.com`                     |
| DNS A records                | `nslookup -type=A tryhackme.com`          |
| DNS MX records at DNS server | `nslookup -type=MX tryhackme.com 1.1.1.1` |
| DNS TXT records              | `nslookup -type=TXT tryhackme.com`        |
| DNS A records                | `dig tryhackme.com A`                     |
| DNS MX records at DNS server | `dig @1.1.1.1 tryhackme.com MX`           |
| DNS TXT records              | `dig tryhackme.com TXT`                   |
