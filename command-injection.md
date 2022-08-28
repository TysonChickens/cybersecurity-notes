---
id: pn4fankyf3uifous1txqj5m
title: Command Injection
desc: ''
updated: 1657401645152
created: 1657335380410
---

# What is Command Injection?

- How to discover the command injection vulnerability.
- How to test and exploit this vulnerability using payloads designed for different operating systems.
- How to prevent this vulnerability in an application.

Command injection the abuse of an application's behavior to execute commands on the operating system, using the same privileges that the application on a device is running with. If a web server running as a user named _joe_, it will execute commands under the user and any permissions the account has.

- Command injection vulnerability is also known as "Remote Code Execution" (RCE) because an attacker can trick the application into executing a series of payloads without direct access to the machine.
- Command injection was one of the top ten vulnerabilities reported by Contrast Security's AppSec intelligence report in 2019 and OWASP framework of a web application.

## Discovering Command Injection

This vulnerability exists because applications often use functions in programming languages such as PHP, Python, and NodeJS to pass data to an to make system calls on the machine's operating system. For example, taking input from a field and searching for an entry into a file.

![php-injection](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/a54a09f7c4efa1d340ab678ece230c44.png)

1. The application stores MP3 files in a directory contained on the operating system.
2. The user inputs the song title to search for. The application stores this input into the `$title` variable.
3. The data `$title` variable is passed to the command `grep` to search for a text file named _songtitle.txt_ for the entry the user searched for.
4. The output of this search of _songtitle.txt_ will determine whether the application informs the user that the song exists or not.

An attacker could abuse the application by injecting their own commands for the application to execute.

- Rather than use `grep` to search for an entry in `songtitle.txt`, they could ask the application to read data from a more sensitive file.

Abusing applications can be possible no matter the programming language the application uses.

![python-injection](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/04a1cb87fad0a9b47761afddc48e0bf2.png)

1. The 'flask' package is used to set up a web server.
2. A function that uses the 'subprocess' package to execute a command on the device.
3. Use a route in the webserver that will execute whatever is provided.

## Exploiting Command Injection

Applications that use user input to populate system commands with data can often be combined in unintended behavior. For example, the shell operators `;`, `&`, and `&&` will combine two (or more) system commands and execute them both.

Command injection can be detected in two ways:

1. **Blind command injection**: There is no direct output from the application when testing payloads. You will have to investigate the behaviors of the application to determine whether or not the payload was successful.
2. **Verbose command injection**: There is direct feedback from the application once you have tested a payload. For example, running the `whoami` command to see what user the application is running under. The web application will output the username on the page directly.

### Detecting Blind Command Injection

There is no output visible, so it is not immediately noticeable when command command injection occurs. A command is executed, but the web application outputs no message.

Must use payloads that will cause some time delay. For example, the `ping` and `sleep` commands are significant payloads to test with.

- Using `ping`, the application will hang for x amount of seconds in relation to how many pings specified.
- Another method to detect blind command injection is by forcing output using redirection operators such as `>`.
  - The web application will execute commands such as `whoami` and redirect to a file and use `cat` to read newly created file content.
- The `curl` command is great to test for command injection. `curl` is used to deliver data to and from an application in your payload.
  - `curl http://vulnerable.app/process.php%3Fsearch%3DThe%20Beatles%3B%20whoami`

### Detecting Verbose Command Injection

Detecting command injection is the easiest method because the application gives you feedback or output to what is happening or being executed.

- The output of commands such as `ping` or `whoami` is directly displayed on the web application.

### Useful Payloads - Linux & Windows

#### Linux Payloads


| Payload | Description                                                                              |
| ------- | ---------------------------------------------------------------------------------------- |
| whoami  | See what user the application is running under.                                          |
| ls      | List the contents of the current directory.                                              |
| ping    | Invoke the application to hang. Useful for testing blind command injection.              |
| sleep   | Useful for blind command injection where the machine does not have `ping` installed.     |
| nc      | Netcat can be used to spawn a reverse shell onto the vulnerable application and escalate |

#### Windows Payloads

| Payload | Description                                                                                          |
| ------- | ---------------------------------------------------------------------------------------------------- |
| whoami  | See what user the application is running under.                                                      |
| dir     | List the contents of the current directory.                                                          |
| ping    | Invoke the application to hang. Useful for testing blind command injection.                          |
| timeout | Invoke the application to hang for blind testing blind command injection if `ping` is not installed. |

## Remediating Command Injection

Command injection can be prevented in a variety of ways. Everything from minimal use of potentially dangerous functions or libraries in a programming language to filtering input without relying on user's input.

### Vulnerable Functions

Below are examples of PHP language, however, the same principles can be extended to many other languages. In PHP, many functions interact with the operating system to execute commands via shell:

- Exec
- Passthru
- System

![PHP-function](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/14acf436361fcfb7efced4b2f416b3d5.png)

1. The application will only accept a specific pattern of characters (the digits 0-9).
2. The application will then only proceed to execute this data which is all numerical.

These functions take input such as string or user data and will execute whatever is provided on the system. Any application that uses these functions without proper checks will be vulnerable to command injection.

### Input Sanitization

Sanitizing any input from a user that an application uses is a great way to prevent command injection. This is a process of specifying the formats or types of data that a user can submit from numerical data or removing any special characters.

![PHP-sanitization](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/06e83dfe3791664ed0bb9bc9ffd3e581.png)

The `filter_input` PHP function is used to check whether or no any data submitted via an input form is a number. If it is not a number, it must be a invalid input.

### Bypassing Filters

Applications will employ numerous techniques in filtering and sanitizing data from a user's input. We can abuse the logic behind an application to bypass these filters.

- An application may strip out quotation marks - Instead, use the hexadecimal value of this to achieve the same result.