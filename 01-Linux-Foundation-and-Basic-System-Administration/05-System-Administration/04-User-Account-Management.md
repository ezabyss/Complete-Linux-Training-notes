# User Account Management in Linux

---

# 📌 Why User Management Matters

In Linux systems:

- Multiple users may access the system
- Permissions must be controlled
- Groups define shared access
- Security depends on proper account management

That’s why Linux provides structured commands for managing users and groups.

---

# 🛠 Core User Management Commands

| Command | Purpose |
|----------|----------|
| `useradd` | Create new user |
| `groupadd` | Create new group |
| `userdel` | Delete user |
| `groupdel` | Delete group |
| `usermod` | Modify user |
| `passwd` | Set/change password |

---

# 📁 Important System Files

When you create users, Linux stores information in:

| File | Purpose |
|------|----------|
| `/etc/passwd` | User account info |
| `/etc/group` | Group info |
| `/etc/shadow` | Encrypted passwords |

⚠️ These are critical system files.

---

# 🔐 Become Root First

Most user management commands require root:

    su -

or

    sudo -i

---

# 1️⃣ Create a User

Create user `spiderman`:

    useradd spiderman

Verify:

    id spiderman

Check home directory:

    ls /home

---

# 2️⃣ Create a Group

Create group `superheroes`:

    groupadd superheroes

Verify:

    grep superheroes /etc/group

---

# 3️⃣ Delete a User

Delete user only:

    userdel spiderman

Delete user including home directory:

    userdel -r spiderman

---

# 4️⃣ Delete a Group

    groupdel superheroes

---

# 5️⃣ Modify a User (Add to Group)

Recreate user:

    useradd spiderman

Add to secondary group:

    usermod -aG superheroes spiderman

Verify:

    id spiderman

Or:

    grep spiderman /etc/group

⚠️ Always use `-aG` when adding supplementary group.
Without `-a`, existing groups may be overwritten.

---

# 📂 Change Primary Group

If you want to change primary group:

    usermod -g superheroes spiderman

---

# 🔑 Set Password

Every new user should have a password:

    passwd spiderman

---

# 🧾 Understanding `/etc/passwd`

Example entry:

    spiderman:x:1002:1002::/home/spiderman:/bin/bash

Field breakdown:

1. Username
2. Password placeholder (x)
3. User ID (UID)
4. Group ID (GID)
5. Description
6. Home directory
7. Default shell

---

# 🧾 Understanding `/etc/group`

Example:

    superheroes:x:1005:spiderman

Fields:

1. Group name
2. Password placeholder
3. Group ID
4. Members

---

# 🧾 Understanding `/etc/shadow`

Contains encrypted password data and:

- Password aging
- Expiry settings
- Security parameters

Only root can read this file.

---

# 🚀 Create User With Full Parameters

Example:

    useradd -g superheroes \
            -s /bin/bash \
            -c "Iron Man Character" \
            -m -d /home/ironman \
            ironman

Set password:

    passwd ironman

Verify:

    id ironman

---

# 🧠 Real-World Corporate Usage

In enterprise environments:

- HR systems create bulk users
- Groups define department access
- Scripts automate user provisioning
- Password policies are enforced
- `/etc/shadow` controls expiry

---

# ⚠ Important Security Notes

- Never manually edit `/etc/shadow`
- Always test commands carefully
- Always use `-aG` when adding groups
- Delete users with `-r` if removing fully

---

# 🎯 Quick Reference

| Task | Command |
|------|----------|
| Create user | `useradd username` |
| Create group | `groupadd groupname` |
| Add user to group | `usermod -aG group user` |
| Delete user | `userdel -r user` |
| Delete group | `groupdel group` |
| Set password | `passwd user` |

---

# 💡 Final Thought

User management is foundational for:

- Linux administration
- DevOps
- Cybersecurity
- Server security

Mastering these commands makes you production-ready.

---

**✍️ Notes By Abhishek (Ez Abyss)**  
