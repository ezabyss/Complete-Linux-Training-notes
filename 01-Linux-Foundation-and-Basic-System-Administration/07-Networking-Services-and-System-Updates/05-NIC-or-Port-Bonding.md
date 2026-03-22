# 🔗 Linux NIC Bonding (VMware)
### High Availability ⚡ | Load Balancing 🚀 | SysAdmin Essential 🧠

---

# 🎯 Why NIC Bonding?

NIC Bonding combines multiple network interfaces into **one logical interface**.

👉 Purpose:
- Increase **network reliability** 🛡️  
- Improve **performance** ⚡  
- Prevent **network failure** ❌  

---

# 🧠 Core Idea

> “Multiple cables → One strong connection”

---

# 🏗️ Real World Analogy

| Concept | Real World | Meaning |
|--------|-----------|--------|
| Single NIC | One road | If blocked → no access ❌ |
| Bonded NICs | Multiple roads | If one fails → others work ✅ |

---

# 📌 What is NIC Bonding?

NIC Bonding = Combining multiple interfaces like:

```
ens33 + ens34 → bond0
```

👉 Result:
- `bond0` = main interface  
- `ens33`, `ens36` = slave interfaces  

---

# 🧪 Lab Setup (VMware)

## 🖥️ Step 1: Add Network Adapters

👉 In VMware:
- Add **2 Network Adapters**
- Set both to **Bridged**

---

# 🔍 Step 2: Verify Interfaces


`ip a`


👉 Example:
```
ens33
ens34
```

---

# ⚙️ Step 3: Create Bond Interface

```
nmcli connection add type bond con-name bond0 ifname bond0 mode active-backup
```

---

# 🔗 Step 4: Add Slave Interfaces

```
nmcli connection add type ethernet slave-type bond con-name bond-slave-ens33 ifname ens33 master bond0

nmcli connection add type ethernet slave-type bond con-name bond-slave-ens34 ifname ens34 master bond0
```

---

# 🌐 Step 5: Assign IP to Bond

```
nmcli connection modify bond0 ipv4.addresses 192.168.1.94/24
nmcli connection modify bond0 ipv4.gateway 192.168.1.1
nmcli connection modify bond0 ipv4.method manual
```

---

# 🚨 IMPORTANT FIX (Common Mistake)

👉 Remove IP from physical interfaces:

```
nmcli connection modify ens33 ipv4.method disabled
nmcli connection modify ens34 ipv4.method disabled
```

👉 Restart everything:

```
nmcli connection down ens33 && nmcli connection up ens33
nmcli connection down ens34 && nmcli connection up ens34
nmcli connection down bond0 && nmcli connection up bond0
```

---

# 🔍 Verification

## Check Interfaces

`ip a`


✔️ Expected:
- `bond0` → has IP  
- `ens33` → NO IP + SLAVE  
- `ens34` → NO IP + SLAVE  

---

## Deep Check

```
cat /proc/net/bonding/bond0
```

✔️ Output:
```
Slave Interface: ens33
Slave Interface: ens34
```

---

# 🧠 Bonding Modes

| Mode | Name | Use Case |
|------|------|--------|
| 0 | round-robin | Performance 🚀 |
| 1 | active-backup | High availability 🛡️ |
| 4 | 802.3ad (LACP) | Enterprise ⚡ |

---

# 🌍 Real World Scenario

👉 A server has **2 NICs**

- Cable 1 fails ❌  
- Bond switches to Cable 2 ✅  

✔️ No downtime  
✔️ No data loss  

---

# 🚨 Troubleshooting

## ❌ Cannot SSH

Check:
```
ip a
systemctl status NetworkManager
```

---

## ❌ Bond not working


`nmcli connection show`


👉 Ensure slaves are attached

---

## ❌ One NIC still has IP


`nmcli connection modify ens33 ipv4.method disabled`


---

# 🔥 Pro Tips

✔️ Assign IP to **bond0 only**  
✔️ Slaves must NOT have IP  
✔️ Use `active-backup` for beginners  

---

# 🧠 Memory Trick


Create → Attach → Remove IP → Activate → Verify


---

# ⚡ Quick Commands Cheat Sheet

```
ip a
nmcli connection show
nmcli connection up bond0
cat /proc/net/bonding/bond0
```

---

# 🏁 Key Takeaways

- Bonding = reliability + performance  
- bond0 = main interface  
- ens33/ens34 = slaves  
- Only bond gets IP  

---

# 🚀 Final Mindset

> “Real sysadmins don’t trust one network path.”

---

**✍️ Notes By Abhishek (Ez Abyss)**
