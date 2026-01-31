# 🧭 Navigating the Linux File System (cd, pwd, ls)

> the next critical skill is learning **how to move inside it**.

Without navigation commands, Linux is unusable.

---

## 🎯 Goal of This Lesson
Learn how to:
- Move between directories
- Know where you are
- View directory contents

Linux does **not** use mouse clicks — everything is done through commands.

---

## 🧠 The 3 MOST IMPORTANT Navigation Commands

| Command | Full Form | Purpose |
|------|---------|--------|
| `cd` | Change Directory | Move from one directory to another |
| `pwd` | Print Working Directory | Show current directory |
| `ls` | List | Show files and folders |

📌 **Master these three and you can navigate anywhere in Linux.**

---

## 🪟 Windows vs 🐧 Linux (Key Comparison)

### Windows (GUI)
- Double-click folder → move inside
- Folder opens → contents listed automatically
- Address bar → shows current location

👉 Windows does **3 actions at once**

### Linux (CLI)
You must do **each action manually**:
1. Move → `cd`
2. Check location → `pwd`
3. View contents → `ls`

📌 Linux makes you **explicit**, not automatic.

---

## 👤 Who Am I Logged In As?

Check current user:
- `whoami`

Become root user:
- `su -`

Clear the screen:
- `clear`

📌 Root user’s home directory is `/root`.

---

## 📍 Where Am I Right Now?

Use:
- `pwd`

Example output:
- `/root`
- `/boot`
- `/etc/sysconfig`

📌 Always use `pwd` when you feel lost.

---

## 📂 Moving Between Directories (`cd`)

### Go to root of filesystem:
- `cd /`

Check location:
- `pwd`

Output:
- `/`

---

### Go into a directory (example: `/boot`)
- `cd boot`

Confirm:
- `pwd`

Output:
- `/boot`

---

## 📜 Listing Directory Contents (`ls`)

List contents:
- `ls`

Detailed listing:
- `ls -l`

📌 In `ls -l` output:
- Starts with `d` → directory
- Starts with `-` → file

---

## 🔙 Moving Back (Very Important)

### Go back **one level**
- `cd ..`

### Go back **multiple levels**
- `cd ..`
- `cd ..`

### Go directly to root
- `cd /`

📌 `..` means **parent directory**

---

## 🏠 What Happens If You Just Type `cd`?

Run:
- `cd`

Check:
- `pwd`

Result:
- `/root` (if logged in as root)
- `/home/username` (for normal users)

📌 `cd` with no arguments = go to **home directory**

---

## 📁 Navigating Multiple Levels

Example:
- `cd /etc/sysconfig`

Check:
- `pwd`

Output:
- `/etc/sysconfig`

Go back:
- `cd ..` → `/etc`
- `cd ..` → `/`

---

## 🧪 Real Navigation Example (Hands-On)

1. Go to root:
   - `cd /`

2. List directories:
   - `ls -l`

3. Go to logs:
   - `cd var`
   - `cd log`

4. View logs:
   - `ls -l`

5. Lost?
   - `pwd`

6. Go back to root:
   - `cd /`

---

## 🧠 Memory Shortcut

| Action | Command |
|------|--------|
| Move | `cd` |
| Check location | `pwd` |
| See contents | `ls -l` |
| Go back | `cd ..` |
| Go home | `cd` |
| Go root | `cd /` |

---

## 📝 Homework

1. `cd /`
2. `ls -l`
3. Enter **each directory one by one**
4. Use `pwd` to confirm location
5. Use `cd ..` to come back
6. Repeat until navigation feels natural

📌 **Linux confidence comes from repetition.**

---

## ✅ Summary

> Navigating Linux requires mastering `cd`, `pwd`, and `ls` — without them, nothing else works.

---

**✍️ Notes By Abhishek (Ez Abyss)**
