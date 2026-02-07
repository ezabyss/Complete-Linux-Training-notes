# 📸 Evidence – Linux File & Directory Operations Lab

This directory contains screenshots that verify the successful completion of each lab task.  
All commands were executed inside the user’s home directory unless stated otherwise.

---

## 🧪 Environment Verification
- User: `ezabyss`
- Working Directory: `/home/ezabyss/labs/linux-file-ops`
- Shell: Bash

The commands `whoami` and `pwd` confirm the user identity and working directory before performing any operations.

---

## 📝 Evidence 1: Creating Files using `touch` and `cp`

**Screenshot:** `01-creating-files-using-touch-and-cp.png`

### Commands Executed
- `touch file1`
- `touch file2`
- `cp file1 copiedfile1`
- `cp file2 copiedfile2`
- `ls -l`

### Outcome
- `file1` and `file2` were successfully created using `touch`
- Copies `copiedfile1` and `copiedfile2` were created using `cp`
- `ls -l` confirms correct ownership, permissions, and timestamps

✅ Task completed successfully.

---

## 📝 Evidence 2: Creating a File using `vi`

**Screenshot:** `02-creating-file-using-vi.png`

### Commands Executed
- `vi file-using-vi`
- `ls -l`
>to exit the vi editor press `esc` then type `:wq;` -means write and quit

### Outcome
- File `file-using-vi` was created and edited using the `vi` text editor
- File size confirms content was written successfully
- Ownership and permissions are correctly assigned

✅ Task completed successfully.

---

## 📝 Evidence 3: Creating a Directory using `mkdir` and Organizing Files

**Screenshot:** `03-folder-using-mkdir-and-mv.png`

### Commands Executed
- `mkdir copiedfiles`
- `mv copiedfile1 copiedfiles/`
- `mv copiedfile2 copiedfiles/`
- `ls -l`

### Outcome
- Directory `copiedfiles` was created successfully
- Copied files were organized into the directory using `mv`
- `ls -l` confirms directory permissions and file structure

✅ Task completed successfully.

---

## 📝 Evidence 4: Permission Denied while Creating File in `/etc`

**Screenshot:** `04-permission-denied.png`

### Commands Executed
- `cd /etc`
- `touch ezabyss`

### Outcome
- File creation inside `/etc` was denied
- Error message displayed: `Permission denied`
- Confirms understanding of Linux permission enforcement on system directories

✅ Expected and correct behavior observed.

---

## 🔐 Security Insight
Protected system directories such as `/etc` require elevated privileges.  
Linux enforces these restrictions to prevent unauthorized configuration changes.

---

**Abhishek (Ez Abyss)**
