# File Comparison in Linux — `diff` and `cmp`

When working in Linux (especially in security, DevOps, or system administration), 
you often need to compare two files.

Examples:
- Compare configuration backups
- Verify if logs changed
- Detect tampering
- Compare exported data files

Linux provides two powerful commands:

- `diff` → line-by-line comparison  
- `cmp` → byte-by-byte comparison  

---

# 1️⃣ `diff` — Line-by-Line Comparison

## What it does
`diff` compares two files and shows:
- Which lines are different
- Where the differences occur

It is **human-readable** and great for text files.

---

## Example Setup

Create first file:

`echo "Pokhara" > Places.txt`  
`echo "Kathmandu" >> Places.txt`  
`echo "Dang" >> Places.txt`

Create second file:

`echo "Pokhara" > Places2.txt`  
`echo "Kathmandu" >> Places2.txt`  
`echo "Butwal" >> Places2.txt`

Check contents:

`cat Places.txt`  
`cat Places2.txt`

---

## Compare Using `diff`

`diff Places.txt Places2.txt`

### Example Output Format
It may show something like:

`3c3`  
`< Dang`  
`---`  
`> Butwal`

Meaning:
- Line 3 changed
- First file has "Dang"
- Second file has "Butwal"

---

## Useful `diff` Options

| Option | Meaning |
|--------|----------|
| `-y` | Side-by-side comparison |
| `-i` | Ignore case |
| `-w` | Ignore whitespace |
| `-q` | Only report if files differ |

Example:

`diff -y Places.txt Places2.txt`

---

# 2️⃣ `cmp` — Byte-by-Byte Comparison

## What it does
`cmp` compares files at the **binary level**.

It tells:
- First byte where files differ
- Exact location of difference

This is useful for:
- Verifying file integrity
- Checking binary files
- Detecting small hidden changes

---

## Basic Usage

`cmp Places.txt Places2.txt`

Example output:

`Places.txt Places2.txt differ: byte 19, line 3`

This means:
- Files differ at byte 19
- The difference is in line 3

---

## Useful `cmp` Options

| Option | Meaning |
|--------|----------|
| `-l` | Show all differing bytes |
| `-s` | Silent mode (useful in scripts) |

Example:

`cmp -l file1 file2`

---

# When to Use Which?

| Use Case | Command |
|-----------|---------|
| Compare config files | `diff` |
| Compare logs | `diff` |
| Compare source code | `diff` |
| Verify file integrity | `cmp` |
| Compare binary files | `cmp` |

---

# Real Security Example

Check if a config file was modified:

`diff /etc/ssh/sshd_config backup-sshd_config`

Check if a binary was altered:

`cmp original.bin suspicious.bin`

---

# Quick Comparison

`diff` → human-readable  
`cmp` → machine-level comparison  

Think:

- `diff` = "What changed?"
- `cmp` = "Exactly where did it change?"

---

# Pro Tip (SOC / Security Use)

To quickly check if files differ:

`diff -q file1 file2`

If no output → files are identical  
If output appears → files differ  

---

# Final Thought

File comparison is essential for:
- Auditing
- Change tracking
- Incident response
- Backup validation
- Configuration management

Mastering `diff` and `cmp` gives you strong troubleshooting power in Linux.

---

**✍️ Notes By Abhishek (Ez Abyss)**  
