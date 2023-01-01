# Memory Forensics

Analysis of the volatile memory in use when a computer is on.&#x20;

* Computers use dedicated storage called RAM (Random Access Memory) RAM is extremely quick and preferred method of storing and accessing data.&#x20;
* Data is volatile = Deleted when the computer is powered off.

Analyze a computer's memory to see what applications (processes), what network connections were being made, and many more pieces of information such as seeing what the malware was doing at the time.

### Why Memory Forensics is Useful

A memory dump is a full capture of what was happening on the computer at the time.

* Network connections running in the background.
* Malicious code attempt hidden from the user.

By analyzing memory, we can detect what the malware was doing, who it was contacting, and more.

### Introduction to Processes

Most simplest definition of a process is a running program. A process is created when running an instance of an application such as notepad. This will help determine what processes were running on the computer at the time of the capture.

* There can be multiple processes for an application.

On a computer, processes are usually categorized into two groups:

| Category           | Description                                                                                                          | Example                                                                                                                 |
| ------------------ | -------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| User Process       | These processes are programs the user has launched (text editors, web browsers, etc.)                                | notepad.exe - A text editor that is launched by the user.                                                               |
| Background Process | Processes are automatically launched and managed by the operating system and essential to the OS behaving correctly. | dwm.exe - An essential process for Windows that is responsible for displaying windows and applications on the computer. |

### Introduction to Volatility

Volatility is an open-source memory forensics toolkit written in Python.

* Allows to analyze memory dumps taken from Windows, Linux, and Mac OS devices and is an extremely popular tool in memory forensics.

Volatility allows us to:

* List all processes running on the device at the time of the capture.
* List active and closed network connections.
* Use Yara rules to search for indicators of malware.
* Retrieve hashed passwords, clipboard contents, and contents of the command prompt.

Volatility can be run using `python3 vol.py` if installed and its requirements.

| Option | Description                                                                                                                                 | Example                                                              |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| -f     | This argument is where you provide the name and location of the memory dump that you wish to analyse.                                       | `python3 vol.py -f /path/to/my/memorydump.vmem`                      |
| -v     | This argument increases the verbosity of Volatility. This is sometimes useful to understand what Volatility is doing in cases of debugging. | <p><code>python3 vol.py -v</code> <br></p>                           |
| -p     | This argument allows you to override the default location of where plugins are stored.                                                      | <p><code>python3 vol.py -p /path/to/my/custom/plugins</code><br></p> |
| -o     | This argument allows you to specify where extracted processes or DLLs are stored.                                                           | `python3 vol.py -o /output/extracted/files/here`                     |

Volatility uses plugins to perform analysis. More documentation [here](https://volatility3.readthedocs.io/en/latest/volatility3.plugins.html).
