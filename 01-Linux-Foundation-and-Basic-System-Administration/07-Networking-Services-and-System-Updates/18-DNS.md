# 🌐 DNS (Domain Name System)

---

## 🎯 1. What is DNS?

**DNS (Domain Name System)** is a network service that translates human-readable domain names into IP addresses.

Example:

`www.google.com`

becomes an IP address such as:

`142.250.x.x`

> **Simple understanding:** DNS is the internet’s contact list.

Humans remember names, but computers communicate using IP addresses.

---

## 🌍 Real-World Example: Phone Contacts

You probably do not memorize every friend’s phone number.

Instead, you save:

```text
Ram → 98XXXXXXXX
```

When you tap Ram’s name, your phone finds the number automatically.

DNS works similarly:

```text
server1.lab.local → 192.168.1.240
```

---

## 🧠 2. Why Do We Need DNS?

Without DNS, users would need to remember IP addresses for every website and server.

Instead of entering:

`142.250.x.x`

you can enter:

`www.google.com`

DNS improves:

* Usability
* Network administration
* Service accessibility
* Scalability
* Centralized name management

---

## 🔄 3. Main DNS Functions

DNS can perform several types of resolution.

### Forward Lookup

Translates a hostname into an IP address.

```text
clienta.lab.local → 192.168.1.240
```

This normally uses an **A record** for IPv4.

---

### Reverse Lookup

Translates an IP address into a hostname.

```text
192.168.1.240 → clienta.lab.local
```

This uses a **PTR record**.

---

### Alias Lookup

Maps one hostname to another hostname.

```text
www.lab.local → webserver01.lab.local
```

This uses a **CNAME record**.

---

## 📋 4. Important DNS Record Types

| Record  | Purpose                  | Example                  |
| ------- | ------------------------ | ------------------------ |
| `A`     | Hostname to IPv4 address | `server1 → 192.168.1.10` |
| `AAAA`  | Hostname to IPv6 address | `server1 → 2001:db8::10` |
| `PTR`   | IP address to hostname   | `192.168.1.10 → server1` |
| `CNAME` | Hostname alias           | `www → webserver1`       |
| `NS`    | Identifies DNS server    | `ns1.lab.local`          |
| `MX`    | Identifies mail server   | `mail.lab.local`         |
| `SOA`   | Defines zone authority   | Primary zone information |

---

## 🧠 Memory Trick

```text
A     = Address
PTR   = Pointer back to name
CNAME = Canonical alias
NS    = Name Server
MX    = Mail Exchange
```

---

# 🏗️ 5. DNS Components in RHEL/CentOS

DNS has three important names that beginners often confuse.

| Term    | Meaning                            |
| ------- | ---------------------------------- |
| DNS     | The overall name-resolution system |
| BIND    | The DNS software package           |
| `named` | The DNS server daemon/service      |

> **BIND** stands for Berkeley Internet Name Domain.

---

## Important Package Names

`bind`

Main DNS server package.

`bind-utils`

Provides troubleshooting tools such as:

* `dig`
* `nslookup`
* `host`

---

## Important Service

`named`

This daemon listens for DNS requests.

---

## Default Port

DNS uses:

`53`

DNS normally uses both:

* UDP port 53 for most queries
* TCP port 53 for large responses and zone transfers

---

# 🗂️ 6. Important DNS Files and Directories

| Location                                  | Purpose                            |
| ----------------------------------------- | ---------------------------------- |
| `/etc/named.conf`                         | Main BIND configuration file       |
| `/var/named/`                             | DNS zone files                     |
| `/etc/resolv.conf`                        | Client DNS resolver configuration  |
| `/etc/yum.repos.d/`                       | Repository configuration, not DNS  |
| `/etc/NetworkManager/system-connections/` | NetworkManager connection profiles |

---

# 🖥️ 7. DNS Server Architecture

A typical DNS environment may include:

```text
Primary DNS Server
        ↓
Secondary DNS Server
        ↓
DNS Clients
```

---

## Primary DNS Server

The main server that stores and manages DNS records.

It was traditionally called the **master server**.

---

## Secondary DNS Server

Maintains a copy of the primary DNS zones.

It was traditionally called the **slave server**.

Benefits:

* Redundancy
* Availability
* Backup name resolution
* Load sharing

---

## DNS Client

A machine that sends DNS queries.

Example:

```text
Client asks:
What is the IP address of server1.lab.local?
```

