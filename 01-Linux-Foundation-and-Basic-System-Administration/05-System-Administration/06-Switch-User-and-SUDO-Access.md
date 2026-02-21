# 🔄 Switching Users & Using sudo in Linux

---

# 🔁 Switch From One User to Another

To switch users in Linux, use:

    su - username

Example:

    su - spiderman

- `su` = switch user  
- `-` = load that user's full login environment  
- System will prompt for the user's password  

After successful authentication, you become that user.

---

# 👑 Switch to Root User

To become root:

    su -

You must enter the root password.

If you are already root and switch to another user:

    su - spiderman

It will NOT ask for password because root has full privileges.

---

# 🔙 Exit Back to Previous User

To return:

    exit

Each `exit` moves you back one level.

---

# 🌐 Finding Your Linux IP Address

To check IP address:

    ifconfig

Or (modern systems):

    ip a

Look for your main network interface (example: `eth0` or `ens33`).

Ignore:

- `lo` → Local loopback
- Virtual or private interfaces

---

# 🔐 Using sudo (Super User Do)

Instead of switching to root, you can use:

    sudo command

Example:

    sudo fdisk -l

It will:

- Ask for your password (not root password)
- Run the command with root privileges

---

# ⚠️ Why sudo May Fail

If you see:

    permission denied

It means your user is not allowed to use sudo.

---

# 🛠 How sudo Permission Works

Permission is controlled by:

    /etc/sudoers

Open safely:

    visudo

Look for this line:

    %wheel  ALL=(ALL)  ALL

OR (on some systems):

    %sudo   ALL=(ALL:ALL) ALL

Users inside that group can run sudo.

---

# 👥 Add User to sudo Group

On RHEL/CentOS systems:

    usermod -aG wheel username

On Ubuntu/Debian systems:

    usermod -aG sudo username

Example:

    usermod -aG wheel abhi

---

# 🔎 Verify Group Membership

    groups abhi

Or:

    grep wheel /etc/group

---

# 🔄 Apply Changes

User must log out and log back in.

Then test:

    sudo whoami

If successful, it should output:

    root

---

# 🧠 su vs sudo

| Command | Description |
|----------|-------------|
| `su -` | Switch completely to another user |
| `sudo` | Run one command as root |
| `exit` | Return to previous user |

---

# 🔐 Why sudo Is Safer Than su

- Logs all commands
- Limits access
- Avoids full root login
- Better for security

---

# 🎯 Key Takeaways

- Use `su - username` to switch users  
- Use `sudo` to run privileged commands  
- Root does not need password to switch users  
- Sudo access is controlled via group membership  
- Always edit sudoers using `visudo`  

---

**✍️ Notes By Abhishek (Ez Abyss)**  
