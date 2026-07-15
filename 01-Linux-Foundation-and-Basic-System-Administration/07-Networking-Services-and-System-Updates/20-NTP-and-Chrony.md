# 🕒 NTP and Chrony — Network Time Synchronization

---

## 🎯 1. What is NTP?

**NTP** stands for **Network Time Protocol**.

It is used to synchronize the date and time of computers and servers over a network.

> **Simple understanding:** NTP ensures that all computers use the same accurate clock.

---

## 🌍 2. Real-World Example

Imagine a company with several employees.

Every employee has a watch, but each watch shows a slightly different time:

```text
Employee A → 10:00:00
Employee B → 10:00:15
Employee C → 09:59:48
```

If everyone follows their own watch, meetings and tasks may happen at different times.

Instead, everyone synchronizes their watch with one official clock:

```text
Official clock → 10:00:00
```

NTP works the same way for computers.

---

# 🧠 3. Why Is Time Synchronization Important?

Correct time is essential for:

* System logs
* Security monitoring
* User authentication
* Database transactions
* Clustered servers
* File timestamps
* Scheduled jobs
* Digital certificates
* Backup operations
* Incident investigations

---

## Example: Security Logs

Suppose three servers record the same cyberattack.

Without synchronized time:

```text
Web server:      Attack at 10:05
Database server: Attack at 10:09
Firewall:        Attack at 10:02
```

The security analyst may struggle to determine the correct order of events.

With NTP:

```text
Web server:      Attack at 10:05
Database server: Attack at 10:05
Firewall:        Attack at 10:05
```

The investigation becomes much easier.

---

# ⏱️ 4. What Is Clock Drift?

**Clock drift** means a computer’s clock slowly becomes inaccurate.

Example:

```text
Actual time:  12:00:00
Server time:  12:03:20
```

Clock drift can happen because computer hardware clocks are not perfectly accurate.

NTP continuously corrects this difference.

---

# 🏢 5. Enterprise Example

A company may have:

```text
Web Server
Database Server
Application Server
File Server
Authentication Server
Monitoring Server
```

All servers should synchronize with the same trusted time source.

Example:

```text
External NTP Servers
          ↓
Internal Company NTP Server
          ↓
All Company Servers
```

This provides consistent time throughout the organization.

---

# 🔄 6. NTP Client and Server Roles

## NTP Client

A machine requesting time from another server.

```text
Client → “What time is it?”
```

---

## NTP Server

A machine providing time to clients.

```text
Server → “The current time is 10:30:00.”
```

---

## Roles Can Change

A server can be:

* A client of an external NTP server
* An NTP server for internal machines

Example:

```text
Internet NTP Server
        ↓
Company Time Server
        ↓
Internal Linux Clients
```

The company server is:

* A client when communicating upward
* A server when providing time internally

---

# 🧱 7. NTP Hierarchy and Stratum

NTP servers are organized into levels called **strata**.

| Stratum       | Meaning                                 |
| ------------- | --------------------------------------- |
| Stratum 0     | Highly accurate reference clock         |
| Stratum 1     | Directly connected to a reference clock |
| Stratum 2     | Synchronizes from Stratum 1             |
| Stratum 3     | Synchronizes from Stratum 2             |
| Higher strata | Farther from the original clock         |

---

## Stratum 0 Examples

* Atomic clocks
* GPS clocks
* Radio clocks

These are reference devices and are not usually regular network servers.

---

## Stratum 1 Example

A server directly connected to a GPS clock.

```text
GPS Clock
    ↓
Stratum 1 Server
```

---

## Important Point

A lower stratum number generally means the source is closer to the original reference clock.

However, the lowest available stratum is not automatically the best source. Network delay, stability, and reliability also matter.

---

# 📦 8. Modern Linux Implementation

On modern Red Hat-based systems such as:

* CentOS Stream 9
* RHEL 8
* RHEL 9
* Fedora

NTP is implemented using the **chrony** suite.

The main components are:

| Component          | Purpose                        |
| ------------------ | ------------------------------ |
| `chrony`           | Package name                   |
| `chronyd`          | Background daemon              |
| `chronyc`          | Monitoring and control command |
| `/etc/chrony.conf` | Main configuration file        |

---

# 🕰️ 9. Older NTP Implementation

