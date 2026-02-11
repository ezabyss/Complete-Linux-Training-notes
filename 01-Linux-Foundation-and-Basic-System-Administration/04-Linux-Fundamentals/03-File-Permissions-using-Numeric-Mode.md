# Linux File Permissions (Numeric Method – chmod with Numbers)

---

## Why learn numeric permissions?

You already know how to use letters:

`chmod ugo+r file`

But in real-world Linux administration, **numeric permissions are faster, cleaner, and more professional**.

Example:
Instead of:
`chmod ugo+r file`

You can simply write:
`chmod 444 file`

Both do the same thing.

---

# Permission Structure Refresher

Every file has permissions divided into **three groups**:

| Position | Applies To |
|----------|-----------|
| First 3 bits | User (Owner) |
| Second 3 bits | Group |
| Last 3 bits | Others |

When you see:

`-rwxrw-r--`

Break it into:

`rwx` → User  
`rw-` → Group  
`r--` → Others  

---

# Numeric Permission Table (MEMORIZE THIS)

Each permission has a numeric value:

| Permission | Value |
|------------|-------|
| No permission | `0` |
| Execute | `1` |
| Write | `2` |
| Write + Execute | `3` |
| Read | `4` |
| Read + Execute | `5` |
| Read + Write | `6` |
| Read + Write + Execute | `7` |

---

# How Numbers Work (Binary Logic)

Permissions are **added together**.

- Read = `4`
- Write = `2`
- Execute = `1`

So:

- `4 + 2 = 6` → Read + Write  
- `4 + 1 = 5` → Read + Execute  
- `4 + 2 + 1 = 7` → Read + Write + Execute  

---

# Understanding chmod 764

Command:
`chmod 764 file`

Breakdown:

- `7` → User → Read + Write + Execute
- `6` → Group → Read + Write
- `4` → Others → Read only

Result:
`rwxrw-r--`

---

# Lab Practice (Step-by-Step)

## Step 1: Create a file
`touch Abyss`

Check default permissions:
`ls -ltr`

---

## Step 2: Assign 764 permission
`chmod 764 Abyss`

Verify:
`ls -ltr Abyss`

You should see:
- User → `rwx`
- Group → `rw-`
- Others → `r--`

---

## Step 3: Remove all permissions
`chmod 000 Abyss`

Verify:
`ls -ltr Abyss`

Result:
`----------`

No one has access.

---

## Step 4: Give only User Read + Write

Read + Write = `6`

`chmod 600 Abyss`

Verify:
`ls -ltr Abyss`

Result:
- User → `rw-`
- Group → `---`
- Others → `---`

---

## Step 5: Give Others Read Permission Only

Read = `4`

If current permission is `600` and you want:
- User → Read + Write (`6`)
- Group → No permission (`0`)
- Others → Read (`4`)

Run:
`chmod 604 Abyss`

Verify:
`ls -ltr Abyss`

Result:
`rw----r--`

---

## Step 6: Give Execute Permission to Everyone

Execute = `1`

To give execute only:
`chmod 111 Abyss`

Verify:
`ls -ltr Abyss`

Result:
`--x--x--x`

Everyone can execute, but cannot read or write.

---

# Most Common Numeric Permissions (Real World)

| Permission | Meaning | Common Use |
|------------|--------|------------|
| `777` | Full access to everyone | Avoid in production |
| `755` | Owner full, others read + execute | Scripts, programs |
| `644` | Owner read/write, others read | Most files |
| `600` | Owner only | Sensitive files |
| `700` | Owner full only | Private scripts |

---

# Real-World Security Advice

❌ Avoid `777` in production  
✔ Use `644` for regular files  
✔ Use `755` for executable scripts  
✔ Use `600` for private configs  

---

# Numeric vs Letter Method

### Letter Method
`chmod u+rwx,g+rw,o+r file`

### Numeric Method
`chmod 764 file`

Numeric is:
- Faster
- Cleaner
- Preferred in automation

---

# Memory Trick

Think of it like this:

- `4` = Read  
- `2` = Write  
- `1` = Execute  

Add them to get the number you want.

---

# One-Line Rule

First digit → User  
Second digit → Group  
Third digit → Others  

---

# Bonus Tip

If you forget numbers:
Search online:
`chmod calculator`

Many free tools instantly convert checkboxes into numeric values.

---

If you understand this fully → you now control Linux file security like a system administrator.

---

**✍️ Notes By Abhishek (Ez Abyss)**
 
