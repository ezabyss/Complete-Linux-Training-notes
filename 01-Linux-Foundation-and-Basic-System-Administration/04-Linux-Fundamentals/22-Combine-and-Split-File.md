# Combining and Splitting Files in Linux

---

# 📌 Combining Files

You can combine multiple files into one using the `cat` command.

---

## Basic Syntax

    cat file1 file2 file3 > file4

What happens?

- Contents of `file1`
- Then contents of `file2`
- Then contents of `file3`
- All combined into `file4`

⚠️ Order matters. Files are merged in the order you specify.

---

# 🧪 Practical Example

## Step 1: Create Sample Files

    echo "Kathmandu is the capital of Nepal." > part1.txt
    echo "Pokhara is famous for lakes." > part2.txt
    echo "Lumbini is the birthplace of Buddha." > part3.txt

Verify:

    cat part1.txt
    cat part2.txt
    cat part3.txt

---

## Step 2: Combine Files

    cat part1.txt part2.txt part3.txt > Nepal.txt

Now check:

    cat Nepal.txt

You will see all three sentences combined into one file.

---

# 📌 Splitting Files

Sometimes files are too large.

Instead of compressing, you may need to split them into smaller files.

Common reasons:

- Email attachment size limits  
- Upload limits  
- Log file sharing  
- Third-party vendor requirements  

---

# 🔧 Basic Syntax

Split by number of lines:

    split -l NUMBER filename prefix

Where:

- `-l` → lines per file  
- `NUMBER` → how many lines per split  
- `prefix` → name for new files  

---

# 🧪 Practical Example

Assume `Nepal.txt` contains:

    Kathmandu is the capital of Nepal.
    Pokhara is famous for lakes.
    Lumbini is the birthplace of Buddha.
    Everest is the highest mountain.
    Chitwan is known for wildlife.
    Mustang is a beautiful region.
    Ilam is famous for tea.

Check line count:

    wc -l Nepal.txt

---

## Split Into 2 Lines Per File

    split -l 2 Nepal.txt splitfile

Now list files:

    ls

You will see:

    splitfileaa
    splitfileab
    splitfileac
    splitfilead

---

## Check Split Contents

    cat splitfileaa
    cat splitfileab
    cat splitfileac
    cat splitfilead

Each file contains 2 lines (except possibly the last one).

---

# ❓ Why Last File May Have Fewer Lines

If total lines are not evenly divisible,  
the last split file will contain the remaining lines only.

Example:

- 7 lines total  
- Split into 2 lines per file  
- Result: 2 + 2 + 2 + 1  

---

# 📌 Splitting by File Size Instead of Lines

You can also split by size:

    split -b 100 Nepal.txt sizefile

This splits by 100 bytes per file.

---

# 📌 Real-World Use Case

Imagine:

- A 5GB log file  
- Vendor only accepts 100MB uploads  

Solution:

    split -b 100M large-log.txt logpart

Send files one by one.

---

# Summary Table

| Task | Command |
|------|----------|
| Combine files | `cat f1 f2 > merged.txt` |
| Split by lines | `split -l 100 file prefix` |
| Split by size | `split -b 10M file prefix` |
| Count lines | `wc -l file` |

---

# 🎯 Key Takeaways

- `cat` → Combine files  
- `split` → Break large files  
- Very useful in log management  
- Helps in file transfer limitations  
- Common in production Linux systems  

---

Linux gives you full control over file manipulation.

Practice combining and splitting using small test files like `Nepal.txt`.

---

**✍️ Notes By Abhishek (Ez Abyss)**  
