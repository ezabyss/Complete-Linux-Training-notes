# 🌐 Linux Networking for Cybersecurity
### Think Like a Hacker 🧠 | Defend Like a SysAdmin 🛡️

---

# 🎯 Why This Matters

Networking is the **entry point of every cyber attack**.

If you understand networking, you can:

- Detect attacks 🚨  
- Prevent intrusions 🔐  
- Analyze traffic 📊  
- Secure systems 🛡️  

---

# 🧠 Core Idea

> “Every cyber attack starts with a network.”

---

# 🏗️ Network = Digital City Analogy

| Component       | Real World        | Cybersecurity Meaning |
|----------------|------------------|----------------------|
| IP Address     | House Address     | Target               |
| Subnet         | Neighborhood      | Attack boundary      |
| Gateway        | Security Gate     | Firewall             |
| Interface      | Door              | Entry point          |
| MAC Address    | Fingerprint       | Device identity      |

---

# 1️⃣ IP Address → 🎯 Target Identifier

### Example
`192.168.1.10`

---

## 🧠 What It Does

- Identifies a device on a network  
- Enables communication  

---

## 🔥 Cybersecurity Use

- Attackers scan IP ranges  
- SOC monitors suspicious IP activity  

---

## 🌍 Real World Attack


`nmap 192.168.1.0/24`


👉 Hacker scanning entire network for targets  

---

# 2️⃣ Subnet Mask → 🧱 Network Boundary

### Example
`255.255.255.0`

---

## 🧠 What It Does

- Separates network and hosts  
- Controls communication scope  

---

## 🔥 Cybersecurity Use

- Limits attack spread  
- Enables segmentation  

---

## 🌍 Real Scenario

> Malware infects one subnet → cannot spread to another (if segmented properly)

---

# 3️⃣ Gateway → 🚪 Security Gate

### Example
`192.168.1.1`

---

## 🧠 What It Does

- Routes traffic outside network  
- Handles incoming responses  

---

## 🔥 Cybersecurity Use

- Firewall location  
- Traffic inspection  

---

## 🌍 Real Scenario

> Gateway blocks malicious traffic  
> **“Unauthorized access denied”**

---

# 4️⃣ Static vs DHCP → 🔐 Identity Control

---

## 🔒 Static IP

- Fixed  
- Used for servers  

---

## 🔄 DHCP

- Dynamic  
- Used for users/devices  

---

## 🔥 Cybersecurity Insight

| Type   | Risk                     |
|--------|--------------------------|
| Static | Easier to track          |
| DHCP   | Harder to trace attacker |

---

## 🌍 Real Attack

> Attacker uses DHCP → changes IP → avoids detection  

---

# 5️⃣ Network Interface → 🚪 Entry Point

### Examples

```
eth0
ens33
wlan0
```

---

## 🧠 What It Does

- Connects system to network  

---

## 🔥 Cybersecurity Risk

- Exposed interface = attack surface  

---

## 🌍 Real Scenario

> Open port = unlocked door  
> Closed port = secured system  

---

# 6️⃣ MAC Address → 🧬 Device Fingerprint

### Example
`00:1A:2B:3C:4D:5E`

---

## 🧠 What It Does

- Unique hardware identity  

---

## 🔥 Cybersecurity Risk

- Can be spoofed  

---

## 🌍 Real Attack


`macchanger -r eth0`


👉 Attacker changes identity to bypass restrictions  

---

# 🔧 Essential Commands

### Check IP Address
`ip a`

### Check Routing
`ip route`

### Test Connectivity
`ping google.com`

### Check DNS
`cat /etc/resolv.conf`

### Check Open Ports
`ss -tuln`

---

# 🧪 Basic Network Check Workflow

```
ip a
ip route
ping 8.8.8.8
```

---

# 🚨 Common Issues (Cyber View)

---

## ❌ No Internet

- Wrong gateway  
- DNS issue  
- Firewall blocking  

---

## ❌ Cannot Reach Server

- Port closed  
- Service down  
- Network blocked  

---

# 🔥 Attack Flow (Understand the Enemy)

---

## Step 1: Scan Network
`nmap target-ip`

---

## Step 2: Find Open Ports
`ss -tuln`

---

## Step 3: Exploit Service

👉 SSH / HTTP / FTP vulnerabilities  

---

## Step 4: Move Laterally

👉 Spread inside subnet  

---

## Step 5: Hide Identity

- Change IP (DHCP)  
- Spoof MAC  

---

# 🛡️ Defense Strategy (Your Role)

---

## 🔐 1. Monitor Traffic

- Logs  
- SIEM (Splunk)  

---

## 🔥 2. Secure Gateway

- Firewall rules  
- Block unwanted traffic  

---

## 🚫 3. Close Ports

`ss -tuln`

---

## 🧱 4. Network Segmentation

- Divide subnets  
- Limit attack spread  

---

## 🧬 5. Track Devices

- IP logs  
- MAC tracking  

---

# 🧠 Quick Questions

---

### What is an IP address?
Unique identifier for a device on a network  

---

### What is subnet mask?
Defines network boundary  

---

### What is gateway?
Routes traffic outside network  

---

### Static vs DHCP?
- Static = fixed  
- DHCP = dynamic  

---

### What is MAC address?
Unique hardware identifier  

---

# 🏁 Key Takeaways

- IP = identity 🎯  
- Subnet = boundary 🧱  
- Gateway = control point 🚪  
- Interface = entry 🔌  
- MAC = fingerprint 🧬  

---

# 💥 Memory Trick

> “Find → Enter → Move → Hide → Attack”


Find → IP scan
Enter → open port
Move → subnet
Hide → MAC/IP
Attack → exploit


---

# 🚀 Pro SysAdmin Habit

Always check:

```
ip a
ip route
ping 8.8.8.8
ss -tuln
```

---

# ⚡ Final Mindset

> “If you understand networking,  
> you understand how attacks happen.”

---

**✍️ Notes By Abhishek (Ez Abyss)**
