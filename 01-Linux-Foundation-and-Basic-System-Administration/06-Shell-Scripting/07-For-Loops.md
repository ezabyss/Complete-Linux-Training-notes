# 🔁 Bash `for` Loop Scripts
### Automating Repetitive Tasks in Linux

---

# 🎯 Why `for` Loops Matter

In Linux administration and automation, many tasks are **repetitive**.

Examples:

- Creating multiple files
- Processing a list of servers
- Running commands several times
- Looping through directories
- Automating batch operations

Instead of typing the same command repeatedly, you can use a **`for` loop**.

A `for` loop runs commands **multiple times automatically**.

---

# 📌 What is a `for` Loop?

A `for` loop executes commands **repeatedly for a defined list of values**.

Example logic:

```
For each value in a list
run a command
repeat until list ends
```

This saves time and **automates repetitive tasks**.

---

# 🧠 Simple Example

Example idea:

```
For numbers 1 to 5
Print welcome message
```

---

# 🧪 Basic `for` Loop Script

Create a script:

`vi for.sh`

Script:

```
#!/bin/bash

for i in 1 2 3 4 5
do
echo "Welcome $i times"
done

```

---

# ⚙️ Make Script Executable

`chmod +x for.sh`

Run the script:

`./for.sh`

Output:

```
Welcome 1 times
Welcome 2 times
Welcome 3 times
Welcome 4 times
Welcome 5 times
```

---

# 📦 Understanding the Script

| Part | Meaning |
|------|------|
| `for` | start loop |
| `i` | variable container |
| `in` | list of values |
| `do` | begin commands |
| `echo` | output command |
| `done` | end loop |

Variable `i` takes each value one by one.

Example flow:
```
i = 1
i = 2
i = 3
i = 4
i = 5
```

---

# 🌍 Real World Scenario

A system administrator needs to **create 10 log files**.

Without loop:
```
touch log1
touch log2
touch log3
...
touch log10
```

With loop:
```
for i in 1 2 3 4 5 6 7 8 9 10
do
touch log$i
done
```

Much faster and automated.

---

# 🧪 Example: Loop Through Words

Create another script:

`vi xyz.sh`

Script:

```
#!/bin/bash

for i in eat run jump play
do
echo "See ezabyss $i"
done
```

---

# ▶ Run Script

`chmod +x xyz.sh`

`./xyz.sh`

Output:

```
See ezabyss eat
See ezabyss run
See ezabyss jump
See ezabyss play
```

---

# 📦 How It Works

Variable `i` stores words one by one.

Example:

```
i = eat
i = run
i = jump
i = play
```

Each value is used in the command:

`echo "See ezabyss $i"`

---

# 🧪 Example: Creating Multiple Files

Script:

```
#!/bin/bash

for i in 1 2 3 4 5
do
touch file$i.txt
done
```

Result:

```
file1.txt
file2.txt
file3.txt
file4.txt
file5.txt
```

---

# 📊 Loop with Numbers Range

Instead of typing numbers manually:

```
for i in {1..10}
do
echo "Number $i"
done
```

Output:

```
Number 1
Number 2
Number 3
...
Number 10
```

---

# 🌍 Real System Administration Use Cases

`for` loops are commonly used for:

### Server Management

```
for server in server1 server2 server3
do
ssh $server uptime
done
```

Checks uptime on multiple servers.

---

### Log Monitoring

```
for file in /var/log/*.log
do
echo $file
done
```

Processes multiple log files.

---

### User Account Creation

```
for user in user1 user2 user3
do
useradd $user
done
```

Creates multiple users automatically.

---

# 🧠 Questions

### What does a `for` loop do?

It runs commands repeatedly for each value in a list.

---

### What keyword ends a `for` loop?

`done`

---

### What is a loop variable?

A container that stores values during each loop iteration.

Example:

`for i in 1 2 3`

Variable is `i`.

---

# 🏁 Key Takeaways

- `for` loops automate repetitive tasks
- They reduce manual work
- They are essential in **Linux automation scripts**
- Used widely in **system administration and DevOps**

Mastering loops helps you build **powerful automation scripts**.

---

**✍️ Notes By Abhishek (Ez Abyss)**
