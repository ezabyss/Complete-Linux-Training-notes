# 🧾 Centralized Logging with rsyslog 

---

## 🎯 1. What Is Centralized Logging?

**Centralized logging** means collecting log messages from many servers, applications, and network devices in one central location.

> **Simple understanding:** A central log server is a control room where logs from the whole environment are collected and reviewed.

```text
Linux Server 1 ──┐
Linux Server 2 ──┤
Web Server ──────┤
Database Server ─┼──→ Central Log Server
Firewall ────────┤
Router ──────────┤
Printer ─────────┘
```

Without centralized logging, an administrator may need to sign in to every system separately.

With centralized logging, events from many systems can be reviewed from one place.

---

# 🌍 2. Real-World Example

Suppose a company has 500 servers.

At the same time:

* An application server stops responding
* A database reports disk errors
* Several hosts report failed SSH logins
* A firewall blocks suspicious traffic

Without a central logger:

```text
Administrator
    ↓
Log in to Server 1
    ↓
Check logs
    ↓
Log in to Server 2
    ↓
Repeat again and again
```

With a central logger:

```text
All systems
     ↓
Central rsyslog server
     ↓
Search by host, service, severity, or time
     ↓
Find the problem faster
```

---

# 🧠 3. Why Do Organizations Centralize Logs?

Central logging helps with:

* Troubleshooting
* Security monitoring
* Incident investigation
* Compliance and auditing
* Detecting repeated failures
* Comparing events across systems
* Preserving logs when a client fails
* Creating alerts
* Capacity planning
* Correlating related events
* Reducing time spent checking hosts individually

Example event sequence:

```text
10:01:02 — Firewall accepts SSH connection
10:01:04 — Server reports failed password
10:01:08 — Server reports another failed password
10:01:15 — Account becomes locked
```

When the events are collected together, the full sequence is easier to understand.

---

# 🏗️ 4. Main Components of a Logging System

| Component | Purpose |
| --- | --- |
| Log source | Generates an event |
| Logging daemon | Collects and processes messages |
| Transport | Sends logs over UDP, TCP, TLS, or RELP |
| Central collector | Receives messages from clients |
| Filter | Selects messages based on rules |
| Queue | Buffers messages during delays or outages |
| Storage | Saves messages in files or platforms |
| Alerting system | Notifies administrators |
| Dashboard | Displays trends and events |
| Retention policy | Controls how long logs are stored |

---

## Easy Analogy

| Logging component | Transportation analogy |
| --- | --- |
| Log source | Passenger |
| rsyslog client | Local station |
| Network transport | Railway line |
| Central logger | Grand Central terminal |
| Log file | Arrival platform |
| Filter | Route controller |
| Queue | Waiting area |
| Alert | Emergency announcement |

---

# 📜 5. What Is a Log?

A **log** is a timestamped record of an event.

Example:

```text
Aug 01 04:30:12 web01 sshd[2150]: Failed password for invalid user admin from 192.168.1.50 port 54210 ssh2
```

This event contains:

* Date
* Time
* Hostname
* Program
* Process ID
* Event description
* Remote IP
* Remote port
* Protocol

Logs help answer:

* What happened?
* When did it happen?
* Where did it happen?
* Which program reported it?
* Who or what caused it?
* Was the action successful?
* How serious was it?

---

# 📦 6. What Is rsyslog?

**rsyslog** is a high-performance logging system used on many Linux distributions.

It can:

* Receive local log events
* Work with `systemd-journald`
* Filter messages
* Transform messages
* Write messages to files
* Forward events to remote systems
* Receive network logs
* Buffer messages in queues
* Use UDP, TCP, TLS, and RELP
* Send events to databases and observability platforms through modules

Important components:

| Item | Value |
| --- | --- |
| Package | `rsyslog` |
| Service | `rsyslog` |
| Daemon | `rsyslogd` |
| Main configuration | `/etc/rsyslog.conf` |
| Additional configuration | `/etc/rsyslog.d/*.conf` |
| Common log location | `/var/log/` |
| Validate configuration | `rsyslogd -N1` |
| Generate test event | `logger` |

---

## Important Name Clarification

```text
Package = rsyslog
Service = rsyslog
Daemon  = rsyslogd
```

The daemon uses the traditional `d` suffix because it is the background process.

---

# 🆚 7. rsyslog and systemd-journald

Modern RHEL-style systems commonly use both.

| systemd-journald | rsyslog |
| --- | --- |
| Receives events from systemd and services | Filters, routes, stores, and forwards events |
| Stores structured journal entries | Commonly writes traditional text logs |
| Queried with `journalctl` | Configured with rsyslog rules |
| Local journal focus | Local and remote pipelines |

Simplified relationship:

```text
Applications and kernel
          ↓
systemd-journald
          ↓
rsyslogd
          ↓
Local files and/or central logger
```

The exact interaction can vary by system configuration.

---

# 🗂️ 8. Journal Logs and Traditional Log Files

View all journal events:

`journalctl`

Show the current boot:

`journalctl -b`

Show one service:

`journalctl -u sshd`

Follow new events:

`journalctl -f`

Common traditional files:

| File | Typical purpose |
| --- | --- |
| `/var/log/messages` | General system messages |
| `/var/log/secure` | Authentication and security events |
| `/var/log/cron` | Scheduled-job activity |
| `/var/log/maillog` | Mail events |
| `/var/log/audit/audit.log` | Linux Audit events |

