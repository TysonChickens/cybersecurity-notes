# Snort

Snort is an open-source, rule-based Network Intrusion Detection and Prevention System (NIDS/NIPS). Developed and maintained by Martin Roesch, open-source contributors, and the Cisco Talos team.

Capabilities of Snort:

* Live traffic analysis
* Attack and probe detection
* Packet logging
* Protocol analysis
* Real-time alert
* Modules & plugins
* Pre-processor
* Cross-platform support (Linux & Windows)

Snort has three main use models:

* **Sniffer Mode** - Read IP packets and prompt them in the console application.
* **Packet Logger Mode** - Log all IP packets (inbound/outbound) that visit the network.
* **NIDS and NIPS Modes** - Log/drop packets that are considered malicious according to user-defined rules.

## Intrusion Detection System (IDS)

IDS is a passive monitoring solution for detecting possible malicious activities/patterns and policy violations to generate alerts for each suspicious event.

Main types of IDS systems and alerts are created:

* **Network Intrusion Detection System (NIDS**) - Monitors the traffic flow from various areas of the network.
* **Host-based Intrusion Detection System (HIDS**) - Monitors the traffic flow from a single endpoint device to investigate the traffic from a specific device.

## Intrusion Prevention System (IPS)

IPS is an active protecting solution to prevent possible malicious activities/patterns to stop/prevent/terminate the suspicious event as the detection is performed.

Main types of IPS systems: The connection is terminated if a signature is found.

* **Network Intrusion Prevention System (NIPS**) - Monitors the traffic flow from various areas of the network.&#x20;
* **Behavior-based Intrusion Prevention System (Network Behavior Analysis - NBA**) - Monitors the traffic flow from various areas of the network. Works similar to NIPS.
  * Requires a baseline to learn the normal traffic and differentiate the malicious traffic and threats. The training period is important to avoid any false positives.
* **Wireless Intrusion Prevention System (WIPS**) - Monitors the traffic flow from a wireless network traffic.
* **Host-based Intrusion Prevention System (HIPS**) - Actively protects the traffic flow from a single endpoint device.

## Detection/Prevention Techniques

| Technique       | Approach                                                                                                                                                                                                         |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Signature-Based | <p>Relies on rules that identify the specific patterns of the known malicious behavior. This model helps detect known threats. <br></p>                                                                          |
| Behavior-Based  | <p>Identifies new threats with new patterns that pass through signatures. The model compares the known/normal with unknown/abnormal behavior. This model helps detect previously unknown or new threats.<br></p> |
| Policy-Based    | Compares detected activities with system configuration and security policies. This model helps detect policy violations.                                                                                         |

## Sniffer Mode

Sniffer mode parameters to use against the network interface:

| Parameter | Description                                                                                                                                                    |
| --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| -v        | Verbose. Display the TCP/IP output in the console.                                                                                                             |
| -d        | <p>Display the packet data (payload).<br></p>                                                                                                                  |
| -e        | <p>Display the link-layer (TCP/IP/UDP/ICMP) headers. <br></p>                                                                                                  |
| -X        | Display the full packet details in HEX.                                                                                                                        |
| -i        | This parameter helps to define a specific network interface to listen/sniff. Once you have multiple interfaces, you can choose a specific interface to sniff.  |

## Packet Logger Mode

Use Snort as a sniffer and log the sniffed packets in logger mode parameters:

| Parameter | Description                                                                                                                                                                |
| --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| -l        | <p>Logger mode, target log and alert output directory. Default output folder is /var/log/snort</p><p>The default action is to dump as tcpdump format in /var/log/snort</p> |
| -K ASCII  | Log packets in ASCII format.                                                                                                                                               |
| -r        | <p>Reading option, read the dumped logs in Snort.<br></p>                                                                                                                  |
| -n        | Specify the number of packets that will process/read. Snort will stop after reading the specified number of packets.                                                       |

"-r" parameter also allows users to filter the binary log files to see specific packets with the "-r" parameter and Berkeley Packet Filters (BPF).&#x20;

* `sudo snort -r logname.log -X`
* `sudo snort -r logname.log icmp`
* `sudo snort -r logname.log tcp`
* `sudo snort -r logname.log 'udp and port 53'`

