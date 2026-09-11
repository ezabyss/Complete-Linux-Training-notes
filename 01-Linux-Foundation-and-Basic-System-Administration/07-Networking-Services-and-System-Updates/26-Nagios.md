# 📡 Nagios Core Monitoring

---

## 🎯 1. What Is Nagios?

**Nagios** is an infrastructure monitoring platform used to watch servers, network devices, applications, and services.

Nagios can:

* Check whether hosts are reachable
* Monitor services such as HTTP, DNS, SSH, SMTP, and databases
* Monitor CPU, disk, memory, processes, and other metrics through plugins or agents
* Detect failures
* Send notifications
* Track when problems recover
* Schedule maintenance downtime
* Display status through a web interface
* Keep monitoring history and logs
* Escalate notifications when required

> **Simple understanding:** Nagios is a digital operations watchtower. It continuously checks important systems and tells administrators when something stops working.

---

# 🌍 2. Real-World Example

Suppose a company operates:

* 50 Linux servers
* 20 Windows servers
* 10 switches
* 4 firewalls
* 3 database servers
* Several websites

Without monitoring:

```text
Server fails
     ↓
Users notice
     ↓
Help desk receives complaints
     ↓
Administrator investigates
```

With Nagios:

```text
Server fails
     ↓
Nagios detects failure
     ↓
Nagios retries the check
     ↓
Failure becomes a HARD state
     ↓
Notification is sent
     ↓
Administrator investigates
     ↓
Server recovers
     ↓
Nagios detects recovery
     ↓
Recovery notification is sent
```

Nagios helps the administrator learn about the problem **before users have to report it**.

---

# 🧠 3. Why Monitoring Matters

Monitoring helps organizations with:

* Availability
* Faster troubleshooting
* Failure detection
* Performance visibility
* Capacity planning
* Security awareness
* SLA monitoring
* Incident response
* Trend analysis
* Maintenance planning
* Reducing downtime
* Proactive administration

Example questions a monitoring system can answer:

```text
Is the server reachable?
Is the website responding?
Is disk space running low?
Is DNS resolving?
Is SSH listening?
Did a service recover?
How long has a host been down?
When was the last successful check?
```

---

# 🏗️ 4. Main Parts of a Nagios Environment

| Component | Purpose |
| --- | --- |
| Nagios Core | Monitoring engine and scheduler |
| Plugins | Perform the actual checks |
| Configuration files | Define hosts, services, contacts, commands, and schedules |
| Web interface | Displays status and allows selected commands |
| Apache HTTP Server | Serves the Nagios Core web interface in common source installs |
| Authentication file | Controls access to the web interface |
| Notification commands | Send alerts through email or integrations |
| Agents | Collect remote system metrics |
| Log files | Record events, states, alerts, and actions |

---

## Easy Analogy

| Nagios component | Security-center analogy |
| --- | --- |
| Nagios Core | Control-room supervisor |
| Plugin | Guard sent to inspect something |
| Host definition | Building being watched |
| Service definition | Specific item inside the building |
| Check interval | Patrol schedule |
| Contact | Person who gets called |
| Notification | Alarm |
| Web interface | Security dashboard |
| Event log | Incident notebook |

---

# 📦 5. Nagios Core vs Nagios XI

These are not the same product.

| Nagios Core | Nagios XI |
| --- | --- |
| Open-source monitoring engine | Commercial enterprise monitoring product |
| Configuration mainly through text files | Includes web-based configuration and enterprise features |
| Free to use under its license | Commercial licensing |
| Foundation of many Nagios-based deployments | Includes Nagios Core plus additional components |
| Best for learning monitoring fundamentals | Designed for easier enterprise administration |

Nagios Core is an excellent platform for learning:

* Monitoring concepts
* Host and service checks
* Plugins
* Notifications
* Configuration files
* State logic
* Troubleshooting

---

# 📜 6. Nagios History

Nagios began before the name “Nagios” existed.

Important milestones:

* **1996:** Ethan Galstad created an early MS-DOS monitoring application
* **1998:** He began developing a Linux monitoring application
* **1999:** The project was released as open source under the name **NetSaint**
* **2002:** NetSaint was renamed **Nagios** because of trademark concerns
* **2007:** Nagios Enterprises was founded to provide commercial services and development
* Nagios Core remains an open-source monitoring project

The name Nagios was historically described as a recursive acronym:

```text
Nagios Ain't Gonna Insist On Sainthood
```

---

# 🆕 7. Current Version Context — Updated 2026

As of September 2026:

```text
Nagios Core: 4.5.14
```

Nagios Core 4.5.14 was released on August 5, 2026 and included security and stability fixes.

The commercial **Nagios XI** product uses a different release naming scheme such as:

```text
Nagios XI 2026R1.x
```

Therefore, do not confuse:

```text
Nagios Core 4.x
```

with:

```text
Nagios XI
```

---

# ⚙️ 8. How Nagios Works

Simplified workflow:

```text
Nagios Core
     ↓
Schedules a check
     ↓
Executes a plugin
     ↓
Plugin tests host/service
     ↓
Plugin returns state + message
     ↓
Nagios processes result
     ↓
State is recorded
     ↓
Notification may be sent
     ↓
Web interface displays result
```

Nagios Core itself does not contain every possible monitoring test.

Plugins perform most checks.

---

# 🔌 9. What Is a Nagios Plugin?

A **plugin** is a program or script that checks something and returns a result to Nagios.

Examples:

```text
check_ping
check_http
check_dns
check_ssh
check_smtp
check_disk
check_load
check_users
check_procs
```

Common source-install plugin directory:

```text
/usr/local/nagios/libexec/
```

List installed plugins:

`ls -l /usr/local/nagios/libexec/`

---

# 🚦 10. Nagios Plugin Exit Codes

Plugins communicate status through exit codes.

| Exit code | State | Meaning |
| ---: | --- | --- |
| `0` | OK | Everything is healthy |
| `1` | WARNING | Something needs attention |
| `2` | CRITICAL | Serious failure |
| `3` | UNKNOWN | Check could not determine status |

This is one of the most important Nagios interview concepts.

Memory:

```text
0 = OK
1 = WARNING
2 = CRITICAL
3 = UNKNOWN
```

---

# 🧪 11. Plugin Output Example

Run:

`/usr/local/nagios/libexec/check_ping -H 192.168.1.162 -w 100.0,20% -c 500.0,60%`

Possible output:

```text
PING OK - Packet loss = 0%, RTA = 1.21 ms
```

Check the exit status:

`echo $?`

If healthy:

```text
0
```

Nagios reads both:

* Exit code
* Text output

---

# 🖥️ 12. What Is a Host?

A **host** is a device or system Nagios monitors.

Examples:

* Linux server
* Windows server
* Router
* Switch
* Firewall
* Printer
* Hypervisor
* Database server
* Virtual machine

Example host:

```text
Hostname: centos-server
IP:       192.168.1.162
```

---

# 🧩 13. What Is a Service?

A **service** is something monitored on a host.

