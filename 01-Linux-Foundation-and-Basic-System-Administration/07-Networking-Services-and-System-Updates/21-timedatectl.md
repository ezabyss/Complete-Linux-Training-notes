# 🕒 `timedatectl` — Date, Time, Timezone and NTP Management

---

## 🎯 1. What Is `timedatectl`?

`timedatectl` is a `systemd` command-line utility used to view and manage:

* System date
* System time
* Timezone
* Hardware clock configuration
* Network time synchronization status

> **Simple definition:** `timedatectl` is the modern control panel for Linux system-time settings.

---

## 🌍 2. Real-World Example

Think of the Date and Time settings on a smartphone.

You can:

* View the current time
* Choose a timezone
* Set the time manually
* Enable automatic time
* Synchronize with a network time source

`timedatectl` provides similar controls from the Linux command line.

---

# 🧠 3. Important Correction: `timedatectl` Does Not Replace `date`

Both commands remain useful.

## `date`

Best used for:

* Displaying the current date and time
* Formatting date output
* Generating timestamps
* Date calculations
* Shell scripts
* Setting time manually in some environments

Check time:

`date`

Custom format:

`date "+%Y-%m-%d %H:%M:%S"`

Example output:

```text
2026-07-24 14:30:00
```

---

## `timedatectl`

Best used for:

* Viewing detailed clock status
* Changing the timezone
* Setting system time
* Managing network-time synchronization
* Checking hardware-clock configuration

Check status:

`timedatectl`

> **Memory rule:** Use `date` for displaying and formatting time. Use `timedatectl` for system-time configuration.

---

# ⚙️ 4. How `timedatectl` Works

`timedatectl` communicates with the `systemd-timedated` service.

It manages settings related to:

* System clock
* Timezone
* Hardware clock
* NTP synchronization control

However, `timedatectl` is not an NTP client.

The actual clock synchronization is performed by a time service such as:

* `chronyd`
* `systemd-timesyncd`
* Older `ntpd`

---

# 🕰️ 5. Time Synchronization on RHEL and CentOS Stream

Modern Red Hat-based systems normally use Chrony.

This includes:

* RHEL 8
* RHEL 9
* RHEL 10
* CentOS Stream 8
* CentOS Stream 9
* CentOS Stream 10

Important Chrony components:

| Component          | Purpose                        |
| ------------------ | ------------------------------ |
| `chrony`           | Package name                   |
| `chronyd`          | Time-synchronization daemon    |
| `chronyc`          | Monitoring and control command |
| `/etc/chrony.conf` | Main configuration file        |

---

## Older NTP Components

Older systems may use:

| Component       | Purpose            |
| --------------- | ------------------ |
| `ntp`           | Package            |
| `ntpd`          | NTP daemon         |
| `ntpq`          | Monitoring command |
| `/etc/ntp.conf` | Configuration file |

For modern RHEL and CentOS Stream, use Chrony unless your environment specifically requires something else.

---

# 🆚 6. `chronyd` vs `systemd-timesyncd`

| Feature                               | `chronyd`          | `systemd-timesyncd`           |
| ------------------------------------- | ------------------ | ----------------------------- |
| Full NTP implementation               | ✅ Yes              | Limited client                |
| NTP server capability                 | ✅ Yes              | ❌ No                          |
| Works well with intermittent networks | ✅ Yes              | Basic support                 |
| Hardware reference clocks             | ✅ Yes              | ❌ No                          |
| Advanced monitoring                   | ✅ Yes              | Limited                       |
| Standard on RHEL                      | ✅ Yes              | Usually not standard          |
| Configuration                         | `/etc/chrony.conf` | `/etc/systemd/timesyncd.conf` |

> **Top 1% rule:** On RHEL and CentOS Stream, learn `chronyd` and `chronyc`.

---

# 🔍 7. Check Current Time Status

`timedatectl`

The following command gives the same standard status:

`timedatectl status`

Example:

```text
Local time: Fri 2026-07-24 14:30:00 +0545
Universal time: Fri 2026-07-24 08:45:00 UTC
RTC time: Fri 2026-07-24 08:45:00
Time zone: Asia/Kathmandu (+0545, +0545)
System clock synchronized: yes
NTP service: active
RTC in local TZ: no
```

---

# 🧩 8. Understanding the Output

## Local Time

```text
Local time: Fri 2026-07-24 14:30:00 +0545
```

