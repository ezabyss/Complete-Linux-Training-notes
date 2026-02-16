# Filters & Text Processing Commands in Linux

---

## Why Text Processing Matters

Text processing commands are extremely powerful in Linux.

As a security analyst, you will often:

- Analyze log files  
- Search for suspicious activity  
- Extract specific fields  
- Sort and clean output  
- Count events  
- Remove duplicates  

These commands allow you to manipulate text efficiently and quickly.

---

# What Are Filters?

Filters:

- Take input (from a file or command)
- Process it
- Produce refined output

Most filter commands are used with pipes `|`.

Example:

    cat messages | grep warning

---

# Commands

1. `cut`  
2. `awk`  
3. `grep` / `egrep`  
4. `sort`  
5. `uniq`  
6. `wc`  

Each command serves a specific purpose.

---

# 1️⃣ `cut` — Extract Specific Columns

The `cut` command extracts sections of text.

Example:

    cut -d ":" -f1 /etc/passwd

Explanation:
- `-d ":"` → Use colon as delimiter
- `-f1` → Select field 1

Useful for:
- Extracting usernames
- Parsing log fields
- Splitting structured text

---

# 2️⃣ `awk` — Advanced Column Processing

`awk` is a powerful text processing tool.

Example:

    awk '{print $1}' file.txt

This prints the first column.

Useful for:
- Structured log analysis
- Conditional processing
- Complex field extraction

---

# 3️⃣ `grep` / `egrep` — Search by Keyword

Search for specific words inside a file.

Example:

    grep "warning" messages

Displays only lines containing "warning" in file `messages`.

Case insensitive search:

    grep -i "error" messages

Search with patterns:

    egrep "error|fail|denied" messages

Common SOC usage:

    grep "Failed password" auth.log

---

# 4️⃣ `sort` — Sort Output

Sort text alphabetically.

Example:

    sort file.txt

Reverse order:

    sort -r file.txt

Numeric sort:

    sort -n numbers.txt

Very useful before using `uniq`.

---

# 5️⃣ `uniq` — Remove Duplicates

Removes consecutive duplicate lines.

Example:

    sort file.txt | uniq

Important:
`uniq` works properly only after sorting.

Count duplicates:

    sort file.txt | uniq -c

Common log analysis pattern.

---

# 6️⃣ `wc` — Word Count

`wc` counts:

- Lines  
- Words  
- Characters  

Example:

    wc file.txt

Options:

    wc -l file.txt   → Count lines
    wc -w file.txt   → Count words
    wc -c file.txt   → Count characters

Example in security:

    grep "Failed password" auth.log | wc -l

Counts failed login attempts.

---

# Why These Commands Are Powerful

They allow you to:

- Extract only relevant information  
- Reduce noise  
- Identify patterns  
- Perform quick forensic analysis  
- Build automation scripts  

---

# Real Security Workflow Example

Count unique IP addresses from log:

    awk '{print $1}' access.log | sort | uniq -c | sort -nr

This:
1. Extracts IP column  
2. Sorts it  
3. Removes duplicates  
4. Counts occurrences  
5. Sorts by highest count  

This is real-world SOC analysis.

---

# Quick Summary

| Command | Purpose |
|----------|----------|
| `cut` | Extract fields |
| `awk` | Advanced processing |
| `grep` | Search by keyword |
| `sort` | Sort output |
| `uniq` | Remove duplicates |
| `wc` | Count lines/words/chars |

---

# Final Thought

Text processing commands are the backbone of:

- Log analysis  
- Threat hunting  
- System auditing  
- Incident response  

Once you master these,  
Linux becomes extremely powerful.

---

**✍️ Notes By Abhishek (Ez Abyss)**
