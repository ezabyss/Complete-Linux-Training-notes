# ⌨️ Bash Input and Output

---

# 🎯 Why Input & Output Matters

In many Linux scripts, you need the script to:

- Ask questions to the user
- Wait for user input
- Use the input in the script
- Display results back to the user

This interaction is called **Input and Output**.

In Bash scripting:

| Purpose | Command |
|------|------|
| Take user input | `read` |
| Display output | `echo` |

---

# 📌 What is Input and Output in Bash?

**Input** → Data provided by the user  
**Output** → Data displayed by the script

Example flow:

```
Script asks question
↓
User types response
↓
Script processes input
↓
Script displays result
```


---

# 🧠 Simple Concept

Think of a script like a **conversation**.

Script:

```
What is your name?
User:
ezabyss
Script responds:
Hello ezabyss

```


This interaction uses:

- `read` → capture user input
- `echo` → display output

---

# 🌍 Real World Scenario

When installing software in Linux or Windows, you see prompts like:

```
Enter your name:
Enter organization:
Do you want to continue? (yes/no)
```

These prompts are implemented using **input/output scripting logic**.

The system collects information and stores it in **variables**.

---

# 🧪 Basic Input Output Script

Create a script:

`vi input_script.sh`

Example script:

```
#!/bin/bash

echo "Hello, my name is Ezabyss"

echo
echo "What is your name?"

read name_container

echo
echo "Hello $name_container"
```

---

# ⚙️ Give Execution Permission

`chmod +x input_script.sh`

Run the script:

`./input_script.sh`

Example output:

```
Hello, my name is ezabyss

What is your name?
Abhishek

Hello Abhishek

```

---

# 📦 How the Script Works

| Line | Function |
|-----|-----|
| `echo` | Prints message to screen |
| `read` | Waits for user input |
| `name_container` | Variable storing input |
| `$name_container` | Displays variable value |

---

# 📊 Variable Containers

Variables act like **containers for data**.

Example:

```
read name

If user enters:

Abhishek

Variable now stores:

name = Abhishek

When used with:

`echo $name`

Output becomes:

Abhishek

```

---

# 🔧 Using Commands Inside Variables

Sometimes variables store **command output**.

Example:
A=\`hostname\`

Then display:

`echo "My host name is $A"`

Example output:

`My host name is server01`

Backticks tell Bash:

Run the command inside and store the result


---

# 🧪 Improved Interactive Script

```
#!/bin/bash

A=`hostname`

echo "Hello, my server name is $A"

echo
echo "What is your name?"

read B

echo
echo "What is your profession?"

read C

echo
echo "What is your favorite thing?"

read D

echo
echo "Hello $B"
echo "Your profession $C is awesome"
echo "You love $D"

```

---

# 🖥️ Example Execution

Run script:

`./input_script.sh`

Output:

```
Hello, my server name is my-linux-vm

What is your name?
ezabyss

What is your profession?
Security Professional

What is your favorite thing?
motorbikes

Hello ezabyss
Your profession Security Professional is awesome
And you love motorbikes
```

---

# 📌 Important Bash Commands Used

| Command | Purpose |
|------|------|
| `echo` | Display output |
| `read` | Take user input |
| `hostname` | Display system hostname |
| `chmod +x` | Make script executable |

---

# 🧠 Advanced Example (Installer Style Script)

```
#!/bin/bash

echo "Welcome to Application Installer"

echo "Enter your name:"
read user

echo "Enter organization:"
read org

echo "Installation starting for $user from $org"


This simulates a **software installation wizard**.
```

---

# 🧠 Questions

### What command takes user input in Bash?

`read`

---

### What command displays output in Bash?

`echo`

---

### How do you access a variable value?

Use `$variable_name`

Example:

`echo $name`

---

### How do you store command output in a variable?

Use backticks:
```
A=`hostname`
```
---

# 🏁 Key Takeaways

- `read` captures user input
- `echo` prints output to screen
- Variables store user input
- Scripts can behave like **interactive programs**

Interactive scripts are used in:

- Software installers
- System configuration tools
- DevOps automation
- User setup scripts

---

**✍️ Notes By Abhishek (Ez Abyss)**