Available files depend on the distribution and installed services.

---

# 🧰 9. Related Logging Technologies

## syslog

A general logging protocol and message-format family.

## syslog-ng

Another flexible logging daemon.

## RELP

Reliable Event Logging Protocol, designed for reliable event delivery.

## Fluent Bit and Fluentd

Log processors often used with containers and cloud environments.

## Logstash

A log-processing pipeline commonly used with Elasticsearch.

## Grafana Loki

A log aggregation platform designed for integration with Grafana.

## SIEM

A Security Information and Event Management platform adds functions such as:

* Search
* Correlation
* Alerting
* Dashboards
* Retention
* Threat detection
* Reporting

rsyslog can forward events into these platforms.

---

# 🌐 10. Important Ports and Transports

| Transport | Purpose | Common port |
| --- | --- | ---: |
| Syslog over UDP | Lightweight connectionless forwarding | `514/udp` |
| Syslog over TCP | Connection-oriented forwarding | `514/tcp` |
| Syslog over TLS | Encrypted syslog | `6514/tcp` |
| RELP | Reliable event delivery | Often `20514/tcp` in examples |

---

## Memory Trick

```text
514  = Traditional remote syslog
6514 = Syslog protected with TLS
```

---

# 📡 11. UDP vs TCP vs TLS vs RELP

| Method | Advantages | Limitations |
| --- | --- | --- |
| UDP | Low overhead and simple | No delivery confirmation; messages can be lost |
| TCP | Connection-oriented and more reliable | Plain TCP is not encrypted |
| TCP with TLS | Reliability, encryption, and authentication | Requires certificates |
| RELP | Stronger reliable-delivery behavior | Requires RELP support |

Use UDP when occasional loss is acceptable.

Use TCP when reliable forwarding matters.

Use TLS when logs cross untrusted networks or contain sensitive information.

Use RELP when the environment strongly prioritizes preventing message loss.

---

# 🔄 12. Basic Central Logging Workflow

```text
Application creates event
          ↓
Local logging system receives it
          ↓
rsyslog applies filters
          ↓
Message enters forwarding action
          ↓
Queue buffers when needed
          ↓
Network sends message
          ↓
Central server receives it
          ↓
Rules select destination
          ↓
Message is stored
```

---

# 🧱 13. Common rsyslog Roles

## Local Logger

```text
Local services → rsyslog → /var/log/messages
```

## Forwarding Client

```text
Client → Central collector
```

## Central Logging Server

```text
Client 1 ─┐
Client 2 ─┼→ Central rsyslog server
Client 3 ─┘
```

## Relay

```text
Branch systems
      ↓
Regional rsyslog relay
      ↓
Central SIEM
```

---

# ⚠️ 14. Central Collection Is Not Automatically SIEM Analysis

A central rsyslog server can:

* Receive logs
* Filter logs
* Store logs
* Forward logs

It does not automatically provide:

* Dashboards
* Full-text indexing
* Threat correlation
* Advanced analytics
* Machine-learning detection

Those functions require another platform.

---

# 🔐 15. Why Central Logs Need Protection

Logs can contain:

* Usernames
* IP addresses
* Hostnames
* Authentication failures
* Internal paths
* Application errors
* Security events
* Transaction identifiers

Attackers may try to:

* Read logs
* Modify evidence
* Delete events
* Flood the collector
* Impersonate a source
* Inject misleading messages

A secure design should consider:

* Encryption
* Authentication
* Permissions
* Network restrictions
* Retention
* Integrity
* Backups
* Time synchronization
* Storage limits

---

# 🕒 16. Time Synchronization Is Critical

Central logs are difficult to compare when clocks are different.

Check time:

`timedatectl`

Check chrony sources:

`chronyc sources -v`

Check tracking:

`chronyc tracking`

> Accurate time is a required part of reliable logging.

---

# 🧪 17. Lab Design

| Role | Hostname | Example IP |
| --- | --- | --- |
| Central logging server | `logserver.lab.local` | `192.168.1.150` |
| Client 1 | `client1.lab.local` | `192.168.1.151` |
| Client 2 | `client2.lab.local` | `192.168.1.152` |

Replace the example addresses with your real lab addresses.

---

# 👤 18. Verify the Current System

`whoami`

`id`

`hostname`

`hostnamectl`

`pwd`

`ip a`

`ip route`

Always confirm whether you are working on the central server or a client.

---

# 🔍 19. Check Whether rsyslog Is Installed

`rpm -q rsyslog`

Another method:

`dnf list installed rsyslog`

Broad search:

`rpm -qa | grep rsyslog`

Find the daemon:

`command -v rsyslogd`

---

# 📥 20. Install rsyslog

`dnf install rsyslog -y`

Verify:

`rpm -q rsyslog`

Show version:

`rsyslogd -v`

List package files:

`rpm -ql rsyslog`

List package configuration files:

`rpm -qc rsyslog`

---

# ▶️ 21. Start and Enable rsyslog

Start:

`systemctl start rsyslog`

Enable at boot:

`systemctl enable rsyslog`

Start and enable together:

`systemctl enable --now rsyslog`

Check status:

`systemctl status rsyslog`

Check active state:

`systemctl is-active rsyslog`

Check enabled state:

`systemctl is-enabled rsyslog`

---

# 🔄 22. Restart, Reload, Stop, and Disable

Restart:

`systemctl restart rsyslog`