This is the time displayed using the configured timezone.

---

## Universal Time

```text
Universal time: Fri 2026-07-24 08:45:00 UTC
```

UTC is the global reference time.

---

## RTC Time

```text
RTC time: Fri 2026-07-24 08:45:00
```

RTC means **Real-Time Clock**.

It is the hardware clock on the computer’s motherboard.

---

## Time Zone

```text
Time zone: Asia/Kathmandu
```

This controls how system time is displayed locally.

---

## System Clock Synchronized

```text
System clock synchronized: yes
```

This means the clock has successfully synchronized with a valid time source.

---

## NTP Service

```text
NTP service: active
```

A supported network-time service is enabled or running.

This does not automatically prove that synchronization succeeded.

---

## RTC in Local TZ

```text
RTC in local TZ: no
```

This means the hardware clock is stored in UTC.

That is normally recommended for Linux.

---

# ⚠️ 9. Active Is Not the Same as Synchronized

These two lines mean different things:

```text
NTP service: active
System clock synchronized: yes
```

## `NTP service: active`

A recognized time service is enabled or running.

## `System clock synchronized: yes`

The system has successfully synchronized with a valid source.

A system can temporarily show:

```text
NTP service: active
System clock synchronized: no
```

Possible reasons:

* The service has only just started
* The network is unavailable
* DNS resolution is failing
* No valid NTP server is reachable
* UDP port 123 is blocked
* The NTP source is incorrectly configured

---

# 🌍 10. Local Time, UTC and Timezone

The actual moment in time is the same worldwide.

Only the local display changes.

Example:

```text
UTC:             08:45
Asia/Kathmandu:  14:30
America/New_York: 04:45
```

Changing the timezone does not change the actual moment.

---

# 📋 11. List Available Timezones

`timedatectl list-timezones`

Use `q` to exit the long list.

Search for Kathmandu:

`timedatectl list-timezones | grep Kathmandu`

Search for New York:

`timedatectl list-timezones | grep New_York`

---

# 🌎 12. Set the Timezone

Set Nepal timezone:

`timedatectl set-timezone Asia/Kathmandu`

Set New York timezone:

`timedatectl set-timezone America/New_York`

Verify:

`timedatectl`

Use the exact timezone spelling shown by:

`timedatectl list-timezones`

---

# 🗓️ 13. Set the Date Manually

Disable automatic synchronization first:

`timedatectl set-ntp false`

Set the date:

`timedatectl set-time "2026-07-24"`

Verify:

`timedatectl`

---

# ⏰ 14. Set the Time Manually

Disable NTP first:

`timedatectl set-ntp false`

Set time:

`timedatectl set-time "14:30:00"`

---

# 📅 15. Set Date and Time Together

`timedatectl set-time "2026-07-24 14:30:00"`

Format:

```text
YYYY-MM-DD HH:MM:SS
```

Examples:

| Time     | 24-hour format |
| -------- | -------------- |
| 1:00 AM  | `01:00:00`     |
| 1:00 PM  | `13:00:00`     |
| 6:30 PM  | `18:30:00`     |
| 11:45 PM | `23:45:00`     |

---

# ⚠️ 16. Why Disable NTP Before Manual Changes?

When automatic synchronization is enabled, the time service may correct and overwrite your manually entered time.

Safe lab sequence:

`timedatectl set-ntp false`

`timedatectl set-time "2026-07-24 14:30:00"`

`timedatectl set-ntp true`

In production, manual time changes should be made carefully because sudden clock changes can affect applications, databases, logs and scheduled jobs.

---

# 🌐 17. Enable Network-Time Synchronization

`timedatectl set-ntp true`

This requests that `systemd` enable and start an available supported network-time service.

Important:

* It does not install Chrony
* It does not choose your time servers
* It does not edit `/etc/chrony.conf`
* It does not guarantee immediate synchronization

Verify:

`timedatectl`

---

# 🚫 18. Disable Network-Time Synchronization

`timedatectl set-ntp false`

Verify:

`timedatectl`

This may disable or stop the supported time synchronization service selected by `systemd`.

For explicit service control on RHEL, use `systemctl` with `chronyd`.

---

# 📦 19. Install Chrony

Check whether it is installed:

`rpm -qa | grep chrony`

Install it:

`dnf install chrony -y`

---

