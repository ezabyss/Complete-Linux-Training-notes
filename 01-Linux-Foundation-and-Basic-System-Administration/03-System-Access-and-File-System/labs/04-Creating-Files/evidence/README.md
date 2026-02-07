# 📸 Evidence – Creating Files and Directories (Linux Lab)

This directory contains screenshots that verify the successful execution of Linux file and directory operations.
All commands were executed by the user `ezabyss` from the home directory (`~`) unless stated otherwise.

---

## 🧪 Environment Verification
- User: `ezabyss`
- Home Directory: `/home/ezabyss`
- Shell: Bash

---

## 1️⃣ Creating Files Using `touch`

**Screenshot:** `01-creating-files-using-touch.png`

### Commands Executed
- `touch abyss`
- `touch Mountain Kathmandu Nepal`
- `ls -l`

### Outcome
- An empty file named `abyss` was created
- Multiple files (`Mountain`, `Kathmandu`, `Nepal`) were created using a single command
- `ls -l` confirms file ownership, permissions, and timestamps

📌 Successful creation with no errors confirms correct usage of `touch`.

---

## 2️⃣ Creating Files Using `cp` (Copy)

**Screenshot:** `02-creating-file-using-cp.png`

### Commands Executed
- `cp Mountain Everest`
- `cp Kathmandu Pokhara`
- `ls -ltr`

### Outcome
- New files `Everest` and `Pokhara` were created by copying existing files
- `ls -ltr` shows the copied files appearing later in the time-sorted list

📌 Destination files inherit the content of their source files.

---

## 3️⃣ Creating Files Using `vi`

**Screenshot:** `03-creating-file-using-vi.png`

### Commands Executed
- `vi Dang`
- `ls`
- `ls -ltr`

### Outcome
- File `Dang` was created and edited using the `vi` editor
- File size confirms content was written successfully
- `ls -ltr` shows `Dang` as one of the most recently modified files

📌 Demonstrates interactive file creation and editing.

---

## 4️⃣ Creating Directories Using `mkdir`

**Screenshot:** `04-folder-using-mkdir.png`

### Commands Executed
- `mkdir Nepal`
- `mkdir Places Mountains`
- `ls -ltr`

### Outcome
- Directories `Nepal`, `Places`, and `Mountains` were created
- `ls -ltr` shows directories marked with `d` at the beginning of permissions

📌 Confirms correct directory creation using `mkdir`.

---

## 5️⃣ Permission Denied (System Directory Protection)

**Screenshot:** `05-permission-denied.png`

### Commands Executed
- `cd /etc`
- `touch test1`
- `whoami`

### Outcome
- File creation inside `/etc` was denied
- Error message displayed: `Permission denied`
- `whoami` confirms the user is not `root`

📌 Demonstrates Linux permission enforcement on system-owned directories.

---

## ✅ Evidence Summary
This evidence confirms:
- File creation using `touch`, `cp`, and `vi`
- Viewing files using time-based sorting with `ls -ltr`
- Directory creation using `mkdir`
- Understanding of Linux permission restrictions in `/etc`

---

**✍️ Notes By Abhishek (Ez Abyss)**
