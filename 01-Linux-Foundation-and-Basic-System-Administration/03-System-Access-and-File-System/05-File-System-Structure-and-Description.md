# 🗂️ Linux File System Structure & Directory Descriptions

> **Goal:** Understand *what each Linux directory does*, *why it exists*, and *when you use it* — not just memorize names.

---

## 🌳 What Is the Linux File System Structure?

Linux uses a **tree-like structure** where **everything starts from `/` (slash)**.

- `/` is the **root of the file system**
- All files, folders, devices, and processes live *under* `/`
- Unlike Windows (`C:\`, `D:\`), Linux has **one unified hierarchy**

📌 Think of `/` as the **trunk of a tree** — every branch grows from it.

---

## 🧠 High-Yield Linux Directories (Ordered by Importance)

Below are the **most important directories**, explained **one by one**, exactly how Linux actually uses them.

---

## 🔑 `/boot` — Bootloader Files (CRITICAL)

### Purpose
- Contains files required to **boot the operating system**
- Includes **GRUB configuration files**

### Key File
- `grub.cfg` → tells the system:
  - Which OS to boot
  - Which kernel version to load

### What Happens During Boot?
1. System powers on
2. Firmware looks for `/boot`
3. GRUB reads `grub.cfg`
4. OS loads based on instructions

📌 **Hard-coded behavior:**  
The system *always* checks `/boot` first.

⚠️ **Do NOT edit files here unless you know exactly what you’re doing.**

---

## 👑 `/root` — Root User Home Directory (NOT `/`)

### Important Clarification
- `/` = root of filesystem  
- `/root` = **home directory of the root user**

### Example
If logged in as root and you run:
- `pwd`  
You will see:
- `/root`

📌 Regular users live in `/home`,  
📌 Root user lives in `/root`.

---

## 🔌 `/dev` — Device Files

### Purpose
- Represents **hardware devices as files**

### Examples
- Hard disks
- USB drives
- CD-ROM
- Keyboard
- Speakers

📌 In Linux:
> **Everything is treated as a file — even hardware.**

---

## ⚙️ `/etc` — Configuration Files (VERY IMPORTANT)

### Purpose
- Stores **system-wide configuration files**
- Almost every service reads configs from here

### Examples
- DNS → `/etc/named.conf`
- Mail → `/etc/mail/sendmail.cf`
- Network → `/etc/network/`

⚠️ **Golden Rule**
> ALWAYS make a backup before editing files in `/etc`.

Example:
- `cp file.conf file.conf.bak`

📌 Messing up `/etc` = broken system.

---

## 📜 `/bin` → `/usr/bin` — User Commands

### Purpose
- Contains **basic commands used by all users**

### Examples
- `ls`
- `pwd`
- `cp`
- `mv`

📌 In modern Linux:
- `/bin` is **linked** to `/usr/bin`

These commands are:
- Essential
- Available even in rescue mode

---

## 🛠️ `/sbin` → `/usr/sbin` — System Commands

### Purpose
- Commands for **system administration**

### Used For
- Disk management
- Filesystem repair
- System configuration

📌 Typically used by **root or sudo users**

---

## 📦 `/opt` — Optional / Third-Party Applications

### Purpose
- Stores **non-OS, third-party software**

### Examples
- Oracle
- SAP
- Custom enterprise applications

📌 OS tools (DNS, NTP) **do NOT go here**  
📌 Third-party software **does**

---

## ⚡ `/proc` — Running Processes (Virtual)

### Purpose
- Stores files representing **currently running processes**
- Created dynamically by the **kernel**

### Key Facts
- Exists only while system is running
- Empties on shutdown
- Files are NOT stored on disk

📌 Think of `/proc` as a **live window into the kernel**

---

## 📚 `/lib` → `/usr/lib` — Libraries

### Purpose
- Stores **shared libraries** needed by commands and applications

### Why It Matters
Commands like `ls` and `pwd`:
- Are written in C/C++
- Depend on library files stored here

📌 No libraries → commands won’t run

---

## 🧪 `/tmp` — Temporary Files

### Purpose
- Temporary storage for short-lived files

### Characteristics
- Files can be deleted anytime
- Cleared on reboot (usually)

📌 Safe place for:
- Scratch files
- Testing
- Temporary downloads

---

## 👤 `/home` — Regular User Directories

### Purpose
- Stores **home directories for non-root users**

### Example
- `/home/ezabyss`
- `/home/abhishek`

📌 Each user gets:
- Desktop
- Documents
- Downloads
- Personal configs

---

## 🧾 `/var` — Logs & Variable Data

### Purpose
- Stores **log files and changing data**

### Most Important Subdirectory
- `/var/log`

📌 If something breaks:
> **Check `/var/log` first**

Used for:
- System logs
- Application logs
- Troubleshooting

---

## 🔄 `/run` — Runtime Data (Temporary)

### Purpose
- Stores **process ID (PID) files**
- Used by system services during boot

### Characteristics
- Exists only while system is running
- Cleared on reboot

📌 Helps system track running services

---

## 🧲 `/mnt` — Manual Mount Point

### Purpose
- Used to **manually mount external filesystems**

### Example
Mounting a drive:
- `mount /dev/sdb1 /mnt`

📌 Empty unless something is mounted

---

## 💿 `/media` — Removable Media

### Purpose
- Auto-mount location for removable devices

### Examples
- CD-ROM
- USB drives
- ISO files in virtual machines

📌 Virtual machine ISO → `/media/cdrom`

---

## 🧠 Memory Hack (Never Forget This)

| Directory | Think of it as |
|--------|----------------|
| `/boot` | System ignition key |
| `/etc` | Control panel |
| `/home` | User apartments |
| `/var` | Security cameras (logs) |
| `/proc` | Live system monitor |
| `/opt` | Installed software store |

---

## ✅ One-Line Summary

> The Linux file system is a structured hierarchy starting from `/`, where each directory has a specific role to ensure stability, security, and efficiency.

---

⭐ **Tip:**  
Don’t memorize blindly — **visualize what breaks if a directory disappears**. That’s real understanding.

---

**✍️ Notes By Abhishek (Ez Abyss)**