Examples:

```text
PING
HTTP
SSH
DNS
CPU Load
Disk Space
Memory
Processes
SMTP
Database
Certificate Expiration
```

A host can be reachable while one of its services is failing.

Example:

```text
Host: web01
PING: OK
SSH: OK
HTTP: CRITICAL
```

The machine is alive, but the website is unavailable.

---

# 🆚 14. Host Monitoring vs Service Monitoring

| Host check | Service check |
| --- | --- |
| Is the device reachable? | Is a specific function healthy? |
| Often uses ping | May use HTTP, DNS, SSH, disk, etc. |
| States: UP/DOWN/UNREACHABLE | States: OK/WARNING/CRITICAL/UNKNOWN |
| Helps determine network reachability | Helps identify application/service failure |

---

# 🟢 15. Host States

Nagios host states include:

```text
UP
DOWN
UNREACHABLE
```

## UP

The host responds successfully.

## DOWN

The host fails its host check and Nagios determines it is down.

## UNREACHABLE

The host cannot be reached because of a failed parent/network path.

Parent relationships are useful for understanding topology.

---

# 🚥 16. Service States

Nagios service states:

```text
OK
WARNING
CRITICAL
UNKNOWN
```

Example:

```text
Disk 45% used  → OK
Disk 82% used  → WARNING
Disk 96% used  → CRITICAL
Plugin failed  → UNKNOWN
```

Thresholds are administrator-defined.

---

# 🧠 17. SOFT and HARD States

Nagios does not normally notify immediately after every single failed check.

A failure first enters a **SOFT** state while Nagios retries.

Example:

```text
Check 1 fails → SOFT CRITICAL 1/3
Check 2 fails → SOFT CRITICAL 2/3
Check 3 fails → HARD CRITICAL
                         ↓
                  Notification possible
```

If the service recovers during retries:

```text
SOFT failure
     ↓
Next check succeeds
     ↓
No HARD problem state
```

This prevents alerts from every tiny temporary network glitch.

---

# 🔁 18. Check Attempts

Important parameters include:

```text
max_check_attempts
check_interval
retry_interval
```

Example:

```nagios
max_check_attempts  5
check_interval      5
retry_interval      1
```

Meaning:

* Normal checks occur every 5 time units
* If a problem occurs, Nagios retries more frequently
* After enough failed attempts, the state becomes HARD

---

# ⏰ 19. Time Periods

Nagios can control when checks and notifications occur.

Common sample time period:

```text
24x7
```

Example:

```nagios
check_period          24x7
notification_period   24x7
```

Organizations may also create:

```text
workhours
weekends
maintenance
night-shift
```

---

# 📣 20. Notifications

Nagios can send notifications when:

* A problem becomes HARD
* A service or host recovers
* Scheduled escalation conditions are met
* Other configured state events occur

Common notification methods include:

* Email
* SMS through an external provider
* Chat integrations
* Pager systems
* Webhooks
* Ticketing integrations
* Custom scripts

Nagios Core does **not** magically make a phone call by itself.

Phone calls and SMS normally require an external integration or custom command.

---

# ⬆️ 21. Notification Escalation

Escalation can notify different people if a problem continues.

Example:

```text
0 minutes   → Linux administrator
15 minutes  → Senior administrator
30 minutes  → Operations manager
60 minutes  → Incident team
```

This prevents long-running incidents from remaining unnoticed.

---

# 🗒️ 22. Logs and Historical Information

Common source-install log:

```text
/usr/local/nagios/var/nagios.log
```

Archive directory:

```text
/usr/local/nagios/var/archives/
```

Follow the main log:

`tail -f /usr/local/nagios/var/nagios.log`

Nagios logs can show:

* State changes
* Notifications
* Service alerts
* Host alerts
* External commands
* Startup events
* Shutdown events
* Configuration issues

---

# 🔄 23. Active Checks

An **active check** is scheduled and initiated by Nagios.

```text
Nagios
   ↓
Plugin
   ↓
Remote host/service
   ↓
Result
   ↓
Nagios
```

Examples:

* Ping a server
* Request a website
* Test port 22
* Query DNS

---

# 📥 24. Passive Checks

A **passive check** result is submitted to Nagios by another system or process.

```text
Remote system/application
          ↓
Sends check result
          ↓
Nagios processes result
```

Useful when:

* A system detects its own event
* Firewalls prevent active checks
* Asynchronous events occur
* External monitoring tools submit results

---

# 🌐 25. Remote Monitoring Methods

Nagios can monitor remote systems through several methods.

| Method | Typical use |
| --- | --- |
| ICMP/Ping | Reachability |
| HTTP/HTTPS | Website availability |
| SNMP | Network devices and metrics |
| SSH | Remote command execution |
| NCPA | Cross-platform agent monitoring |
| NRPE | Traditional remote plugin execution |
| Custom APIs | Application metrics |
| Passive results | Event-driven monitoring |

For new deployments, evaluate the currently supported agent and security requirements rather than automatically choosing an old protocol.

---

# 🛰️ 26. SNMP Monitoring

SNMP is widely used for:

* Routers
* Switches
* Firewalls
* Printers
* Network appliances

Useful packages on RHEL-style systems:

`net-snmp`

`net-snmp-utils`

Example SNMP query tool:

`snmpwalk`

Prefer SNMPv3 when supported because it provides authentication and encryption capabilities unavailable in SNMPv1/v2c.

---

# 🏗️ 27. Nagios Core Architecture

```text
                    +----------------------+
                    |     Nagios Core      |
                    | Scheduler + Engine   |
                    +----------+-----------+
                               |
               +---------------+---------------+
               |               |               |
               v               v               v
          check_ping      check_http      check_ssh
               |               |               |
               v               v               v
           Server A        Website B        Server C

                    Results return to Core
                               |
                     +---------+---------+
                     |                   |
                     v                   v
                Notifications       Web Interface
```

---

# 📂 28. Important Source-Install Paths

| Path | Purpose |
| --- | --- |
| `/usr/local/nagios/` | Main installation prefix |
| `/usr/local/nagios/bin/nagios` | Nagios Core binary |
| `/usr/local/nagios/etc/nagios.cfg` | Main configuration |
| `/usr/local/nagios/etc/objects/` | Example/default object files |
| `/usr/local/nagios/libexec/` | Plugins |
| `/usr/local/nagios/share/` | Web content |
| `/usr/local/nagios/sbin/` | CGI programs |
| `/usr/local/nagios/var/` | Runtime data and logs |
| `/usr/local/nagios/var/nagios.log` | Main log |
| `/usr/local/nagios/etc/htpasswd.users` | Common web authentication file |

Paths can differ with packages or custom compile options.

---

# 📄 29. Important Configuration Files

Common source-install files:

| File | Purpose |
| --- | --- |
| `nagios.cfg` | Main Nagios configuration |
| `objects/commands.cfg` | Check and notification commands |
| `objects/contacts.cfg` | Contacts and contact groups |
| `objects/templates.cfg` | Reusable templates |
| `objects/timeperiods.cfg` | Check/notification schedules |
| `objects/localhost.cfg` | Sample localhost definitions |
| Custom `.cfg` files | Additional hosts/services |

