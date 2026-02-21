# 🔐 Password Aging in Linux (chage Command)

---

# 📌 What Is Password Aging?

Password aging means setting:

- Password expiration date  
- Minimum days before password can be changed  
- Maximum valid days  
- Warning days before expiration  
- Account disable period after expiration  

It improves security by:

- Forcing regular password changes  
- Reducing risk of long-term credential compromise  
- Enforcing security policies  

---

# 🛠 Command Used: `chage`

`chage` = Change Age  

It works **per user**.

Basic syntax:

    chage [options] username

---

# 🔎 View Current Password Aging Settings

    chage -l spiderman

This displays:

- Last password change
- Password expiration date
- Minimum days
- Maximum days
- Warning days
- Inactive period

You can also inspect directly:

    grep spiderman /etc/shadow

---

# 📂 Where Password Aging Is Stored

Password aging information is stored in:

    /etc/shadow

Fields format:

    username:password:lastchange:min:max:warn:inactive:expire

---

# 🔧 Important chage Options

| Option | Meaning |
|--------|----------|
| `-d` | Set last password change (days since Jan 1, 1970) |
| `-m` | Minimum days before password change |
| `-M` | Maximum days password is valid |
| `-W` | Warning days before expiration |
| `-I` | Inactive days after expiration |
| `-E` | Absolute account expiration date |
| `-l` | List password aging information |

---

# 🔐 Example: Set Password Policy for User

Set:

- Minimum days = 5  
- Maximum days = 90  
- Warning = 10 days  
- Inactive = 3 days  

    chage -m 5 -M 90 -W 10 -I 3 spiderman

---

# 🔎 Verify Changes

    chage -l spiderman

Or check shadow file:

    grep spiderman /etc/shadow

You will see values updated in these fields:

    :lastchange:5:90:10:3:

---

# 📅 About the -d Option

`-d` sets the last password change date.

Example:

    chage -d 0 spiderman

This forces password change at next login.

Note:
The value is stored as number of days since Jan 1, 1970 (Unix epoch).

---

# 🚫 Common Mistake

Running command without username:

    chage -m 5 -M 90 -W 10 -I 3

This will return an error because username is required.

Correct:

    chage -m 5 -M 90 -W 10 -I 3 spiderman

---

# 🌍 Set Default Password Aging for All New Users

Instead of configuring per user, modify:

    /etc/login.defs

Open:

    vi /etc/login.defs

Look for:

    PASS_MAX_DAYS
    PASS_MIN_DAYS
    PASS_WARN_AGE

Example:

    PASS_MAX_DAYS   90
    PASS_MIN_DAYS   5
    PASS_WARN_AGE   10

These settings apply to **new users only**.

---

# 🔎 Other Important Settings in `/etc/login.defs`

- `UID_MIN` → Starting UID for regular users
- `UID_MAX` → Maximum UID
- `SYS_UID_MIN` → System user ID minimum
- `SYS_UID_MAX` → System user ID maximum
- `CREATE_HOME` → Auto create home directory
- `ENCRYPT_METHOD` → Default password encryption (e.g., SHA512)
- `UMASK` → Default file permission for new users

---

# 🔐 Difference Between Commands

| Command | Purpose |
|----------|---------|
| `chage` | Modify password aging settings |
| `usermod` | Modify user account properties |
| `/etc/login.defs` | Set system-wide defaults |

---

# 🎯 Key Takeaways

- `chage` controls password expiration per user  
- `/etc/login.defs` controls defaults for new users  
- Password aging data is stored in `/etc/shadow`  
- Always verify changes using `chage -l username`  

Password aging is a core part of Linux user security management.

---

**✍️ Notes By Abhishek (Ez Abyss)**  
