# Linux Lab 01 — File System Navigation (`cd`, `pwd`, `ls`)

## Objective
Practice essential Linux navigation commands to move confidently through the Linux file system.

This lab builds the foundation for log analysis, scripting, and system investigation.

---

## Commands Covered
- `pwd` — print working directory  
- `ls`, `ls -l` — list directory contents  
- `cd` — change directory  
- `cd ..` — move to parent directory  
- `cd /` — go to root directory  
- `cd` — return to home directory  

---

## Lab Tasks

### 1. Identify current user and location
Run `whoami`  
Then run `pwd`

---

### 2. Navigate to the root directory
Run `cd /`  
Verify with `pwd`  
Expected output: `/`

---

### 3. List contents of root
Run `ls -l`  
Observe directories such as `/etc`, `/var`, `/boot`, and `/home`

---

### 4. Navigate to log directory
Run `cd /var/log`  
Verify with `pwd`  
List files using `ls -l`

---

### 5. Move back to root
Run `cd ..`  
Run `cd ..` again  
Verify with `pwd`  
Expected output: `/`

---

### 6. Navigate using absolute path
Run `cd /etc/sysconfig`  
Verify with `pwd`

---

### 7. Return to home directory
Run `cd`  
Verify with `pwd`

Expected:
- `/root` for root user  
- `/home/username` for standard user  

---

## Expected Outcome
- Always know your current directory  
- Navigate efficiently using relative and absolute paths  
- Move through system directories without confusion  

---

## Security Relevance
- Incident response relies on fast log navigation  
- Incorrect paths can lead to wrong conclusions  
- Filesystem awareness is foundation  

---

## Reflection
This lab reinforced how Linux separates movement, location, and visibility.  
Mastering navigation commands removes friction when working with logs, scripts, and system files.

---

**✍️ Notes By Abhishek (Ez Abyss)**