The DNS server replies with the matching IP address.

---

# 🧪 8. Lab Design

Example lab domain:

`lab.local`

Example DNS server:

```text
Hostname: masterdns.lab.local
IP:       192.168.1.153
```

Example clients:

```text
clienta.lab.local → 192.168.1.240
clientb.lab.local → 192.168.1.241
```

> Use your machine’s actual IP address. Do not copy the example IP blindly.

---

# ⚠️ 9. Static IP Requirement

A DNS server should normally use a **static IP address**.

If its IP changes, clients may no longer be able to reach it.

A dynamically assigned DHCP address is acceptable for temporary lab practice, but not ideal for production.

---

## 🌍 Real-World Example

A DNS server with a changing IP address is like a police station that changes its phone number every day.

People would not know where to contact it.

---

# 🛡️ 10. Before Starting

If you are using a virtual machine, create a snapshot before editing DNS configuration.

Why?

* DNS configuration is sensitive
* A syntax error may stop the service
* Wrong resolver settings may interrupt internet access
* Snapshot allows quick recovery

> Snapshot = save point for your virtual machine.

---

# 🔍 11. Check Current System Information

Become root:

`su -`

Confirm user:

`whoami`

Check hostname:

`hostname`

Check IP addresses:

`ip a`

Check the active interface:

`ip addr show enp0s3`

Your interface name may be different, such as:

* `enp0s3`
* `ens33`
* `eth0`

---

# 🌐 12. Check Internet Connectivity

Before installing packages:

`ping www.google.com`

Stop the command with:

`Ctrl+C`

A safer short test is:

`ping -c 4 www.google.com`

If replies return, the machine has network and DNS connectivity.

---

# 📦 13. Check Whether BIND Is Installed

`rpm -qa | grep bind`

This searches installed RPM packages for names containing `bind`.

---

# 📥 14. Install DNS Packages

`dnf install bind bind-utils -y`

Meaning:

* `bind` installs the DNS server
* `bind-utils` installs DNS query tools
* `-y` automatically answers yes

---

## Verify Installation

`rpm -qa | grep bind`

---

# 💾 15. Back Up the Main Configuration

Before editing:

`cp /etc/named.conf /etc/named.conf.backup`

Verify:

`ls -l /etc/named.conf*`

---

# ⚙️ 16. Configure `/etc/named.conf`

Open the file:

`vi /etc/named.conf`

The main configuration controls:

* Which IP addresses BIND listens on
* Which clients may query it
* Which zones the server manages
* DNS security options

---

## Listen on Port 53

Example:

```conf
listen-on port 53 { 127.0.0.1; 192.168.1.153; };
```

This tells BIND to listen on:

* Local loopback
* Server’s network IP

---

## Allow DNS Queries

For a simple isolated lab:

```conf
allow-query { localhost; 192.168.1.0/24; };
```

This permits DNS queries from the local subnet.

Avoid using overly broad access rules in production unless required.

---

# 🧭 17. Define a Forward Zone

Add a zone block:

```conf
zone "lab.local" IN {
    type master;
    file "forward.lab";
    allow-update { none; };
};
```

Meaning:

* `zone "lab.local"` defines the domain
* `type master` means this server owns the zone
* `file "forward.lab"` identifies the zone file
* `allow-update { none; };` blocks dynamic updates

---

# 🔁 18. Define a Reverse Zone

For the network:

```text
192.168.1.0/24
```

The reverse zone is:

```text
1.168.192.in-addr.arpa
```

Configuration:

```conf
zone "1.168.192.in-addr.arpa" IN {
    type master;
    file "reverse.lab";
    allow-update { none; };
};
```

> Reverse zone numbers are written in reverse order.

---

## Example

Network:

```text
10.20.30.0/24
```

Reverse zone:

```text
30.20.10.in-addr.arpa
```

---

# 📂 19. Create Zone Files

Move to the zone directory:

`cd /var/named`

Create forward zone file:

`touch forward.lab`

Create reverse zone file:

`touch reverse.lab`

Verify:

`ls -l forward.lab reverse.lab`

---

# ➡️ 20. Forward Zone File

Edit:

`vi /var/named/forward.lab`

Example:

```dns
$TTL 86400

@   IN  SOA masterdns.lab.local. admin.lab.local. (
        2026071401
        3600
        1800
        604800
        86400
)

@           IN  NS      masterdns.lab.local.

masterdns   IN  A       192.168.1.153
clienta     IN  A       192.168.1.240
clientb     IN  A       192.168.1.241
```