---

# 🧬 30. Templates and Inheritance

Nagios supports reusable object templates.

Example concept:

```nagios
define host {
    name                    linux-server
    use                     generic-host
    check_period            24x7
    notification_period     workhours
    register                0
}
```

Then:

```nagios
define host {
    use         linux-server
    host_name   web01
    address     192.168.1.162
}
```

Templates reduce duplicated configuration.

---

# 🧪 31. Lab Design

We will use:

| Role | Hostname | Example IP |
| --- | --- | --- |
| Nagios Core server | `monitor.lab.local` | `192.168.1.161` |
| Linux target | `centos-server.lab.local` | `192.168.1.162` |

The first system runs Nagios Core.

The second system is monitored.

Replace these IP addresses and names with your lab environment.

---

# 👤 32. Verify the Correct System

Check user:

`whoami`

Check identity:

`id`

Check hostname:

`hostnamectl`

Check IP:

`ip a`

Check operating system:

`cat /etc/os-release`

Check directory:

`pwd`

> Always confirm you are installing monitoring software on the intended server.

---

# 📥 33. Installation Strategy

Nagios Core can be installed in different ways:

* Distribution package
* Third-party repository package
* Source compilation
* Automation scripts
* Configuration management

This lab uses **source installation** because it teaches:

* Build dependencies
* Compile process
* Installation layout
* Configuration verification
* Apache integration
* Plugin installation

For enterprise systems, package-based or automated installations may be easier to maintain.

---

# 📦 34. Install Nagios Core Prerequisites — CentOS Stream 9

A practical source-build prerequisite set includes:

`dnf install -y gcc glibc glibc-common perl httpd php wget gd gd-devel s-nail postfix openssl-devel make tar`

Why these packages?

| Package | Purpose |
| --- | --- |
| `gcc` | C compiler |
| `glibc` | Core C library |
| `perl` | Required by build/support components |
| `httpd` | Apache web server |
| `php` | Used by related web functionality/integrations |
| `wget` | Downloads source |
| `gd` / `gd-devel` | Graphics library support |
| `openssl-devel` | OpenSSL headers required by modern Nagios Core |
| `make` | Compiles and installs source |
| `s-nail` / `postfix` | Useful for email notification capability |

---

# 🔐 35. OpenSSL Development Headers Are Required

Modern Nagios Core requires OpenSSL development headers during source compilation.

If configure reports an SSL header error:

`dnf install openssl-devel -y`

Then rerun:

`./configure`

Do not ignore configure errors.

---

# ⬇️ 36. Download the Latest Nagios Core Release

Use the official Nagios/GitHub release source.

Example current version:

```text
4.5.14
```

A version-pinned example:

`cd /tmp`

`wget -O nagioscore.tar.gz https://github.com/NagiosEnterprises/nagioscore/archive/nagios-4.5.14.tar.gz`

Extract:

`tar xzf nagioscore.tar.gz`

Enter the source directory:

`cd /tmp/nagioscore-nagios-4.5.14`

For long-lived automation, pin and test versions instead of blindly installing an unexpected future release.

---

# ⚙️ 37. Configure the Nagios Core Build

Run:

`./configure`

The configure script checks:

* Compiler
* Libraries
* Headers
* Operating-system capabilities
* Installation paths
* Web-server integration requirements

If configure fails:

1. Read the error
2. Install the missing development dependency
3. Run configure again

---

# 🛠️ 38. Compile Nagios Core

Compile:

`make all`

This transforms the source code into executable programs and CGIs.

If compilation fails:

* Read the first meaningful compiler error
* Verify development packages
* Verify disk space
* Verify source version
* Avoid continuing with installation until the build succeeds

---

# 👥 39. Create Nagios User and Group

Current official source-install workflow provides:

`make install-groups-users`

This creates the required Nagios account/group structure.

Then add Apache to the Nagios group:

`usermod -a -G nagios apache`

Verify:

`id nagios`

`id apache`

This is cleaner than manually inventing a separate group when the build system already provides the supported installation target.

---

# 📥 40. Install Nagios Core Binaries

Install the binary files, CGIs, and HTML:

`make install`

Typical result:

```text
/usr/local/nagios/
```

---

# ⚡ 41. Install the systemd Service

Current official source workflow:

`make install-daemoninit`

This installs service/daemon support for systemd-based systems.

Check unit:

`systemctl cat nagios`

Enable later after configuration validation.

---

# 🔐 42. Install External Command Permissions

Run:

`make install-commandmode`

This configures permissions used by the external command interface.

The web interface can use this interface for permitted commands such as:

* Rescheduling checks
* Acknowledging problems
* Scheduling downtime
* Submitting selected external commands

Permissions around the command file are security-sensitive.

---

# 📄 43. Install Sample Configuration

Run:

`make install-config`

This installs sample configuration files required to start learning and testing.

Typical location:

```text
/usr/local/nagios/etc/
```

---

# 🌐 44. Install Apache Web Configuration

Run:

`make install-webconf`

This installs Apache configuration required for the Nagios Core web interface.

Then enable Apache:

`systemctl enable httpd`

Do not start serving the interface until authentication and firewall rules are ready.

---

# 🔌 45. Install Nagios Plugins Prerequisites

On CentOS Stream 9, plugin builds commonly require tools such as:

`dnf install -y gcc glibc glibc-common make gettext automake autoconf wget openssl-devel net-snmp net-snmp-utils`

Some plugin features may require additional libraries or EPEL packages.

Not every plugin is built when every optional library is missing.

---

# ⬇️ 46. Download Nagios Plugins

The Nagios Plugins project is separate from Nagios Core.

Download an approved current release from the official project/GitHub release page.

Generic workflow:

```bash
cd /tmp
wget -O nagios-plugins.tar.gz RELEASE_URL
tar zxf nagios-plugins.tar.gz
cd nagios-plugins-*
```

Do not hard-code a stale lecture version forever.

---

# 🛠️ 47. Compile and Install Plugins

Typical source workflow:

`./configure`

`make`

`make install`

Verify:

`ls -l /usr/local/nagios/libexec/`

Test:

`/usr/local/nagios/libexec/check_ping --help`

---

# 🔑 48. Create the Web Interface Account

Create the initial authentication file:

`htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin`

Enter a strong password.

Important:

> Use `-c` only when creating the file for the first time.

To add another user later:

`htpasswd /usr/local/nagios/etc/htpasswd.users anotheruser`

Using `-c` again would recreate the file and can remove existing users.

---

# 🔥 49. Configure firewalld — Do Not Disable It

Allow HTTP:

`firewall-cmd --permanent --add-service=http`

If HTTPS is configured:

`firewall-cmd --permanent --add-service=https`

Reload:

`firewall-cmd --reload`

Verify:

`firewall-cmd --list-services`

Do **not** use:

