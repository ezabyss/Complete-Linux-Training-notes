# ⚡ Linux `alias` Command
### Create Shortcuts for Long Commands

---

# 🎯 Why Aliases Matter

In Linux, many commands are:

- long
- repetitive
- hard to remember

Example:

`ls -al`

You type it **many times daily**.

Instead of typing full commands → use **aliases (shortcuts)**.

---

# 📌 What is an Alias?

An alias is a **short name for a long command**.

Think of it like:

- nickname
- shortcut
- custom command

---

# 🧠 Simple Explanation

Instead of:

`ls -al`

Create shortcut:

`alias l='ls -al'`

Now just type:

`l`

---

# 🌍 Real World Analogy

Just like:
- Marshal Mathers -> **Eminem**
- Curtis James → **50 Cent**

Linux command:

- `ls -al` → **`l`**

---

# 🧪 Basic Alias Syntax


`alias name='command'`


---

# 🧪 Example 1: List Files

Create alias:

`alias l='ls -al'`

Run:

`l`

Output → same as:

`ls -al`

---

# 🧪 Example 2: Multiple Commands

Create alias:

`alias pl='pwd; ls'`

Run:

`pl`

Output:

- current directory
- list of files

---

# 🧪 Example 3: Show Only Directories

Command:

`ls -l | grep '^d'`

Alias:

`alias dir='ls -l | grep ^d'`

Run:

`dir`

Shows only directories.

---

# 🧪 Example 4: Disk Usage Shortcut

Command:

`df -h | awk '{print $6}' | cut -c1-4`

Alias:

    alias d='df -h | awk "{print $6}" | cut -c1-4'


⚠️ Note:

- Use `\` before `$`
- Prevents variable interpretation

---

# 🧠 Special Character Tip

When using `$` inside alias:

Use:

`\$`

Example:

`awk "{print $6}"`


---

# 🔍 View All Aliases

Run:

`alias`

Shows all active aliases.

---

# ❌ Remove Alias

Syntax:

`unalias name`

Example:

`unalias l`

---

# ⚠️ Important Note

Aliases are **temporary**.

They disappear when:

- you log out
- terminal closes

---

# 💾 Make Aliases Permanent

Add aliases to:

`~/.bashrc`

Example:

```
alias l='ls -al'
alias pl='pwd; ls'
```

Then apply:

`source ~/.bashrc`

---

# 🌍 Real System Admin Use Cases

### 🔹 Quick Navigation

`alias h='cd ~'`

---

### 🔹 Frequent Commands

`alias update='dnf update -y'`

---

### 🔹 Safety Commands

`alias rm='rm -i'`

(prevents accidental deletion)

---

### 🔹 Monitoring Shortcut

`alias disk='df -h'`

---

# 📊 Why Aliases Are Powerful

| Benefit | Explanation |
|------|------|
| Save time | fewer keystrokes |
| Reduce errors | no need to remember long syntax |
| Improve productivity | faster workflow |
| Customize Linux | personalized commands |

---

# 🧠 Quick Questions

### What is an alias?

A shortcut for a command.

---

### How do you create an alias?

`alias name='command'`

---

### How to remove an alias?

`unalias name`

---

### Where to store permanent aliases?

`~/.bashrc`

---

# 🏁 Key Takeaways

- Aliases simplify long commands
- Improve speed and efficiency
- Widely used by **system administrators**
- Easy to create and manage
- Essential for daily Linux usage

---

# 🚀 Pro Tip

Creating your own **custom toolkit** of aliases:

- navigation
- monitoring
- automation

This is how professionals work faster than others.

---

**✍️ Notes By Abhishek (Ez Abyss)**
