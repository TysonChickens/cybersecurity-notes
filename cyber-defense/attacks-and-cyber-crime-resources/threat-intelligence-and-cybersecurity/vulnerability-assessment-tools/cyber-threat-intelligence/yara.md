---
description: >-
  "The pattern matching swiss knife for malware researchers (and everyone
  else)."
---

# YARA

YARA can identify information based on both binary and textual patterns, such as hexadecimal and strings contained within a file.

* Rules are used to label these pattern to determine if a file is malicious or not, based on the features - or patterns - it presents. Strings are a fundamental component of programming languages and applications use strings to store data such as text.

We could write a YARA rule to search for "hello world" in every program on the operating system. Malware uses strings to store textual data similar to a "Hello World" program. Here are some examples of the data that various malware types store within strings:

| **Type**   | **Data**                                                                                                                              | **Description**                                         |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| Ransomware | <p><a href="https://www.blockchain.com/btc/address/12t9YDPgwueZ9NyMgw519p7AA8isjr6SMw">12t9YDPgwueZ9NyMgw519p7AA8isjr6SMw</a><br></p> | <p>Bitcoin Wallet for ransom payments<br></p>           |
| Botnet     | <p>12.34.56.7<br></p>                                                                                                                 | The IP address of the Command and Control (C\&C) server |

## Create a YARA Rule

Every `yara` command requires two arguments to be valid:

1. The rule file created.
2. Name of file, directory, or process ID to use the rule for.

Every rule must have a name and condition.

For example, to use "myrule.yar" on directory "some directory", use the following command:

`yara myrule.yar somedirectory`

If the file does not exist, YARA will output an error. If the file does exist, we are given an output of the rule.

### Expanding on YARA Rules and Conditions

Yara has a few conditions that will be helpful. Read [here](https://yara.readthedocs.io/en/stable/writingrules.html).

* Desc / Meta - YARA rule is reserved for descriptive information by the author of the rule. `desc` is short for description, to summarize what the rule checks are for. Anything within this section does not influence the rule itself. Similar to commenting code and useful to summarize the rule.
* Strings - Used to search for specific text or hexadecimal in files or programs. An example is to search a directory for all files containing "Hello World!" rule would look like:

<pre><code>rule helloworld_checker {
    strings:
<strong>        $hello_world = "Hello World!"
</strong><strong>        $hello_world_lowercase = "hello world"
</strong><strong>        $hello_world_uppercase = "HELLO WORLD"
</strong><strong>        
</strong><strong>    condition:
</strong><strong>        any of them
</strong>}
</code></pre>

Now, any file with the strings of will trigger the rule:

1. Hello World!
2. hello world
3. HELLO WORLD

* Conditions - Much like regular programming, there are operators to use such as <=, >=, and !=

<pre><code>rule helloworld_checker {
    strings:
<strong>        $hello_world = "Hello World!"
</strong><strong>        
</strong><strong>    condition:
</strong><strong>        #hello_world &#x3C;= 10
</strong><strong>}
</strong></code></pre>

The rule will now look for the "Hello World!" string and only rule matches if there are less than or equal to ten occurrences of the "Hello World!" string.

* Combine keywords such as:
  * and
  * not
  * or

To combine multiple conditions to check if a file has a string and is of a certain size to checking **less than** < 10 kb and has "Hello World!":

<pre><code>rule helloworld_checker {
    strings:
<strong>        $hello_world = "Hello World!"
</strong><strong>        
</strong><strong>    condition:
</strong><strong>        #hello_world and filesize &#x3C; 10
</strong><strong>}
</strong></code></pre>

The rule will only match if both conditions are true.

### Anatomy of a YARA Rule

Information security researcher "fr0gger\_" has created a [handy cheat-sheet](https://medium.com/malware-buddy/security-infographics-9c4d3bd891ef#18dd) that breaks down and visualizes the elements of a YARA rule.

<figure><img src="https://miro.medium.com/max/875/1*gThGNPenpT-AS-gjr8JCtA.png" alt=""><figcaption><p>Anatomy YARA Rule</p></figcaption></figure>

## YARA Modules

YARA is able to integrate with other libraries and frameworks such as the Cuckoo Sandbox or Python's PE Module to improve technicality of rules.

### Cuckoo

Cuckoo Sandbox is an automated malware analysis environment. This module allows to generate YARA rules based upon the behaviors discovered from Cuckoo Sandbox. As the environment executes malware, allows to create rules on specific behaviors such as runtime strings and the like.

### Python PE

Python PE module allows to create YARA rules from the various sections and elements of the Windows Portable Executable (PE) structure.

* Examining a PE file's contents is essential technique in malware analysis because behaviors such as cryptography or worming can be identified without reverse engineering or execution of the sample.

## Other Tools and YARA

There are plenty of [GitHub resources](https://github.com/InQuest/awesome-yara) and open-source tools that can be utilized to leverage YARA in hunt operation and/or incident response engagements.

### LOKI

LOKI is a free open-source IOC (Indicator of Compromise) scanner created/written by Florian Roth.

Based on the GitHub page, detected is based on 4 methods:

1. File Name IOC Check
2. YARA Rule Check
3. Hash Check
4. C2 Back Connect Check

LOKI can be used on both Windows and Linux systems.

#### Using LOKI and YARA Rule Set

IOCs (hashes, IP addresses, domain names, etc.) will be shared information so rules can be created to detect threats in an environment, along with YARA rules. Using tools such as Loki, you will need to add your own rules based on your threat intelligence gathers or findings from an incident response engagement (forensics).&#x20;

### THOR

THOR Lite is Florian's newest multi-platform IOC and YARA scanner. You need to subscribe to their mailing list to obtain a copy of the binary. **Note that THOR is geared towards corporate customers**. THOR Lite is the free version.

### FENRIR

This is the 3rd tool created to address the issue from its predecessors, where requirements must be met for them to function. Fenrir is a bash script; it will run on any system capable of running bash (nowadays even Windows).

### YAYA (_Yet Another Yara Automaton_)

Created by the [EFF](https://www.eff.org/deeplinks/2020/09/introducing-yaya-new-threat-hunting-tool-eff-threat-lab) (Electronic Frontier Foundation) and released in September 2020. According to their website, "_YAYA is a new open-source tool to help researchers manage multiple YARA rule repositories. YAYA starts by importing a set of high-quality YARA rules and then lets researchers add their own rules, disable specific rulesets, and run scans of files._"

* Currently, YAYA only runs on Linux systems.

## Creating YARA Rules with yarGEN

[yarGEN](https://github.com/Neo23x0/yarGen) is another tool created by Florian Roth to generate YARA rules. From the README - "_The main principle is the creation of yara rules from strings found in malware files while removing all strings that also appear in goodware files. Therefore yarGen includes a big goodware strings and opcode database as ZIP archives that have to be extracted before the first use_."

**Note**: Another tool created to assist with this is called [yarAnalyzer](https://github.com/Neo23x0/yarAnalyzer/) to assist in creating own YARA rules.

## Valhalla

Valhalla is an online YARA feed created and hosted by [Nextron-Systems](https://www.nextron-systems.com/valhalla/). Per the website, "_Valhalla boosts detection capabilities with the power of thousands of hand-cracted high-quality YARA rules."_