```text
systemctl disable --now firewalld
```

as normal production practice.

Open only the services your monitoring architecture actually requires.

---

# 🛡️ 50. SELinux — Keep It Enforcing

Check mode:

`getenforce`

Detailed status:

`sestatus`

The upstream source-install guide has historically assumed permissive/disabled SELinux for simplicity, but production systems should not disable SELinux merely to make Nagios work.

For a source installation under `/usr/local/nagios`:

1. Keep SELinux enforcing
2. Start with correct Apache/Nagios permissions
3. Test the interface and external commands
4. Check AVC denials if something fails

Recent denials:

`ausearch -m AVC -ts recent`

Detailed suggestion:

`sealert -a /var/log/audit/audit.log`

If a policy adjustment is truly required, create the narrowest appropriate file-context or local policy change.

Do not blindly generate and install `audit2allow` rules without reviewing what they permit.

---

# ✅ 51. Validate Nagios Configuration

Before starting or restarting:

`/usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg`

A successful validation should report:

```text
Total Warnings: 0
Total Errors:   0
```

or otherwise clearly indicate no fatal configuration errors.

This is the Nagios equivalent of:

```text
nginx -t
```

for NGINX.

---

# ▶️ 52. Start and Enable Services

Start Apache:

`systemctl start httpd`

Enable Apache:

`systemctl enable httpd`

Start Nagios:

`systemctl start nagios`

Enable Nagios:

`systemctl enable nagios`

Or enable and start together:

`systemctl enable --now httpd nagios`

Check:

`systemctl status httpd`

`systemctl status nagios`

---

# 🌐 53. Access the Nagios Web Interface

Open:

```text
http://192.168.1.161/nagios/
```

or preferably a configured hostname:

```text
http://monitor.lab.local/nagios/
```

Log in with:

```text
nagiosadmin
```

and the password created with `htpasswd`.

In production, use HTTPS rather than sending monitoring credentials over plain HTTP.

---

# 🔒 54. Production Web Security

For production:

* Use HTTPS
* Use trusted certificates
* Restrict access by firewall/VPN
* Use strong credentials
* Avoid exposing Nagios directly to the public internet
* Keep Nagios Core and Apache patched
* Limit administrative users
* Review external-command permissions
* Monitor authentication logs

Monitoring systems contain valuable infrastructure information and should be treated as sensitive administrative systems.

---

# 📁 55. Create a Separate Host Configuration File

Instead of putting all hosts in `localhost.cfg`, create:

`vi /usr/local/nagios/etc/objects/hosts.cfg`

This keeps configuration organized.

A large environment might use:

```text
hosts-linux.cfg
hosts-network.cfg
services-web.cfg
services-database.cfg
contacts-oncall.cfg
```

---

# 🖥️ 56. Define a Linux Host

Example:

```nagios
define host {
    use                     linux-server
    host_name               centos-server
    alias                   CentOS Server
    address                 192.168.1.162
    max_check_attempts      5
    check_period            24x7
    notification_interval   30
    notification_period     24x7
}
```

Meaning:

| Directive | Purpose |
| --- | --- |
| `use` | Inherit from a template |
| `host_name` | Internal Nagios object name |
| `alias` | Human-readable description |
| `address` | IP or resolvable address |
| `max_check_attempts` | Attempts before HARD state |
| `check_period` | When checks run |
| `notification_interval` | Repeat-notification interval |
| `notification_period` | When notifications are allowed |

---

# 📡 57. Define a PING Service

Example:

```nagios
define service {
    use                     generic-service
    host_name               centos-server
    service_description     PING
    check_command           check_ping!100.0,20%!500.0,60%
    max_check_attempts      5
    check_interval          5
    retry_interval          1
    check_period            24x7
    notification_interval   30
    notification_period     24x7
}
```

This monitors network reachability.

---

# 📊 58. Understand the PING Thresholds

Command:

```text
check_ping!100.0,20%!500.0,60%
```

Conceptually:

```text
Warning:
RTA > 100 ms or packet loss > 20%

Critical:
RTA > 500 ms or packet loss > 60%
```

Actual interpretation follows the plugin’s threshold syntax.

Always test the plugin manually:

`/usr/local/nagios/libexec/check_ping -H 192.168.1.162 -w 100.0,20% -c 500.0,60%`

---

# 🌐 59. Add the New Config File to `nagios.cfg`

Edit:

`vi /usr/local/nagios/etc/nagios.cfg`

Add:

```nagios
cfg_file=/usr/local/nagios/etc/objects/hosts.cfg
```

Nagios only loads object files referenced through the main configuration or included directory rules.

---

# ✅ 60. Validate After Every Configuration Change

Run:

`/usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg`

Do not restart if validation reports configuration errors.

Preferred workflow:

```text
Edit
  ↓
Validate
  ↓
Fix errors
  ↓
Validate again
  ↓
Restart/reload service
  ↓
Verify web interface
```

---

# 🔄 61. Restart Nagios

After successful validation:

`systemctl restart nagios`

Check:

`systemctl status nagios`

Review logs:

`tail -n 100 /usr/local/nagios/var/nagios.log`

---

# 🌐 62. Monitor an HTTP Service

If the remote server runs a website:

```nagios
define service {
    use                     generic-service
    host_name               centos-server
    service_description     HTTP
    check_command           check_http
    check_interval          5
    retry_interval          1
}
```

Test manually first:

`/usr/local/nagios/libexec/check_http -H 192.168.1.162`

---

# 🔐 63. Monitor SSH

Example service:

```nagios
define service {
    use                     generic-service
    host_name               centos-server
    service_description     SSH
    check_command           check_ssh
}
```

Manual test:

`/usr/local/nagios/libexec/check_ssh -H 192.168.1.162`

This checks SSH service availability, not full login functionality.

---

# 💽 64. Monitoring Disk Space Requires Remote Data

`check_disk` running locally on the Nagios server checks **the Nagios server's** filesystems.

To check a remote server's disk usage, use a remote method such as:

* NCPA
* NRPE
* SSH-based checks
* SNMP
* Custom API

This distinction is critical.

A beginner mistake is to assume:

```text
check_disk -H remote_server
```

works like `check_ping`.

It does not work that way.

---

# 🧑‍💻 65. Localhost Monitoring

The sample `localhost.cfg` often demonstrates:

* PING
* Root partition usage
* Current users
* Process counts
* Load
* SSH
* HTTP

These examples are useful templates, but do not blindly copy every threshold to production.

Thresholds should match the workload and operational requirements.

---

# 🧰 66. Useful Web Interface Areas

Common Nagios Core interface views include:

* Hosts
* Services
* Host Groups
* Service Groups
* Problems
* Tactical Overview
* Notifications
* Event Log
* Process Info
* Scheduling Queue
* System Information

The web UI helps visualize configuration and status, but Nagios Core configuration itself remains primarily file-based.

---

# 📴 67. Scheduled Downtime

During planned maintenance, schedule downtime instead of allowing expected alerts to page administrators.

Example:

