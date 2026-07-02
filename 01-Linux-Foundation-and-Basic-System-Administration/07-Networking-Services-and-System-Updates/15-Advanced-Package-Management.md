# 📦 Advanced Package Management

---

# 🎯 1. What is Package Management?

**Package management** means installing, upgrading, removing, and checking software packages in Linux.

In Red Hat-based systems like:

- RHEL
- CentOS
- Fedora

We mainly use:

- `dnf`
- `rpm`

---

# 🌍 Real-World Example

Think of Linux packages like **apps on your phone**.

| Phone | Linux |
|---|---|
| App Store | Repository |
| Install app | Install package |
| Update app | Upgrade package |
| Delete app | Remove package |
| App details | Package information |

---

# 🧠 2. RPM vs DNF

## 🔹 RPM

**RPM** stands for **Red Hat Package Manager**.

It installs `.rpm` files directly.

Example:

`rpm -ivh package.rpm`

---

## 🔹 DNF

**DNF** is a smarter package manager.

It can:

- Download packages
- Install packages
- Resolve dependencies
- Remove packages
- Update packages

Example:

`dnf install ksh`

---

# ⭐ Rule

Use **DNF first** whenever possible.

Use **RPM** when you already have the `.rpm` file.

---

# 🔁 3. DNF vs RPM

| Feature | DNF | RPM |
|---|---|---|
| Downloads package | ✅ Yes | ❌ No |
| Installs package | ✅ Yes | ✅ Yes |
| Handles dependencies | ✅ Yes | ❌ No |
| Removes package | ✅ Yes | ✅ Yes |
| Best for beginners | ✅ Yes | ⚠️ Advanced |

---

# 🌍 Real-World Example

## DNF

Like ordering food through an app.

The app finds the restaurant, orders food, and delivers it.

## RPM

Like you already have food in your hand and just need to eat it.

---

# 🧪 4. Practice Package: Korn Shell

In this lesson, we use **Korn Shell** package.

Package name:

`ksh`

Korn Shell is another Linux shell, like Bash.

---

# 🔍 5. Check If Package Is Installed

`rpm -qa | grep ksh`

Meaning:

- `rpm` = package manager
- `-q` = query
- `-a` = all packages
- `grep ksh` = search for ksh

If nothing shows, package is not installed.

---

# 🌐 6. Check Internet Connection

`ping www.facebook.com`

or

`ping www.google.com`

If replies come back, internet works.

---

# 🌐 7. Check IP Address

`ip a`

This shows your machine IP address.

Example:

`192.168.1.49`

---

# 📥 8. Install Package Using DNF

`dnf install ksh`

If asked:

`Is this ok [y/N]:`

Type:

`y`

---

## Auto Yes Install

`dnf install ksh -y`

The `-y` means automatically answer yes.

---

# ✅ 9. Verify Installation

`rpm -qa | grep ksh`

If installed, you will see package name.

Example:

`ksh-xxxx.x86_64`

---

# ❌ 10. Remove Package Using DNF

`dnf remove ksh`

Auto yes:

`dnf remove ksh -y`

Verify removal:

`rpm -qa | grep ksh`

---

# 📦 11. Install RPM File Manually

Sometimes you may already have the `.rpm` file.

Example file:

`ksh-xxxx.x86_64.rpm`

Install it using:

`rpm -ivh ksh-xxxx.x86_64.rpm`

---

# 🧠 Meaning of RPM Options

| Option | Meaning |
|---|---|
| `-i` | Install |
| `-v` | Verbose / show details |
| `-h` | Show hash progress |

---

# 🌍 Real-World Example

Installing with RPM is like using an offline installer:

`setup.exe`

You already downloaded it, now you just install it.

---

# 🌐 12. Download RPM Using wget

If you have a direct RPM link:

`wget rpm-link-here`

Example:

`wget https://example.com/package.rpm`

Then install:

`rpm -ivh package.rpm`

---

# ℹ️ 13. View Package Information

`rpm -qi ksh`

Meaning:

- `-q` = query
- `-i` = information

This shows:

- Package name
- Version
- Release
- Architecture
- Install date
- Summary
- Description

---

# ❌ 14. Remove Package Using RPM

First find full package name:

`rpm -qa | grep ksh`

Then remove:

`rpm -e full-package-name`

Example:

`rpm -e ksh-xxxx.x86_64`

Verify:

`rpm -qa | grep ksh`

---

# ⚠️ RPM Remove Tip

With `rpm -e`, use the **exact installed package name**, not the `.rpm` filename.

---

