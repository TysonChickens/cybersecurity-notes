---
id: y56v7cc2bqtallfb8ofxl8k
title: Privilege Escalation
desc: ''
updated: 1655962312019
created: 1655517261836
---

# What is Privilege Escalation?

Involves moving from a lower permission to a higher permission level. Technically, it is the exploitation of vulnerability, design flaw or configuration oversight in an operating system or application to gain unauthorized access to resources that are usually restricted from the users.

Rarely during CTF or real-world penetration test, will be able to gain initial access that affords administrator access. Privilege escalation allows to gain system administrator levels of access to:

- Reset passwords
- Bypass access controls to compromise protected data
- Edit software configurations
- Enable persistence to gain access to the machine later
- Change privilege of users
- And other administrator or super user commands...

## Direction of Privilege Escalation

![privilege tree](https://github.com/TheRealPoloMints/Blog/blob/master/Security%20Challenge%20Walkthroughs/Common%20Linux%20Privesc/Resources/tree.png?raw=true)

There are two main privilege escalation variants:

### Horizontal Privilege Escalation

- Expand reach over the compromised system by taking over a different user who is on the same privilege level.
  - Hijack a normal user to inherit files and access the user has.
  - Can be used to access another normal privilege user that haves their SUID file attached to their home directory which can then be used to get super user access (travel sideways on the tree).

### Vertical Privilege Escalation

- Attempt to gain higher privileges or access, with an existing account that is already compromised.
- For local privilege escalation attacks, this might mean hijacking an account with administrator privileges or root privileges (travel up on the tree).

## Enumeration with LinEnum

LinEnum is a simple bash script that performs commands related to privilege escalation, saving time and allowing more effort to be put toward getting root.

- Download a local copy of LinEnum from: https://github.com/rebootuser/LinEnum/blob/master/LinEnum.sh

### How to get LinEnum on Target Machine

There are two ways to get LinEnum on the target machine.

![server](https://github.com/TheRealPoloMints/Blog/blob/master/Security%20Challenge%20Walkthroughs/Common%20Linux%20Privesc/Resources/1.png?raw=true)

1. Go to the directory where the local copy of LinEnum is stored in and start a Python web server using `python3 -m http.server 8000`. Then use `wget` on the target machine, and local IP, to grab the file from the local machine.

![wget](https://github.com/TheRealPoloMints/Blog/blob/master/Security%20Challenge%20Walkthroughs/Common%20Linux%20Privesc/Resources/2.png?raw=true)

2. Make the file executable using the command `chmod +x FILENAME.sh`.

If unable to transport the file, and if have sufficient permissions, copy the raw LinEnum code from the local machine and paste it into a new file on the target, using Vi or Nano. Then save the file with the .sh extension.

- Finally make the file executable using the command `chmod +x FILENAME.sh` to have own executable copy of the LinEnum script on the target machine.

### Running LinEnum

LinEnum can be run similar to any bash script.

- Go to the directory where LinEnum is located.
- Run the command `./LinEnum.sh`.

### Understanding LinEnum Output

The LinEnum output is broken down into different sections:

- **Kernel information** is shown here to show a likely kernel exploit available for the machine.
- **Can we read/write sensitive files**: Files that any authenticated user can read and write to. By looking at the permissions of these sensitive files, potentially find a misconfiguration that allows users who should not be able to, able to write to sensitive files.
- **SUID Files**: SUID (Set owner User ID up on execution) is a special type of file permissions given to a file. It allows the file to run with permissions of whoever the owner is. If this is root, it runs with root permissions and allow us to escalate privileges.
- **Crontab Contents**: The scheduled cron jobs are shown - used to schedule commands at a specific time.

#### Abusing SUID/GUID Files

The first step in Linux privilege escalation exploitation is to check for files with the SUID/GUID bit set.

- File or files can be run with the permissions of the file(s) owner/group.

##### SUID Binary

In Linux, everything is a file, including directories and devices which have permission to allow restrict three operations (read/write/execute).

Here is how maximum privileges (rwx-rwx-rwx) look:

- r = read
- w = write
- x = execute

| user | group | others |
| ---- | ----- | ------ |
| rwx  | rwx   | rwx    |
| 421  | 421   | 421    |

The maximum number of bit that can be used to set permission for each user is 7, which is a combination of read (4) write (2) and execute (1) operation. For example, if you set permissions using "chmod" as 755, then it will be: rwxr-xr-x.

- When a special permission is given to each user it becomes SUID or SGID. When extra bit '4' is set to user(Owner) it becomes SUID (Set User ID).
  - '2' is set to group it becomes SGID(Set Group ID)
- SUID: rws-rwx-rwx
- GUID: rwx-rws-rwx

###### Finding SUID Binaries

To find SUID capable files on the system: `find /-perm -u=s type f 2>/dev/null`

- `find` - Initiates the 'find' command
- `/` - Searches the whole file system
- `-perm` - Searches for files with specific permissions
- `-u=s` - Any of the permission bits mode are set for the file
- `-type f` - Only search for files
- `2>/dev/null` - Suppresses errors

## Exploiting Writeable /etc/passwd

Continue with enumeration, we discovered that user7 is a member of the root group with gid 0. From the LinEnum scan, we know the `/etc/passwd` file is writable for the user. We can conclude that user7 can edit the file.

### Understanding /etc/passwd

The `/etc/passwd` file stores essential information, which is required during login - storing user account information.

- File is a plain text file. It contains a list of the system's accounts, giving for each account useful information like user ID, group ID, home directory, shell and more.
- Write access must only limit for the superuser/root account.

### Understanding /etc/passwd Format

The file contains one entry per line for each user (user account) of the system. All fields are separated by a colon `:` symbol.

- test:x:0:0:root:/root:/bin/bash

1. **Username**: Used when user logs in. It should be between 1 and 32 characters in length.
2. **Password**: An x character indicates that encrypted password is stored in /etc/shadow file. You need to use the passwd command to compute the hash of a password typed at the CLI or to store/update the hash of the password in the file. In this case, the password hash is stored as an 'x'.
3. **User ID (UID)**: Each user must be assigned a user ID (UID).
   - UID 0 (zero) is reserved for root and UIDs 1-99 are reserved for other predefined accounts. UID 100-999 are reserved by system for administrative and system accounts/groups.
4. **Group ID (GID)**: The primary group ID (stored in /etc/group file)
5. **User ID Info**: The comment field allows to add extra information about the users such as user's full name, phone number, etc.
6. **Home directory**: The absolute path to the directory to the user will be in when they log in.
7. **Command/shell**: The absolute path of a command or shell (/bin/bash).

### How to Exploit a Writable /etc/passwd

If we have a writable /etc/passwd file, we can write a new line entry and create a new user.

- Add the password hash of our choice, set the UID, GID and shell to root and allowing us to log in as our own root user!

## Escaping

**Sudo -l**

- Every time have access to an account, always use `sudo -l` to list what commands are able to use as a super user account.

**Escaping Vi**

- Running this command as 'user8' account shows us that this user can run vi with root privileges. This will allow us to escape vim in order to escalate privileges and get a shell as the root user.

**Misconfigured Binaries and GTFOBins**

- A good place to look on how to exploit them is GTFOBins.
- GTFOBins is a curated list of Unix binaries that can be exploited by an attacker to bypass local security restrictions.
- https://gtfobins.github.io/

## Exploit Crontab

The Cron daemon is a long-running process that executes commands at specific dates and times.

- Use to schedule activities, either as one-time events or as recurring tasks.
- Can create a crontab file containing commands and instructions for the Cron daemon to execute.

### How to View Active Cronjobs

Use the command `cat /etc/crontab` to view what cron jobs are scheduled.

- Always check manually, especially if LinEnum, or a similar script, does not find anything.

### Format of a Cronjob

Cronjob exist in a certain format.

- '#' = ID
- m = Minute
- h = Hour
- dom = Day of the Month
- mon = Month
- dow = Day of the week
- user = What user the command will run as
- command = What command should be run

### Exploit

From the LinEnum scan, the file autoscript.sh, on user4's desktop is scheduled to run every five minutes.

- Owned by root, meaning it will run with root privileges.
  - The task then is to create a command that will return a shell and paste it in this file.

## Exploit PATH Variable

PATH is an environmental variable in Linux and Unix-like operating systems which specifies directories that hold executable programs.

- When the user runs any command in the terminal, it searches for executable files with the help of the PATH variable in response to commands.
- We can re-write the PATH variable to a location of our choosing.
  - SUID binary calls the system shell to run an executable.