```text
Server reboot window
      ↓
Schedule downtime
      ↓
Checks continue
      ↓
Notifications suppressed according to downtime rules
      ↓
Maintenance completes
```

This keeps alerting meaningful.

---

# ✅ 68. Problem Acknowledgement

If an administrator is already working on an incident, the problem can be acknowledged.

Acknowledgement communicates:

```text
"We know about this problem and someone is handling it."
```

It is not the same as fixing the service.

Use acknowledgements to reduce unnecessary repeated handling while preserving visibility.

---

# 🔗 69. Host Parents and Network Topology

Example:

```text
Nagios
  ↓
Core Router
  ↓
Branch Router
  ↓
Branch Server
```

If the branch router fails, the branch server may be **UNREACHABLE** rather than independently **DOWN**.

Correct parent relationships help Nagios understand network topology.

---

# 📚 70. Host Groups and Service Groups

Host group example:

```text
linux-servers
web-servers
database-servers
network-devices
```

Service group example:

```text
web-services
database-checks
storage-checks
```

Groups improve organization and web-interface visibility.

---

# 📇 71. Contacts and Contact Groups

Nagios notifications are sent to contacts.

Example concepts:

```text
linux-admin
database-admin
network-admin
```

Contact groups:

```text
linux-team
network-team
oncall-team
```

Notifications should go to the team responsible for the affected service.

---

# 📧 72. Email Notifications

Nagios Core can invoke commands that send email through the local mail system.

Typical architecture:

```text
Nagios state change
       ↓
Notification command
       ↓
Local mail utility
       ↓
Postfix / SMTP relay
       ↓
Administrator mailbox
```

The monitoring server must have a functional mail delivery path.

---

# 🚨 73. Notification Design

Avoid alerting on everything.

Good alerts should be:

* Actionable
* Timely
* Routed to the right team
* Based on meaningful thresholds
* Resistant to tiny transient failures
* Escalated appropriately
* Suppressed during scheduled maintenance

Too many useless alerts cause **alert fatigue**.

---

# 📈 74. Monitoring Threshold Design

Bad threshold:

```text
CPU > 50% = CRITICAL
```

for every system.

Better approach:

* Understand normal workload
* Define warning and critical levels
* Consider duration
* Avoid one-size-fits-all thresholds
* Review historical behavior
* Tune based on service impact

Monitoring should represent business impact, not just arbitrary numbers.

---

# 🧪 75. Full Practical Lab Workflow

```text
Verify server
     ↓
Install prerequisites
     ↓
Download Nagios Core
     ↓
Configure
     ↓
Compile
     ↓
Create user/group
     ↓
Install binaries
     ↓
Install service
     ↓
Install command mode
     ↓
Install configs
     ↓
Install Apache config
     ↓
Install plugins
     ↓
Create web user
     ↓
Configure firewall
     ↓
Validate
     ↓
Start Apache + Nagios
     ↓
Create remote host
     ↓
Create PING service
     ↓
Include config file
     ↓
Validate again
     ↓
Restart
     ↓
Verify through browser
```

---

# 🧪 76. Test Before Blaming Nagios

If Nagios reports a problem, run the same plugin manually from the monitoring server.

For ping:

`/usr/local/nagios/libexec/check_ping -H 192.168.1.162 -w 100.0,20% -c 500.0,60%`

For HTTP:

`/usr/local/nagios/libexec/check_http -H 192.168.1.162`

For SSH:

`/usr/local/nagios/libexec/check_ssh -H 192.168.1.162`

This separates:

```text
Nagios configuration problem
```

from:

```text
Actual network/service problem
```

---

# 🔍 77. Check Nagios Configuration Errors

Validate:

`/usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg`

Look for:

* Invalid directive
* Duplicate object
* Unknown host
* Unknown contact
* Missing command
* Missing template
* Missing time period
* Circular dependency
* Referenced file not found

Do not restart Nagios until fatal validation errors are fixed.

---

# ❌ 78. Nagios Service Will Not Start

Check:

`systemctl status nagios`

Review journal:

`journalctl -u nagios -n 100`

Validate:

`/usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg`

Check main log:

`tail -n 100 /usr/local/nagios/var/nagios.log`

Common causes:

* Invalid configuration
* Wrong file ownership
* Missing directories
* Broken plugin path
* Failed install step
* SELinux denial
* Permission problem
* Incorrect object reference

---

# 🌐 79. Apache Web Interface Does Not Load

Check Apache:

`systemctl status httpd`

Check port 80:

`ss -ltnp | grep :80`

Test locally:

`curl -I http://localhost/nagios/`

Check firewall:

`firewall-cmd --list-services`

Check Apache logs:

`journalctl -u httpd -n 100`

Typical Apache log files may include:

```text
/var/log/httpd/access_log
/var/log/httpd/error_log
```

Possible causes:

* Apache stopped
* Firewall blocking HTTP
* Apache configuration not installed
* SELinux denial
* Wrong URL
* Port conflict
* Authentication problem

---

# 🔑 80. Web Login Fails

Check authentication file:

`ls -l /usr/local/nagios/etc/htpasswd.users`

List usernames safely:

`cut -d: -f1 /usr/local/nagios/etc/htpasswd.users`

Reset password:

`htpasswd /usr/local/nagios/etc/htpasswd.users nagiosadmin`

Do not use `-c` unless intentionally recreating the entire authentication file.

Never publish:

```text
htpasswd.users
```

to GitHub.

---

# 🔌 81. Plugin Is Missing

Check:

`ls -l /usr/local/nagios/libexec/`

Search:

`find /usr/local/nagios/libexec -maxdepth 1 -type f -name 'check_*'`

If a plugin did not build, inspect the Nagios Plugins configure output.

Optional plugins may depend on:

* SNMP libraries
* OpenSSL
* Perl modules
* Database client libraries
* Development headers

Not every plugin is guaranteed to compile with the minimum prerequisite set.

---

# 🚫 82. Plugin Returns Permission Denied

Check:

`ls -l /usr/local/nagios/libexec/PLUGIN`

Check path permissions:

`namei -l /usr/local/nagios/libexec/PLUGIN`

Test as the Nagios user:

`sudo -u nagios /usr/local/nagios/libexec/PLUGIN OPTIONS`

Check SELinux:

`ausearch -m AVC -ts recent`

Avoid solving permission problems with:

```text
chmod -R 777
```

Use the least permission required.

---

# 📡 83. PING Check Fails but Host Is Up

Possible causes:

* ICMP blocked by firewall
* Network ACL
* Routing problem
* Wrong IP
* Host firewall
* Plugin permissions
* Packet loss
* High latency

Test:

`ping -c 4 192.168.1.162`

Run plugin:

`/usr/local/nagios/libexec/check_ping -H 192.168.1.162 -w 100.0,20% -c 500.0,60%`

Important:

> A host can be alive even when it does not answer ICMP.

For such systems, choose another host-check strategy.

---

# 🌍 84. HTTP Check Is CRITICAL

Manual test:

`curl -I http://192.168.1.162`