### Logfile Ownership

Whoever creates a file becomes the owner of the corresponding file. Snort requires superuser (root) to sniff the traffic. Therefore, will need "root" permissions to investigate the log files.

* Elevation of privileges using the "sudo" command to examine the generated log files. Also elevate the session and switch to the superuser account using `sudo su`
* Change the ownership of files/directories with `sudo chown username file` or `sudo chown username -R directory`

## IDS/IPS Mode

Helps manage the traffic according to the user-defined rules.

NIDS mode parameters:

| Parameter | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| -c        | Defining the configuration file.                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| -T        | Testing the configuration file.                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| -N        | <p>Disable logging.<br></p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -D        | <p>Background mode.<br></p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -A        | <p>Alert modes;<br></p><p>full: Full alert mode, providing all possible information about the alert. This one also is the default mode; once you use -A and don't specify any mode, snort uses this mode.</p><p>fast:  Fast mode shows the alert message, timestamp, source and destination IP, along with port numbers.</p><p>console: Provides fast style alerts on the console screen.</p><p>cmg: CMG style, basic header details with payload in hex and text format.</p><p>none: Disabling alerting.</p> |

## PCAP Investigation Mode

PCAP read/investigate mode helps work with pcap files to process and alert based on a ruleset. Snort pcap benefits from the rules to speed up investigation process using known patterns of threats.

PCAP mode parameters:

| Parameter           | Description                                       |
| ------------------- | ------------------------------------------------- |
| -r / --pcap-single= | Read a single pcap                                |
| --pcap-list=""      | Read pcaps provided in command (space separated). |
| --pcap-show         | Show pcap name on console during processing.      |

## Snort Rule Structure

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/fc3650c5dbad35d4a7b7bc606788e809.png" alt=""><figcaption><p>Snort rule structure</p></figcaption></figure>

Each rule should have a type of action, protocol, source and destination IP, source and destination port and an option.

* Snort is in passive mode by default and will need to start in IDS using "inline mode" to turn it on.

Focus on two actions; "alert"  for IDS mode and "reject" for IPS mode.

Rules cannot be processed without a header. Rule options are "optional" parts. However, it is almost impossible to detect sophisticated attacks without using the rule options.

| <p>Action<br></p>   | <p> The most common actions are listed below.</p><ul><li>alert: Generate an alert and log the packet.</li><li>log: Log the packet.</li><li>drop: Block and log the packet.</li><li>reject: Block the packet, log it and terminate the packet session. </li></ul>                                                                                                                                                                       |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>Protocol<br></p> | <ul><li>Identifies the type of the protocol that filtered for the rule.</li></ul><ul><li><p>Snort2 supports only four protocols filters in the rules (IP, TCP, UDP and ICMP). </p><ul><li>However, you can detect the application flows using port numbers and options. For instance, if you want to detect FTP traffic, you cannot use the FTP keyword in the protocol field - Filter FTP TCP traffic on port 21.</li></ul></li></ul> |

### IP and Port Numbers

Parameters identify the source and destination IP addresses and port numbers filtered for the rule.

