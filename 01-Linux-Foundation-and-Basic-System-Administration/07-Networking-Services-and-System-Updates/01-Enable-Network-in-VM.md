# 🌐 Linux VM Internet Setup (VirtualBox + VMware)
### Complete Networking Guide for Virtual Machines

---

# 🎯 Why This Matters

Without internet, your VM cannot:

- 📦 install packages (`dnf`, `apt`)
- 🔄 update system
- 🌍 access servers
- 🛠️ perform real-world tasks

👉 Internet = **mandatory for real sysadmin work**

---

# 🧠 Simple Explanation

Your VM is like:

👉 a **separate computer**

To give it internet:

👉 connect it to your real network

---

# 🌍 Real World Analogy

| Device | Role |
|------|------|
| Laptop | Router |
| VM | New device (phone/laptop) |

---

# 🔌 Networking Modes (IMPORTANT)

| Mode | Internet | Use Case |
|------|--------|---------|
| NAT | ✅ | basic internet |
| Bridged | ✅✅ | real network (BEST) |
| Host-only | ❌ | isolated lab |

---

# ⚡ RECOMMENDED: Bridged Mode

👉 Gives VM:

- real IP address
- full network access
- behaves like real machine

---

# 🖥️ VirtualBox Setup

---

## 🧪 Step 1 — Open Settings

- Select VM
- Click **Settings**

---

## 🧪 Step 2 — Network

- Go to **Network tab**

---

## 🧪 Step 3 — Configure Adapter

Set:

`Attached to: Bridged Adapter`

---

## 🧪 Step 4 — Select Interface

Choose:

- WiFi adapter (laptop)
- Ethernet adapter (desktop)

---

## 🧪 Step 5 — Apply

Click:

`OK`

---

# 🖥️ VMware Setup

---

## 🧪 Step 1 — Open VM Settings

- Right-click VM
- Click **Settings**

---

## 🧪 Step 2 — Network Adapter

Select:

`Network Adapter`

---

## 🧪 Step 3 — Choose Mode

Select:

`Bridged (Connect directly to physical network)`

---

## 🧪 Step 4 — Apply

Click:

`OK`

---

# 🔄 Step 6 — Reboot VM

Run:

`reboot`

---

# 🔍 Step 7 — Verify IP Address

Run:

`ip a`

---

# ✅ Expected Output


`192.168.x.x`


👉 Same network as your host machine

---

# 🌐 Step 8 — Test Internet

Run:

`ping google.com`

---

# ✅ Success Output


`64 bytes from ...`


---

# 🔧 Troubleshooting (VERY IMPORTANT)

---

## ❌ No Internet?

### 1. Restart Network

`systemctl restart NetworkManager`

---

### 2. Check IP

`ip a`

No IP? → DHCP issue

---

### 3. Test Direct Connectivity

`ping 8.8.8.8`

- works → DNS issue
- fails → network issue

---

### 4. Fix DNS

Edit:

`/etc/resolv.conf`

Add:


`nameserver 8.8.8.8`


---

### 5. Check Firewall

`systemctl stop firewalld`

(test only)

---

### 6. VMware Specific Fix

- Disable VPN
- Try NAT mode first
- Ensure VMnet is enabled

---

### 7. VirtualBox Specific Fix

- Try different adapter (WiFi/Ethernet)
- Enable **Promiscuous Mode → Allow All**

---

# 🔥 Key Commands

| Command | Purpose |
|------|------|
| `ip a` | show IP |
| `ping google.com` | test DNS |
| `ping 8.8.8.8` | test connectivity |
| `systemctl restart NetworkManager` | restart network |

---

# 🌍 Real SysAdmin Scenario

You need to:

- install tools
- connect to servers
- download updates

👉 No internet = no work

---

# 🧠 Quick Questions

### What is NAT?

VM shares host network.

---

### What is Bridged?

VM gets real IP from network.

---

### Which is better?

👉 Bridged (for real-world labs)

---

### How to test connectivity?

`ping google.com`

---

# 🏁 Key Takeaways

- VM networking is essential
- Bridged mode = real device behavior
- Always verify with `ip a` + `ping`
- Troubleshooting = key skill

---

# 🚀 Pro Tip 

Always run:

```
whoami
hostname
ip a
```

Before doing anything

---

# 💥 Final Mindset

> “If your VM can’t reach the internet,  
> you’re not learning Linux —  
> you’re just staring at it.”

---

**✍️ Notes By Abhishek (Ez Abyss)**