Older systems may use:

| Component       | Purpose                      |
| --------------- | ---------------------------- |
| `ntp`           | Package                      |
| `ntpd`          | NTP daemon                   |
| `ntpq`          | Query and monitoring command |
| `/etc/ntp.conf` | Configuration file           |

Examples include some older Linux environments.

For CentOS Stream 9, use:

```text
chrony
chronyd
chronyc
/etc/chrony.conf
```

---

# 🆚 10. Chrony vs Older NTP Tools

| Modern Chrony              | Older NTP               |
| -------------------------- | ----------------------- |
| Package: `chrony`          | Package: `ntp`          |
| Daemon: `chronyd`          | Daemon: `ntpd`          |
| Command: `chronyc`         | Command: `ntpq`         |
| Config: `/etc/chrony.conf` | Config: `/etc/ntp.conf` |

---

# ⭐ Top  Rule

For CentOS Stream 9:

* Do not search for `/etc/ntp.conf`
* Do not start `ntpd`
* Use `/etc/chrony.conf`
* Start `chronyd`
* Verify with `chronyc`

---

# 🔍 11. Check the Current Date and Time

`date`

Example:

```text
Thu Jul 16 23:10:30 +0545 2026
```

---

# 🌐 12. Check Time and Synchronization Status

`timedatectl`

Example output:

```text
Local time: Thu 2026-07-16 23:10:30 +0545
Universal time: Thu 2026-07-16 17:25:30 UTC
Time zone: Asia/Kathmandu
System clock synchronized: yes
NTP service: active
```

---

## Important Fields

| Field                     | Meaning                                          |
| ------------------------- | ------------------------------------------------ |
| Local time                | Time in the configured timezone                  |
| Universal time            | UTC time                                         |
| RTC time                  | Hardware clock time                              |
| Time zone                 | Current timezone                                 |
| System clock synchronized | Whether synchronization succeeded                |
| NTP service               | Whether a time synchronization service is active |

---

# 📦 13. Check Whether Chrony Is Installed

`rpm -qa | grep chrony`

Another method:

`dnf list installed chrony`

---

# 📥 14. Install Chrony

`dnf install chrony -y`

Meaning:

* `dnf install` installs the package
* `chrony` is the package name
* `-y` automatically confirms the installation

---

# ✅ 15. Verify Installation

`rpm -qa | grep chrony`

You should see a package similar to:

```text
chrony-version.el9.x86_64
```

---

# 💾 16. Back Up the Configuration

Before editing:

`cp /etc/chrony.conf /etc/chrony.conf.backup`

Verify:

`ls -l /etc/chrony.conf*`

---

# ⚙️ 17. Chrony Configuration File

The main file is:

`/etc/chrony.conf`

Open it:

`vi /etc/chrony.conf`

---

# 🌐 18. Configure NTP Sources

A time source may be defined with either:

* `server`
* `pool`

---

## Server Directive

Example:

```conf
server time-server.example.com iburst
```

This configures one specific NTP server.

---

## Pool Directive

Example:

```conf
pool pool.example.com iburst
```

A pool name may resolve to multiple NTP servers.

This improves:

* Reliability
* Availability
* Redundancy

---

# ⚡ 19. What Does `iburst` Mean?

Example:

```conf
server time-server.example.com iburst
```

The `iburst` option allows chrony to send several requests quickly when synchronization begins.

This helps the system synchronize faster after:

* Booting
* Restarting `chronyd`
* Reconnecting to the network

---

# ⚠️ 20. Do Not Use `8.8.8.8` as an NTP Server

`8.8.8.8` is a public DNS resolver.

It provides DNS services, not standard NTP service.

Incorrect:

```conf
server 8.8.8.8 iburst
```

Use an actual NTP server supplied by:

* Your company
* Your cloud provider
* Your Linux distribution
* A trusted NTP pool

---

# 🧠 21. DNS Server vs NTP Server

| DNS Server                   | NTP Server                          |
| ---------------------------- | ----------------------------------- |
| Resolves names               | Provides accurate time              |
| Usually uses port 53         | Usually uses UDP port 123           |
| Example function: name to IP | Example function: synchronize clock |
| Service: DNS                 | Service: NTP                        |

---

# 🌍 Real-World Analogy

DNS is like a contact list:

