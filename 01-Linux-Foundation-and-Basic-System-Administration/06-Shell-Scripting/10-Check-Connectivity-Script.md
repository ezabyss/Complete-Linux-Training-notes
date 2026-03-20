# 🌐 Bash Server Connectivity Monitoring Script
### Ping Automation for System Administrators

---

# 🎯 Why This Script Matters

In real-world environments:

- Companies have **dozens or hundreds of servers**
- You must constantly check:
  - Is server alive?
  - Is network reachable?
  - Is service down?

Even with monitoring tools, **manual + scripted checks are essential**.

---

# 📌 What This Script Does

This script:

- Pings remote server(s)
- Checks if they are reachable
- Returns:
  - ✅ OK (reachable)
  - ❌ NOT OK (unreachable)

---

# 🧠 Core Concepts Used

This script combines:

- `ping` → network check  
- `if-else` → decision making  
- `$?` → command status  
- `for loop` → multiple servers  
- `/dev/null` → clean output  

---

# 🌍 Real World Scenario

Imagine:

- You manage **50+ servers**
- A user says: “Server is down”

Instead of manually checking:

You run a script that instantly tells:


    Server1 → OK
    Server2 → NOT OK
    Server3 → OK


---

# 🔎 Understanding `ping`

Basic command:

`ping -c 1 192.168.1.1`

- `-c 1` → send 1 packet only
- If reachable → success
- If not → failure

---

# 🧠 Understanding Exit Status `$?`

After any command:

`echo $?`

Returns:

| Value | Meaning |
|------|--------|
| `0` | Success |
| `1+` | Failure |

---

# 🧪 Script 1: Single Host Check

Create file:

`vi ping_script.sh`

Script:

```
#!/bin/bash

# This command checks if the ip is reachable or not

ping -c 1 192.168.1.1 > /dev/null
if [ $? -eq 0 ]
then
echo "OK"
else
echo "NOT OK"
fi

```

---

# ⚙️ Make Executable

`chmod +x ping_script.sh`

Run:

`./ping_script.sh`

---

# 🧹 Clean Output Trick

`> /dev/null`

This hides unnecessary output.

Instead of:

`64 bytes from ...`

You only get:

`OK`


---

# 🧪 Script 2: Using Variable (Best Practice)

```
#!/bin/bash

# this script uses host variable to store the ip address which make it reusing much easier.
host="192.168.1.1"

ping -c 1 $host > /dev/null

if [ $? -eq 0 ]
then
echo "$host is OK"
else
echo "$host is NOT OK"
fi
```

---

# 🧠 Why Use Variables?

Instead of repeating IP:

- easier to update
- reusable
- cleaner code

---

# 🧪 Script 3: Multiple Servers (Advanced)

---

## Step 1 — Create Host File

`vi myhosts`

```
192.168.1.1
192.168.1.235
```

---

## Step 2 — Create Script

`vi ping_all.sh`

```
#!/bin/bash
# this scripts loops over the list of ip addresses stored in file name: myhost

hosts_file="/home/user/ps/myhosts"

for ip in $(cat $hosts_file)
do
ping -c 1 $ip > /dev/null

if [ $? -eq 0 ]
then
    echo "$ip is OK"
else
    echo "$ip is NOT OK"
fi

done

```
---

# ⚙️ Run Script

`chmod +x ping_all.sh`

`./ping_all.sh`

---

# 🖥 Example Output

```
192.168.1.1 is OK
192.168.1.235 is NOT OK
```

---

# 📦 Script Flow 

1. Read host list
2. Loop through each IP
3. Ping each IP
4. Check `$?`
5. Print result

---

# 🔥 Pro Tip: Cleaner Loop (Modern Style)

Instead of:

`for ip in \`cat file\``

Use:

```
while read ip
do
ping -c 1 $ip > /dev/null

if [ $? -eq 0 ]
then
    echo "$ip is OK"
else
    echo "$ip is NOT OK"
fi

done < myhosts  # here we pass the file location at the end
```

Better performance and safer.


---

# 🌍 Real System Admin Use Cases

### 🔹 Daily Health Check

Run script via cron:

`crontab -e`

    0 * * * * /home/user/ping_all.sh


Runs every hour.

---

### 🔹 Alert System

Modify script to send alert:

    echo "$ip is DOWN" | mail -s "Server Alert" admin@example.com


---

### 🔹 Monitoring Before Deployment

Check servers before deployment:

- avoids failures
- ensures availability

---

# 🧠 Quick Questions

### What does `$?` represent?

Exit status of last command.

---

### Why use `/dev/null`?

To suppress unnecessary output.

---

### Why use loop in this script?

To handle multiple servers automatically.

---

### What happens if ping fails?

Exit status ≠ 0 → script prints NOT OK.

---

# 🏁 Key Takeaways

- Automates server connectivity checks
- Uses real-world scripting logic
- Combines multiple Bash concepts:
  - loops
  - conditions
  - variables
- Essential for **DevOps & System Admin roles**

This is a **real production-level beginner script**.

---


**✍️ Notes By Abhishek (Ez Abyss)**
