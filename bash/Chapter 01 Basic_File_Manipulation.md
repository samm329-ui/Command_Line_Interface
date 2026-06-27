# Chapter 1: Basic File Manipulation

## Introduction

Before learning Bash commands, it's important to understand the environment in which they run. Every command entered into a terminal is processed by a **shell**, which acts as the interface between the user and the operating system.

This chapter introduces the shell, explains the REPL model, and covers the fundamental Bash commands used for navigating directories and performing basic file operations.

---

## What is a Shell?

A **shell** is a **command-line interpreter** that allows users to communicate with the operating system by executing commands.

Whenever you enter a command, the shell is responsible for:

* Reading the command.
* Interpreting and evaluating it.
* Executing the requested operation.
* Displaying the output or an error message.
* Waiting for the next command.

When a terminal is opened, the shell starts in a **working directory** (also called the **current working directory**). Unless another path is specified, all commands are executed relative to this directory.

> **Note**
>
> A **terminal** is the application where you type commands, whereas a **shell** is the program that interprets and executes those commands. Although the terms are commonly used together, they refer to different components.

---

## Common Shells

This repository focuses on **Bash**, but several command-line shells are available across different operating systems.

### Bash (Bourne Again SHell)

* The most widely used Unix shell.
* Default shell on many Linux distributions.
* Available on macOS and Windows (through WSL or Git Bash).
* Primarily used for scripting, development, and system administration.

### Zsh (Z Shell)

* An extended version of Bash.
* Offers advanced auto-completion and customization.
* Default shell on modern versions of macOS.

### Fish (Friendly Interactive Shell)

* Designed for simplicity and ease of use.
* Provides syntax highlighting and intelligent command suggestions.
* Popular among users who prefer an interactive shell experience.

### PowerShell

* Developed by Microsoft.
* Available on Windows, Linux, and macOS.
* Uses objects instead of plain text as command output.
* Commonly used for Windows automation and administration.

### Command Prompt (CMD)

* The traditional Windows command-line interpreter.
* Supports basic file and directory operations.
* Less feature-rich than PowerShell or Bash.

> **Note**
>
> Many Unix-like shells share common commands, but certain features and syntax may differ depending on the shell.

---

## The REPL Model

Most command-line shells follow the **REPL** model.

**REPL** stands for:

* **R** — Read
* **E** — Evaluate
* **P** — Print
* **L** — Loop

The shell repeatedly performs the following steps:

1. Reads the command entered by the user.
2. Evaluates and executes the command.
3. Prints the output or an error message.
4. Loops back to wait for the next command.

This cycle continues until the shell is closed.

---

## `pwd`

Prints the absolute path of the current working directory.

### Syntax

```bash
pwd
```

### Example

```bash
$ pwd
/home/john/Documents
```

### Explanation

Use `pwd` whenever you want to know your current location in the filesystem. It returns the complete path of the directory you are currently working in.

---

## `ls`

Lists the files and directories in the current working directory.

### Syntax

```bash
ls
```

### Example

```bash
$ ls
Documents  Downloads  notes.txt
```

### Explanation

The `ls` command displays all visible files and directories in the current location. It is one of the most frequently used Bash commands for exploring the filesystem.

> **Tip**
>
> Run `ls` before performing file operations to verify that the required file or directory exists.

---

## `touch`

Creates a new empty file.

If the file already exists, the command updates its timestamp instead of creating a duplicate.

### Syntax

```bash
touch <filename>
```

### Example

```bash
touch notes.txt
```

### Explanation

The command creates an empty file named `notes.txt` in the current directory. It is commonly used before adding content with a text editor.

---

## `rm`

Permanently removes a file from the filesystem.

### Syntax

```bash
rm <filename>
```

### Example

```bash
rm notes.txt
```

### Explanation

The `rm` command deletes the specified file immediately.

> **Warning**
>
> Files deleted using `rm` are generally **not** moved to the Recycle Bin or Trash. Always verify the filename before executing this command.

---

## `clear`

Clears the terminal screen.

### Syntax

```bash
clear
```

### Example

```bash
clear
```

### Explanation

The `clear` command removes previous output from the terminal window, providing a clean workspace. It does not delete command history or stop running programs.

---

## `cd`

Changes the current working directory.

### Syntax

```bash
cd <directory>
```

### Example

```bash
cd Documents
```

### Explanation

If the specified directory exists, the shell changes the current working directory to that location. All subsequent commands will be executed relative to the new directory.

> **Tip**
>
> Use `pwd` after `cd` if you want to confirm your current location.

---

## `mv`

Moves files or directories from one location to another.

The same command can also be used to rename files and directories.

### Syntax

```bash
mv <source> <destination>
```

### Example 1 — Rename a File

```bash
mv notes.txt lecture-notes.txt
```

The file `notes.txt` is renamed to `lecture-notes.txt`.

### Example 2 — Move a File

```bash
mv notes.txt Documents/
```

