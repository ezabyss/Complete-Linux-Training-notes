# ⚙️ Linux Process Management 

---

# 🎯 What is Process Management?

Process Management = Controlling how programs run in Linux.

It includes:

- Starting a process
- Stopping a process
- Running in background
- Bringing to foreground
- Running after terminal closes
- Killing processes
- Setting priority
- Monitoring processes

---

# 🧠 Core Concept

When you run a command in terminal:

`command`

It runs in the **foreground** by default.

That means:
- You DO NOT get your prompt back
- Terminal is attached to that process
- Closing terminal kills the process

---

# 🔄 Foreground vs Background

| Mode | What Happens |
|------|--------------|
| Foreground | Terminal is occupied |
| Background | Terminal is free |

---

# 🔹 Running Process in Background (Step-by-Step)

Example:

`sleep 100`

You won’t get your prompt back.

### Step 1 – Stop the Process

Press:

`Ctrl + Z`

This suspends the process.

---

### Step 2 – Check Suspended Jobs

`jobs`

Output shows stopped processes.

---

### Step 3 – Send to Background

`bg`

Now process runs in background.

Check again:

`jobs`

You’ll see status as **Running**

---

# 🔁 Bring Process Back to Foreground

If process is running in background:

`fg`

Now it becomes active in terminal again.

You won’t get prompt until it finishes.

---

# 🧪 Example Using sleep Command

`sleep 5`

Waits 5 seconds.

`sleep 100`

Runs for 100 seconds.

Used only for demonstration of process control.

---

# 🛑 Stop vs Kill

- `Ctrl + Z` → Suspend (temporary stop)
- `Ctrl + C` → Kill immediately

---

# 🚪 What Happens If You Close Terminal?

If process is attached to terminal:

It dies when terminal closes.

---

# 🚀 Run Process Even After Terminal Closes (nohup)

## Basic Syntax

`nohup command &`

Example:

`nohup sleep 75 &`

Now:
- Process runs in background
- Not attached to terminal
- Survives logout

---

## Why `&` ?

The `&` sends process to background immediately.

---

# 📄 What is nohup.out?

Whenever you run `nohup`, it creates:

`nohup.out`

It stores:
- Output
- Error messages
- Warnings

---

# 🗑 Suppress All Output (Clean Execution)

If you don’t want messages:

`nohup sleep 73 > /dev/null 2>&1 &`

### Breakdown:

| Part | Meaning |
|------|---------|
| `>` | Redirect output |
| `/dev/null` | Discard output |
| `2>&1` | Redirect errors to same place |
| `&` | Background |

Result:
- No messages shown
- No nohup.out clutter

---

# 🔎 View Running Processes

## Method 1

`jobs`

Shows background jobs of current session only.

---

## Method 2

`ps -ef`

Shows ALL system processes.

Filter example:

`ps -ef | grep sleep`

---

# 💀 Kill Process

## Kill by PID

`kill PID`

Example:

`kill 1234`

---

## Kill by Name

`pkill process_name`

Example:

`pkill top`

Kills all processes named "top"

---

# 🎯 Process Priority (Nice)

Linux priority scale:

-20  → Highest Priority  
19   → Lowest Priority  

Lower number = Higher priority

---

## Run Process with Priority

`nice -n 5 sleep 10`

This tells CPU:

> Give priority level 5 to this process.

---

## Highest Priority Example

`nice -n -20 command`

⚠ Only root can assign negative priorities.

---

# 🧠 Why Priority Matters?

CPU can process only one task per core at a time.

Imagine juggling balls:
- Each ball = process
- Your hand = CPU

`nice` tells CPU:

> This ball is more important. Hold it more often.

---

# 📊 Monitor System in Real Time

`top`

Shows:
- CPU usage
- Memory usage
- Running processes
- Load average

Press `q` to exit.

---

# 🧠 Memory Anchors

Remember these 7 truths:

1. Default process runs in foreground
2. `Ctrl + Z` suspends
3. `bg` sends to background
4. `fg` brings to foreground
5. `nohup` detaches from terminal
6. `pkill` kills by name
7. `nice` range = -20 to 19

---

# 🏗 Process Lifecycle Map

Run Command  
↓  
Foreground  
↓  
`Ctrl + Z`  
↓  
Stopped  
↓  
`bg`  
↓  
Background  
↓  
`fg`  
↓  
Foreground Again  

---

# 🏁 Final Takeaway

Process management gives you:

- Control
- Efficiency
- System stability
- Production-level flexibility

Mastering this = Thinking like a Linux System Engineer.

---

**✍️ Notes By Abhishek (Ez Abyss)**
