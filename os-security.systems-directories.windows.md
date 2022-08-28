---
id: 2lhz6tfxy0roh9bey7pg0i8
title: Windows
desc: ''
updated: 1653111555491
created: 1653111538198
---

# File Systems and Directory Structure

- [ ] Describe the NTFS and FAT file systems used by Windows.

- [ ] Describe the Windows directory structure and how Windows handles the separation of 32-bit and 64-bit applications.

---

## File Systems

A file system enables applications to store and retrieve files on storage devices, such as a hard drive (HDD).

- Files are placed in a hierarchical structure. The file system specifies naming conventions for files and the format for specifying the path to a file in the tree structure.
  - A *file* is a unit of data in the file system that a user can access and manage. A file must have a unique name in its directory.
  - A *directory* is a hierarchical collection of directories and files.

### Types of File Systems

#### NTFS (New Technology File System)

- Introduced in 1993.
- Most common file system for Windows end user systems.
- Most Windows server use NTFS as well.

#### FATxx (File Allocation Table)

- Simple file system used since the 80s.
- Numbers proceeding FAT refer to the number of bits used to enumerate a file system block.
  - FAT16
  - FAT32
- Now mainly used for removable storage devices under 32GB capacity.

---

## Directory Structure

### Windows Directory Structure

In DOS, Windows, and OS/2, the root directory is *drive:/*.

- Usually the root directory is usually `C:\`.
- Physical and virtual drives are named by a drive letter.

| Folder                      | Description                                                                                                                                                                           |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \PerfLogs                   | May hold Windows performance logs, but on a default configuration, it is empty.                                                                                                       |
| \Program Files              | **32-bit architecture**: All programs (both 16-bit and 32-bit) are installed in this folder.                                                                                          |
|                             | **64-bit architecture**: 64-bit programs are installed in this folder.                                                                                                                |
| \Program Files(x86)         | Appears on 64-bit editions of Windows. 32-bit and 160bit programs are default installed here                                                                                          |
| \ProgramData (Hidden)       | Contains program data that is expected to be accessed by computer programs regardless of the user account.                                                                            |
| \Users                      | User profile folders containing one subfolder for each user that has logged onto the system at least once.                                                                            |
| \Public                     | This folder serves as a buffer for users of a computer to share files. By default this folder is accessible to all users that can log on to the computer and shared over the network. |
| (username)\AppData (hidden) | Folder stores per-user application data and settings.                                                                                                                                 |
| \Windows                    | Windows itself is installed into this folder                                                                                                                                          |
| \System, System32, SysWOW64 | Store dynamic-link library (DLL) files that implement the core features of Windows and Windows API.                                                                                   |
| \WinSxS                     | Called "Windows Component store" and constitutes the majority of Windows. A copy of Windows components, updates, and service packs.                                                   |

<https://en.wikipedia.org/wiki/Directory_structure>
