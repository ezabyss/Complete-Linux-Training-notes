# 🌐 Linux Network Files & Commands
### Think Simple 🧠 | Think Security 🛡️

---

# 🎯 Why This Matters

Without network configuration:

- ❌ No internet  
- ❌ No server communication  
- ❌ No remote access  

👉 In cybersecurity → **network = attack surface**

---

# 🧠 Core Idea (Easy)

> “Linux uses files to decide:
> who to talk to, where to go, and how to connect.”

---

# 🏗️ Simple Analogy (Remember Forever)

| File / Concept | Real Life | Meaning |
|---------------|----------|--------|
| `/etc/hosts` | Contact list 📒 | Saved names |
| `/etc/resolv.conf` | Phonebook 🌐 | Find unknown names |
| `/etc/nsswitch.conf` | Rulebook 📜 | Which to check first |
| NetworkManager | Settings app ⚙️ | Controls everything |
| IP | Home address 🏠 | Identity |

---

# 📁 IMPORTANT FILES (VERY IMPORTANT 🚨)

---

# 1️⃣ `/etc/hosts` → 📒 Saved Contacts

---

## 🧠 What It Does

Manually map:

👉 Name → IP

---

## Example

`192.168.1.10 myserver`

---

## Test

`ping myserver`

---

## 🔐 Cybersecurity Risk

- Can redirect traffic  
- Used in phishing  

---

## 🌍 Real Attack

> Hacker edits `/etc/hosts` → google.com → fake server  

---

# 2️⃣ `/etc/resolv.conf` → 🌐 DNS Settings

---

## 🧠 What It Does

Tells system:

👉 “Which DNS server to use”

---

## Example

`nameserver 8.8.8.8`

---

## 🔐 Cybersecurity Risk

- DNS hijacking  
- Traffic redirection  

---

## 🌍 Real Scenario

> Fake DNS → user opens bank → redirected to attacker  

---

# 3️⃣ `/etc/nsswitch.conf` → 📜 Lookup Rules

---

## 🧠 What It Does

Defines:

👉 “Where should I check first?”

---

## Example

`hosts: files dns`

---

## 🧠 Meaning

1. Check `/etc/hosts`  
2. Then DNS  

---

## 💡 Memory

> “Contacts first, Google later”

---

---

# 4️⃣ `/etc/NetworkManager/system-connections/` → ⚙️ Network Settings

---

## 🧠 What It Does

Stores:

- IP address  
- Gateway  
- DNS  
- DHCP / Static  

---

## Example File


`ens33.nmconnection`


---

## 🔐 Cybersecurity Insight

- Wrong config = network failure  
- Attackers may modify config  

---

## 💡 Memory

> “This file gives your system its identity”

---

---

# 🔧 IMPORTANT COMMANDS

---

# 📡 `ping` → “Is it reachable?”

`ping google.com`

---

# 🧠 `ip a` → “What is my IP?”

---

# 🛣️ `ip route` → “Where do I go?”

---

# 🔍 `ss -tuln` → “Which ports are open?”

---

# 🧪 `tcpdump` → “See live traffic”

`tcpdump -i eth0`

---

# 🧪 Basic Check (Always Run)

```
ip a
ip route
ping 8.8.8.8
```

---

# 🔄 How Everything Works Together

---

## Step-by-step:

1. You type:

`ping google.com`

---

2. System checks:

👉 `/etc/nsswitch.conf`

---

3. Then checks:

👉 `/etc/hosts`

---

4. If not found:

👉 `/etc/resolv.conf` (DNS)

---

5. Then:

👉 Gateway sends request  

---

# 🚨 Common Problems

---

## ❌ No Internet

- Wrong gateway  
- DNS missing  
- Interface down  

---

## ❌ Website not opening

- DNS issue  
- `/etc/hosts` wrong  

---

## ❌ Server unreachable

- Port closed  
- Service stopped  

---

# 🔥 Hacker View

1. Scan IP  
2. Check ports  
3. Enter system  
4. Move inside  
5. Hide identity  

---

# 🛡️ Defender View

- Protect DNS  
- Monitor traffic  
- Check configs  
- Close ports  

---

# 🧠 Quick Questions

---

### What is `/etc/hosts`?

Manual name → IP mapping  

---

### What is `/etc/resolv.conf`?

DNS server configuration  

---

### What is `/etc/nsswitch.conf`?

Lookup order rules  

---

### What is NetworkManager?

Controls network settings  

---

# 🏁 Key Takeaways

- `/etc/hosts` = saved names 📒  
- `/etc/resolv.conf` = DNS 🌐  
- `/etc/nsswitch.conf` = rules 📜  
- NetworkManager = control ⚙️  

---

# 💥 Memory Trick

> “Check → Ask → Connect”

```
Check → /etc/hosts
Ask → DNS (/etc/resolv.conf)
Connect → gateway
```

---

# 🚀 Daily Habit

Always run:

```
ip a
ip route
ping 8.8.8.8
```

---

# ⚡ Final Mindset

> “Wrong network config = broken system.”

---

**✍️ Notes By Abhishek (Ez Abyss)**
