# 🛠️ Ultimate Linux Troubleshooting Guide
### `ping` + `curl` + `wget` + `ss` 🚀 | SysAdmin Playbook 🧠

---

## 🎯 Goal

When something breaks (server, website, network):

👉 Follow a **clear step-by-step process**

---

## 🧠 Core Mindset

> “Check connectivity → Check service → Check download → Check connections”

---

# 🔄 Troubleshooting Flow

```text
1. ping → Is system reachable?
2. curl → Is website/service working?
3. wget → Can I download from source?
4. ss → What connections are active?
```

---

# 📡 STEP 1: `ping` (Network Check)

## Purpose:
Check if server is alive

```bash
ping google.com
```

## Result:
- ✅ Reply → Network OK  
- ❌ No reply → Network issue  

---

# 🌐 STEP 2: `curl` (Service Check)

## Purpose:
Check if website/service is running

```bash
curl https://google.com
```

## Result:
- ✅ HTML output → Service working  
- ❌ No response → Service down  

---

# 📥 STEP 3: `wget` (Download Check)

## Purpose:
Check if file can be downloaded

```bash
wget https://example.com/file.tar.gz
```

## Result:
- ✅ Download works → Source OK  
- ❌ Fail → URL / network issue  

---

# 🔍 STEP 4: `ss` (Connection Check)

## Purpose:
Check active connections and ports

```bash
ss -tln
```

## Result:
- Shows open ports  
- Shows listening services  

---

# 🧠 Simple Understanding

| Command | Meaning |
|--------|--------|
| ping | Is server alive? |
| curl | Is website working? |
| wget | Can I download file? |
| ss | What connections exist? |

---

# 🌍 Real Troubleshooting Example

## Problem: Website not loading

### Step 1:
```bash
ping google.com
```
❌ Fail → Network issue  

---

### Step 2:
```bash
curl google.com
```
❌ Fail → Web server down  

---

### Step 3:
```bash
wget https://google.com
```
❌ Fail → Internet issue  

---

### Step 4:
```bash
ss -tln
```
👉 Check if service is listening  

---

# 🚨 Common Issues

## ❌ Ping works but curl fails
👉 Server alive, service down  

---

## ❌ wget fails
👉 Wrong URL or blocked  

---

## ❌ ss shows no listening port
👉 Service not running  

---

## ❌ No ping response
👉 Network/firewall issue  

---

# 🔥 Pro Tips

- ✔ Always start with `ping`  
- ✔ Use `curl` for web debugging  
- ✔ Use `wget` for downloads  
- ✔ Use `ss` for deep analysis  
- ✔ Use IP if DNS fails  

---

# 🧠 Memory Trick

```text
Ping → Curl → Wget → SS
```

---

# ⚡ Quick Commands

```bash
ping google.com
curl google.com
wget <URL>
ss -tln
ip a
```

---

# 🏁 Key Takeaways

- Troubleshooting = step-by-step process  
- Each command checks different layer  
- Combine tools for best results  

---

# 🚀 Final Mindset

> “Don’t guess — test layer by layer.”

---

**✍️ Notes By Abhishek (Ez Abyss)**
