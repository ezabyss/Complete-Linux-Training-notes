# `grep` & `egrep` — Linux Text Processing

---

# 📌 What Is `grep`?

`grep` stands for:

> **Global Regular Expression Print**

It searches text line-by-line and prints lines that match a pattern.

In simple words:

`grep` = Search tool in Linux

It works on:
- Files
- Command output
- Logs
- Configuration files
- Pipelines

---

# 🧠 Why `grep` Is Important (Especially for Security)

Security analysts use `grep` to:

- Search logs for failed logins
- Detect suspicious IPs
- Extract user activity
- Investigate incidents
- Filter large outputs instantly

---

# 🗂 Practice File Used

We will use:

## `employee-list.txt`

    ID,Name,Department,Age,District
    301,Sita Karki,IT,23,Dang
    302,Ramesh Shrestha,HR,29,Bardiya
    303,Binita Gurung,Finance,26,Banke
    304,Sanjay Thapa,Marketing,31,Kailali
    305,Anjali Rai,IT,24,Kanchanpur
    306,Prakash Adhikari,Finance,32,Surkhet
    307,Nirmala Bhandari,HR,27,Achham
    308,Deepak Magar,Marketing,28,Doti
    309,Kabita Tamang,IT,25,Bajhang
    310,Suman Poudel,Finance,30,Jumla
    311,Arjun Bohora,IT,28,Dailekh
    312,Manisha Thakuri,HR,26,Humla

---

# 🔎 Basic Syntax

    grep "pattern" filename

---

# 1️⃣ Check Version / Help

    grep --version
    grep --help
    man grep

---

# 2️⃣ Basic Search

## Find All IT Employees

    grep "IT" employee-list.txt

---

## Find All Finance Employees

    grep "Finance" employee-list.txt

---

# 3️⃣ Case-Insensitive Search (`-i`)

Very important option.

Without `-i`, grep is case-sensitive.

    grep -i "finance" employee-list.txt

This matches:
- Finance
- FINANCE
- finance

---

# 4️⃣ Count Matches (`-c`)

Count how many lines match:

    grep -c "IT" employee-list.txt

---

# 5️⃣ Show Line Numbers (`-n`)

    grep -n "HR" employee-list.txt

Output example:

    3:302,Ramesh Shrestha,HR,29,Bardiya

---

# 6️⃣ Invert Match (`-v`)

Show everything EXCEPT pattern:

    grep -v "IT" employee-list.txt

Very useful for exclusion filtering.

---

# 7️⃣ Combine Options

Example:

    grep -in "finance" employee-list.txt

- `-i` → ignore case
- `-n` → show line number

---

# 8️⃣ Use `grep` with Command Output

`grep` works perfectly with pipes.

Example:

    ls -l | grep "Desktop"

---

## Extract Only Marketing Employees (Cleaner Output)

    grep "Marketing" employee-list.txt

---

## Chain with `cut`

    grep "IT" employee-list.txt | cut -d, -f2

Extracts only names of IT employees.

---

# 9️⃣ Using `egrep` (Extended grep)

`egrep` allows multiple patterns using OR (`|`).

Modern equivalent:

    grep -E

---

## Match IT OR HR

    grep -E "IT|HR" employee-list.txt

OR

    egrep "IT|HR" employee-list.txt

---

# 🔟 Advanced Examples

## Search Employees from Dang or Doti

    grep -E "Dang|Doti" employee-list.txt

---

## Count Employees from Western Districts

    grep -E "Dang|Banke|Bardiya|Kailali" employee-list.txt | wc -l

---

# 🛡 Real Security Use Cases

## Find Failed Logins in Log File

    grep "Failed password" auth.log

---

## Find Specific IP Address

    grep "192.168.1.10" access.log

---

## Count Suspicious Attempts

    grep -c "Failed" auth.log

---

## Exclude Noise (Filter Out Successful Logins)

    grep -v "Accepted password" auth.log

---

# 🔥 Combine `grep` + `awk`

Example:

    grep "IT" employee-list.txt | awk -F, '{ print $2, $5 }'

Output:
Name + District of IT employees

---

# 📊 Combine `grep` + `sort` + `uniq`

Count department occurrences:

    cut -d, -f3 employee-list.txt | sort | uniq -c

Or with grep:

    grep "IT" employee-list.txt | wc -l

---

# 🧩 Important Options Summary

| Option | Meaning |
|--------|----------|
| `-i` | Ignore case |
| `-n` | Show line number |
| `-c` | Count matches |
| `-v` | Invert match |
| `-E` | Extended regex (OR logic) |

---

# ⚠ Best Practices

✔ Always use `-i` unless case matters  
✔ Combine with pipes for power  
✔ Test small before large logs  
✔ Use `-n` when debugging  

---

# 🚀 Why `grep` Is Powerful

It:
- Searches massive logs instantly
- Filters output in pipelines
- Works with automation scripts
- Is essential for SOC analysts

---

# 🏁 Final Thought

If `cut` extracts  
If `awk` processes  
Then `grep` searches  

Together they form the foundation of Linux text processing.

Mastering `grep` means:

- Faster investigations  
- Cleaner log analysis  
- Stronger automation skills  

---

**✍️ Notes By Abhishek (Ez Abyss)**  
