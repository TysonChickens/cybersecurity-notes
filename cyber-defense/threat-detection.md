---
description: Defense is offense.
---

# Threat Detection

Cyber threats and criminals have advanced tactics to ensure they steal information and cause havoc.

Blue-team activities will require proactive approaches to practice threat detection, such as analyzing different logs, malware, and network traffic.

## Attack Scenario

Logs pointed to a likely attack chain and can be mapped to the Unified Kill chain. Known phases observed:

* **Persistence**: Adversary established persistence by creating a local user account they could use during the attack.
* **Discovery**: Gather information about their target by running commands to learn about the processes and software on devices to search for potential vulnerabilities.
* **Execution**: Scheduled jobs were created to provide an initial means of executing malicious code. This may also provide them with persistence and elevating their privileges.

The attack chain report included indicators of compromise (IOCs) and detected parameters. The attack techniques have been linked to the MITRE ATT\&CK framework:

| Attack Technique                                                                       | Indicators of Compromise                                                                                                                                                                                                                                                                                   | Required Detection Fields                                                            |
| -------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| [Account Creation](https://attack.mitre.org/techniques/T1136/)                         | <ul><li>EventID: 4720</li><li>Service: Security</li></ul>                                                                                                                                                                                                                                                  | <ul><li>Service</li><li>EventID</li></ul>                                            |
| [Software Discovery](https://attack.mitre.org/techniques/T1518/)                       | <ul><li>Category: Process Creation</li><li>EventID: 1</li><li>Service: Sysmon</li><li>Image: C:\Windows\System32\reg.exe</li><li>CommandLine: <code>reg query “HKEY_LOCAL_MACHINE\Software\Microsoft\Internet Explorer” /v svcVersion</code></li></ul>                                                     | <ul><li>Category</li><li>EventID</li><li>Image</li><li>CommandLine strings</li></ul> |
| <p><a href="https://attack.mitre.org/techniques/T1053/005/">Scheduled Task</a><br></p> | <ul><li>Category: Process Creation</li><li>EventID: 1</li><li>Service: Sysmon</li><li>Image: C:\Windows\System32\schtasks.exe</li><li>Parent Image: C:\Windows\System32\cmd.exe</li><li>CommandLine: <code>schtasks /create /tn "T1053_005_OnLogon" /sc onlogon /tr "cmd.exe /c calc.exe"</code></li></ul> | <ul><li>Category</li><li>EventID</li><li>Image</li><li>CommandLine strings</li></ul> |

## Chopping Logs with Sigma Rules

Sigma is an open-source generic signature language developed by Florian Roth & Thomas Patzke to describe log events in a structured format. The format uses a markup language called YAML. The common factors to note about YAML files:

* YAML is case-sensitive.
* Files should have the `.yml` extension.
* Spaces are used for indentation and not tabs.
* Comments are attributed using the `#` character.
* Key-value pairs are denoted using the colon `:` character.
* Array elements are denoted using the dash `-` character.

Log files are usually collected and stored in a database or a Security Information and Event Management (SIEM) solution for further analysis.

Sigma is a vendor-agnostic - Rules can be converted to a format that fits the target SIEM. Sigma was developed to satisfy the following scenarios:

* Make detection methods and signatures shareable alongside IOCs and YARA rules.
* Write SIEM searches that avoid vendor lock-in.
* Share signatures with threat intelligence communities.
* Write custom detection rules for malicious behavior based on specific conditions.

### Sigma Rule Syntax

* **Title**: Names the rule based on what to detect.
* **ID**: A global unique identifier that the developers of Sigma mainly use to maintain the order of **identification** for the rules submitted to the public repository in UUID format.
* **Status**: Describes the stage in which the rule maturity is while in use.
  * _Stable_: The rule may be used in production environments and dashboards.
  * _Test_: Trials are being done to the rule and could require fine-tuning.
  * _Experimental_: Rule is generic and being tested that could lead to false results.
  * _Deprecated_: The rule has been replaced and no longer yield accurate results.
  * _Unsupported_: The rule is not usable in its current state.
* **Description**: Provides more context about the rule and its intended purpose.
* **Log source**: Describes the log data to be used for the detection and other optional attributes:
  * _Product_: Selects all log outputs of a certain product (Windows, Apache).
  * _Category_: Selects the log files written by the selected product (Firewalls, web, and antivirus).
  * _Service_: Select only a subset of the logs (sshd on Linux or Security on Windows).
  * _Definition_: Describes the log source and its applied configurations.
* **Detection:** A required field in the detection rule describes the parameters of the malicious activity to alert for. The parameters divided in two parts:
  * _Search identifiers_ are the fields and values the detection should search for.
    * Can be enhanced using different modifiers appended to the field name with the pipe character `|`The main type of modifiers are known as **Transformation modifiers: **_**contains**_**, **_**endswith**_**, **_**startswith**_**, and **_**all**_
  * Condition expression - Action to be taken on the detection, such as selection or filtering.
* **FalsePositives**: A list of known false positives that may occur based on log data.
* **Level**: Describes The severity level which the security team should take under the written rule. Five levels: Informational -> Low -> Medium -> High -> Critical
* **Tags**: Adds information that can be used to categorize the rule. Sigma developers have defined a list of [predefined tags](https://github.com/SigmaHQ/sigma/wiki/Tags) with tactics and techniques from the MITRE ATT\&CK framework.

Sigma rules are converted to fit the desired SIEM query. A notable tool is [Uncoder.IO](https://uncoder.io/) - An open-source web Sigma converter for numerous SIEM and EDR platforms.
