---
description: 70+ Windows-based tools
---

# Sysinternals

The Sysinternals tools is a compilation of over 70+ Windows-based tools. Each falls into one of the categories:

* File and Disk Utilities
* Networking
* Process
* Security
* System Information
* Miscellaneous

Sysinternals tools and its website (sysinternals.com) were created by Mark Russinovich in the late '90s, along Bryce Cogswell under the company Wininternals Software.

* In 2006, Microsoft acquired Wininternals Software, and Mark Russinovich joined Microsoft. Today he is the CTO of Microsoft Azure.
* Made headlines when he reported Sony embedded rootkits into their music CDs back in 2005. Read more [here](https://www.zdnet.com/article/symantec-confesses-to-using-rootkit-technology/) how Sysinternals tools help make the discovery.

Sysinternals tools are popular among IT professionals who manage Windows systems and even for red teamers and adversaries.

## Install Sysinternals Suite

Sysinternals tool(s) can be downloaded and run from the local system, or can be run from the web.

* Can download individual tools instead of the entire suite by Sysinternals Utilities Index page, [https://docs.microsoft.com/en-us/sysinternals/downloads/](https://docs.microsoft.com/en-us/sysinternals/downloads/), and download the tool(s).

To run tools from the web, Sysinternals Live URL, [https://live.sysinternals.com/](https://live.sysinternals.com/). The tools are listed in alphabetical order and are not separated by categories.

To download the Sysinternals Suite, you can download the zip file from [here](https://docs.microsoft.com/en-us/sysinternals/downloads/sysinternals-suite).

* In Environment Variables, verify the system path variables includes the path to where Sysinternals Suite was extracted to.

Alternatively, a PowerShell module can download and install all of the Sysinternals tools.&#x20;

* PowerShell command: `Download-SysInternalsTools C:\Tools\Sysint`

### Using Sysinternals Live

Per the Sysinternals website, "Sysinternals Live is a service that enables you to execute Sysinternals tools directly from the Web without hunting for and manually downloading them. Simply enter a tool's Sysinternals Live path into Windows Explorer or a command prompt as `live.sysinternals.com/toolname` or `\\live.sysinternals.com\tools<toolname>`"

WebDAV client must be installed and running on the machine. The WebDAV protocol allows a local machine to access a remote machine running a WebDAV share and perform actions.

* On a Windows 10 client, the WebDAV client is installed but the client is most likely not running. If you try to run a Sysinternals tool it will fail with a message "The network path was not found."
* **Network Discovery** also needs to be enabled from the **Network and Sharing Center**.
  * Command line to launch it: `control.exe /name Microsoft.NetworkAndSharingCenter`
* To install with PowerShell, `Install-WindowsFeature WebDAV-Redirector –Restart`. The server needs to reboot for the installation to complete.
  * After reboot, verify `Get-WindowsFeature WebDAV-Redirector | Format-Table –Autosize` using PowerShell.

Method 1: Launch from command line `\\live.sysinternals.com\tools<toolname>`

Method 2: Run tool from a mapped drive `net use *` `\\live.sysinternals.com\tools<toolname>`

* The asterisk will auto-assign a drive letter. Can be replaced with an actual drive letter instead.

## File and Disk Utilities

Will try to cover a few tools in each category.

### Sigcheck

{% embed url="https://learn.microsoft.com/en-us/sysinternals/downloads/sigcheck" %}

A command-line utility that shows file version number, timestamp, and digital signature details. Includes option to check a file's status on VirusTotal.

_Use Case_: Check for unsigned files in C:\Windows\System32

_Command_: `sigcheck -u -e C:\Windows\System32`

_Parameter Usage:_

* `-u` show only unsigned files or files unknown by VirusTotal if enabled.
* `-e` Scan executable images only (regardless of extension).

### Streams

{% embed url="https://learn.microsoft.com/en-us/sysinternals/downloads/streams" %}

The NTFS file system provides applications the ability to create alternate data streams of information. By default, all data is stored in a file's main unnamed data stream, but by using the syntax 'file:stream', you are able to read and write to alternates.

Alternate Data Streams (ADS) is a file attribute specific to Windows NTFS (New Technology File System). Every file has at least one data stream ($DATA) and ADS allows files to contain more than one stream of data.

* There are 3rd party executables to display this data, while native Windows Explorer does not display ADS to the user. Powershell also gives the ability to view ADS for files.
* Malware writers have used ADS to hide data in an endpoint but not all are malicious.

### SDelete

{% embed url="https://learn.microsoft.com/en-us/sysinternals/downloads/sdelete" %}

A command line utility that allows to delete one or more files and/or directories to cleanse the free space on a logical disk.

Per the documentation page, SDelete (Secure Delete) implemented the **DOD 5220.22-M** (Department of Defense clearing and sanitizing protocol).

<figure><img src="https://assets.tryhackme.com/additional/sysinternals/sdelete.png" alt=""><figcaption></figcaption></figure>

SDelete has been used by adversaries and is associated with MITRE techniques [T1485](https://attack.mitre.org/techniques/T1485/) (Data Destruction) and [T1070.004](https://attack.mitre.org/techniques/T1070/004/) (Indicator Removal on Host: File Deletion). It's MITRE ID [S0195](https://attack.mitre.org/software/S0195/).

## Networking Utilities

### TCPView

{% embed url="https://learn.microsoft.com/en-us/sysinternals/downloads/tcpview" %}

A program that will show detailed listings of all TCP and UDP endpoints on the system, including the local and remote addresses and state of TCP connections. TCPView provides more information and nicely presented of the Netstat program. The TCPView download includes Tcpvcon, a command-line version with the same functionality.

* Apply additional filtering by turning off TCP v4, TCP v6, UDP v4, and UDP v6 at the top toolbar, depending on which protocols we want to display.

## Process Utilities

_Some tools may require to run as administrator._

### Autoruns

{% embed url="https://learn.microsoft.com/en-us/sysinternals/downloads/autoruns" %}

The utility provides knowledge of auto-starting locations of any startup monitor, show what programs are configured to run during system boot or login. Autoruns reports Explorer shell extensions, toolbars, browser helper objects, Winlogon notifications, auto-start services, and more - beyond other autostart utilities.

### ProcDump

{% embed url="https://learn.microsoft.com/en-us/sysinternals/downloads/procdump" %}

A command-line utility to monitor an application for CPU spikes and generating crash dumps to determine the cause of the spike.

### Process Explorer

{% embed url="https://learn.microsoft.com/en-us/sysinternals/downloads/process-explorer" %}

Show a list of the current active processes, including the names of their owning accounts.

* Handle mode to see the handles the process selected the window has opened.
* DLL mode allows to see DLLs and memory-mapped files the process has loaded.

<figure><img src="https://assets.tryhackme.com/additional/sysinternals/procexp-colors.png" alt=""><figcaption></figcaption></figure>

### Process Monitor

{% embed url="https://learn.microsoft.com/en-us/sysinternals/downloads/procmon" %}

An advanced monitoring tool for Windows shows real-time file system, registry and process/thread activity. Provides a comprehensive list of event properties such as session IDs and user names, reliable process information, full thread stacks with integrated symbol support for each operation, simultaneously logging to a file and more - Powerful features for system troubleshooting and malware hunting toolkit.

[Here](https://adamtheautomator.com/procmon/) is a useful guide on configuring ProcMon.

### PsExec

{% embed url="https://learn.microsoft.com/en-us/sysinternals/downloads/psexec" %}

A light-weight telnet-replacement that lets you execute processes on other systems, complete with full interactivity for console applications, without having to manually install client software.

PsExec is another tool that is utilized by adversaries. This tool is associated with MITRE techniques [T1570](https://attack.mitre.org/techniques/T1570) (Lateral Tool Transfer), [T1021.002](https://attack.mitre.org/techniques/T1021/002) (Remote Services: SMB/Windows Admin Shares), and [T1569.002](https://attack.mitre.org/techniques/T1569/002) (System Services: Service Execution). It's MITRE ID is [S0029](https://attack.mitre.org/software/S0029/).

## Security Utilities

### Sysmon

{% embed url="https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon" %}

System Monitor (sysmon) is a Windows system service and device driver to monitor and log system activity to the Windows event log. It collects the events to generate using Windows Event Collection or SIEM agents to help identify malicious or anamolous activity and understand how intruders and malware operate on the network.

## System Information

### WinObj

{% embed url="https://learn.microsoft.com/en-us/sysinternals/downloads/winobj" %}

A 32-bit Windows NT program that uses the native Windows NT API (provided by NTDLL.DLL) to access and display information on the NT Object Manager's name space.

Remember that Session 0 is the OS session and Session 1 is the User session.

* Session 1 will be for the first user logged into the system.

## Miscellaneous

### BgInfo

{% embed url="https://learn.microsoft.com/en-us/sysinternals/downloads/bginfo" %}

Automatically displays relevant information about a Windows computer on the desktop's background, such as the computer name, IP address, service pack version, and more.

### RegJump

{% embed url="https://learn.microsoft.com/en-us/sysinternals/downloads/regjump" %}

Takes a registry path and makes Regedit open to that path. It accepts root keys in standard (e.g. HKEY\_LOCAL\_MACHINE) and abbreviated form (e.g. HKLM).

* Using RegJump will open the Registry Editor and automatically open the editor directly at the path

### Strings

scans the file you pass it for UNICODE (or ASCII) strings of a default length of 3 or more UNICODE (or ASCII) characters.

## Summary

Tools will help troubleshoot as a security engineer in certain scenarios such as:

* ProcExp = Inspect the agent process, its properties, and associated threads and handles.
* ProcMon = Investigate if there were any indicators on why the agent was not operating as it should.
* ProcDump = Create a dump of the agent process to send to the vendor for further analysis.
