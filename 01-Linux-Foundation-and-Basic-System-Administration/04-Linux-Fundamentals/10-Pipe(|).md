# Pipes in Linux (`|`) — Connecting Commands Like a Pro

---

## What Is a Pipe?

A **pipe** connects the output of one command directly to the input of another command.

Symbol:

    |

Think of it like a conveyor belt:

    Command 1 → Output → Pipe → Command 2 → Processed Output

Instead of saving output to a file, a pipe sends it directly into another command.

---

# Basic Syntax

    command1 | command2

You can also include options and arguments:

    command1 -option | command2 -option

---

# Why Pipes Are Powerful

Without pipes:
- You run a command
- Save output to a file
- Then run another command on that file

With pipes:
- No temporary file needed
- Direct command chaining
- Faster and cleaner workflows

---

# Example 1 — Large Directory Output

Go to `/etc`:

    cd /etc

Run listing:

    ls -ltr

Problem:
Too much output scrolls quickly.

---

## Solution — Use `more`

    ls -ltr | more

Now:
- Output appears one page at a time
- Press Space → next page
- Press Q → quit

This makes large outputs readable.

---

# Example 2 — Get Only the Last Line

    ls -ltr | tail -1

Explanation:
- `ls -ltr` lists files
- `tail -1` returns only the last line

Result:
Only the newest file (since `-tr` sorts by time).

---

# Example 3 — Count Files

    ls | wc -l

Explanation:
- `ls` lists files
- `wc -l` counts lines

Result:
Total number of files in directory.

---

# Example 4 — Filter Output with `grep`

    ls -l | grep ".conf"

Explanation:
- `ls -l` lists files
- `grep ".conf"` filters only config files

Very useful for security analysis.

---

# Example 5 — View Hidden Files Only

    ls -la | grep "^."

Explanation:
- `ls -la` shows hidden files
- `grep "^."` filters dot files

---

# Pipe Flow Visualization

    [Command 1] → (Output) → | → [Command 2] → (Refined Output)

Example:

    ls -l | grep root | wc -l

Step-by-step:
1. `ls -l` → list files
2. `grep root` → show only files owned by root
3. `wc -l` → count them

This is command chaining.

---

# Real-World Security Example

Find failed login attempts:

    cat auth.log | grep "Failed password"

Or better:

    grep "Failed password" auth.log

(Still internally similar to piping)

Count failed attempts:

    grep "Failed password" auth.log | wc -l

This is common SOC workflow.

---

# Combine with `tee`

You can mix pipes with `tee`:

    ls -l | tee listing.txt | grep ".log"

This:
- Saves full listing
- Filters only `.log` files
- Displays filtered output

---

# Why Pipes Are Critical in Cybersecurity

Pipes allow you to:

- Analyze logs quickly
- Chain filters
- Count events
- Extract specific data
- Build automation scripts
- Perform incident triage faster

Most Linux-based security tools rely heavily on pipes.

---

# Important Note

A pipe is not a command.
It is a shell operator.

That’s why:

    man |

does not work.

---

# Quick Memory Rule

Redirect (`>`) → Send output to file  
Pipe (`|`) → Send output to another command  

---

# Practice Exercises

1. Count number of users in `/etc/passwd`
2. List only `.conf` files in `/etc`
3. Show only last 5 files sorted by time
4. Count how many directories exist in `/etc`

---

# Final Thought

If you master pipes,  
you master Linux efficiency.

Pipes are the foundation of:
- Shell scripting
- Log analysis
- Security automation
- System administration

---

**✍️ Notes By Abhishek (Ez Abyss)**
