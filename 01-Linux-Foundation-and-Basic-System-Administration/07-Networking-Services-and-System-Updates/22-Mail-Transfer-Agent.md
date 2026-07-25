# 📧 Linux Mail Servers and Postfix — Master Notes

---

## 🎯 1. What Is a Mail Server?

A **mail server** is a system that sends, receives, routes, stores, or provides access to email messages.

> **Simple understanding:** A mail server is a digital post office.

A traditional post office:

* Accepts letters
* Reads destination addresses
* Routes letters
* Delivers them
* Stores undelivered mail temporarily

A mail system performs similar tasks electronically.

---

# 🌍 2. Real-World Example

Suppose an application server completes a nightly backup.

It needs to send this notification:

```text
Backup completed successfully.
```

The workflow may look like this:

```text
Backup script
      ↓
Local mail command
      ↓
Postfix
      ↓
Company SMTP relay
      ↓
Administrator's mailbox
```

The application does not need to understand the entire internet mail system.

It hands the message to Postfix, and Postfix handles delivery.

---

# 🧠 3. Why Do Linux Servers Need Email?

Linux servers commonly send messages for:

* Backup results
* Cron job failures
* Disk-space warnings
* Security alerts
* Monitoring notifications
* Application errors
* Account notifications
* Workflow completion
* System reports

Example alert:

```text
Subject: Disk Space Warning

The /var filesystem has reached 90% usage.
```

---

# 🏗️ 4. Main Components of an Email System

A complete email environment may contain several different components.

| Component         | Full name             | Purpose                                   |
| ----------------- | --------------------- | ----------------------------------------- |
| MUA               | Mail User Agent       | Used to write and read email              |
| MSA               | Mail Submission Agent | Accepts messages from authenticated users |
| MTA               | Mail Transfer Agent   | Transfers email between servers           |
| MDA               | Mail Delivery Agent   | Places messages in a local mailbox        |
| IMAP/POP3 server  | Mail-access server    | Allows users to retrieve email            |
| Spam filter       | Content filter        | Detects unwanted messages                 |
| Antivirus scanner | Malware scanner       | Checks attachments and content            |

---

## Easy Analogy

| Email component | Post-office analogy           |
| --------------- | ----------------------------- |
| MUA             | Person writing a letter       |
| MSA             | Local post-office counter     |
| MTA             | Delivery truck between cities |
| MDA             | Local postal worker           |
| Mailbox         | Recipient's mailbox           |
| IMAP/POP3       | Recipient collecting mail     |

---

# 📤 5. What Is an MTA?

**MTA** stands for **Mail Transfer Agent**.

An MTA:

* Accepts email
* Examines the recipient
* Selects a destination
* Transfers the message
* Queues mail if delivery fails
* Retries delivery later

Common MTAs include:

* Postfix
* Sendmail
* Exim
* OpenSMTPD

---

# 📦 6. What Is Postfix?

**Postfix** is a popular Mail Transfer Agent.

It is used to:

* Send local system messages
* Receive SMTP mail
* Relay messages to another server
* Route messages between domains
* Queue and retry failed messages

Important components:

| Item                        | Value                    |
| --------------------------- | ------------------------ |
| Package                     | `postfix`                |
| Service                     | `postfix`                |
| Main configuration          | `/etc/postfix/main.cf`   |
| Service configuration       | `/etc/postfix/master.cf` |
| Queue command               | `postqueue`              |
| Configuration query command | `postconf`               |

---

## Important Clarification

Postfix is primarily an SMTP transport system.

Postfix alone does not normally provide users with IMAP or POP3 access.

For mailbox access, organizations commonly use software such as:

`Dovecot`

---

# 🆚 7. Postfix and Dovecot

| Postfix                      | Dovecot                          |
| ---------------------------- | -------------------------------- |
| Sends and receives SMTP mail | Provides mailbox access          |
| MTA                          | IMAP/POP3 server                 |
| Routes messages              | Lets users read messages         |
| Common ports: 25, 587        | Common ports: 143, 993, 110, 995 |

Example complete mail system:

```text
Internet
   ↓
Postfix
   ↓
User mailbox
   ↓
Dovecot
   ↓
Email client
```

---

# 📚 8. Other Mail-Related Software

