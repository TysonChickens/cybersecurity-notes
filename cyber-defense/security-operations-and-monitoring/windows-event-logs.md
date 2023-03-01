# Windows Event Logs

Event logs record events taking palce in the execution of a system to provide a a trail to understand the activity of the system and diagnose problems.

* Help gives clues to see what led to a problem. The operating system writes messages to the logs.
* SIEMs (Security Information and Event Management) such as Splunk and Elastic to query logs from multiple devices and investigate.

<figure><img src="https://assets.tryhackme.com/additional/win-event-logs/siem.png" alt=""><figcaption></figcaption></figure>

## Event Viewer

The Windows Event Logs are not text files that can be viewed using a text editor. The raw data can be translated into XML using the Windows API.

* The log files are stored in a proprietary format with a .evt or .evtx extension found `C:\Windows\System32\winevt\Logs`

### Elements of Windows Event Logs &#x20;

* **System Logs:** Records events about the OS. Includes hardware changes, device drivers system changes, and other system related activities.&#x20;
* **Security Logs:** Logon/Logoff activities, system audit policies. Helpful to investigate unauthorized activity.
* **Application Logs:** Related to applications installed-information include application errors, events, and warnings.
* **Directory Service Events:** Active Directory changes/activities on domain controllers.
* **File Replication Service:** Windows servers sharing of Group Policies and logon scripts to domain controllers to client servers.
* **DNS:** Record domain events and to map out.&#x20;
* **Custom:** Applications require custom data storage. They can control the log size or attach other parameters.

**5 Event Types:**&#x20;

<figure><img src="https://assets.tryhackme.com/additional/win-event-logs/five-event-types.png" alt=""><figcaption></figcaption></figure>

&#x20;Main ways to access event logs on Windows:

1. **Event Viewer** (GUI-based)
2. **Wevtutil.exe** (command-line)
3. **Get-WinEvent** (PowerShell cmdlet)

Event Viewer is included on any Windows system, Microsoft Management Console (MMC).

* Can be launched with command `eventvwr.msc`
* GUI-based to analyze/ interact logs.

## wevtutil.exe

{% embed url="https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/wevtutil" %}

Per Microsoft, "enables you to retrieve information about event logs and publishers. Also use this command to install and uninstall event manifests, to run queries, and to export, archive, and clear logs."

With any tool, access help commands with `wevtutil.exe /?`

```powershell
PS> C:\Users\Administrator> wevtutil.exe /?
Windows Events Commandline Utility.
Enables you to retrieve information about event logs and publishers, install and uninstall event manifests, run queries, and export, archive and clear logs.

Usage:

You can use either the short (for example, ep /uni) or long (for example, enum-publishers /unicode) version of the command and option names. Commands, options and option values are not case-sensitive.

Variables are noted in all upper-case.

wevtutil COMMAND [ARGUMENT [ARGUMENT] ...] [/OPTION:VALUE [/OPTION:VALUE] ...]

Commands:

el  | enum-logs              List log names.
gl  | get-log                Get log configuration information.
sl  | set-log                Modify configuration of a log.
ep  | enum-publishers        List event publishers.
gp  | get-publisher          Get publisher configuration information.
im  | install-manifest       Install event publishers and logs from manifest.
um  | uninstall-manifest     Uninstall event publishers and logs from manifest.
qe  | query-events           Query events from a log or log file.
gli | get-log-info           Get log status information.
epl | export-log             Export a log.
al  | archive-log            Archive an exported log.
cl  | clear-log              Clear a log.
```

## Get-WinEvent

{% embed url="https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.diagnostics/get-winevent?view=powershell-5.1" %}

A PowerShell cmdlet to "get events from event logs and event tracing log files on local and remote computers".

### Get all logs from computer

Obtain all event logs locally.

```powershell
Get-WinEvent -ListLog *
```

### Get event log providers and log names

Result in the event log providers and their associated logs.

