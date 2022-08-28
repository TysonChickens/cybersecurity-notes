---
id: op8gluer5gorswd1xkdwwis
title: Os Security
desc: ''
updated: 1653111526177
created: 1653098733559
---

# User and Kernel Mode

- [ ] Describe the Windows components User mode and Kernel mode and how they differ.

---

## Microsoft Windows

Windows OS, computer operating system (OS) developed by Microsoft Corporation to run personal computers (PCs).

- The first graphical user interface (GUI) for IBM-compatible PCs.
- Approximately 90% of PCs run some version of Windows.

### Windows Components

- User Mode and Kernel Mode
- Drivers call routine that are exported by various kernel components.
- Drivers must respond to specific calls from the operating system and can respond to other system calls.

![Components](https://docs.microsoft.com/en-us/windows-hardware/drivers/kernel/images/ntarch.png)

#### User Mode

When you start a user-mode application, Windows create a process for the application.

- Private virtual address space.
- Private handle table.
- Each application runs in isolation, and if an application crashes, the crash is limited to that one application.

### Kernel Mode

All code that runs in kernel mode shares a single virtual address space.

- If a kernel-mode driver accidentally writes to the wrong virtual address, data that belongs to the operating system or another driver could be compromised.
  - If a kernel-mode driver crashes, the entire operating system crashes.