Reload:

`systemctl reload rsyslog`

Stop:

`systemctl stop rsyslog`

Disable:

`systemctl disable rsyslog`

Stop and disable:

`systemctl disable --now rsyslog`

Use service-management commands instead of manually killing `rsyslogd`.

---

# 📂 23. Important Files and Directories

| Path | Purpose |
| --- | --- |
| `/etc/rsyslog.conf` | Main configuration |
| `/etc/rsyslog.d/` | Additional configuration snippets |
| `/var/log/` | Common local log storage |
| `/var/lib/rsyslog/` | Common working or queue-data location |
| `/run/log/journal/` | Runtime journal storage |
| `/var/log/journal/` | Persistent journal storage when configured |
| `/etc/logrotate.conf` | Main logrotate configuration |
| `/etc/logrotate.d/` | Per-service rotation rules |

---

## Important Correction

The main configuration file is:

```text
/etc/rsyslog.conf
```

It is not normally:

```text
/etc/syslog.conf
```

on a modern RHEL system using rsyslog.

---

# 💾 24. Back Up Configuration

`cp /etc/rsyslog.conf /etc/rsyslog.conf.backup`

Back up a snippet:

`cp /etc/rsyslog.d/central.conf /etc/rsyslog.d/central.conf.backup`

Verify:

`ls -l /etc/rsyslog.conf.backup /etc/rsyslog.d/*.backup`

---

# 👁️ 25. View Configuration

`less /etc/rsyslog.conf`

List snippets:

`find /etc/rsyslog.d -maxdepth 1 -type f -print`

Search modules:

`grep -R "module(" /etc/rsyslog.conf /etc/rsyslog.d`

Search forwarding rules:

`grep -R "omfwd\|@@\|@" /etc/rsyslog.conf /etc/rsyslog.d`

---

# ✅ 26. Validate Configuration

`rsyslogd -N1`

Recommended workflow:

```text
Edit
  ↓
rsyslogd -N1
  ↓
Restart or reload
  ↓
Generate a test
  ↓
Verify storage
```

---

# 🧩 27. Configuration Building Blocks

Modern rsyslog configurations use:

* Global settings
* Modules
* Inputs
* Templates
* Filters
* Rulesets
* Actions
* Queues

Example:

```rsyslog
module(load="imtcp")

template(
    name="RemoteFile"
    type="string"
    string="/var/log/remote/%HOSTNAME%/%PROGRAMNAME%.log"
)

ruleset(name="RemoteRules") {
    action(type="omfile" dynaFile="RemoteFile")
}

input(type="imtcp" port="514" ruleset="RemoteRules")
```

---

# 🔌 28. Input Modules

| Module | Purpose |
| --- | --- |
| `imjournal` | Reads from systemd journal |
| `imuxsock` | Receives local Unix-socket messages |
| `imklog` | Reads kernel events |
| `imtcp` | Receives syslog over TCP |
| `imudp` | Receives syslog over UDP |
| `imfile` | Reads text files |
| `imrelp` | Receives RELP messages |

TCP input example:

```rsyslog
module(load="imtcp")
input(type="imtcp" port="514")
```

---

# 📤 29. Output Modules

| Module | Purpose |
| --- | --- |
| `omfile` | Writes messages to files |
| `omfwd` | Forwards messages over the network |
| `omrelp` | Sends through RELP |
| `omprog` | Sends events to a program |

File action:

```rsyslog
action(type="omfile" file="/var/log/custom.log")
```

Forwarding action:

```rsyslog
action(
    type="omfwd"
    target="192.168.1.150"
    port="514"
    protocol="tcp"
)
```

---

# 🏷️ 30. Syslog Facilities

| Facility | Typical use |
| --- | --- |
| `kern` | Kernel |
| `user` | User-level messages |
| `mail` | Mail subsystem |
| `daemon` | System daemons |
| `auth` | Authentication |
| `authpriv` | Private authentication |
| `syslog` | Logging system |
| `cron` | Scheduled jobs |
| `lpr` | Printing |
| `ftp` | FTP service |
| `local0`–`local7` | Custom applications |
| `*` | All facilities |

---

# 🚨 31. Severity Levels

| Number | Name | Meaning |
| ---: | --- | --- |
| `0` | `emerg` | System unusable |
| `1` | `alert` | Immediate action required |
| `2` | `crit` | Critical condition |
| `3` | `err` | Error |
| `4` | `warning` | Warning |
| `5` | `notice` | Normal but significant |
| `6` | `info` | Informational |
| `7` | `debug` | Debug details |

Memory:

```text
Emergency
Alert
Critical
Error
Warning
Notice
Information
Debug
```

---

# 🎯 32. Traditional Selector Syntax

Format:

```text
facility.severity    action
```

Example:

```rsyslog
authpriv.*    /var/log/secure
```

Another example:

```rsyslog
*.err    /var/log/all-errors.log
```

This selects error events and more severe messages from all facilities.

---

# 🧪 33. Generate Test Messages

Basic test:

`logger "Central logging test from $(hostname)"`

Add a tag:

`logger -t LABTEST "Testing rsyslog"`

Choose facility and severity:

`logger -p local0.notice "Local0 notice from $(hostname)"`

Send an error:

`logger -p user.err "User error from $(hostname)"`

Search the journal:

`journalctl -t LABTEST`

Search local files:

`grep -R "Central logging test" /var/log 2>/dev/null`

---

