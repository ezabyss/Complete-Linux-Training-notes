# 🔪 `cut` Command 

---

# 📌 What Is `cut`?

`cut` is a Linux text processing utility that:

- Extracts specific parts of text
- Cuts by **character position**
- Cuts by **byte position**
- Cuts by **field (column)**
- Works on **files OR command output**
- Prints result to standard output

It is lightweight, fast, and extremely useful for:

- Log analysis
- CSV parsing
- Security auditing
- Column extraction
- Data filtering
- Automation scripts

---

# ⚠️ Basic Rule

You **cannot** run `cut` without an option.

❌ Wrong:

    cut filename

✅ Correct:

    cut -option filename

You MUST specify:
- What to cut
- How to cut it

---

# 📘 Help & Documentation

    cut --version
    cut --help
    man cut

---

# 🧠 Core Options

| Option | Meaning |
|--------|----------|
| `-c` | Cut by character position |
| `-b` | Cut by byte position |
| `-d` | Specify delimiter |
| `-f` | Specify field number |

---

# 📂 Practical File Example

## File: `employee-list.txt`

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
    

This is a **CSV file**.

Delimiter = comma `,`

View file:

    cat employee-list.txt

---

# 🔹 1️⃣ Cut by Character Position (`-c`)

## Get First Character of Every Line

    cut -c1 employee-list.txt

---

## Get First 3 Characters

    cut -c1-3 employee-list.txt

---

## Select Specific Characters

Example: Characters 1–3 and 5–8

    cut -c1-3,5-8 employee-list.txt

⚠️ Best used for fixed-width files.

---

# 🔹 2️⃣ Cut by Byte Position (`-b`)

Works similar to `-c`.

    cut -b1-3 employee-list.txt

Usually same as `-c` unless working with special encoding.

---

# 🔹 3️⃣ Cut by Field (Most Important 🔥)

For structured files like CSV or `/etc/passwd`.

---

## Extract Only IDs

    cut -d, -f1 employee-list.txt

---

## Extract Only Names

    cut -d, -f2 employee-list.txt

---

## Extract Department Column

    cut -d, -f3 employee-list.txt

---

## Extract District Column

    cut -d, -f5 employee-list.txt

---

## Extract Multiple Fields

Get Name and Department:

    cut -d, -f2,3 employee-list.txt

---

## Extract Range of Fields

Get ID through Age:

    cut -d, -f1-4 employee-list.txt

---

# 🔹 Skip Header Line

    tail -n +2 employee-list.txt | cut -d, -f2

Explanation:
- `tail -n +2` → skip first line
- Pipe into `cut`

---

# 🔹 Using `cut` with Command Output

Example:

    ls -l | cut -c2-4

Extracts user permission bits from `ls -l`.

---

# 🔹 Real Linux Example: `/etc/passwd`

View file:

    cat /etc/passwd

Fields separated by colon `:`

Example line:

    ihaveso:x:1001:1001::/home/ihaveso:/bin/bash

Extract usernames:

    cut -d: -f1 /etc/passwd

Extract home directories:

    cut -d: -f6 /etc/passwd

Extract username + shell:

    cut -d: -f1,7 /etc/passwd

---

# 🔥 Security / SOC Use Cases

## Extract IT Employees

    grep ",IT," employee-list.txt

---

## Count Finance Employees

    grep ",Finance," employee-list.txt | wc -l

---

## Get Unique Districts

    cut -d, -f5 employee-list.txt | sort | uniq

---

## Count Department Distribution

    cut -d, -f3 employee-list.txt | sort | uniq -c

Output example:

    4 IT
    3 HR
    3 Finance
    2 Marketing

---

# 🧩 Combine With Other Commands

`cut` becomes powerful when combined with:

    grep
    sort
    uniq
    wc
    head
    tail

Example:

    cut -d, -f2 employee-list.txt | sort

---

# 🚨 Important Notes

- Field numbering starts at **1** (not 0).
- Always inspect file first using `cat`.
- Confirm delimiter before using `-d`.
- Works best with structured text.
- Not ideal for complex logic (use `awk` for advanced tasks).

---

# 🎯 When To Use `cut`

Use `cut` when:

- File is structured (CSV, colon-separated, etc.)
- You need quick column extraction
- You want lightweight parsing
- You are processing logs
- You are doing security audits

---

# 💡 Pro-Level Tip

Think of `cut` as:

> “Column Extractor”

If your file is structured → `cut` is your fastest tool.

---

# 🏁 Final Takeaway

`cut` is simple but extremely powerful.

It improves:

- Log parsing speed
- Data extraction efficiency
- Automation scripting
- Security investigation workflow

Mastering `cut` is foundational for:

- Linux administrators
- SOC analysts
- Cybersecurity professionals
- DevOps engineers

---

**✍️ Notes By Abhishek (Ez Abyss)**
