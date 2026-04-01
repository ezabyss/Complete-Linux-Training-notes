# 🌐 Linux Networking Troubleshooting (`ping` + `curl`)
### Connectivity Check 📡 | Web Testing 🌍 | SysAdmin Essential 🧠

---

## 🎯 Why Do We Need These Commands?

When something is not working:

- Server down ❌  
- Website not opening ❌  
- Network issue ❌  

👉 First step = **Check connectivity**

---

## 🧠 Core Idea

> “First check if the system is reachable, then check if the service is working.”

---

## 🌍 General Understanding

Think like this:

- `ping` = “Is the system alive?” 💓  
- `curl` = “Is the website working?” 🌐  

---

# 📡 1. `ping` Command

## 📌 Purpose
Check if another system is reachable

---

## ⚙️ Syntax

```bash
ping <hostname or IP>
```

---

## 🧪 Example

```bash
ping google.com
```

---

## 🧠 What Happens?

```text
Your Machine → Target Server → Response
```

---

## ✅ Output Meaning

- Reply received → Server is UP ✅  
- No reply → Server DOWN / Network issue ❌  

---

## 🔍 Example Output

```text
64 bytes from 216.58.x.x: time=20ms
```

👉 Means:
- Server reachable  
- Network working  

---

## 🧠 Key Use

- Check network connectivity  
- Verify server is alive  
- Get IP from hostname  

---

# 🌐 2. `curl` Command

## 📌 Purpose
Check if a website/service is working

---

## ⚙️ Syntax

```bash
curl <URL>
```

---

## 🧪 Example

```bash
curl https://google.com
```

---

## 🧠 What Happens?

- Sends request to website  
- Returns HTML/content  

---

## ✅ Output Meaning

- HTML shown → Website is UP ✅  
- No response → Website issue ❌  

---

## 📥 Download with `curl`

```bash
curl -O <URL>
```

---

## 🧪 Example

```bash
curl -O https://example.com/file.tar.gz
```

---

## 📂 Check File

```bash
ls -l
```

---

# 🔥 `ping` vs `curl`

| Command | Checks |
|--------|--------|
| `ping` | Server/network |
| `curl` | Website/service |

---

# 🌍 Real Scenario

👉 Problem: Website not opening

Step 1:
```bash
ping google.com
```
✔ If fail → network issue  

Step 2:
```bash
curl google.com
```
✔ If fail → web service issue  

---

# 🌉 VMware Tip

- Bridged Adapter → Internet works ✅  
- Host-only → No internet ❌  

---

# 🚨 Common Mistakes

## ❌ Ping works but website not loading
👉 Server is up, but web service down  

---

## ❌ curl fails
👉 Check:
- Internet
- Firewall
- DNS  

---

## ❌ No response in ping
👉 Check:
```bash
ip a
ping 8.8.8.8
```

---

# 🔥 Pro Tips

- ✔ Use `ping` first (basic check)  
- ✔ Use `curl` for web testing  
- ✔ Use IP if DNS fails  
- ✔ Combine with `wget` for downloads  

---

# 🧠 Memory Trick

```text
Ping → Curl → Fix
```

---

# ⚡ Quick Commands

```bash
ping google.com
ping 8.8.8.8
curl google.com
curl -O <URL>
ls -l
ip a
```

---

# 🏁 Key Takeaways

- `ping` = network check  
- `curl` = website check  
- Both are troubleshooting tools  
- Essential for sysadmins  

---

# 🚀 Final Mindset

> “First check the network, then check the service.”

---

**✍️ Notes By Abhishek (Ez Abyss)**
