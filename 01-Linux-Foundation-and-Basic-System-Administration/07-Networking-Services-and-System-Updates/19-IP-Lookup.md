# 🔎 Hostname and IP Address Lookup

---

## 🎯 1. What is Hostname and IP Address Lookup?

Hostname and IP address lookup is the process of finding:

* The IP address connected to a hostname
* The hostname connected to an IP address
* DNS records associated with a domain

Examples:

```text
www.google.com → IP address
```

```text
192.168.1.20 → server1.lab.local
```

DNS performs this translation.

> **Simple understanding:** Lookup tools let you ask DNS, “What IP belongs to this name?” or “What name belongs to this IP?”

---

# 🌍 2. Real-World Example

Think about your phone contacts.

You search for:

```text
Ram
```

Your phone finds:

```text
98XXXXXXXX
```

This is similar to a forward DNS lookup.

If you receive a call from a number and your phone shows the person's name, that is similar to a reverse lookup.

```text
Ram → phone number
```

```text
Phone number → Ram
```

DNS performs the same type of translation for computers.

---

# 🧠 3. Why Do We Need Lookup Tools?

Some programs automatically perform DNS lookups.

Examples include:

* Web browsers
* `ping`
* Email clients
* SSH clients
* Network applications

When you enter:

`www.google.com`

the application first asks DNS for an IP address.

However, a system administrator may want to manually check DNS information.

For this, Linux provides tools such as:

* `nslookup`
* `dig`
* `host`

---

# 🔄 4. Types of DNS Lookups

## Forward Lookup

Finds an IP address from a hostname.

Example:

```text
www.google.com → 142.250.x.x
```

Common DNS records:

* `A` for IPv4
* `AAAA` for IPv6

---

## Reverse Lookup

Finds a hostname from an IP address.

Example:

```text
8.8.8.8 → dns.google
```

Uses a:

`PTR`

record.

---

## Hostname-to-Hostname Lookup

Finds whether one hostname is an alias of another.

Example:

```text
www.example.com → server01.example.com
```

This normally uses a:

`CNAME`

record.

---

# 🧰 5. Main DNS Lookup Tools

## `nslookup`

An older but widely available DNS lookup utility.

It can be used in:

* Linux
* Windows
* macOS

Example:

`nslookup www.google.com`

---

## `dig`

A more detailed DNS troubleshooting tool.

`dig` stands for:

**Domain Information Groper**

Example:

`dig www.google.com`

It is commonly preferred by Linux administrators because it provides more DNS details.

---

## `host`

A simpler DNS lookup tool.

Example:

`host www.google.com`

It produces shorter and easier-to-read output.

---

# 📦 6. Install Lookup Tools

On RHEL, CentOS Stream, or Fedora:

`dnf install bind-utils -y`

The `bind-utils` package normally provides:

* `dig`
* `nslookup`
* `host`

Verify:

`rpm -qa | grep bind-utils`

---

# 🔍 7. Using `nslookup`

## Basic Forward Lookup

`nslookup www.google.com`

Example output:

```text
Server:         192.168.1.1
Address:        192.168.1.1#53

Non-authoritative answer:
Name:   www.google.com
Address: 142.250.x.x
```

---

# 🧠 8. Understanding `nslookup` Output

## Server

```text
Server: 192.168.1.1
```

This is the DNS resolver used by your machine.

It may be:

* Your router
* Company DNS server
* ISP DNS server
* Public DNS server
* Local DNS server

---

## Address and Port

```text
Address: 192.168.1.1#53
```

This means the DNS server is using:

* IP address: `192.168.1.1`
* Port: `53`

---

## Name

```text
Name: www.google.com
```

The hostname that was queried.

---

## Address

```text
Address: 142.250.x.x
```

The IP address returned by DNS.

---

# 📌 9. What Does “Non-Authoritative Answer” Mean?

You may see:

```text
Non-authoritative answer:
```

This means the DNS server answering your request is not the original authoritative DNS server for that domain.

It may have received the answer from:

* Its cache
* Another DNS resolver
* The authoritative DNS server

It does **not** mean the answer is incorrect.

---

## 🌍 Real-World Example

You ask your teacher:

> “What is the capital of Japan?”

