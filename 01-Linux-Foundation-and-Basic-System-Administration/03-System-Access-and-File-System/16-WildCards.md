# Linux Wildcards (Globbing)
**Goal:** Understand Linux wildcards so you can *list, create, copy, move, and delete* files fast—without doing boring one-by-one work.

---

## What are wildcards?
Wildcards (also called **globs**) are special characters the **shell** (Bash/Zsh) expands into matching filenames **before** running your command.

Think of it like this:

- You type: `ls ABC*`
- The shell converts it into: `ls ABCD1-XYZ ABCD2-XYZ ...`
- Then `ls` runs on that full list.

✅ Wildcards save time  
✅ Reduce manual typing  
⚠️ Can be dangerous with `rm` if you match too broadly

---

## Wildcards you MUST know
| Wildcard | Meaning | Matches |
|---------|---------|---------|
| `*` | Zero or more characters | `A`, `AB`, `ABCD1-XYZ` |
| `?` | Exactly one character | `A1`, `AB` (if pattern fits) |
| `[ ]` | A set or range of characters | `[AB]`, `[0-9]`, `[a-z]` |
| `{ }` | Brace expansion (generate multiple strings) | `{1..9}`, `{png,jpg}` |

> Note: `{ }` is *not* a wildcard match — it *generates* text combinations.

---

## Real-world reason this matters (Corporate example)
Imagine you're a sysadmin and you have:
- **5,000 log files**
- Only the ones starting with `auth` need to be moved to an archive folder

You don’t do it one by one.

You do something like:
- `mv auth* /var/log/archive/`

That’s why wildcards are a “must-have” skill.

---

# Lab Practice (Safe + Fast)

## 1) Create 9 files quickly using `{ }`
Instead of typing touch 9 times, do:

`touch ABCD{1..9}-XYZ`

Verify:
`ls -l`

You should see:
- `ABCD1-XYZ`
- `ABCD2-XYZ`
- ...
- `ABCD9-XYZ`

✅ This is the clean way.

---

## 2) The `*` (asterisk / star) wildcard
### A) List files that start with `ABCD`
`ls ABCD*`

Meaning:
- “Show me anything that begins with `ABCD` and continues with anything (or nothing).”

### B) Delete files that start with `ABCD`
`rm ABCD*`

⚠️ Safety tip (ALWAYS do this first):
`ls ABCD*`

If the `ls` output looks correct, then run the `rm`.

---

## 3) Match files that end with something
### Remove everything that ends with `XYZ`
`rm *XYZ`

Meaning:
- “Delete anything that ends with `XYZ`.”

---

## 4) The `?` wildcard (exactly ONE character)
Example:
`ls ?BCD*`

This matches:
- `ABCD1-XYZ`
- `XBCD9-XYZ`
- but NOT `ABBCD1-XYZ` (because `?` is only ONE character)

✅ Use `?` when you know the filename structure but one character can vary.

---

## 5) Brackets `[ ]` (choose from a set / range)
### A) Match either A or B at the start
`ls [AB]BCD*`

Matches files starting with:
- `ABCD...`
- `BBCD...`

### B) Match digits 1–9
`ls ABCD[1-9]-XYZ`

Matches:
- `ABCD1-XYZ` ... `ABCD9-XYZ`

### C) Match ranges (letters)
`ls [a-z]*`

Matches anything starting with a lowercase letter.

---

# Power Moves (Common patterns you’ll actually use)

## Find by file extension
List all `.log` files:
`ls *.log`

Delete all `.tmp` files:
`rm *.tmp`

Copy all `.txt` files to a folder:
`cp *.txt notes/`

---

## Combine wildcards
List files like `report1.txt`, `report2.txt`, etc.:
`ls report?.txt`

Match `img01.png` to `img99.png`:
`ls img[0-9][0-9].png`

---

# Safety Rules (Memorize this)
✅ **Rule #1:** Before any destructive wildcard command, preview with `ls`  
Example:
- `ls a*`
- then if safe → `rm a*`

✅ **Rule #2:** Don’t use broad wildcards in important directories  
Avoid risky stuff like:
- `rm *` (especially in places like `/`, `/home`, `/etc`)

✅ **Rule #3:** Be specific
Prefer:
- `rm ABCD*`
Over:
- `rm a*`

---

# Quick Cheat Sheet
| Task | Command |
|------|---------|
| Create 9 numbered files | `touch file{1..9}` |
| List files starting with “AB” | `ls AB*` |
| List files ending with “XYZ” | `ls *XYZ` |
| Match exactly one unknown character | `ls file?.txt` |
| Match one of several letters | `ls [ABC]*` |
| Match a digit range | `ls file[0-9].txt` |

---

# Mini Practice Challenges (Do these)
1) Create files: `log1.txt` to `log5.txt`  
Use: `touch log{1..5}.txt`

2) List only `log1.txt` to `log3.txt`  
Use: `ls log[1-3].txt`

3) Delete all `.txt` logs safely  
Preview: `ls log*.txt`  
Then delete: `rm log*.txt`

<img width="1632" height="995" alt="image" src="https://github.com/user-attachments/assets/6733e9f3-ca3a-4bf7-96b3-99ad64bc5c3f" />

---

**✍️ Notes By Abhishek (Ez Abyss)**