Plugin test:

`/usr/local/nagios/libexec/check_http -H 192.168.1.162`

Check remote listener:

`ss -ltnp | grep :80`

Possible causes:

* Web service stopped
* Firewall
* Wrong virtual host
* TLS required
* DNS issue
* Wrong port
* Application returning an error

For HTTPS:

`/usr/local/nagios/libexec/check_http -S -H example.com`

---

# 🔐 85. SSH Check Is CRITICAL

Test network:

`nc -vz 192.168.1.162 22`

Plugin:

`/usr/local/nagios/libexec/check_ssh -H 192.168.1.162`

Possible causes:

* `sshd` stopped
* Port 22 blocked
* SSH uses a custom port
* Wrong address
* Routing problem

Custom port example:

`/usr/local/nagios/libexec/check_ssh -p 2222 -H 192.168.1.162`

---

# 🧭 86. Host Shows DOWN vs UNREACHABLE

**DOWN** normally means the host itself failed and Nagios considers it unavailable.

**UNREACHABLE** usually means Nagios cannot reach it because a parent/network path is down.

Example:

```text
Nagios
   ↓
Router A — DOWN
   ↓
Server B — UNREACHABLE
```

This prevents dozens of downstream devices from looking like independent failures when one network device caused the outage.

---

# 🔄 87. Nagios Shows PENDING

A service may show:

```text
PENDING
```

when a check has not yet completed.

Possible reasons:

* Nagios just started
* New object recently added
* Check not scheduled yet
* Active checks disabled
* Scheduling issue

Check:

* Scheduling Queue
* Process Info
* `nagios.log`
* Service object settings

---

# 🚨 88. Notifications Are Not Being Sent

Check:

* Is the state HARD?
* Are notifications enabled globally?
* Are notifications enabled for the object?
* Is the notification period active?
* Is the contact assigned?
* Is the contact group correct?
* Are notification options correct?
* Does the notification command work?
* Does the local SMTP/mail relay work?

Search logs:

`grep "NOTIFICATION" /usr/local/nagios/var/nagios.log | tail -n 50`

Test mail separately before blaming Nagios.

---

# 📧 89. Test the Mail Path Separately

Example:

`echo "Nagios mail test" | mail -s "Nagios Test" admin@example.com`

If this fails, troubleshoot:

* Postfix
* SMTP relay
* DNS
* Authentication
* Firewall
* Sender restrictions

Nagios cannot deliver email successfully if the underlying mail path is broken.

---

# 💤 90. Avoid Alert Fatigue

Alert fatigue occurs when administrators receive too many low-value notifications.

Symptoms:

* Hundreds of alerts
* Same issue repeated constantly
* Administrators ignore notifications
* Critical events get lost in noise

Improve monitoring by:

* Setting meaningful thresholds
* Using retry logic
* Using dependencies
* Scheduling downtime
* Escalating carefully
* Removing useless checks
* Routing alerts to responsible teams
* Reviewing recurring alerts

---

# 🔒 91. Security Best Practices

A strong Nagios deployment should:

* Keep Nagios Core updated
* Keep plugins updated
* Keep Apache updated
* Use HTTPS
* Restrict web UI access
* Keep `firewalld` enabled
* Keep SELinux enforcing
* Use strong passwords
* Protect configuration files
* Protect monitoring credentials
* Avoid running checks as root unnecessarily
* Restrict plugin execution
* Validate third-party plugins
* Limit remote-agent permissions
* Prefer secure protocols
* Monitor the monitoring server itself
* Back up configuration
* Test restoration

---

# ⚠️ 92. Plugins Are Executable Code

A plugin can be:

* Binary
* Shell script
* Python script
* Perl script
* Other executable program

Therefore, third-party plugins are code execution.

Before installing one:

* Review source
* Verify publisher
* Check permissions
* Avoid unnecessary root execution
* Test in a safe environment
* Pin versions
* Record changes

Do not download random monitoring scripts directly onto a production monitoring server and execute them blindly.

---

# 👑 93. Avoid Running Every Check as Root

Nagios typically runs checks using its service account.

If a plugin needs privileged information, safer patterns include:

* Narrow `sudoers` rule
* Agent-specific permission
* Read-only API
* SNMP
* Capability-based access

Avoid:

```text
nagios ALL=(ALL) NOPASSWD: ALL
```

This grants excessive privilege.

Use the smallest required permission.

---

# 🔐 94. Protect Secrets

Nagios configurations or plugins may need:

* API keys
* Database passwords
* SNMP credentials
* Agent tokens
* SSH keys

Do not place secrets:

* In public repositories
* In screenshots
* In world-readable files
* Directly in documentation

Restrict permissions:

`chmod 600 SECRET_FILE`

Use organizational secret-management practices where possible.

---

# 💾 95. Back Up Nagios Configuration

Important paths:

```text
/usr/local/nagios/etc/
/usr/local/nagios/var/
/usr/local/nagios/libexec/
```

At minimum, back up:

* Main configuration
* Object definitions
* Contacts
* Commands
* Custom plugins
* Web authentication configuration
* TLS/Apache configuration
* Custom scripts

Test restoration periodically.

---

# 🧹 96. Configuration Organization for Larger Environments

Avoid one huge `hosts.cfg`.

Example:

```text
/usr/local/nagios/etc/objects/
├── commands.cfg
├── contacts.cfg
├── templates.cfg
├── timeperiods.cfg
├── hosts-linux.cfg
├── hosts-network.cfg
├── services-web.cfg
├── services-dns.cfg
├── services-database.cfg
└── hostgroups.cfg
```

Then include the files through `nagios.cfg`.

Consistent naming makes troubleshooting easier.

---

# 📏 97. Naming Conventions

Good object names:

```text
web-prod-01
db-prod-01
router-branch-01
HTTP - Customer Portal
DISK - Root Filesystem
SSL - Certificate Expiration
```

Avoid vague names:

```text
server1
server2
test
thing
```

Clear names make alerts actionable.

---

# 🧠 98. Monitoring Design Principle: Monitor the Service, Not Only the Server

A server responding to ping does not mean the business service works.

Example:

```text
PING       OK
SSH        OK
HTTP       OK
Login API  CRITICAL
Database   CRITICAL
```

Good monitoring combines:

* Infrastructure reachability
* Service availability
* Application behavior
* Performance
* Business-level checks

---

# 🎯 99. Monitor What Users Actually Experience

A stronger web check may test:

* DNS lookup
* TCP connection
* TLS certificate
* HTTP response code
* Page content
* Response time

Example idea:

```text
Does https://shop.example.com return 200?
Does the response contain "Checkout"?
Does it respond within 2 seconds?
Is the TLS certificate valid?
```

This is more useful than ping alone.

---

# 📊 100. Performance Data

Many plugins return performance data.

Example:

```text
PING OK - Packet loss = 0%, RTA = 1.66 ms | rta=1.660ms;100.000;500.000;0; pl=0%;20;60;;
```

Text before `|`:

```text
Human-readable status
```

