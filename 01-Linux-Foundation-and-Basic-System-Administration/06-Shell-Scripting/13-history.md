# 📜 Linux Shell History
### Track, Reuse & Investigate Commands

---

# 🎯 Why History is Important

Every command you run in Linux is **recorded**.

This helps you:

- 🔍 troubleshoot issues
- 🔁 reuse commands
- 🧠 learn faster
- 🔐 audit user activity

---

# 📌 What is Shell History?

Shell history is a **log of commands** executed by a user.

Stored automatically by the system.

---

# 🧠 Simple Explanation

When you run:

`ls`

Linux remembers it.

Later you can:

- view it
- search it
- rerun it

---

# 🌍 Real World Scenario

A server crashed.

You need to find:

- ❓ who ran a risky command
- ❓ what deleted a file
- ❓ what caused the issue

👉 Use:

`history`

---

# 🧪 Basic Usage

## View history

`history`

---

## Paginated view

`history | more`

---

# 🔍 Search in History

## Find commands with keyword

`history | grep awk`

---

## Example

`history | grep chmod`

Shows all `chmod` commands used before.

---

# 🔁 Re-run Commands

## Run by number

Example:

`!406`

Runs command number 406.

---

## Run last command

`!!`

---

## Run last command starting with word

`!ls`

Runs last command starting with `ls`.

---

# 🧠 Example Workflow


`history`

Output:

```
405 ls
406 last | awk '{print $1}' | sort | uniq
```

Run again:

`!406`

---

# ⚡ Productivity Trick

Instead of typing long command:

`last | awk '{print $1}' | sort | uniq`

Just use:

`!406`

---

# 📂 Where History is Stored

File:

`~/.bash_history`

---

# ⚙️ History Configuration

## Number of commands stored

Check:

`echo $HISTSIZE`

---

## Change history size

`export HISTSIZE=2000`


---

# 🧹 Clear History

## Clear current session

`history -c`

---

## Clear file

`> ~/.bash_history`

---

# ⚠️ Important Notes

| Behavior | Explanation |
|--------|-----------|
| Stores failed commands | yes |
| Per user history | yes |
| Session-based update | yes |
| Not always real-time saved | yes |

---

# 🧠 Security Insight

History can expose:

- passwords (if typed incorrectly)
- sensitive commands

👉 Be careful when typing secrets.

---

# 🧠 Quick Questions

### What is history command?

Displays previously executed commands.

---

### How to rerun a command?

`!number`

---

### Where is history stored?

`~/.bash_history`

---

### How to search history?

`history | grep keyword`

---

# 🏁 Key Takeaways

- History records all commands
- Helps in debugging & auditing
- Speeds up workflow
- Allows command reuse
- Essential tool for sysadmins

---

# 🚀 Pro Tip

Use reverse search:

Press:

`Ctrl + R`

Then type:

`ssh`

👉 It finds previous `ssh` commands instantly.

---

# 💥 Advanced Tip

Ignore commands from history:

`export HISTCONTROL=ignoredups`


---

**✍️ Notes By Abhishek (Ez Abyss)**
