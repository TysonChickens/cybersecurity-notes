---
id: ptonz0zapnutyahjkedfn8f
title: Scripting
desc: ''
updated: 1653180226185
created: 1653180215973
---

# Scripting Overview

- [ ] Learn about the history of scripting languages.
- [ ] Learn about the common uses of scripting today.

- [ ] Learn about the different concepts related to scripting languages.

- [ ] Learn about the different scripting languages.

---

IBM's Job Control Language (JCL) is often cited as one of the first scripting languages. But while scripting languages were functional, their response time wasn't nearly as fast as modern computers - often took at least a day to get results!

## History of Scripting

- The first interactive shells were developed in the 1960s to enable remote operation of the first time-sharing systems. These used shell scripts, which controlled running computer programs within a computer program, the shell.
- Calvin Mooers in his TRAC language is generally credited with inventing command substitution, the ability to embed commands in scripts that when interpreted insert a character string into the script.
- One innovation in the Unix shells was the ability to send the output of one program into the input of another, making it possible to do complex tasks in one line of shell code.

## Script Usage

Scripts have multiple uses, but automation is the name of the game.

- Image rollovers
- Validation
- Backup
- Testing

## Concepts

### Scripts

- Small interpreted programs.
- Script can use functions, procedures, external calls, variables, etc.

### Variables

- Most scripts need to calculate a result or execute a series of instructions and a great way to do so is storing any information we need a variable.
- A variable is a memory address paired with a symbolic name (identifier) which contain a value.
  - Can be used to reference, manipulate, replace or delete, the value.
- Memory space needed for a variable may be allocated only when the variable is first used and freed when it is no longer needed.

### Arguments /  Parameters

- Parameters are pre-established variables which will be used to perform the related process of our function.
- Parameters appear in procedure definitions; arguments appear in procedure calls.
  - In the function definition `f(x) = x*x`, the variable x is a parameter.
  - In the function call f(2), the value 2 is the argument of the function.
- Although parameters are also commonly referred to as arguments, arguments are sometimes thought of as the actual values or references assigned to the parameter variables when the subroutine is called at run-time.

### If Statement

- The if-then construct (sometimes called if-then-else) is common across many programming languages. Although the syntax varies from language to language, the basic structure looks like this:
  - If (boolean condition) Then (consequent) Else (alternative) End If.

### Loops

- For Loop
- While Loop
- Until Loop

## Scripting Languages

### JavaScript

JavaScript
: An object oriented scripting language developed in 1995 by Netscape Communications.

- Although it can be used server or client sided, its most popular use by is its client side.
- A multi-paradigm language, JavaScript supports event-driven, functional, and imperative (including object-oriented and prototype-based) programming styles. It has APIs for working with text, arrays, dates, regular expressions, and the DOM, but the language itself does not include any I/O, such as networking, storage, or graphics facilities. It relies upon the host environment in which it is embedded to provide these features.

Variables in JavaScript can be defined using either the var, let or const keywords.

- `let x` // declares the variable x and assigns to it the special value "undefined".
- `let y = 2;` // declares the variable y and assigns to it the value 2.
- `let z = "Hello, World!";` // declares the variable z and assigns to it a string containing "Hello, World!".

### Bash

Bash
: GNU Bash or simply bash is Unix shell and command language written by Brian Fox for GNU Project as a free software replacement for the Bourne shell. First released in 1989, it has been used widely as the default login shell for most Linux distributions and Apple's macOS Mojave and earlier versions.

- Bash is a command processor that typically runs in a text window where the user types commands that cause actions. Bash can also read and execute commands from a file, called a shell script.
- Supports filename globbing (wildcard matching), piping, here documents, command substitution, variables, and control structures for condition-testing and iteration.
- Bash is a POSIX-compliant shell, but with a number of extensions.

Here is an example:

``` bash
#!/bin/bash
myvariable=Hello
anothervar=Fred
echo $myvariable $anothervar
echo
sampledir=/etc
ls $sampledir
```

### Perl

Perl
: Larry Wall began work on Perl in 1987, while working as a programmer at Unisys, and released version 1.0 to the comp.sources.misc newsgroup on December 18, 1987.

- Perl 2, released in 1988, featured a better regular expression engine.
- Perl 3, released in 1989, added support for binary data streams.

Originally, the only documentation for Perl was a single lengthy man page. In 1991, Programming Perl, known to many Perl programmers as the "Camel Book" because of its cover, was published and became the reference for the language.

Perl variables do not have to be explicitly declared to reserve memory space. The declaration happens automatically when you assign a value to a variable. The equal sign (=) is used to assign values to a variables.

- `$age = 25; # An integer assignment`
- `$name = "John Paul"; # A string`
- `$salary = 1445.50; # A floating point`

### PowerShell

PowerShell
: A task automation and configuration management from Microsoft, consisting of command-line shell and associated scripting language. Initially, a Windows component only, known as Windows PowerShell, it was made open-source and cross-platform on 18 August 2016 with the introduction of PowerShell Core. The former is built on .NET Framework while the latter on .NET Core.

- Administrative tasks are generally performed by cmdlets (pronounced command-lets), which are specialized .NET classes implementing a particular operation. These work by accessing data in different data stores, like the file system or registry, which are made available to PowerShell via providers. Third-party developers can add cmdlets and providers to PowerShell. Cmdlets may be used by scripts and scripts may be packaged into modules.

### Binary

Binary
: Code represents text, computer processor instructions, or any other data using a two-symbol system. Often "0" and "1" from the binary number system. The binary code assigns a pattern of binary digits, also known as bits, to each character, instruction, etc. A binary string of eight bights can represent any of 256 possible values and can, therefore, represent a wide variety of different items.

- In computing and telecommunications, binary codes are used for various methods of encoding data, such as character strings, into bit strings. Those methods may use fixed-width strings. In fixed-width binary code, each letter, digit, or other character is represented by a bit string of the same length; that big string, interpreted as a binary number, is usually displayed in code tables in octal, decimal or hexadecimal notation.

### Hex

Hex
: Advanced hex editors have scripting systems that let the user create macro like functionality as a sequence of user interface commands for automating common tasks.

- Can be used for providing scripts that automatically patch files (e.g., game cheating, modding, or product fixes provided by community) or to write more complex/intelligent templates.
- Scripting languages vary widely, often being product specific languages resembling MS-DOS batch files, to systems that support fully-fledged scripting languages such as Lua or Python.