```text
Name → Phone number
```

NTP is like an official clock:

```text
Official source → Correct time
```

They solve completely different problems.

---

# ▶️ 22. Start Chrony

`systemctl start chronyd`

---

# 🔁 23. Enable Chrony at Boot

`systemctl enable chronyd`

This ensures time synchronization starts whenever the system boots.

---

# ⚡ 24. Start and Enable Together

`systemctl enable --now chronyd`

This command:

* Starts `chronyd` now
* Enables it for future boots

---

# 🔎 25. Check Chrony Status

`systemctl status chronyd`

Look for:

```text
Active: active (running)
```

---

# 🔄 26. Restart Chrony

After modifying `/etc/chrony.conf`:

`systemctl restart chronyd`

---

# ⏹️ 27. Stop Chrony

`systemctl stop chronyd`

Stopping the service prevents ongoing network time synchronization.

---

# 🚫 28. Disable Chrony at Boot

`systemctl disable chronyd`

This prevents automatic startup after reboot.

---

# 🧪 29. Check the Process

`ps -ef | grep chronyd`

A running daemon may appear as:

```text
/usr/sbin/chronyd
```

However, `systemctl status chronyd` is generally a better service check.

---

# ⚠️ 30. Avoid Killing the Process Directly

Do not normally stop chrony using:

`kill PID`

Use:

`systemctl stop chronyd`

Why?

`systemctl` manages the service cleanly and tracks its state.

Directly killing the process should be reserved for troubleshooting when normal service management fails.

---

# 🔍 31. Check Time Synchronization

`chronyc tracking`

This displays the current synchronization status.

---

## Important `tracking` Fields

| Field        | Meaning                                |
| ------------ | -------------------------------------- |
| Reference ID | Current time source                    |
| Stratum      | NTP hierarchy level                    |
| System time  | Difference between system and NTP time |
| Last offset  | Most recent clock correction           |
| RMS offset   | Long-term average offset               |
| Leap status  | Synchronization condition              |

---

## Healthy Result

Look for:

```text
Leap status : Normal
```

This generally indicates that the system has a valid time source.

---

# 🌐 32. View NTP Sources

`chronyc sources`

For more detail:

`chronyc sources -v`

---

## Example Source Output

```text
MS Name/IP address         Stratum Poll Reach LastRx Last sample
===============================================================================
^* time-server.example.com       2   6   377    20   +25us[ +30us] +/- 10ms
^+ backup-time.example.com       2   6   377    18   -15us[ -10us] +/- 15ms
```

---

# 🧠 33. Source Symbols

| Symbol | Meaning                          |
| ------ | -------------------------------- |
| `^`    | NTP server                       |
| `=`    | NTP peer                         |
| `#`    | Local reference clock            |
| `*`    | Current selected source          |
| `+`    | Acceptable combined source       |
| `-`    | Valid but not currently used     |
| `?`    | Unreachable or invalid source    |
| `x`    | Falseticker or inaccurate source |
| `~`    | Source has too much variability  |

---

## Most Important Symbol

```text
^*
```

The asterisk means this is the source currently selected for synchronization.

---

# 📶 34. Understanding Reach

The `Reach` field shows whether recent requests received replies.

A common healthy value is:

```text
377
```

This is an octal value showing that the most recent polling attempts succeeded.

If it remains:

```text
0
```

the source may be unreachable.

---

# 📊 35. View Source Statistics

`chronyc sourcestats -v`

This shows measurements related to:

* Clock offset
* Network delay
* Frequency estimation
* Source stability

---

# ⚡ 36. Force an Immediate Clock Step

Normally, chrony adjusts time gradually to avoid sudden jumps.

For a lab system with a large time difference:

`chronyc makestep`

This immediately corrects the system clock.

---

## Warning

Sudden time changes may affect:

* Databases
* Applications
* Logs
* Scheduled tasks

Use carefully on production systems.

---

# 🔄 37. Force Source Refresh

`chronyc burst 4/4`

This asks chrony to make several quick measurements.

It can help during troubleshooting.

---

# 🌍 38. Timezone vs Time Synchronization

These are different concepts.

## Time Synchronization

Ensures the clock is accurate.

Handled by:

* NTP
* Chrony

---

## Timezone

Controls how the time is displayed locally.

