# 📁 FTP (File Transfer Protocol)

---

# 🎯 1. What is FTP?

**FTP (File Transfer Protocol)** is a **standard network protocol** used to transfer files between computers over a network.

💡 **Simple Understanding:**
> FTP = A rulebook that tells computers how to send and receive files

---

# 🌍 Real-World Example

### 📦 Example: Sending Files Like Courier

- You → sending a package (Client)
- Courier company → rules/process (FTP)
- Friend → receiving package (Server)
- Office gate → Port 21

👉 If the office is closed (no FTP service) → package rejected ❌  
👉 If gate is blocked (firewall) → delivery fails ❌  

---

# 🧠 2. Core Concepts

## 🔹 Protocol
- Set of predefined communication rules
- Defines:
  - Port
  - Format
  - Communication method

---

## 🔹 Default Ports

| Service | Port |
|--------|------|
| FTP | 21 |
| SSH | 22 |
| DNS | 53 |

---

## 🔹 Client vs Server

| Role | Description |
|------|------------|
| Client | Sends request / uploads file |
| Server | Receives and stores file |

---

# 🏗️ 3. FTP Architecture

FTP uses **2 connections**:

### 🔸 Control Connection
- Handles commands & login

### 🔸 Data Connection
- Transfers actual files

💡 Server must run FTP service (`vsftpd`) or connection fails

---

# 🌍 Real-World Example (Architecture)

- Control connection = Talking to courier office 📞  
- Data connection = Actual package delivery 📦  

---

# 🖥️ 4. Lab Setup

- VM1 → Client
- VM2 → FTP Server

---

# ⚙️ 5. FTP Server Setup

## Become root
`su -`

## Check installation
`rpm -qa | grep vsftpd`

## Check internet
`ping www.google.com`

## Install FTP server
`yum install vsftpd`

## Verify install
`rpm -qa | grep vsftpd`

---

## Configuration File

`/etc/vsftpd/vsftpd.conf`

---

## Backup config
`cp /etc/vsftpd/vsftpd.conf /etc/vsftpd/vsftpd.conf.orig`

---

## Edit config
`vi /etc/vsftpd/vsftpd.conf`

### Important changes:

Disable anonymous login:
`anonymous_enable=NO`

Enable upload/download:
`ascii_upload_enable=YES`
`ascii_download_enable=YES`

Set banner:
`ftpd_banner=Welcome to My FTP Server`

Add at end:
`use_localtime=YES`

---

## Start service
`systemctl start vsftpd`

## Enable at boot
`systemctl enable vsftpd`

---

# 🔥 6. Firewall

Lab:
`systemctl stop firewalld`
`systemctl disable firewalld`

Production:
👉 Allow port **21**

---

# 👤 7. User Setup

`useradd username`

---

# 💻 8. FTP Client Setup

`yum install ftp`

---

# 📂 9. File Transfer

Create file:
`touch my_file`

Add content:
`echo "Hello FTP" > my_file`

Get IP:
`ifconfig`

Connect:
`ftp 192.168.1.58`

Login

Binary mode:
`bin`

Progress:
`hash`

Upload:
`put my_file`

Exit:
`bye`

Verify:
`ls -ltr`

---

# 🌍 Real-World Example (File Transfer)

👉 Scenario:

- You send a file "resume.pdf"
- Server stores it

Steps:
1. You go to courier office → `ftp IP`
2. Show ID → login
3. Choose safe packaging → `bin`
4. Send package → `put file`
5. Courier delivers → transfer complete

---

# 🔁 10. Workflow

Client → FTP → Server (Port 21)

---

# ⚠️ 11. Common Errors

| Problem | Fix |
|--------|-----|
| Connection refused | Start vsftpd |
| Login failed | Check credentials |
| Transfer blocked | Allow port 21 |
| File corrupted | Use `bin` |

---

# 🧠 12. Memory Tricks

- 21 → FTP
- vsftpd → server
- ftp → client
- put → upload
- get → download

---

# 🌍 13. Pro Insight

🚨 FTP is NOT secure:
- Sends data in plain text
- Can be intercepted

---

## Better Alternatives

| Protocol | Security |
|----------|--------|
| FTP | ❌ No encryption |
| SFTP | ✅ Secure (SSH) |
| FTPS | ✅ Secure (SSL/TLS) |

---

# 📌 14. Ultra Short Revision

- FTP = file transfer protocol  
- Port = 21  
- Upload = `put`  
- Mode = `bin`  

---

# 🏆 Final Tip

👉 Don’t just read — DO THIS:
- Create 2 VMs
- Transfer file
- Break firewall
- Fix it

---

# ✍️ Notes By Abhishek (Ez Abyss)