## Sendmail

One of the oldest Unix MTAs.

Characteristics:

* Historically important
* Highly configurable
* Complex configuration
* Less common for new deployments

---

## Exim

A flexible MTA commonly found on some Linux systems and hosting platforms.

---

## OpenSMTPD

A lightweight SMTP server originally associated with OpenBSD.

---

## Dovecot

Provides:

* IMAP
* POP3
* Secure mailbox access
* Authentication integration

Dovecot is not a replacement for Postfix.

They perform different jobs and are often used together.

---

## SpamAssassin

Analyzes email and assigns spam scores.

---

## ClamAV

Scans content and attachments for known malware.

---

## Amavis

Can connect an MTA to:

* Spam filters
* Antivirus scanners
* Content-checking systems

---

## Zimbra

A larger collaboration platform that can provide:

* Email
* Calendar
* Contacts
* Webmail
* Administration tools

It is not simply a small Postfix replacement.

---

# 🌐 9. Important Email Protocols and Ports

| Protocol           | Purpose                                   | Default port |
| ------------------ | ----------------------------------------- | -----------: |
| SMTP               | Server-to-server delivery                 |         `25` |
| Message submission | Authenticated client submission           |        `587` |
| Implicit TLS SMTP  | Encrypted submission in some environments |        `465` |
| IMAP               | Mailbox access                            |        `143` |
| IMAPS              | Encrypted IMAP                            |        `993` |
| POP3               | Mailbox download                          |        `110` |
| POP3S              | Encrypted POP3                            |        `995` |

---

## Memory Trick

```text
25  = SMTP transfer
587 = SMTP submission
993 = Secure IMAP
995 = Secure POP3
```

---

# 🔄 10. Basic Email Delivery Workflow

```text
User or script creates message
             ↓
s-nail submits message
             ↓
Postfix accepts message
             ↓
Postfix checks destination
             ↓
Message delivered locally or relayed
             ↓
Recipient's mail server accepts it
             ↓
Recipient reads it through IMAP/webmail
```

---

# 🧱 11. Common Postfix Roles

Postfix can be configured in different ways.

## Local-Only Mail System

Used for messages between local Linux accounts.

Example:

```text
root → student
```

No internet delivery is required.

---

## Outbound Relay Client

The Linux server sends all external email through a company SMTP relay.

```text
Linux server
     ↓
Company relay
     ↓
Internet recipient
```

This is common for:

* Application servers
* Monitoring servers
* Backup systems
* Cron notifications

---

## Internet-Facing SMTP Server

The server directly receives email for a domain.

This requires significantly more configuration:

* Public DNS
* MX records
* PTR record
* TLS certificate
* Firewall rules
* Anti-spam controls
* Authentication security
* Reputation management
* DKIM
* SPF
* DMARC

A beginner lab should generally start with local mail or an approved company relay.

---

# ⚠️ 12. Never Create an Open Relay

An **open relay** allows unauthorized users to send mail through your server.

Attackers can use it to distribute:

* Spam
* Phishing messages
* Malicious attachments

Consequences can include:

* IP blacklisting
* Domain reputation damage
* Resource exhaustion
* Security incidents

> Only trusted users, systems, or networks should be permitted to relay mail.

---

# 🧪 13. Lab Goal

This lab will configure Postfix for:

* Local mail testing
* Optional outbound delivery through an approved relay

It will not build a complete public email provider.

---

# 👤 14. Confirm the Current User

`whoami`

Detailed identity:

`id`

Become root if required:

`su -`

---

# 🌐 15. Verify Network Access

Check IP information:

`ip a`

Check routing:

`ip route`

Test DNS resolution:

`getent hosts example.com`

Test basic connectivity:

`ping -c 4 example.com`

Remember that ping does not prove an SMTP relay is available.

---

# 🔍 16. Check Whether Postfix Is Installed

`rpm -qa | grep postfix`

Another method:

`dnf list installed postfix`

If no package appears, install it.

---

# 📥 17. Install Postfix

`dnf install postfix -y`

Verify:

`rpm -qa | grep postfix`

---

# ✉️ 18. Install the Command-Line Mail Client

On RHEL 9 and similar systems:

`dnf install s-nail -y`

The package provides the `mail` command.