# 🖥️ 34. Configure the Central Server for TCP

Create:

`vi /etc/rsyslog.d/10-central-server.conf`

Add:

```rsyslog
module(load="imtcp")

template(
    name="RemoteLogs"
    type="string"
    string="/var/log/remote/%HOSTNAME%/%PROGRAMNAME%.log"
)

ruleset(name="RemoteTcpRules") {
    action(
        type="omfile"
        dynaFile="RemoteLogs"
        createDirs="on"
    )
}

input(
    type="imtcp"
    port="514"
    ruleset="RemoteTcpRules"
)
```

This configuration:

1. Enables TCP input
2. Creates a dynamic file path
3. Stores messages by hostname and program
4. Uses a separate ruleset for remote messages
5. Listens on TCP port 514

---

# 📁 35. Understand the Dynamic Template

Template:

```text
/var/log/remote/%HOSTNAME%/%PROGRAMNAME%.log
```

Example:

```text
Hostname: client1
Program: sshd
```

Stored as:

```text
/var/log/remote/client1/sshd.log
```

This is cleaner than storing every host in one large file.

---

# 🔥 36. Configure the Firewall

Allow TCP port 514:

`firewall-cmd --permanent --add-port=514/tcp`

Reload:

`firewall-cmd --reload`

Verify:

`firewall-cmd --list-ports`

After restarting rsyslog, check:

`ss -ltnp | grep :514`

---

# ✅ 37. Validate and Activate the Server

Validate:

`rsyslogd -N1`

Restart:

`systemctl restart rsyslog`

Check status:

`systemctl status rsyslog`

Check listener:

`ss -ltnp | grep :514`

Review service errors:

`journalctl -u rsyslog -n 50`

---

# 💻 38. Configure a Client for TCP Forwarding

Create:

`vi /etc/rsyslog.d/90-central-forwarding.conf`

Add:

```rsyslog
action(
    type="omfwd"
    target="192.168.1.150"
    port="514"
    protocol="tcp"

    queue.type="LinkedList"
    queue.filename="central_fwd"
    queue.maxdiskspace="1g"
    queue.saveOnShutdown="on"

    action.resumeRetryCount="-1"
)
```

Replace the example IP with the real collector address.

---

# 🧠 39. Why Use an Action Queue?

A queue helps when the central server is temporarily unavailable.

It can:

* Buffer pending events
* Keep local processing separated from remote delivery
* Retry later
* Reduce message loss during outages

| Parameter | Purpose |
| --- | --- |
| `queue.type="LinkedList"` | Enables a linked-list queue |
| `queue.filename` | Adds disk-assisted persistence |
| `queue.maxdiskspace` | Limits disk use |
| `queue.saveOnShutdown="on"` | Saves queued messages during shutdown |
| `action.resumeRetryCount="-1"` | Keeps retrying |

Queue values should match expected volume and available disk capacity.

---

# ✅ 40. Validate and Test the Client

Validate:

`rsyslogd -N1`

Restart:

`systemctl restart rsyslog`

Check status:

`systemctl status rsyslog`

Generate a test:

`logger -t CENTRALTEST "TCP test from $(hostname) at $(date --iso-8601=seconds)"`

---

# 🔎 41. Verify on the Central Server

List remote files:

`find /var/log/remote -type f -ls`

Search:

`grep -R "TCP test" /var/log/remote`

Follow remote logs:

`tail -F /var/log/remote/*/*.log`

Expected path may resemble:

```text
/var/log/remote/client1/CENTRALTEST.log
```

---

# 📮 42. Legacy Forwarding Syntax

UDP:

```rsyslog
*.*    @192.168.1.150:514
```

TCP:

```rsyslog
*.*    @@192.168.1.150:514
```

Memory:

```text
@  = UDP
@@ = TCP
```

Modern `action(type="omfwd" ...)` syntax is clearer and supports queues cleanly.

---

# 📡 43. Configure UDP Receiving

Server configuration:

```rsyslog
module(load="imudp")
input(type="imudp" port="514")
```

Allow UDP:

`firewall-cmd --permanent --add-port=514/udp`

`firewall-cmd --reload`

Validate and restart:

`rsyslogd -N1`

`systemctl restart rsyslog`

Check:

`ss -lunp | grep :514`

---

# 📤 44. Configure UDP Forwarding

```rsyslog
action(
    type="omfwd"
    target="192.168.1.150"
    port="514"
    protocol="udp"
)
```

UDP is connectionless and does not provide the same delivery guarantees as TCP.

---

# 🧱 45. Use a Custom Port

Example server:

```rsyslog
module(load="imtcp")
input(type="imtcp" port="10514")
```

Example client:

```rsyslog
action(
    type="omfwd"
    target="192.168.1.150"
    port="10514"
    protocol="tcp"
    queue.type="LinkedList"
)
```

---

# 🛡️ 46. SELinux for a Custom Port

Install tools if needed:

`dnf install policycoreutils-python-utils -y`

Assign the port:

`semanage port -a -t syslogd_port_t -p tcp 10514`

If the port already exists under another type:

`semanage port -m -t syslogd_port_t -p tcp 10514`

Verify:

`semanage port -l | grep syslogd_port_t`

Allow the firewall port:

`firewall-cmd --permanent --add-port=10514/tcp`

`firewall-cmd --reload`

---

# 🔒 47. Why Plain TCP Is Not Enough

TCP improves delivery behavior, but plain TCP does not automatically provide:

