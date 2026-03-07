# 🧭 Bash `case` Statement Scripts
### Interactive Menu-Based Automation in Linux

---

# 🎯 Why `case` Statements Matter

In many scripts, users must **choose between multiple options**.

Examples:

- System administration tools
- Installation scripts
- Menu-driven utilities
- Troubleshooting tools

Instead of writing many `if` statements, Bash provides the **`case` statement**.

It allows scripts to behave like a **menu system**.

---

# 📌 What is a `case` Statement?

A `case` statement is used to **compare one variable against multiple options**.

Depending on the option selected, **different commands run**.

General logic:

```
case variable in
option1)
command
;;

option2)
command
;;

*)
default action
;;

esac
```

---

# 🧠 Simple Explanation

Think of a **restaurant menu**.

```
Press 1 → Order Pizza
Press 2 → Order Burger
Press 3 → Order Salad
```

The script checks your choice and runs the corresponding action.

---

# 🌍 Real World Scenario

System administrators often create **interactive scripts**.

Example script menu:

```
Show system date

List files

Show logged in users

Check system uptime
```

Instead of remembering commands, users simply choose a number or letter.

---

# 🧪 Example `case` Script

Create script:

`vi case_script.sh`

Script:

```
#!/bin/bash

echo
echo "Please choose one of the options below"
echo
echo "A = Display date and time"
echo "B = List files and directories"
echo "C = List users logged in"
echo "D = Check system uptime"
echo

read choice

case $choice in

A)
date
;;

B)
ls
;;

C)
who
;;

D)
uptime
;;

*)
echo "Invalid choice. Bye."
;;

esac
```

---

# ⚙️ Make Script Executable

`chmod +x case_script.sh`

Run script:

`./case_script.sh`

---

# 🖥 Example Interaction

Script output:

```
Please choose one of the options below

A = Display date and time
B = List files and directories
C = List users logged in
D = Check system uptime


User enters:

`A`

Output:


Sun Mar 8 02:43:33 AM +0545 2026

```
---

# 📦 How the Script Works

| Step | Explanation |
|-----|-------------|
| `echo` | prints menu text |
| `read choice` | stores user input |
| `case $choice` | evaluates the option |
| `A)` | run `date` command |
| `B)` | run `ls` command |
| `C)` | run `who` command |
| `D)` | run `uptime` command |
| `*` | default option (invalid input) |

---

# 🔎 Important Syntax Pieces

### Case keyword

Starts comparison:

`case $variable in`

---

### Pattern

Example option:

```
A)
command
;;

```

`;;` means **end of that option block**.

---

### Default Option

```
*)
echo "Invalid choice"
;;
```

`*` matches **anything not listed above**.

---

# 🌍 Real System Administration Example

Interactive system menu script:

```
#!/bin/bash

echo "System Utility Menu"

echo "1 - Check Disk Usage"
echo "2 - Check Memory"
echo "3 - Check Uptime"

read option

case $option in

df -h
;;

free -m
;;

uptime
;;

*)
echo "Invalid selection"
;;

esac
```

---

# 📊 Why `case` is Better Than Multiple `if`

| Feature | `if` statements | `case` statement |
|------|------|------|
| Multiple conditions | messy | clean |
| Menu scripts | difficult | perfect |
| Readability | harder | easier |

---

# 🧠 Questions

### What does a `case` statement do?

It compares a variable against multiple options and executes the matching command.

---

### What does `;;` mean?

It ends a case block.

---

### What does `*` represent?

A default case when no option matches.

---

# 🏁 Key Takeaways

- `case` statements simplify **multi-option scripts**
- widely used in **interactive Linux tools**
- cleaner than multiple `if` conditions
- perfect for **menu-driven automation scripts**

Learning `case` statements helps you build **professional Linux administration scripts**.

---

**✍️ Notes By Abhishek (Ez Abyss)**
