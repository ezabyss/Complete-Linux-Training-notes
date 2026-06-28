# 📦 Creating a Local Repository from DVD

---

# 🎯 1. What is a Repository?

A **repository (repo)** is a **storage location that contains software packages (RPMs)**. Linux uses repositories to install, update, and manage software.

> 💡 **Simple Understanding:**
> A repository is like an **App Store** for Linux.

Instead of downloading apps one by one, Linux searches the repository for the package you request.

---

# 🌍 Real-World Example

## 📱 Google Play Store / Apple App Store

When you install WhatsApp:

You don't search the internet manually.

Your phone contacts:

Google Play Store

↓

Downloads the app

↓

Installs it

Linux works exactly the same way.

Instead of Google Play Store, Linux contacts a **repository**.

---

# 🧠 2. Types of Repositories

## 1️⃣ Online Repository

Packages are stored on remote servers.

Requirements:

- Internet connection
- Access to repository

Example:

```
Linux
    ↓
Internet
    ↓
CentOS Repository
```

---

## 2️⃣ Local Repository

Packages are stored **inside your own machine**.

No internet required.

Example:

```
Linux
   ↓
Local Repository
   ↓
Packages Installed
```

---

# 🌍 Real-World Example

Imagine you're in a village with no internet.

You have a DVD containing Microsoft Office.

Instead of downloading Office online,

you install directly from the DVD.

That DVD becomes your **local software repository**.

Linux does the exact same thing.

---

# ❓ Why Create a Local Repository?

Sometimes:

- No internet access
- Company blocks internet
- Secure environments
- Military networks
- Banking servers
- Production servers

Instead of downloading packages,

Linux installs software from a DVD or local storage.

---

# 🌍 Enterprise Example

Many companies use:

**Red Hat Satellite Server**

Instead of every server downloading packages from the internet,

all servers download from the company's internal repository.

```
Internet
      ↓
Satellite Server
      ↓
Linux Servers
```

Benefits:

- Faster
- More secure
- Controlled updates

---

# 🧠 3. Important Commands

## Older CentOS (7 and below)

`createrepo`

Installed by default.

---

## CentOS Stream 8+

`createrepo_c`

Must be installed manually.

---

# 🖥️ 4. Workflow Overview

```
DVD
   ↓
Copy RPM Packages
   ↓
Create Local Repository
   ↓
Configure DNF
   ↓
Install Software
```

---

# 🛡️ 5. Before Starting

## Create VirtualBox Snapshot

Always create a snapshot before changing repository settings.

Why?

If something breaks,

restore the snapshot instead of reinstalling Linux.

---

## 🌍 Real-World Example

Think of a snapshot like:

**Save Game** 🎮

If you lose,

you simply load your previous save.

---

# 📦 6. Install createrepo_c

Become root

`su -`

Install package

`dnf install createrepo_c`

---

# 💿 7. Mount the DVD

VirtualBox:

Devices

↓

Optical Drives

↓

Choose Disk Image

↓

Select CentOS ISO

---

Linux automatically mounts it.

---

# Verify Mount

`df -h`

Example output:

```
/dev/sr0
```

Mounted under:

```
/run/media/username/CentOS-Stream-9
```

---

# If Not Mounted Automatically

Mount manually

`mount /dev/cdrom /mnt`

---

# 🌍 Real-World Example

Think of plugging in a USB drive.

Until you mount it,

Linux cannot access the files.

---

# 📂 8. Create Repository Folder

Go to root

`cd /`

Create folder

`mkdir localrepo`

Verify

`ls`

---

# 🌍 Real-World Example

Like creating a new folder called:

```
Downloads
```

before copying files into it.

---

# 📦 9. Locate RPM Packages

Navigate to DVD

`cd /run/media/...`

Go into

`AppStream`

Go into

`Packages`

List packages

`ls`

---

# Count Packages

`ls | wc -l`

Example

```
5811 RPM packages
```

---

# 🌍 Real-World Example

Imagine opening a warehouse.

Each box is an RPM package.

You count every box.

---

# 💾 10. Check Disk Space

Current package size

`du -sh .`

Check free disk

`df -h`

Ensure enough storage exists before copying.

---

# 🌍 Real-World Example

Before moving furniture,

make sure your new room has enough space.

---

# 📋 11. Copy All Packages

Copy every RPM

`cp /run/media/.../Packages/* /localrepo`

This copies thousands of RPM packages.

