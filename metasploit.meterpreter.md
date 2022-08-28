---
id: 5jlm4r7fxj9qpp2xtelvktu
title: Meterpreter
desc: ''
updated: 1654824928287
created: 1654811064385
---

# Introduction to Meterpreter

Meterpreter is a Metasploit payload that supports the penetration testing process with many valuable components.

- Meterpreter will run on the target system and act as an agent within a command and control architecture.
- Interact with the target operating system and use Meterpreter's specialized commands.

- Meterpreter runs on the target system in memory (RAM - Random Access Memory) to avoid having a file that has to be written to the disk.
  - Meterpreter will be seen as a process and not have a file on the target system.
  - Aims to avoid being detected by network-based IPS (Intrusion Prevention System) and IDS (Intrusion Detection System) solutions by using encrypted communication with the server where Metasploit runs (typically attacking machine).
    - If the target organization does not decrypt and inspect encrypted traffic (e.g. HTTPS) coming to and going out of the local network, IPS and IDS solutions will not be able to detect its activities.
  - Recognized by major antivirus software and this provides some degree of stealth.

## Meterpreter Flavors

Staged payloads are sent to the target in two steps allowing for smaller initial payload size. The inline payloads are sent in a single step.

1. The stager
2. Requests the rest of the payload
Meterpreter payloads are divided into staged and inline versions.

- Meterpreter has a wide range of different versions to choose from based on the target system.

`msfvenom --list payloads | grep meterpreter` to view available Meterpreter versions.

The list will show Meterpreter versions available for the following platforms:

- Android
- Apple iOS
- Java
- Linux
- OSX
- PHP
- Python
- Windows

Choosing a version of Meterpreter to use will be based on three factors:

1. Target operating system (Linux, Mac, or Windows, etc.)
2. Components available on the target system (Is Python installed, PHP website?)
3. Network connection types on the target system (Do they allow TCP connections? HTTPS reverse connections? Are IPv6 addresses are not closely monitored as IPv4 addresses?)

Also list other available payloads using the `show payloads` command with any module.

## Meterpreter Commands

Meterpreter will provide with three primary categories of tools:

- Built-in commands
- Meterpreter tools
- Meterpreter scripting

Running the `help` will show Meterpreter commands for different categories:

- Core 
- File system
- Networking 
- System 
- User interface 
- Webcam 
- Audio output
- Elevate
- Password database
- Timestomp

### Core Commands

- `background`: Backgrounds the current session
- `exit`: Terminate the Meterpreter session
- `guid`: Get the session GUID (Globally Unique Identifier)
- `help`: Displays the help menu
- `info`: Displays information about a Post module
- `irb`: Opens an interactive Ruby shell on the current session
- `load`: Loads one or more Meterpreter extensions
- `migrate`: Allows to migrate Meterpreter to another process
- `run`: Executes a Meterpreter script or Post module
- `sessions`: Quickly switch to another session

### File System Commands

- `cd`: Change directory
- `ls`: List files in the current directory (dir will also work)
- `pwd`: Prints the current working directory
- `edit`: Allow to edit a file
- `cat`: Show contents of a file to the screen
- `rm`: Delete the specified file
- `search`: Search for files
- `upload`: Upload a file or directory
- `download`: Download a file or directory

### Networking Commands

- `arp`: Displays the host ARP (Address Resolution Protocol) cache
- `ifconfig`: Displays network interfaces available on the target system
- `netstat`: Displays the network connections
- `portfwd`: Forwards a local port to a remote service
- `route`: Allows to view and modify the routing table

### System Commands

- `clearev`: Clears the event logs
- `execute`: Executes a command
- `getpid`: Shows the current process identifier
- `getuid`: Shows the user that Meterpreter is running as
- `kill`: Terminates a process
- `pkill`: Terminates processes by name
- `ps`: List running processes
- `reboot`: Reboots the remote computer
- `shell`: Drops into a system command shell
- `shutdown`: Shuts down the remote computer
- `sysinfo`: Gets information about the remote system, such as OS

### Others Commands (listed under different categories)

- `idletime`: Returns the number of seconds the remote user has been idle
- `keyscan_dump`: Dumps the keystroke buffer
- `keyscan_start`: Starts capturing keystrokes
- `keyscan_stop`: Stops capturing keystrokes
- `screenshare`: Allows to watch the remote user's desktop in real time
- `screenshot`: Grabs a screenshot of the interactive desktop
- `record_mic`: Records audio from the default microphone for X seconds
- `webcam_chat`: Starts a video chat
- `webcam_list`: Lists webcams
- `webcam_snap`: Takes a snapshot from the specified webcam
- `webcam_stream`: Plays a video stream from the specified webcam
- `getsystem`: Attempts to elevate privilege to that of a local system
- `hashdump`: Dumps the contents of the SAM database

## Post-Exploitation with Meterpreter

Meterpreter provides many useful commands for the post-exploitation phase.

- `getuid` command will display the user which Meterpreter is currently running to give an idea of possible privilege level on the target system.
- `ps` command will list running processes. The PID column gives the PID information to migrate Meterpreter to another process.

### Migrate

Migrating to another process will help Meterpreter interact with it.

- If you see a word process running on the target (e.g. word.exe, notepad.exe, etc.), can migrate to to it and start capturing keystrokes sent by the user to this process.
  - Careful to lose user privileges from SYSTEM user to a process started by a lower privileged user.

### Hashdump

`hashdump` will list the content of the SAM database.

- The SAM (Security Account Manager) database stores user's passwords on Windows systems. These passwords are stored in the NTLM (New Technology LAN Manager) format.
  - While not mathematically possible to 'crack' these hashes, can still discover the cleartext password using online NTLM databases or a rainbow table attack.

### Search

`search` is useful to locate files with potential information.

### Shell

A regular command-line shell on the target system. Pressing CTRL+Z will return to the Meterpreter shell