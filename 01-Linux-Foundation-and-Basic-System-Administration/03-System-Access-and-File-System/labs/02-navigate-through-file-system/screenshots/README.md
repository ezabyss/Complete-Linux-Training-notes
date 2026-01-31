# Linux Lab 01 — File System Navigation

This README documents the **command-line evidence** collected during Linux Lab 01.  
Each screenshot demonstrates correct usage of core Linux navigation commands used in SOC and system investigation workflows.

---

## Environment Details
- Hostname: `localhost`
- User: `ezabyss`
- Shell: Linux Bash
- Interface: CLI (Terminal)

---

## Screenshot Evidence

### Screenshot 1 — Root Directory Enumeration
**File:** `1-ls-root.png`

**Commands Executed:**
- `whoami`
- `pwd`
- `cd /`
- `ls -l`

**What This Shows:**
- User identity confirmed as `ezabyss`
- Successful navigation to the root directory `/`
- Enumeration of core Linux directories such as:
  - `/etc`
  - `/var`
  - `/boot`
  - `/home`
  - `/usr`

**SOC Relevance:**
- Root directory awareness is essential before accessing logs or system files
- Prevents accidental operations in incorrect locations

---

### Screenshot 2 — Log Directory Enumeration
**File:** `2-ls-log.png`

**Commands Executed:**
- `cd /var/log`
- `ls -l`

**What This Shows:**
- Successful navigation to `/var/log`
- Visibility of key log files including:
  - `messages`
  - `secure`
  - `boot.log`
  - `cron`
  - `vmware` logs

**SOC Relevance:**
- `/var/log` is a primary source of evidence during incident response
- Log enumeration is a foundational skill

---

### Screenshot 3 — Absolute Path Navigation
**File:** `3-cd-sysconfig.png`

**Commands Executed:**
- `cd /etc/sysconfig`
- `pwd`

**What This Shows:**
- Use of absolute paths to reach configuration directories
- Confirmation of correct directory using `pwd`

**SOC Relevance:**
- Configuration files may reveal persistence mechanisms or system misconfigurations
- Absolute paths reduce error during investigations

---

### Screenshot 4 — Returning to Home Directory
**File:** `4-cd-returning-home.png`

**Commands Executed:**
- `cd`
- `pwd`

**What This Shows:**
- Default behavior of `cd` returning the user to their home directory
- Home directory confirmed as `/home/ezabyss`

**SOC Relevance:**
- Home directories may contain scripts, artifacts, or attacker-placed files
- Analysts often pivot between system and user directories

---

**✍️ Notes By Abhishek (Ez Abyss)**