The file `notes.txt` is moved into the `Documents` directory.

> **Note**
>
> If a file with the same name already exists in the destination, it may be overwritten depending on your system configuration.

---

## `rm *.txt`

Removes all files that match a specific pattern.

The `*` symbol is called a **wildcard** and represents any sequence of characters.

### Syntax

```bash
rm *.txt
```

### Example

Before running the command:

```text
notes.txt
chapter1.txt
chapter2.txt
README.md
```

Run:

```bash
rm *.txt
```

After execution:

```text
README.md
```

### Explanation

The command deletes every file whose name ends with `.txt` in the current directory.

> **Warning**
>
> Be careful when using wildcards. Once executed, all matching files are permanently removed.

---

## `rm -i`

Removes files interactively by asking for confirmation before each deletion.

### Syntax

```bash
rm -i <filename>
```

### Example

```bash
rm -i notes.txt
```

Output:

```text
remove regular file 'notes.txt'? y
```

### Explanation

Instead of deleting the file immediately, Bash asks for confirmation.

This is useful when deleting important files because it reduces the chance of accidental deletion.

---

## `alias rm='rm -i'`

Creates an alias that makes the `rm` command interactive by default.

### Syntax

```bash
alias rm='rm -i'
```

### Example

```bash
alias rm='rm -i'
```

### Explanation

After creating this alias, every time you use the `rm` command, Bash automatically behaves as if you had typed `rm -i`.

This is a common safety practice for beginners.

---

## `alias rm`

Displays the alias currently assigned to the `rm` command.

### Syntax

```bash
alias rm
```

### Example

```bash
alias rm='rm -i'
```

### Explanation

This command allows you to verify whether an alias has been created successfully.

---

## `history`

Displays the list of commands that have previously been executed.

### Syntax

```bash
history
```

### Example

```text
1  pwd
2  ls
3  touch notes.txt
4  rm notes.txt
```

### Explanation

Every command entered into the shell is stored in the command history.

The `history` command allows you to review previously executed commands, making it easier to repeat or troubleshoot commands.

---

## `ls -a`

Lists all files and directories, including hidden files.

### Syntax

```bash
ls -a
```

### Example

```text
.
..
.bashrc
.git
notes.txt
```

### Explanation

By default, `ls` hides files whose names begin with a dot (`.`).

Using the `-a` option displays both visible and hidden files.

> **Note**
>
> Hidden files are commonly used to store configuration settings for applications and the shell.

---

## `.` (Current Directory)

The single dot (`.`) represents the **current working directory**.

### Example

```bash
cd .
```

### Explanation

Since `.` refers to the current directory, running this command does not change your location.

The `.` symbol is frequently used in Bash scripts and file paths.

---

## `..` (Parent Directory)

The double dot (`..`) represents the **parent directory** of the current working directory.

### Example

```bash
cd ..
```

### Explanation

This command moves one directory level up in the filesystem hierarchy.

For example:

```text
/home/john/Documents
```

After running:

```bash
cd ..
```

Current directory becomes:

```text
/home/john
```

---

## `cd -`

Returns to the previously visited working directory.

### Syntax

```bash
cd -
```

### Example

Suppose you are currently in:

```text
/home/john/Documents
```

Move to another directory:

```bash
cd Downloads
```

Return to the previous directory:

```bash
cd -
```

Output:

```text
/home/john/Documents
```

### Explanation

The `cd -` command is useful when switching between two directories frequently, as it immediately returns you to your previous location.

---

# Summary

In this chapter, you learned the fundamental Bash commands required for navigating directories and performing basic file operations.

The commands covered were:

* `pwd` — Print the current working directory.
* `ls` — List files and directories.
* `touch` — Create a new empty file.
* `rm` — Remove a file.
* `clear` — Clear the terminal screen.
* `cd` — Change the current working directory.
* `mv` — Move or rename files and directories.
* `rm *.txt` — Delete multiple files using a wildcard.
* `rm -i` — Remove files with confirmation.
* `alias rm='rm -i'` — Make `rm` interactive by default.
* `alias rm` — Display the current alias for `rm`.
* `history` — Display previously executed commands.
* `ls -a` — List all files, including hidden files.
* `.` — Represents the current directory.
* `..` — Represents the parent directory.
* `cd -` — Return to the previous working directory.

---

## Key Takeaways

* A shell interprets and executes commands entered by the user.
* Bash follows the **REPL (Read, Evaluate, Print, Loop)** execution model.
* Navigation commands such as `pwd`, `cd`, and `ls` help you move through the filesystem.
* File management commands such as `touch`, `mv`, and `rm` allow you to create, rename, move, and delete files.
* Wildcards like `*` can be used to perform operations on multiple files simultaneously.
* Hidden files can be viewed using `ls -a`.
* Directory shortcuts (`.`, `..`, and `cd -`) simplify filesystem navigation.

---

Congratulations! You have completed **Chapter 1: Basic File Manipulation**.