Your teacher knows the answer but is not the Japanese government.

The answer can still be correct, but the teacher is not the official source.

That is similar to a non-authoritative DNS answer.

---

# 🏛️ 10. Authoritative Answer

An authoritative answer comes directly from a DNS server responsible for that domain.

For example, the authoritative DNS server for:

```text
example.com
```

stores the official records for that domain.

---

# 🖥️ 11. Interactive `nslookup` Mode

Run:

`nslookup`

This opens an interactive prompt.

Example:

```text
>
```

Enter a domain:

`www.google.com`

Enter another domain:

`www.facebook.com`

Exit:

`exit`

You may also press:

`Ctrl+C`

---

# ⚡ 12. One-Line `nslookup`

Instead of entering interactive mode:

`nslookup www.hotmail.com`

This performs the query directly.

---

# 🔁 13. Reverse Lookup with `nslookup`

`nslookup 8.8.8.8`

Possible result:

```text
name = dns.google
```

This asks DNS for the PTR record associated with the IP address.

---

# 🎯 14. Query a Specific DNS Server

`nslookup www.google.com 8.8.8.8`

Meaning:

* Query: `www.google.com`
* DNS server: `8.8.8.8`

This is useful when testing whether a specific DNS server works.

---

# 🔎 15. Using `dig`

Basic query:

`dig www.google.com`

This gives detailed information about:

* DNS response
* Record type
* Query status
* Authoritative servers
* Query time
* DNS server used

---

# 🧩 16. Important Sections in `dig` Output

A typical `dig` output contains:

* Header
* Question section
* Answer section
* Authority section
* Additional section
* Query statistics

---

## Header

Example:

```text
status: NOERROR
```

This means the DNS query completed successfully.

---

## Question Section

Example:

```text
www.google.com. IN A
```

Meaning:

* Requested hostname: `www.google.com`
* Class: `IN`
* Record type: `A`

---

## Answer Section

Example:

```text
www.google.com. 300 IN A 142.250.x.x
```

Meaning:

* Hostname: `www.google.com`
* TTL: `300`
* Record type: `A`
* IP address: `142.250.x.x`

---

## Query Time

Example:

```text
Query time: 25 msec
```

Shows how long the lookup took.

---

## Server

Example:

```text
SERVER: 192.168.1.1#53
```

Shows which DNS resolver answered the request.

---

# ✨ 17. Short `dig` Output

Use:

`dig www.google.com +short`

Example result:

```text
142.250.x.x
```

This returns only the main answer.

It is useful in:

* Shell scripts
* Automation
* Quick checks

---

# 🔁 18. Reverse Lookup with `dig`

`dig -x 8.8.8.8`

The `-x` option performs a reverse DNS lookup.

Possible result:

```text
dns.google.
```

---

# 🎯 19. Query a Specific DNS Server with `dig`

`dig @8.8.8.8 www.google.com`

Meaning:

* `@8.8.8.8` = DNS server to query
* `www.google.com` = hostname to resolve

---

## Query Local DNS Server

`dig @192.168.1.153 clienta.lab.local`

This is useful when testing your own DNS lab.

---

# 🧾 20. Query Specific Record Types

## IPv4 Address

`dig www.google.com A`

---

## IPv6 Address

`dig www.google.com AAAA`

---

## Mail Server

`dig example.com MX`

---

## Name Servers

`dig example.com NS`

---

## Alias Record

`dig www.example.com CNAME`

---

## Text Records

`dig example.com TXT`

---

## Start of Authority

`dig example.com SOA`

---

# 📋 21. Common DNS Record Queries

| Purpose        | Command                  |
| -------------- | ------------------------ |
| IPv4 record    | `dig example.com A`      |
| IPv6 record    | `dig example.com AAAA`   |
| Mail server    | `dig example.com MX`     |
| Name server    | `dig example.com NS`     |
| Alias          | `dig example.com CNAME`  |
| Text record    | `dig example.com TXT`    |
| Reverse lookup | `dig -x 8.8.8.8`         |
| Short answer   | `dig example.com +short` |

---

# 🖥️ 22. Using `host`

Basic lookup:

`host www.google.com`

Reverse lookup:

`host 8.8.8.8`

Query a specific record:

`host -t MX example.com`

