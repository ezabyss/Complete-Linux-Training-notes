# 🌍 Linux User vs Global Aliases
### Making Aliases Permanent & System-Wide

---

# 🎯 Why This Matters

By default:

- Aliases are **temporary**
- They disappear after logout

Problem:

You create an alias → works
You log out → it's gone ❌


Solution:

- Save aliases permanently
- Make them user-specific or global

---

# 📌 Types of Aliases

There are **2 types of persistent aliases**:

| Type | Scope |
|------|------|
| User Alias | Only one user |
| Global Alias | All users |

---

# 🧠 Key Concept

| Location | Purpose |
|--------|--------|
| `~/.bashrc` | user-specific aliases |
| `/etc/bashrc` | global aliases |

---

# 🧪 Temporary Alias (Session Only)

Example:

`alias hh='hostname'`

Works immediately:

`hh`

But after logout:


command not found ❌


---

# 👤 User-Specific Alias

## Step 1 — Go to home directory

`cd ~`

---

## Step 2 — Open bashrc

`vi .bashrc`

---

## Step 3 — Add alias

## Personal aliases

`alias hh='hostname'`

---

## Step 4 — Apply changes

`source ~/.bashrc`

OR reopen terminal

---

## ✅ Result

Now:

`hh`

Works every time **for that user only**.

---

# 🌍 Global Alias (All Users)

## ⚠️ Requires root access

---

## Step 1 — Open global config

`vi /etc/bashrc`

---

## Step 2 — Add alias

## Global aliases

`alias hh='hostname'`


---

## Step 3 — Save and exit

---

## Step 4 — Reload or relogin

`source /etc/bashrc`

OR logout/login

---

## ✅ Result

Now:

- works for all users
- new users also get it

---

# 🌍 Real World Scenario

You are a system administrator:

You want every user to have:

`alias ll='ls -al'`

Instead of setting for each user:

👉 Add to `/etc/bashrc`

---

# 🧪 Test Across Users

### User 1:

`hh` → works ✅  

### Root:

`hh` → works ✅  

### New user:

`hh` → works ✅  

---

# 🔍 View Aliases

`alias`

Shows all active aliases.

---

# ❌ Remove Alias

`unalias hh`

---

# ⚠️ Important Behavior

| Action | Result |
|------|------|
| Add alias in terminal | temporary |
| Add in `.bashrc` | permanent (user) |
| Add in `/etc/bashrc` | permanent (global) |

---

# 🧠 Quick Questions

### Why do aliases disappear after logout?

Because they are stored in **temporary session memory**.

---

### Where to store permanent aliases?

- User → `~/.bashrc`
- Global → `/etc/bashrc`

---

### Who can modify global aliases?

Only **root user**.

---

### Why use global aliases?

To standardize commands across all users.

---

# 🏁 Key Takeaways

- Aliases are temporary unless saved
- `.bashrc` → user-level persistence
- `/etc/bashrc` → system-wide aliases
- Requires reload or new session
- Essential for **productivity & consistency**

---

# 🚀 Pro Tip

Create a **personal alias library**:

alias ll='ls -al'
alias cls='clear'
alias h='history'
alias gs='git status'


Add to `.bashrc` → become faster than 90% of users.

---

**✍️ Notes By Abhishek (Ez Abyss)**
