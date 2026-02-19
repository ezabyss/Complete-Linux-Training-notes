# `truncate` Command — Practical Example Using `Nepal.txt`

---

## What is `truncate`?

The `truncate` command is used to:

- Shrink a file to a specific size  
- Extend a file to a specific size  
- Modify file size instantly  

⚠️ Important:  
`truncate` does NOT compress a file.  
It literally **cuts or extends** the file.

---

# Basic Syntax

    truncate -s SIZE filename

---

# 🏔 Practice Example Using `Nepal.txt`

## 1️⃣ Create the File

    touch Nepal.txt

Verify:

    ls -l Nepal.txt

You will see:
- File exists
- Size = 0 bytes

---

## 2️⃣ Add Content

Let’s write a short sentence:

    echo "Nepal is a beautiful country with mountains and rich culture." > Nepal.txt

Check content:

    cat Nepal.txt

Check size:

    ls -l Nepal.txt

You will see the file now has some bytes (for example around 60+ bytes).

---

# 3️⃣ Shrink the File

Now let's reduce the file size to 30 bytes:

    truncate -s 30 Nepal.txt

Check size:

    ls -l Nepal.txt

Now view content:

    cat Nepal.txt

You may see something like:

    Nepal is a beautiful country

Notice:
- The sentence is cut
- Everything after byte 30 is permanently removed
- Data is lost

⚠️ This cannot be recovered.

---

# 4️⃣ Extend the File

Now let’s increase the size to 60 bytes:

    truncate -s 60 Nepal.txt

Check size:

    ls -l Nepal.txt

Now check content:

    cat Nepal.txt

You will notice:
- The old deleted words did NOT come back
- The file just became larger
- Extra space is filled with empty (null) bytes

If opened in `vi`, you may see padding characters.

---

# Real-World Use Case

## Clear a Log File Safely

Instead of deleting:

    rm app.log

You can do:

    truncate -s 0 app.log

This:
- Keeps file permissions
- Keeps ownership
- Keeps application references

Very common in Linux servers.

---

# Summary

| Action | Command |
|--------|----------|
| Shrink file | `truncate -s 30 Nepal.txt` |
| Extend file | `truncate -s 60 Nepal.txt` |
| Clear file | `truncate -s 0 Nepal.txt` |

---

# ⚠️ Important Warning

Never use `truncate` on:
- Database files
- System files
- Important configuration files

It permanently modifies data.

---

# Final Takeaway

`truncate` is:

- Fast  
- Powerful  
- Destructive if misused  

Practice safely using small test files like `Nepal.txt`.

---

**✍️ Notes By Abhishek (Ez Abyss)**  
