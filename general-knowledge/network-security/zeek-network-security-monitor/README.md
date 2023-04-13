---
description: Formerly known as Bro
---

# Zeek Network Security Monitor

An open-source and commercial network monitoring tool (traffic analyzer). Many use Zeek as a network security monitor (NSM) to support suspicious or malicious activity investigations.

{% embed url="https://docs.zeek.org/en/master/about.html" %}

## Zeek and Network Monitoring

Network monitoring is a set of management actions to watch/continuously overview and save the network traffic for further investigation.

* Focused on uptime (availability), device health and connection quality (performance), and network traffic balance and management (configuration). Includes monitoring and visualizing the network traffic, troubleshooting, and root cause analysis.

### Network Security Monitoring

Network Security Monitoring is focused on network anomalies like rogue hosts, encrypted traffic, suspicious service and port usage, and malicious/suspicious traffic patterns in an intrusion/anomaly detection and response.

* Model is helpful to identifying threats, vulnerabilities and security issues with a set of rules, signatures and patterns (part of SOC analyst levels).

### Zeek vs Snort

Both open source and commercial. The differences between the open-source version and the commercial version are detailed [here](https://corelight.com/products/compare-to-open-source-zeek?hsLang=en).

Zeek provides a wide range of detailed logs ready to investigate both for forensics and data analysis actions 50+ logs in 7 categories.

| Tool            | Zeek                                                                                                                                                                                                                  | Snort                                                                                                                                     |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| Capabilities    | NSM and IDS framework. Focused on network analysis. It is more focused on specific threats to trigger alerts. The detection mechanism is focused on events.                                                           | An IDS/IPS system. Focused on signatures to detect vulnerabilities. The detection mechanism is focused on signature patterns and packets. |
| Cons            | <p>Hard to use.</p><p>The analysis is done out of the Zeek, manually or by automation. </p>                                                                                                                           | Hard to detect complex threats.                                                                                                           |
| Pros            | <p>It provides in-depth traffic visibility.</p><p>Useful for threat hunting.</p><p>Ability to detect complex threats.</p><p>It has a scripting language and supports event correlation. </p><p>Easy to read logs.</p> | <p>Easy to write rules.</p><p>Cisco supported rules.</p><p>Community support.</p>                                                         |
| Common Use Case | <p>Network monitoring.<br>In-depth traffic investigation.<br>Intrusion detecting in chained events. </p>                                                                                                              | <p>Intrusion detection and prevention.<br>Stop known attacks/threats.</p>                                                                 |

### Zeek Architecture

Zeek has 2 primary layers:&#x20;

* Event Engine: Where the packets are processed and called the event core, responsible for describing the event without focusing on event details.
* Policy Script Interpreter: Semantic analysis is conducted and responsible for describing the event correlations by using Zeek scripts.

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/b94f413787763b1bdefe17c4bfb29782.png" alt=""><figcaption></figcaption></figure>

### Frameworks

Zeek has some frameworks to provide extended functionality in the scripting layer to enhance flexibility and compatibility with other network components.

* Logging
* Cluster
* Signature
* Notice
* Broker Communication
* Summary
* Input
* Supervisor
* NetControl
* Configuration
* GeoLocation
* Packet Analysis
* Intelligence
* File Analysis
* TLS Decryption

### Zeek Output

Zeek provides 50+ log files under seven different categories. When running Zeek, it will automatically start investigating the traffic and generate logs automatically in the working directory.

* If Zeek is running as a service, logs will be located in the default path: `/opt/zeek/logs`

### Working with Zeek

Check the version of Zeek with: `zeek -v`

Make sure Zeek is installed using the ZeekControl module (requires superuser privileges to start as a service):

* `zeekctl status`
* `zeekctl start`
* `zeekctl stop`

The only way to listen to live network traffic is using Zeek as a service.

Zeek can also be used as a packet investigator and will need to process the pcap files.

Main Zeek command line parameters:

| Parameter | Description                                |
| --------- | ------------------------------------------ |
| -r        |  Reading option, read/process a pcap file. |
| -C        |  Ignoring checksum errors.                 |
| -v        |  Version information.                      |
| zeekctl   | ZeekControl module.                        |

## Zeek Logs

Zeek generates log files according to the traffic data. The logs are well structured and tab-separated ASCII files so reading and processing is easy but requires effort.

| Category                        | Description                                                                         | Log Files                                                                                                                                                                                                                                                                                                                                            |
| ------------------------------- | ----------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>Network<br></p>              | <p>Network protocol logs.<br></p>                                                   | <p><em>conn.log, dce_rpc.log, dhcp.log, dnp3.log, dns.log, ftp.log, http.log, irc.log, kerberos.log, modbus.log, modbus_register_change.log, mysql.log, ntlm.log, ntp.log, radius.log, rdp.log, rfb.log, sip.log, smb_cmd.log, smb_files.log, smb_mapping.log, smtp.log, snmp.log, socks.log, ssh.log, ssl.log, syslog.log, tunnel.log.</em><br></p> |
| <p>Files<br></p>                | <p>File analysis result logs.<br></p>                                               | <p><em>files.log, ocsp.log, pe.log, x509.log.</em><br></p>                                                                                                                                                                                                                                                                                           |
| <p>NetControl<br></p>           | <p>Network control and flow logs.<br></p>                                           | <p><em>netcontrol.log, netcontrol_drop.log, netcontrol_shunt.log, netcontrol_catch_release.log, openflow.log.</em><br></p>                                                                                                                                                                                                                           |
| <p>Detection<br></p>            | <p>Detection and possible indicator logs.<br></p>                                   | <p><em>intel.log, notice.log, notice_alarm.log, signatures.log, traceroute.log.</em><br></p>                                                                                                                                                                                                                                                         |
| <p>Network Observations<br></p> | <p>Network flow logs.<br></p>                                                       | <p><em>known_certs.log, known_hosts.log, known_modbus.log, known_services.log, software.log.</em><br></p>                                                                                                                                                                                                                                            |
| <p>Miscellaneous<br></p>        | <p>Additional logs cover external alerts, inputs and failures.<br></p>              | <p><em>barnyard2.log, dpd.log, unified2.log, unknown_protocols.log, weird.log, weird_stats.log.</em><br></p>                                                                                                                                                                                                                                         |
| <p>Zeek Diagnostic<br></p>      | <p>Zeek diagnostic logs cover system messages, actions and some statistics.<br></p> | _broker.log, capture\_loss.log, cluster.log, config.log, loaded\_scripts.log, packet\_filter.log, print.log, prof.log, reporter.log, stats.log, stderr.log, stdout.log._                                                                                                                                                                             |

Refer to [Zeek's official documentation](https://docs.zeek.org/en/current/script-reference/log-files.html) and [Corelight log cheat sheet](https://corelight.com/about-zeek/zeek-data) for more information.

In addition to Linux command-line tools, one auxiliary program called `zeek-cut` reduces the effort extracting specific columns from log files. Each log file provides "field names" in the beginning.

### CLI-Kung-Fu Recall: Processing Zeek Logs

Manipulating the data at the command line is a crucial skill for Berkeley Packet Filters (BPF) and regular expressions to find/view/extract data.

Zeek signatures are composed of three logical paths: signature id, conditions, and actions.

| **Signature ID** | Unique signature name                                                                                                                                                                                                   |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Conditions**   | <p><strong>Header</strong>: Filter the packet headers for specific source and destination addresses, protocol, and port numbers.<br><strong>Content</strong>: Filter the packet payload for specific value/pattern.</p> |
| **Action**       | <p>Default: Create the "signatures.log" file in case of a signature match.<br>Additional action: Trigger a Zeek script.</p>                                                                                             |

Below are the most common conditions and filters for the Zeek signatures.

| Condition Field                                                  | Available Filters                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ---------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Header**                                                       | **src-ip**: Source IP.dst-ip: Destination IP.src-**port**: Source port.dst-port: Destination **port.ip-proto**: Target protocol. Supported protocols; TCP, UDP, ICMP, ICMP6, IP, IP6                                                                                                                                                                                                                                                                       |
| **Content**                                                      | <p><strong>payload</strong>: Packet payload.<br><strong>http-request</strong>: Decoded HTTP requests.<br><strong>http-request-header</strong>: Client-side HTTP headers.<br><strong>http-request-body</strong>: Client-side HTTP request bodys.<br><strong>http-reply-header</strong>: Server-side HTTP headers.<br><strong>http-reply-body</strong>: Server-side HTTP request bodys.<br><strong>ftp</strong>: Command line input of FTP sessions.<br></p> |
| **Context**                                                      | <p><strong>same-ip</strong>: Filtering the source and destination addresses for duplication.<br></p>                                                                                                                                                                                                                                                                                                                                                       |
| **Action**                                                       | <p><strong>event</strong>: Signature match message.<br></p>                                                                                                                                                                                                                                                                                                                                                                                                |
| <p><strong>Comparison</strong><br><strong>Operators</strong></p> | ==, !=, <, <=, >, >=                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| NOTE!                                                            |  Filters accept string, numeric and regex values.                                                                                                                                                                                                                                                                                                                                                                                                          |

Zeek signatures use the ".sig" extension.

* \-C ignore checksum errors
* \-r read pcap file
* \-s Use signature file

## Zeek Scripts: Fundamentals

Zeek has its own scripting language to investigate and correlate the detected events. These scripts can be used to apply a policy, called policy scripts.

| <p>Zeek has base scripts installed by default, and these are not intended to be modified.<br></p>                                                                                                         | <p>Located in<br> "/opt/zeek/share/zeek/base".<br></p>                                  |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| User-generated or modified scripts should be located in a specific path.                                                                                                                                  | <p>Located in<br>"/opt/zeek/share/zeek/site".<br></p>                                   |
| Policy scripts are located in a specific path.                                                                                                                                                            | <p>Located in<br> "/opt/zeek/share/zeek/policy".<br></p>                                |
| Like Snort, to automatically load/use a script in live sniffing mode, you must identify the script in the Zeek configuration file. You can also use a script for a single run, just like the signatures.  | <p>The configuration file is located in<br> "/opt/zeek/share/zeek/site/local.zeek".</p> |

Learn and practice the Zeek scripting language by using [Zeek's official training platform](https://try.bro.org/#/?example=hello) for free.

## Zeek Scripts and Signatures

Scripts contain operators, types, attributes, declarations and statements and directives.

### Write Basic Scripts

```markdown
event zeek_init()
    {
     print ("Started Zeek!");
    }
event zeek_done()
    {
    print ("Stopped Zeek!");
    }

# zeek_init: Do actions once Zeek starts its process.
# zeek_done: Do activities once Zeek finishes its process.
# print: Prompt a message on the terminal.
```

The script works and provides messages on the terminal. Zeek will create logs in the working directory separately from the scripts.

#### Packet Raw Data Script

Print raw data to the terminal by requesting details of a connection and extracting them without any filtering or sorting any data.

```markdown
event new_connection(c: connection)
{
	print c;
}
```

* An event is automatically generated for each new connection.
* To filter the event of interest, use the primary tag (c comes from the "c: connection"), id value (id=), and field name.

### Scripts and Signatures Together

Zeek scripts can refer to signatures and other Zeek scripts to provide flexibility and advantage in event correlation.

#### ftp-admin

```markdown
event signature_match (state: signature_state, msg: string, data: string)
{
if (state$sig_id == "ftp-admin")
    {
    print ("Signature hit! --> #FTP-Admin ");
    }
}
```

The script checks if there is a signature hit for ftp-admin. The signature is shown below:

```markdown
signature ftp-admin {
    ip-proto == tcp
    ftp /.*USER.*admin.*/
    event "FTP Username Input Found!"
}
```

```markdown
zeek -C -r ftp.pcap -s ftp-admin.sig 201.zeek
```

### Load Local Scripts

Base scripts are located in /opt/zeek/share/zeek/base. Load all local scripts identified in "local.zeek" file by using the `local` command.

`zeek -C -r ftp.pcap local`

#### Load Specific Scripts

Another method to load scripts is by identifying the script path.

## Load Frameworks

Zeek has 15+ built scripts and frameworks. Visit Zeek's online book [here](https://docs.zeek.org/en/master/frameworks/index.html) for more details.

### File Framework - Hashes

Call a specific framework with `@load$PATH/base/frameworks/framework-name`

* Built-in function of the file framework to detect file hashes for MD5, SHA1 and SHA256.
* ```markdown
  # Enable MD5, SHA1 and SHA256 hashing for all files.
  @load /opt/zeek/share/zeek/policy/frameworks/files/hash-all-files.zeek
  ```

### File Framework - Extract Files

Extract files from the pcap and a new folder called "extract\_files" is automatically created.&#x20;

```markdown
zeek -C -r case1.pcap /opt/zeek/share/zeek/policy/frameworks/files/extract-all-files.zeek
```

* Use `file` command to determine the file type of the extracted files.
* Utilize grep tool to investigate particular values across all logs.

### Notice Framework - Intelligence

The intelligence framework can work with data feeds to process and correlate events and identify anomalies. The framework requires a feed to match and create alerts from the network traffic.

Intelligence source location: `/opt/zeek/intel/zeek_intel.txt`

## Zeek Scripts | Packages

Zeek Package Manager helps users install third-party scripts and plugins to extend Zeek functionalities. The package manager is installed with Zeek and available with the `zkg` command. Root privileges need to use the "zkg" tool.

| Command                    | Description                                                                  |
| -------------------------- | ---------------------------------------------------------------------------- |
| `zkg install package_path` | Install a package. Example (zkg install zeek/j-gras/zeek-af\_packet-plugin). |
| `zkg install git_url`      | Install package. Example (zkg install https://github.com/corelight/ztest).   |
| `zkg list`                 | List installed package.                                                      |
| `zkg remove`               | Remove installed package.                                                    |
| `zkg refresh`              | Check version updates for installed packages.                                |
| `zkg upgrade`              | Update installed packages.                                                   |

There are multiple ways of using packages:

1. Use them as frameworks and calling specific package path/directory per usage.
2. Most common is calling packages from a script with the @load method.
3. Calling their package names (only works for packages installed with zkg install method).

## Zeek Exercises

### Anamalous DNS

Investigate the dns-tunneling.pcap and find the number of DNS records linked to the IPv6 address from the dns.log file.

* `zeek -Cr dns-tunneling.pcap`
* `cat dns.log | grep AAAA | wc -l`

Investigate the conn.log file to find the longest connection duration.

* `cat conn.log | zeek-cut duration | sort`

Investigate the dns.log file to filter all unique DNS queries.

* cat dns.log | zeek-cut query | rev | cut -d '.' -f1-2 | sort -rn | uniq

### Phishing

Investigate the logs to find the suspicious source address (de-fanged format).

* `cat files.log | zeek-cut rx_hosts`
  * Defang the value with CyberChef.

Investigate the http.log to find domain addresses where the malicious files downloaded from (de-fanged format).

* `cat http.log | zeek-cut host`
  * Defang the value with CyberChef.

Investigate the malicious document in VirusTotal to find the associated file.

* `zeek -Cr phishing.pcap hash-demo.zeek`

Investigate the extracted malicious .exe file and find the given file name in VirusTotal.

* Take the MD5 value and search in VirusTotal.
  * cc28e40b46237ab6d5282199ef78c464

Investigate the malicious .exe for the contacted domain name.

* VirusTotal -> Behavior -> DNS Resolutions

Investigate the http.log to find the request name of the downloaded malicious .exe file.

* `cat http.log | zeek-cut uri`

### Log4J

Investigate the log4shell.pcapng file with detection-log4j.zeek script to find the number of signature hits.

* `zeek -Cr log4shell.pcapng detection-log4j.zeek`
* `cat signatures.log`

Investigate the http.log file to find tool used for scanning.

* `cat http.log | zeek-cut user_agent`

Investigate the http.log file to find the extension of the exploit file.

* `cat http.log | zeek-cut uri`

Investigate the log4j.log file to decode the base64 commands.

* `cat log4j.log | zeek-cut value | head`
