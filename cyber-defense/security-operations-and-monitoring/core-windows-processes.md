---
description: Core processes in a Windows operating system.
---

# Core Windows Processes

Windows operating system is the most used in the world and users are happy that it works - Most do not understand the inter-workings.

Malware and attacks have evolved and antivirus has struggled to keep up designed to catch evil.

New security tools such as EDR (Endpoint Detection and Response) have been created because anti-viruses cannot catch every malicious binary and process running on the endpoint.

* These new tools are still not 100% effective and still bypass the defenses running on the endpoint.
  * The tool will alert of a suspicious binary or process so an analyst can investigate and take action.

## Task Manager

A built-in GUI Windows utility to allow users to see what processes on running on the Windows system - Provides information on resource usage, each process CPU and memory utilization.

### Processes

* **Type** - Each process belongs 1 of 3 categories (Apps, Background Process, or Windows process).
* **Publisher** - Author of the program/file.
* **PID** - Process Identifier Number. Windows assigns a unique process identifier each time a program starts. If the same program has multiple running processes, each will have a unique PID.
* **Process name** - File name of the process name.
* **Command line** - The full command used to launch the process.
* **CPU** - The amount of CPU (processing power) the process uses.
* **Memory** - Amount of physical memory utilized by the process.

There are other utilities that are more powerful to analyze _parent process information_ and parent-child process view - **Process Hacker** and **Process Explorer**

## System

The first Windows process on the list is **System.** The PID for system is always 4.

The official definition from Windows Internals 6th Edition:\
"_The System process (process ID 4) is the home for a special kind of thread that runs only in kernel mode a kernel-mode system thread. System threads have all the attributes and contexts of regular user-mode threads (such as a hardware context, priority, and so on) but are different in that they run only in kernel-mode executing code loaded in system space, whether that is in Ntoskrnl.exe or in any other loaded device driver. In addition, system threads don't have a user process address space and hence must allocate any dynamic storage from operating system memory heaps, such as a paged or non-paged pool._"

Visit the following [link](https://docs.microsoft.com/en-us/windows-hardware/drivers/gettingstarted/user-mode-and-kernel-mode) to understand user vs. kernel mode.

## System -> smss.exe

The next process is **smss.exe (Session Manager Subsystem**), also known as the Windows Session Manager, is responsible for creating new sessions. This is the first user-mode process started by the kernel.

* Starts the kernel and user modes of the Windows subsystem. This includes win32k.sys (kernel mode), winsrv.dll (user mode), and csrss.exe (user mode). Read more about the NT Architecture [here](https://en.wikipedia.org/wiki/Architecture\_of\_Windows\_NT).
* Smss.exe starts csrss.exe (Windows subsystem) and wininit.exe in Session 0, an isolated Windows session for the operating system.
* csrss.exe and winlogon.exe in Session 1, which is the user session. Read more about this process [here](https://en.wikipedia.org/wiki/Session\_Manager\_Subsystem).

SMSS is also responsible for creating environment variables, virtual memory paging files and starts winlogon.exe (Windows Logon Manager).

* Any other subsystem listed in the `Required` value of `HKLM\System\CurrentControlSet\Control\Session Manager\Subsystems` is also launched.

### csrss.exe

**csrss.exe (Client Server Runtime Process)** is the user-mode side of the Windows subsystem. This process is always running and is critical to system operation. These processes are spawned by smss.exe, which self-terminates itself

* If the process is terminated, it will result in system failure.
* Responsible for the Win32 console window and process thread creation and deletion.

This process is also responsible for making the Windows API available to other processes, mapping drive letters, and handling the Windows shutdown process. You can read more about this process [here](https://en.wikipedia.org/wiki/Client/Server\_Runtime\_Subsystem).

### wininit.exe

The **Windows Initialization Process, wininit.exe** - Responsible to launching services.exe (Service Control Manager), lsass.exe (Local Security Authority), and lsaiso.exe within Session 0.

* lsaiso.exe process is associated with Credential Guard and KeyGuard (only if Credential Guard is enabled).

### winit.exe -> services.exe

The Service Control Manager (SCM) or services.exe - Handle system services: loading services, interacting/starting/ending services. It maintains a database that can be queried using a Windows built-in utility, sc.exe.

* Information to services is stored in the registry - `HKLM\System\CurrentControlSet\Services`
* This process also loads device drivers marked auto-start into memory.
* A successful user login sets the value of the Last Known Good control configuration `HKLM\System\Select\LastKnownGood` to the CurrentControlSet.
* Process also important to other key processes: svchost.exe, spoolsv.exe, msmpeng.exe, dllhost.exe, and more...read more about this process [here](https://en.wikipedia.org/wiki/Service\_Control\_Manager).

### wininit.exe -> services.exe -> svchost.exe

The **Service Host** (Host Process for Windows Services), or **svchost.exe**, is responsible for hosting and managing Windows services.

* Services running in this process are implemented as DLLs. The DLL is stored in the registry for the service under the Parameters subkey in ServiceDLL. Full path: `HKLM\SYSTEM\CurrentControlSet\Services\SERVICE NAME\Parameters`
* The -k parameter from svchost.exe binary/command path is for grouping similar services to share the same process. This concept was based on the OS design and implemented to reduce resource consumption. Starting from Windows 10 Version 1703, services grouped into host processes changed.

svchost.exe will always have multiple running processes on any Windows system and a common target for malicious use. A tactic for malware to masquerade this process and install/call a malicious service (DLL).

### lsass.exe

Local Security Authority Subsystem Service (LSASS) is a process in Microsoft Windows operating systems responsible for enforcing security policy on the system.

* Verifies users login to a Windows computer or server, handles password changes, and creates access tokens. Also writes to Windows Security Log.
* It creates security tokens for SAM (Security Account Manager), AD (Active Directory), and NETLOGON. It uses authentication packages specified in `HKLM\System\CurrentControlSet\Control\Lsa`.

Common tools such as mimikatz are used to dump credentials to hide in plain sight to mimic as Lsass.exe.

### winlogon.exe

Windows Logon is responsible for handling the **Secure Attention Sequence** (SAS). It is the ALT+CTRL+DELETE key combination users press to enter their username & password.

* This process is also responsible for loading the user profile. It loads the user's NTUSER.DAT into HKCU, and userinit.exe loads the user's shell. Read more about this process [here](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc939862\(v=technet.10\)?redirectedfrom=MSDN).
* It is also responsible for locking the screen and running the user's screensaver, among other functions. You can read more about this process [here](https://en.wikipedia.org/wiki/Winlogon).

### explorer.exe

Windows Explorer gives the user access to their folders and files. Also provides functionality for other features such as the Start Menu and Taskbar.

* Winlogon process runs userinit.exe, which launches the value in `HKLM\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\Shell`. Userinit.exe exits after spawning explorer.exe. Because of this, the parent process is non-existent.
* There will be many child processes for explorer.exe

## Summary

With the introduction of Windows 10, new processes have been added to the list of core processes. It is important to understand how Windows operating system functions as a defender is vital. For more information,&#x20;

* [https://www.threathunting.se/tag/windows-process/](https://www.threathunting.se/tag/windows-process/)
* [https://www.sans.org/security-resources/posters/hunt-evil/165/download](https://www.sans.org/security-resources/posters/hunt-evil/165/download)
* [https://docs.microsoft.com/en-us/sysinternals/resources/windows-internals](https://docs.microsoft.com/en-us/sysinternals/resources/windows-internals)
