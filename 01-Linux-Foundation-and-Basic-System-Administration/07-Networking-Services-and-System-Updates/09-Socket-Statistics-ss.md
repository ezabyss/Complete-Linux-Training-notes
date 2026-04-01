# 🔍 Linux `ss` Command
### Network Monitoring 📡 | Troubleshooting ⚡ | SysAdmin Essential 🧠

---

## 🎯 Why `ss` Command?

When your system is slow or network has issues:

- Server lagging ❌  
- Unknown connections ❌  
- Too many processes ❌  

👉 You need to see **what’s happening in network**

---

## 🧠 Core Idea

> “See all network connections and find problems fast.”

---

## 🌍 General Understanding

Think like this:

- Your computer = a phone 📱  
- Connections = phone calls ☎️  

👉 `ss` shows:
- Who you're talking to  
- How many connections  
- Which app is using network  

---

## 📌 What is `ss`?

`ss` = Socket Statistics

👉 It shows:
- Network connections  
- Ports  
- Processes  
- Data flow  

---

## 🔌 What is a Socket?

> “A socket is like a connection line between two computers.”

---

## 🌐 Types of Sockets

| Type | Meaning | Example |
|------|--------|--------|
| TCP | Reliable | Web, SSH |
| UDP | Fast | Streaming |
| Unix | Local | Same machine |

---

## ⚙️ Basic Command

```bash
ss
```

👉 Shows all active connections

---

## 📊 Output Columns

| Column | Meaning |
|--------|--------|
| Netid | Protocol (TCP/UDP) |
| State | Connection status |
| Recv-Q | Data waiting to receive |
| Send-Q | Data waiting to send |
| Local Address | Your system |
| Peer Address | Remote system |

---

## 🔍 Common Options

### 1. Show TCP only
```bash
ss -t
```

---

### 2. Show UDP only
```bash
ss -u
```

---

### 3. Show Unix sockets
```bash
ss -x
```

---

### 4. Show Listening ports
```bash
ss -l
```

---

### 5. Combine filters
```bash
ss -tln
```

👉 Meaning:
- `-t` = TCP  
- `-l` = Listening  
- `-n` = Numeric  

---

## 🧪 Example

```bash
ss -tln
```

👉 Shows:
- Open TCP ports  
- Services waiting for connections  

---

## 🌐 Real Scenario

👉 SSH connection:

- Uses TCP  
- Shows as ESTABLISHED  

👉 DHCP:

- Uses UDP  

---

## 🚨 Troubleshooting Use

| Problem | Use |
|--------|-----|
| Server slow | Check active connections |
| Port not working | Check listening ports |
| Unknown traffic | Check processes |

---

## 🔥 Pro Tips

- ✔ Use `ss -tln` to check open ports  
- ✔ Use `ss -u` for UDP issues  
- ✔ Combine options for better filtering  
- ✔ Faster than old `netstat`  

---

## 🧠 Memory Trick

```text
Check Connections → Filter → Analyze
```

---

## ⚡ Quick Commands

```bash
ss
ss -t
ss -u
ss -x
ss -l
ss -tln
```

---

## 🏁 Key Takeaways

- `ss` = network inspection tool  
- Shows connections + ports  
- Helps in troubleshooting  
- Replaces `netstat`  

---

## 🚀 Final Mindset

> “You can’t fix the network if you can’t see it.”

---

**✍️ Notes By Abhishek (Ez Abyss)**
