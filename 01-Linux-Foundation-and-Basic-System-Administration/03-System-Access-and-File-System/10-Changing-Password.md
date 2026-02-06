# 🔐 Changing Passwords in Linux (`passwd`)

> Changing passwords is a **basic but critical security task** in Linux.  
> Every user should change their password **immediately after first login**.

---

## 🎯 When Do You Change a Password?

You may need to change a password when:
- Your account is created for the first time
- You log in with a temporary password
- The system forces a password change on first login
- You want to update your password for security
- You are root and need to reset another user’s password

---

## 🧠 The Password Command

### Command Used
- `passwd`

⚠️ **Important**
- The command is **NOT** `password`
- Correct command is: `passwd` (no `o`, no `r`)

---

## 👤 Changing *Your Own* Password (Normal User)

If you are logged in as yourself:

### Step 1: Run the command
- `passwd`

### Step 2: Enter current password
- (You will not see characters while typing)

### Step 3: Enter new password
- Must meet system security rules

### Step 4: Re-enter new password
- Confirms there were no typing mistakes

### Success Message
- `authentication tokens updated successfully`

📌 This confirms the password was changed.

---

## 👑 Changing a User Password as Root

Only **root** can change another user’s password.

### Become root
- `su -`

### Change another user’s password
- `passwd username`

📌 Example:
- `passwd abhishek`

⚠️ Be careful — this **resets** the user’s password immediately.

---

## ⚠️ Very Important Behavior to Remember

| Command | What It Does |
|------|------------|
| `passwd` | Changes **your own** password |
| `passwd root` | Changes **root** password (only as root) |
| `passwd username` | Changes **that user’s** password |

📌 If you are root and run `passwd` **without a username**,  
you are changing **root’s password**.

---

## 🔒 Password Security Rules (Common Errors)

Linux enforces password policies such as:

### ❌ Too short
- Less than 8 characters

### ❌ Dictionary words
- `password`
- `admin`
- `welcome`

### ❌ Simple sequences
- `12345678`
- `abcdefg`

📌 Use:
- Uppercase + lowercase
- Numbers
- Special characters

---

## 🧪 Common Error Messages Explained

| Message | Meaning |
|------|--------|
| Password too short | Increase length |
| Fails dictionary check | Avoid common words |
| Authentication failure | Incorrect current password |

---

## 🧠 Best Practices (Interview + Real World)

- Change password immediately after first login
- Never share passwords
- Avoid predictable patterns
- Root should **rarely** be used for daily work
- Prefer `sudo` over direct root login

---

## 📝 Practice Exercise

1. Log in as normal user  
2. Run `passwd` and change your password  
3. Switch to root using `su -`  
4. Change another user’s password using `passwd username`  
5. Log back in as that user to confirm

📌 Practice builds confidence.

---

## ✅ In One-Line

> The `passwd` command is used to change user passwords in Linux, where normal users can change their own passwords and root can change any user’s password.

---

**✍️ Notes By Abhishek (Ez Abyss)**
