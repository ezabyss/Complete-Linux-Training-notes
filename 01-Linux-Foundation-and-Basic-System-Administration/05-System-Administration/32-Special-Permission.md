# 🔐 Linux Special Permissions – SUID, SGID, Sticky Bit

---

# 🎯 Learning Objective

Understand advanced Linux permissions used to control:

- Program execution privileges
- Group execution behavior
- File deletion protection in shared directories

These permissions are critical in **multi-user Linux systems** and are widely used in **system administration and cybersecurity**.

---

# 📌 Linux Permission Basics

Every Linux file or directory has **three permission sets**:

| Category | Meaning |
|--------|--------|
| User (u) | Owner of the file |
| Group (g) | Users belonging to the file’s group |
| Others (o) | All other users |

Each category has three permissions:

| Symbol | Meaning |
|------|------|
| r | read |
| w | write |
| x | execute |

Example permission:

`-rwxr-xr-x`

Explanation:

| Section | Meaning |
|------|------|
| `-` | file type |
| `rwx` | owner permissions |
| `r-x` | group permissions |
| `r-x` | others permissions |

Permissions are modified using:

`chmod`

Example:

`chmod 777 /testfile`

---

# ⚡ Special Permissions

Linux supports **three special permission bits**:

| Permission | Name |
|-----------|------|
| SUID | Set User ID |
| SGID | Set Group ID |
| Sticky Bit | Restricted deletion |

These permissions **modify how files behave when executed or deleted**.

---

# 1️⃣ SUID (Set User ID)

## Definition

SUID allows a program to run with the **permissions of the file owner instead of the user executing it**.

---

# 🔍 Real World Scenario

Consider the command:

`passwd`

When users change their password, the system updates:

`/etc/shadow`

This file is **owned by root** and cannot be modified by normal users.

However, users still run:

`passwd`

How?

The `passwd` program has **SUID enabled**, so it temporarily runs with **root privileges**.

---

# 🔎 Checking SUID Permission

Find command location:

`which passwd`

Example:

`/usr/bin/passwd`

Check permissions:

`ls -l /usr/bin/passwd`

Example output:

`-rwsr-xr-x`

Notice the **`s`** replacing the execute permission in the owner section.

This indicates **SUID is enabled**.

---

# 🔧 Setting SUID

Enable SUID using:

`chmod u+s program`

Example:

`chmod u+s /testfile`

---

# ❌ Removing SUID

`chmod u-s program`

Example:

`chmod u-s /testfile`

---

# 2️⃣ SGID (Set Group ID)

## Definition

SGID allows a program to run with the **group permissions of the file instead of the executing user**.

---

# 🔍 Real World Scenario

Imagine a **shared development directory** used by a team.

Developers belong to a group called:

`developers`

When SGID is enabled on a directory:

- Every file created inside inherits the **same group ownership**

This simplifies collaboration.

---

# 🔎 Checking SGID

Example:

`ls -l /usr/bin/locate`

Example output:

`-rwxr-sr-x`

Notice the **`s`** in the group section.

This means **SGID is active**.

---

# 🔧 Setting SGID

`chmod g+s directory`

Example:

`chmod g+s /projectfiles`

---

# ❌ Removing SGID

`chmod g-s directory`

Example:

`chmod g-s /projectfiles`

---

# 🔍 Find All SUID and SGID Files

System administrators often audit these permissions.

Command:

`find / -perm /6000 -type f`

Explanation:

| Command | Meaning |
|------|------|
| `find /` | search entire system |
| `-perm /6000` | files with SUID or SGID |
| `-type f` | files only |

---

# ⚠ Important Security Note

SUID and SGID work **only on compiled executables**, typically written in:

- C
- C++

They **do NOT work on bash scripts**.

---

# 3️⃣ Sticky Bit

## Definition

Sticky bit prevents users from deleting files they **do not own**, even if they have write permissions in that directory.

---

# 🔍 Real World Scenario

Consider the shared directory:

`/tmp`

Every user can write to this directory.

Without protection, users could delete each other's files.

Sticky bit ensures:

- Users can delete **their own files**
- Users cannot delete **files owned by others**

---

# 🔎 Checking Sticky Bit

Run:

`ls -ld /tmp`

Example output:

`drwxrwxrwt`

Notice the **`t`** at the end.

This indicates **sticky bit enabled**.

---

# 🔧 Setting Sticky Bit

`chmod +t directory`

Example:

`chmod +t /sharedfolder`

---

# ❌ Removing Sticky Bit

`chmod -t directory`

Example:

`chmod -t /sharedfolder`

---

# 🧪 Practical Lab Example

### Step 1 — Create shared directory

`mkdir /allinone`

---

### Step 2 — Allow full access

`chmod 777 /allinone`

---

### Step 3 — User creates directory

`mkdir /allinone/userfiles`

---

### Step 4 — Another user deletes it

`rm -rf /allinone/userfiles`

Deletion succeeds.

---

### Step 5 — Enable sticky bit

`chmod +t /allinone`

Verify:

`ls -ld /allinone`

Example output:

`drwxrwxrwt`

---

### Step 6 — Try deleting again

`rm -rf /allinone/userfiles`

Result:

`Operation not permitted`

Deletion blocked.

---

# 📊 Numeric Representation

| Permission | Numeric Value |
|-----------|--------------|
| SUID | 4 |
| SGID | 2 |
| Sticky Bit | 1 |

---

# Example Numeric Usage

Enable SUID:

`chmod 4755 /testfile`

Breakdown:

| Digit | Meaning |
|------|------|
| 4 | SUID |
| 7 | owner permissions |
| 5 | group permissions |
| 5 | others permissions |

---

# 🧠 Quick Questions

### What is SUID?

Allows a program to run with **owner privileges**.

---

### What is SGID?

Allows a program to run with **group privileges**.

---

### What does sticky bit do?

Prevents users from deleting files they do not own.

---

### Which directory commonly uses sticky bit?

`/tmp`

---

# 🏁 Key Takeaways

| Permission | Purpose |
|-----------|--------|
| SUID | Run program as file owner |
| SGID | Run program as file group |
| Sticky Bit | Protect shared directories |

These permissions are essential for **Linux security and multi-user systems**.

---

**✍️ Notes By Abhishek (Ez Abyss)**