Verify:

`rpm -qa | grep s-nail`

Find the command:

`command -v mail`

---

## Postfix vs `s-nail`

| Postfix                   | `s-nail`                     |
| ------------------------- | ---------------------------- |
| Transfers and queues mail | Creates and submits messages |
| Background service        | Command-line client          |
| MTA                       | MUA                          |
| Service name: `postfix`   | Command: `mail`              |

---

## Real-World Analogy

Postfix is the postal transportation system.

`s-nail` is the pen and envelope used to prepare the letter.

---

# 📂 19. Important Postfix Files

| Path                     | Purpose                                 |
| ------------------------ | --------------------------------------- |
| `/etc/postfix/main.cf`   | Main Postfix configuration              |
| `/etc/postfix/master.cf` | Controls Postfix services and processes |
| `/etc/aliases`           | Local email aliases                     |
| `/var/spool/postfix/`    | Postfix queue and spool data            |
| `/usr/sbin/postfix`      | Postfix management command              |

---

# 💾 20. Back Up the Configuration

Before making changes:

`cp /etc/postfix/main.cf /etc/postfix/main.cf.backup`

Also back up `master.cf` before editing it:

`cp /etc/postfix/master.cf /etc/postfix/master.cf.backup`

Verify:

`ls -l /etc/postfix/*.backup`

---

# ⚙️ 21. View Current Postfix Configuration

Show all configuration values:

`postconf`

Show values changed from defaults:

`postconf -n`

Show one parameter:

`postconf relayhost`

Show the server hostname setting:

`postconf myhostname`

---

# ✍️ 22. Modify Configuration Safely

You can edit the main file directly:

`vi /etc/postfix/main.cf`

However, for individual parameters, `postconf -e` is often safer.

Example:

`postconf -e 'myhostname = mail.lab.local'`

This updates the appropriate parameter in `main.cf`.

---

# 🏷️ 23. Important Identity Parameters

## `myhostname`

Defines the fully qualified hostname of the mail server.

Example:

```conf
myhostname = server1.lab.local
```

Command:

`postconf -e 'myhostname = server1.lab.local'`

---

## `mydomain`

Defines the domain portion.

Example:

```conf
mydomain = lab.local
```

Command:

`postconf -e 'mydomain = lab.local'`

---

## `myorigin`

Controls the domain appended to locally submitted mail.

Example:

```conf
myorigin = $mydomain
```

Command:

`postconf -e 'myorigin = $mydomain'`

---

# 🏠 24. Local Mail Configuration

For a simple local-only lab, Postfix can listen only on the local machine.

Example:

```conf
inet_interfaces = loopback-only
```

Command:

`postconf -e 'inet_interfaces = loopback-only'`

This prevents external systems from connecting to the SMTP service.

It is a good choice for a server that only sends locally generated notifications.

---

# 📬 25. What Is a Relay Host?

A **relay host** is another SMTP server that accepts your message and forwards it toward the final destination.

Example:

```text
Application server
        ↓
Company relay
        ↓
Recipient's mail server
```

Typical reasons to use a relay:

* Direct internet SMTP is blocked
* Company policy requires central mail delivery
* Authentication is required
* Central logging is required
* One server manages email reputation
* Applications should not deliver mail directly

---

# ⚙️ 26. Configure a Basic Relay Host

Example hostname:

```conf
relayhost = [smtp.company.example]:25
```

Command:

`postconf -e 'relayhost = [smtp.company.example]:25'`

Example IP:

```conf
relayhost = [192.168.1.100]:25
```

Command:

`postconf -e 'relayhost = [192.168.1.100]:25'`

---

## Why Use Square Brackets?

This:

```conf
[smtp.company.example]
```

tells Postfix to connect directly to that host without first looking up an MX record.

Without brackets, Postfix may perform MX lookup behavior.

---

# 🔐 27. Modern Relay Requirements

Most external SMTP providers require:

* Authentication
* TLS encryption
* Approved sender addresses
* Port `587` or `465`
* Provider-specific credentials

A basic `relayhost` line alone may not be enough.

Do not place an ordinary personal password directly into `main.cf`.

Use the approved relay method provided by your organization or mail provider.

---

# 🔑 28. Authenticated Relay Example

