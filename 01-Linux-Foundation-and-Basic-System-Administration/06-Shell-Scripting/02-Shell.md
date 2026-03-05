# Linux Shell and Types of Shells

## What is a Shell?

A **shell** is a program that acts as an **interface between the user and the operating system kernel**.

It provides an environment where users can execute commands and interact with the operating system.

Think of a shell like a **container (similar to a Tupperware container)** that holds the environment and allows users to interact with the operating system.

The shell provides:

- Command execution environment
- Interaction between users and the OS kernel
- Platform to run programs and scripts

---

# How a Shell Works

The communication flow inside an operating system works like this:

```
User → Application → Shell → Kernel → Hardware
```

### Explanation

| Component | Role |
|---|---|
| User | Executes commands |
| Application | Program initiated by user |
| Shell | Interprets commands |
| Kernel | Core of operating system |
| Hardware | Physical system components |

The **shell interprets user commands and passes them to the kernel**, which then interacts with the hardware.

---

# Shell in Different Operating Systems

Different operating systems provide different shells.

| Operating System | Shell Type |
|---|---|
| Windows | GUI Shell |
| Linux (GUI) | GNOME / KDE |
| Linux (CLI) | Bash, sh, etc |

---

# GUI Shell vs CLI Shell

## GUI Shell (Graphical User Interface)

Examples:

- Windows Desktop
- Linux GNOME
- Linux KDE

Users interact using:

- Mouse
- Icons
- Menus
- Drag and drop

---

## CLI Shell (Command Line Interface)

Examples:

- Bash
- sh
- zsh

Users interact by typing commands in a terminal.

Example commands:

```
ls
cd
mkdir
```

---

# Checking Your Current Shell

To identify which shell you are currently using:

```
echo $0
```

Example output:

```
bash
```

This means the user is currently using the **Bash shell**.

---

# Viewing Available Shells

Linux keeps a list of available shells in:

```
/etc/shells
```

To display the list:

```
cat /etc/shells
```

Example output:

```
/bin/sh
/bin/bash
usr/bin/bash
usr/bin/tmux
/bin/tmux
```

---

# Default Shell for Users

Each user has a default shell assigned in the file:

```
/etc/passwd
```

Example command:

```
cat /etc/passwd
```

Example entry:

```
username:x:1000:1000:User Name:/home/username:/bin/bash
```

The **last field specifies the user's default shell**.

---

# Types of Linux Shells

Linux provides several types of shells.

## 1. GNOME Shell

GNOME is a **graphical desktop environment**.

Features:

- Graphical interface
- Uses mouse and keyboard
- Provides desktop environment for Linux

Users interact through:

- Icons
- Windows
- Menus

---

## 2. KDE Shell

KDE is another **Linux graphical desktop environment**.

Features:

- Highly customizable
- Graphical desktop interface
- Similar functionality to GNOME

Both **GNOME and KDE are GUI shells**.

---

# Command-Line Shells

Now let's focus on **command-line shells**.

These are used when Linux runs without a GUI.

---

# 3. Bourne Shell (sh)

The **Bourne Shell (sh)** is one of the oldest Unix shells.

Developed by:

**Stephen Bourne**

Year:

**1977**

Organization:

**AT&T Bell Labs**

Features:

- Input/output redirection
- Shell scripting
- Variables (string and integer)
- Condition testing
- Loops

Because of its long history, many developers are familiar with it.

---

# 4. Bash (Bourne Again Shell)

**Bash** is the most widely used shell in Linux.

Bash stands for:

```
Bourne Again Shell
```

It was created as an improved version of the Bourne Shell.

Features:

- User-friendly
- Advanced scripting capabilities
- Improved command history
- Better variable handling

Most Linux systems use **Bash as the default shell**.

---

# 5. C Shell (csh)

The **C Shell** was developed by:

**Bill Joy**

Location:

**University of California, Berkeley**

Features:

- Syntax similar to the C programming language
- Command history
- Job control

It is mainly useful for users familiar with **C programming**.

---

# 6. TC Shell (tcsh)

The **TC Shell** is an improved version of the C Shell.

Developed by:

**Ken Greer**

Features:

- Command-line editing
- Command completion
- Improved shell features

However, **TC Shell cannot run Bash scripts directly**.

---

# 7. Korn Shell (ksh)

The **Korn Shell** was developed by:

**David Korn**

Features:

- Compatible with Bourne Shell
- Compatible with Bash scripts
- Floating-point arithmetic
- Job control improvements

It is commonly used in **Unix systems like Solaris**.

---

# Common Shell Usage

| Shell | Common Usage |
|---|---|
| Bash | Most Linux systems |
| sh | Older Unix systems |
| csh | C language programmers |
| tcsh | Enhanced C shell |
| ksh | Solaris / Unix environments |

---

# Important Tip for Beginners

For beginners learning Linux:

**Focus on Bash shell.**

Reasons:

- Most Linux systems use Bash
- Large community support
- Extensive documentation
- Widely used in automation and scripting

---

# Why Shell Knowledge is Important

Learning shell concepts helps you:

- Automate tasks
- Manage servers
- Write shell scripts
- Perform system administration
- Work in cybersecurity and DevOps environments

---

# Summary

A **shell** is a program that allows users to interact with the operating system.

Key points:

- It acts as an interface between users and the kernel.
- Linux provides both GUI shells and command-line shells.
- Bash is the most widely used shell in Linux.
- Multiple shells exist because developers created their own improved versions.

Understanding shells is fundamental for:

- Linux administration
- Shell scripting
- System automation
- Cybersecurity operations

---

**✍️ Notes By Abhishek (Ez Abyss)**