* Name is the provider.
* LogLinks is the log is written to.

```powershell
Get-WinEvent -ListProvider *
```

### Log Filtering

Allows to select events from an event log using the **Where-Object** cmdlet:

```powershell
Get-WinEvent -LogName Application | Where-Object { $_.ProviderName -Match 'WLMS' }
```

* Per Microsoft, it is inefficient to send objects down the pipeline to Where-Object command.

The use of the Get-WinEvent cmdlet's FilterHashtable parameter is recommended to filter event logs:

```powershell
Get-WinEvent -FilterHashtable @{
  LogName='Application' 
  ProviderName='WLMS' 
}
```

Syntax of a hash table:

* Begin the hash table with an @ sign.
* Enclose the hash table in braces {}
* Enter one or more key-value pairs for the content of the hash table.
* Use an equal sign (=) to separate each key from its value.

{% embed url="https://learn.microsoft.com/en-us/powershell/scripting/samples/Creating-Get-WinEvent-queries-with-FilterHashtable?view=powershell-7.3&viewFallbackFrom=powershell-7.1" %}

## XPath Queries

The W3C created XPath, or XML Path Language in full, to provide a standard syntax and semantics for addressing parts of an XML document and manipulating strings, numbers, and booleans.

* Windows Event  Log supports a subset of XPath 1.0

{% embed url="https://learn.microsoft.com/en-us/windows/win32/wes/consuming-events#xpath-10-limitations" %}

An XPath event query starts with '\*' or 'Event'. Note both wevtutil and Get-WinEvent support XPath queries as event filters.

<figure><img src="https://assets.tryhackme.com/additional/win-event-logs/xpath-3c.png" alt=""><figcaption></figcaption></figure>

Example command: `Get-WinEvent -LogName Application -FilterXPath '*/System/EventID=100'`

* Can also query a different element such as Provider Name.
* Combine both queries with EventID and Provider Name: `Get-WinEvent -LogName Application -FilterXPath '*/System/EventID=101 and */System/Provider[@Name="WLMS"]'`
* Find WLMS events with a System Time: `Get-WinEvent -LogName Application -FilterXPath '*/System/Provider[@Name="WLMS"] and */System/TimeCreated[@SystemTime="2020-12-15T01:09:08.940277500Z"]'`
* Find a user named Sam with an Logon Event ID of 4720: `Get-WinEvent -LogName Security -FilterXPath '*/EventData/Data[@Name="TargetUserName"]="System" and */System/EventID=4720'`

## Event IDs

Need to know what to look for when monitoring and hunting. Here is a [Windows Logging Cheat Sheet (Windows 7 - Windows 2012](https://static1.squarespace.com/static/552092d5e4b0661088167e5c/t/580595db9f745688bc7477f6/1476761074992/Windows+Logging+Cheat+Sheet\_ver\_Oct\_2016.pdf) to look for what event IDs based on different categories.

Get a list of event IDs to monitor/hunt from [MITRE ATT\&CK](https://attack.mitre.org/)!

The last two resources are from Microsoft:

* [Events to Monitor](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/plan/appendix-l--events-to-monitor) (Best Practices for Securing Active Directory)
* [The Windows 10 and Windows Server 2016 Security Auditing and Monitoring Reference](https://www.microsoft.com/en-us/download/confirmation.aspx?id=52630) (a comprehensive list \[over 700 pages])

_Note: Some events will not be generated by default, and certain features will need to be enabled/configured on the endpoint, such as PowerShell logging. This feature can be enabled via Group Policy or the Registry._

`Local Computer Policy > Computer Configuration > Administrative Templates > Windows Components > Windows PowerShell`

Another feature to enable/configure is Audit Process Creation, which will generate event ID 4688. This will allow command-line process auditing.pdf to epub

`Local Computer Policy > Computer Configuration > Administrative Templates > System > Audit Process Creation`
