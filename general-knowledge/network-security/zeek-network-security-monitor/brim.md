---
description: Log investigation, pcap analysis and threat hunting.
---

# Brim

[BRIM](https://www.brimdata.io/) is an open-source desktop application to help process pcap and log files. Primary focus is to provide search and analytics. Uses the Zeek log processing format and supports Zeek signatures and Suricata rules for detection.

It can handle two types of data as an input:

* **Packet Capture Files**: Pcap files created with tcpdump, tshark and Wireshark-like applications.
* **Log files**: Structured log files like Zeek logs.

Brim is built on open-source platforms:

* Zeek
* Zed Language
* ZNG Data Format
* Electron and React

Brim reduces the time and effort spent processing pcap files and investigating the log files by provided a simple and powerful GUI application.

### Brim vs Wireshark vs Zeek

| <p><br></p>              | Brim                                                 | Wireshark                                                           | Zeek                                                 |
| ------------------------ | ---------------------------------------------------- | ------------------------------------------------------------------- | ---------------------------------------------------- |
| Purpose                  | Pcap processing; event/stream and log investigation. | Traffic sniffing. Pcap processing; packet and stream investigation. | Pcap processing; event/stream and log investigation. |
| GUI                      | <p>✔<br></p>                                         | <p>✔<br></p>                                                        | <p>✖<br></p>                                         |
| Sniffing                 | <p>✖<br></p>                                         | <p>✔<br></p>                                                        | <p>✔<br></p>                                         |
| Pcap processing          | <p>✔<br></p>                                         | <p>✔<br></p>                                                        | <p>✔<br></p>                                         |
| Log processing           | <p>✔<br></p>                                         | <p>✖<br></p>                                                        | <p>✔<br></p>                                         |
| Packet decoding          | <p>✖<br></p>                                         | <p>✔<br></p>                                                        | <p>✔<br></p>                                         |
| Filtering                | <p>✔<br></p>                                         | <p>✔<br></p>                                                        | <p>✔<br></p>                                         |
| <p>Scripting<br></p>     | <p>✖<br></p>                                         | <p>✖<br></p>                                                        | <p>✔<br></p>                                         |
| Signature Support        | <p>✔<br></p>                                         | <p>✖<br></p>                                                        | <p>✔<br></p>                                         |
| Statistics               | <p>✔<br></p>                                         | <p>✔<br></p>                                                        | <p>✔<br></p>                                         |
| File Extraction          | <p>✖<br></p>                                         | <p>✔<br></p>                                                        | <p>✔<br></p>                                         |
| Handling  pcaps over 1GB | <p>Medium performance<br></p>                        | <p>Low performance<br></p>                                          | <p>Good performance<br></p>                          |
| Ease of Management       | 4/5                                                  | 4/5                                                                 | 3/5                                                  |

### Use Cases

Custom queries and use cases allow to see common patterns and indicators of anomaly or malicious traffic.

#### Brim Query Reference

| Purpose                                    | Syntax                                        | Example Query                                                                                                                                  |
| ------------------------------------------ | --------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| Basic search                               | You can search any string and numeric value.  | Find logs containing an IP address or any value.`10.0.0.1`                                                                                     |
| Logical operators                          | Or, And, Not.                                 | Find logs contain three digits of an IP AND NTP keyword.`192 and NTP`                                                                          |
| Filter values                              | "field name" == "value"                       | Filter source IP.`id.orig_h==192.168.121.40`                                                                                                   |
| <p>List specific log file contents<br></p> | <p>_path=="log name"<br></p>                  | List the contents of the conn log file.`_path=="conn"`                                                                                         |
| Count field values                         | count () by "field"                           | Count the number of the available log files.`count () by _path`                                                                                |
| Sort findings                              | sort                                          | Count the number of the available log files and sort recursively.`count () by _path \| sort -r`                                                |
| Cut specific field from a log file         | \_path=="conn" \| cut "field name"            | Cut the source IP, destination port and destination IP addresses from the conn log file.`_path=="conn" \| cut id.orig_h, id.resp_p, id.resp_h` |
| List unique values                         | uniq                                          | <p>Show the unique network connections. </p><p><code>_path=="conn" | cut id.orig_h, id.resp_p, id.resp_h | sort | uniq</code></p>              |

Best practice is to always use the field filters to search for the event of interest.

| **Communicated Hosts**            | <p>Identify a list of network hosts to detect any suspicious activity.<br><code>_path=="conn" | cut id.orig_h, id.resp_h | sort | uniq</code></p>                                                                                                                                                                              |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Frequently Communicated Hosts** | <p>Identify which hosts communicate with each other most frequently.<br><code>_path=="conn" | cut id.orig_h, id.resp_h | sort | uniq -c | sort -r</code></p>                                                                                                                                                                   |
| **Most Active Ports**             | <p>Investigating the most active ports will help detect silent and well-hidden anomalies and used services.<br><code>_path=="conn" | cut id.resp_p, service | sort | uniq -c | sort -r count</code><br><br><code>_path=="conn" | cut id.orig_h, id.resp_h, id.resp_p, service | sort id.resp_p | uniq -c | sort -r</code> </p> |
| **Long Connections**              | <p>If the client is not designed to serve a continuous service, investigating the connection duration between two IP addresses can reveal possible anomalies like backdoors.<br><code>_path=="conn" | cut id.orig_h, id.resp_p, id.resp_h, duration | sort -r duration</code></p>                                              |
| **Transferred Data**              | <p>If the client is not designed to serve and receive files and act as a file server, it is important to investigate the total bytes for each connection.<br><code>_path=="conn" | put total_bytes := orig_bytes + resp_bytes | sort -r total_bytes | cut uid, id, orig_bytes, resp_bytes, total_bytes</code></p>              |
| **DNS and HTTP Queries**          | <p>Abnormal connections can help detect C2 communications and possible compromised/infected hosts.<br><code>_path=="dns" | count () by query | sort -r</code><br><br><code>_path=="http" | count () by uri | sort -r</code></p>                                                                                                |
| **Suspicious IP Hostnames**       | <p>Identifying suspicious and out of ordinary hostnames helps analysts to detect rogue hosts.<br><code>_path=="dhcp" | cut host_name, domain</code></p>                                                                                                                                                                        |
| **Suspicious IP Addresses**       | `_path=="conn" \| put classnet := network_of(id.resp_h) \| cut classnet \| count() by classnet \| sort -r`                                                                                                                                                                                                                     |
| **Detect Files**                  | <p>Detect the transfer of malware or infected files by correlating the hash values. This act is also valuable for detecting transferring of sensitive files.<br><code>filename!=null</code></p>                                                                                                                                |
| **SMB Activity**                  | <p>Detect possible malicious activities like exploitation, lateral movement and malicious file sharing.<br><code>_path=="dce_rpc" OR _path=="smb_mapping" OR _path=="smb_files"</code></p>                                                                                                                                     |
| **Known Patterns**                | <p>Alerts are generated against the common attack/threat/malware patterns and known by endpoint security products, firewalls and IDS/IPS solutions. This data source highly relies on available signatures, attacks and anomaly patterns.<br><code>event_type=="alert" or _path=="notice" or _path=="signatures"</code></p>    |