* Encryption
* Server identity verification
* Client identity verification
* Protection from interception

Sensitive logs sent over untrusted networks should use TLS or another protected transport.

---

# 🔐 48. Syslog over TLS

TLS can provide:

* Encryption
* Integrity protection
* Certificate-based authentication
* Protection against passive monitoring
* Greater confidence in the collector’s identity

Common port:

```text
6514/tcp
```

A full deployment requires:

* Trusted CA
* Server certificate
* Private key
* Optional client certificates
* Correct permissions
* Correct stream-driver settings
* Firewall and SELinux rules
* Certificate-renewal planning

Never upload private keys to GitHub.

---

# 📬 49. What Is RELP?

**RELP** means **Reliable Event Logging Protocol**.

It is useful when:

* Message loss is not acceptable
* The receiver may temporarily fail
* Both sender and receiver support RELP

Install support on compatible RHEL-style systems:

`dnf install rsyslog-relp -y`

Example server:

```rsyslog
module(load="imrelp")
input(type="imrelp" port="20514")
```

Example client:

```rsyslog
module(load="omrelp")

action(
    type="omrelp"
    target="192.168.1.150"
    port="20514"
)
```

`20514` is an example port.

---

# 🧪 50. Test TCP Connectivity

Install Ncat if needed:

`dnf install nmap-ncat -y`

Test from the client:

`nc -vz 192.168.1.150 514`

This confirms that the TCP port is reachable.

It does not prove the full logging pipeline works.

Always send a `logger` test afterward.

---

# 📡 51. Capture Syslog Traffic

On the central server:

`tcpdump -nn -i any port 514`

Generate a client event:

`logger -t PACKETTEST "Packet capture test from $(hostname)"`

Interpretation:

* Packets arrive but no file appears → check rules, permissions, SELinux, and storage
* No packets arrive → check client forwarding, route, firewall, IP, and protocol

---

# 🧭 52. Filter Which Logs Are Forwarded

Forward all messages:

```rsyslog
*.*    action(
    type="omfwd"
    target="192.168.1.150"
    protocol="tcp"
    port="514"
    queue.type="LinkedList"
)
```

Forward authentication events:

```rsyslog
authpriv.*    action(
    type="omfwd"
    target="192.168.1.150"
    protocol="tcp"
    port="514"
    queue.type="LinkedList"
)
```

Forward errors and more severe events:

```rsyslog
*.err    action(
    type="omfwd"
    target="192.168.1.150"
    protocol="tcp"
    port="514"
    queue.type="LinkedList"
)
```

Filtering reduces traffic, but overly strict filters can remove useful investigation evidence.

---

# 🧪 53. Property-Based Filtering

Forward only `sshd` events:

```rsyslog
if $programname == "sshd" then {
    action(
        type="omfwd"
        target="192.168.1.150"
        port="514"
        protocol="tcp"
        queue.type="LinkedList"
    )
}
```

Store failed-password messages separately:

```rsyslog
if $msg contains "Failed password" then {
    action(
        type="omfile"
        file="/var/log/failed-passwords.log"
    )
}
```

Always test the actual message text and case sensitivity.

---

# 🏷️ 54. Use `local0`–`local7` for Applications

Custom applications can use local facilities.

Test:

`logger -p local0.info -t INVENTORY "Inventory sync completed"`

Rule:

```rsyslog
local0.*    /var/log/inventory.log
```

This keeps application messages separate from general system logs.

---

# 📄 55. Read Application Files with `imfile`

Some applications write directly to a text file.

Example:

```rsyslog
module(load="imfile")

input(
    type="imfile"
    File="/opt/myapp/logs/application.log"
    Tag="myapp"
    Facility="local1"
    Severity="info"
)
```

Forward the imported messages:

```rsyslog
local1.*    action(
    type="omfwd"
    target="192.168.1.150"
    port="514"
    protocol="tcp"
    queue.type="LinkedList"
)
```

rsyslog must have permission and an appropriate SELinux context to read the source file.

---

# 🗃️ 56. Organize Logs by Host and Program

Example layout:

```text
/var/log/remote/
├── client1/
│   ├── sshd.log
│   ├── sudo.log
│   └── systemd.log
├── client2/
│   ├── sshd.log
│   └── cron.log
└── web01/
    ├── nginx.log
    └── systemd.log
```

Benefits:

* Easier host-based searches
* Cleaner troubleshooting
* Simpler permissions
* Better retention management
* Faster incident exports

---

# 🧹 57. Log Rotation

Logs can grow until they fill the filesystem.

`logrotate` can:

* Rotate old files
* Compress older files
* Remove logs after a retention period
* Rotate based on size or time
* Run post-rotation actions

Check configuration:

`less /etc/logrotate.conf`

List service rules:

`ls -l /etc/logrotate.d/`

Debug the full configuration:

`logrotate -d /etc/logrotate.conf`

Do not force rotation in production without understanding its effects.

---

# 💽 58. Capacity Planning

A basic estimate:

```text
Daily storage =
Events per second
× Average message size
× 86,400 seconds
```

Also include:

* Filesystem overhead
* Compression
* Retention period
* Traffic bursts
* Duplicate events
* Backup copies
* Growth margin
* Indexing overhead when using a search platform

Questions to answer:

* How many clients?
* How many events per second?
* How long must logs be retained?
* What happens when storage reaches 100%?
* Are old logs archived?
* Who can delete logs?

