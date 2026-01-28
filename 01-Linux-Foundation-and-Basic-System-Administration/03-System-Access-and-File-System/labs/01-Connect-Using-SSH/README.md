# 🧪 Lab: SSH Connection from Windows to Linux

This lab documents the process of accessing a Linux virtual machine **remotely** from a Windows system using **SSH**.  
It reflects a **real-world enterprise scenario**, where Linux servers are managed over the network rather than through physical or graphical access.

---

## 🎯 Lab Objective

- Understand how SSH works in a client–server model
- Access a Linux system remotely from Windows
- Learn the difference between console and remote access
- Observe first-time SSH trust behavior

---

## 🧠 Concepts Covered

- SSH (Secure Shell)
- Console access vs remote access
- First-time host key verification
- Linux user authentication

---

## 🧰 Lab Environment

### Host System
- Operating System: Windows 11
- SSH Client: Built-in OpenSSH (Command Prompt)

### Guest System
- Operating System: CentOS Stream
- Virtualization Platform: VMWARE
- Network Configuration: Private network (NAT / Bridged)
- Linux User Account: ezabyss

---

## 🔹 Lab Prerequisites

- Linux virtual machine is installed and powered ON
- Network interface is active
- SSH service is running on the Linux machine
- User account exists on the Linux system

---

## 🔹 High-Level Lab Flow

1. Access Linux locally through console
2. Identify the Linux machine’s private IP address
3. Verify SSH availability on Windows
4. Connect from Windows to Linux using SSH
5. Authenticate using Linux user credentials
6. Observe and understand SSH behavior

---


## 🧠 Key Learnings

- SSH requires the target system to be powered ON
- First SSH connections establish trust via host keys
- Permission denied errors usually indicate authentication issues
- Remote access is the standard method of managing Linux systems

---

✍️ Notes By Abhishek (Ez Abyss)