---

# Verify

Count copied packages

`ls /localrepo | wc -l`

Should match DVD package count.

---

# ⚙️ 12. Configure Repository

Repository files are stored here:

`/etc/yum.repos.d`

List them

`ls /etc/yum.repos.d`

---

## Backup First (Recommended)

`cp -r /etc/yum.repos.d /etc/yum.repos.d.backup`

---

## Remove Existing Repository Files (Lab Only)

`rm -rf /etc/yum.repos.d/*`

> ⚠️ Only do this in a lab. In production, disable or back up repositories instead of deleting them.

---

# Create Local Repo File

`vi /etc/yum.repos.d/local.repo`

Example:

```ini
[CentOS9]
name=CentOS 9 Local Repository
baseurl=file:///localrepo
enabled=1
gpgcheck=0
```

---

# Understanding Configuration

## baseurl

Repository location.

```
file:///localrepo
```

Means:

Look inside localrepo folder.

---

## enabled=1

Repository is active.

---

## gpgcheck=0

Disable GPG verification.

Mostly used in labs.

Production usually keeps:

```
gpgcheck=1
```

---

# 🌍 Real-World Example

Imagine giving GPS directions.

Instead of:

```
Go to Google Store
```

You tell Linux:

```
Go to local warehouse.
```

---

# 🏗️ 13. Create Repository Metadata

Command

`createrepo_c /localrepo`

This generates metadata.

Without metadata,

Linux cannot search packages.

---

# 🌍 Real-World Example

Think of a library.

Books exist.

But without a catalog,

nobody knows where the books are.

Metadata = Library Catalog

---

# 🧹 14. Clean DNF Cache

`dnf clean all`

Removes old repository cache.

---

# 📋 15. Verify Repository

`dnf repolist`

Example

```
repo id      : CentOS9
status       : enabled
```

---

# 📦 16. Test Repository

Install Apache

`dnf install httpd`

Linux now installs directly from:

```
Local Repository
```

instead of

```
Internet Repository
```

---

# 🌍 Real-World Example

Instead of ordering food online,

you walk to your own kitchen.

Faster.

No internet.

---

# 🔄 Complete Workflow

```
CentOS DVD
      ↓
Mount DVD
      ↓
Locate Packages
      ↓
Copy RPMs
      ↓
Create Repository
      ↓
Configure DNF
      ↓
Clean Cache
      ↓
Install Software
```

---

# 🧠 Memory Tricks

Remember:

**DVD → Copy → Repository → Install**

Easy shortcut:

> **"Copy, Create, Configure, Clean, Install."**

---

# 🚨 Common Problems

| Problem | Cause | Solution |
|----------|-------|----------|
| `createrepo_c` not found | Package missing | `dnf install createrepo_c` |
| Repository not detected | Wrong baseurl | Check `local.repo` |
| No space left | Disk full | Check `df -h` |
| Package not found | Metadata missing | Run `createrepo_c` |
| Old cache | Cached repository | `dnf clean all` |

---

# 💼 Interview Questions

## Q1. What is a repository?

A storage location containing software packages.

---

## Q2. Why create a local repository?

To install software without internet access.

---

## Q3. Which command creates repository metadata?

`createrepo_c`

---

## Q4. Where are repository configuration files stored?

`/etc/yum.repos.d`

---

## Q5. Why run `dnf clean all`?

To clear old repository cache.

---

## Q6. What does `baseurl=file:///localrepo` mean?

Use the local folder as the software source.

---

## Q7. What is RPM?

**RPM (Red Hat Package Manager)** is the package format used by Red Hat-based Linux distributions.

---

# 📌 Ultra Short Revision

- Repository = Linux App Store
- Online Repo = Internet required
- Local Repo = DVD/local storage
- Install tool = `dnf install createrepo_c`
- Create folder = `mkdir localrepo`
- Copy RPMs = `cp`
- Create metadata = `createrepo_c /localrepo`
- Clear cache = `dnf clean all`
- Verify = `dnf repolist`
- Test = `dnf install httpd`

---

# 🏆 Takeaway

A **repository** is where Linux finds software packages.

Normally, Linux downloads packages from the internet. When there is **no internet**, you can **build your own local repository** from a DVD or ISO. This allows you to install and update software in isolated or secure environments, making local repositories essential for enterprise, military, banking, and offline systems.

---

# ✍️ Notes By Abhishek (Ez Abyss)
