# 🛣️ Linux File System Paths (Absolute vs Relative)

> To navigate efficiently in Linux, you must understand **file system paths**.  
> Linux provides **two ways** to reach any directory or file.

---

## 🎯 What Is a File System Path?

A **path** is the route Linux uses to locate a file or directory inside the file system.

There are **two types of paths**:
1. Absolute Path
2. Relative Path

---

## 1️⃣ Absolute Path

### 🔹 Definition
An **absolute path**:
- **Always starts with `/`**
- Begins from the **root directory**
- Works from **any location**

📌 Absolute paths are **independent of where you currently are**.

---

### 🔹 Example (Absolute Path)

Go directly to the Samba logs directory:
- `cd /var/log/samba`

Check location:
- `pwd`

Output:
- `/var/log/samba`

📌 No matter where you are, this command will always work.

---

### 🔹 When to Use Absolute Path
- When you know the **exact location**
- When writing **scripts**
- When avoiding navigation mistakes
- When working as **root**

---

## 2️⃣ Relative Path

### 🔹 Definition
A **relative path**:
- **Does NOT start with `/`**
- Is relative to your **current directory**
- Depends on where you are now

📌 Relative paths are **shorter but context-dependent**.

---

### 🔹 Example (Relative Path)

Step 1: Go to `/var`
- `cd /var`

Step 2: Go to `log`
- `cd log`

Step 3: Go to `samba`
- `cd samba`

Check location:
- `pwd`

Output:
- `/var/log/samba`

📌 Notice: No `/` at the beginning.

---

## ⚠️ Common Mistake (Very Important)

If you are in `/` and run:
- `cd /log`

❌ This fails because:
- `/log` does not exist at root level

✅ Correct way:
- `cd var`
- `cd log`

or use absolute path:
- `cd /var/log`

---

## 🧠 Absolute vs Relative

| Feature | Absolute Path | Relative Path |
|------|--------------|--------------|
| Starts with `/` | Yes | No |
| Depends on current location | No | Yes |
| Works from anywhere | Yes | No |
| Safer for scripts | Yes | No |
| Faster for short navigation | No | Yes |

---

## 🧭 Moving Up the Directory Tree

### Go back one level:
- `cd ..`

### Go back multiple levels:
- `cd ..`
- `cd ..`

📌 `..` means **parent directory**

---

## 🧪 Practical Navigation Example

### Absolute Path
- `cd /etc/sysconfig/network-scripts`

Check:
- `pwd`

Output:
- `/etc/sysconfig/network-scripts`

---

### Relative Path
- `cd /etc`
- `cd sysconfig`
- `cd network-scripts`

Check:
- `pwd`

Output:
- `/etc/sysconfig/network-scripts`

---

## ⌨️ Productivity Tip: Tab Completion

Press:
- `Tab`

Linux will:
- Auto-complete directory names
- Reduce typing errors
- Speed up navigation

📌 Use `Tab` **all the time** — professionals do.

---

## 🧠 Memory Trick

Think of paths like addresses:

- **Absolute path** → Full home address  
- **Relative path** → Directions from where you’re standing

---

## ✅ In One-Line

> An absolute path starts from `/` and works from anywhere, while a relative path depends on the current directory and does not begin with `/`.

---

**✍️ Notes By Abhishek (Ez Abyss)**
