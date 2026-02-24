# 🔥 top Command in Linux (Real-Time Process Monitor)


The `top` command provides a **real-time view** of:

- Running processes
- CPU usage
- Memory usage
- System load
- Tasks and threads

It runs in **interactive mode**.

To exit, press:

`q`

---

# 🧩 Basic Usage

Simply run:

`top`

You do not need to be root to view processes.

However:

- To kill processes owned by other users
- Or root-owned processes

You must be root.

---

# 📊 Understanding the top Output

When you run `top`, the screen is divided into two parts:

---

## 🔝 Top Section (System Summary)

### 1️⃣ Uptime & Load

Shows:

- System uptime
- Number of users logged in
- Load average (1, 5, 15 minutes)

Example:
`load average: 0.10, 0.20, 0.15`


---

### 2️⃣ Tasks

Shows total processes:

- Running
- Sleeping
- Stopped
- Zombie

🔎 Zombie Process:
A child process whose parent has died but hasn’t been cleaned up.

---

### 3️⃣ CPU Usage

Displays:

- User CPU %
- System CPU %
- Idle %
- I/O wait
- Interrupt usage

---

### 4️⃣ Memory Usage

Shows:

- Total RAM
- Used memory
- Free memory
- Buffers/cache
- Swap usage

---

# 📌 Process Columns Explained

Below the summary section, you see process details.

| Column | Meaning |
|---------|----------|
| PID | Process ID |
| USER | Process owner |
| PR | Priority |
| NI | Nice value |
| VIRT | Virtual memory used |
| RES | Physical RAM used |
| SHR | Shared memory |
| S | Process state |
| %CPU | CPU usage |
| %MEM | Memory usage |
| TIME+ | Total CPU time |
| COMMAND | Process name |

---

## 🔹 Nice Value (NI)

- Negative value → Higher priority
- Positive value → Lower priority

---

## 🔹 Process States (S Column)

| Code | Meaning |
|------|---------|
| R | Running |
| S | Sleeping |
| T | Stopped |
| Z | Zombie |

---

# 🎮 Interactive Controls Inside top

Once inside `top`, you can press keys to perform actions.

---

## 🔹 Show Full Command Path

Press:

`c`

This shows the absolute path of processes.

---

## 🔹 Kill a Process

Press:

`k`

Then:

1. Enter PID
2. Confirm

Example:

Kill process 5216.

If you kill `top` itself, it exits immediately.

---

## 🔹 Sort by Memory Usage

Press:

`Shift + M`

Sorts processes by highest memory usage.

---

## 🔹 Sort by CPU Usage

Press:

`Shift + P`

Sorts processes by highest CPU usage.

---

# 👤 Show Processes for Specific User

View processes for a specific user:

`top -u username`

Example:

`top -u root`

Or:

`top -u abhi`

---

# 🔄 Refresh Rate

By default, `top` refreshes every **3 seconds**.

You can change the refresh rate inside top using:

`d`

Then enter number of seconds.

---

# 🖥 Windows Comparison

In Windows:
- You open Task Manager.

In Linux:
- `top`
- `ps`
- `htop` (advanced version)

`top` is the Linux equivalent of Task Manager.

---

# 🧠 Why top Is Important

You will use `top` for:

- Troubleshooting high CPU usage
- Diagnosing memory leaks
- Identifying runaway processes
- Checking system performance
- Finding processes to kill

Every system administrator uses `top` daily.

---

# 🎯 Key Takeaway

- `top` provides real-time system monitoring.
- It is interactive.
- You can sort, filter, and kill processes.
- Essential for performance troubleshooting.

---

**✍️ Notes By Abhishek (Ez Abyss)**
