# VI Editor — Linux File Editor

---

# 📝 What Is an Editor?

An editor is a program used to:

- Create files
- Modify text
- Insert, delete, replace content
- Search inside files
- Save changes

Common Linux editors:

- `vi`
- `vim` (advanced version of vi)
- `nano`
- `emacs`

We focus on **`vi`** because:

- It exists on almost every Linux system
- Works in minimal environments
- Required skill for system administrators

---

# 🧠 Two Modes in `vi`

Understanding this is critical.

## 1️⃣ Command Mode (Default Mode)

When you open a file:

    vi filename

You are in **command mode**.

In this mode:
- You cannot type text normally
- Keys perform actions (delete, move, copy, etc.)

---

## 2️⃣ Insert Mode

To start typing:

    i

You will see:

    -- INSERT --

Now you can type normally.

To exit insert mode:

    Esc

**Esc is your lifesaver key.**

---

# 📁 Create Your First File

Open a new file:

    vi myfile.txt

You are now in command mode.

Press:

    i

Type:

    Hello world
    I am learning vi editor.

Press:

    Esc

---

# 💾 Save and Exit

### Method 1

Press:

    Shift + ZZ

---

### Method 2

Press:

    :wq!

Then press Enter.

---

# 🚪 Quit Without Saving

If you made mistakes and want to exit:

    Esc
    :q!

---

# 🧹 Delete Text

## Delete One Character

Move cursor to character and press:

    x

---

## Delete Entire Line

Press:

    dd

---

## Undo Last Change

Press:

    u

---

# ✏ Replace Text

## Replace One Character

Move cursor to character and press:

    r

Then type replacement letter.

---

## Better Method to Replace a Word

1. Move cursor to word
2. Press `x` multiple times to delete
3. Press `i` to insert new word
4. Press `Esc`

---

# ➕ Add New Line

## Add Line Below

Press:

    o

Automatically enters insert mode.

---

## Add Line Above

Press:

    O

---

# 🔎 Search Inside File

While in command mode:

    /word

Example:

    /lesson

Press Enter.

To move to next match:

    n

---

# 📌 Movement Keys

| Key | Action |
|------|--------|
| `h` | Move left |
| `l` | Move right |
| `j` | Move down |
| `k` | Move up |

Arrow keys also work.

---

# ⚠ Common Beginner Mistake

Typing but nothing works?

You're probably in the wrong mode.

Always remember:

    Esc

Then continue.

---

# 🧠 Important Survival Commands

| Command | Meaning |
|----------|----------|
| `i` | Insert |
| `a` | Append |
| `o` | New line below |
| `x` | Delete character |
| `dd` | Delete line |
| `u` | Undo |
| `:wq` | Save and quit |
| `:q!` | Quit without saving |
| `/text` | Search |

---

# 🎯 Real-World Tip

In production Linux servers:

- GUI is usually not installed
- `vi` is often your only editor
- Config files must be edited via terminal

Mastering `vi` = professional Linux skill.

---

# 💡 Practice Exercise

1. Create a file.
2. Insert 5 lines.
3. Delete one line.
4. Replace one word.
5. Search for a word.
6. Save and exit.
7. Reopen and verify.

Practice until it becomes muscle memory.

---

# Final Thought

`vi` feels hard at first.

But once mastered,  
it becomes extremely fast and powerful.

This is one skill every Linux administrator must have.

---

**✍️ Notes By Abhishek (Ez Abyss)**  
