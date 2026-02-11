# Linux File Ownership (User & Group Ownership)

---

## Why File Ownership Matters

Linux is a **multi-user system**.

Every file and directory has:
- A **user owner**
- A **group owner**

Ownership determines:
- Who controls the file
- Who can modify it
- Who can delete it
- Who can change permissions

Understanding ownership is essential for:
- System administration
- Security
- Production environments

---

# Two Types of Ownership

Every file has:

1. **User (Owner)**
   - The person who created the file
2. **Group**
   - The group associated with the file

Check ownership using:
`ls -l`

Example:
`-rw-r--r-- 1 ezabyss ezabyss 0 Mountain`

Breakdown:
- `ezabyss` (3rd column) → User owner
- `ezabyss` (4th column) → Group owner

---

# Important Rule

Permissions are checked in this order:

1. User
2. Group
3. Others

If you belong to a group that has permissions, you inherit those permissions.

---

# Commands to Change Ownership

## Change User Ownership
`chown`

## Change Group Ownership
`chgrp`

---

# Viewing Ownership

Run:
`ls -ltr`

You will see:

- File name
- User owner
- Group owner

Example:
`-rw-r--r-- 1 ezabyss ezabyss 0 Mountain`

---

# Changing Ownership (Requires Root)

Normal users **cannot** change file ownership to another user.

Only `root` can do that.

Switch to root:
`su -`

---

# Change File Owner

Change file `Mountain` to be owned by `root`:

`chown root Mountain`

Verify:
`ls -l Mountain`

Now:
- User owner = `root`

---

# Change Group Ownership

Change group of `Mountain` to `root`:

`chgrp root Mountain`

Verify:
`ls -l Mountain`

Now:
- Group owner = `root`

---

# Change Both User and Group Together

`chown root:root Mountain`

This changes:
- User → root
- Group → root

---

# Recursive Ownership Change

If you want to change ownership of a directory AND everything inside it:

`chown -R root directory_name`

`-R` = Recursive

This changes:
- Parent directory
- All subdirectories
- All files inside

Same for group:
`chgrp -R groupname directory_name`

---

# Important Concept: Why You Could Still Delete a File

Even if a file is owned by `root`, you may still delete it if:

You have write permission on the **parent directory**.

Example:

Your home directory:
`/home/abhishek`

Check permissions:
`ls -ld /home/abhishek`

If you have:
`rwx`

Then you can:
- Create files
- Delete files
- Modify files inside

Even if the file owner is `root`.

---

# Why You Cannot Create Files in `/etc`

Try:
`touch /etc/testfile`

You get:
`Permission denied`

Check:
`ls -ld /etc`

You will see:
- Owned by `root`
- Only `root` has write permission

Others cannot write there.

---

# Real-World Example

If root creates a file in `/etc`:
`touch /etc/test123`

Normal user:
`rm /etc/test123`

You get:
`Permission denied`

Because:
- You do not have write permission in `/etc`

Ownership + Directory permissions both matter.

---

# Ownership Summary

| Command | Purpose |
|----------|----------|
| `ls -l` | View owner and group |
| `chown user file` | Change file owner |
| `chgrp group file` | Change file group |
| `chown user:group file` | Change both |
| `chown -R` | Recursive ownership change |

---

# Key Security Rule

File deletion depends on:
- Write permission of **directory**
Not
- File ownership alone

---

# One-Line Memory Trick

**Ownership controls authority.**  
**Directory permissions control deletion.**

---

If you understand ownership + permissions together,  
you are now thinking like a real Linux administrator.

---

**✍️ Notes By Abhishek (Ez Abyss)**
