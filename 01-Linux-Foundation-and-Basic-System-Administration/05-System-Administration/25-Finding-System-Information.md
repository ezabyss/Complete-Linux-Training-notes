# 🖥️ Finding System Information in Linux

---

# 🎯 Why System Information Matters

Every time you log into a Linux machine, the FIRST thing you should know:

- What OS is running?
- What kernel version?
- What hardware is underneath?
- What architecture (32-bit / 64-bit)?
- Which hostname is this?

⚠ Logging into the wrong machine and running `reboot` can cause serious problems.

Professional admins ALWAYS verify system info first.

---

# 🧠 Core Commands You Must Know

| Purpose | Command |
|----------|----------|
| OS version | `cat /etc/redhat-release` |
| Kernel + OS info | `uname -a` |
| Hardware details | `dmidecode` |
| Hostname | `hostname` |

---

# 🔎 1. Check Operating System Version

`cat /etc/redhat-release`

Example output:

CentOS Streat release 9

---

### What This Tells You

- Distribution name
- Version
- Update level

📌 This file exists in RHEL-based systems (CentOS, RHEL, Rocky, AlmaLinux).

---

# 🧠 2. Check Kernel & System Info

`uname -a`

---

### What It Shows

- OS name
- Hostname
- Kernel version
- Architecture (x86_64)
- Build date

---

### Example Breakdown

| Field | Meaning |
|--------|----------|
| Linux | OS |
| hostname | Machine name |
| 5.x.x | Kernel version |
| x86_64 | 64-bit architecture |

---

# 🔐 3. Check Hardware Info (dmidecode)

⚠ Requires root.

Run:

`dmidecode`

If permission denied:

`su -`

Then:

`dmidecode | more`

---

### What It Shows

- BIOS version
- Manufacturer
- Product name
- Serial number
- Processor info
- RAM details
- Motherboard info

---

### Example Insights

- Manufacturer: VMware, Inc.
- Product Name: VMware Virtual Platform
- Memory Size
- CPU Model

Very useful for:

- Inventory tracking
- Hardware troubleshooting
- Asset auditing

---

# 🧠 4. Always Check Hostname

`hostname`

Why?

Before:

- Rebooting
- Shutting down
- Making configuration changes

ALWAYS confirm hostname.

---

# 🔍 Quick Professional Workflow

Every time you SSH into a server:

1. `hostname`
2. `uname -a`
3. `cat /etc/redhat-release`

Takes 5 seconds. Prevents disasters.

---

# 🏗 What Is Under the Hood?

Linux system consists of:

- Hardware
- BIOS
- Kernel
- OS distribution
- Userland applications

These commands help you see each layer.

---

# 🎓 Rapid-Fire Answers

### ❓ How do you check Linux OS version?
`cat /etc/redhat-release`

### ❓ How do you check kernel version?
`uname -a`

### ❓ How do you check hardware info?
`dmidecode`

### ❓ Why run hostname first?
To ensure you're on the correct machine.

---

# 🧠 Advanced Insight

`uname -a` → Software layer  
`cat /etc/redhat-release` → Distribution layer  
`dmidecode` → Hardware layer  

Together → Full system visibility.

---

# ⚠ Common Mistake

Beginner:

Logs in and immediately runs commands.

Professional:

Verifies system identity first.

---

# 🏁 Final Takeaway

Before touching a system:

- Verify hostname
- Verify OS version
- Verify kernel
- Verify hardware

System awareness = Professional discipline.

---

**✍️ Notes By Abhishek (Ez Abyss)**
