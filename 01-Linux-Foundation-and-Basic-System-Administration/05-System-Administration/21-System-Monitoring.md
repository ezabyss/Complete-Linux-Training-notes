# 🖥️ Linux System Monitoring – System Administrator 
- df, dmesg, iostat 1, netstat, free, top

---

# 🎯 Who uses it?

- System Administration
- Linux Engineering
- DevOps
- Cloud Infrastructure
- SRE (Site Reliability Engineering)

You MUST know system monitoring commands.

These commands tell you:

- Is CPU overloaded?
- Is memory full?
- Is disk full?
- Is network overloaded?
- Is hardware failing?

---

# 🧠 The Core Monitoring Commands

| Resource | Command |
|-----------|----------|
| CPU + Processes | `top` |
| Disk Usage | `df` |
| Disk Usage by File | `du` |
| Kernel Messages | `dmesg` |
| Disk IO Stats | `iostat` |
| Network Info | `ip` |
| Socket Connections | `ss` |
| Memory Usage | `free` |
| CPU Info | `cat /proc/cpuinfo` |
| Memory Info | `cat /proc/meminfo` |

---

# 🔥 1. `top` – Real-Time Process Monitoring

Run:

`top`

Shows:

- CPU usage
- Memory usage
- Running processes
- Load average
- PID, User, Command

Exit:

`q`

---

### 🔎 Why It’s Important

If server is slow → First command to check is `top`.

---

# 💾 2. `df` – Disk Space Usage

Basic:

`df`

Human readable:

`df -h`

---

### Key Columns

| Column | Meaning |
|---------|----------|
| Size | Total disk |
| Used | Used space |
| Avail | Available |
| Use% | Percentage used |

---

### 🚨 Scenario

If `Use%` shows **100%** → System may crash.

First troubleshooting step:

`df -h`

---

# 📁 3. `du` – Disk Usage Per File/Directory

Used to find **what is filling disk**.

Example:

`du -h /var`

Useful when disk is full.

---

# 🧠 4. `dmesg` – Kernel & Hardware Messages

Run:

`dmesg`

View page by page:

`dmesg | more`

---

### Shows:

- Boot messages
- Hardware errors
- CPU errors
- Memory errors
- Driver issues

---

### Real-World Use

If system crashes or hardware fails → check `dmesg`.

---

# 💿 5. `iostat` – Disk IO Statistics

Run:

`iostat`

Refresh every second:

`iostat 1`

Exit:

`Ctrl + C`

---

### Shows:

- Read per second
- Write per second
- Disk utilization
- IO wait

---

### Why Important?

If disk is slow → `iostat` helps identify bottleneck.

---

# 🌐 6. Network Monitoring – Modern Replacement for netstat

Older Systems (CentOS 7 and below):

`netstat`

Newer Systems (CentOS 8+):

Use:

- `ip`
- `ss`

---

# 🔹 `ip` Command

Show routing info:

`ip route`

Shows:

- Default gateway
- Source IP
- Interface

---

# 🔹 `ss` Command (Socket Statistics)

View active connections:

`ss`

Page view:

`ss | more`

---

### Shows:

- Local address
- Remote address
- Port numbers
- Connection state
- Send/Receive queue

---

### Rember

If asked:

> How do you check open ports?

Answer: 

`ss -tuln`

---

# 🧠 7. `free` – Memory Usage

Run:

`free`

Better format:

`free -h`

Shows:

- Total RAM
- Used RAM
- Free RAM
- Swap (virtual memory)

---

# 📂 8. `/proc` Directory – System Information

Linux stores live system info in:

`/proc`

---

## CPU Info

`cat /proc/cpuinfo`

Shows:

- CPU cores
- Model
- Speed
- Architecture

---

## Memory Info

`cat /proc/meminfo`

Page by page:

`cat /proc/meminfo | more`

Shows:

- Total memory
- Free memory
- Buffers
- Cached memory

---

# 🧠 System Monitoring Workflow (Real Scenario)

If server is slow:

1. Check CPU → `top`
2. Check memory → `free -h`
3. Check disk → `df -h`
4. Check IO → `iostat`
5. Check logs → `dmesg`
6. Check network → `ss`

---

# 🎓 Rapid-Fire Answers

If asked:

### ❓ How do you monitor CPU?
`top`

### ❓ How do you check disk space?
`df -h`

### ❓ How do you find which directory is filling disk?
`du -h`

### ❓ How do you check hardware errors?
`dmesg`

### ❓ How do you check memory?
`free -h`

### ❓ How do you check active connections?
`ss`

---

# 🧠 Advanced Insight

Linux performance is based on:

- CPU
- Memory
- Disk IO
- Network

These commands map directly to those four pillars.

---

# 🏁 Final Takeaway

You do NOT need to memorize every option.

But you MUST:

- Know what each command does
- Know when to use it
- Know what problem it solves

That is what separates:

Beginner ❌  
From  
System Engineer ✅  

---

**✍️ Notes By Abhishek (Ez Abyss)**