---

# 🚨 59. Protect Against Log Flooding

A broken or compromised client may send huge volumes of logs.

Possible controls:

* Network restrictions
* Queue limits
* Disk quotas
* Dedicated filesystem
* Monitoring and alerts
* Per-host rules
* Client authentication
* Filtering unwanted debug events
* Capacity planning

Do not allow one client to fill the root filesystem.

---

# 🔍 60. Search Central Logs

Search text:

`grep -R "Failed password" /var/log/remote`

Search one host:

`grep -R "error" /var/log/remote/client1`

Ignore case:

`grep -Ri "critical" /var/log/remote`

Follow one program:

`tail -f /var/log/remote/client1/sshd.log`

Search compressed rotated logs:

`zgrep "Failed password" /var/log/remote/client1/*.gz`

For very large environments, use an indexed search platform rather than only `grep`.

---

# 📊 61. Useful Log Fields

Important fields include:

* Timestamp
* Hostname
* Source IP
* Facility
* Severity
* Program name
* Process ID
* Message
* Message ID
* Structured data
* Original sender
* Transport protocol

Consistent fields improve search and correlation.

---

# 🧾 62. Traditional and Structured Syslog Formats

Two commonly discussed formats are:

* RFC 3164-style traditional syslog
* RFC 5424 structured syslog

RFC 5424 supports explicit fields such as:

* Version
* Timestamp
* Hostname
* Application name
* Process ID
* Message ID
* Structured data

Device and application support varies.

---

# 🛡️ 63. Security Best Practices

A strong central logging environment should:

* Prefer TCP with TLS or RELP when appropriate
* Restrict collector ports to approved networks
* Keep SELinux enforcing
* Keep `firewalld` enabled
* Protect log files from unauthorized users
* Synchronize system time
* Monitor disk space
* Rotate and archive logs
* Back up critical events
* Authenticate sources where possible
* Avoid exposing the collector publicly
* Apply security updates
* Document retention requirements
* Test recovery procedures

---

# 🔥 64. Restrict Firewall Access by Source

Example trusted subnet:

```text
192.168.1.0/24
```

Allow only that subnet:

`firewall-cmd --permanent --add-rich-rule='rule family="ipv4" source address="192.168.1.0/24" port port="514" protocol="tcp" accept'`

Reload:

`firewall-cmd --reload`

Review:

`firewall-cmd --list-rich-rules`

Use the real trusted subnet for your environment.

---

# 🚫 65. Common Configuration Mistakes

* Editing `/etc/syslog.conf` instead of `/etc/rsyslog.conf`
* Forgetting `rsyslogd -N1`
* Using UDP while expecting guaranteed delivery
* Opening the wrong firewall protocol
* Client uses TCP while server listens only on UDP
* Wrong server IP or hostname
* No action queue for TCP forwarding
* Disabling SELinux instead of configuring it
* Ignoring time synchronization
* Filling the root filesystem
* Forgetting log rotation
* Sending sensitive logs without encryption
* Assuming a collector automatically provides SIEM analysis
* Creating a forwarding loop
* Using duplicate matching rules

---

# ❌ 66. rsyslog Will Not Start

Check status:

`systemctl status rsyslog`

Validate:

`rsyslogd -N1`

Review journal:

`journalctl -u rsyslog -n 100`

Common causes:

* Syntax error
* Unknown module
* Invalid parameter
* Duplicate configuration
* Permission problem
* Wrong path
* Port already in use

---

# 🚧 67. Port 514 Is Not Listening

TCP check:

`ss -ltnp | grep :514`

UDP check:

`ss -lunp | grep :514`

Search configuration:

`grep -R 'imtcp\|imudp\|port="514"' /etc/rsyslog.conf /etc/rsyslog.d`

Validate:

`rsyslogd -N1`

Restart:

`systemctl restart rsyslog`

Remember:

```text
imtcp = TCP listener
imudp = UDP listener
```

---

# 📭 68. Client Logs Do Not Reach the Server

On the client:

`systemctl status rsyslog`

`rsyslogd -N1`

`grep -R "omfwd\|@@" /etc/rsyslog.conf /etc/rsyslog.d`

`nc -vz 192.168.1.150 514`

`logger -t FORWARDTEST "Forwarding test from $(hostname)"`

On the server:

`ss -ltnp | grep :514`

`firewall-cmd --list-all`

`tcpdump -nn -i any port 514`

`journalctl -u rsyslog -n 100`

`grep -R "Forwarding test" /var/log/remote`

---

# 🧩 69. Packets Arrive but No File Is Written

Possible causes:

* Input bound to the wrong ruleset
* Ruleset has no file action
* Dynamic template is incorrect
* Directory permissions
* SELinux denial
* Filesystem full
* Inodes exhausted
* Invalid hostname or program property

Check disk space:

`df -h`

Check inodes:

`df -i`

Check SELinux:

`ausearch -m AVC -ts recent`

Check service errors:

`journalctl -u rsyslog -n 100`

---

# 💾 70. Queue Is Growing

A growing queue usually means the destination is unavailable or too slow.

Check:

* Collector availability
* Network latency
* Firewall
* DNS
* Disk space
* Collector performance
* Message volume
* Retry configuration

Do not delete queue files while rsyslog is running.

First determine why delivery stopped and whether messages must be preserved.

---

# 🌐 71. Hostnames Are Incorrect

Possible causes:

* Wrong client hostname
* DNS behavior
* NAT
* Device sends an unexpected hostname
* Template uses the wrong property
* A relay replaces sender information

Check:

`hostnamectl`

`getent hosts client1.lab.local`

Inspect raw traffic when necessary:

`tcpdump -A -nn -i any port 514`

---

# 🕵️ 72. Duplicate Messages

Possible causes:

* Same event enters through multiple inputs
* Multiple forwarding rules match
* Journal and socket inputs duplicate a source
* A relay sends messages back to the sender
* Logging topology contains a loop
* Duplicate snippets exist

Search:

`grep -R "omfwd\|imjournal\|imuxsock" /etc/rsyslog.conf /etc/rsyslog.d`

Design the forwarding path to prevent loops.

---

# 🧪 73. Complete TCP Central Logging Lab

## Step 1: Verify both systems

`hostnamectl`

`ip a`

---

## Step 2: Install rsyslog

`dnf install rsyslog -y`

---

## Step 3: Enable the service

`systemctl enable --now rsyslog`

---

## Step 4: Create the server input

`vi /etc/rsyslog.d/10-central-server.conf`

---

## Step 5: Allow TCP 514

`firewall-cmd --permanent --add-port=514/tcp`

`firewall-cmd --reload`

---

## Step 6: Validate the server

`rsyslogd -N1`

---

## Step 7: Restart the server

`systemctl restart rsyslog`

---

## Step 8: Verify the listener

`ss -ltnp | grep :514`

---

## Step 9: Configure client forwarding

`vi /etc/rsyslog.d/90-central-forwarding.conf`

---

## Step 10: Validate the client

`rsyslogd -N1`

---

## Step 11: Restart the client

`systemctl restart rsyslog`

---

## Step 12: Send a test

`logger -t CENTRALTEST "Central logging works from $(hostname)"`

---

## Step 13: Verify on the server

`grep -R "Central logging works" /var/log/remote`

---

# 🧪 74. Failure-Recovery Queue Lab

1. Confirm forwarding works.
2. Stop rsyslog on the collector:

`systemctl stop rsyslog`

3. Generate test events on the client:

`for i in {1..10}; do logger -t QUEUETEST "Queued message $i"; done`

4. Start the collector:

`systemctl start rsyslog`

5. Follow the client journal:

`journalctl -u rsyslog -f`

6. Search centrally:

`grep -R "Queued message" /var/log/remote`

This lab demonstrates how an action queue handles a temporary outage.

---

# 🧪 75. Multi-Client Practical Example

Client 1:

`logger -p local0.notice -t WEBAPP "Checkout service started"`

Client 2:

`logger -p local0.err -t DATABASE "Database connection failed"`

Client 3:

`logger -p authpriv.warning -t SECURITY "Repeated authentication failures"`

Central searches:

`grep -R "WEBAPP" /var/log/remote`

`grep -R "DATABASE" /var/log/remote`

`grep -R "SECURITY" /var/log/remote`

---

# 🧠 76. Memory Framework

```text
Input    = Where messages come from
Filter   = Which messages match
Action   = Where messages go
Queue    = What happens during delay or failure
Template = How messages or paths are formatted
Ruleset  = A named processing pipeline
```

Pipeline:

> **Generate → Collect → Filter → Queue → Forward → Receive → Store → Search**

Administrator workflow:

> **Install → Configure → Validate → Allow → Restart → Test → Verify → Monitor**

---

# 📋 77. Command Cheat Sheet

| Task | Command |
| --- | --- |
| Check package | `rpm -q rsyslog` |
| Install | `dnf install rsyslog -y` |
| Show version | `rsyslogd -v` |
| Main configuration | `vi /etc/rsyslog.conf` |
| Additional configuration | `vi /etc/rsyslog.d/file.conf` |
| Validate | `rsyslogd -N1` |
| Start | `systemctl start rsyslog` |
| Enable | `systemctl enable rsyslog` |
| Start and enable | `systemctl enable --now rsyslog` |
| Restart | `systemctl restart rsyslog` |
| Reload | `systemctl reload rsyslog` |
| Status | `systemctl status rsyslog` |
| Generate test event | `logger -t TEST "Message"` |
| Set facility/severity | `logger -p local0.notice "Message"` |
| View journal | `journalctl` |
| Follow service journal | `journalctl -u rsyslog -f` |
| Check TCP 514 | `ss -ltnp \| grep :514` |
| Check UDP 514 | `ss -lunp \| grep :514` |
| Allow TCP 514 | `firewall-cmd --permanent --add-port=514/tcp` |
| Allow UDP 514 | `firewall-cmd --permanent --add-port=514/udp` |
| Reload firewall | `firewall-cmd --reload` |
| Test TCP | `nc -vz SERVER_IP 514` |
| Capture traffic | `tcpdump -nn -i any port 514` |
| Search remote logs | `grep -R "text" /var/log/remote` |
| Follow remote logs | `tail -F /var/log/remote/*/*.log` |
| Add SELinux port | `semanage port -a -t syslogd_port_t -p tcp PORT` |
| Check disk | `df -h` |
| Check inodes | `df -i` |

---

# 💼 78. Questions

## Q1. What is centralized logging?

It collects logs from multiple systems in one central location.

---

## Q2. What is rsyslog?

A high-performance logging system that receives, filters, stores, transforms, and forwards events.

---

## Q3. What are the package, service, and daemon names?

