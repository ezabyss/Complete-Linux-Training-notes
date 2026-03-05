# 🖥️ Linux `tmux` Command
### Modern Terminal Multiplexer for System Administrators

---

# 🎯 Why `tmux`

`tmux` helps you:

- Manage multiple terminal sessions
- Run long tasks safely
- Continue processes after SSH disconnects
- Split your terminal into multiple panes
- Work on several tasks simultaneously

It is widely used by **system administrators, DevOps engineers, and developers**.

---

# 📌 What is `tmux`?

`tmux` stands for **Terminal Multiplexer**.

It allows you to:

- Run **multiple terminal sessions inside one window**
- Split terminal into **multiple panes**
- Detach sessions and reconnect later
- Manage tasks on remote servers efficiently

Think of it as **a workspace manager for your terminal**.

---

# 🧠 Mental Model

Without `tmux`:


SSH → Run Command → Connection Lost → Process Stops


With `tmux`:

```
SSH → Start tmux → Run Command → Connection Lost
↓
Process Keeps Running
↓
Reconnect With tmux attach
```

---

# 🌍 Real World Scenario

Imagine you are:

- Deploying a production server
- Running database migration
- Uploading a **50GB backup**
- Monitoring logs during deployment

Command running:

`rsync -av backup.tar server:/backup`

Suddenly:

- VPN disconnects
- WiFi drops
- Laptop shuts down

Without `tmux` → process stops ❌  
With `tmux` → process continues running ✅

You reconnect later and resume work.

---

# 🕰️ Brief History

| Year | Event |
|-----|------|
| 2007 | `tmux` created by Nicholas Marriott |
| 2009 | First stable release (tmux 1.0) |
| 2019 | tmux 3.0 added plugins & improvements |
| Today | Most popular terminal multiplexer |

It was designed to be a **modern replacement for `screen`**.

---

# 🔎 Check if `tmux` is Installed

Run:

`rpm -qa | grep tmux`

If installed you will see:

`tmux-x.x.x`

If not installed, install it.

---

# 📦 Installing `tmux`

Install using:

`dnf install tmux -y`

Verify installation:

`tmux -V`

---

# 🚀 Starting a `tmux` Session

Run:

`tmux`

You will see a **status bar at the bottom**.

Example:

`[0] bash`


Meaning:

- `0` → window number
- `bash` → shell running in that window

---

# 📊 Basic `tmux` Shortcuts

| Action | Shortcut |
|------|------|
| Create new window | `Ctrl + B` then `C` |
| Switch window | `Ctrl + B` then `N` |
| Split vertically | `Ctrl + B` then `%` |
| Split horizontally | `Ctrl + B` then `"` |
| Detach session | `Ctrl + B` then `D` |
| Rename window | `Ctrl + B` then `,` |

---

# 🪟 Splitting Windows

`tmux` allows multiple panes in one terminal.

---

## Vertical Split

Press:

`Ctrl + B` then `%`

Result:

`| Pane 1 | Pane 2 |`


You now have **two side-by-side terminals**.

---

## Horizontal Split

Press:

`Ctrl + B` then `"`

Result:

```
Pane 1

Pane 2
```

You now have **stacked terminals**.

---

# 🔄 Switching Between Panes

Press:

`Ctrl + B` then arrow keys

Examples:

- `Ctrl + B` then `←`
- `Ctrl + B` then `→`
- `Ctrl + B` then `↑`
- `Ctrl + B` then `↓`

---

# 🧪 Example: Run Command in tmux

Start tmux:

`tmux`

Split terminal:

`Ctrl + B` then `%`

Run command:

`ping google.com`

The bottom bar will show:


`[0] ping*`


This indicates the command is running.

---

# 🔌 Detaching a Session

Press:

`Ctrl + B` then `D`

Your session detaches.

Output:


`[detached]`


Your processes **continue running in the background**.

---

# 🔍 List Active Sessions

Run:

`tmux ls`

Example output:


`0: 1 windows (created Tue 12:00)`


This means session **0 is running**.

---

# 🔁 Reattach to Session

Run:

`tmux attach`

or

`tmux a`

You return to your previous session.

---

# 🏷️ Create Named Session

Creating named sessions is a **best practice**.

Example:

`tmux new -s deploy`

Session name:

`deploy`

---

# 🔁 Attach Named Session

`tmux attach -t deploy`

This reconnects to the **deploy session**.

---

# 🪟 Creating Multiple Windows

Inside tmux press:

`Ctrl + B` then `C`

This creates a **new window**.

Example:

```
Window 0 → bash
Window 1 → logs
Window 2 → monitoring
```

Switch windows using:

`Ctrl + B` then `N`

---

# ❌ Closing a Window

Press:

`Ctrl + D`

or type:

`exit`

The window closes.

---

# 🧹 Killing a Session

List sessions:

`tmux ls`

Kill session:

`tmux kill-session -t session_name`

Example:

`tmux kill-session -t deploy`

---

# 📊 Key `tmux` Commands

| Command | Purpose |
|------|------|
| `tmux` | Start tmux |
| `tmux ls` | List sessions |
| `tmux attach` | Reconnect session |
| `tmux new -s name` | Create named session |
| `tmux kill-session -t name` | Terminate session |

---

# 🧠 Pro Tip (Top Sysadmin Workflow)

Always create named sessions:

`tmux new -s server-maintenance`

Inside tmux:

```
- Pane 1 → system logs
- Pane 2 → deployment script
- Pane 3 → monitoring
```

This creates a **powerful server management workspace**.

---

# 🧠 Questions

### What is `tmux`?

A terminal multiplexer that allows multiple terminal sessions in one window.

---

### Why use `tmux`?

To keep processes running even if SSH disconnects.

---

### How to list sessions?

`tmux ls`

---

### How to reconnect to a session?

`tmux attach`

---

# 🏁 Key Takeaways

`tmux` allows you to:

- Manage multiple terminals
- Run tasks safely
- Reconnect after disconnect
- Improve productivity on remote servers

It is one of the **most powerful Linux tools for remote system management**.

---

**✍️ Notes By Abhishek (Ez Abyss)**