Data after `|`:

```text
Performance metrics
```

Nagios Core can expose this data to addons for graphing and trend systems.

---

# 🧱 101. Nagios Core Does Not Provide Every Enterprise Feature by Itself

Core provides the monitoring engine and basic web status interface.

Features such as:

* Advanced dashboards
* Configuration wizards
* Rich reporting
* Capacity planning
* Large-scale graphical management
* Built-in enterprise configuration UI

are more characteristic of Nagios XI or external addons.

Understanding this distinction prevents unrealistic expectations from Nagios Core.

---

# 🔄 102. Core Configuration Workflow

Remember:

```text
Define command
      ↓
Define host
      ↓
Define service
      ↓
Assign contact/time periods
      ↓
Include configuration file
      ↓
Validate
      ↓
Restart
      ↓
Verify check
```

---

# 🧪 103. Complete Remote Host Lab

## Step 1: Confirm target is reachable

`ping -c 4 192.168.1.162`

---

## Step 2: Test plugin manually

`/usr/local/nagios/libexec/check_ping -H 192.168.1.162 -w 100.0,20% -c 500.0,60%`

---

## Step 3: Create object file

`vi /usr/local/nagios/etc/objects/hosts.cfg`

---

## Step 4: Define host

```nagios
define host {
    use                     linux-server
    host_name               centos-server
    alias                   CentOS Server
    address                 192.168.1.162
    max_check_attempts      5
    check_period            24x7
    notification_interval   30
    notification_period     24x7
}
```

---

## Step 5: Define PING service

```nagios
define service {
    use                     generic-service
    host_name               centos-server
    service_description     PING
    check_command           check_ping!100.0,20%!500.0,60%
    max_check_attempts      5
    check_interval          5
    retry_interval          1
    check_period            24x7
    notification_interval   30
    notification_period     24x7
}
```

---

## Step 6: Include the file

Add to:

`/usr/local/nagios/etc/nagios.cfg`

```nagios
cfg_file=/usr/local/nagios/etc/objects/hosts.cfg
```

---

## Step 7: Validate

`/usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg`

---

## Step 8: Restart

`systemctl restart nagios`

---

## Step 9: Verify

Open:

```text
http://monitor.lab.local/nagios/
```

Check:

```text
Hosts
Services
```

---

# 🧪 104. Failure Simulation Lab

To understand Nagios state changes:

1. Confirm target shows UP
2. Shut down the target or block the monitored service
3. Watch SOFT failures
4. Wait for the configured maximum attempts
5. Observe HARD state
6. Review notification/log behavior
7. Restore the target
8. Observe recovery

Follow the Nagios log:

`tail -f /usr/local/nagios/var/nagios.log`

This teaches more than merely seeing a green dashboard.

---

# 🧪 105. HTTP Failure Simulation

If monitoring HTTP:

1. Confirm HTTP is OK
2. Stop the remote web server:

`systemctl stop httpd`

or:

`systemctl stop nginx`

3. Watch Nagios detect failure
4. Check plugin manually
5. Start the service again
6. Observe recovery

This demonstrates the difference between:

```text
Host UP
```

and:

```text
HTTP CRITICAL
```

---

# 🧰 106. Troubleshooting Workflow

```text
Is Nagios running?
        ↓
Is configuration valid?
        ↓
Does the plugin exist?
        ↓
Does the plugin work manually?
        ↓
Can the monitoring server reach the target?
        ↓
Is firewall blocking it?
        ↓
Is SELinux denying access?
        ↓
Is the object definition correct?
        ↓
Are thresholds correct?
        ↓
Are notifications configured?
        ↓
Check Nagios + Apache logs
```

---

# 📋 107. Command Cheat Sheet

| Task | Command |
| --- | --- |
| Validate Nagios config | `/usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg` |
| Start Nagios | `systemctl start nagios` |
| Stop Nagios | `systemctl stop nagios` |
| Restart Nagios | `systemctl restart nagios` |
| Enable Nagios | `systemctl enable nagios` |
| Status | `systemctl status nagios` |
| Start Apache | `systemctl start httpd` |
| Enable Apache | `systemctl enable httpd` |
| Apache status | `systemctl status httpd` |
| Follow Nagios log | `tail -f /usr/local/nagios/var/nagios.log` |
| List plugins | `ls -l /usr/local/nagios/libexec/` |
| Test ping | `/usr/local/nagios/libexec/check_ping -H HOST -w 100.0,20% -c 500.0,60%` |
| Test HTTP | `/usr/local/nagios/libexec/check_http -H HOST` |
| Test SSH | `/usr/local/nagios/libexec/check_ssh -H HOST` |
| Check firewall | `firewall-cmd --list-all` |
| Allow HTTP | `firewall-cmd --permanent --add-service=http` |
| Allow HTTPS | `firewall-cmd --permanent --add-service=https` |
| Reload firewall | `firewall-cmd --reload` |
| Check SELinux | `getenforce` |
| Review AVC denials | `ausearch -m AVC -ts recent` |
| Create web user | `htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin` |
| Add another web user | `htpasswd /usr/local/nagios/etc/htpasswd.users USER` |
| Check port 80 | `ss -ltnp \| grep :80` |
| Test local web UI | `curl -I http://localhost/nagios/` |

---

# 🧠 108. Memory Framework

Remember:

```text
Core    = Schedules and processes monitoring
Plugin  = Performs the actual check
Host    = Device
Service = Function on the device
Contact = Person/team notified
```

States:

```text
Host:
UP / DOWN / UNREACHABLE

Service:
OK / WARNING / CRITICAL / UNKNOWN
```

Plugin exit codes:

```text
0 = OK
1 = WARNING
2 = CRITICAL
3 = UNKNOWN
```

Workflow:

> **Install → Configure → Validate → Start → Check → Alert → Troubleshoot → Recover**

---

# 💼 109. Questions

## Q1. What is Nagios?

Nagios is an infrastructure monitoring system used to monitor hosts, services, applications, and network devices and notify administrators about problems and recoveries.

---

## Q2. What is Nagios Core?

Nagios Core is the open-source monitoring engine that schedules checks, processes results, tracks state, and triggers notifications.

---

## Q3. What is Nagios XI?

Nagios XI is a commercial product that builds on Nagios Core and adds enterprise management, configuration, reporting, dashboards, and support features.

---

## Q4. What was Nagios originally called?

NetSaint.

---

## Q5. Who created Nagios?

Ethan Galstad.

---

## Q6. When was NetSaint released as open source?

1999.

---

## Q7. When was it renamed Nagios?

2002.

---

## Q8. What is a Nagios plugin?

An executable program or script that performs a monitoring check and returns a status to Nagios.

---

## Q9. What are the plugin exit codes?

```text
0 = OK
1 = WARNING
2 = CRITICAL
3 = UNKNOWN
```

---

## Q10. What is the difference between a host and a service?

A host is a monitored device or system. A service is a specific function or metric monitored on that host.

---

## Q11. What are host states?

UP, DOWN, and UNREACHABLE.

