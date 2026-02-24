# ⚙️ Processes and Jobs in Linux

Before learning commands, let’s clearly understand the terminology.

---

# 📌 Key Terms Explained

---

## 🖥 1️⃣ Application / Service

An application (or service) is a program that runs on your system.

Examples:

- Apache (httpd)
- NTP
- NFS
- SSH
- MySQL

In Windows:
- Word
- PowerPoint
- Excel

In Linux:
- Services usually run in the background.

---

## 📜 2️⃣ Script

A script is:

- A file containing commands
- Executed by the system
- Used to automate tasks

Examples:

- Bash scripts
- Startup scripts
- Application startup files

Most Linux commands are executable files (scripts or binaries).

---

## 🔄 3️⃣ Process

When you run a program, it becomes a process.

Each process has:

- PID (Process ID)
- Parent process
- Memory usage
- CPU usage

One application can create multiple processes.

Example:
Starting Apache may create several child processes.

---

## 👹 4️⃣ Daemon

A daemon is:

- A background process
- Always running
- Usually ends with “d”

Examples:

- httpd
- sshd
- crond

Daemons continuously listen for requests.

---

## 🧵 5️⃣ Thread

A thread is:

- A smaller unit inside a process
- One process can have multiple threads
- Used to handle multiple tasks simultaneously

Example:
If multiple clients connect to NFS, each connection may create a thread.

---

## 📅 6️⃣ Job

A job is:

- A scheduled task
- Created by a scheduler
- Runs automatically at specified time

Schedulers:

- `cron`
- `at`

---

# 🛠 Important Commands

---

# 🔹 1️⃣ `systemctl` — Manage Services

Modern Linux systems use:

    systemctl

Examples:

Start service:

    systemctl start httpd

Stop service:

    systemctl stop httpd

Check status:

    systemctl status httpd

Older systems used:

    service httpd start

Now replaced by `systemctl`.

---

# 🔹 2️⃣ `ps` — View Running Processes

Basic:

    ps

Common usage:

    ps -ef

Shows:

- PID
- Parent PID
- CPU usage
- Start time
- Command name

---

# 🔹 3️⃣ `top` — Live Process Monitor

    top

Displays:

- Real-time process list
- CPU usage
- Memory usage
- Load average

Press:

    q

to quit.

---

# 🔹 4️⃣ `kill` — Terminate Process

Kill by PID:

    kill 1234

Force kill:

    kill -9 1234

Always try normal kill before force kill.

---

# 🔹 5️⃣ `crontab` — Schedule Recurring Jobs

Edit cron jobs:

    crontab -e

Example entry:

    0 2 * * * /home/user/backup.sh

Runs daily at 2:00 AM.

Cron = recurring schedule.

---

# 🔹 6️⃣ `at` — One-Time Scheduled Job

Schedule one-time task:

    at 10:30

Then type command:

    reboot

Press:

    Ctrl + D

`at` = one-time execution.

---

# 🧠 Quick Comparison

| Term | Meaning |
|-------|----------|
| Application | Program running on system |
| Script | Executable command file |
| Process | Running instance of program |
| Daemon | Background process |
| Thread | Sub-task inside process |
| Job | Scheduled task |

---

# 🎯 Key Takeaway

Application → creates → Process  
Process → may contain → Threads  
Daemon → background process  
Cron / at → schedule jobs  

Understanding these concepts is essential before managing services and troubleshooting performance.

---

**✍️ Notes By Abhishek (Ez Abyss)**  
