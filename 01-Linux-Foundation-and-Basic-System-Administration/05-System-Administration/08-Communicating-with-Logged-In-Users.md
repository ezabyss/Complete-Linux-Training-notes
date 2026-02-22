# 💬 Communicating With Logged-In Users in Linux

As a system administrator, you sometimes need to communicate with users who are currently logged into the system.

Reasons may include:

- Scheduled maintenance  
- System reboot  
- High CPU or memory usage  
- Application causing load  
- Emergency shutdown  

Linux provides simple built-in commands to communicate with active users.

---

# 👥 1️⃣ `users` — See Who Is Logged In

    users

Displays usernames currently logged in.

Example:

    ezabyss ezabyss spiderman

If the same user has multiple sessions, their name appears multiple times.

To get more detailed session info:

    who

---

# 📢 2️⃣ `wall` — Broadcast Message to All Users

`wall` = write all

It sends a message to every logged-in user.

Run:

    wall

Type your message:

    System will reboot in 10 minutes.
    Please save your work.

Press:

    Ctrl + D

All logged-in users will immediately see:

    Broadcast message from root@hostname
    System will reboot in 10 minutes.
    Please save your work.

Use cases:

- Reboot warning  
- Maintenance notification  
- Security alert  
- Emergency downtime  

---

# ✍️ 3️⃣ `write` — Send Message to One User

To message a specific user:

    write username

Example:

    write spiderman

Then type your message:

    Your process is consuming high CPU.
    Please review your application.

Press:

    Ctrl + D

Only that user receives the message.

---

# 🔄 Replying Back

The receiving user can respond using:

    write ezabyss

Communication continues until either user presses:

    Ctrl + D

---

# 🧠 When to Use Each Command

| Command | Purpose |
|----------|----------|
| `users` | See logged-in users |
| `who` | See detailed session info |
| `wall` | Broadcast to everyone |
| `write` | Message one specific user |

---

# ⚠️ Important Notes

- `wall` requires permission (usually root)
- `write` works only if the user’s terminal allows messages
- Some systems disable `write` for security

To check if your terminal accepts messages:

    mesg

To enable messages:

    mesg y

To disable:

    mesg n

---

# 🔐 Why This Matters

In production environments:

- You must warn users before shutdown  
- You must coordinate maintenance  
- You may need to stop resource abuse  
- You may need to notify users of policy violations  

These simple commands are powerful tools for real-time communication.

---

# 🎯 Key Takeaway

Linux allows terminal-based communication between users without email, chat apps, or GUI tools.

Simple, direct, and immediate.

---

**✍️ Notes By Abhishek (Ez Abyss)**  
