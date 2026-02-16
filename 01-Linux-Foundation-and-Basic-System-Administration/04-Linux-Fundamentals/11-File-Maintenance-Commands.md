# File Maintenance Commands in Linux 
(cp, mv, mkdir, rm, rmdir, chgrp, chown) 

---

## Why File Maintenance Matters

As a Linux user (or security analyst), you must know how to:

- Copy files  
- Move files  
- Rename files  
- Delete files  
- Create directories  
- Remove directories  
- Change file ownership  

These are everyday administrative tasks.

---

# 1️⃣ `cp` — Copy Files

The `cp` command copies files or directories.

Basic syntax:

    cp source destination

### Example — Copy and Rename

    cp Mountain Everest

This:
- Copies `Mountain`
- Creates new file named `Everest`
- Original file remains unchanged

Verify:

    ls -ltr

---

### Copy to Another Directory

    cp Mountain /tmp

Now the file exists:
- In current directory
- In `/tmp`

Verify:

    cd /tmp
    ls -ltr

---

# 2️⃣ `rm` — Remove Files

The `rm` command deletes files.

    rm filename

Example:

    rm Everest

After running:

    ls

The file is gone.

---

⚠️ Important:
`rm` permanently deletes files.
There is no recycle bin.

---

# 3️⃣ `mv` — Move or Rename Files

The `mv` command does TWO things:

1. Rename a file  
2. Move a file to another location  

---

## Rename Example

    mv abyss ezabyss

This:
- Renames `abyss` to `ezabyss`
- Content remains the same

---

## Move to Another Directory

    mv Kathmandu /tmp

Now:
- File disappears from current directory
- Appears inside `/tmp`

Move it back:

    mv /tmp/Kathmandu ~

`~` means home directory.

---

# 4️⃣ `mkdir` — Create Directory

    mkdir Nepal

Verify:

    ls -ltr

Directory created.

---

# 5️⃣ `rmdir` — Remove Directory

Remove empty directory:

    rmdir Nepal

---

## Alternative Method

    rm -r Nepal

`-r` means recursive.

⚠️ Be careful:
`rm -r` deletes directories and everything inside.

---

# 6️⃣ `chgrp` — Change Group Ownership

Changes the group of a file.

    chgrp groupname filename

Example (as root):

    chgrp root Mountain

---

# 7️⃣ `chown` — Change File Owner

Changes the owner of a file.

    chown username filename

Example:

    chown root Mountain

---

## Change Owner AND Group Together

    chown username:groupname filename

Example:

    chown ihaveso:ihaveso Mountain

This:
- Changes user ownership
- Changes group ownership
- In one command

---

# Important Permission Note

To change ownership:
- You must be `root`
- Or have sudo privileges

Check current user:

    whoami

Switch to root:

    su -

---

# Quick Command Summary

| Command | Purpose |
|----------|----------|
| `cp` | Copy file |
| `rm` | Remove file |
| `mv` | Move or rename |
| `mkdir` | Create directory |
| `rmdir` | Remove empty directory |
| `rm -r` | Remove directory recursively |
| `chgrp` | Change group |
| `chown` | Change owner |

---

# Real Security Use Case

As a security analyst, you might:

- Copy suspicious logs
- Move evidence files
- Change ownership for investigation
- Archive old logs
- Clean temporary files

These commands are foundational for:
- System administration
- SOC operations
- Incident response

---

# Safety Tip

Before deleting:

    ls -l filename

Before recursive delete:

    ls directory_name

Always verify what you're deleting.

---

# Final Thought

File maintenance commands are basic —
but mastering them makes you efficient.

These are daily tools in Linux administration and cybersecurity.

---

**✍️ Notes By Abhishek (Ez Abyss)**