The `host` command is useful when you need a quick and readable result.

---

# 🆚 23. `nslookup` vs `dig` vs `host`

| Tool       | Best Use                               |
| ---------- | -------------------------------------- |
| `nslookup` | Basic lookup and Windows compatibility |
| `dig`      | Detailed DNS troubleshooting           |
| `host`     | Quick and simple lookup                |

---

## Top Rule

Use:

* `nslookup` for simple checks
* `dig` for detailed analysis
* `host` for quick results

---

# 🌐 24. Checking the Current DNS Server

View resolver configuration:

`cat /etc/resolv.conf`

Example:

```text
nameserver 192.168.1.1
```

This is the DNS resolver your Linux machine normally uses.

---

## Using NetworkManager

`nmcli device show | grep DNS`

This displays DNS servers configured through NetworkManager.

---

# 🧪 25. Using `ping` for Name Resolution

`ping -c 4 www.google.com`

Before sending packets, `ping` resolves the hostname to an IP address.

Example:

```text
PING www.google.com (142.250.x.x)
```

This confirms that hostname resolution worked.

However, remember:

> Successful DNS resolution does not guarantee that the target will respond to ping.

Some systems block ICMP traffic.

---

# 🚫 26. DNS Resolution vs Network Connectivity

These are different tests.

## DNS Test

`dig www.google.com`

Checks whether the name resolves.

---

## Connectivity Test

`ping -c 4 8.8.8.8`

Checks whether the machine can reach an IP address.

---

## Combined Test

`ping -c 4 www.google.com`

Checks name resolution first, then network reachability.

---

# 🧠 27. Troubleshooting Logic

## Case 1: IP Works, Hostname Fails

This works:

`ping -c 4 8.8.8.8`

But this fails:

`ping -c 4 www.google.com`

Likely problem:

* DNS configuration
* Resolver unavailable
* Incorrect `/etc/resolv.conf`

---

## Case 2: Both IP and Hostname Fail

Likely problem:

* Network interface
* IP configuration
* Default gateway
* Firewall
* Internet connection

---

## Case 3: `dig` Works but Browser Fails

Likely problem:

* Browser settings
* Proxy
* HTTPS certificate
* Application-level issue

---

# ⚠️ 28. Why Opening a Website by IP May Fail

Typing a website’s IP address into a browser does not always open the expected website.

Reasons include:

* Multiple websites share one IP address
* HTTPS certificates are issued to hostnames
* Web servers use virtual hosting
* Content delivery networks use different servers
* The IP may change
* The site may require the hostname in the request

Therefore:

> DNS resolution proves the name maps to an IP, but directly opening that IP may not produce the same website.

---

# 🌍 Real-World Example

Imagine one office building hosting 20 companies.

The building has one street address, but visitors must also provide the company name.

The IP address is the building address.

The hostname is the company name.

Without the hostname, the receptionist may not know which company you want.

---

# 🧭 29. DNS Resolution Workflow

```text
User enters www.example.com
              ↓
Application checks local cache
              ↓
System checks local configuration
              ↓
Query sent to configured DNS resolver
              ↓
Resolver searches for DNS record
              ↓
IP address returned
              ↓
Application connects to the IP
```

---

# 📂 30. Local Hostname Resolution

Before asking an external DNS server, Linux may check:

`/etc/hosts`

Example:

```text
192.168.1.240 clienta.lab.local clienta
```

Test:

`ping -c 4 clienta`

This can resolve locally without a DNS server.

---

# 🆚 31. `/etc/hosts` vs DNS

| `/etc/hosts`              | DNS                     |
| ------------------------- | ----------------------- |
| Stored locally            | Stored on DNS server    |
| Good for small testing    | Good for large networks |
| Must update every machine | Update centrally        |
| No DNS server required    | Requires DNS service    |

---

# 🚨 32. Common Lookup Errors

## `NXDOMAIN`

Meaning:

The requested hostname does not exist.

Example:

```text
status: NXDOMAIN
```

Possible causes:

* Typing error
* Missing DNS record
* Wrong domain

---

## `SERVFAIL`

Meaning:

The DNS server failed to process the query.

Possible causes:

* Broken zone configuration
* DNSSEC problem
* Upstream server issue

---

