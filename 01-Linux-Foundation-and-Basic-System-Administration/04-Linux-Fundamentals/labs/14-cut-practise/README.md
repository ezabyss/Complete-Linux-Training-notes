Practicing cut command

---
# 🧠 Core Options

| Option | Meaning |
|--------|----------|
| `-c` | Cut by character position |
| `-b` | Cut by byte position |
| `-d` | Specify delimiter |
| `-f` | Specify field number |

---

# Quick Reference

| Task | Command |
|------|----------|
| Extract ID | `cut -d, -f1 employee-list.txt` |
| Extract Name | `cut -d, -f2 employee-list.txt` |
| Extract Department | `cut -d, -f3 employee-list.txt` |
| Extract District | `cut -d, -f5 employee-list.txt` |
| Extract Name + District | `cut -d, -f2,5 employee-list.txt` |

---

# Important Notes

- `cut` works best with structured files.
- Field numbering starts at 1.
- Always confirm delimiter first.
- CSV files use comma `,`.

---

