# 🔪 kill Command in Linux (Terminate Processes)

The `kill` command is used to **terminate processes manually**.

It sends a **signal** to a process, instructing it what to do.

---

# 📌 Why Do We Need kill?

Normally, you stop services using:

`systemctl stop service_name`

But sometimes:

- A service refuses to stop
- A process becomes unresponsive
- A process consumes high CPU/memory

In those cases, `kill` helps.

---

# 🧩 Basic Syntax

`kill [signal] PID`

Where:

- **signal** → Tells the process what action to take
- **PID** → Process ID

You must know the PID before killing a process.

---

# 🔎 How to Find PID?

You can find PID using:

`ps -ef`

or

`top`

Example:

`ps -ef | grep firewalld`

---

# 🔔 Default Behavior

If you run:

`kill PID`

It sends:

`SIGTERM (15)`

This attempts to terminate the process **gracefully**.

---

# 📜 View All Available Signals

To list signals:

`kill -l`

You will see many signal numbers and names.

Signals instruct the process how to behave.

---

# 🔥 Commonly Used Signals

| Signal | Meaning |
|--------|----------|
| 1 (SIGHUP) | Restart process |
| 2 (SIGINT) | Interrupt (like Ctrl+C) |
| 9 (SIGKILL) | Force kill |
| 15 (SIGTERM) | Graceful termination |

---

# 🛑 Graceful Termination

`kill -15 PID`

Or simply:

`kill PID`

This allows process to clean up before stopping.

---

# 💣 Force Kill

`kill -9 PID`

Used when:

- Process refuses to stop
- Process is stuck
- Graceful termination fails

⚠ Warning:
`kill -9` does not allow cleanup.

Use only when necessary.

---

# 🧪 Practical Example (sleep Command)

Run a test process:

`sleep 50`

Find its PID:

`ps -ef | grep sleep`

Then kill it:

`kill -9 6576`

The process ends immediately.

---

# 🔄 Restart Using Signal 1

`kill -1 PID`

This sends a restart signal (SIGHUP).

Often used to reload services.

---

# 🔹 Killing a Service Example

Check service status:

`systemctl status firewalld`

Note PID.

Then:

`kill PID`

Or:

`kill -9 PID`

Verify:

`systemctl status firewalld`

---

# 🔧 Other Related Commands

## Kill by Process Name

`pkill process_name`

Example:

`pkill sleep`

---

## Kill All Matching Processes

`killall process_name`

Kills all processes with that name.

Example:

`killall firefox`

---

# 🖥 Windows Comparison

In Windows:

- Open Task Manager
- Right-click process
- Click “End Task”

In Linux:

- `kill`
- `pkill`
- `killall`

Same concept — different interface.

---

# 🧠 Key Differences Between kill, pkill, killall

| Command | How It Works |
|----------|--------------|
| kill | Uses PID |
| pkill | Uses process name |
| killall | Kills all processes by name |

---

# 🎯 Best Practice

1. Try normal kill first:
   `kill PID`

2. If it fails:
   `kill -9 PID`

3. Avoid overusing `-9`

---

# 🧠 Key Takeaway

- `kill` sends signals to processes.
- Signals control how process behaves.
- `kill -9` is force kill.
- Always try graceful termination first.
- Essential tool for troubleshooting.

---

**✍️ Notes By Abhishek (Ez Abyss)**
