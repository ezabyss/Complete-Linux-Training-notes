# Linux File Permissions (Read, Write, Execute)

---

## Why file permissions matter
Linux is a **multi-user operating system**.  
That means many users can exist on the same system at the same time.

File permissions allow you to:
- Protect your files from other users
- Prevent accidental deletion
- Control who can read, modify, or execute files
- Secure directories from unauthorized access

Understanding permissions is **critical** for system administration, security, and real-world Linux usage.

---

## The three types of permissions

Linux has **three basic permissions**:

| Permission | Symbol | Meaning |
|---------|-------|--------|
| Read | `r` | View file contents |
| Write | `w` | Modify or delete file |
| Execute | `x` | Run a program or script |

### What does execute mean?
- For **files**: allows the file to be run as a program or script
- For **directories**: allows entering the directory using `cd`

---

## Permission levels (who gets access)

Permissions are controlled at **three levels**:

| Level | Symbol | Applies to |
|----|------|-----------|
| User | `u` | File owner |
| Group | `g` | Users in the same group |
| Others | `o` | Everyone else |
| All | `a` | User + Group + Others |

---

## Viewing permissions
Use:
`ls -l`

Example:
`-rw-rw-r-- 1 ezabyss ezabyss 13 Abhishek`

### How to read this
`- rw- rw- r--`
- First character: file type  
  - `-` → file  
  - `d` → directory  
  - `l` → link  

Then groups of three:
- `rw-` → user permissions  
- `rw-` → group permissions  
- `r--` → others permissions  

---

## File permission breakdown
For file `Abhishek`:
- User: read + write
- Group: read + write
- Others: read only
- No execute permission (not a script)

---

## The command to change permissions
`chmod`

Often remembered as **change mode**.

Always explore with:
`man chmod`

---

## Removing permissions (examples)

### Remove write permission from group
`chmod g-w Abhishek`

Verify:
`ls -l Abhishek`

Now:
- Group can read
- Group cannot write

---

### Remove read permission from everyone
`chmod a-r Abhishek`

Verify:
`ls -l Abhishek`

Now:
- No one can read the file

---

### Remove write permission from user
`chmod u-w Abhishek`

Verify:
`ls -l Abhishek`

Result:
- User, group, and others have **no permissions**

---

## What happens with no permissions?

### Try to read the file
`cat Abhishek`

Result:
`Permission denied`

### Try to remove the file
`rm Abhishek`

Linux warns:
`remove write-protected regular empty file?`

Since you are the owner, Linux still asks for confirmation.

---

## Restoring permissions

### Give user read and write
`chmod u+rw Abhishek`

Verify:
`ls -l Abhishek`

---

### Give group read and write
`chmod g+rw Abhishek`

Verify again:
`ls -l Abhishek`

---

### Give others read permission
`chmod o+r Abhishek`

Verify:
`ls -l Abhishek`

Now permissions are restored similar to original state.

---

## Permissions on directories (VERY important)

### Why directories need execute permission
For directories:
- `r` → list files
- `w` → create/delete files
- `x` → enter directory (`cd`)

Without execute permission:
- You **cannot** `cd` into the directory

---

## Example: directory permissions

Directory `Nepal`

Check permissions:
`ls -ltr`

---

### Remove execute permission for everyone
`chmod a-x Nepal`

Verify:
`ls -ltr`

Now try:
`cd Nepal`

Result:
`Permission denied`

---

### Restore execute permission
`chmod a+x Nepal`

Verify:
`ls -ltr`

Now:
`cd Nepal`  
✔️ Works

---

## Key rules to remember

- `r` → read file contents
- `w` → modify or delete
- `x` → execute file or enter directory
- Directories **must have `x`** to access
- Permissions apply to **user, group, others**
- `chmod` controls access and safety

---

## One-line memory trick

**Files need `x` to run.**  
**Directories need `x` to enter.**

---

If permissions make sense now → you’re thinking like a Linux admin.

---

**✍️ Notes By Abhishek (Ez Abyss)**
