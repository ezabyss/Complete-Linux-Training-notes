# Standard Output to a File Using the `tee` Command

---

## Why Learn `tee`?

You already learned how to redirect output using:

    >

and

    >>

But there is another powerful method:

    tee

The `tee` command allows you to:

- View output on the screen  
- Save the same output to a file  
- Do both at the same time  

---

# What Is `tee`?

The name comes from a plumbing **T-splitter**.

Water flows in → splits into two directions.

Similarly:

Command output →  
1. Displays on screen  
2. Writes into file  

---

# Basic Syntax

    command | tee filename

---

# Example 1 — Basic Echo with `tee`

    echo "Nepal is a beautiful country" | tee Nepal.txt

Output:
- Displays text on screen
- Saves text inside `Nepal.txt`

Verify:

    cat Nepal.txt

---

# Why Use `tee` Instead of `>` ?

Using redirect:

    echo "Hello" > file.txt

Result:
- Saves to file
- Does NOT display on screen

Using `tee`:

    echo "Hello" | tee file.txt

Result:
- Displays on screen
- Saves to file

`tee` is useful when you want to:
- Monitor output live
- Verify correct output
- Log command execution

---

# Appending with `tee`

By default, `tee` overwrites the file.

To append instead:

    command | tee -a filename

Example:

    echo "Nepal is landlocked country." | tee -a Nepal.txt

Now the file contains multiple lines.

---

# Example 2 — Save Directory Listing

    ls -l | tee listdir.txt

Result:
- Shows directory listing
- Saves same output to `listdir.txt`

Verify:

    cat listdir.txt

---

# Example 3 — Save Word Count Output

Count characters:

    wc -c Nepal.txt | tee charcount.txt

Now:
- Character count appears on screen
- Also saved to `charcount.txt`

---

# Write to Multiple Files

You can write to multiple files:

    ls -l | tee file1.txt file2.txt file3.txt

All three files will contain identical content.

---

# Useful Options

Append:

    tee -a filename

View version:

    tee --version

Get help:

    tee --help

---

# Real-World Security Use Case

As a security analyst, you might:

- Run log parsing scripts  
- Check suspicious file activity  
- Scan for vulnerabilities  

Example:

    grep "failed" auth.log | tee failed_logins.txt

This:
- Displays failed login attempts
- Saves them for reporting

Very useful in SOC environments.

---

# When to Use `tee`

Use `tee` when:

- You need a log copy
- You want real-time output visibility
- You are troubleshooting
- You are debugging scripts
- You are building automation

---

# Quick Comparison

| Method | Shows Output | Saves Output |
|---------|--------------|--------------|
| `>` | ❌ | ✅ |
| `>>` | ❌ | ✅ (append) |
| `tee` | ✅ | ✅ |
| `tee -a` | ✅ | ✅ (append) |

---

# Final Thought

`tee` is extremely useful for:

- Debugging
- Logging
- Script building
- Security monitoring

Once you start scripting, you will use `tee` frequently.

---

**✍️ Notes By Abhishek (Ez Abyss)**