---

# 🧠 21. Understanding the Forward Zone

## `$TTL`

```dns
$TTL 86400
```

TTL means **Time To Live**.

It controls how long DNS information may be cached.

`86400` seconds equals 24 hours.

---

## `SOA`

```dns
@ IN SOA masterdns.lab.local. admin.lab.local.
```

SOA means **Start of Authority**.

It identifies important zone information, including:

* Primary DNS server
* Administrative contact
* Serial number
* Refresh timing
* Retry timing
* Expiration timing

---

## Administrator Email Format

This:

```dns
admin.lab.local.
```

represents an email similar to:

```text
admin@lab.local
```

The first dot replaces the `@` symbol in SOA syntax.

---

## Serial Number

Example:

```text
2026071401
```

A common format is:

```text
YYYYMMDDNN
```

Where:

* `YYYY` = year
* `MM` = month
* `DD` = day
* `NN` = change number

Increase the serial every time you edit the zone.

Example:

```text
2026071401
2026071402
2026071403
```

---

## `NS` Record

```dns
@ IN NS masterdns.lab.local.
```

Identifies the authoritative name server for the zone.

---

## `A` Records

```dns
clienta IN A 192.168.1.240
```

Maps hostname to IPv4 address.

---

# ⬅️ 22. Reverse Zone File

Edit:

`vi /var/named/reverse.lab`

Example:

```dns
$TTL 86400

@   IN  SOA masterdns.lab.local. admin.lab.local. (
        2026071401
        3600
        1800
        604800
        86400
)

@       IN  NS      masterdns.lab.local.

153     IN  PTR     masterdns.lab.local.
240     IN  PTR     clienta.lab.local.
241     IN  PTR     clientb.lab.local.
```

---

# 🧠 23. Understanding PTR Entries

For this IP:

```text
192.168.1.240
```

The PTR entry uses only the host portion:

```dns
240 IN PTR clienta.lab.local.
```

The network portion is already defined in:

```text
1.168.192.in-addr.arpa
```

---

# ✍️ 24. Importance of the Final Dot

Fully qualified domain names in zone files normally end with a dot.

Correct:

```dns
masterdns.lab.local.
```

Potentially incorrect:

```dns
masterdns.lab.local
```

Without the final dot, BIND may append the current zone name.

That could produce:

```text
masterdns.lab.local.lab.local
```

---

# 🔐 25. Set Permissions and Ownership

Set owner:

`chown root:named /var/named/forward.lab`

`chown root:named /var/named/reverse.lab`

Set permissions:

`chmod 640 /var/named/forward.lab`

`chmod 640 /var/named/reverse.lab`

---

## Restore SELinux Context

`restorecon -v /var/named/forward.lab`

`restorecon -v /var/named/reverse.lab`

SELinux context matters because BIND may be blocked from reading incorrectly labeled files.

---

# ✅ 26. Validate the Main Configuration

`named-checkconf /etc/named.conf`

If there is no output, the syntax is usually valid.

> In Linux administration, no output often means success.

---

# ✅ 27. Validate the Forward Zone

`named-checkzone lab.local /var/named/forward.lab`

Expected result:

```text
zone lab.local/IN: loaded serial 2026071401
OK
```

---

# ✅ 28. Validate the Reverse Zone

`named-checkzone 1.168.192.in-addr.arpa /var/named/reverse.lab`

Expected result:

```text
zone 1.168.192.in-addr.arpa/IN: loaded serial 2026071401
OK
```

---

# ▶️ 29. Start and Enable DNS

Start BIND:

`systemctl start named`

Enable at boot:

`systemctl enable named`

Check status:

`systemctl status named`

Look for:

```text
Active: active (running)
```

---

## Restart After Configuration Changes

`systemctl restart named`

---

## Reload Without Full Restart

`rndc reload`

or:

`systemctl reload named`

Reloading is less disruptive than restarting.

---

# 🔥 30. Configure the Firewall

Do not normally disable the firewall in production.

Allow DNS traffic:

`firewall-cmd --permanent --add-service=dns`

Reload firewall:

`firewall-cmd --reload`

Verify:

`firewall-cmd --list-services`

DNS requires both UDP and TCP port 53, and the predefined DNS service handles both.

---

# 🧪 31. Verify Port 53

`ss -tulpn | grep :53`

This checks whether a process is listening on DNS port 53.

