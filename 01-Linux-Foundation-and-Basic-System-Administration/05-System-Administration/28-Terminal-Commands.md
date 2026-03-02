# 🖥️ Linux Terminal Utility Commands

---

# 🎯 Why These Commands Matter

Terminal utility commands help you:

- Manage your session
- Keep your screen clean
- Exit safely from shells
- Record your work
- Improve productivity

Small commands. Big efficiency.

---

# 🧠 Core Terminal Utility Commands

| Command | Purpose |
|----------|----------|
| `clear` | Clear terminal screen |
| `exit` | Exit shell/session |
| `script` | Record terminal session |

---

# 🔥 1. `clear` – Clean Your Screen

When you run many commands:

`ls -ltr`  
`pwd`  
`history`  

Your screen gets cluttered.

Instead of scrolling:

`clear`

Clears the entire terminal display.

---

### Pro Tip

Many scripts begin with:

`clear`

So output starts fresh and clean.

---

# 🚪 2. `exit` – Exit Shell or Session

Used to:

- Exit current shell
- Exit from `su` user
- Close terminal
- End `script` recording
- Log out of SSH

---

## Example: Switch User

Switch user:

`su spider`

Now you are logged in as spider.

To return to original user:

`exit`

---

## Example: Close Terminal

Simply type:

`exit`

Terminal session ends.

---

# 🧠 How exit Works

Each `su` creates a new shell layer.

`exit` removes one shell layer at a time.

Think of it like:

Stack layers → `exit` removes one layer.

---

# 📜 3. `script` – Record Everything in Terminal

One of the most powerful but underrated commands.

---

## Start Recording

`script log-activity.log`

If no filename provided:

`script`

Default file name:

`typescript`

---

## What Happens?

- Every command you run
- Every output displayed
- All terminal activity

Gets saved in the log file.

---

## Example Workflow

Start recording:

`script session.log`

Run commands:

`pwd`  
`ls -ltr`  
`cd /etc`  
`clear`

Everything is recorded.

---

## Stop Recording

`exit`

Output:

Script done, file is session.log

Recording stops.

---

# 📂 View Recorded Session

`more session.log`

You will see:

- Commands typed
- Output of each command
- Timestamps

---

# 🧠 Why script is Extremely Useful

Used for:

- Troubleshooting documentation
- Lab exercises
- Creating training material
- Auditing activity
- Repeating tasks later
- Change tracking

---

# 📈 Notice File Growth

While script is running:

`ls -ltr`

You’ll see the log file size increasing.

It keeps recording until `exit`.

---

# 🧠 Real-World Use Case

Scenario:

You are troubleshooting production issue.

Start:

`script troubleshooting.log`

Perform investigation.

Later:

You have full record of what you did.

Professional admins use this often.

---

# 🎓 Rapid-Fire Answers

### ❓ How do you clear terminal?
`clear`

### ❓ How do you exit a shell?
`exit`

### ❓ How do you record terminal session?
`script filename`

### ❓ What is default script filename?
`typescript`

---

# 🏗 Productivity Mindset

Beginner:

Scrolls up to check previous commands.

Professional:

Uses `script` to log everything.

---

# 🏁 Final Takeaway

Memorize these:

`clear`  
`exit`  
`script`

They improve:

- Organization
- Documentation
- Professional workflow

Terminal mastery is not about knowing many commands.

It’s about using small commands efficiently.

---

**✍️ Notes By Abhishek (Ez Abyss)**