---

## Q12. What are service states?

OK, WARNING, CRITICAL, and UNKNOWN.

---

## Q13. What is a SOFT state?

A temporary problem state while Nagios retries the check before confirming a HARD state.

---

## Q14. What is a HARD state?

A confirmed state reached after the configured check attempts, which can trigger notifications.

---

## Q15. Why does Nagios retry failed checks?

To avoid alerting on temporary glitches.

---

## Q16. What is `max_check_attempts`?

The number of attempts used before a state is confirmed as HARD.

---

## Q17. What is `check_interval`?

The interval between normal scheduled checks.

---

## Q18. What is `retry_interval`?

The shorter interval used while retrying a problem before it becomes HARD.

---

## Q19. What is an active check?

A check initiated and scheduled by Nagios.

---

## Q20. What is a passive check?

A result submitted to Nagios by another process or system.

---

## Q21. Where are plugins stored in a common source installation?

`/usr/local/nagios/libexec/`

---

## Q22. What is the main Nagios configuration file?

`/usr/local/nagios/etc/nagios.cfg`

---

## Q23. How do you validate Nagios configuration?

`/usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg`

---

## Q24. Where is the main Nagios log in a source installation?

`/usr/local/nagios/var/nagios.log`

---

## Q25. What web server is commonly used with Nagios Core source installs?

Apache HTTP Server (`httpd`).

---

## Q26. What is `check_ping` used for?

To test host reachability, round-trip time, and packet loss.

---

## Q27. What does `check_http` monitor?

HTTP/HTTPS service behavior such as connectivity, response status, content, and timing depending on options.

---

## Q28. Can `check_disk` on the Nagios server directly see a remote server's disks?

No. Remote disk metrics require an agent or remote execution method such as NCPA, NRPE, SSH, SNMP, or another integration.

---

## Q29. What is notification escalation?

Sending continued problem notifications to additional or higher-level contacts according to defined rules.

---

## Q30. What is scheduled downtime?

A maintenance period during which Nagios knows a host or service is intentionally unavailable and suppresses normal problem notifications according to downtime behavior.

---

## Q31. What is acknowledgement?

Marking a known problem as being handled by an administrator.

---

## Q32. What is the difference between DOWN and UNREACHABLE?

DOWN indicates the host itself is considered failed. UNREACHABLE indicates the network path or parent relationship prevents Nagios from reaching it.

---

## Q33. Why are parent relationships useful?

They allow Nagios to understand network topology and distinguish root network failures from downstream unreachable devices.

---

## Q34. What is alert fatigue?

A condition where too many low-value alerts cause administrators to ignore notifications.

---

## Q35. Why should Nagios web access use HTTPS?

The web interface contains sensitive infrastructure information and credentials should not travel in clear text.

---

## Q36. Should you disable `firewalld` for Nagios?

No. Allow only the required services and ports.

---

## Q37. Should you disable SELinux for Nagios?

Not as normal production practice. Keep SELinux enforcing and troubleshoot specific denials.

---

## Q38. How do you troubleshoot a CRITICAL plugin result?

Run the plugin manually as the Nagios user, verify connectivity, review thresholds, inspect firewall/SELinux, and check Nagios logs.

---

## Q39. Why validate configuration before restart?

A syntax or object-reference error can prevent Nagios from starting correctly.

---

## Q40. What is the most important monitoring principle?

Monitor what matters to users and the business—not merely whether a server responds to ping.

---

# 📌 110. Ultra-Short Revision

* Nagios = Infrastructure monitoring
* Nagios Core = Open-source monitoring engine
* Nagios XI = Commercial enterprise product
* Original name = NetSaint
* Creator = Ethan Galstad
* NetSaint open-source release = 1999
* Renamed Nagios = 2002
* Core current in Aug/Sep 2026 = `4.5.14`
* Core binary = `/usr/local/nagios/bin/nagios`
* Main config = `/usr/local/nagios/etc/nagios.cfg`
* Object configs = `/usr/local/nagios/etc/objects/`
* Plugins = `/usr/local/nagios/libexec/`
* Log = `/usr/local/nagios/var/nagios.log`
* Validate = `nagios -v nagios.cfg`
* Web server = Apache `httpd`
* Web path = `/nagios/`
* Default web user often = `nagiosadmin`
* Plugin exit `0` = OK
* Plugin exit `1` = WARNING
* Plugin exit `2` = CRITICAL
* Plugin exit `3` = UNKNOWN
* Host states = UP/DOWN/UNREACHABLE
* Service states = OK/WARNING/CRITICAL/UNKNOWN
* SOFT = Retrying
* HARD = Confirmed
* Active check = Nagios initiates
* Passive check = External result submitted
* PING = Reachability
* `check_http` = Web service
* `check_ssh` = SSH service
* Remote disk requires remote monitoring method
* Keep firewalld enabled
* Keep SELinux enforcing
* Use HTTPS in production
* Validate before restart
* Test plugins manually during troubleshooting

---

# 📚 111. Official References

* Nagios Core project: `https://www.nagios.org/projects/nagios-core/`
* Nagios Core downloads: `https://www.nagios.org/downloads/nagios-core-/`
* Nagios history: `https://www.nagios.org/about/history/`
* Nagios Core 4.x changelog: `https://www.nagios.org/projects/nagios-core/4x/`
* Nagios Core GitHub: `https://github.com/NagiosEnterprises/nagioscore`
* Nagios Core source-install guide: `https://support.nagios.com/kb/article.php?id=96`
* Nagios Plugins GitHub: `https://github.com/nagios-plugins/nagios-plugins`
* Nagios Plugins project: `https://nagios-plugins.org/`

---

# 🏆 112. Takeaway

A beginner knows that Nagios shows green and red status screens.

A strong Linux administrator understands:

* The difference between Nagios Core and Nagios XI
* How the Nagios scheduler and plugins work together
* Plugin exit codes
* Host states and service states
* SOFT vs HARD states
* Active vs passive checks
* Check attempts and retry intervals
* Host parents and network reachability
* How host and service objects are defined
* How templates reduce duplicated configuration
* How plugins should be tested manually
* Why remote metrics require agents or remote execution
* How contacts, time periods, notifications, and escalations work
* How to avoid alert fatigue
* How to schedule downtime and acknowledge incidents
* How to validate configuration before restarting
* How to secure the Apache web interface
* Why monitoring credentials and plugins must be protected
* Why firewalld and SELinux should be configured rather than disabled
* How to troubleshoot a failed check systematically
* Why monitoring must represent real user and business impact

Nagios is not simply a dashboard. It is an event-processing and monitoring engine that schedules checks, executes plugins, tracks state, detects failures, generates notifications, and gives administrators a structured way to understand infrastructure health.

A useful monitoring system should answer three questions quickly:

```text
What failed?
How serious is it?
Who needs to act?
```

When those questions are answered correctly, monitoring becomes an operational tool rather than just another screen full of alerts.

---

✍️ Notes By Abhishek (Ez Abyss)
