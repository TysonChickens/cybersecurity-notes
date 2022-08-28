---
id: 4y5a7pfy3t0luytuqebdydo
title: Linux
desc: ''
updated: 1653113213020
created: 1653113106430
---

# Linux File Systems

- [ ] Describe the Linux File System

---

## Files and Directories

- A file is the basic unit of storage for data. Usually stored on physical media such as hard drives. Represented by `-` in the Command-line Interface (CLI).
- A directory is a special type of file. Linux uses directories to hold information about other files. The equivalent of folders in Windows. Represented by a letter `d` in the CLI.

## Directory Structure

![Linux Directory](https://media.geeksforgeeks.org/wp-content/uploads/linuxDir.jpg)

### Root

- Every single file and directory starts from the root directory.
- Only the root user has write privileges under this directory.
- /root is not the same as /./root which is the home directory of root.

### /bin

- Contains binary executables.
- Common Linux commands are found here.
- Ps, ls, ping, grep, cp, mv, etc.

### /sbin

- Contains binary executables, but are more related to system maintenance.
- Iptables, reboot, fdisk, ifconfig, etc.

### /etc

- Contains configurations files required by all programs.
- Most applications will have a directory under /etc with all its configurations.

### /var

- Contains files that are expected to grow or change constantly.
- Referred to as variable files.
- Application logs are usually found in /var/log.

### /tmp

- Contains temporary files.
- They are deleted when system reboots.

### /home

- Where the home directories for all the users are located.
- Personal files can be stored here.

### /boot

- Contains boot loaded files.
- Used at boot time.

## Run Levels

![Levels](http://4.bp.blogspot.com/-3PtmjG_fLLo/UY5rpk0igII/AAAAAAAAAP4/tdPkyXIUXwg/s1600/run_levels.png)

