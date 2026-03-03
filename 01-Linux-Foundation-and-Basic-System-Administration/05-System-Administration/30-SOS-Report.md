# 🆘 SOS Report (sosreport) 

---

# 🎯 What is SOS Report?

SOS is historically a distress signal (Save Our Ship / Save Our Souls).

In Linux (RHEL-based systems), `sosreport` follows the same concept:

It is used when your system is in trouble.

The command:

`sosreport`

Collects:

- System configuration
- Logs
- Kernel info
- Hardware info
- Running services
- Installed packages
- Network configuration

Then packages everything into a compressed archive for support analysis.

---

# 🧠 Why It Exists

When opening a support case with:

- Red Hat
- Rocky Linux support
- AlmaLinux support
- Enterprise vendor

They request:

> Please provide sosreport.

Why?

Because instead of asking you for 20 different files,
they get everything at once.

---

# 📦 Package Name (Modern Versions)

## RHEL 7

Package name:

`sos`

## RHEL 8 / 9 (Modern)

Package name:

`sos`

Install if missing:

`dnf install sos`

Or older systems:

`yum install sos`

---

# 🚀 Running sosreport

⚠ Must be root.

Become root:

`su -`

Then run:

`sosreport`

---

# 🧾 What Happens Next?

You will see:

- Version of sosreport
- Warning message
- Prompt to continue

Press:

Enter

---

# 📝 It Will Ask For:

1. First initial & last name
2. Case ID (provided by Red Hat support)

Example:

9009000

---

# 🔄 What It Collects

- `/etc` configuration files
- `/var/log` logs
- Kernel info
- Hardware info
- Network config
- Running services
- RPM database
- Memory & CPU info

It creates a compressed `.tar.xz` archive.

---

# 📂 Where Report Is Saved

Typically:

`/var/tmp/`

Check:

`cd /var/tmp`

`ls -ltr`

Example file:

`sosreport-hostname-123456-2024-07-01.tar.xz`

---

# 📤 How to Send It to Support

Options:

- Upload via Red Hat portal
- SCP to your workstation
- FTP upload
- Web upload

Example copy to remote machine:

`scp sosreport-file.tar.xz user@remote:/home/user/`

---

# 🆕 Modern Alternative (RHEL 8/9)

Modern systems use:

`sos report`

Notice space between.

Example:

`sos report`

It works same as `sosreport`.

---

# 🔐 Security Warning

⚠ sosreport contains:

- Configuration files
- Network settings
- Possibly sensitive data

Always:

- Review before sharing
- Share only with trusted support

---

# 🎓 Rapid-Fire Answers

### ❓ What is sosreport used for?
Collecting system diagnostics for support.

### ❓ Where is sosreport stored?
`/var/tmp`

### ❓ Is root required?
Yes.

### ❓ Why is it useful?
Reduces back-and-forth troubleshooting.

---

# 🧠 Real-World Admin Workflow

When system issue cannot be resolved:

1. Try local troubleshooting
2. If unresolved → open support case
3. Run `sosreport`
4. Upload report
5. Support analyzes it

---

# 🏗 What’s Inside the Archive?

You can inspect without extracting:

`tar -tf sosreport-file.tar.xz`

Extract:

`tar -xvf sosreport-file.tar.xz`

---

# 🏁 Final Takeaway

`sosreport` is:

- Mandatory for enterprise support
- A complete system snapshot
- A must-know admin tool

Every serious Linux administrator must know this command.

---

**✍️ Notes By Abhishek (Ez Abyss)**