# ▶️ 20. Start and Enable Chrony

Start now:

`systemctl start chronyd`

Enable at boot:

`systemctl enable chronyd`

Start and enable together:

`systemctl enable --now chronyd`

Check status:

`systemctl status chronyd`

---

# 🔄 21. Restart Chrony

After changing `/etc/chrony.conf`:

`systemctl restart chronyd`

A reload may also be available for supported changes:

`systemctl reload chronyd`

---

# 🔎 22. Check Actual Synchronization

General system status:

`timedatectl`

Detailed Chrony tracking:

`chronyc tracking`

View time sources:

`chronyc sources -v`

View source statistics:

`chronyc sourcestats -v`

---

# 📊 23. Understand `chronyc tracking`

`chronyc tracking`

Important fields:

| Field        | Meaning                            |
| ------------ | ---------------------------------- |
| Reference ID | Current reference source           |
| Stratum      | Distance from the reference clock  |
| System time  | Current clock difference           |
| Last offset  | Most recent correction             |
| RMS offset   | Long-term average clock difference |
| Frequency    | Estimated clock drift              |
| Leap status  | Synchronization condition          |

A healthy result normally shows:

```text
Leap status : Normal
```

---

# 🌐 24. Understand `chronyc sources -v`

`chronyc sources -v`

Important symbols:

| Symbol | Meaning                             |
| ------ | ----------------------------------- |
| `^*`   | Selected NTP source                 |
| `^+`   | Acceptable additional source        |
| `^-`   | Valid source not currently selected |
| `^?`   | Unreachable or insufficient data    |
| `^x`   | Source considered inaccurate        |
| `^~`   | Source has excessive variability    |

The most important symbol is:

```text
^*
```

It identifies the source currently selected for synchronization.

---

# ⚡ 25. Force a Time Correction

Chrony normally corrects time gradually.

For a large clock error in a controlled lab:

`chronyc makestep`

Use this carefully in production because a sudden time jump can affect:

* Databases
* Authentication
* Log ordering
* Scheduled tasks
* Distributed applications

---

# 🔄 26. System Clock vs Hardware Clock

Linux maintains two clocks.

## System Clock

Used by the operating system while it is running.

Check:

`date`

or:

`timedatectl`

---

## Hardware Clock

Stored in the motherboard’s RTC.

Check:

`hwclock --show`

It continues running when the machine is powered off.

---

# 🔁 27. Copy System Time to Hardware Clock

`hwclock --systohc`

Meaning:

```text
System clock → Hardware clock
```

---

# 🔁 28. Copy Hardware Clock to System Clock

`hwclock --hctosys`

Meaning:

```text
Hardware clock → System clock
```

Use carefully because it changes the running system clock.

---

# ⚙️ 29. Keep the Hardware Clock in UTC

Recommended:

`timedatectl set-local-rtc 0`

Verify:

`timedatectl`

Expected:

```text
RTC in local TZ: no
```

---

## Avoid Local RTC Unless Required

`timedatectl set-local-rtc 1`

Using local time in the hardware clock may cause problems with:

* Daylight-saving changes
* Timezone changes
* Dual-boot configurations
* Clock interpretation during startup

---

# 🔍 30. Show Individual Properties

Display all machine-readable properties:

`timedatectl show`

Show timezone:

`timedatectl show -p Timezone`

Show only its value:

`timedatectl show -p Timezone --value`

Check NTP setting:

`timedatectl show -p NTP`

Check synchronization:

`timedatectl show -p NTPSynchronized`

These commands are useful in scripts.

---

# 🔐 31. Administrative Permissions

A normal user can usually view time settings:

`timedatectl`

Changing them normally requires root or administrative permission:

`sudo timedatectl set-timezone Asia/Kathmandu`

`sudo timedatectl set-ntp true`

---

# 🔒 32. Modern Time Security: NTS

**NTS** stands for **Network Time Security**.

It adds authentication and integrity protection to NTP communication.

It helps verify that:

* The time server is authentic
* NTP messages were not altered in transit
* Attackers cannot easily provide false time information

A Chrony source may be configured with NTS support when the selected server supports it.

Example structure:

```conf
server time.example.com iburst nts
```

Do not add `nts` blindly. Confirm that the selected time provider supports NTS.

---

# 🏢 33. Enterprise Automation

Managing time manually on hundreds of servers is inefficient.

