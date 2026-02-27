# 🕒 at Command in Linux (One-Time Scheduler)

The `at` command is similar to `crontab`, but with one key difference:

👉 `at` schedules a task **only once**.

`crontab` = recurring tasks  
`at` = one-time task

---

# 📌 Basic Usage

Schedule a job:

`at time`

After pressing Enter, you enter **interactive mode**.

Type your command(s), then press:

`Ctrl + D`

to finish.

---

# 🧩 Example: Schedule a Job for 1:28 AM

First, check current time:

`date`

If current time is 1:25 AM, schedule:

`at 1:28 AM`

After pressing Enter:
`echo "This is my first at entry" > at_entry`


Then press:

`Ctrl + D`

---

# 📋 Check Scheduled Jobs

To list scheduled jobs:

`atq`

Example output:
`4 Sat Feb 28 01:30:00 2026 a ezabyss`


Each job is assigned a **job number**.

---

# 🗑 Remove Scheduled Job

To remove a job:

`atrm job_number`

Example:

`atrm 4`

Then verify:

`atq`

Job is removed.

---

# 🧠 Check at Daemon

The service managing `at` is called:

`atd`

Check status:

`systemctl status atd`

If `atd` is stopped:

- You can still create entries
- But they will NOT execute

---

# 🧪 Practical Demo

Schedule two jobs:

`at 1:31 AM`
`echo "World" > file1`


`Ctrl + D`

Then:

`at 4:00 AM`
`echo "Hello World" > file2`


Check jobs:

`atq`

You will see:

- Job 4
- Job 5

Remove job 5:

`atrm 5`

Check again:

`atq`

Only job 4 remains.

---

# 📅 Flexible Time Scheduling

One powerful feature of `at` is its natural language understanding.

You can schedule like this:

Run on October 16 at 2:45 AM:

`at 2:45 AM 02/28/2026`

Run 4 days from now:

`at 4 PM + 4 days`

Run 5 hours from now:

`at now + 5 hours`

Run next Sunday at 8 AM:

`at 8 AM next Sunday`

Run at 10 AM next month:

`at 10 AM next month`

`at` understands natural time expressions.

---

# 🔄 Difference Between at and crontab

| Feature | at | crontab |
|----------|------|-----------|
| Runs once | ✅ | ❌ |
| Recurring | ❌ | ✅ |
| Uses table format | ❌ | ✅ |
| Natural language scheduling | ✅ | ❌ |

---

# 🎯 When to Use at?

Use `at` when:

- You need to run something one time only
- Temporary scheduling
- Quick future execution
- Maintenance tasks

---

# 🧠 Key Takeaway

- `at` schedules one-time jobs.
- Uses natural time format.
- Managed by `atd` daemon.
- Use `atq` to list jobs.
- Use `atrm` to remove jobs.

Very useful for quick, temporary scheduling.

---

**✍️ Notes By Abhishek (Ez Abyss)**



