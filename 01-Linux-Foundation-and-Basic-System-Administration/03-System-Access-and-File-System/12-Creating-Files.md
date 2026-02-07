# 🛠️ Creating Files and Directories in Linux

> Linux provides **multiple ways to create files** and a **simple command to create directories**.  
> Knowing these methods is essential for daily system usage and interviews.

---

## 🎯 What You’ll Learn in This Lesson
- Different ways to create files
- How to create directories
- How to verify creation
- Understanding permission errors

---

## 👤 Step 1: Know Who You Are & Where You Are

Check logged-in user:
- `whoami`

Check current directory:
- `pwd`

📌 In this lesson, all files and directories are created inside the **home directory**.

---

## 📄 Ways to Create Files in Linux

There are **three common ways** to create files:

1. Using `touch`
2. Using `cp` (copy)
3. Using `vi` / `vim` editor

---

## 1️⃣ Creating Files Using `touch`

### Purpose
- Creates an **empty file**

### Example
- `touch abyss`

Verify:
- `ls -l`

📌 If you get your prompt back with no error, the file is created.

---

### Creating Multiple Files at Once
- `touch Mountain Kathmandu Nepal`

📌 One command → multiple files.

---

## 2️⃣ Creating Files Using `cp` (Copy)

### Purpose
- Creates a **new file by copying an existing file**

### Syntax
- `cp source_file destination_file`

### Example
- `cp Mountain Everest`
- `cp Kathmandu Pokhara`


Verify:
- `ls -ltr`

📌 The new file gets the **same content** as the source file.

---

## 📋 Viewing Files by Creation Time

- `ls -ltr`

Meaning:
- `-l` → long listing
- `-t` → sort by time
- `-r` → reverse order

📌 Oldest files at the top, newest at the bottom.

---

## 3️⃣ Creating Files Using `vi` / `vim`

### Purpose
- Creates and edits files interactively

### Example
- `vi Pokhara`

📌 This opens the editor.

To **save and exit safely**:
- Press `Shift + :`
- Type `wq!`
- Press `Enter`

Verify:
- `ls -ltr`

⚠️ **Important**
- `vi` is powerful but tricky
- We’ll cover it in detail later

---

## 📁 Creating Directories Using `mkdir`

### Purpose
- Creates directories (folders)

### Example
- `mkdir Nepal`

Verify:
- `ls -ltr`

📌 Directories usually appear with a different color and start with `d` in `ls -l`.

---

### Creating Multiple Directories at Once
- `mkdir Places Mountains`

📌 One command → multiple directories.

---

## 🚫 Permission Denied (Very Important Concept)

### Example
Try creating a file in `/etc`:
- `cd /etc`
- `touch test123`

❌ Result:
- Permission denied

### Why?
- `/etc` is owned by **root**
- Normal users **cannot write there**

Check user:
- `whoami`

📌 Only root can create or modify system directories.

---

## 🧠 Summary of Commands Learned

| Command | Purpose |
|------|--------|
| `touch` | Create empty file |
| `cp` | Copy file to create new file |
| `vi` / `vim` | Create/edit file |
| `mkdir` | Create directory |
| `ls -l` | Verify files/directories |
| `ls -ltr` | View files by time |
| `whoami` | Check logged-in user |
| `pwd` | Check current directory |

---

## 📝 Practice Homework (Highly Recommended)

1. Create files using `touch`
2. Create files using `cp`
3. Create one file using `vi`
4. Create multiple files in one command
5. Create directories using `mkdir`
6. Try creating a file in `/etc` (observe error)

📌 Errors teach you permissions faster than theory.
---
🔗 Hands-on Lab: Creating Files (Linux):: [Creating Files – Linux](https://github.com/ezabyss/Complete-Linux-Training-notes/tree/main/01-Linux-Foundation-and-Basic-System-Administration/03-System-Access-and-File-System/labs/04-Creating-Files)

---

## ✅ One-Line Summary

> Linux files can be created using `touch`, `cp`, or `vi`, while directories are created using `mkdir`, and permissions control where files can be created.

---

**✍️ Notes By Abhishek (Ez Abyss)**
