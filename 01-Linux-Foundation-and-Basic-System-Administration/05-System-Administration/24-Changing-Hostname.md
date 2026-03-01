# 🖥️ Changing Linux Hostname

---

# 🎯 What is a Hostname?

Hostname = The unique name assigned to a Linux machine.

It identifies:

- Servers in a network
- Systems in a domain
- Machines in enterprise infrastructure

Example:

`web-prod-01`  
`db-ktm-02`  
`backup-server`

---

# 🧠 Why Change Hostname?

You change hostname when:

- Server is repurposed
- Company naming standards change
- System is migrated to new environment
- Machine is cloned
- Old server is decommissioned

---

# 🔎 Check Current Hostname

`hostname`

---

# 📂 Where Hostname is Stored

## In Linux 7+ (CentOS 7, RHEL 7+)

Stored in:

`/etc/hostname`

Check:

`cat /etc/hostname`

---

## In Older Linux (CentOS 6)

Stored in:

`/etc/sysconfig/network`

---

# 🚀 Recommended Method (Modern Way)

Use `hostnamectl`

---

## Change Hostname

`hostnamectl set-hostname new-hostname`

Example:

`hostnamectl set-hostname vmware-host-01`

---

# 🔐 Root Required

To change hostname:

`su -`

or

`sudo hostnamectl set-hostname vmware-host-01`

---

# 🧠 What Happens Internally?

When you run:

`hostnamectl set-hostname vmware-host-01`

It:

1. Updates `/etc/hostname`
2. Updates systemd configuration
3. Sets new hostname immediately

---

# 🔍 Verify Change

Check file:

`cat /etc/hostname`

Check system hostname:

`hostname`

---

# ⚠ Why Prompt Still Shows Old Name?

Your shell session was started before hostname changed.

To refresh:

- Log out and log back in
OR
- Reboot system

---

# 🔄 Reboot System

`reboot`

OR

`init 6`

After reboot → Prompt reflects new hostname.

---

# 🛠 Alternative Method (Manual Edit)

You can manually edit:

`vi /etc/hostname`

Change value → Save → Reboot.

⚠ Not recommended over `hostnamectl`.

---

# 🧠 Temporary Hostname Change (Not Persistent)

`hostname temporary-name`

⚠ This change is lost after reboot.

---

# 🎓 Rapid-Fire Answers

### ❓ How do you check hostname?
`hostname`

### ❓ How do you permanently change hostname?
`hostnamectl set-hostname new-name`

### ❓ Where is hostname stored in Linux 7?
`/etc/hostname`

### ❓ Does hostname change require reboot?
Not required, but recommended to refresh shell.

---

# 🏗 Real-World Naming Convention Example

Enterprise naming example:

`ktm-web-prod-01`

Breakdown:

- Location → ktm
- Role → web
- Environment → prod
- Instance → 01

Good naming = Better infrastructure management.

---

# 🧠 Best Practice Workflow

Before changing hostname:

1. Confirm current hostname → `hostname`
2. Confirm correct server → `hostname`
3. Become root
4. Run `hostnamectl set-hostname new-name`
5. Verify with `hostname`
6. Reboot if necessary

---

# 🏁 Final Takeaway

Changing hostname is simple.

But:

- Always verify server first
- Use `hostnamectl`
- Understand where it's stored
- Know difference between temporary & permanent change

Small command. Big responsibility.

---

**✍️ Notes By Abhishek (Ez Abyss)**