| IP Filtering                            | <p>alert icmp 192.168.1.56 any &#x3C;> any any  (msg: "ICMP Packet Found"; sid: 100001; rev:1;)</p><ul><li>Alerts for each ICMP packet originating from the 192.168.1.56 IP address.</li></ul>                                                                                                                                       |
| --------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <p>Filter an IP range<br></p>           | <p>alert icmp 192.168.1.0/24 any &#x3C;> any any  (msg: "ICMP Packet Found"; sid: 100001; rev:1;)</p><ul><li>Alerts for each ICMP packet originating from the 192.168.1.0/24 subnet.</li></ul>                                                                                                                                       |
| <p>Filter multiple IP ranges<br></p>    | <p>alert icmp [192.168.1.0/24, 10.1.1.0/24] any &#x3C;> any any  (msg: "ICMP Packet Found"; sid: 100001; rev:1;)</p><ul><li>Alerts for each ICMP packet originating from the 192.168.1.0/24 and 10.1.1.0/24 subnets.</li></ul>                                                                                                       |
| <p>Exclude IP addresses/ranges<br></p>  | <p>"negation operator" is used for excluding specific addresses and ports. Negation operator is indicated with "!"alert </p><ul><li>icmp !192.168.1.0/24 any &#x3C;> any any  (msg: "ICMP Packet Found"; sid: 100001; rev:1;)</li></ul><ul><li>Alerts for each ICMP packet not originating from the 192.168.1.0/24 subnet.</li></ul> |
| Port Filtering                          | <p>alert tcp !192.168.1.0/24 21 &#x3C;> any any  (msg: "ICMP Packet Found"; sid: 100001; rev:1;)</p><ul><li>Alerts for each TCP packet originating from port 21.</li></ul>                                                                                                                                                           |
| <p>Exclude a specific port<br></p>      | <p>alert tcp !192.168.1.0/24 !21 &#x3C;> any any  (msg: "ICMP Packet Found"; sid: 100001; rev:1;)</p><ul><li>Alerts for each TCP packet not originating from port 21.</li></ul>                                                                                                                                                      |
| <p>Filter a port range (Type 1)<br></p> | <p>alert tcp !192.168.1.0/24 1:1024 &#x3C;> any any  (msg: "ICMP Packet Found"; sid: 100001; rev:1;)</p><ul><li>Alerts for each TCP packet originating from ports between 1-1024.</li></ul>                                                                                                                                          |
| <p>Filter a port range (Type 2)<br></p> | <p>alert icmp any :1024 &#x3C;> any any  (msg: "ICMP Packet Found"; sid: 100001; rev:1;)</p><ul><li>Alerts for each TCP packet originating from ports less than or equal to 1024.</li></ul>                                                                                                                                          |
| <p>Filter a port range (Type 3)<br></p> | <p>alert icmp any 1024: &#x3C;> any any (msg: "ICMP Packet Found"; sid: 100001; rev:1;)</p><ul><li>Alerts for each TCP packet originating from a source port higher than or equal to 1024.</li></ul>                                                                                                                                 |
| <p>Filter a port range (Type 4)<br></p> | <p>alert icmp any 80,1024: &#x3C;> any any (msg: "ICMP Packet Found"; sid: 100001; rev:1;)</p><ul><li>Alerts for each TCP packet originating from a source port 80 and higher than or equal to 1024.</li></ul>                                                                                                                       |

### Direction

The direction operator indicates the traffic flow to be filtered by Snort.

* \-> Source to destination flow.
* <-> Bidirectional flow.
* There is no <- operator in Snort.

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/40e476d05bb7806cada61d5c9ce4cfc9.png" alt=""><figcaption></figcaption></figure>

### Rule Options

* General - Fundamental rule options for Snort.
* Payload - Help investigate payload data and detect specific payload patterns.
* Non-Payload - Focus on non-payload data to help create specific patterns and identify network issues.

| Msg                  | <p>The message field is a basic prompt and quick identifier of the rule. Once the rule is triggered, the message filed will appear in the console or log. Usually, the message part is a one-liner that summarizes the event.<br></p>                                                                                                                                                                                                                                          |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <p>Sid<br></p>       | <p>Snort rule IDs (SID) come with a pre-defined scope, and each rule must have a SID in a proper format. There are three different scopes for SIDs shown below.</p><ul><li>&#x3C;100: Reserved rules</li><li>100-999,999: Rules came with the build.</li><li>>=1,000,000: Rules created by user.</li></ul><p>Briefly, the rules we will create should have sid greater than 100.000.000. Another important point is; SIDs should not overlap, and each id must be unique. </p> |
| <p>Reference<br></p> | <p>Each rule can have additional information or reference to explain the purpose of the rule or threat pattern. That could be a Common Vulnerabilities and Exposures (CVE) ID or external information.<br></p>                                                                                                                                                                                                                                                                 |
| <p>Rev<br></p>       | <p>Snort rules can be modified and updated for performance and efficiency issues. Rev option help analysts to have the revision information of each rule. Therefore, it will be easy to understand rule improvements.</p><ul><li>alert icmp any any &#x3C;> any any (msg: "ICMP Packet Found"; sid: 100001; reference:cve,CVE-XXXX; rev:1;)</li></ul>                                                                                                                          |

#### Payload Detection Rules Options