Example relay:

```conf
relayhost = [smtp.company.example]:587
smtp_sasl_auth_enable = yes
smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd
smtp_sasl_security_options = noanonymous
smtp_tls_security_level = encrypt
```

Set parameters:

`postconf -e 'relayhost = [smtp.company.example]:587'`

`postconf -e 'smtp_sasl_auth_enable = yes'`

`postconf -e 'smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd'`

`postconf -e 'smtp_sasl_security_options = noanonymous'`

`postconf -e 'smtp_tls_security_level = encrypt'`

---

# 🗝️ 29. Create the Authentication File

Create:

`vi /etc/postfix/sasl_passwd`

Example structure:

```text
[smtp.company.example]:587 username:application-password
```

Use credentials specifically approved for SMTP relay.

Prefer an application-specific credential rather than a normal account password when your provider supports it.

---

# 🔒 30. Protect the Credential File

`chmod 600 /etc/postfix/sasl_passwd`

Create the Postfix lookup database:

`postmap /etc/postfix/sasl_passwd`

Protect the generated database:

`chmod 600 /etc/postfix/sasl_passwd.db`

---

## Important Security Rule

Do not:

* Publish this file
* Upload it to GitHub
* Include it in screenshots
* Store it in world-readable locations
* Share the password in documentation

---

# 🛡️ 31. TLS Configuration

For an authenticated SMTP relay, a common client setting is:

```conf
smtp_tls_security_level = encrypt
```

This requires an encrypted connection to the relay.

A less strict setting is:

```conf
smtp_tls_security_level = may
```

This uses TLS when available but can allow unencrypted delivery.

For credential-based relay submission, `encrypt` is generally safer when supported by the relay.

---

# ✅ 32. Validate Postfix Configuration

Run:

`postfix check`

If no error is printed, the basic configuration and permissions passed the check.

Display non-default settings:

`postconf -n`

Review them carefully before restarting the service.

---

# ▶️ 33. Start Postfix

`systemctl start postfix`

---

# 🔁 34. Enable Postfix at Boot

`systemctl enable postfix`

---

# ⚡ 35. Start and Enable Together

`systemctl enable --now postfix`

---

# 🔄 36. Apply Configuration Changes

Reload without a complete restart:

`systemctl reload postfix`

Or:

`postfix reload`

Restart when needed:

`systemctl restart postfix`

Reloading is generally less disruptive for ordinary configuration changes.

---

# 🔎 37. Check Service Status

`systemctl status postfix`

Look for:

```text
Active: active (running)
```

---

# 🧪 38. Check Postfix Processes

`ps -ef | grep postfix`

You may see processes such as:

* `master`
* `pickup`
* `qmgr`
* `smtp`
* `cleanup`

The `master` process controls other Postfix services.

---

## Important Correction

Do not normally stop Postfix using:

`kill PID`

Use:

`systemctl stop postfix`

This allows the service manager to stop processes cleanly.

---

# ⏹️ 39. Stop Postfix

`systemctl stop postfix`

Disable it at boot:

`systemctl disable postfix`

---

# ✉️ 40. Send an Interactive Test Message

`mail -s "Postfix test" user@example.com`

Type the message body:

```text
Hello,

This is a test message from my Linux server.
```

Press:

`Ctrl+D`

This finishes the message and normally submits it.

---

# ⚡ 41. Send a One-Line Test Message

`echo "This is a Postfix test." | mail -s "Postfix test" user@example.com`

This is easier for scripts and lab testing.

---

# 📄 42. Send a File as the Message Body

`mail -s "System report" user@example.com < /tmp/system-report.txt`

---

# 👥 43. Send to a Local Linux User

`echo "Local mail test" | mail -s "Test" student`

This delivers mail to the local account named `student`, assuming local delivery is configured.

Read local mail:

`mail`

---

# 📤 44. Test with the Sendmail-Compatible Interface

Postfix provides a sendmail-compatible command.

Example:

`printf "Subject: Test\n\nHello from Postfix.\n" | sendmail -v user@example.com`

The `-v` option displays delivery activity.

---

# 📋 45. Understand the Mail Queue

When Postfix cannot deliver a message immediately, it places the message in a queue.

Reasons include:

