# Installing CentOS Stream

CentOS Stream is an enterprise-focused Linux distribution closely aligned with Red Hat Enterprise Linux (RHEL).  
It is commonly used for learning Linux system administration and server concepts.

---

## What You Need

- A laptop or desktop (Windows or macOS)
- Virtualization software:
  - VMware Workstation Player OR
  - Oracle VirtualBox
- CentOS Stream ISO file
- Minimum:
  - 2 GB RAM (4 GB recommended)
  - 20 GB disk space

---

## Installation Steps (Summary)

1. Download the CentOS Stream ISO from the official CentOS website.
2. Create a new virtual machine in VMware or VirtualBox.
3. Attach the CentOS ISO to the VM.
4. Start the VM and select “Install CentOS Stream”.
5. Configure:
   - Language
   - Time & date
   - Disk (automatic partitioning recommended)
   - Network and hostname
6. Set root password and create a user account.
7. Begin installation and wait for completion.
8. Reboot and log in.

---

## After Installation

- Verify OS version:
  cat /etc/os-release
- Update system:
  sudo dnf update -y
- Install basic tools:
  sudo dnf install -y vim curl wget

---

## Notes

- CentOS Stream is server-first and CLI-focused.
- GUI may not be installed by default.
- This setup is ideal for learning Linux fundamentals and enterprise administration.

---

**✍️ Notes By Abhishek (Ez Abyss)**
