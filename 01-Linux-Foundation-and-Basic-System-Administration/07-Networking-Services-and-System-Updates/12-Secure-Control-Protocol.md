# 🔐 SCP (Secure Copy Protocol)

---

# 🎯 1. What is SCP?

**SCP (Secure Copy Protocol)** is used to **securely transfer files** between systems over a network.

💡 **Simple Understanding:**
> SCP = Secure version of file transfer using SSH

---

# 🌍 Real-World Example

### 📦 Example: Secure Courier Service

- You → sending package (Client)
- Friend → receiving package (Server)
- Courier → SCP
- Security guard → SSH encryption

👉 Difference:
- FTP = normal delivery (no security) ❌  
- SCP = locked + verified delivery ✅  

---

# 🧠 2. Core Concepts

## 🔹 Protocol
- Set of rules computers follow to communicate

---

## 🔹 Port Used

| Protocol | Port |
|---------|------|
| SCP (via SSH) | 22 |

💡 Important:
> SCP uses **SSH (port 22)** — no separate protocol

---

## 🔹 Key Idea

👉 SCP **does NOT have its own protocol**

It **piggybacks on SSH**

---

# 🏗️ 3. SCP Architecture

- Client → Sends file
- Server → Receives file
- Uses:
  - SSH connection
  - Encryption + authentication

---

# 🌍 Real-World Example (Architecture)

- SSH = Secure tunnel 🚇  
- SCP = Package moving inside tunnel 📦  

---

# 🖥️ 4. Lab Setup

- Machine A → Client
- Machine B → Server

Requirement:
- SSH service must be running on server

---

# ⚙️ 5. SCP Workflow

1. Create file on client
2. Use `scp` command
3. Authenticate (username/password)
4. File transferred securely

---

# 💻 6. Step-by-Step Commands

## Step 1: Create file
`touch Mountain`

---

## Step 2: Add content
`vi Mountain`

Example content:
Nepal is full of mountains

---

## Step 3: Check file
`ls -ltr`

---

## Step 4: Get server IP
`ifconfig`

Example:
`192.168.1.58`

---

## Step 5: Transfer file (IMPORTANT)

`scp Mountain username@192.168.1.58:/home/username`

---

## Step 6: Enter password

- First time:
  - Accept fingerprint → type `yes`
- Then enter password

---

## Step 7: Transfer success

Output:
- 100% complete
- File size
- Transfer speed

---

## Step 8: Verify on server

`ls -ltr`

Check content:
`cat Mountain`

---

# 🔁 7. Reverse Transfer (Server → Client)

👉 To download file:

`scp username@192.168.1.58:/home/username/Mountain .`

---

# 🔥 8. Key Commands Summary

| Action | Command |
|------|--------|
| Upload | `scp file user@IP:/path` |
| Download | `scp user@IP:/path/file .` |
| Check files | `ls -ltr` |
| View content | `cat file` |

---

# ⚠️ 9. Common Errors

| Problem | Cause | Fix |
|--------|------|-----|
| Permission denied | Wrong user/password | Check credentials |
| Connection refused | SSH not running | Start SSH |
| Host verification failed | First-time connection | Type `yes` |
| File not found | Wrong path | Check path |

---

# 🧠 10. Memory Tricks

- SCP = Secure Copy
- Uses → SSH
- Port → 22
- `scp` = copy command
- `:` = remote path separator

---

# 🌍 11. FTP vs SCP (IMPORTANT)

| Feature | FTP | SCP |
|--------|-----|-----|
| Security | ❌ No | ✅ Yes |
| Port | 21 | 22 |
| Encryption | ❌ | ✅ |
| Authentication | Basic | Strong |

---

# 🚀 12. Pro Insight

👉 SCP is:
- Simple
- Secure
- Built on SSH

👉 Used in:
- Server backups
- DevOps deployments
- Secure file transfer

---

# 🌍 Real-World Scenario

👉 You are a system admin:

- You need to send logs to remote server
- Data is sensitive

❌ FTP → not safe  
✅ SCP → best choice  

---

# 📌 13. Ultra Short Revision

- SCP = secure file transfer  
- Uses SSH  
- Port = 22  
- Command = `scp`  
- Upload = `scp file user@IP:/path`  

---

# 👉 Practice this:
- Transfer file client → server
- Reverse transfer
- Break SSH → fix it



---

# ✍️ Notes By Abhishek (Ez Abyss)