| <p>Content<br></p>      | <p>Payload data. It matches specific payload data by ASCII, HEX or both. It is possible to use this option multiple times in a single rule. </p><p>Following rules will create an alert for each HTTP packet containing the keyword "GET". This rule option is case sensitive!</p><ul><li>ASCII mode - alert tcp any any &#x3C;> any 80  (msg: "GET Request Found"; content:"GET"; sid: 100001; rev:1;)</li><li>HEX mode - alert tcp any any &#x3C;> any 80  (msg: "GET Request Found"; content:"|47 45 54|"; sid: 100001; rev:1;)</li></ul>                                  |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>Nocase<br></p>       | <p>Disabling case sensitivity. Used for enhancing the content searches.</p><ul><li>alert tcp any any &#x3C;> any 80  (msg: "GET Request Found"; content:"GET"; nocase; sid: 100001; rev:1;)</li></ul>                                                                                                                                                                                                                                                                                                                                                                         |
| <p>Fast_pattern<br></p> | <p>Prioritize content search to speed up the payload search operation. By default, Snort uses the biggest content and evaluates it against the rules. "fast_pattern" option helps you select the initial packet match with the specific value for further investigation. This option always works case insensitive and can be used once per rule. Note that this option is required when using multiple "content" options.</p><ul><li>alert tcp any any &#x3C;> any 80  (msg: "GET Request Found"; content:"GET"; fast_pattern; content:"www";  sid:100001; rev:1;)</li></ul> |

#### Non-Payload Detection Rules Options

| ID                | <p>Filtering the IP id field.</p><ul><li>alert tcp any any &#x3C;> any any (msg: "ID TEST"; id:123456; sid: 100001; rev:1;)</li></ul>                                                                                              |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>Flags<br></p>  | <p>Filtering the TCP flags.</p><ul><li>F - FIN</li><li>S - SYN</li><li>R - RST</li><li>P - PSH</li><li>A - ACK</li><li>U - URG</li></ul><p>alert tcp any any &#x3C;> any any (msg: "FLAG TEST"; flags:S;  sid: 100001; rev:1;)</p> |
| <p>Dsize<br></p>  | <p>Filtering the packet payload size.</p><ul><li>dsize:min&#x3C;>max;</li><li>dsize:>100</li><li>dsize:&#x3C;100</li></ul><p>alert ip any any &#x3C;> any any (msg: "SEQ TEST"; dsize:100&#x3C;>300;  sid: 100001; rev:1;)</p>     |
| <p>Sameip<br></p> | <p>Filtering the source and destination IP addresses for duplication.</p><ul><li>alert ip any any &#x3C;> any any (msg: "SAME-IP TEST";  sameip; sid: 100001; rev:1;)</li></ul>                                                    |

A created rule is a local rule and should be located under "/etc/snort/rules/local.rules".

## Summary

Main Components of Snort

* **Packet Decoder** - Packet collector component of Snort. It collects and prepares the packets for pre-processing.&#x20;
* **Pre-processors** - A component that arranges and modifies the packets for the detection engine.
* **Detection Engine** - The primary component that process, dissect and analyse the packets by applying the rules.&#x20;
* **Logging and Alerting** - Log and alert generation component.
* **Outputs and Plugins** - Output integration modules (i.e. alerts to syslog/mysql) and additional plugin (rule management detection plugins) support is done with this component.

### Types of Rules Available

* Community Rules - Free ruleset under the GPLv2. Publicly accessible, no need for registration.
* Registered Rules - Free ruleset (requires registration). This ruleset contains subscriber rules with 30 days delay.
* Subscriber Rules (Paid) - Paid ruleset (requires subscription). This ruleset is the main ruleset and is updated twice a week (Tuesdays and Thursdays).

You can download and read more on the rules [here](https://www.snort.org/downloads).

if you want to use the community or the paid rules, you need to indicate each rule in the snort.conf file.

Since it is a long, all-in-one configuration file, editing it without causing misconfiguration is troublesome for some users. That is why Snort has several rule updating modules and integration tools. To sum up, never replace your configured Snort configuration files; you must edit your configuration files manually or update your rules with additional tools and modules to not face any fail/crash or lack of feature.

* snort.conf: _Main configuration file._
* local.rules: _User-generated rules file._
