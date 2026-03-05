# 🖥️ Linux `screen` Command
### Terminal Multiplexing for System Administrators

---

# 🎯 Why

`screen` command to:

- Manage multiple terminal sessions
- Prevent task interruption
- Resume work after connection loss
- Run long processes safely

This is a **must-know tool for system administrators and engineers** working on remote Linux servers.

---

# 📌 What is the `screen` Command?

The `screen` command (GNU Screen) is a **terminal multiplexer**.

It allows you to:

- Run **multiple terminal sessions inside one terminal**
- Keep tasks running **even after SSH disconnects**
- Resume sessions later

---

# 🧠 Simple Explanation

Normally when you SSH into a server:

`ssh root@server-ip`

If your connection drops:

- The terminal closes
- Your running command stops
- Your work is lost

But if you run your task inside `screen`:

`screen`

Your process **continues running in the background** even if your connection drops.

You can reconnect later and resume your work.

---

# 🧠 Mental Model

Without `screen`:

`
SSH Session → Command Running → Connection Lost → Process Stops
`

With `screen`:

```
SSH Session → Start Screen → Run Command → Connection Lost
↓
Process Continues Running
↓
Reconnect Later With screen -r
```

---
# 🌍 Real World Scenario

Imagine you are:

- Transferring a **50GB backup file**
- Running a **database migration**
- Compiling software that takes **2 hours**

You start the task via SSH:


`scp bigfile.tar server:/backup`


Suddenly:

- VPN disconnects
- WiFi drops
- Laptop shuts down

Without `screen`, the process **stops**.

With `screen`, the process **continues running safely**.

You reconnect and resume the session.

---

# 🕰️ Brief History

| Year | Event |
|-----|------|
| 1980s | GNU Screen developed |
| 1990s | Became standard Unix tool |
| 2000s | Popular for remote server work |
| Today | Still widely used by sysadmins |

---

# 🔎 Check if `screen` is Installed

Run:

`rpm -qa | grep screen`

If installed you will see:

`screen-4.x.x`

If not installed, install it.

---

# 📦 Installing `screen`

Sometimes `screen` requires the **EPEL repository**.

Install EPEL:

`dnf install epel-release`

Then install screen:

`dnf install screen`

Verify installation:

`screen --version`

---

# 🚀 Starting a Screen Session

Run:

`screen`

This creates your **first screen session**.

Example session name:

`screen-0`

Each new session gets its own number.

---

# 🧭 Screen Navigation Basics

| Action | Shortcut |
|------|------|
| Create new window | `Ctrl + A` then `C` |
| Switch window | `Ctrl + A` then `Tab` |
| Detach session | `Ctrl + A` then `D` |
| List sessions | `screen -ls` |
| Reattach session | `screen -r` |

---

# 🧪 Example: Start a Screen Session

Start screen:

`screen`

Run a long process:

`ping google.com`

Detach from session:

`Ctrl + A` then `D`

Your process **continues running in background**.

---

# 🔍 List Running Screen Sessions

Run:

`screen -ls`

Example output:

`
There are screens on:
1234.pts-0.server (Detached)
`

Meaning:

- Screen session exists
- It is running in background

---

# 🔁 Reconnect to Screen Session

Run:

`screen -r`

You reconnect to your previous session.

Your process is still running.

---

# 🧪 Practical Lab Example

### Step 1 — Start screen

`screen`

---

### Step 2 — Run long command

`ping google.com`

---

### Step 3 — Detach screen

Press:

`Ctrl + A` then `D`

Output:

`
[detached]
`

---

### Step 4 — List sessions

`screen -ls`

---

### Step 5 — Reattach session

`screen -r`

You return to the running process.

---

# 🪟 Splitting Screen Windows

Screen allows multiple terminal views.

---

## Vertical Split

Press:

`Ctrl + A` then `|`

This splits the screen **vertically**.

---

## Horizontal Split

Press:

`Ctrl + A` then `Shift + S`

This splits the screen **horizontally**.

---

# 🔄 Switch Between Windows

Press:

`Ctrl + A` then `Tab`

This moves focus between sections.

---

# 🌐 Running Multiple Servers in One Screen

Example workflow:

Terminal 1:

`ssh root@192.168.1.10`

Terminal 2:

`ssh root@192.168.1.11`

Terminal 3:

`ssh root@192.168.1.12`

All inside **one screen session**.

Perfect for system administrators managing multiple servers.

---

# 🔄 Recovering Lost Work

If terminal closes unexpectedly:

Reconnect via SSH.

Then run:

`screen -r`

Your previous session returns exactly where you left off.

---

# 📊 Key Screen Commands

| Command | Purpose |
|------|------|
| `screen` | Start screen |
| `screen -ls` | List sessions |
| `screen -r` | Resume session |
| `screen -S name` | Create named session |
| `screen -X -S name quit` | Kill session |

---

# 🧠 Pro Tip

Always name your screen sessions:

`screen -S backup`

Later reconnect with:

`screen -r backup`

This helps manage multiple sessions.

---

# 🧠 Questions

### What is `screen`?

A terminal multiplexer used to manage multiple terminal sessions.

---

### Why is `screen` useful?

It allows processes to **continue running even after SSH disconnects**.

---

### How do you reconnect to a session?

`screen -r`

---

### How do you see running sessions?

`screen -ls`

---

# 🏁 Key Takeaways

The `screen` command helps you:

- Run long tasks safely
- Avoid losing work
- Manage multiple terminals
- Resume sessions after disconnect

It is one of the **most useful Linux tools for remote server management**.

---

**✍️ Notes By Abhishek (Ez Abyss)**