Examples:

* `Asia/Kathmandu`
* `America/Chicago`
* `UTC`

---

# 🗺️ 39. View Current Timezone

`timedatectl`

---

# 📋 40. List Timezones

`timedatectl list-timezones`

Search for Kathmandu:

`timedatectl list-timezones | grep Kathmandu`

---

# ⚙️ 41. Set Timezone

`timedatectl set-timezone Asia/Kathmandu`

Verify:

`timedatectl`

Changing the timezone does not change the actual moment in time. It changes how the time is displayed.

---

# 🌍 Real-World Example

At the same moment:

```text
Kathmandu → 10:45 PM
New York  → 1:00 PM
UTC       → 5:00 PM
```

The clocks display different local times, but they represent the same moment.

---

# 🔥 42. NTP Firewall Requirement

NTP normally uses:

```text
UDP port 123
```

A client needs to send requests to the NTP server on UDP port 123.

If this traffic is blocked, synchronization may fail.

---

## Allow NTP Service on an NTP Server

When configuring a machine to serve NTP to other clients:

`firewall-cmd --permanent --add-service=ntp`

Reload:

`firewall-cmd --reload`

Verify:

`firewall-cmd --list-services`

---

# 🏢 43. Configure an Internal Chrony Server

Suppose a company has this internal time server:

```text
192.168.1.10
```

The server receives time from external sources and provides it to internal clients.

---

## Server Configuration

Edit:

`vi /etc/chrony.conf`

Add an allowed client network:

```conf
allow 192.168.1.0/24
```

This permits machines from that subnet to request time.

Restart:

`systemctl restart chronyd`

Allow firewall service:

`firewall-cmd --permanent --add-service=ntp`

Reload firewall:

`firewall-cmd --reload`

---

## Client Configuration

On each client, edit:

`vi /etc/chrony.conf`

Add:

```conf
server 192.168.1.10 iburst
```

Restart:

`systemctl restart chronyd`

Verify:

`chronyc sources -v`

---

# 🧭 44. Complete Synchronization Workflow

```text
Reference Clock
       ↓
External NTP Server
       ↓
Company Chrony Server
       ↓
Internal Linux Clients
       ↓
Applications and Logs
```

---

# 🧪 45. Complete Lab Procedure

## Step 1: Check time

`date`

---

## Step 2: Check synchronization status

`timedatectl`

---

## Step 3: Check package

`rpm -qa | grep chrony`

---

## Step 4: Install package if needed

`dnf install chrony -y`

---

## Step 5: Back up configuration

`cp /etc/chrony.conf /etc/chrony.conf.backup`

---

## Step 6: Edit configuration

`vi /etc/chrony.conf`

---

## Step 7: Start and enable service

`systemctl enable --now chronyd`

---

## Step 8: Check service

`systemctl status chronyd`

---

## Step 9: Check selected sources

`chronyc sources -v`

---

## Step 10: Check synchronization details

`chronyc tracking`

---

## Step 11: Confirm system status

`timedatectl`

---

# 🚨 46. Common Problems

| Problem                                  | Possible Cause            | Solution                         |
| ---------------------------------------- | ------------------------- | -------------------------------- |
| `chronyd` not found                      | Chrony not installed      | Install `chrony`                 |
| Service inactive                         | Service stopped           | Start `chronyd`                  |
| Source shows `?`                         | Server unreachable        | Check network and source address |
| Reach stays at `0`                       | No NTP replies            | Check UDP port 123               |
| Wrong time source                        | Invalid server configured | Use a real NTP server            |
| Time still incorrect                     | Large clock difference    | Use `chronyc makestep` carefully |
| Hostname source fails                    | DNS problem               | Test DNS resolution              |
| Service works but local time looks wrong | Incorrect timezone        | Set timezone with `timedatectl`  |

---

# 🧰 47. Troubleshooting Checklist

Check current time:

`date`

Check timezone and synchronization:

`timedatectl`

Check service:

`systemctl status chronyd`

Check process:

`ps -ef | grep chronyd`

Check sources:

`chronyc sources -v`

Check tracking:

`chronyc tracking`

Check source statistics:

`chronyc sourcestats -v`

Check logs:

`journalctl -u chronyd`

Check DNS:

`getent hosts time-server.example.com`

