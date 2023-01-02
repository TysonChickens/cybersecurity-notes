# Firmware Reverse Engineering

## Objectives

* [ ] What is firmware reverse engineering?
* [ ] Techniques for extracting code from the firmware.
* [ ] Extracting hidden keys from an encrypted firmware.
* [ ] Modifying and rebuilding a firmware.

Every embedded system, such as cameras, routers, smart watches, etc. has pre-installed firmware, with its own set of instructions running on the hardware's processor. It allows the **hardware to communicate with other software running on the device**. The firmware provides low-level control for the developer to make changes at the root level.

Reverse engineering is the process of going back through the code to figure out how it was built and what it does. Firmware reverse engineering is extracting the original code from the firmware binary file and verifying the code does not carry out any malicious or unintended functionality.

* Firmware reversing is usually done for security reasons to ensure the safe usage of devices that may have critical vulnerabilities leading to possible exploitation or data leakage.

## Firmware Reversing Steps

* The firmware is first obtained from the vendor's website or extracted from the device to perform the analysis.
* The obtained/extracted firmware, usually a binary file, is first analyzed to figure out its type (bare metal or OS-based).
* Verified that the firmware is either encrypted or packed. The encrypted firmware is more challenging to analyze as it usually needs a workaround, such as reversing the previous non-encrypted released of the firmware or performing hardware attacks like [Side Channel Attacks (SCA)](https://en.wikipedia.org/wiki/Side-channel\_attack) to fetch the encryption keys.
* Once the encrypted firmware is decrypted, different techniques and tools are used to perform reverse engineering based on type.

## Types of Firmware Analysis

Firmware analysis is carried through Static or Dynamic techniques.

### Static Analysis

Static analysis involves essential examination of the binary file contents and reading the assembly instructions to understand the functionality. There are common used command line utilies and binary analysis tools:

* [BinWalk](https://github.com/ReFirmLabs/binwalk): A firmware extraction tool that extracts code snippets inside any binary by searching for signatures against many standard binary file formats like `zip, tar, exe, ELF,` etc.
  * Binwalk has a database of binary header signatures against which the signature match is performed. The common objective of using this tool is to extract a file system like `Squashfs, yaffs2, Cramfs, ext*fs, jffs2,` etc., which is embedded in the firmware binary.&#x20;
* [Firmware ModKit (FMK)](https://www.kali.org/tools/firmware-mod-kit/): FMK is widely used for firmware reverse engineering. It extracts the firmware using `binwalk` and outputs a directory with the firmware file system.&#x20;
  * Once the code is extracted, a developer can modify desired files and repack the binary file with a single command.&#x20;
* [FirmWalker](https://github.com/craigz28/firmwalker): Searches through the extracted firmware file system for unique strings and directories like `etc/shadow`, `etc/passwd`, `etc/ssl`, special keywords like `admin, root, password`, etc., vulnerable binaries like `ssh, telnet, netcat` etc.

### Dynamic Analysis

Firmware dynamic analysis involves running the firmware code on actual hardware and observing its behavior through emulation and hardware/software-based debugging. The following tools are commonly used for dynamic analysis:

* [Qemu](https://www.qemu.org/): Free and open-source emulator and enables working on cross-platform environments. The tool provides various ways to emulate binary firmware for different architectures like Advanced RISC Machines (ARM), Microprocessors without Interlocked Pipelined Stages (MIPS), etc., on the host system.
  * Qemu can help in full-system emulation or a single binary emulation of ELF (Executable and Linkable Format) files for the Linux system and many different platforms.
* [Gnu DeBugger (GDB)](https://www.sourceware.org/gdb/)[:](https://www.sourceware.org/gdb/) GDB is a dynamic debugging tool for emulating a binary and inspecting its memory and registers. GDB also supports remote debugging, commonly used during firmware reversing when the target binary runs on a separate host and reversing is carried out from a different host.

## Reverse the Firmware

Tools will be used:

* Binwalk: To verify encryption and can also be used to decrypt the firmware. (`binwalk -E -N`)
* Firmware Mod Kit (FMK): Library for firmware extraction and modification. (`extract-firmware.sh`)

### 1. Verify Encryption

Verify the binary is encrypted through [file entropy analysis](https://en.kali.tools/?p=1634) using Binwalk tool using the command:`binwalk -E -N FIRMWARE_NAME`

### 2. Finding Unencrypted Older Version

Find an older version of the same firmware to find encryption keys to decrypt the original firmware and reverse engineer it.

Extract the firmware using command:`extract-firmware.sh UNSIGNED_FIRMWARE_NAME`

### 3. Find Encryption Keys

The original firmware is gpg protected, which requires a public, and private key and a paraphrase to decrypt the original signed firmware. Use the `grep` command with the `-i` flag to ignore case sensitivity while the `-r` operator recursively searches the current directory and sub-directories.

### 4. Decrypt the Encrypted Firmware

With the keys, import them using the command: `gpg --import fmk/rootfs/gpg/private.key`

* List the secret keys: `gpg --list-secret-keys`
* Once the keys are imported, use the gpg command on the firmware to decrypt it.

### 5. Reverse the Original Encrypted Firmware

Use binwalk or FMK to extract code from the recently unencrypted firmware.

* `extract-firmware.sh ENCRYPTED_FIRMWARE_NAME`
