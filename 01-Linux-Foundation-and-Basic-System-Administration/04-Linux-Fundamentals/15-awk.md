# ⚡ `awk` Command — Powerful Text Processing Utility

---

# 📌 What Is `awk`?

`awk` is a powerful:

- Text processing utility
- Pattern scanning tool
- Data extraction language

It is mainly used to:

- Extract columns (fields)
- Search patterns
- Modify text
- Perform calculations
- Process structured files
- Generate reports

Think of `awk` as:

> Smart column processor + mini programming language

---

# 🔍 Check Version / Help

    awk --version
    man awk

---

# 🧠 How `awk` Works

Basic structure:

    awk 'pattern { action }' filename

Important concepts:

- `$1` → First field
- `$2` → Second field
- `$NF` → Last field
- `$0` → Entire line
- `NF` → Number of fields in a line

Default delimiter = space

---

# 📂 Example File: `employee-list.txt`

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

This file is comma-separated (CSV).

---

# 🔹 Set Delimiter for CSV

Because this file uses comma `,`, we must specify:

    awk -F, '{ action }' employee-list.txt

`-F,` → Field separator is comma

---

# 🔹 Print First Column (ID)

    awk -F, '{ print $1 }' employee-list.txt

---

# 🔹 Print Name Column

    awk -F, '{ print $2 }' employee-list.txt

---

# 🔹 Print Name and Department

    awk -F, '{ print $2, $3 }' employee-list.txt

---

# 🔹 Skip Header Line

    awk -F, 'NR>1 { print $2 }' employee-list.txt

`NR` = record number (line number)

---

# 🔹 Filter Only IT Employees

    awk -F, '$3=="IT" { print $2, $5 }' employee-list.txt

Explanation:
- `$3=="IT"` → Department column
- Print Name and District

---

# 🔹 Count Employees Per Department

    awk -F, '{ print $3 }' employee-list.txt | sort | uniq -c

---

# 🔹 Print Last Field Automatically

    awk -F, '{ print $NF }' employee-list.txt

`$NF` = last column

---

# 🔹 Search for Specific Keyword

Find employees from Dang:

    awk -F, '$5=="Dang"' employee-list.txt

---

# 🔹 Replace Field Value (Modify Output)

Example: Replace all "IT" with "CyberSecurity"

    awk -F, '{ if($3=="IT") $3="CyberSecurity"; print }' employee-list.txt

---

# 🔹 Modify Name Field Example

Replace all Names with "ezabyss":

    awk -F, '{ $2="ezabyss"; print }' employee-list.txt

---

# 🔹 Print Lines Longer Than X Characters

    awk 'length($0) > 25' employee-list.txt

---

# 🔹 Print Total Number of Fields

    awk -F, '{ print NF }' employee-list.txt

---

# 🔹 Print Only Rows Where Age > 28

    awk -F, '$4 > 28' employee-list.txt

---

# 🔹 Print Only Name and Age Where Age > 28

    awk -F, '$4 > 28 { print $2, $4 }' employee-list.txt

---

# 🔹 Use With `ls -l`

Print permission and owner:

    ls -l | awk '{ print $1, $3 }'

---

# 🔹 Print Last Column of `ls -l`

    ls -l | awk '{ print $NF }'

---

# 🔹 Count Total Fields in `ls -l`

    ls -l | awk '{ print NF }'

---

# 💡 Powerful `awk` Concepts

| Symbol | Meaning |
|--------|----------|
| `$1` | First field |
| `$2` | Second field |
| `$NF` | Last field |
| `$0` | Entire line |
| `NR` | Line number |
| `NF` | Number of fields |

---

# 🔥 Why `awk` Is Powerful

Unlike `cut`, `awk` can:

- Perform conditional logic
- Replace values
- Perform calculations
- Filter rows intelligently
- Combine pattern + action
- Work like a mini programming language

---

# 🔐 Real SOC / Security Use Cases

Extract usernames from `/etc/passwd`:

    awk -F: '{ print $1 }' /etc/passwd

Find users with bash shell:

    awk -F: '$7=="/bin/bash"' /etc/passwd

Extract failed login attempts:

    awk '/Failed/' /var/log/auth.log

---

# 🚀 Difference: `cut` vs `awk`

| Feature | cut | awk |
|----------|------|------|
| Extract columns | ✅ | ✅ |
| Conditional filtering | ❌ | ✅ |
| Replace values | ❌ | ✅ |
| Calculations | ❌ | ✅ |
| Complex logic | ❌ | ✅ |

If `cut` is a knife,
`awk` is a Swiss army knife 🔥

---

# 🏁 Final Takeaway

`awk` is one of the most powerful tools in Linux.

It helps with:

- CSV parsing
- Log analysis
- Security audits
- Automation scripts
- Field manipulation
- Pattern matching

Mastering `awk` separates beginners from advanced Linux users.

---

**✍️ Notes By Abhishek (Ez Abyss)**