## Timeout

Meaning:

The DNS server did not respond in time.

Possible causes:

* DNS service stopped
* Firewall blocking port 53
* Wrong DNS server IP
* Network problem

---

## Connection Refused

Meaning:

The destination is reachable, but no DNS service is accepting queries.

---

# 🧰 33. Troubleshooting Commands

Check resolver:

`cat /etc/resolv.conf`

Check DNS through NetworkManager:

`nmcli device show | grep DNS`

Test name resolution:

`dig www.google.com`

Test short answer:

`dig www.google.com +short`

Test a specific DNS server:

`dig @8.8.8.8 www.google.com`

Test reverse resolution:

`dig -x 8.8.8.8`

Test with `nslookup`:

`nslookup www.google.com`

Check network:

`ip a`

Check route:

`ip route`

Check connectivity:

`ping -c 4 8.8.8.8`

---

# 🧠 34. Memory Tricks

Remember:

```text
Name → IP = Forward lookup
IP → Name = Reverse lookup
```

Easy command memory:

```text
nslookup = Simple
dig      = Detailed
host     = Quick
```

---

# 📋 35. Command Cheat Sheet

| Task                   | Command                         |
| ---------------------- | ------------------------------- |
| Basic lookup           | `nslookup www.google.com`       |
| Interactive lookup     | `nslookup`                      |
| Detailed lookup        | `dig www.google.com`            |
| Short IP result        | `dig www.google.com +short`     |
| Reverse lookup         | `dig -x 8.8.8.8`                |
| Query specific DNS     | `dig @8.8.8.8 www.google.com`   |
| Check A record         | `dig example.com A`             |
| Check MX record        | `dig example.com MX`            |
| Check NS records       | `dig example.com NS`            |
| Quick lookup           | `host www.google.com`           |
| Check resolver         | `cat /etc/resolv.conf`          |
| Check DNS settings     | `nmcli device show \| grep DNS` |
| Check local hosts file | `cat /etc/hosts`                |

---

# 💼 36. Questions

## Q1. What is hostname lookup?

It is the process of translating a hostname into an IP address.

---

## Q2. What is reverse DNS lookup?

It translates an IP address into a hostname using a PTR record.

---

## Q3. Which tools perform DNS lookups?

Common tools include:

* `dig`
* `nslookup`
* `host`

---

## Q4. What is the difference between `dig` and `nslookup`?

`dig` provides more detailed DNS information, while `nslookup` is simpler and widely available.

---

## Q5. What does a non-authoritative answer mean?

The reply came from a DNS resolver or cache rather than directly from the domain’s authoritative DNS server.

---

## Q6. How do you get only the IP address with `dig`?

`dig hostname +short`

---

## Q7. How do you perform a reverse lookup?

`dig -x IP-address`

---

## Q8. How do you query a specific DNS server?

`dig @DNS-server-IP hostname`

---

## Q9. What does NXDOMAIN mean?

It means the requested DNS name does not exist.

---

## Q10. Why might opening a website by IP fail?

Because of virtual hosting, HTTPS certificates, shared IP addresses, or CDN configuration.

---

# 📌 37. Ultra-Short Revision

* Hostname lookup = Name to IP
* Reverse lookup = IP to name
* DNS port = `53`
* Basic tool = `nslookup`
* Detailed tool = `dig`
* Quick tool = `host`
* Short result = `dig hostname +short`
* Reverse lookup = `dig -x IP`
* Specific DNS server = `dig @DNS-IP hostname`
* Resolver file = `/etc/resolv.conf`
* Local mappings = `/etc/hosts`
* `NXDOMAIN` = Name does not exist
* Non-authoritative = Answer did not come directly from the authoritative server

---

# 🏆 Takeaway

A beginner uses `ping` and sees whether a hostname resolves.

A strong Linux administrator understands:

* Forward and reverse lookups
* DNS record types
* Resolver configuration
* Authoritative and non-authoritative answers
* Differences between `dig`, `nslookup`, and `host`
* How to query a specific DNS server
* How to separate DNS problems from network problems

DNS lookup commands are among the most important troubleshooting tools for Linux administrators, network engineers, and cybersecurity professionals.

---

# ✍️ Notes By Abhishek (Ez Abyss)