```text
Package = rsyslog
Service = rsyslog
Daemon  = rsyslogd
```

---

## Q4. What is the main configuration file?

`/etc/rsyslog.conf`

---

## Q5. Where are additional snippets stored?

`/etc/rsyslog.d/*.conf`

---

## Q6. How do you validate configuration?

`rsyslogd -N1`

---

## Q7. How do you generate a test event?

`logger "Test message"`

---

## Q8. What is a facility?

A category identifying the message source or subsystem.

---

## Q9. What is a severity?

A level identifying the importance or urgency of a message.

---

## Q10. Name the severity levels.

`emerg`, `alert`, `crit`, `err`, `warning`, `notice`, `info`, and `debug`.

---

## Q11. What is the traditional syslog port?

Port `514`.

---

## Q12. What is the difference between UDP and TCP?

UDP is connectionless and may lose events. TCP is connection-oriented and supports queued forwarding.

---

## Q13. What is syslog over TLS?

Syslog transferred through a TLS-protected connection for encryption and authentication.

---

## Q14. Which port is commonly used for TLS syslog?

TCP port `6514`.

---

## Q15. What is RELP?

Reliable Event Logging Protocol, designed for reliable event delivery.

---

## Q16. What does `imtcp` do?

It receives syslog messages through TCP.

---

## Q17. What does `imudp` do?

It receives syslog messages through UDP.

---

## Q18. What does `omfwd` do?

It forwards messages to remote systems through UDP, TCP, or TLS-capable configurations.

---

## Q19. What is an action queue?

A buffer attached to an output action that holds events when a destination is slow or unavailable.

---

## Q20. Why use a linked-list queue?

It separates forwarding from local processing and can buffer messages during outages.

---

## Q21. What is a template?

A definition controlling message formatting or dynamic file paths.

---

## Q22. What is a ruleset?

A named logging-processing pipeline containing filters and actions.

---

## Q23. What does one `@` mean in legacy syntax?

UDP forwarding.

---

## Q24. What do two `@@` symbols mean?

TCP forwarding.

---

## Q25. Why is time synchronization important?

It allows events from multiple systems to be correlated in the correct order.

---

## Q26. How do you configure a custom port with SELinux?

Assign the port the `syslogd_port_t` type using `semanage port`.

---

## Q27. What should you check if packets arrive but no file appears?

Check rulesets, templates, permissions, SELinux, disk space, and service errors.

---

## Q28. Does rsyslog automatically provide dashboards?

No. Advanced dashboards and analytics require another platform.

---

# 📌 79. Ultra-Short Revision

* Central logger = One location for logs from many systems
* Package = `rsyslog`
* Service = `rsyslog`
* Daemon = `rsyslogd`
* Main configuration = `/etc/rsyslog.conf`
* Snippets = `/etc/rsyslog.d/*.conf`
* Validate = `rsyslogd -N1`
* Test event = `logger`
* Local files = Usually `/var/log/`
* Journal tool = `journalctl`
* TCP input = `imtcp`
* UDP input = `imudp`
* Forwarding = `omfwd`
* Reliable protocol = RELP
* Traditional port = `514`
* Common TLS port = `6514`
* Legacy UDP = `@server`
* Legacy TCP = `@@server`
* TCP forwarding should use an action queue
* Custom SELinux ports use `syslogd_port_t`
* Keep `firewalld` enabled
* Keep SELinux enforcing
* Synchronize time
* Rotate logs
* Monitor disk use
* Encrypt sensitive remote logging traffic

---

# 📚 80. Official References

* Red Hat Enterprise Linux 9 — Configuring a remote logging solution: `https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/security_hardening/assembly_configuring-a-remote-logging-solution_security-hardening`
* Red Hat Enterprise Linux 9 — Using the logging system role: `https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/security_hardening/assembly_using-the-logging-system-role_security-hardening`
* rsyslog documentation: `https://docs.rsyslog.com/`
* Forwarding guide: `https://docs.rsyslog.com/doc/getting_started/forwarding_logs.html`
* `omfwd` module: `https://docs.rsyslog.com/doc/configuration/modules/omfwd.html`
* Queue concepts: `https://docs.rsyslog.com/doc/concepts/queues.html`
* TCP input module: `https://docs.rsyslog.com/doc/configuration/modules/imtcp.html`

---

# 🏆 81. Takeaway

A beginner knows that rsyslog writes messages under `/var/log`.

A strong Linux administrator understands:

* The relationship between `systemd-journald` and rsyslog
* The package, service, and daemon names
* Facilities and severities
* Inputs, filters, actions, templates, queues, and rulesets
* Why TCP is more reliable than UDP
* Why TLS protects sensitive logs
* Why RELP is useful when loss is unacceptable
* How to build a central TCP collector
* How to forward using `omfwd`
* Why forwarding actions should use queues
* How to organize logs by host and program
* How to validate before restarting
* How to test using `logger`
* How to troubleshoot with sockets, packet capture, journals, and files
* How to configure `firewalld` and SELinux instead of disabling them
* Why time synchronization, rotation, retention, and disk monitoring matter
* Why central collection is different from full SIEM analysis

Centralized logging is not simply moving text from one server to another. It is an operational and security pipeline that must collect events reliably, preserve useful context, protect sensitive information, survive outages, control storage growth, and help administrators understand what happened throughout an environment.

---

✍️ Notes By Abhishek (Ez Abyss)