Check network:

`ping -c 4 time-server.example.com`

---

# ⚠️ 48. Ping Does Not Test NTP Directly

`ping` tests ICMP network reachability.

It does not confirm that NTP is working.

A server may:

* Respond to ping but block UDP port 123
* Ignore ping but still provide NTP service

Use:

`chronyc sources -v`

to verify actual time-source communication.

---

# 🧠 49. Memory Tricks

Remember:

```text
NTP      = Protocol
chrony   = Package
chronyd  = Daemon
chronyc  = Control command
```

Easy formula:

> **Install → Configure → Start → Check Sources → Check Tracking**

---

# 📋 50. Command Cheat Sheet

| Task                 | Command                                   |
| -------------------- | ----------------------------------------- |
| Show current time    | `date`                                    |
| Show time settings   | `timedatectl`                             |
| Check chrony package | `rpm -qa \| grep chrony`                  |
| Install chrony       | `dnf install chrony -y`                   |
| Edit configuration   | `vi /etc/chrony.conf`                     |
| Start chrony         | `systemctl start chronyd`                 |
| Enable chrony        | `systemctl enable chronyd`                |
| Start and enable     | `systemctl enable --now chronyd`          |
| Restart chrony       | `systemctl restart chronyd`               |
| Check status         | `systemctl status chronyd`                |
| View sources         | `chronyc sources -v`                      |
| View tracking        | `chronyc tracking`                        |
| View statistics      | `chronyc sourcestats -v`                  |
| Step clock           | `chronyc makestep`                        |
| Check logs           | `journalctl -u chronyd`                   |
| Set timezone         | `timedatectl set-timezone Asia/Kathmandu` |

---

# 💼 51. Questions

## Q1. What is NTP?

NTP is a network protocol used to synchronize computer clocks.

---

## Q2. Why is time synchronization important?

It keeps logs, transactions, authentication systems, clusters, and scheduled operations consistent.

---

## Q3. What port does NTP use?

NTP normally uses UDP port `123`.

---

## Q4. What package implements NTP on RHEL 9?

`chrony`

---

## Q5. What is `chronyd`?

It is the background daemon that synchronizes the system clock.

---

## Q6. What is `chronyc`?

It is the command-line interface used to monitor and control `chronyd`.

---

## Q7. Where is the Chrony configuration file?

`/etc/chrony.conf`

---

## Q8. How do you check Chrony sources?

`chronyc sources -v`

---

## Q9. How do you check synchronization details?

`chronyc tracking`

---

## Q10. What does the asterisk mean in `chronyc sources`?

It identifies the currently selected synchronization source.

---

## Q11. What is clock drift?

It is the gradual difference between a computer’s clock and the correct time.

---

## Q12. What does `iburst` do?

It speeds up initial synchronization by sending several requests quickly.

---

## Q13. What is a stratum?

It represents a time source’s distance from the original reference clock.

---

## Q14. Is `8.8.8.8` an NTP server?

No. It is primarily a public DNS resolver.

---

## Q15. What is the difference between timezone and NTP?

NTP keeps the clock accurate, while the timezone controls how that time is displayed locally.

---

# 📌 52. Ultra-Short Revision

* NTP = Network Time Protocol
* Purpose = Synchronize clocks
* Port = UDP `123`
* Modern package = `chrony`
* Daemon = `chronyd`
* Command = `chronyc`
* Configuration = `/etc/chrony.conf`
* Start = `systemctl start chronyd`
* Enable = `systemctl enable chronyd`
* Sources = `chronyc sources -v`
* Status details = `chronyc tracking`
* Time settings = `timedatectl`
* Timezone and synchronization are different
* `8.8.8.8` is DNS, not an NTP time source

---

# 🏆 53. Takeaway

A beginner knows that NTP corrects the computer clock.

A strong Linux administrator understands:

* Why synchronized time is critical
* How clock drift affects systems
* The difference between NTP and Chrony
* How `chronyd` selects time sources
* How to interpret `chronyc sources`
* How to configure an internal NTP server
* How timezone differs from clock synchronization
* How to troubleshoot source and network problems

Accurate time is essential for reliable logging, authentication, databases, cybersecurity investigations, and distributed systems.

---

# ✍️ Notes By Abhishek (Ez Abyss)
