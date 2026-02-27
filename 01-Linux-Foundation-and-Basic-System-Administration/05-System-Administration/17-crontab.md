# ⏰ Crontab Command in Linux (Task Scheduler)

`crontab` is used to **schedule tasks automatically**.

Instead of logging in daily to run the same command, you can schedule it once and let the system handle it.

---

# 📌 What is Cron?

- `cron` → Scheduler
- `crond` → Daemon (service) that runs scheduled tasks
- `crontab` → Table of scheduled jobs

---

# 🧩 Basic Crontab Commands

Edit crontab:

`crontab -e`

List current cron jobs:

`crontab -l`

Remove all cron jobs:

`crontab -r`

---

# 🔧 Check Cron Service Status

Check if cron daemon is running:

`systemctl status crond`

If crond is stopped:

- Jobs will not execute
- Even if entries exist in crontab

---

# 📊 Crontab Entry Format

Each cron entry has **6 fields**:

```
* * * * * command
│ │ │ │ │
│ │ │ │ └── Day of Week (0–7) (Sun=0 or 7)
│ │ │ └──── Month (1–12)
│ │ └────── Day of Month (1–31)
│ └──────── Hour (0–23)
└────────── Minute (0–59)

```


---

# 📌 Columns Explained

| Field | Range | Meaning |
|--------|--------|---------|
| Minute | 0–59 | Minute of execution |
| Hour | 0–23 | Hour (24-hour format) |
| Day of Month | 1–31 | Specific date |
| Month | 1–12 | Month |
| Day of Week | 0–7 | Day (Sun=0 or 7) |
| Command | — | Command to execute |

⚠ Interview Tip:
You should memorize these fields. It’s a common Linux interview question.

---

# 🧪 Example: Schedule a Task

We want to:

Create a file that contains:

"This is my first crontab entry"

---

### Step 1️⃣ Check Current Time

`date`

Suppose current time is:

16:18

We schedule task for:

16:21

---

### Step 2️⃣ Edit Crontab

`crontab -e`

Add entry:

`21 16 * 10 * echo "This is my first crontab entry" > /home/ezabyss/crontab_entry`

Explanation:

- 21 → Minute
- 16 → Hour
- * → Every day
- 10 → October
- * → Every weekday
- echo → Command
- > → Redirect output to file

Save and exit.

---

### Step 3️⃣ Verify Execution

After scheduled time:

`ls -ltr`

You should see:

`crontab_entry`

Check content:

`cat crontab_entry`

Output:

This is my first crontab entry

---

# 📋 View Current Cron Jobs

`crontab -l`

---

# 🗑 Remove All Cron Entries

`crontab -r`

Verify:

`crontab -l`

(No entries)

---

# 🔄 Important Notes

- If you do not specify full path, cron uses default environment.
- It’s best practice to use **absolute paths**.
- Cron does not load your shell environment variables.
- Always test your command manually first.

---

# 🧠 Wildcards in Crontab

| Symbol | Meaning |
|----------|----------|
| * | Every value |
| , | Multiple values |
| - | Range |
| */5 | Every 5 minutes |

Example:

Run every 5 minutes:

`*/5 * * * * command`

---

# 🎯 Real-World Use Cases

- Backups
- Log cleanup
- Script automation
- Monitoring checks
- Report generation

---

# 🧠 Key Takeaway

- `crontab` schedules recurring tasks.
- `crond` must be running.
- Format must be exact.
- Extremely important for automation.
- Frequently asked in interviews.

---

**✍️ Notes By Abhishek (Ez Abyss)**
