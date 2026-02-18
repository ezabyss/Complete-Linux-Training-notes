# `sort` & `uniq` — Linux Text Processing Commands

---

# 📌 Overview

Both `sort` and `uniq` are powerful Linux text processing commands.

| Command | Purpose |
|----------|----------|
| `sort` | Sorts lines alphabetically or numerically |
| `uniq` | Removes duplicate adjacent lines |

They are often used together.

---

# 🧠 Important Rule

> ⚠️ Always run `sort` before `uniq`

Why?

`uniq` only removes **adjacent duplicates**.  
If duplicates are not next to each other, it will not remove them.

---

# 📂 Practice File: `employee-list.txt`

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

# 🔎 Check Version / Help

    sort --version
    sort --help
    man sort

    uniq --version
    uniq --help
    man uniq

---

# 🔤 SORT COMMAND

---

## 1️⃣ Basic Sort (Alphabetical)

Sort entire file:

    sort employee-list.txt

---

## 2️⃣ Reverse Sort

    sort -r employee-list.txt

---

## 3️⃣ Sort by Specific Column

Since file is comma-separated:

Delimiter = `,`

Sort by Name (field 2):

    sort -t, -k2 employee-list.txt

---

Sort by Department (field 3):

    sort -t, -k3 employee-list.txt

---

Sort by District (field 5):

    sort -t, -k5 employee-list.txt

---

## 4️⃣ Numeric Sort (Important)

Sort by Age numerically:

    sort -t, -k4 -n employee-list.txt

`-n` ensures numeric sorting (not alphabetical).

---

# 🔄 UNIQ COMMAND

---

## What `uniq` Does

Removes duplicate adjacent lines.

---

## Example: Create Duplicate for Practice

Add duplicate line:

    echo "301,Sita Karki,IT,23,Dang" >> employee-list.txt

---

## Check File

    cat employee-list.txt

Now duplicate exists.

---

## ❌ Wrong Way

    uniq employee-list.txt

Duplicate may remain.

---

## ✅ Correct Way

    sort employee-list.txt | uniq

Now duplicate removed.

---

# 🔢 Count Duplicates (`-c`)

    sort employee-list.txt | uniq -c

Shows count of each line.

Example output:

    2 301,Sita Karki,IT,23,Dang

---

# 🔎 Show Only Duplicate Lines (`-d`)

    sort employee-list.txt | uniq -d

Shows only repeated entries.

---

# 🧩 Real Practical Examples

---

## Count Employees Per Department

    cut -d, -f3 employee-list.txt | sort | uniq -c

---

## Count Employees Per District

    cut -d, -f5 employee-list.txt | sort | uniq -c

---

## Sort Names Only

    cut -d, -f2 employee-list.txt | sort

---

## Sort Ages Numerically

    cut -d, -f4 employee-list.txt | sort -n

---

# 🔗 Using with Command Output

You can pipe anything.

Example:

    ls -l | sort

---

Sort by filename column:

    ls -l | sort -k9

---

Count file types:

    ls | sort | uniq -c

---

# ⚠ Why `sort` Before `uniq`?

Example without sorting:

Line A  
Line B  
Line A  

`uniq` will NOT remove duplicates because they are not adjacent.

After sorting:

Line A  
Line A  
Line B  

Now `uniq` works.

---

# 📊 Summary Table

| Command | Purpose |
|----------|----------|
| `sort file` | Alphabetical sort |
| `sort -r` | Reverse order |
| `sort -n` | Numeric sort |
| `sort -t, -k3` | Sort by column |
| `uniq` | Remove adjacent duplicates |
| `uniq -c` | Count duplicates |
| `uniq -d` | Show only duplicates |

---

# 🚀 Security Use Cases

Security analysts use:

    sort auth.log | uniq -c

To:
- Count repeated login attempts
- Detect brute-force attacks
- Analyze repeated IP addresses

---

# 🏁 Final Thought

`sort` organizes  
`uniq` filters  

Together they:

- Clean data
- Count duplicates
- Prepare logs for analysis
- Improve automation pipelines

Mastering `sort | uniq` is foundational for log analysis and security operations.

---

**✍️ Notes By Abhishek (Ez Abyss)**  
