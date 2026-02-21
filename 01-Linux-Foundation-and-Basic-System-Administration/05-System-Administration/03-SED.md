# `sed` Command — Stream Editor (Substitute & Manipulate Text)

---

# 📌 What Is `sed`?

`sed` (Stream Editor) is a powerful Linux text-processing command used to:

- Replace text
- Delete lines
- Remove empty lines
- Print specific lines
- Modify large files automatically

Unlike `vi`, `sed` works non-interactively and is ideal for automation.

---

# 🧠 Basic Syntax

    sed 'command' filename

To modify file permanently:

    sed -i 'command' filename

⚠️ Without `-i`, it only displays output on screen.

---

# 🧪 Example File — `Nepal.txt`

Assume `Nepal.txt` contains:

    Nepal is a beautiful country.
    Tourism is important in Nepal.
    It is known for mountains.
    Life in Nepal is peaceful.

---

# 1️⃣ Replace a Word Globally

Replace "Nepal" with "MyCountry":

    sed 's/Nepal/MyCountry/g' Nepal.txt

To save changes:

    sed -i 's/Nepal/MyCountry/g' Nepal.txt

---

# 2️⃣ Replace Word Except Line 3

Now let’s include your example:

Replace `is` with `iz` **in all lines except line 3**:

    sed '3!s/is/iz/g' Nepal.txt

Explanation:

- `3!` → NOT line 3  
- `s/is/iz/` → substitute  
- `g` → replace all matches in each line  

Output would look like:

    Nepal iz a beautiful country.
    Tourism iz important in Nepal.
    It is known for mountains.
    Life in Nepal iz peaceful.

Notice:
- Line 3 remains unchanged.
- All other lines replace `is` → `iz`.

To apply permanently:

    sed -i '3!s/is/iz/g' Nepal.txt

---

# 3️⃣ Delete Lines Containing a Word

Delete lines containing "Tourism":

    sed '/Tourism/d' Nepal.txt

Permanent:

    sed -i '/Tourism/d' Nepal.txt

---

# 4️⃣ Remove Empty Lines

    sed '/^$/d' Nepal.txt

---

# 5️⃣ Delete First Line

    sed '1d' Nepal.txt

Delete first two lines:

    sed '1,2d' Nepal.txt

---

# 6️⃣ Print Specific Line Range

Print lines 2 to 3:

    sed -n '2,3p' Nepal.txt

---

# 7️⃣ Replace Tabs With Spaces

    sed 's/\t/ /g' Nepal.txt

---

# 8️⃣ Add Blank Line After Each Line

    sed G Nepal.txt

---

# 🧠 Inside `vi` Equivalent

Inside `vi` you can do:

    :%s/is/iz/g

To replace in entire file.

---

# 🔥 Real-World Example

If a 500MB log file contains thousands of lines with:

    DEBUG

And you want to remove them:

    sed -i '/DEBUG/d' logfile.txt

Instant cleanup.

---

# ⚠ Important Rules

- Always test without `-i` first.
- `g` ensures global replacement in line.
- Line-specific control like `3!` is very powerful.
- `sed` is case-sensitive unless specified otherwise.

---

# 🎯 Final Takeaway

`sed` is:

- Fast
- Scriptable
- Extremely powerful for bulk operations

For large-scale text manipulation,  
`sed` is far superior to manual editing.

Practice carefully before using `-i` in production.

---

**✍️ Notes By Abhishek (Ez Abyss)**  
