# Adding Text to Files & Redirects in Linux

---

# Why This Matters

You already learned how to create empty files using:

`touch filename`

But an empty file is useless unless you can:

- Add text
- Append content
- Save command output
- Populate logs
- Redirect results

This lesson covers:

1. `echo` with redirect
2. Command output redirection
3. Overwrite vs append
4. Viewing file content

---

# Method 1: Using `echo` + Redirect

## Basic Echo

`echo Hello`

Output:
`Hello`

The `echo` command simply prints text to the terminal.

---

## Redirect Output to a File (Overwrite)

`echo Hello World > Nepal`

What happens:
- Creates file if it doesn’t exist
- Overwrites file if it exists

Verify:
`ls -l Nepal`

View content:
`cat Nepal`

---

## Important: Single `>` Overwrites

If you run:

`echo New Line > Nepal`

It will:
❌ Delete old content
✔ Replace with new content

Always remember:
Single `>` = overwrite

---

# Append Instead of Overwrite

To append (add without deleting existing content):

`echo Another Line >> Nepal`

Verify:
`cat Nepal`

Now both lines exist.

---

# Rule to Memorize

`>` → Replace file  
`>>` → Add to file  

---

# Method 2: Redirect Command Output

You can redirect the output of any command.

Example:

`ls -ltr > listing.txt`

Instead of printing to screen,
it saves the output into `listing.txt`.

Check:
`cat listing.txt`

---

# Example: Save Date to File

Overwrite:
`date > Nepal`

Append:
`date >> Nepal`

Check:
`cat Nepal`

---

# Why Redirect Is Powerful

You can:
- Save logs
- Capture system info
- Automate reports
- Store command results
- Generate audit files

Example:

`whoami > user.txt`

`pwd >> user.txt`

Now `user.txt` contains:
- Current user
- Current directory

---

# Viewing File Contents

To read file content:

`cat filename`

Example:
`cat Nepal`

---

# File Size Growth Example

Check size:
`ls -l Nepal`

Append content:
`echo Extra line >> Nepal`

Check again:
`ls -l Nepal`

Notice:
File size increases.

---

# Practical Exercise

1. Create file:
   `touch notes.txt`

2. Add first line:
   `echo Linux is powerful > notes.txt`

3. Add second line:
   `echo I am learning redirects >> notes.txt`

4. Append system date:
   `date >> notes.txt`

5. View file:
   `cat notes.txt`

---

# Advanced Tip: Redirecting Errors

Standard output:
`command > file`

Standard error:
`command 2> errorfile`

Both together:
`command > outputfile 2>&1`

(Not required now, but useful later.)

---

# Summary Table

| Symbol | Meaning |
|---------|---------|
| `>` | Overwrite file |
| `>>` | Append to file |
| `cat` | View file contents |
| `touch` | Create empty file |

---

# Real-World Usage Examples

Save disk usage report:
`df -h > disk_report.txt`

Append system uptime:
`uptime >> disk_report.txt`

---

# Memory Trick

Single arrow replaces.  
Double arrow adds.

---

Practice this repeatedly until:
- You instinctively know when to use `>` vs `>>`
- You stop typing long manual notes
- You start capturing output professionally

---

**✍️ Notes By Abhishek (Ez Abyss)**
