# 🔐 Recovering Root Password in Linux

---

# 🎯 Why Root Password Recovery Matters

Every system administrator will eventually face this situation:

- Password expired and forgotten
- Mistyped password during change (fat-finger error)
- Inherited system with unknown root password
- Compliance policy required password change

Problem:

To change root password, you must be root.  
But to become root, you need the password.

Classic Catch-22.

---

# ⚠ Critical Requirement

You MUST have:

- Physical console access
OR
- Direct VM console access (VirtualBox, VMware, Cloud Console)

⚠ This cannot be done over normal SSH if password is unknown.

---

# 🧠 High-Level Recovery Process

1. Reboot system
2. Interrupt GRUB boot menu
3. Edit kernel parameters
4. Boot into single-user mode
5. Remount filesystem as read-write
6. Change root password
7. Reboot normally

---

# 🚀 Step-by-Step Recovery (CentOS / RHEL 7)

---

## 🔹 Step 1 – Reboot System

`reboot`

You must be physically present or using console.

---

## 🔹 Step 2 – Interrupt GRUB Menu

When GRUB menu appears:

Press `e` to edit boot entry.

⚠ You must act quickly (default timeout ~5 seconds).

---

## 🔹 Step 3 – Modify Kernel Line

Find line that contains:

`ro`

This means system mounts as read-only.

Replace `ro` with:

`rw init=/sysroot/bin/sh`

Example modification:

Change:

ro

To:

rw init=/sysroot/bin/sh

---

## 🔹 Step 4 – Boot With Modified Parameters

Press:

`Ctrl + X`

System boots into emergency shell.

---

# 🔹 Step 5 – Mount System Properly

Remount root filesystem:

`chroot /sysroot`

This makes `/sysroot` your active root environment.

---

# 🔹 Step 6 – Change Root Password

`passwd`

Enter new root password.

You should see:

Password updated successfully.

---

# 🔹 Step 7 – Exit and Reboot

Exit chroot:

`exit`

Then reboot:

`reboot`

System starts normally.

Login with new root password.

---

# 🆕 For RHEL 8 / CentOS 8 / 9

Instead of modifying `ro`, add at end of kernel line:

`rd.break`

Then:

Press `Ctrl + X`

After boot:

Remount filesystem:

`mount -o remount,rw /sysroot`

Then:

`chroot /sysroot`

Change password:

`passwd`

Create SELinux autorelabel file:

`touch /.autorelabel`

Exit and reboot:

`exit`
`reboot`

---

# 🧠 Why SELinux Relabel Is Needed (Newer Systems)

If SELinux is enabled, after password change:

You must run:

`touch /.autorelabel`

Or system may fail to boot properly.

---

# 🎓 Rapid-Fire Answers

### ❓ How do you recover root password?
Reboot → Edit GRUB → Boot into single-user → Change password → Reboot.

### ❓ Why can’t you just run `passwd root`?
Because you must already be root to do that.

### ❓ Why is console access required?
Because SSH requires password authentication first.

---

# ⚠ Security Consideration

If someone has:

- Physical access
- Console access

They can reset root password.

Solution:

- Secure server room
- Use BIOS password
- Encrypt disk
- Secure cloud console access

---

# 🧠 Professional Mindset

Good administrators:

- Document recovery steps
- Practice in lab
- Understand differences between versions
- Verify SELinux behavior

---

# 🏁 Final Takeaway

Root password recovery:

- Is a real-world task
- Requires calm execution
- Requires console access
- Is a must-know skill

Practice it in your lab.

Never practice first time in production.

---

**✍️ Notes By Abhishek (Ez Abyss)**
