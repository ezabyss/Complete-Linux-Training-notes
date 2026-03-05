# Shell Scripting Basics

## Introduction

Shell scripting allows users to **automate tasks by writing a series of commands in a script file**.

Instead of typing commands one by one in the terminal, a script can run them automatically in sequence.

This makes system administration and automation **much faster and more efficient**.

---

# What is a Shell Script?

A **shell script** is an executable file containing multiple shell commands that are executed **sequentially**.

Execution order:

```
Command 1
Command 2
Command 3
Command 4
```

Commands always run **from top to bottom** in the order they appear.

---

# Structure of a Shell Script

A typical shell script consists of the following parts:

1. **Shebang (Shell Definition)**
2. **Comments**
3. **Commands**
4. **Control Statements (conditions, loops)**

---

# 1. Shebang (Shell Definition)

The **first line of every shell script defines which shell interpreter should run the script**.

Example:

```
#!/bin/bash
```

Explanation:

| Symbol | Meaning |
|------|--------|
| `#!` | Called **Shebang** |
| `/bin/bash` | Specifies Bash shell interpreter |

The `!` symbol is often called **"bang"**, so `#!` is pronounced **"shebang"**.

Most Linux scripts use **Bash**.

---

# 2. Comments in Shell Scripts

Comments are used to describe what the script does.

They help make scripts easier to understand.

Comments start with:

```
#
```

Example:

```
# This script prints system information
```

Everything after `#` on that line is ignored by the shell.

---

# 3. Commands in Shell Scripts

The main purpose of a shell script is to execute commands.

Example:

```
#!/bin/bash

echo "Hello World"
date
whoami
```

This script:

1. Prints "Hello World"
2. Shows the current date
3. Displays the current user

---

# 4. Control Statements

Shell scripts can also include programming logic.

Examples include:

- `if` statements
- `for` loops
- `while` loops
- `case` statements

Example:

```
if [ $USER == "root" ]
then
    echo "You are root"
else
    echo "You are not root"
fi
```

These statements allow scripts to make decisions and perform repeated tasks.

---

# Shell Script File Permissions

In Linux, every script is simply a **file** until execution permission is granted.

To run a script, it must have **executable permission**.

Example permission:

```
-rwxr-xr-x
```

The `x` represents **executable permission**.

---

# Making a Script Executable

To make a script executable, run:

```
chmod +x scriptname.sh
```

Example:

```
chmod +x backup.sh
```

Now the script can be executed.

---

# Running a Shell Script

There are two main ways to run a shell script.

---

## Method 1: Absolute Path

Use the full path of the script.

Example:

```
/home/user/scripts/myscript.sh
```

---

## Method 2: Current Directory

If you are already in the script's directory, use:

```
./scriptname.sh
```

Example:

```
./myscript.sh
```

The `./` means **run the script from the current directory**.

---

# Why Shell Scripting is Important

Shell scripting is widely used for:

- System administration
- Task automation
- Server maintenance
- Backup scripts
- Log monitoring
- Deployment automation

It is a **fundamental skill in Linux, DevOps, and cybersecurity**.

---

# Summary

A shell script is a file containing commands executed in sequence.

Key elements of a shell script:

| Component | Purpose |
|---|---|
| Shebang (`#!/bin/bash`) | Defines shell interpreter |
| Comments (`#`) | Explain script purpose |
| Commands | Perform system operations |
| Control statements | Add logic and automation |

Scripts must have **executable permissions** before they can run.

---

**✍️ Notes By Abhishek (Ez Abyss)**
