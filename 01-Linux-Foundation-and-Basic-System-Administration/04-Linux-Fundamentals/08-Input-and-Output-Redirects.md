# Linux Input & Output Redirection (stdin, stdout, stderr)

---

# Everything in Linux is a File

In Linux:
- Regular files → file
- Directories → file
- Keyboard → file
- Monitor → file
- Devices → file

Linux communicates using **file descriptors**.

---

# The Three Standard Streams

| Stream | Name | File Descriptor | Default Source |
|--------|------|-----------------|----------------|
| Standard Input | `stdin` | `0` | Keyboard |
| Standard Output | `stdout` | `1` | Screen |
| Standard Error | `stderr` | `2` | Screen |

---

# 1️⃣ Standard Output (stdout)

By default, command output goes to the terminal (screen).

Example:
`ls -l`

Output appears on screen.

---

## Redirect Output to File (Overwrite)

`ls -l > listings`

What happens:
- Output goes into `listings`
- Nothing prints on screen
- If file exists → overwritten

Check:
`cat listings`

---

## Append Output Instead of Overwrite

`ls -la >> listings`

Now:
- Old content stays
- New content is appended

Remember:

`>` → overwrite  
`>>` → append  

---

## Another Example

Save current path:
`pwd > findpath`

Append date:
`date >> findpath`

Verify:
`cat findpath`

---

# 2️⃣ Standard Input (stdin)

Standard input comes from:
`0` → keyboard

Example:

Normally:
`cat filename`

But you can feed input like this:

`cat < findpath`

This tells Linux:
Take input from file instead of keyboard.

---

## Practical Example (Conceptual)

Send file content into command:

`mail -s "Office Memo" user@example.com < memo.txt`

Meaning:
- Subject: Office Memo
- Content: memo.txt file

---

# 3️⃣ Standard Error (stderr)

Errors use file descriptor:
`2`

Example:

`ls -l /root`

If you are not root:
You see:
`Permission denied`

That error = `stderr`

---

## Redirect Error Only

`ls -l /root 2> errorfile`

Now:
- Error goes into `errorfile`
- Nothing prints on screen

Check:
`cat errorfile`

---

## Example with telnet

`telnet localhost`

If connection fails:
Error shows on screen.

Redirect error:

`telnet localhost 2> errorfile`

Now error messages go into file.

---

# Combine Output and Error

## Redirect Both stdout and stderr

`command > outputfile 2>&1`

Meaning:
- `>` redirect stdout
- `2>&1` redirect stderr to same place as stdout

Example:
`ls -l /root > alloutput.txt 2>&1`

Now:
- Both output and error go to `alloutput.txt`

---

# Advanced Shortcut (Bash)

Redirect everything:

`command &> alloutput.txt`

Equivalent to:
`command > alloutput.txt 2>&1`

---

# Quick Reference

| Redirect | Meaning |
|----------|----------|
| `>` | Redirect stdout (overwrite) |
| `>>` | Append stdout |
| `<` | Redirect stdin |
| `2>` | Redirect stderr |
| `2>>` | Append stderr |
| `2>&1` | Combine stderr with stdout |
| `&>` | Redirect both (bash shortcut) |

---

# Visual Flow

Keyboard → `0` → command  
Command → `1` → screen  
Errors → `2` → screen  

You can redirect any of these.

---

# Practical Exercise

1. Run:
   `ls -l > file1.txt`

2. Append:
   `date >> file1.txt`

3. Cause error:
   `ls /root 2> error.txt`

4. Combine both:
   `ls /root > combined.txt 2>&1`

5. View files:
   `cat file1.txt`
   `cat error.txt`
   `cat combined.txt`

---

# Why This Is Important

Redirection is essential for:
- Shell scripting
- Logging
- Automation
- Cron jobs
- Debugging
- System monitoring

---

# Memory Trick

`0` → Input  
`1` → Output  
`2` → Error  

Single arrow replaces.  
Double arrow appends.  

---

If you master redirection,  
you unlock real Linux automation power.

---

**✍️ Notes By Abhishek (Ez Abyss)**