* Relay unavailable
* DNS failure
* Network problem
* Authentication failure
* Recipient server temporarily unavailable

---

## Display Queue

`postqueue -p`

Alternative:

`mailq`

---

## Force Queue Retry

`postqueue -f`

This tells Postfix to attempt queued deliveries again.

Do not repeatedly force the queue without first solving the underlying problem.

---

## Delete One Queued Message

First find its queue ID:

`postqueue -p`

Then remove it:

`postsuper -d QUEUE_ID`

---

## Delete All Queued Messages

`postsuper -d ALL`

Use this carefully because it permanently removes all queued mail.

---

# 📜 46. Check Postfix Logs

On systems using the systemd journal:

`journalctl -u postfix`

Show recent entries:

`journalctl -u postfix -n 50`

Follow logs live:

`journalctl -u postfix -f`

Some systems with traditional mail logging may also use:

`/var/log/maillog`

Check it with:

`tail -f /var/log/maillog`

The available log location depends on the system’s logging configuration.

---

# 🔍 47. Common Log Messages

## Authentication Failure

Possible message:

```text
SASL authentication failed
```

Check:

* Username
* Password or application password
* Relay hostname
* SASL configuration

---

## Relay Access Denied

Possible message:

```text
Relay access denied
```

The relay does not allow your server or account to send through it.

---

## Connection Timed Out

Possible causes:

* Firewall
* Wrong port
* Network problem
* SMTP provider blocking the connection

---

## Name or Service Not Known

Possible cause:

* DNS resolution failure
* Incorrect relay hostname

---

## Connection Refused

Possible causes:

* SMTP service not running
* Wrong port
* Relay refusing connections

---

# 🔥 48. Firewall Considerations

If the server only sends mail through an external relay, you may not need to open an inbound SMTP firewall port.

If the server must receive SMTP connections, allow SMTP:

`firewall-cmd --permanent --add-service=smtp`

Reload:

`firewall-cmd --reload`

Verify:

`firewall-cmd --list-services`

---

## Important Rule

Only open inbound SMTP when the server is intentionally configured to receive email.

Do not expose port 25 unnecessarily.

---

# 🌐 49. Check Listening Ports

`ss -ltnp | grep :25`

Possible output indicates Postfix is listening on SMTP port 25.

Check submission port:

`ss -ltnp | grep :587`

---

# 🧱 50. Listening Interface Security

For a local notification system, use:

```conf
inet_interfaces = loopback-only
```

For an intentionally network-accessible mail server, an administrator may configure:

```conf
inet_interfaces = all
```

Do not use `all` without:

* Firewall controls
* Correct relay restrictions
* Authentication design
* Anti-abuse configuration

---

# 📮 51. Local Aliases

Linux services often send notifications to:

`root`

You can redirect root’s mail to an administrator.

Edit:

`vi /etc/aliases`

Example:

```text
root: administrator@example.com
```

Rebuild aliases:

`newaliases`

Send a test:

`echo "Root alias test" | mail -s "Alias test" root`

---

# 🌍 52. Why Direct Internet Email Often Fails

A small lab server may not be able to deliver directly to public services.

Possible reasons:

* ISP blocks outbound port 25
* Cloud provider restricts SMTP
* No valid PTR record
* No SPF record
* No DKIM signature
* No DMARC policy
* Dynamic IP address
* Poor IP reputation
* Recipient rejects unauthenticated delivery
* TLS or hostname problems

For application notifications, an approved authenticated relay is usually more practical.

---

# 🧾 53. Important Email DNS Records

A public mail domain commonly needs:

| Record        | Purpose                                     |
| ------------- | ------------------------------------------- |
| `MX`          | Identifies receiving mail servers           |
| `A` or `AAAA` | Maps mail hostname to IP                    |
| `PTR`         | Maps sending IP back to hostname            |
| `SPF`         | Identifies approved sending systems         |
| `DKIM`        | Cryptographically signs messages            |
| `DMARC`       | Defines authentication policy and reporting |

These records are not required for a simple local-mail lab, but they are essential concepts for public email delivery.

---

# 🔐 54. Email Security Principles

A secure mail environment should:

