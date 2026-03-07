# 🔁 Bash `while` (Do-While Style) Loop Scripts
### Running Commands Until a Condition Changes

---

# 🎯 Why `while` Loops Matter

Many Linux scripts need to **run continuously** until a certain condition is met.

Examples:

- Monitor system logs
- Run process until specific time
- Retry a command until it succeeds
- Wait until a file appears
- Monitor server health

This behavior is implemented using a **`while` loop**.

---

# 📌 What is a `while` Loop?

A `while` loop repeatedly executes commands **as long as a condition remains true**.

General logic:

```
while condition_is_true
do
run commands
done
```

When the condition becomes **false**, the loop stops.

---

# 🧠 Mental Model

Think of a **security guard checking a door**.

```
While door is open
keep watching
Once door closes
stop monitoring
```

Similarly in Bash:

```
while condition
do
command
done
```

---

# 🌍 Real World Scenario

System administrators often run scripts like:

- Monitor a service
- Check logs
- Retry failed operations

Example:

```
while server is down
try reconnect
```

Example command:

`ping server-ip`

Until the server responds.

---

# 🧪 Basic `while` Loop Script

Create script:

`vi while_script.sh`

Example script:

```
#!/bin/bash

count=0
number=10

while [ $count -lt $number ]
do
echo "Counter: $count"
count=$((count+1))
done
```

---

# ⚙️ Make Script Executable

`chmod +x while_script.sh`

Run:

`./while_script.sh`

Output:

```
Counter: 0
Counter: 1
Counter: 2
Counter: 3
Counter: 4
Counter: 5
Counter: 6
Counter: 7
Counter: 8
Counter: 9
```

---

# 📦 Understanding the Script

| Part | Purpose |
|-----|-----|
| `count=0` | starting value |
| `number=10` | stopping value |
| `while [ $count -lt $number ]` | loop condition |
| `count=$((count+1))` | increase counter |
| `done` | end loop |

---

# 🧪 Countdown Timer Script

Example script:

```
#!/bin/bash

count=10

while [ $count -gt 0 ]
do
echo "$count seconds left"
sleep 1
count=$((count-1))
done

echo "Process stopped"
```

---

# ▶ Example Output

```
10 seconds left
9 seconds left
8 seconds left
7 seconds left
6 seconds left
5 seconds left
4 seconds left
3 seconds left
2 seconds left
1 seconds left
Process stopped
```

---

# ⏳ What `sleep` Does

`sleep` pauses the script.

Example:

`sleep 1`

Meaning:

wait 1 second


This is often used in **monitoring scripts**.

---

# 🌍 Real System Administration Example

Example: monitor server until it becomes reachable.

```
#!/bin/bash

while ! ping -c1 google.com >/dev/null
do
echo "Waiting for network..."
sleep 5
done

echo "Network is up!"
```

This script:

- checks network connectivity
- retries every 5 seconds
- stops when network works

---

# 📊 Difference Between `for` and `while`

| Feature | `for` Loop | `while` Loop |
|------|------|------|
| Execution count | fixed list | condition based |
| Use case | repetitive tasks | monitoring / waiting |
| Example | loop through files | run until condition changes |

---

# 🔁 Example: Infinite Loop

Some scripts must **run forever**.

Example:

```
while true
do
echo "Monitoring system..."
sleep 10
done
```

This is commonly used in **background services and daemons**.

---

# 🧠 Questions

### What does a `while` loop do?

It executes commands repeatedly while a condition remains true.

---

### What ends a `while` loop?

`done`

---

### What command pauses a script?

`sleep`

Example:

`sleep 5`

---

### When do system administrators use `while` loops?

- monitoring scripts
- retry mechanisms
- automation processes

---

# 🏁 Key Takeaways

- `while` loops run commands **until a condition changes**
- widely used in **automation and monitoring**
- useful for **timers, retries, and continuous tasks**
- commonly used in **Linux daemons and background scripts**

Mastering `while` loops helps you build **powerful automation scripts**.

---

**✍️ Notes By Abhishek (Ez Abyss)**
