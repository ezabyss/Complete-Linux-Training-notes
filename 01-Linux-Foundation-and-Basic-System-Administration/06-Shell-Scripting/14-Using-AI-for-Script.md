# 🤖 AI + Linux Shell Scripting
### Build Scripts Faster with ChatGPT ⚡

---

# 🎯 Why This Matters (VERY IMPORTANT)

Old way ❌:
- Write scripts manually
- Debug for hours
- Search Google repeatedly

New way ✅:
- Ask ChatGPT
- Get script instantly
- Customize + run

---

# 📌 What is AI-Assisted Scripting?

Using ChatGPT to:

- Generate scripts
- Debug scripts
- Improve scripts
- Automate tasks quickly

---

# 🧠 Simple Explanation

Instead of writing:

```
#!/bin/bash
... (50 lines of code)
```

You just ask:

👉 *"Create a backup script in Linux"*

And AI gives you ready-to-use code.

---

# 🌍 Real World Scenario

You are a system admin:

You need to:
- backup directories
- monitor disk usage
- check server status

Instead of spending hours:

👉 Ask ChatGPT → get script → run → done

---

# ⚡ Workflow

1️⃣ Ask clearly  
2️⃣ Copy script  
3️⃣ Paste in file  
4️⃣ Make executable  
5️⃣ Run & test  
6️⃣ Improve with prompts  

---

# 🧪 Example 1 — Backup Script (Basic)

### 🧠 Prompt

"Write a shell script that asks user for directory and backs it up"

---

### 🧑‍💻 Script

```
#!/bin/bash

echo "Enter directory to backup:"
read dir

tar -czf backup.tar.gz "$dir"

echo "Backup completed"

```

---

# 🚀 Example 2 — Advanced Backup Script

### 🧠 Prompt

"Improve script with validation, timestamp, and success message"

---

### 🧑‍💻 Script

```
#!/bin/bash

echo "Enter directory to backup:"
read source_dir

if [ ! -d "$source_dir" ]; then
echo "Directory does not exist!"
exit 1
fi

backup_dir="${source_dir}_backup"
mkdir -p "$backup_dir"

timestamp=$(date +%Y%m%d_%H%M%S)
backup_file="$backup_dir/backup_$timestamp.tar.gz"

tar -czf "$backup_file" "$source_dir"

if [ $? -eq 0 ]; then
echo "Backup successful: $backup_file"
else
echo "Backup failed!"
fi

```

---

# 🌍 Real Output


`Backup successful: documents_backup/backup_20260321_1015.tar.gz`


---

# 🧪 Example 3 — User Info Script

### 🧠 Prompt

"Create script to show user details"

---

### 🧑‍💻 Script

```
#!/bin/bash

echo "User: $(whoami)"
echo "Home: $HOME"
echo "Shell: $SHELL"
echo "Directory: $(pwd)"
echo "Login Time:"
who

```

---

# 🧪 Example 4 — Disk Alert Script

### 🧠 Prompt

"Check disk usage and alert if above 80%"

---

### 🧑‍💻 Script

```
#!/bin/bash

threshold=80

df -h | awk '{print $5 " " $1}' | while read output;
do
usage=$(echo $output | awk '{print $1}' | cut -d'%' -f1)
partition=$(echo $output | awk '{print $2}')

if [ $usage -ge $threshold ]; then
echo "⚠️ Alert: $partition is ${usage}% full"
fi
done
```

---

# ⚡ How to Run Script

### Step 1 — Create file

`vi script.sh`

---

### Step 2 — Paste code

---

### Step 3 — Give permission

`chmod +x script.sh`

---

### Step 4 — Run

`./script.sh`

---

# 🧠 Best Prompting Strategy

### ❌ Bad Prompt

"write script"

---

### ✅ Good Prompt

"Create a bash script that:
- takes user input
- checks directory exists
- creates backup with timestamp
- shows success message"

---

# 🔥 Pro Prompt Formula

👉 Use this:


Create a bash script that:
```
[task]

[conditions]

[output format]

include error handling

```
---

# ⚠️ Important Reality Check

ChatGPT is powerful but:

| Risk | Solution |
|------|--------|
| Wrong logic | Test script |
| Security issue | Review code |
| Syntax errors | Debug |

---

# 🧠 Golden Rule

> NEVER run a script blindly  
> ALWAYS read + understand

---

# 🚀 Pro Tips

### 🔹 Break tasks into steps

Instead of one big script → ask step by step

---

### 🔹 Improve script iteratively

"add logging"  
"add error handling"  
"optimize performance"

---

### 🔹 Use ChatGPT for debugging

Paste error:

👉 "Why is this script failing?"

---

# 🌍 Real SysAdmin Use Cases

- backup automation
- server monitoring
- log analysis
- disk alerts
- user management
- cron jobs

---

# 🧠 Quick Questions

### Why use AI in scripting?

To save time and improve productivity.

---

### What is risk of AI scripts?

May contain errors → must verify.

---

### How to improve AI scripts?

Refine prompts and test outputs.

---

# 🏁 Key Takeaways

- AI speeds up scripting drastically
- ChatGPT = coding assistant
- Always verify before running
- Combine AI + Linux knowledge = POWER

---

# 💥 Final Mindset

> "AI won't replace engineers.  
> Engineers using AI will replace others."


---

**✍️ Notes By Abhishek (Ez Abyss)**