* Use TLS
* Require authentication for submission
* Prevent open relaying
* Restrict trusted networks
* Protect credential files
* Monitor logs
* Apply security updates
* Use spam and malware controls when receiving public mail
* Use SPF, DKIM, and DMARC for internet domains
* Limit unnecessary listening interfaces

---

# 🧪 55. Complete Local Lab Procedure

## Step 1: Confirm user

`whoami`

---

## Step 2: Check package

`rpm -qa | grep postfix`

---

## Step 3: Install Postfix

`dnf install postfix -y`

---

## Step 4: Install mail client

`dnf install s-nail -y`

---

## Step 5: Back up configuration

`cp /etc/postfix/main.cf /etc/postfix/main.cf.backup`

---

## Step 6: Configure local-only listening

`postconf -e 'inet_interfaces = loopback-only'`

---

## Step 7: Check configuration

`postfix check`

---

## Step 8: Start and enable

`systemctl enable --now postfix`

---

## Step 9: Check status

`systemctl status postfix`

---

## Step 10: Send local message

`echo "Postfix is working." | mail -s "Local Postfix Test" root`

---

## Step 11: Read local mail

`mail`

---

## Step 12: Check queue

`postqueue -p`

---

## Step 13: Check logs

`journalctl -u postfix -n 50`

---

# 🌐 56. Complete Relay Lab Workflow

Use only an approved relay and approved credentials.

```text
Install Postfix
       ↓
Install s-nail
       ↓
Back up main.cf
       ↓
Configure relayhost
       ↓
Configure TLS
       ↓
Configure authentication
       ↓
Protect password map
       ↓
Run postmap
       ↓
Validate configuration
       ↓
Restart Postfix
       ↓
Send test message
       ↓
Check queue and logs
```

---

# 🚨 57. Common Problems and Solutions

| Problem                          | Likely cause                    | Solution                      |
| -------------------------------- | ------------------------------- | ----------------------------- |
| `mail: command not found`        | `s-nail` missing                | Install `s-nail`              |
| Postfix inactive                 | Service stopped                 | Start `postfix`               |
| Message remains queued           | Delivery failure                | Check queue and logs          |
| Authentication failed            | Wrong credentials               | Check SASL password map       |
| Relay denied                     | Relay policy                    | Use approved account/server   |
| Connection timed out             | Network or firewall             | Check route and SMTP port     |
| Name resolution error            | DNS problem                     | Test relay hostname           |
| TLS failure                      | Certificate or TLS setting      | Review TLS configuration      |
| Local mail works, external fails | Relay/internet configuration    | Configure approved relay      |
| Mail marked as spam              | Reputation/authentication issue | Configure SPF, DKIM and DMARC |
| Recipient never receives message | Queue or remote rejection       | Inspect logs and queue        |

---

# 🧰 58. Troubleshooting Checklist

Check service:

`systemctl status postfix`

Check configuration syntax:

`postfix check`

Show changed settings:

`postconf -n`

Check relay setting:

`postconf relayhost`

Check listening sockets:

`ss -ltnp | grep master`

Check queue:

`postqueue -p`

Check logs:

`journalctl -u postfix -n 100`

Follow logs:

`journalctl -u postfix -f`

Check DNS:

`getent hosts smtp.company.example`

Check routes:

`ip route`

Retry queue after fixing problem:

`postqueue -f`

---

# 🧠 59. Memory Framework

Remember:

```text
s-nail  = Write and submit
Postfix = Transfer and queue
Dovecot = Read and retrieve
```

Basic workflow:

> **Install → Configure → Validate → Start → Send → Check Queue → Check Logs**

---

# 📋 60. Command Cheat Sheet