Modern RHEL environments can use the RHEL `timesync` System Role to manage time synchronization consistently across multiple machines.

Typical enterprise workflow:

```text
Automation Controller
        ↓
RHEL timesync System Role
        ↓
Configure chrony on many servers
        ↓
Verify consistent time sources
```

This reduces configuration drift and human error.

---

# 🎯 34. Precision Time Protocol

NTP is sufficient for most servers.

Some environments require much higher accuracy, such as:

* Telecommunications
* Financial trading
* Industrial control
* Scientific systems
* Network measurement

These environments may use **PTP**, the Precision Time Protocol.

PTP can use hardware timestamping from supported network cards to achieve much higher accuracy than normal software-based NTP.

For standard system administration, Chrony with NTP remains the usual choice.

---

# 🚨 35. Common Problems

| Problem                             | Possible Cause                       | Solution                          |
| ----------------------------------- | ------------------------------------ | --------------------------------- |
| `NTP service: inactive`             | Chrony stopped or missing            | Install and start `chronyd`       |
| Clock not synchronized              | No valid source                      | Run `chronyc sources -v`          |
| Wrong local time                    | Incorrect timezone                   | Set the correct timezone          |
| Manual time changes back            | NTP enabled                          | Disable NTP before manual setting |
| `chronyd` not found                 | Chrony not installed                 | Install `chrony`                  |
| Invalid timezone                    | Incorrect spelling                   | Use `list-timezones`              |
| Source shows `?`                    | Network or source issue              | Check network, DNS and NTP source |
| Service active but not synchronized | Source unavailable or still starting | Check `chronyc tracking`          |
| Large clock error                   | System clock far from source         | Use `chronyc makestep` carefully  |
| Time differs after reboot           | RTC configuration issue              | Check `timedatectl` and `hwclock` |

---

# 🧰 36. Troubleshooting Workflow

## Step 1: Check general status

`timedatectl`

---

## Step 2: Check Chrony service

`systemctl status chronyd`

---

## Step 3: Check selected sources

`chronyc sources -v`

---

## Step 4: Check detailed tracking

`chronyc tracking`

---

## Step 5: Check service logs

`journalctl -u chronyd`

---

## Step 6: Check configuration

`cat /etc/chrony.conf`

---

## Step 7: Check network

`ip a`

`ip route`

---

## Step 8: Check DNS resolution

`getent hosts time-server.example.com`

---

## Step 9: Restart after configuration changes

`systemctl restart chronyd`

---

## Step 10: Verify again

`timedatectl`

`chronyc sources -v`

`chronyc tracking`

---

# ⚠️ 37. Ping Does Not Verify NTP

`ping` checks ICMP network reachability.

It does not prove that NTP is working.

A server may:

* Respond to ping but block NTP
* Ignore ping but still provide NTP
* Resolve through DNS but not provide a valid time service

Use these commands to verify synchronization:

`chronyc sources -v`

`chronyc tracking`

---

# 🧪 38. Complete Lab Procedure

## Step 1: Check system time

`date`

---

## Step 2: Check full time status

`timedatectl`

---

## Step 3: Check installed Chrony package

`rpm -qa | grep chrony`

---

## Step 4: Install Chrony if required

`dnf install chrony -y`

---

## Step 5: Start and enable Chrony

`systemctl enable --now chronyd`

---

## Step 6: Enable network time

`timedatectl set-ntp true`

---

## Step 7: Check service

`systemctl status chronyd`

---

## Step 8: Check time sources

`chronyc sources -v`

---

## Step 9: Check synchronization details

`chronyc tracking`

---

## Step 10: Confirm final system status

`timedatectl`

---

# 🧠 39. Memory Framework

Remember:

```text
timedatectl = Configure system-time settings
chronyd     = Synchronize the system clock
chronyc     = Monitor and control Chrony
date        = Display and format time
hwclock     = Manage the hardware clock
```

Easy workflow:

> **Check → Configure timezone → Start Chrony → Enable NTP → Verify sources**

---

# 📋 40. Command Cheat Sheet

