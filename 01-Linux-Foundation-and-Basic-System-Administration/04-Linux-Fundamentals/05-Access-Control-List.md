# Linux Access Control Lists (ACL) – Fine-Grained Permissions

---

## Why ACL Exists

You already learned:

- Standard permissions → `rwx`
- Ownership → user + group
- `chmod`, `chown`, `chgrp`

But sometimes standard permissions are **not flexible enough**.

### Problem Scenario

Suppose:

- File is owned by `root`
- User `ezabyss` is NOT in the `root` group
- You want ONLY `ezabyss` to edit the file

If you give write permission to:
- Others → everyone can write ❌
- Group → entire group can write ❌

But you want:
✔ Only ONE specific user

That’s where **ACL (Access Control List)** comes in.

---

# What is ACL?

ACL = **Access Control List**

It is an additional permission layer built on top of standard Unix permissions.

It allows:
- Per-user permissions
- Per-group permissions
- Fine-grained access control

Think of it as:

Standard permissions → basic control  
ACL → advanced precision control

---

# Check if a File Has ACL

Run:
`ls -l`

If you see a `+` at the end of permissions:

Example:
`-rw-r--r--+`

The `+` means:
✔ This file has ACL entries

---

# ACL Commands

| Command | Purpose |
|----------|----------|
| `getfacl file` | View ACL permissions |
| `setfacl` | Set or modify ACL |
| `setfacl -x` | Remove specific ACL |
| `setfacl -b` | Remove all ACL entries |
| `setfacl -R` | Recursive ACL |

---

# Viewing ACL

`getfacl Mountain`

Output shows:
- Owner
- Group
- Standard permissions
- Extra ACL entries (if any)

---

# Grant Permission to a Specific User

## Syntax

`setfacl -m u:username:permissions filename`

> Create file using root
Example:

`setfacl -m u:ezabyss:rw Everest`

Meaning:
- Modify ACL
- User = abhishek
- Permission = read + write
- File = Texas

---

## Verify

`getfacl Everest`

You will see:

`user:ezabyss:rw-`

Now only `ezabyss` can modify the file.

---

# Important: Why ACL Is Useful

Without ACL:

If you gave:
`chmod o+w Everest`

Then:
❌ Everyone can write

With ACL:
✔ Only specific user can write

---

# Grant Permission to a Specific Group

Syntax:

`setfacl -m g:groupname:permissions filename`

Example:

`setfacl -m g:developers:rw Everest`

Now:
- Only users in `developers` group get write access

---

# Recursive ACL (Very Powerful)

To apply ACL to directory AND everything inside:

`setfacl -R -m u:ezabyss:rw directory_name`

`-R` = recursive

---

# Default ACL (Inheritance for New Files)

If you want all future files inside a directory to inherit ACL:

`setfacl -d -m u:ezabyss:rw directory_name`

`-d` = default ACL

This ensures:
- New files automatically inherit permission

---

# Remove Specific ACL Entry

`setfacl -x u:ezabyss Everest`

Removes ACL for that user only.

Verify:
`getfacl Everest`

---

# Remove All ACL Entries

`setfacl -b Everest`

Now:
- ACL is cleared
- File returns to standard permissions
- `+` disappears from `ls -l`

---

# Important Rule About Deleting Files

Even if ACL gives write permission:

✔ User can modify file  
✔ User can edit file  
❌ User cannot delete file  

Why?

File deletion depends on:
- Write permission of the **parent directory**

Not the file itself.

This is critical for exams and real-world troubleshooting.

---

# Real-World Example

Root creates file:
`touch Texas`

Root gives ACL:
`setfacl -m u:ezabyss:rw Everest`

User `ezabyss`:
- Can edit file
- Can modify file
- Cannot delete file (unless directory allows)

---

# Compare: Standard vs ACL

| Feature | Standard Permission | ACL |
|----------|--------------------|------|
| User-level control | Owner only | Any user |
| Group-level control | Single group | Multiple groups |
| Fine-grained access | Limited | Precise |
| Shows `+` in `ls -l` | No | Yes |

---

# When Should You Use ACL?

Use ACL when:

- One user needs special access
- Temporary permission is needed
- You don’t want to change group structure
- Shared environments
- Enterprise systems

Avoid ACL when:
- Simple permission structure works
- Environment must remain minimal

---

# Quick Memory Rules

Standard permissions → broad control  
ACL → precision control  

Deletion depends on directory, not file.  

If you see `+` → ACL exists.

---

# Practice (Highly Recommended) as root user

1. Create file:
   `touch Everest`

2. Check ACL:
   `getfacl Everest`

3. Add ACL for user:
   `setfacl -m u:ezabyss:rw Everest`

4. Verify:
   `getfacl Everest`

5. Remove specific ACL:
   `setfacl -x u:ezabyss Everest`

6. Remove all ACL:
   `setfacl -b Everest`

---

If you understand ACL,  
you now understand **enterprise-level Linux permission control**.

---

**✍️ Notes By Abhishek (Ez Abyss)**