# ⚙️ 15. Find Configuration Files of a Package

`rpm -qc ksh`

Meaning:

- `-q` = query
- `-c` = configuration files

This shows config files related to that package.

---

# 🌍 Real-World Example

Installing an app is easy.

But changing its settings requires finding the settings file.

In Linux, package settings are usually inside:

`/etc`

---

# 📍 16. Find Command Path

To find where a command is located:

`which ksh`

Example output:

`/usr/bin/ksh`

---

# 📦 17. Find Which Package Owns a Command

Use:

`rpm -qf /usr/bin/ksh`

Meaning:

- `-q` = query
- `-f` = file

This tells which package provides that command.

---

# Example with pwd Command

Find path:

`which pwd`

Output:

`/usr/bin/pwd`

Find package:

`rpm -qf /usr/bin/pwd`

Output may show:

`coreutils-xxxx`

So the `pwd` command belongs to the **coreutils** package.

---

# 🚨 Important Warning

If you remove the package that owns an important command, that command may stop working.

Example:

If you remove `coreutils`, commands like these can break:

- `pwd`
- `ls`
- `cat`
- `cp`
- `mv`

---

# 📌 18. Important Commands Summary

| Task | Command |
|---|---|
| Check installed package | `rpm -qa | grep ksh` |
| Install with DNF | `dnf install ksh` |
| Remove with DNF | `dnf remove ksh` |
| Install RPM file | `rpm -ivh package.rpm` |
| Remove with RPM | `rpm -e package-name` |
| Package info | `rpm -qi ksh` |
| Config files | `rpm -qc ksh` |
| Command path | `which ksh` |
| Package owning file | `rpm -qf /usr/bin/ksh` |
| Check IP | `ip a` |
| Check internet | `ping www.google.com` |

---

# ⚠️ 19. Common Problems

| Problem | Cause | Fix |
|---|---|---|
| Package not found | Wrong name or repo issue | Check package name |
| No internet | Network issue | Use `ping www.google.com` |
| Permission denied | Not root | Use `su -` |
| Dependency error | RPM does not resolve dependencies | Use DNF |
| Command not found | Package not installed | Install package |

---

# 🧠 20. Memory Tricks

Remember:

> **DNF = Smart installer**  
> **RPM = Manual installer**

Easy formula:

- Install online → `dnf install`
- Install local file → `rpm -ivh`
- Remove package → `dnf remove` or `rpm -e`
- Package info → `rpm -qi`
- Config files → `rpm -qc`
- File owner → `rpm -qf`

---

# 🌍 Real-World Scenario

You are working as a Linux admin.

Your manager says:

> “Install Korn Shell on this server.”

Best command:

`dnf install ksh`

Later manager asks:

> “Where are its configuration files?”

Use:

`rpm -qc ksh`

Then manager asks:

> “Which package gives us the pwd command?”

Use:

`which pwd`

Then:

`rpm -qf /usr/bin/pwd`

That is real package management work.

---

# 💼 Questions

## Q1. What is RPM?

RPM means Red Hat Package Manager.

---

## Q2. What is DNF?

DNF is a package manager used to install, update, and remove packages while handling dependencies.

---

## Q3. Difference between RPM and DNF?

DNF handles dependencies and can download packages. RPM installs local `.rpm` files directly.

---

## Q4. How do you check if a package is installed?

`rpm -qa | grep package-name`

---

## Q5. How do you install a package using DNF?

`dnf install package-name`

---

## Q6. How do you install a local RPM file?

`rpm -ivh package.rpm`

---

## Q7. How do you remove a package using RPM?

`rpm -e package-name`

---

## Q8. How do you view package information?

`rpm -qi package-name`

---

## Q9. How do you find package configuration files?

`rpm -qc package-name`

---

## Q10. How do you find which package owns a command?

First:

`which command-name`

Then:

`rpm -qf full-command-path`

---

# 📌 Short Revision

- Package management = install, update, remove, inspect software
- RHEL/CentOS uses `dnf` and `rpm`
- Best install method = `dnf install package`
- Manual RPM install = `rpm -ivh package.rpm`
- Remove package = `dnf remove package`
- Package info = `rpm -qi package`
- Config files = `rpm -qc package`
- Find command package = `rpm -qf /path/to/command`

---

# 🏆 Takeaway

A normal Linux user installs packages.

A strong Linux admin knows:

- How to install packages
- How to remove packages
- How to inspect package details
- How to find configuration files
- How to identify which package owns a command

This is what makes package management a real admin skill.

---

# ✍️ Notes By Abhishek (Ez Abyss)
