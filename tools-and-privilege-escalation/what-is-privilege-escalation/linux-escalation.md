---
description: >-
  From enumeration to exploitation and privilege escalation using a variety of
  techniques.
---

# Linux Escalation

## Enumeration

Enumeration is the first to take when gaining access to any system. Penetration testing engagements, unlike CTF machines do not end once gain access to a specific system or user privilege level. Enumeration is also important in post-exploit phase as it is before.

### hostname

`hostname` command will return the hostname of the target machine and could provide information about the target system's role within the corporate network.

### uname -a

Will print system information giving additional detail about the kernel used by the system. This will be useful for when searching for any potential kernel vulnerabilities leading to privilege escalation.

### /proc/version

The proc filesystem (procfs) provides information about the target system processes. `/proc/version` may give information on the kernel version and additional data such as whether a compiler is installed.

### /etc/issue

Systems can also be identified the `/etc/issue` file. The file usually contains information about the operating system.

### ps

The `ps` command is an effective way to see the running processes on a Linux system. The output of the `ps` (Process Status) will show the following:

* PID: The process ID (unique to the process)
* TTY: Terminal type used by the user
* Time: Amount of CPU time used by the process (NOT time process has been running for)
* CMD: The command or executable running (NOT display any command line parameter)

The ps command provides several options:

* `ps -A`: View all running processes
* `ps axjf`: View process tree
* `ps aux`: Will show processes for all users (a), display the user that launched the process (u), and show processes that are not attached to a terminal (x).

### env

`env` command will show environmental variables. The PATH variable may have compiler or a scripting language that could be used to run code on the target system or leveraged for privilege escalation.

### sudo -l

The target system may be configured to allow users to run some (or all) commands with root privileges.

* `sudo -l` command can be used to list all commands user can run using sudo.

### ls

`ls` command with the `-la` parameter will show all files in the working directory.

### id

`id` command will provide a general overview of the user's privilege level and group memberships.

### /etc/passwd

Reading the `/etc/passwd` file can be an easy way to discover users on the system.

### history

Looking at earlier commands with `history` command will provide us an idea about the target system, have stored information such as passwords or usernames.

### ifconfig

The command will give us information about the network interfaces of the system.&#x20;

* `ip route` command to see which network routes exist.

### netstat

After checking for existing interfaces and network routes, gather more information with the `netstat` command can be used with several different options on existing connections.

* `netstat -a`: Show all listening ports and established connections.
* `netstat -at` or `netstat -au` can also be used to list TCP or UDP protocols.
* `netstat -l`: List ports in "listening" mode to open and ready to accept incoming connections.
* `netstat -s` : List network usage statistics by protocol and can be used with `-t` or `-u` options to limit the output to a specific protocol.
* `netstat -tp`: f

### find

Search the target system for important information and potential privilege escaltion vectors.

* Find files with example commands:
  * `find . -name flag1.txt`: find the file named "flag1.txt" in the current directory
  * `find /home -name flag1.txt`: find the file names "flag1.txt" in the /home directory
  * `find / -type d -name config`: find the directory named config under “/”
  * `find / -type f -perm 0777`: find files with the 777 permissions (files readable, writable, and executable by all users)
  * `find / -perm a=x`: find executable files
  * `find /home -user frank`: find all files for user “frank” under “/home”
  * `find / -mtime 10`: find files that were modified in the last 10 days
  * `find / -atime 10`: find files that were accessed in the last 10 day
  * `find / -cmin -60`: find files changed within the last hour (60 minutes)
  * `find / -amin -60`: find files accesses within the last hour (60 minutes)
  * `find / -size 50M`: find files with a 50 MB size
*   Find folder and files that can be written to or executed from:

    * `find / -writable -type d 2>/dev/null` : Find world-writeable folders
    * `find / -perm -222 -type d 2>/dev/null`: Find world-writeable folders
    * `find / -perm -o w -type d 2>/dev/null`: Find world-writeable folders


*   Find development tools and supported languages:

    * `find / -name perl*`
    * `find / -name python*`
    * `find / -name gcc*`



## Kernel Exploits Escalation

Privilege escalation leads to root privileges. This can be a simple exploit on an existing vulnerability or accessing another user account that has more privileges, information, or access.

