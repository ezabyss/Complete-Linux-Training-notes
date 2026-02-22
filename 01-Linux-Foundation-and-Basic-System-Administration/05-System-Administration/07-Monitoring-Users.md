# 👀 Monitoring Users in Linux

Managing users does not stop at creating accounts.  
A system administrator must monitor:

- Who is logged in  
- When they logged in  
- From where they logged in  
- What they are running  

Below are the basic commands used to monitor users.

---

# 🔎 1️⃣ `who` — Who Is Logged In

Basic command:

    who

Shows:

- Username
- Terminal (tty/pts)
- Login time
- Remote IP (if applicable)

Example output:

    ezabyss    pts/0    2025-07-18 10:12 (192.168.1.15)
    spiderman pts/1  2025-07-18 10:15 (192.168.1.20)

If multiple terminals are opened, each session appears separately.

Purpose:
- Check active sessions
- Investigate high system load
- Confirm remote logins

---

# 📜 2️⃣ `last` — Login History

Displays login history from `/var/log/wtmp`.

    last

To view page by page:

    last | more

Shows:

- Username
- Terminal
- Source IP
- Login time
- Logout time
- System reboot history

Useful when:
- Investigating suspicious login
- Checking reboot events
- Auditing access history

---

## 🎯 Show Only Usernames

    last | awk '{print $1}'

Remove duplicates:

    last | awk '{print $1}' | sort | uniq

---

# 📊 3️⃣ `w` — Who + What They Are Doing

    w

Displays:

- Username
- Login time
- Idle time
- CPU usage
- Current command being executed

More detailed than `who`.

Example:

    USER     TTY   FROM         LOGIN@   IDLE   JCPU   PCPU  WHAT
    ezabyss     pts/0 192.168.1.15 10:12    2:00   0.10s  0.01s bash

Useful for:
- Checking system load
- Seeing long-running processes
- Identifying idle users

---

# 🧑‍💻 4️⃣ `id` — User Identity Information

Check your own identity:

    id

Check another user:

    id spiderman

Displays:

- UID (User ID)
- GID (Primary Group ID)
- Supplementary groups

Example:

    uid=1001(abhi) gid=1001(abhi) groups=1001(abhi),10(wheel)

---

# 🧠 5️⃣ `finger` (Optional Tool)

    finger username

Provides:

- Login info
- Real name
- Last login time

Note:
`finger` is not installed by default.
Must install manually.

---

# 🏷 Additional Helpful Commands

Check hostname:

    hostname

Check current user:

    whoami

Check logged-in terminals only:

    users

---

# 🔐 Why Monitoring Matters

User monitoring helps:

- Detect unauthorized access
- Investigate performance issues
- Track login history
- Audit system usage

In production environments, these commands are used daily.

---

# 🎯 Key Commands Summary

| Command | Purpose |
|----------|---------|
| `who` | Show currently logged-in users |
| `last` | Show login history |
| `w` | Show users + what they are doing |
| `id` | Show user identity info |
| `finger` | Detailed user info (if installed) |

---

Practice each command with:

    man command_name

Example:

    man who

---

**✍️ Notes By Abhishek (Ez Abyss)**  
