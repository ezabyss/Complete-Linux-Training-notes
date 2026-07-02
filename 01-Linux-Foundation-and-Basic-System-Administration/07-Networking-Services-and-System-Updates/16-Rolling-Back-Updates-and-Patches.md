# 🔙 Rolling Back Updates & Patches — Master Notes

---

# 🎯 1. What is Rollback?

**Rollback** means undoing an update, patch, or package installation.

Used when a new update causes problems.

---

# 🌍 Real-World Example

Imagine your phone updates overnight.

After update:

- App crashes
- Battery drains
- Features break

You may want to go back to the older version.

That is rollback.

---

# 🧠 2. Why Rollback is Needed

Updates can sometimes cause:

- Application compatibility issues
- Database problems
- Service failures
- Package dependency issues
- System instability

---

# 🛡️ 3. Best Practice Before Updating

## If using Virtual Machine

Always take a **snapshot** before updates.

Snapshot = saved state of VM.

If update breaks system, restore snapshot.

---

# 🌍 Real-World Example

Snapshot is like a **save point in a video game**.

If you lose, you go back to the saved point.

---

# 🖥️ 4. Virtual Machine vs Physical Machine

| Machine Type | Rollback Option |
|---|---|
| Virtual Machine | Snapshot restore |
| Physical Machine | Yum history rollback |
| Physical Machine | Backup restore |

---

# ⚠️ 5. Important Warning

Rolling back a full system update is **not always safe**.

It can leave system unstable.

Best option:

- Use VM snapshot
- Use backup
- Test updates first
- Avoid full downgrade unless required

---

# 🔄 6. Update vs Upgrade

## yum update

`yum update`

- Updates packages
- Preserves older packages
- Easier to rollback

---

## yum upgrade

`yum upgrade`

- Updates packages
- Removes obsolete packages
- Harder to rollback

---

# ⭐ Top Rule

Use:

`yum update`

instead of:

`yum upgrade`

when rollback might be needed.

---

# 📦 7. Rollback Single Package

## Step 1: Install package

`yum install screen`

---

## Step 2: Verify package

`rpm -qa | grep screen`

---

## Step 3: Check yum history

`yum history`

Example:

```text
ID | Command line | Date and time | Action
17 | install screen | ... | Install
```

---

## Step 4: Undo package install

`yum history undo 17`

---

## Step 5: Verify removal

`rpm -qa | grep screen`

---

# 🌍 Real-World Example

You installed a new printer driver.

It caused printing issues.

You remove only that driver.

That is single-package rollback.

---

# 🔁 8. Rollback Full System Update

## Step 1: Run update

`yum update`

---

## Step 2: Check history

`yum history`

Example:

```text
19 | update | ... | Update
```

---

## Step 3: Undo update

`yum history undo 19`

---

# ⚠️ Warning

Full update rollback may downgrade many packages.

Example:

```text
159 packages to downgrade/remove
```

Only do this if:

- You have snapshot
- You have backup
- You understand risk
- You have admin approval

---

# 🧪 9. Safer Lab Workflow

1. Take VM snapshot
2. Run update
3. Test application
4. If broken, revert snapshot
5. If no snapshot, use `yum history undo`

---

# 🧠 10. Important Commands

| Task | Command |
|---|---|
| Install package | `yum install screen` |
| Check package | `rpm -qa | grep screen` |
| View yum history | `yum history` |
| Undo transaction | `yum history undo ID` |
| Update system | `yum update` |
| Upgrade system | `yum upgrade` |

---

# 🚨 11. Common Problems

| Problem | Cause | Best Fix |
|---|---|---|
| App breaks after update | Compatibility issue | Rollback or snapshot |
| No rollback available | Used upgrade | Restore backup |
| System unstable | Full downgrade issue | Rebuild or restore |
| Package still exists | Wrong history ID | Check `yum history` |

---

# 🧠 12. Memory Tricks

Remember:

- Snapshot first
- Update safer than upgrade
- `yum history` shows past actions
- `yum history undo ID` reverses action

Easy formula:

> **Snapshot → Update → Test → Rollback if needed**

---

# 💼 Interview Questions

## Q1. What is patch rollback?

Undoing an update or patch after it causes problems.

---

## Q2. Best practice before applying updates?

Take a VM snapshot or backup.

---

## Q3. Which command shows yum history?

`yum history`

---

## Q4. How do you undo a yum transaction?

`yum history undo ID`

---

## Q5. Difference between yum update and yum upgrade?

`yum update` preserves older packages.

`yum upgrade` removes obsolete packages.

---

## Q6. Is full system downgrade recommended?

No. It can make the system unstable.

---

# 📌 Ultra Short Revision

- Rollback = undo update/package
- Best method = VM snapshot
- Check history = `yum history`
- Undo = `yum history undo ID`
- Use `yum update` instead of `yum upgrade`
- Full rollback is risky

---

# 🏆 Takeaway

A strong Linux admin never updates blindly.

Before patching:

- Take snapshot
- Check backup
- Understand risk
- Test application
- Keep rollback plan ready

Rollback is not the main solution.

**Preparation is the real solution.**

---

# ✍️ Notes By Abhishek (Ez Abyss)
