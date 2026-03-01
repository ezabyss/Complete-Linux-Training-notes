# 🔧 Linux System Maintenance Commands

---

# 🎯 What Are System Maintenance Commands?

System maintenance commands are used by system administrators to:

- Reboot the system
- Shut down the system
- Power off the system
- Change run levels
- Switch to single-user mode
- Perform maintenance while users are logged in

These commands directly affect system availability.

⚠ Use carefully in production environments.

---

# 🧠 Most Important Rule Before Rebooting

Always confirm:

`hostname`

Why?

You must ensure you are on the correct server before rebooting.

Accidentally rebooting production = Career risk.

---

# 🚀 Core System Maintenance Commands

| Command | Purpose |
|----------|----------|
| `shutdown` | Controlled system shutdown |
| `init` | Change runlevel |
| `reboot` | Restart system |
| `halt` | Stop system immediately |
| `poweroff` | Power off machine |

---

# 🔥 1. shutdown – Safe & Controlled Shutdown

View options:

`man shutdown`

---

## Basic Usage

Shut down immediately:

`shutdown now`

Reboot immediately:

`shutdown -r now`

Power off:

`shutdown -h now`

---

## Schedule Shutdown

Shutdown in 10 minutes:

`shutdown +10`

Cancel scheduled shutdown:

`shutdown -c`

---

### Important Options

| Option | Meaning |
|--------|----------|
| `-r` | Reboot |
| `-h` | Halt/Power off |
| `-P` | Power off |
| `-c` | Cancel |

---

# 🧠 Why Use shutdown?

It:

- Notifies logged-in users
- Gracefully stops services
- Allows processes to close safely
- Prevents corruption

---

# 🔄 2. init – Change Run Levels

Older Linux systems used runlevels (0–6).

Common ones:

| Runlevel | Meaning |
|------------|----------|
| 0 | Shutdown |
| 1 | Single-user mode |
| 3 | Multi-user (CLI) |
| 6 | Reboot |

---

## Example

Reboot:

`init 6`

Shutdown:

`init 0`

Switch to multi-user mode:

`init 3`

---

⚠ Modern systems use `systemctl` instead, but `init` still works in many environments.

---

# 🔁 3. reboot – Simple Restart

`reboot`

Equivalent to:

`shutdown -r now`

Requires root privileges.

---

# ⛔ 4. halt – Immediate Stop

`halt`

Immediately stops system.

⚠ Does NOT always gracefully stop services.

Think of it like:

Holding physical power button.

Use carefully.

---

# ⚡ poweroff – Power Down

`poweroff`

Completely powers off system.

Often safer alternative to `halt`.

---

# 🔐 Root Access Required

To reboot or shut down system:

`su -`

or

`sudo reboot`

---

# 🧠 Safe Reboot Workflow (Professional Practice)

Before rebooting:

1. Confirm hostname → `hostname`
2. Check users logged in → `who`
3. Check running services → `top`
4. Notify users if needed
5. Schedule shutdown → `shutdown -r +5`

---

# 🏗 What Happens During Reboot?

1. Processes stop
2. Services terminate
3. Filesystems unmount
4. System powers down
5. Boot sequence restarts

---

# 🎓 Rapid-Fire Answers

### ❓ How do you safely reboot a Linux system?
`shutdown -r now`

### ❓ How do you cancel a scheduled shutdown?
`shutdown -c`

### ❓ What runlevel reboots system?
6

### ❓ What runlevel shuts down system?
0

### ❓ How do you switch to single-user mode?
`init 1`

---

# 🧠 Single User Mode (Maintenance Mode)

Used for:

- Password reset
- Filesystem repair
- System recovery

Command:

`init 1`

Only root has access.

---

# 🔍 Difference Between Commands

| Command | Graceful? | Immediate? |
|----------|------------|------------|
| `shutdown` | Yes | Can schedule |
| `reboot` | Yes | Immediate |
| `halt` | Not always | Immediate |
| `poweroff` | Yes | Immediate |

---

# 🏁 Final Takeaway

Beginner Admin:

Runs `reboot`.

Professional Admin:

- Checks hostname
- Notifies users
- Uses `shutdown -r`
- Monitors reboot

System maintenance commands = Power tools.

Use with discipline.

---

**✍️ Notes By Abhishek (Ez Abyss)**
