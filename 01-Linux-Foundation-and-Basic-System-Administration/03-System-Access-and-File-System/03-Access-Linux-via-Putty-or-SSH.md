# 🔐 Accessing a Linux Machine Using PuTTY and SSH

How to **access a Linux machine remotely** using:
- 🪟 PuTTY (Windows SSH client)
- ⌨️ SSH command-line (native method)

Remote access is a **core Linux skill**, especially in enterprise environments.

---

## 🧠 Big Picture: How Remote Access Works

To connect to a Linux machine remotely, you need:
- A running Linux system
- Network connectivity
- The **IP address** of the Linux machine
- An SSH client (PuTTY or built-in SSH)

📌 Without the IP address, remote access is not possible.

---

## ⚠️ Important Note (Windows Users)

If you are using:
- **Windows 10 or newer**

Then:
- SSH is already built in
- PuTTY is **optional**
- You can connect using the Command Prompt

👉 If you are comfortable using SSH from the command line, you may skip PuTTY.

---

## 🌐 Step 1: Find the IP Address of the Linux Machine

Before connecting remotely, you must know the **IP address** of the Linux system.

### 📍 Why IP Address Matters (Real-World Example)

Think of the IP address like a **house address**:
- Without it, you cannot reach the house
- SSH and PuTTY need this address to connect

---

### 🖥️ Getting IP Address from Linux Console

1. Open the Linux console (VM or physical system)
2. Open the Terminal

Run one of the following commands:

- ifconfig  
- ip addr  

📌 Newer versions of CentOS may not include `ifconfig` by default.

---

### ⚙️ If `ifconfig` Is Missing

Install networking tools (as root):

yum install net-tools

After installation:
- `ifconfig` will be available

---

### 🔍 Identifying the Correct Interface

When you run `ifconfig` or `ip addr`, you may see multiple interfaces.

Common interfaces:
- lo → Loopback (ignore)
- virtual adapters → ignore
- **enp0s3 or eth0** → Primary network interface

📌 The IP address you need is next to this primary interface.

Example:
- 192.168.1.10
- 10.x.x.x

Your IP may differ based on your network/router.

---

## 🪟 Method 1: Access Linux Using PuTTY (Windows Only)

### 🧠 What PuTTY Does

PuTTY allows:
- Windows → Linux remote access
- Command-line only (no GUI)

Used commonly in:
- Legacy environments
- Beginner-friendly SSH access
- Corporate Windows setups

---

### 🛠️ Steps to Connect Using PuTTY

1. Open PuTTY on Windows
2. Enter the Linux IP address in:
   Host Name (or IP address)
3. Ensure:
   Connection Type = SSH
4. Click Open

---

### ⚠️ First-Time Connection Warning

You may see a message:
- “Host key not cached”

This is normal.

Click:
- Accept or Yes

📌 This simply confirms trust for the first connection.

---

### 🔑 Login to Linux

You will be prompted for:
- Username (created during Linux installation)
- Password

After successful login:
- You are connected to Linux via command-line

---

## ⌨️ Method 2: Access Linux Using SSH (Recommended)

This method uses **built-in SSH** and works on:
- Windows 10+
- macOS
- Linux

---

### 🪟 SSH from Windows Command Prompt

1. Open Windows Search
2. Type:
   cmd
3. Press Enter

Verify SSH exists:
- Type `ssh`
- If options appear → SSH is installed

---

### 🔐 Connect Using SSH

Use this format:

ssh <ip-address>

Or specify username:

ssh -l username <ip-address>

Example:
ssh -l user1 192.168.1.10

Enter password when prompted.

---

## 🍎 SSH from macOS or Linux

1. Open Terminal
2. Run:
   ssh -l username <ip-address>
3. Enter password

No extra software needed.

---

## 🧠 Real-World Comparison

### 🖥️ Console Access
- Physical or VM screen
- Requires monitor or VM window
- Rarely used in corporate environments

### 🌐 Remote Access
- Uses SSH
- No physical access required
- Most common method in real jobs

📌 In real companies, **you almost always access Linux remotely**.

---

## 🎯 Key Things to Remember

- SSH is the standard way to access Linux
- PuTTY is just a Windows SSH client
- Windows 10+ does not require PuTTY
- IP address is mandatory
- GUI is rarely used on Linux servers

---

## 🧠 Memory Rule

> PuTTY and SSH do the same job.  
> SSH is the concept. PuTTY is just a tool.

---

## 💼 Who use SSH ??
- Linux system administrator
- Cloud engineer
- DevOps engineer
- Cybersecurity professional

Mastering remote access is **non-negotiable** for Linux careers.

---

✍️ Notes By Abhishek (Ez Abyss)