| Task                   | Command                                             |
| ---------------------- | --------------------------------------------------- |
| Check Postfix package  | `rpm -qa \| grep postfix`                           |
| Install Postfix        | `dnf install postfix -y`                            |
| Install mail client    | `dnf install s-nail -y`                             |
| Main configuration     | `vi /etc/postfix/main.cf`                           |
| Show changed settings  | `postconf -n`                                       |
| Show relay host        | `postconf relayhost`                                |
| Validate configuration | `postfix check`                                     |
| Start Postfix          | `systemctl start postfix`                           |
| Enable Postfix         | `systemctl enable postfix`                          |
| Start and enable       | `systemctl enable --now postfix`                    |
| Restart Postfix        | `systemctl restart postfix`                         |
| Reload Postfix         | `systemctl reload postfix`                          |
| Check status           | `systemctl status postfix`                          |
| Send interactive mail  | `mail -s "Subject" user@example.com`                |
| Send one-line mail     | `echo "Body" \| mail -s "Subject" user@example.com` |
| Show queue             | `postqueue -p`                                      |
| Retry queue            | `postqueue -f`                                      |
| Check logs             | `journalctl -u postfix -n 50`                       |
| Follow logs            | `journalctl -u postfix -f`                          |
| Rebuild aliases        | `newaliases`                                        |
| Build password map     | `postmap /etc/postfix/sasl_passwd`                  |

---

# 💼 61. Questions

## Q1. What is a mail server?

A mail server sends, receives, routes, stores, or provides access to email.

---

## Q2. What is an MTA?

An MTA is a Mail Transfer Agent that transports email between systems.

---

## Q3. What is Postfix?

Postfix is an MTA commonly used for SMTP transport on Linux.

---

## Q4. What is the main Postfix configuration file?

`/etc/postfix/main.cf`

---

## Q5. What is `/etc/postfix/master.cf`?

It controls the Postfix services, listeners, and process behavior.

---

## Q6. What is the Postfix service name?

`postfix`

---

## Q7. What is the difference between Postfix and `s-nail`?

Postfix transfers and queues mail, while `s-nail` provides the user-facing `mail` command.

---

## Q8. What is the difference between Postfix and Dovecot?

Postfix handles SMTP transport. Dovecot provides IMAP and POP3 mailbox access.

---

## Q9. What is a relay host?

It is an SMTP server that accepts mail from another system and forwards it toward the destination.

---

## Q10. Why are brackets used around a relay host?

They tell Postfix to connect directly to that host without performing an MX lookup.

---

## Q11. How do you validate Postfix configuration?

`postfix check`

---

## Q12. How do you display changed Postfix settings?

`postconf -n`

---

## Q13. How do you view queued mail?

`postqueue -p`

---

## Q14. How do you force queue delivery?

`postqueue -f`

---

## Q15. How do you check Postfix logs?

`journalctl -u postfix`

---

## Q16. What is an open relay?

A server that permits unauthorized systems to send mail through it.

---

## Q17. Which port is normally used for SMTP server-to-server delivery?

Port `25`.

---

## Q18. Which port is commonly used for authenticated message submission?

Port `587`.

---

## Q19. What protects authenticated SMTP traffic?

TLS encryption and SASL authentication.

---

## Q20. Why might a lab server fail to deliver directly to Gmail or another public provider?

It may lack a valid PTR record, SPF, DKIM, DMARC, reputation, allowed port 25 access, or proper relay authentication.

---

# 📌 62. Ultra-Short Revision

* Mail server = Digital post office
* Postfix = Mail Transfer Agent
* Package = `postfix`
* Service = `postfix`
* Main configuration = `/etc/postfix/main.cf`
* Service configuration = `/etc/postfix/master.cf`
* Command-line client = `s-nail`
* User command = `mail`
* SMTP transfer port = `25`
* Submission port = `587`
* Relay host = Intermediate SMTP server
* Validate = `postfix check`
* Changed settings = `postconf -n`
* Queue = `postqueue -p`
* Retry queue = `postqueue -f`
* Logs = `journalctl -u postfix`
* Dovecot provides IMAP/POP3 access
* Never configure an open relay
* Modern external relays normally require TLS and authentication

---

# 🏆 63. Takeaway

A beginner knows that Postfix sends email.

A strong Linux administrator understands:

* The difference between MUA, MSA, MTA, and MDA
* The difference between Postfix and Dovecot
* Local delivery versus SMTP relaying
* Why modern relays require authentication and TLS
* How to secure credential maps
* How to prevent open relaying
* How to inspect the mail queue
* How to troubleshoot delivery through logs
* Why public email delivery requires proper DNS and reputation
* Why application servers should normally use an approved central relay

Postfix is not simply a command for sending email. It is a complete message-transport and queue-management system that must be configured carefully and securely.

---

# ✍️ Notes By Abhishek (Ez Abyss)