---

# 🖥️ 32. Configure the DNS Client

A client must know which DNS server to query.

Example DNS server:

```text
192.168.1.153
```

---

## Temporary Resolver Configuration

Edit:

`vi /etc/resolv.conf`

Add:

```conf
nameserver 192.168.1.153
```

However, NetworkManager may overwrite this file.

---

# ⚙️ 33. Persistent DNS Configuration with NetworkManager

List connections:

`nmcli connection show`

Set DNS on a connection:

`nmcli connection modify "System enp0s3" ipv4.dns "192.168.1.153"`

Ignore automatic DNS if required:

`nmcli connection modify "System enp0s3" ipv4.ignore-auto-dns yes`

Activate changes:

`nmcli connection up "System enp0s3"`

Use your actual connection name from:

`nmcli connection show`

---

# 🔍 34. Test DNS with `dig`

Forward lookup:

`dig masterdns.lab.local`

Test client A:

`dig clienta.lab.local`

Test client B:

`dig clientb.lab.local`

---

## Query a Specific DNS Server

`dig @192.168.1.153 clienta.lab.local`

This is useful when your system has multiple DNS servers.

---

# 🔍 35. Test DNS with `nslookup`

`nslookup masterdns.lab.local`

`nslookup clienta.lab.local`

`nslookup clientb.lab.local`

---

# 🔁 36. Test Reverse DNS

Using `dig`:

`dig -x 192.168.1.240`

Using `nslookup`:

`nslookup 192.168.1.240`

Expected hostname:

```text
clienta.lab.local
```

---

# 🆚 37. `dig` vs `nslookup`

| Tool       | Purpose                      |
| ---------- | ---------------------------- |
| `dig`      | Detailed DNS troubleshooting |
| `nslookup` | Simple DNS lookup            |
| `host`     | Quick and readable lookup    |

Examples:

`host clienta.lab.local`

`host 192.168.1.240`

---

# ➕ 38. Add a New DNS Record

Suppose you add:

```text
clientc.lab.local → 192.168.1.242
```

Edit forward zone:

`vi /var/named/forward.lab`

Add:

```dns
clientc IN A 192.168.1.242
```

Increase the serial number.

---

## Add Reverse Record

Edit:

`vi /var/named/reverse.lab`

Add:

```dns
242 IN PTR clientc.lab.local.
```

Increase the serial number.

---

## Validate Changes

`named-checkzone lab.local /var/named/forward.lab`

`named-checkzone 1.168.192.in-addr.arpa /var/named/reverse.lab`

---

## Reload DNS

`rndc reload`

---

## Test

`dig clientc.lab.local`

`dig -x 192.168.1.242`

---

# 🧭 39. Complete DNS Query Workflow

```text
User enters clienta.lab.local
              ↓
Client checks resolver settings
              ↓
Query sent to DNS server on port 53
              ↓
DNS server searches forward zone
              ↓
A record found
              ↓
192.168.1.240 returned
```

---

# 🌍 40. Real-World Enterprise Example

A company may have:

```text
payroll.company.local
database.company.local
mail.company.local
intranet.company.local
```

Employees use names instead of remembering IP addresses.

If the payroll server’s IP changes, administrators update DNS once.

Users continue using:

```text
payroll.company.local
```

They do not need to learn the new IP address.

---

# 🚨 41. Common DNS Problems

| Problem                             | Likely Cause                            | Fix                           |
| ----------------------------------- | --------------------------------------- | ----------------------------- |
| `named` fails to start              | Syntax error                            | Run `named-checkconf`         |
| Zone does not load                  | Zone file error                         | Run `named-checkzone`         |
| Query times out                     | Firewall or service issue               | Check port 53 and `named`     |
| Forward lookup works, reverse fails | PTR zone missing                        | Check reverse zone            |
| Old answer returned                 | DNS cache or serial not updated         | Increase serial and reload    |
| Internet stops working              | Wrong resolver setting                  | Correct DNS in NetworkManager |
| Permission denied                   | Wrong file ownership or SELinux context | Use `chown` and `restorecon`  |
| `dig` not found                     | `bind-utils` missing                    | Install `bind-utils`          |

---

# 🧰 42. Troubleshooting Checklist

Check service:

`systemctl status named`

Check logs:

`journalctl -u named`

Check main configuration:

`named-checkconf /etc/named.conf`

Check forward zone:

`named-checkzone lab.local /var/named/forward.lab`

