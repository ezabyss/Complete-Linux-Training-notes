# 📘 Linux Lab – Creating Files and Directories

## 🧪 Lab Objective
This lab focuses on fundamental Linux file and directory operations.  
It demonstrates different methods of creating files, organizing directories, viewing files by time, and understanding permission restrictions in system directories.

---

## 🛠️ Environment
- Operating System: Linux
- Shell: Bash
- Working Directory: Home directory (`~`)

---

## 1️⃣ Creating Files Using `touch`

### Purpose
Creates an empty file.

### Example
- `touch abyss`

### Verify
- `ls -l`

📌 If the command returns to the prompt with no error, the file is created successfully.

---

### Creating Multiple Files at Once
- `touch Mountain Kathmandu Nepal`

📌 One command → multiple files created.

---

## 2️⃣ Creating Files Using `cp` (Copy)

### Purpose
Creates a new file by copying an existing file.

### Syntax
- `cp source_file destination_file`

### Example
- `cp Mountain Everest`
- `cp Kathmandu Pokhara`

📌 The destination file contains the same content as the source file.

---

### Verify
- `ls -ltr`

---

## 📋 Viewing Files by Creation Time

### Command
- `ls -ltr`

### Meaning
- `-l` → long listing format  
- `-t` → sort by modification time  
- `-r` → reverse the order  

📌 Oldest files appear at the top and newest files appear at the bottom.

---

## 3️⃣ Creating Files Using `vi / vim`

### Purpose
Creates and edits files interactively.

### Example
- `vi Pokhara`

📌 This opens the `vi` editor.

### To Save and Exit Safely
1. Press `Shift + :`
2. Type `wq!`
3. Press `Enter`

### Verify
- `ls -ltr`

⚠️ **Important**
- `vi` is powerful but can be confusing for beginners
- It will be covered in more detail in a dedicated lab

---

## 📁 Creating Directories Using `mkdir`

### Purpose
Creates directories (folders).

### Example
- `mkdir Nepal`

### Verify
- `ls -ltr`

📌 Directories:
- Start with `d` in `ls -l`
- Often appear in a different color

---

### Creating Multiple Directories at Once
- `mkdir Places Mountains`

📌 One command → multiple directories created.

---

## 🚫 Permission Denied (Important Concept)

### Example
Attempt to create a file inside `/etc`:
- `cd /etc`
- `touch test123`

### Result
❌ `Permission denied`

---

### Why This Happens
- `/etc` is owned by the `root` user
- Normal users do not have permission to write there

### Check Current User
- `whoami`

📌 Only `root` can modify system directories.

---

## ✅ Lab Summary
By completing this lab, I learned:
- Multiple ways to create files in Linux
- How to copy files and preserve content
- How to use `vi` to create and edit files
- How to create single and multiple directories
- How to view files based on time
- Why Linux enforces permission restrictions

---

**✍️ Notes By Abhishek (Ez Abyss)**
