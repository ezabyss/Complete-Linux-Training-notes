# 📄 Linux File & Directory Properties (Understanding `ls -l`)

> In Linux, **every file and directory has properties** (metadata) that describe *what it is*, *who owns it*, *how big it is*, and *when it was changed*.

Understanding these properties is essential for **navigation, security, and system administration**.

---

## 🪟 Windows vs 🐧 Linux: Understanding “Properties”

### Windows (GUI)
In Windows, you:
- Identify folders by their **icon**
- Right-click → **Properties**
- Instantly see:
  - Type (file/folder)
  - Location
  - Size
  - Owner
  - Created / Modified time
  - Security & permissions

📌 Windows makes properties **visual and clickable**.

---

### Linux (CLI)
In Linux:
- You **cannot rely on icons**
- You must use commands
- Properties are displayed using:
  - `ls -l`

📌 Linux makes properties **explicit and readable**.

---

## 🔍 Viewing File & Directory Properties in Linux

### Basic command
- `ls -l`

This command shows **detailed information** (properties) for each file and directory.

---

## 🧱 `ls -l` Output Structure (Column Breakdown)

Example: ```drwxr-xr-x 2 root root 4096 Mar 10 10:20 Desktop```


Each column has meaning 👇

---

## 1️⃣ File Type (First Character)

| Symbol | Meaning |
|------|--------|
| `d` | Directory |
| `-` | Regular file |
| `l` | Symbolic link |

📌 **Linux does NOT show icons**  
👉 The **first character** tells you what it is.

Example:
- `d` → directory
- `-` → file
- `l` → link

---

## 2️⃣ Number of Links

- For **files** → number of hard links
- For **directories** → number of:
  - Subdirectories
  - Plus `.` (itself)
  - Plus `..` (parent)

📌 Links will be covered in detail later — just know this number is **important internally**.

---

## 3️⃣ Owner (User)

- Shows **who owns** the file or directory

Example:
- `root`
- `ezabyss`

📌 Owner controls the file.

---

## 4️⃣ Group Owner

- Shows **which group** owns the file

Example:
- `root`
- `users`
- `admins`

📌 Groups allow **shared access control**.

---

## 5️⃣ Size

- File size in **bytes**
- For directories → size of directory metadata

📌 Directories don’t show total contents size here.

---

## 6️⃣ Date & Time

- Month
- Day
- Time (or year if old)

📌 Shows **last modification time**, not creation time.

---

## 7️⃣ File / Directory Name

- Actual name of the file or directory

📌 This is what you interact with using `cd`, `cp`, `rm`, etc.

---

## 🧪 Hands-On Example

### Check current user
- `whoami`

### Check current directory
- `pwd`

### List files
- `ls`

### View properties
- `ls -l`

---

## 📁 Directory vs File (Practical Example)

From `ls -l` output:

- `drwxr-xr-x Desktop` → directory
- `-rw-r--r-- somefile` → regular file

### Try entering a file (won’t work)
- `cd somefile`
❌ Error: Not a directory

### Enter a directory (works)
- `cd Desktop`

---

## 🔙 Coming Back
- `cd ..` → go back one level

---

## 🧠 Why File Properties Matter

Using properties, you can determine:
- Is it a file or directory?
- Who owns it?
- Who can access it?
- Is it safe to delete?
- Why access is denied?

📌 **Most Linux problems are solved by reading properties correctly.**

---

## 🧠 Memory Trick

| Question | Look At |
|------|--------|
| File or directory? | First character |
| Who owns it? | Owner column |
| Permissions issue? | Permissions (next lesson) |
| Why can’t I `cd`? | File type |

---

## ✅ Summary

> In Linux, file and directory properties are viewed using `ls -l`, which reveals type, ownership, size, and modification details needed to manage the system effectively.

---

**✍️ Notes By Abhishek (Ez Abyss)**
