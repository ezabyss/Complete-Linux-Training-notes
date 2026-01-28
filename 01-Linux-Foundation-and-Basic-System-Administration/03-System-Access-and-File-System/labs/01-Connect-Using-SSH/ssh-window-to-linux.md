# 🧪 Lab: Secure SSH Access from Windows to Linux (Virtual Machine)

## 🎯 Lab Objective
To practice accessing a Linux virtual machine **remotely** from a Windows system using **SSH**, and to understand real-world SSH authentication behavior.

This lab reflects where a Linux servers are accessed remotely rather than through a physical console.

---

## 🧠 Concepts Covered
- SSH (Secure Shell) fundamentals
- Console access vs remote access
- Private IP addressing
- First-time SSH host key verification
- User authentication flow
- Troubleshooting common SSH errors

---

## 🧰 Lab Environment

### Host System
- Operating System: Windows 11
- SSH Client: Built-in OpenSSH (Command Prompt)

### Guest System
- Operating System: CentOS Stream
- Virtualization Platform: VMWARE
- Network Configuration: NAT / Bridged
- Linux User Account: ezabyss

---

## 🔹 Step 1: Power On the Linux Virtual Machine

Ensure the Linux virtual machine is **powered ON**.

Important note:  
SSH connections are **not possible** if the virtual machine is powered off.

---

## 🔹 Step 2: Obtain the Linux VM IP Address

Log in to the Linux VM **via console**, then run:

    ifconfig

Identify the active network interface (for example: ens33) and note the **private IP address**.

Example used in this lab:

    192.168.14.128

This is a **private IP address**.

---

## 🔹 Step 3: Verify SSH Availability on Windows

Open **Command Prompt** on Windows and run:

    ssh

If SSH usage information is displayed, OpenSSH is installed and ready to use.

---

## 🔹 Step 4: Connect to Linux Using SSH

From the Windows command prompt, run:

    ssh -l ezabyss 192.168.14.128

---

### First-Time SSH Connection Behavior

On the first connection attempt, SSH may display a host authenticity warning similar to:

The authenticity of host '192.168.14.128' can't be established.  
Are you sure you want to continue connecting (yes/no)?

    yes

>This action stores the server’s fingerprint in the local `known_hosts` file and establishes trust for future connections.

---

## 🔹 Step 5: Authenticate with User Credentials

When prompted, enter the password for the Linux user account `ezabyss`.

Upon successful authentication, you should see:

    [ezabyss@localhost ~]$

You are now logged into the Linux system **remotely via SSH**.

---

## 🧠 Key Learnings

- SSH requires the target system to be powered on
- First-time SSH connections establish host trust
- Permission denied errors usually indicate authentication issues
- Private IP addresses are safe for internal documentation
- Enterprise Linux systems are typically managed remotely

---

## 🧠 Memory Rule 

If SSH reaches the server but denies access, investigate authentication — not networking.

---

## 🏁 Lab Outcome

- Successfully accessed a Linux VM remotely from Windows
- Understood SSH trust and authentication flow

---

✍️ Notes By Abhishek (Ez Abyss)
