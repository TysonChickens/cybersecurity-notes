---
id: n5z3lhz8zrjnlc2acd66bmb
title: Commands
desc: ''
updated: 1653129928181
created: 1653129908123
---

# Linux Basic Commands

What do these useful Linux commands do:

- [ ] cd
- [ ] cp
- [ ] mv
- [ ] ls
- [ ] df
- [ ] kill
- [ ] rm
- [ ] rmdir
- [ ] cat
- [ ] mkdir
- [ ] ifconfig
- [ ] locate
- [ ] tail
- [ ] less
- [ ] more
- [ ] nano
- [ ] chmod

- [ ] Describe the basic Linux file and directory permission structure.

---

## Basic Commands

### cd

Changes the directory where the user is currently located.

### cp

Copies files or directories.

### mv

Moves files or directories

### ls

Lists information related to files and directories, like owner and privileges.

### df

Displays file system disk space.

### kill

Used to "kill" or stop an executing process.

### rm

Deletes file and directories.

### rmdir

Deletes an empty directory.

### cat

Short for concatenate. It can combine several files into one. Also used to see content of a file.

### mkdir

Creates a new directory.

### ifconfig

Used to view or configure network interfaces.

### locate

Quickly searches for the locations of files. It uses an internal database that is updated using the updatedb command.

### tail

Views the end of a text file, by default the last 10 lines.

### less

Efficient while viewing huge log files as it does not need to load the full file while opening.

### more

Displays text, one screen at a time.

### nano

A basic text editor.

### chmod

Changes privileges for a file or directory.

---

## Permissions and Owners

![Permissions](http://linux-blog.org/wp-content/uploads/2009/09/permissions.png)

- There are three groups that can "own" a file.
  - User, group, everybody.
- For each group, there are also three types of permissions: Read, Write, Execute.
- Read: 4 (100), Write: 2 (010), Execute: 1 (001).

### Permissions Visualized

![Permissions](https://miro.medium.com/max/2112/0*TJYlcsbddAMcxEOt)

### Change Permission

Use the `chmod` command to change the permissions of a file or directory.

- `chmod <permissions><filename>`
- `chmod 755 <filename>`
- `chmod u=rw,g=r,o=r <filename>`

Change owner and group owner of a file with the `chown` command.

- `chown <user>:<group> <filename>`
