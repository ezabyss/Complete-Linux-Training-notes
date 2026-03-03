# 🔐 Recovering Root Password in Modern Linux (RHEL 7/8/9, Rocky, Alma)  


---

# 🎯 Why This Still Matters in Modern Linux

Even today, admins lose root access due to:

- Password rotation policies
- Mistyped password (fat finger)
- Taking over old servers
- Security compliance requirements

And remember:

You cannot run:

`passwd root`

Unless you are already root.

So we must boot into recovery mode.

---

# ⚠ CRITICAL REQUIREMENT

You MUST have:

- Physical console access  
OR  
- Direct hypervisor console (VMware / VirtualBox / Cloud console)

❌ This cannot be done over normal SSH.

---

# 🧠 Version Differences Overview

| Version | Recovery Method |
|----------|----------------|
| RHEL/CentOS 7 | Modify `ro` → `rw init=/sysroot/bin/sh` |
| RHEL/Rocky/Alma 8 | Use `rd.break` |
| RHEL/Rocky/Alma 9 | Use `rd.break` (same as 8) |

Modern systems use **systemd**, not traditional runlevels.

---

# 🚀 METHOD 1 — RHEL / CentOS 7

---

## 🔹 Step 1 – Reboot

`reboot`

Interrupt GRUB.

---

## 🔹 Step 2 – Edit GRUB Entry

At GRUB menu:

Press `e`

Find the line that contains:

`ro`

Replace it with:

`rw init=/sysroot/bin/sh`

---

## 🔹 Step 3 – Boot

Press:

`Ctrl + X`

System boots into emergency shell.

---

## 🔹 Step 4 – Mount System Properly

`chroot /sysroot`

---

## 🔹 Step 5 – Change Password

`passwd`

---

## 🔹 Step 6 – Exit & Reboot

`exit`

`reboot`

---

# 🚀 METHOD 2 — RHEL / Rocky / Alma / CentOS Stream 8 & 9 (Modern Method)

This is the most common modern recovery method.

---

## 🔹 Step 1 – Reboot

`reboot`

Interrupt GRUB menu.

---

## 🔹 Step 2 – Edit GRUB Entry

Press:

`e`

Go to the line starting with:

`linux`

At the END of that line, add:

`rd.break`

Do NOT remove anything.

Just append it.

---

## 🔹 Step 3 – Boot

Press:

`Ctrl + X`

System boots into emergency mode.

You will land in:

`switch_root:/#`

---

## 🔹 Step 4 – Remount Filesystem as Read-Write

`mount -o remount,rw /sysroot`

---

## 🔹 Step 5 – Enter Real Root Environment

`chroot /sysroot`

---

## 🔹 Step 6 – Change Root Password

`passwd`

Enter new password.

---

## 🔹 Step 7 – Fix SELinux (VERY IMPORTANT)

Modern systems use SELinux.

You must run:

`touch /.autorelabel`

If you skip this step:

System may fail to boot properly.

---

## 🔹 Step 8 – Exit and Reboot

`exit`

`exit`

System reboots.

---

# 🔍 Why SELinux Relabel is Required

Changing password modifies system files.

SELinux must relabel them.

The command:

`touch /.autorelabel`

Tells system to relabel during next boot.

---

# 🆕 Modern Alternative (If systemctl Rescue Mode Available)

Some systems allow:

At GRUB, append:

`systemd.unit=rescue.target`

Then:

Boot → Enter root password (if known).

But this does NOT work if password is forgotten.

So `rd.break` remains standard.

---

# 🛡 Security Note (Very Important)

If someone has:

- Physical access
- Console access

They can reset root password.

To protect systems:

- Secure BIOS with password
- Encrypt disks (LUKS)
- Restrict console access
- Use full disk encryption

---

# 🎓 Rapid-Fire Answers (Modern)

### ❓ How do you recover root password in RHEL 8/9?
Reboot → Edit GRUB → Append `rd.break` → Remount → `chroot` → `passwd` → `touch /.autorelabel` → Reboot.

### ❓ Why is SELinux relabel required?
To restore correct file security contexts.

### ❓ Can this be done over SSH?
No.

---

# 🧠 Professional Workflow Checklist

Before performing recovery:

- Confirm physical console access
- Confirm correct machine
- Document changes
- Test in lab first

Never attempt first time in production.

---

# 🏁 Final Takeaway

Root password recovery in modern Linux:

- Requires GRUB modification
- Requires console access
- Requires SELinux relabel in 8/9
- Is a must-know admin skill

Practice this in lab environment.

This is a real-world scenario.

---

**✍️ Notes By Abhishek (Ez Abyss)**
