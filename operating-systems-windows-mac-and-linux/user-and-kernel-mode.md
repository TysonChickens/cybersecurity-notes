# User and Kernel Mode

* [ ] Describe the Windows components User mode and Kernel mode and how they differ.

## Microsoft Windows

Windows OS, computer operating system (OS) developed by Microsoft Corporation to run personal computers (PCs).

* The first graphical user interface (GUI) for IBM-compatible PCs.
* Approximately 90% of PCs run some version of Windows.

### Windows Components

* User Mode and Kernel Mode
* Drivers call routine that are exported by various kernel components.
* Drivers must respond to specific calls from the operating system and can respond to other system calls.

![Components](https://docs.microsoft.com/en-us/windows-hardware/drivers/kernel/images/ntarch.png)

#### User Mode

When you start a user-mode application, Windows create a process for the application.

* Private virtual address space.
* Private handle table.
* Each application runs in isolation, and if an application crashes, the crash is limited to that one application.

### Kernel Mode

All code that runs in kernel mode shares a single virtual address space.

* If a kernel-mode driver accidentally writes to the wrong virtual address, data that belongs to the operating system or another driver could be compromised.
  * If a kernel-mode driver crashes, the entire operating system crashes.

## Linux Components

* [ ] Describe what makes Linux unique as an operating system.

Linux is an open source operating system, with a license under the General Public License (GNU)

* Guarantees end users the freedom to run, study, share and modify the software.

Linux has two major components:

### Kernel

* Core of the OS and interacts directly with the hardware.
* Manages system and user input/output. Processes, files, memory and devices.

### Shell

* Interface design for the user to interact directly with the kernel.
* Users input command through the shell and the kernel performs the commands.
