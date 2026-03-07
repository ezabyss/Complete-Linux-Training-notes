# ⚙️ Bash `if`, `then`, `else` Scripts
### Conditional Logic in Linux Shell Scripting

---

# 🎯 Why Conditional Scripts Matter

In automation and system administration, scripts often need to **make decisions**.

Examples:

- If a service stops → restart it
- If disk usage exceeds limit → send alert
- If a file exists → process it
- If user input matches value → run action

This logic is implemented using **`if`, `then`, `else` statements**.

---

# 📌 What is an `if` Statement?

An `if` statement allows a script to **check a condition**.

If the condition is true → perform one action.  
If the condition is false → perform another action.

General logic:

```
IF condition is true
do this
ELSE
do something else
```

---

# 🧠 Simple Example

```
if count = 100
print "count is 100"
else
print "count is not 100"
```

This is exactly how **decision-making scripts work**.

---

# 🧪 Basic `if then else` Script

Create a script:

`vi if_then_script.sh`

Example script:

```
#!/bin/bash

count=100

if [ $count -eq 100 ]
then
echo "The count is 100"
else
echo "The count is not 100"
fi
```

---

# ⚙️ Make Script Executable

`chmod +x if_then_script.sh`

Run the script:

`./if_then_script.sh`

Output:

`The count is 100`

---

# 🔄 Changing Variable Value

Edit script:
`count=1`

Run again:

`./if_then_script.sh`

Output:

`The count is not 100`


This shows the **decision logic working**.

---

# 📦 Structure of an `if` Script

```
if [ condition ]
then
commands
else
commands
fi
```

Explanation:

| Keyword | Purpose |
|------|------|
| `if` | checks condition |
| `then` | runs commands if true |
| `else` | runs if condition is false |
| `fi` | ends the if statement |

---

# 📊 Comparison Operators

| Operator | Meaning |
|------|------|
| `-eq` | equal |
| `-ne` | not equal |
| `-gt` | greater than |
| `-lt` | less than |
| `-ge` | greater or equal |
| `-le` | less or equal |

Example:

`if [ $num -gt 10 ]`

Means:

`If number is greater than 10`


---

# 🧪 Example: File Existence Check

Create script:

`vi check_file.sh`

Script:

```
#!/bin/bash

clear

if [ -e /home/ezabyss/error.txt ]
then
echo "File exists"
else
echo "File does not exist"
fi

```
---

# 🔎 What `-e` Means

`-e` checks if a file exists.

Example:

`if [ -e filename ]`

True → file exists  
False → file missing

---

# 🖥️ Running the Script

Run script:

`./check_file.sh`

Output:

`File does not exist`

---

# 🧪 Create File

Create test file:

`touch /home/ezabyss/error.txt`

Run script again:

`./check_file.sh`

Output:

`File exists`


---

# 🌍 Real World Scenario

System administrators often monitor **error logs**.

Example script logic:

```
If error log exists
alert administrator
Else
continue monitoring
```

Example usage with cron:

`0 * * * * /scripts/check_errors.sh`

Runs every hour to check if **application error file exists**.

---

# 🧠 Example Interactive Script

```
#!/bin/bash

echo "Enter your name:"
read name

echo "Do you like working in IT? (yes/no)"
read answer

if [ "$answer" = "yes" ]
then
echo "You are awesome!"
else
echo "You should try IT!"
fi
```

---

# 🧪 Example Output

```
Enter your name:
Abhishek

Do you like working in IT? (yes/no)
yes

You are awesome!

```
---

# 📊 Useful File Test Operators

| Operator | Description |
|------|------|
| `-e` | file exists |
| `-f` | regular file |
| `-d` | directory exists |
| `-r` | file readable |
| `-w` | file writable |
| `-x` | file executable |

Example:

`if [ -d /home/user/scripts ]`

Checks if directory exists.

---

# 🧠 Questions

### What does `if` statement do?

It allows scripts to make decisions based on conditions.

---

### What is `fi`?

It marks the **end of an `if` statement**.

---

### What does `-e` check?

It checks whether a file exists.

---

### What command makes scripts executable?

`chmod +x scriptname.sh`

---

# 🏁 Key Takeaways

- `if` statements allow **decision making in scripts**
- `then` runs commands when condition is true
- `else` runs commands when condition is false
- `fi` ends the conditional block

Conditional scripting is essential for:

- automation
- monitoring
- system administration
- DevOps pipelines

---

**✍️ Notes By Abhishek (Ez Abyss)**