Check reverse zone:

`named-checkzone 1.168.192.in-addr.arpa /var/named/reverse.lab`

Check listening port:

`ss -tulpn | grep :53`

Check firewall:

`firewall-cmd --list-services`

Check resolver:

`cat /etc/resolv.conf`

Test server directly:

`dig @192.168.1.153 clienta.lab.local`

---

# 🧠 43. Memory Framework

Remember:

```text
Install
Configure
Create zones
Validate
Start
Allow firewall
Configure client
Test
```

Short form:

> **I-C-C-V-S-A-C-T**

---

# 📋 44. Command Cheat Sheet

| Task               | Command                                                         |
| ------------------ | --------------------------------------------------------------- |
| Check IP           | `ip a`                                                          |
| Install BIND       | `dnf install bind bind-utils -y`                                |
| Check packages     | `rpm -qa \| grep bind`                                          |
| Edit main config   | `vi /etc/named.conf`                                            |
| Zone directory     | `cd /var/named`                                                 |
| Check main config  | `named-checkconf /etc/named.conf`                               |
| Check forward zone | `named-checkzone lab.local /var/named/forward.lab`              |
| Check reverse zone | `named-checkzone 1.168.192.in-addr.arpa /var/named/reverse.lab` |
| Start DNS          | `systemctl start named`                                         |
| Enable DNS         | `systemctl enable named`                                        |
| Restart DNS        | `systemctl restart named`                                       |
| Reload DNS         | `rndc reload`                                                   |
| Check status       | `systemctl status named`                                        |
| Allow firewall     | `firewall-cmd --permanent --add-service=dns`                    |
| Reload firewall    | `firewall-cmd --reload`                                         |
| Forward lookup     | `dig clienta.lab.local`                                         |
| Reverse lookup     | `dig -x 192.168.1.240`                                          |
| Simple lookup      | `nslookup clienta.lab.local`                                    |

---

# 💼 45. Questions

## Q1. What is DNS?

DNS translates domain names and hostnames into IP addresses and can also perform reverse lookups.

---

## Q2. What port does DNS use?

Port `53`, using both UDP and TCP.

---

## Q3. What is an A record?

It maps a hostname to an IPv4 address.

---

## Q4. What is a PTR record?

It maps an IP address back to a hostname.

---

## Q5. What is a CNAME record?

It maps one hostname or alias to another hostname.

---

## Q6. What package provides DNS on RHEL?

`bind`

---

## Q7. What is the DNS service called?

`named`

---

## Q8. Where is the main BIND configuration file?

`/etc/named.conf`

---

## Q9. Where are zone files stored?

Usually under:

`/var/named/`

---

## Q10. How do you validate BIND configuration?

`named-checkconf /etc/named.conf`

---

## Q11. How do you validate a zone file?

`named-checkzone zone-name zone-file`

---

## Q12. Why must the zone serial number be increased?

Secondary servers and DNS processes use it to identify that the zone has changed.

---

## Q13. Why should DNS servers use static IP addresses?

Clients must always be able to find the DNS server at the same address.

---

## Q14. What is the difference between forward and reverse DNS?

Forward DNS maps hostname to IP.

Reverse DNS maps IP to hostname.

---

## Q15. What is the difference between BIND and `named`?

BIND is the DNS software package, while `named` is its running daemon.

---

# 📌 46. Ultra-Short Revision

* DNS = Domain Name System
* Purpose = Translate names and IP addresses
* `A` = Hostname to IPv4
* `PTR` = IP to hostname
* `CNAME` = Hostname alias
* Package = `bind`
* Tools = `bind-utils`
* Service = `named`
* Port = `53`
* Main config = `/etc/named.conf`
* Zone files = `/var/named/`
* Client resolver = `/etc/resolv.conf`
* Test forward = `dig hostname`
* Test reverse = `dig -x IP`
* Validate config = `named-checkconf`
* Validate zone = `named-checkzone`

---

# 🏆 Takeaway

A beginner memorizes that DNS converts names into IP addresses.

A strong Linux administrator understands:

* Forward and reverse resolution
* DNS record types
* BIND packages and services
* Forward and reverse zone files
* Serial number management
* Firewall and SELinux requirements
* Persistent client configuration
* Testing and troubleshooting with `dig`

DNS is one of the most important services in networking. If DNS fails, servers may still be running, but users and applications may not be able to find them.

---

# ✍️ Notes By Abhishek (Ez Abyss)
