# 🌍 Linux Environment Variables

---

# 🎯 What Are Environment Variables?

An **environment variable** is a dynamic named value that affects how programs and processes run on a computer.

They define the **environment in which a user session operates**.

In simple terms:

Environment variables are **system-defined settings that control how your Linux session behaves**.

---

# 🏠 Simple Example (House Analogy)

Think of your computer environment like a **house**.

Every room has a specific purpose:

| Room | Purpose |
|-----|------|
| Bedroom | Sleep |
| Kitchen | Cook |
| Dining Room | Eat |
| Playroom | Play |

You **don't cook in the bedroom** or **sleep in the kitchen**.

These are **rules of the house environment**.

Similarly, Linux provides **rules and settings** that define how a user session works.

These rules are called **environment variables**.

---

# 👤 User Login Environment

When a user logs into Linux, the system automatically assigns:

- Home directory
- Default shell
- System paths
- Language settings
- Terminal type
- History size

All these values are stored in **environment variables**.

---

# 🔎 Viewing Environment Variables

Two common commands:

### Show all environment variables


`printenv`


or


`env`


Example:


`printenv | more`


This shows the variables page by page.

---

# 🧾 Example Environment Variables

| Variable | Meaning |
|--------|--------|
| `HOME` | User home directory |
| `SHELL` | Default shell |
| `PATH` | Command search locations |
| `USER` | Logged-in user |
| `HOSTNAME` | Machine name |
| `LANG` | System language |
| `HISTSIZE` | Command history size |

---

# 🔍 Viewing a Specific Environment Variable

Use `echo`.

### Check shell

`echo $SHELL`

Example output:

`/bin/bash`


---

### Check PATH

`echo $PATH`

Example output:

`/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/user/bin`

This tells Linux **where to search for commands**.

---

### Check home directory

`echo $HOME`

Example:

`/home/user`

You can even navigate using it:

`cd $HOME`

---

# ⚙️ Creating Environment Variables (Temporary)

Create a variable for current session:

`export TEST=1`

Check it:

`echo $TEST`

Output:

`1`

⚠ This variable disappears after logout.

---

# 💾 Setting Environment Variables Permanently

Permanent variables are stored in:

`~/.bashrc`

Steps:

### 1️⃣ Go to home directory

`cd`

---

### 2️⃣ Backup bashrc

`cp .bashrc .bashrc.backup`

---

### 3️⃣ Edit bashrc

`vi .bashrc`

Add:

`TEST='123'`

`export TEST`

Save the file.

---

### 4️⃣ Reload session

Logout and login again.

or

`source ~/.bashrc`

---

### 5️⃣ Verify

`echo $TEST`

Output:

`123`

---

# 👀 Hidden Files

Files starting with `.` are hidden.

Example:

`.bashrc`

View hidden files:

`ls -la`

---

# 🌐 Global Environment Variables (For All Users)

If you want variables available for **all users**, modify:

`/etc/profile`

or

`/etc/bashrc`


Example entry:

`export COMPANY_NAME="MyCompany"`

⚠ Requires root access.

---

# ⚠ Important Warning

Changing global environment files incorrectly can cause:

- login failures
- system errors
- broken shells

Always test in **development environments first**.

---

# 🧠 Useful Environment Variables

| Variable | Description |
|--------|-------------|
| `$PATH` | Command search path |
| `$HOME` | User home directory |
| `$USER` | Current user |
| `$PWD` | Current directory |
| `$HOSTNAME` | System hostname |
| `$SHELL` | Default shell |

---

# 🧪 Example Workflow

Check environment:

`printenv`


Check specific value:

`echo $PATH`

Create variable:

`export PROJECT=cybersecurity`

Verify:

`echo $PROJECT`

---

# 🏁 Key Takeaways

Environment variables:

- Define the Linux session environment
- Control command behavior
- Store system paths
- Can be temporary or permanent
- Can be user-specific or global

Understanding environment variables is **essential for Linux administrators and DevOps engineers**.

---

**✍️ Notes By Abhishek (Ez Abyss)**
