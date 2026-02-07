# 📁 Copying Directories in Linux (`cp -r`)

> Copying directories is a **very common and very important task** in Linux, especially when working with **configuration files**.  
> Best practice: **Always back up a directory before modifying it.**

---

## 🎯 Why Copy Directories?

You usually copy directories when:
- Backing up configuration files
- Testing changes safely
- Restoring settings after mistakes
- Migrating files to another location

📌 Configuration directories almost always contain **multiple files**, so copying them requires special handling.

---

## 🧠 Key Rule (Very Important)

To copy a directory in Linux:
- You **must** use the recursive option `-r`

### Why?
A directory can contain:
- Files
- Subdirectories
- Files inside subdirectories

📌 Linux needs to be told to copy **everything inside**, not just the directory name.

---

## 🔑 Command Used

### Syntax
- `cp -r source_directory destination_directory`

Where:
- `cp` → copy
- `-r` → recursive (directory + contents)

---

## ❌ What Happens If You Forget `-r`?

Example:
- `cp config /tmp/config-backup`

❌ Error:
- `cp: omitting directory 'config'`

📌 Linux thinks you’re trying to copy a **file**, not a directory.

---

## ✅ Correct Way (With `-r`)

- `cp -r config /tmp/config-backup`

📌 This copies:
- The directory
- All files inside it
- All subdirectories inside it

---

## 🧪 Hands-On Example (Step by Step)

### Step 1: Confirm user
- `whoami`

### Step 2: Confirm location
- `pwd`

---

### Step 3: Create a directory
- `mkdir config`

---

### Step 4: Create files inside the directory
- `cd config`
- `touch a.conf b.conf c.conf`

Verify:
- `ls -l`

---

### Step 5: Go back to home directory
- `cd`

---

### Step 6: Copy directory **without** `-r` (to see the error)
- `cp config /tmp/config-backup`

❌ Fails

---

### Step 7: Copy directory **with** `-r`
- `cp -r config /tmp/config-backup`

✅ Success (prompt returns, no error)

---

### Step 8: Verify copied directory
- `cd /tmp`
- `ls -ltr`

---

### Step 9: Verify files inside copied directory
- `cd config-backup`
- `ls -ltr`

📌 All files are copied correctly.
<img width="1907" height="1079" alt="image" src="https://github.com/user-attachments/assets/419f6e8d-70bb-4e7b-812d-3920c87f807d" />


---

## 🔄 What Does Recursive (`-r`) Mean?

Recursive copy means:
- Copy the directory
- Copy all subdirectories
- Copy all files inside them

📌 Think of `-r` as:
> “Copy everything inside, no matter how deep.”

---

## 🧠 Common Use Case (Real World)

Before editing system configs:
- Copy `/etc` subdirectory
- Modify original
- Restore from backup if needed

Example:
- `cp -r /etc/httpd /tmp/httpd-backup`

---

## 🧠 Memory Trick (Never Forget)

| Task | Command |
|----|--------|
| Copy file | `cp file1 file2` |
| Copy directory | `cp -r dir1 dir2` |
| Forget `-r` | ❌ Error |

📌 **Directory = recursive**

---

## ✅ One-Line Summary

> Directories in Linux are copied using the `cp -r` command, which recursively copies the directory and all of its contents.

---

**✍️ Notes By Abhishek (Ez Abyss)**
