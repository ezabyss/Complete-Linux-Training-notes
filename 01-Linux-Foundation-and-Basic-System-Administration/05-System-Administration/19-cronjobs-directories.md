# 🕒 Linux Cron Jobs – System Default Scheduling 

---

## 🎯 Big Picture First

In Linux, tasks can be scheduled in **two main ways**:

| Tool | Purpose | Type |
|------|---------|------|
| `at` | One-time task | Ad hoc |
| `cron` | Repetitive tasks | Scheduled |

If you need:

- ✅ One-time execution → Use `at`
- ✅ Repeated execution → Use `cron`

---

# 🧠 Hidden Power: Built-in Cron Directories

Linux already provides built-in scheduling directories.

You do NOT always need `crontab -e`.

Out of the box, Linux provides:

- `/etc/cron.hourly`
- `/etc/cron.daily`
- `/etc/cron.weekly`
- `/etc/cron.monthly`

Any executable script placed inside these folders will automatically run based on system schedule.

---

# 📂 Where They Live

Go to:

`cd /etc`

List cron directories:

`ls -l | grep cron`

Or:

`ls -l cron.*`

You will see:

- `cron.hourly`
- `cron.daily`
- `cron.weekly`
- `cron.monthly`
- `crontab`

---

# ⚙️ Two Ways to Schedule Recurring Jobs

## 🔹 Method 1 — Use `crontab -e`

Edit user cron table:

`crontab -e`

Example format:

    * * * * * /path/to/script.sh

( Minute | Hour | Day | Month | Weekday )

---

## 🔹 Method 2 — Drop Script Into System Folder (Cleaner Method)

Instead of editing crontab:

1. Move script into correct directory:

    /etc/cron.hourly/
    /etc/cron.daily/
    /etc/cron.weekly/
    /etc/cron.monthly/

2. Make it executable:

`chmod +x script.sh`

3. Done ✅

No need to edit `crontab`.

---

# 📌 Example Walkthrough

## 🔹 Check Daily Jobs

`cd /etc/cron.daily`

`ls -l`

To add a daily job:

    mv backup.sh /etc/cron.daily/

---

## 🔹 Add Hourly Job

`cd /etc/cron.hourly`

Move your script:

    mv monitor.sh /etc/cron.hourly/

It will now run every hour automatically.

---

# ⏰ When Do These Run?

## 🗂 Daily, Weekly, Monthly → Controlled by Anacron

View schedule:

`cat /etc/anacrontab`

Example structure:

    1   5   cron.daily
    7   25  cron.weekly
    @monthly 45 cron.monthly

### Field Meaning

| Field | Meaning |
|-------|---------|
| Period (days) | How often it runs |
| Delay (minutes) | Delay after boot |
| Job Identifier | Name |
| Command | What gets executed |

Example:

`1 5 cron.daily`

Means:
- Every 1 day
- Wait 5 minutes after boot
- Execute cron.daily scripts

---

# 🧨 Hourly Is Different

Hourly jobs are NOT controlled by `anacrontab`.

They are defined in:

    /etc/cron.d/0hourly

View it:

`cat /etc/cron.d/0hourly`

Example:

    01 * * * * root run-parts /etc/cron.hourly

### Meaning:

`01 * * * *`

| Field | Meaning |
|-------|---------|
| 01 | Minute 1 |
| * | Every hour |
| * | Every day |
| * | Every month |
| * | Every weekday |

So hourly scripts run at:

- 12:01
- 1:01
- 2:01
- 3:01
- Every hour at minute 01

---

# 🔎 Internal Execution Flow

Your Script  
→ Placed inside `/etc/cron.daily`  
→ Triggered by `anacron`  
→ `run-parts` executes all scripts in that directory  

---

# 🧠 Memory Anchors 

Remember these 5 truths:

1. `at` = one-time job  
2. `cron` = recurring job  
3. Built-in directories exist  
4. Daily/Weekly/Monthly → `/etc/anacrontab`  
5. Hourly → `/etc/cron.d/0hourly`  

---

# 📊 Final System Map

| Frequency | Directory | Timing Defined In |
|------------|------------|------------------|
| Hourly | `/etc/cron.hourly` | `/etc/cron.d/0hourly` |
| Daily | `/etc/cron.daily` | `/etc/anacrontab` |
| Weekly | `/etc/cron.weekly` | `/etc/anacrontab` |
| Monthly | `/etc/cron.monthly` | `/etc/anacrontab` |

---

# 🏁 Final Takeaway

You do NOT always need `crontab -e`.

Linux already provides a structured, production-ready scheduling system.

Drop your executable script in the right directory — and let the OS handle the rest.

---

**✍️ Notes By Abhishek (Ez Abyss)**
