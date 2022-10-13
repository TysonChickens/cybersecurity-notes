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


\


\
