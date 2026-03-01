# 📜 Linux Log Monitoring – System Administrator

---

# 🎯 Why Log Monitoring Matters

Think of logs like medical records.

Doctor → Checks your health history  
System Admin → Checks system logs  

Logs tell you:

- What happened?
- When did it happen?
- Who did it?
- Why did it fail?

If you want to work in:

- System Administration
- Linux Engineering
- DevOps
- Security
- SOC

You MUST understand logs.

---

# 📂 Main Log Directory

All system logs are stored in:

`/var/log`

Navigate:

`cd /var/log`

List logs:

`ls -l | more`

---

# 🧠 Key Log Files You Must Know

| Log File | Purpose |
|-----------|----------|
| `boot.log` | System boot activity |
| `cron` | Scheduled job logs |
| `secure` | Login & authentication logs |
| `messages` | General system activity |
| `maillog` | Mail server logs |
| `httpd/` | Apache web server logs |
| `audit/` | Security auditing logs |

---

# 🚀 1. boot.log – Boot Process Log

View:

`more /var/log/boot.log`

Shows:

- Services starting
- Memory initialization
- Boot errors
- Failed services

---

### Important Behavior

When system reboots → `boot.log` gets overwritten.

It records only the latest boot.

---

# ⏰ 2. cron – Scheduled Jobs Log

View:

`more /var/log/cron`

Every cron job entry records:

- Month
- Date
- Time
- Hostname
- Daemon name (crond)
- PID
- User
- Command executed

---

### Example Insight

If scheduled job fails → check:

`/var/log/cron`

---

# 🔐 3. secure – Authentication Log

One of the most important logs.

View:

`more /var/log/secure`

---

### Records:

- Login attempts
- Failed logins
- SSH access
- sudo usage
- Root access
- Source IP address

---

## 🔥 Live Monitoring Login Activity

`tail -f /var/log/secure`

Now open another terminal and attempt login.

You’ll see:

- Failed password attempts
- Successful logins
- Session opened/closed

---

### SOC / Security Interview Tip

If asked:

> How do you detect brute-force attack?

Answer:

`tail -f /var/log/secure`

---

# 📧 4. maillog – Email Server Logs

View:

`more /var/log/maillog`

Records:

- Emails sent
- Emails received
- Sendmail/Postfix activity
- Mail failures

Used when troubleshooting mail issues.

---

# 🧠 5. messages – The Most Important Log

View:

`more /var/log/messages`

This file logs:

- Hardware events
- Software events
- Kernel messages
- Application issues
- System failures

---

### 🚨 First Command Admin Runs When System Fails

`more /var/log/messages`

---

# 🔎 Search for Errors in Logs

Count lines:

`wc -l /var/log/messages`

Search for errors:

`grep -i error /var/log/messages`

Explanation:

| Option | Meaning |
|--------|----------|
| `-i` | Ignore uppercase/lowercase |
| `grep` | Search text |

---

# 🧠 dmesg vs messages

`dmesg`

Shows kernel ring buffer (hardware messages).

`/var/log/messages`

Contains similar info but stored permanently.

---

# 🔄 Real-Time Log Monitoring

Most powerful technique:

`tail -f /var/log/messages`

or

`tail -f /var/log/secure`

This command:

- Keeps file open
- Shows new entries live
- Updates automatically

Exit:

`Ctrl + C`

---

# 🔐 Permission Insight (Very Important)

Some logs require root access.

Example:

`boot.log` is owned by root.

If permission denied:

Switch to root:

`su -`

Then access log.

---

# 🧠 Log Format Structure

Most logs follow this format:

Month Date Time Hostname Service[PID]: Message

Example:

Jul 10 14:32:01 server crond[1234]: (root) CMD (backup.sh)

---

# 🧠 Log Monitoring Workflow (Real Scenario)

If server has issue:

1. Check authentication issues → `secure`
2. Check system errors → `messages`
3. Check boot problems → `boot.log`
4. Check cron issues → `cron`
5. Check email problems → `maillog`

---

# 🎓 Rapid-Fire Answers

### ❓ Where are Linux logs stored?
`/var/log`

### ❓ Which log checks login attempts?
`/var/log/secure`

### ❓ Which log checks cron jobs?
`/var/log/cron`

### ❓ Which log checks general system activity?
`/var/log/messages`

### ❓ How to monitor logs live?
`tail -f filename`

### ❓ How to search errors in logs?
`grep -i error filename`

---

# 🧠 Advanced Insight

Logs are:

- Evidence
- Troubleshooting tool
- Security audit trail
- Performance tracker

System Administration = 50% Logs + 50% Monitoring

---

# 🏁 Final Takeaway

A beginner runs commands.

A System Administrator reads logs.

Master these:

- `/var/log/messages`
- `/var/log/secure`
- `/var/log/cron`
- `tail -f`
- `grep`

And you will troubleshoot like a professional.

---

**✍️ Notes By Abhishek (Ez Abyss)**