The kernel on Linux system manages the communication between components such as the memory on the system and applications. This critical function requires the kernel to have specific privileges by a successful exploit potentially to lead to root privileges.

The kernel exploit methodology is simple:

1. Identify the kernel version.
2. Search and find an exploit code for the kernel version of the target system.
3. Run the exploit.

* Remember that a failed kernel exploit can lead to a system crash. Make sure the potential outcome is acceptable within the scope of penetration testing engagement before attempting a kernel exploit.

**Research sources**:

* Based on findings, use Google to search for an existing exploit code.
* Sources such as [https://www.linuxkernelcves.com/cves](https://www.linuxkernelcves.com/cves) can be useful.

**Hints/Notes:**

* Being too specific about the kernel version when searching for exploits on Google, Exploit-DB, or searchsploit.
* Understand how the exploit code BEFORE launch it. Some exploits can make changes on the operating system that would make them unsecured in further use or make irreversible changes to the system, creating problems later.
* Some exploits may require further interaction once they are run. Read all comments and instructions provided with the exploit code.
* Transfer the exploit code from machine to the target system using the `SimpleHTTPServer` python module and `wget` respectively.

## Sudo Escalation

The sudo command, by default, allows to run a program with root privileges. Under some conditions, system administrators may need to give regular users some flexibility on their privileges. An example is a junior SOC analyst may need to use Nmap regularly but not cleared for full root access.

* Any user can check its current situation related to root privileges using the `sudo -l` command.
* [https://gtfobins.github.io/](https://gtfobins.github.io/) is a valuable source that provides information on how any program, on which may have sudo rights, can be used.
  * Leverage application functions where some applications will not have a known exploit within context. For example, Apache2 has an option that supports loading alternative configuration files (`-f` to specify an alternate ServerConfigFile).
    * Loading the `/etc/shadow` file using this option will result in an error message that includes the first line of the shadow file.

### LD\_PRELOAD

Some systems have LD\_PRELOAD environment option - A function that allows any program to use shared libraries.

* If the "envkeep" option is enabled, we can generate a shared library which will be loaded and executed before the program is run. Note the `LD_PRELOAD` option will be ignored if the real user ID is different from the effective user ID.

The steps of privilege escalation:

1. Check for `LD_PRELOAD` (with the env\_keep option).
2. Write a simple C code compiled as a share object (.so extension) file.
3. Run the program with sudo rights and the `LD_PRELOAD` option pointing to our .so file.

Save the code as shell.c and compile it using gcc into a shared object file using `gcc -fPIC -shared -o shell.so shell.c -nostartfiles`

Run the program by specifiying the shared object file when launching any program user can run with `sudo LD_PRELOAD=/home/user/ldpreload/shell.so find` - Results in shell spawn with root privileges.

## SUID Privilege

Linux privilege controls rely on controlling the users and files interactions. Files can have read, write, and execute permissions. SUID (Set-user Identification) and SGID (Set-group Identification) allow files to be executed with the permission level of the file owner or the group owner.

`find / -type f -perm -04000 -ls 2>/dev/null` will list files that have SUID or SGID bits set.

<figure><img src="https://i.imgur.com/fJEeZ4m.png" alt=""><figcaption></figcaption></figure>

Compare executable on this list with [GTFOBins](https://gtfobins.github.io/) and clicking on the SUID button to filter binaries known to be exploitable when the SUID bit is set.

The SUID bit set for the nano text editor allows us to create, edit and read files using the file owner's privilege. Nano is owned by root, which probably means that we can read and edit files at a higher privilege level than our current user.

* Reading the `/etc/shadow` or adding a user to `/etc/passwd`
* We see that the nano text editor has the SUID bit set by running the `find / -type f -perm -04000 -ls 2>/dev/null` command.
* `nano /etc/shadow` will print the contents of the `/etc/shadow` file. We can now use the unshadow tool to create a file crack-able by John the Ripper. To achieve this, unshadow needs both the `/etc/shadow` and `/etc/passwd` files.
  * An alternative to using unshadTHM-3847834ow and cracking passwords, we can add a new user that has root privileges using the hash value of the password we want.

## Capabilities Escalation

Another method system administrators can use to increase the privilege level of a process or binary is "capabilities". Capabilities help manage privileges at a more granular level. The capabilities man page provides detailed information on its usage and options.

* Use the `getcap` tool to list enabled capabilities.
  * When run as an unprivileged user, `getcap -r /` will generate a huge amount of errors. It is good practice to redirect the error messages to /dev/null.
  * GTFOBins has a good list of binaries to be leveraged for privilege escalation if we find any set capabilities.

<figure><img src="https://i.imgur.com/Q6XYr0p.png" alt=""><figcaption><p>getcap -r / 2>/dev/null</p></figcaption></figure>

<figure><img src="https://i.imgur.com/6csoabB.png" alt=""><figcaption><p>vim</p></figcaption></figure>

Neither vim or its copy has the SUID bit set so this privilege escalation vector is not discoverable when enumerating files looking for SUID.

<figure><img src="https://i.imgur.com/nlpCMWj.png" alt=""><figcaption><p>command and payload</p></figcaption></figure>

## Automated Enumeration Tools

These automated tools should only be used to save time knowing they may miss some privilege escalation vectors.

The target system's environment will influence which tool will be used.

* [LinPeas](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS)
* [LinEnum](https://github.com/rebootuser/LinEnum)
* [LES (Linux Exploit Suggester)](https://github.com/mzet-/linux-exploit-suggester)
* [Linux Smart Enumeration](https://github.com/diego-treitos/linux-smart-enumeration)
* [Linux Priv Checker](https://github.com/linted/linuxprivchecker)

### Enumeration with LinEnum

LinEnum is a simple bash script that performs commands related to privilege escalation, saving time and allowing more effort to be put toward getting root.

* Download a local copy of LinEnum from: https://github.com/rebootuser/LinEnum/blob/master/LinEnum.sh

#### How to get LinEnum on Target Machine

There are two ways to get LinEnum on the target machine.

![server](https://github.com/TheRealPoloMints/Blog/blob/master/Security%20Challenge%20Walkthroughs/Common%20Linux%20Privesc/Resources/1.png?raw=true)

1. Go to the directory where the local copy of LinEnum is stored in and start a Python web server using `python3 -m http.server 8000`. Then use `wget` on the target machine, and local IP, to grab the file from the local machine.

![wget](https://github.com/TheRealPoloMints/Blog/blob/master/Security%20Challenge%20Walkthroughs/Common%20Linux%20Privesc/Resources/2.png?raw=true)

1. Make the file executable using the command `chmod +x FILENAME.sh`.

If unable to transport the file, and if have sufficient permissions, copy the raw LinEnum code from the local machine and paste it into a new file on the target, using Vi or Nano. Then save the file with the .sh extension.

* Finally make the file executable using the command `chmod +x FILENAME.sh` to have own executable copy of the LinEnum script on the target machine.

#### Running LinEnum

LinEnum can be run similar to any bash script.

* Go to the directory where LinEnum is located.
* Run the command `./LinEnum.sh`.

### Understanding LinEnum Output

The LinEnum output is broken down into different sections:

* **Kernel information** is shown here to show a likely kernel exploit available for the machine.
* **Can we read/write sensitive files**: Files that any authenticated user can read and write to. By looking at the permissions of these sensitive files, potentially find a misconfiguration that allows users who should not be able to, able to write to sensitive files.
* **SUID Files**: SUID (Set owner User ID up on execution) is a special type of file permissions given to a file. It allows the file to run with permissions of whoever the owner is. If this is root, it runs with root permissions and allow us to escalate privileges.
* **Crontab Contents**: The scheduled cron jobs are shown - used to schedule commands at a specific time.

#### Abusing SUID/GUID Files

The first step in Linux privilege escalation exploitation is to check for files with the SUID/GUID bit set.

* File or files can be run with the permissions of the file(s) owner/group.

**SUID Binary**

In Linux, everything is a file, including directories and devices which have permission to allow restrict three operations (read/write/execute).

Here is how maximum privileges (rwx-rwx-rwx) look:

* r = read
* w = write
* x = execute

| user | group | others |
| ---- | ----- | ------ |
| rwx  | rwx   | rwx    |
| 421  | 421   | 421    |

The maximum number of bit that can be used to set permission for each user is 7, which is a combination of read (4) write (2) and execute (1) operation. For example, if you set permissions using "chmod" as 755, then it will be: rwxr-xr-x.

* When a special permission is given to each user it becomes SUID or SGID. When extra bit '4' is set to user(Owner) it becomes SUID (Set User ID).
  * '2' is set to group it becomes SGID(Set Group ID)
* SUID: rws-rwx-rwx
* GUID: rwx-rws-rwx

**Finding SUID Binaries**

To find SUID capable files on the system: `find /-perm -u=s type f 2>/dev/null`

* `find` - Initiates the 'find' command
* `/` - Searches the whole file system
* `-perm` - Searches for files with specific permissions
* `-u=s` - Any of the permission bits mode are set for the file
* `-type f` - Only search for files
* `2>/dev/null` - Suppresses errors

## Exploiting Writeable /etc/passwd

Continue with enumeration, we discovered that user7 is a member of the root group with gid 0. From the LinEnum scan, we know the `/etc/passwd` file is writable for the user. We can conclude that user7 can edit the file.

### Understanding /etc/passwd

The `/etc/passwd` file stores essential information, which is required during login - storing user account information.

* File is a plain text file. It contains a list of the system's accounts, giving for each account useful information like user ID, group ID, home directory, shell and more.
* Write access must only limit for the superuser/root account.

### Understanding /etc/passwd Format

The file contains one entry per line for each user (user account) of the system. All fields are separated by a colon `:` symbol.

* test:x:0:0:root:/root:/bin/bash

1. **Username**: Used when user logs in. It should be between 1 and 32 characters in length.
2. **Password**: An x character indicates that encrypted password is stored in /etc/shadow file. You need to use the passwd command to compute the hash of a password typed at the CLI or to store/update the hash of the password in the file. In this case, the password hash is stored as an 'x'.
3. **User ID (UID)**: Each user must be assigned a user ID (UID).
   * UID 0 (zero) is reserved for root and UIDs 1-99 are reserved for other predefined accounts. UID 100-999 are reserved by system for administrative and system accounts/groups.
4. **Group ID (GID)**: The primary group ID (stored in /etc/group file)
5. **User ID Info**: The comment field allows to add extra information about the users such as user's full name, phone number, etc.
6. **Home directory**: The absolute path to the directory to the user will be in when they log in.
7. **Command/shell**: The absolute path of a command or shell (/bin/bash).

### How to Exploit a Writable /etc/passwd

If we have a writable /etc/passwd file, we can write a new line entry and create a new user.

* Add the password hash of our choice, set the UID, GID and shell to root and allowing us to log in as our own root user!

## Escaping

**Sudo -l**

* Every time have access to an account, always use `sudo -l` to list what commands are able to use as a super user account.

**Escaping Vi**

* Running this command as 'user8' account shows us that this user can run vi with root privileges. This will allow us to escape vim in order to escalate privileges and get a shell as the root user.

**Misconfigured Binaries and GTFOBins**

* A good place to look on how to exploit them is GTFOBins.
* GTFOBins is a curated list of Unix binaries that can be exploited by an attacker to bypass local security restrictions.
* https://gtfobins.github.io/

## Exploit Crontab

The Cron daemon is a long-running process that executes commands at specific dates and times.

* Use to schedule activities, either as one-time events or as recurring tasks.
* Can create a crontab file containing commands and instructions for the Cron daemon to execute.

### How to View Active Cronjobs

Use the command `cat /etc/crontab` to view what cron jobs are scheduled.

* Always check manually, especially if LinEnum, or a similar script, does not find anything.

### Format of a Cronjob

Cronjob exist in a certain format.

* '#' = ID
* m = Minute
* h = Hour
* dom = Day of the Month
* mon = Month
* dow = Day of the week
* user = What user the command will run as
* command = What command should be run

### Exploit

From the LinEnum scan, the file autoscript.sh, on user4's desktop is scheduled to run every five minutes.

* Owned by root, meaning it will run with root privileges.
  * The task then is to create a command that will return a shell and paste it in this file.

## Exploit PATH Variable

PATH is an environmental variable in Linux and Unix-like operating systems which specifies directories that hold executable programs.

* When the user runs any command in the terminal, it searches for executable files with the help of the PATH variable in response to commands.
* We can re-write the PATH variable to a location of our choosing.
  * SUID binary calls the system shell to run an executable.
