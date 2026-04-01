# 🌐 Linux NetworkManager (`nmcli` + `nmtui`)
### Modern Networking ⚡ | Easy Configuration 🚀 | SysAdmin Essential 🧠

---

## 🎯 Why NetworkManager?

In older Linux systems, networking was configured manually using files.

### ❌ Problems with old method:
- Hard to remember  
- Easy to break  
- Time-consuming  

### ✅ NetworkManager solves this:
- Manage interfaces easily  
- Configure IP, Gateway, DNS  
- Control active connections  
- Support bonding / teaming  

---

## 🧠 Core Idea

> “One tool to manage everything instead of many config files.”

---

## 🏗️ Real World Analogy

| Old Way | New Way |
|--------|--------|
| Manual wiring | Control panel |
| More errors | Cleaner setup |
| Time-consuming | Fast & easy |

---

## 📌 What is NetworkManager?

NetworkManager is a Linux service that manages all network configurations.

### 📦 It controls:
- IP Address  
- Gateway  
- DNS  
- Network Interfaces  
- Bonding / Teaming  
- Hostname  

---

## ⚙️ Tools Overview

| Tool | Description |
|------|------------|
| `nmcli` | CLI (powerful & scriptable) |
| `nmtui` | Terminal UI (easy) |
| `nm-connection-editor` | GUI tool |
| `GNOME Settings` | Desktop settings |

---

## 🔍 Step 1: Check Interfaces

```
ip a
```

### Example Output:
```
ens33
ens38
lo
```

### Meaning:
- `ens33` → Primary NIC  
- `ens38` → Secondary NIC  
- `lo` → Loopback  

---

## 🧪 Step 2: Use `nmtui` (Beginner Friendly)

```bash
nmtui
```

### Menu Options:
```text
Edit a connection
Activate a connection
Set system hostname
```

### 👍 Why use `nmtui`?
- Easy to use  
- Menu-based  
- No need to memorize commands  
- Works without GUI  

---

## 🗑️ Step 3: Remove Extra Connection

Inside `nmtui`:

```text
Edit a connection → Select → Delete → Quit
```

### Verify:
```bash
ip a
```

### Expected:
- One interface → has IP  
- Other interface → no IP  

---

## 🔗 Step 4: Create Team Interface

### 👉 Teaming = Advanced bonding alternative

### Purpose:
- Combine NICs  
- Provide redundancy  
- Prevent network failure  

### Steps in `nmtui`:
```text
Edit a connection
Add → Team
Name: team1
Add slaves:
  - ens33
  - ens38
```

### IPv4:
- Use `Automatic` (DHCP)

---

## 🌐 Result

```text
ens33 → no IP
ens38 → no IP
team1 → gets IP
```

👉 Team interface becomes main connection

---

## 🔍 Verification

```bash
ip a
```

### Expected:
```text
Physical NICs → no IP
Team interface → has IP
```

---

## 💻 Step 5: Use `nmcli` (Pro Way)

### Best for:
- Servers  
- SSH  
- Automation  

---

## 📋 Show Devices

```bash
nmcli device
```

---

## 📋 Show Connections

```bash
nmcli connection show
```

---

## 🌐 Step 6: Assign Static IP

```bash
nmcli connection modify ens33 ipv4.addresses 10.253.10.211/24
nmcli connection modify ens33 ipv4.gateway 10.253.10.1
nmcli connection modify ens33 ipv4.dns 8.8.8.8
nmcli connection modify ens33 ipv4.method manual
```

---

## 🧠 Command Breakdown

| Field | Meaning |
|------|--------|
| `ipv4.addresses` | Set IP |
| `ipv4.gateway` | Set gateway |
| `ipv4.dns` | Set DNS |
| `ipv4.method manual` | Static IP |

---

## 🔄 Step 7: Restart Connection

```bash
nmcli connection down ens33
nmcli connection up ens33
```

---

## 🔍 Verify IP

```bash
ip a
```

or

```bash
ip address show ens33
```

---

## ➕ Step 8: Add Secondary IP

```bash
nmcli connection modify ens33 +ipv4.addresses 10.0.0.211/24
```

### Important:
- `+` = add (not replace)

---

## 🧠 Example Output

```text
Primary IP → 10.253.10.211
Secondary IP → 10.0.0.211
```

---

## 🖥️ GUI Tools

### `nm-connection-editor`
```bash
nm-connection-editor
```

### GNOME:
```text
Settings → Network
```

👉 Only works in GUI environment

---

## 🚨 Common Mistakes

### ❌ Wrong Interface
```bash
ip a
```

---

### ❌ Not Restarting
```bash
nmcli connection down ens33
nmcli connection up ens33
```

---

### ❌ IP on Slave Interfaces
✔ Only team/bond should have IP

---

### ❌ Using GUI on SSH
Use:
```bash
nmcli
nmtui
```

---

## 🔥 Pro Tips

- ✔ Use `nmtui` for quick setup  
- ✔ Use `nmcli` for real-world work  
- ✔ Always verify with `ip a`  
- ✔ DHCP → labs  
- ✔ Static IP → servers  
- ✔ Take VM snapshot  

---

## 🧠 Memory Trick

```text
Check → Edit → Apply → Verify
```

---

## ⚡ Quick Commands

```bash
ip a
nmcli device
nmcli connection show
nmtui
nmcli connection modify ens33 ipv4.addresses 192.168.1.100/24
nmcli connection modify ens33 ipv4.gateway 192.168.1.1
nmcli connection modify ens33 ipv4.dns 8.8.8.8
nmcli connection modify ens33 ipv4.method manual
nmcli connection down ens33
nmcli connection up ens33
```

---

## 🏁 Key Takeaways

- NetworkManager simplifies networking  
- `nmtui` = easy  
- `nmcli` = powerful  
- Teaming = redundancy  
- Static IP = easy setup  
- Multiple IPs supported  

---

## 🚀 Final Mindset

> “A top sysadmin doesn’t memorize configs — they master tools.”

---

**✍️ Notes By Abhishek (Ez Abyss)**
