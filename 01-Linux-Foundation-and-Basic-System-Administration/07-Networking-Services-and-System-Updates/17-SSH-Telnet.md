# 🔐 SSH & Telnet

---

# 🎯 1. What are SSH and Telnet?

SSH and Telnet are **remote access protocols** that allow one computer to connect to another over a network.

They let administrators manage Linux systems **without being physically present**.

---

# 🌍 Real-World Example

Imagine your office has a server in another city.

Instead of traveling there:

- You remotely connect
- Run commands
- Install software
- Restart services

That's exactly what **SSH** does.

---

# 🧠 2. SSH vs Telnet

| Feature | SSH | Telnet |
|----------|------|---------|
| Full Form | Secure Shell | Teletype Network |
| Default Port | **22** | **23** |
| Encryption | ✅ Yes | ❌ No |
| Security | Very Secure | Insecure |
| Authentication | Encrypted | Plain Text |
| Used Today | ✅ Yes | ❌ Rarely |

---

# 🌍 Real-World Example

## Telnet

Like sending a postcard.

Everyone handling it can read the message.

❌ Not secure.

---

## SSH

Like putting your message inside a locked safe.

Only the receiver has the key.

✅ Secure.

---

# ⭐ Rule

Today,

**Always use SSH.**

Telnet is mainly used for:

- Legacy systems
- Network troubleshooting
- Old devices

---

# 🏗️ 3. Client vs Server

Every remote connection has two parts.

## Client

The computer initiating the connection.

Example:

Your laptop.

---

## Server

The computer receiving the connection.

Example:

Linux server in data center.

---

# 🌍 Real-World Example

Think of making a phone call.

You dial someone.

You are the **client**.

The person answering becomes the **server**.

---

# 🔄 Client and Server Can Change

Computer A connects to Computer B.

```
Computer A ----SSH----> Computer B
(Client)              (Server)
```

Later,

Computer B connects back.

```
Computer B ----SSH----> Computer A
(Client)              (Server)
```

The role depends on **who starts the connection**.

---

# 📦 4. Client Package vs Server Package

Most Linux services have two packages.

## Client Package

Used to connect **to another machine**.

Example:

`ssh`

---

## Server Package

Used to **accept incoming connections**.

Example:

`sshd`

---

# 🧠 Easy Memory

```
ssh
 ↓
Client

sshd
 ↓
Server Daemon
```

---

# 🌍 Real-World Example

Imagine WhatsApp.

Your phone:

Client

WhatsApp servers:

Server

Same idea.

---

# 💻 5. Telnet

Check if installed:

`telnet`

If command not found:

Install:

`dnf install telnet`

---

## Why isn't Telnet installed?

Modern Linux distributions disable it by default because:

- No encryption
- Passwords sent as plain text
- Easily intercepted

---

# 🌍 Real-World Example

Logging into your bank account with Telnet would be like shouting your password in a crowded room.

---

# 🔐 6. SSH Client

Use:

`ssh root@192.168.1.12`

Example:

`ssh root@192.168.1.12`

Login:

Enter password.

Now you are connected.

---

# 🌍 Real-World Example

It's like remotely sitting in front of another computer.

Everything you type runs on the remote machine.

---

# 🖥️ 7. Multiple SSH Sessions

You can open multiple SSH sessions simultaneously.

Each one works independently.

Useful for:

- Monitoring logs
- Installing software
- Editing files
- Restarting services

---

# 🔎 8. Check SSH Process

Using `ps`

`ps -ef | grep sshd`

Example output:

```
/usr/sbin/sshd
```

Meaning:

SSH daemon is running.

---

# 🌍 Real-World Example

Think of `sshd` as a receptionist.

When someone knocks,

the receptionist answers.

If the receptionist goes home,

nobody opens the door.

---

# ⚙️ 9. Stop SSH Service

`systemctl stop sshd`

Now SSH server stops accepting new connections.

Existing sessions may continue until closed.

---

# Verify

`ps -ef | grep sshd`

The main daemon should disappear.

---

# 🌍 Real-World Example

Closing your office entrance.

People already inside remain.

New visitors cannot enter.

---

# 🚫 10. What Happens?

Trying to SSH again:

```
Connection refused
```

Why?

No SSH daemon is listening.

---

# ▶️ 11. Start SSH Service

`systemctl start sshd`

Now server accepts connections again.

---

# Verify

`ps -ef | grep sshd`

---

Or

`systemctl status sshd`

Look for:

```
Active: active (running)
```

---

# 🌍 Real-World Example

Opening your office entrance again.

Visitors can now enter.

---

# 📋 12. Common SSH Commands

Connect

`ssh user@IP`

---

Check process

`ps -ef | grep sshd`

---

Check status

`systemctl status sshd`

---

Start service

`systemctl start sshd`

---

Stop service

`systemctl stop sshd`

---

Restart service

`systemctl restart sshd`

---

Enable on boot

`systemctl enable sshd`

---

Disable on boot

`systemctl disable sshd`

---

# 📌 13. SSH Workflow

```
Client
   │
   │ SSH Port 22
   ▼
SSH Server (sshd)
   │
Authenticate
   │
Run Commands
```

---

# 🚨 14. Common Problems

| Problem | Cause | Solution |
|----------|-------|----------|
| Connection refused | SSH service stopped | Start `sshd` |
| Permission denied | Wrong password | Check credentials |
| Timeout | Firewall blocking port 22 | Allow SSH |
| Host unreachable | Network issue | Check IP |

---

# 🔥 15. Why SSH Is Secure

SSH encrypts:

- Passwords
- Commands
- Files
- Output

Nobody between the client and server can read the communication.

---

# 🌍 Real-World Example

SSH is like talking through an encrypted phone call.

Even if someone listens,

they cannot understand the conversation.

---

# 🧠 16. Memory Tricks

Remember:

```
SSH = Secure
Telnet = Old
```

Easy Formula:

```
SSH
↓

Port 22

↓

Encrypted

↓

Safe
```

---

# 💼 17. Questions

## Q1. What is SSH?

SSH (Secure Shell) is a secure protocol used to remotely access Linux systems.

---

## Q2. Default SSH port?

`22`

---

## Q3. Default Telnet port?

`23`

---

## Q4. Why is SSH preferred?

Because it encrypts communication.

---

## Q5. What is `sshd`?

The SSH daemon that accepts incoming SSH connections.

---

## Q6. Difference between ssh and sshd?

`ssh` = Client

`sshd` = Server daemon

---

## Q7. How do you check SSH service?

`systemctl status sshd`

---

## Q8. How do you stop SSH?

`systemctl stop sshd`

---

## Q9. What happens if sshd is stopped?

New SSH connections are refused.

---

## Q10. Which protocol is insecure?

Telnet.

---

# 📌 Ultra Short Revision

- SSH = Secure remote login
- Telnet = Insecure remote login
- SSH Port = 22
- Telnet Port = 23
- Client = `ssh`
- Server = `sshd`
- Start = `systemctl start sshd`
- Stop = `systemctl stop sshd`
- Status = `systemctl status sshd`

---

# 🏆 Takeaway

SSH is one of the **most important Linux administration services**.

Almost every Linux server in production is managed remotely using SSH.

A Linux administrator should know how to:

- Connect using SSH
- Check SSH status
- Start/stop SSH
- Troubleshoot SSH issues
- Understand why SSH is more secure than Telnet

Mastering SSH is one of the first essential skills for every Linux System Administrator.

---

# ✍️ Notes By Abhishek (Ez Abyss)
