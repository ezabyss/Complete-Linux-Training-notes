# 🛠 Linux System Utility Commands

These are basic system utility commands commonly used in Linux environments.  

When working in GUI mode, you can see:

- Time
- Calendar
- Calculator

But when working in terminal (SSH / PuTTY), you rely on commands.

Below are the most useful system utility commands.

---

# 📅 1️⃣ `date` — Show Current Date & Time

    date

Example output:

    Tue Mar 13 10:45:22 EDT 2025

Used for:
- Checking system time
- Logging
- Scripts (cron jobs, automation)

---

# ⏱ 2️⃣ `uptime` — System Running Time

    uptime

Example:

    10:50:03 up 3 days,  4:21,  2 users,  load average: 0.15, 0.20, 0.10

Shows:

- Current time
- How long system has been running
- Number of users logged in
- Load average (1, 5, 15 minutes)

---

# 🖥 3️⃣ `hostname` — System Name

    hostname

Displays the system’s hostname.

Important:
Always check hostname before running critical commands to avoid mistakes.

---

# 🧬 4️⃣ `uname` — System Information

Basic:

    uname

Output:

    Linux

Detailed:

    uname -a

Shows:

- Kernel name
- Hostname
- Kernel version
- Architecture
- Build date

Useful in multi-OS environments.

---

# 📍 5️⃣ `which` — Command Location

Find where a command is stored:

    which pwd

Example output:

    /usr/bin/pwd

Every command in Linux is a file stored in directories like:

- /usr/bin
- /bin
- /sbin

Check file details:

    ls -l /usr/bin/pwd

---

# 📦 Count Total Commands

Example: count commands in `/usr/bin`

    ls /usr/bin | wc -l

Shows total number of commands available in that directory.

---

# 📆 6️⃣ `cal` — Calendar

Current month:

    cal

Specific year:

    cal 2025

Specific month & year:

    cal 9 1977

Shows September 1977 calendar.

---

# 🧮 7️⃣ `bc` — Command-Line Calculator

Start calculator:

    bc

Example:

    2+2
    256*321
    100/5

To exit:

    quit

For floating-point math:

    bc -l

---

# 🧠 Quick Summary

| Command | Purpose |
|----------|----------|
| `date` | Show date and time |
| `uptime` | Show system running time |
| `hostname` | Show system name |
| `uname` | Show OS details |
| `which` | Locate command file |
| `cal` | Display calendar |
| `bc` | Terminal calculator |

---

# 🎯 Key Takeaway

These small commands are simple but powerful.

They are commonly used in:

- Troubleshooting
- Monitoring
- Automation scripts
- System administration tasks

Always use:

    man command_name

to explore more options.

---

**✍️ Notes By Abhishek (Ez Abyss)**  
