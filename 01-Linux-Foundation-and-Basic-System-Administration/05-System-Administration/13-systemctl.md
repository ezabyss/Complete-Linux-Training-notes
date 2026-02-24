# ⚙️ systemctl Command in Linux (System Control)


`systemctl` (pronounced system control) is used to manage services in modern Linux systems.

In Windows:
- You double-click an icon to start an application.

In Linux:
- Most servers run without GUI.
- Services are controlled from the terminal.
- That’s where `systemctl` comes in.

---

# 📌 What is systemctl?

`systemctl` is the command-line tool used to control `systemd`.

It is:

- Available in RHEL 7+, CentOS 7+, and modern Linux distributions
- Replacement for the older `service` command
- Used to manage services (called *units*)

---

# 🧩 Basic Syntax

`systemctl <action> <service-name>`

Common actions:

- start
- stop
- restart
- reload
- status
- enable
- disable

---

# 🔥 Example: Managing firewalld Service

We’ll use `firewalld` as an example.

---

## 🔎 Check Service Status

`systemctl status firewalld`

Output shows:

- Loaded → configuration file is recognized
- Active → whether service is running
- Enabled → whether service starts at boot
- Main PID → process ID
- Logs → recent service logs

---

## ▶ Start Service

`systemctl start firewalld`

---

## ⛔ Stop Service

`systemctl stop firewalld`

---

## 🔁 Restart Service

Used after configuration changes:

`systemctl restart firewalld`

---

## 🔄 Reload Service

Reloads configuration without full restart:

`systemctl reload firewalld`

---

# 🚀 Enable / Disable at Boot

## Enable service at boot:

`systemctl enable firewalld`

## Disable service at boot:

`systemctl disable firewalld`

---

# 📋 List Services (Units)

Every service in systemctl is called a **unit**.

---

## List Active Units

`systemctl list-units`

Columns Explained:

| Column | Meaning |
|--------|----------|
| UNIT | Name of service |
| LOAD | Whether config file is loaded |
| ACTIVE | High-level state |
| SUB | Detailed state |
| DESCRIPTION | What the service does |

---

## List All Units (Active + Inactive)

`systemctl list-units --all`

This shows:

- Active services
- Inactive services
- Failed services

---

# 📁 Where Are Service Files Stored?

Service files are stored in:

`/etc/systemd/system/`

or

`/usr/lib/systemd/system/`

Custom services must:

- Be named like `application.service`
- Follow systemd unit file format

---

# 🖥 Control Entire System

`systemctl` can also control the system itself.

## Shutdown system:

`systemctl poweroff`

## Reboot system:

`systemctl reboot`

---

# 🧠 Summary

| Command | Purpose |
|----------|----------|
| start | Start service |
| stop | Stop service |
| restart | Restart service |
| reload | Reload config |
| status | Check service status |
| enable | Start at boot |
| disable | Do not start at boot |
| list-units | Show running services |

---

# 🎯 Key Takeaway

- `systemctl` manages services.
- Replaces old `service` command.
- Controls services and system state.
- Essential for Linux administration.

---

**✍️ Notes By Abhishek (Ez Abyss)**
