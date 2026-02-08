# Soft Links vs Hard Links in Linux (Inodes Explained)

---

## Why this topic matters
Links are **everywhere** in Linux:
- `/bin/python` → `/usr/bin/python`
- Versioned libraries
- Config shortcuts
- Shared files without duplication

If you truly understand **inodes + links**, Linux suddenly makes sense at a deeper level.

---

## First: What is an inode?
> **An inode is the real identity of a file in Linux.**

- Humans use **names** → `Abhishek`
- Linux uses **numbers** → inode `123456`

When you create a file:
- Linux assigns it an **inode number**
- The filename is just a *label* pointing to that inode

### Think like this
`Filename ──► Inode ──► Data on disk`

Linux does **not** care about names.  
It cares about **inode numbers**.

---

## Check inode numbers
`ls -li`

Example:
`123456 -rw-r--r-- 1 user user 20 Abhishek`

- `123456` → inode number  
- `1` → link count (important later!)

---

## Links = Multiple ways to reach data
A **link** is simply another way to reference data.

Windows analogy:
- Shortcut on Desktop → Soft link  
- Duplicate file but same identity → Hard link  

---

# Soft Link (Symbolic Link)

## What is a soft link?
A **soft link** is a file that:
- Points to a **filename**
- NOT directly to the inode

`Soft link ──► Filename ──► Inode ──► Data`

If the filename disappears → 💥 broken link

---

## Create a soft link
`ln -s /home/user/Abhishek /tmp/Abhishek`

Verify:
`ls -ltr`

Output looks like:
`l--------- Abhishek -> /home/user/Abhishek`

- `l` = link  
- `->` shows where it points  

---

## Soft link behavior (important)

### Read via soft link
`cat Abhishek`  
✔️ Works (as long as source exists)

### Remove original file
`rm /home/user/Abhishek`

Now:
- Soft link still exists
- But it is **broken**

Try:
`cat Abhishek`

❌ `No such file or directory`

> Soft link depends on the **path**, not the inode.

---

## Inode check (soft link)
`ls -li`

You’ll notice:
- Original file inode ≠ soft link inode  
- Soft link has its **own inode**

---

# Hard Link

## What is a hard link?
A **hard link**:
- Points **directly to the inode**
- Has no filename dependency

`Hard link ──► Inode ──► Data`

Multiple names, **same inode**, same data.

---

## Create a hard link
`ln /home/user/Abhishek /tmp/Abhishek`

(No `-s` option)

Verify:
`ls -li`

You’ll see:
- Same inode number  
- Link count increased (for example `1` → `2`)

---

## Hard link behavior (key difference)

### Modify content
From home:
`echo "123" >> Abhishek`

From `/tmp`:
`cat Abhishek`

✔️ Change appears

Why?
- Same inode  
- Same data  

---

### Delete original file
`rm /home/user/Abhishek`

Now check `/tmp`:
`cat Abhishek`

✔️ File still exists

> Data is deleted **only when link count = 0**

---

## Why hard links survive deletion
Linux rule:
> Data is removed **only when no filenames reference the inode**

Hard links = multiple references.

---

# Side-by-Side Comparison

| Feature | Soft Link | Hard Link |
|------|----------|----------|
| Points to | Filename | Inode |
| Survives source deletion | ❌ No | ✅ Yes |
| Inode number | Different | Same |
| Cross filesystem | ✅ Yes | ❌ No |
| Link count increases | ❌ No | ✅ Yes |
| Can link directories | ❌ (usually) | ❌ |
| Looks like shortcut | ✅ | ❌ |

---

## Visual intuition (memorize this)
<img width="855" height="426" alt="image" src="https://github.com/user-attachments/assets/873c18eb-0c63-4e89-a8c0-90942bf83e6e" />

### Soft link
`Abhishek_link ──► Abhishek ──► inode ──► data`

### Hard link
`Abhishek`  
`Abhishek_link ──► same inode ──► same data`

---

## When to use what (real world)

### Use **soft links** when:
- You want shortcuts
- Config paths change
- Cross filesystem links
- `/etc/alternatives`

### Use **hard links** when:
- You want data safety
- Backup systems
- Shared files without duplication
- Version control internals

---

## Golden rules 
- Soft link breaks if source path breaks  
- Hard link survives deletion  
- Hard links share inode  
- Soft links have their own inode  
- Data dies only when inode link count = 0  

---

## One-line memory trick
**Soft link remembers the name.**  
**Hard link remembers the number (inode).**

---

## Practice (do this!)
1. Create a file  
2. Create both links  
3. Modify content  
4. Delete source  
5. Observe behavior with `ls -li`

👉 [Lab 05: Hard and Soft Links](labs/05-Hard-and-Soft-Links)

---

**✍️ Notes By Abhishek (Ez Abyss)**