| Task                     | Command                                        |
| ------------------------ | ---------------------------------------------- |
| Show current date        | `date`                                         |
| Show detailed status     | `timedatectl`                                  |
| List timezones           | `timedatectl list-timezones`                   |
| Search timezone          | `timedatectl list-timezones \| grep Kathmandu` |
| Set timezone             | `timedatectl set-timezone Asia/Kathmandu`      |
| Disable network time     | `timedatectl set-ntp false`                    |
| Enable network time      | `timedatectl set-ntp true`                     |
| Set date                 | `timedatectl set-time "2026-07-24"`            |
| Set time                 | `timedatectl set-time "14:30:00"`              |
| Set date and time        | `timedatectl set-time "2026-07-24 14:30:00"`   |
| Install Chrony           | `dnf install chrony -y`                        |
| Start Chrony             | `systemctl start chronyd`                      |
| Enable Chrony            | `systemctl enable chronyd`                     |
| Start and enable         | `systemctl enable --now chronyd`               |
| Restart Chrony           | `systemctl restart chronyd`                    |
| Check Chrony             | `systemctl status chronyd`                     |
| Check sources            | `chronyc sources -v`                           |
| Check tracking           | `chronyc tracking`                             |
| Force clock step         | `chronyc makestep`                             |
| Check logs               | `journalctl -u chronyd`                        |
| Show hardware clock      | `hwclock --show`                               |
| System to hardware clock | `hwclock --systohc`                            |
| Configure RTC as UTC     | `timedatectl set-local-rtc 0`                  |
| Show timezone value      | `timedatectl show -p Timezone --value`         |

---

# 💼 41. Questions

## Q1. What is `timedatectl`?

It is a `systemd` utility used to view and manage system time, date, timezone, hardware-clock and NTP settings.

---

## Q2. Has `timedatectl` completely replaced `date`?

No. `date` remains useful for displaying, formatting and scripting, while `timedatectl` manages system-time settings.

---

## Q3. Is `timedatectl` an NTP daemon?

No. It controls settings and works with a synchronization service such as `chronyd`.

---

## Q4. Which NTP implementation is standard on modern RHEL?

Chrony.

---

## Q5. What does `timedatectl set-ntp true` do?

It requests that the system enable and start an available supported network-time service.

---

## Q6. Does `set-ntp true` install Chrony?

No. The synchronization service must already be installed.

---

## Q7. What is the difference between active and synchronized?

Active means the service is running. Synchronized means the system has successfully obtained accurate time from a valid source.

---

## Q8. Which command shows Chrony’s selected time source?

`chronyc sources -v`

---

## Q9. Which command displays detailed clock tracking?

`chronyc tracking`

---

## Q10. What is RTC?

RTC is the hardware real-time clock on the motherboard.

---

## Q11. Should the hardware clock use UTC?

Yes, that is normally recommended for Linux.

---

## Q12. What is NTS?

Network Time Security authenticates NTP communication and helps protect it from modification.

---

## Q13. What is PTP?

Precision Time Protocol is used for environments requiring greater clock accuracy than normal NTP.

---

## Q14. How can RHEL time synchronization be automated across many servers?

By using tools such as the RHEL `timesync` System Role.

---

# 📌 42. Ultra-Short Revision

* `timedatectl` manages system-time settings
* It is part of `systemd`
* It has not completely replaced `date`
* `timedatectl` is not an NTP daemon
* RHEL 8, 9 and 10 use Chrony
* Package = `chrony`
* Daemon = `chronyd`
* Control command = `chronyc`
* Configuration = `/etc/chrony.conf`
* Show status = `timedatectl`
* Set timezone = `timedatectl set-timezone Asia/Kathmandu`
* Enable NTP = `timedatectl set-ntp true`
* Check source = `chronyc sources -v`
* Check synchronization = `chronyc tracking`
* Hardware clock should normally use UTC
* Active service does not automatically mean synchronized
* NTS adds security to NTP
* PTP provides higher precision for specialized environments

---

# 🏆 43. Takeaway

A beginner uses `date` to check the clock.

A strong Linux administrator understands:

* The difference between `date` and `timedatectl`
* How `systemd-timedated` manages time settings
* Why `chronyd` performs the actual synchronization
* The difference between an active service and a synchronized clock
* Local time, UTC and hardware-clock relationships
* How to verify sources using `chronyc`
* Why sudden clock changes can damage application consistency
* How NTS protects time communication
* When high-precision environments require PTP
* How enterprise systems automate time configuration

Correct time is essential for authentication, certificates, databases, logs, backups, automation and cybersecurity investigations.

---

# ✍️ Notes By Abhishek (Ez Abyss)
