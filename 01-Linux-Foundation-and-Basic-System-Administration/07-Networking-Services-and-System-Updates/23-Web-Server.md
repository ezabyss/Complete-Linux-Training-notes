# 🌐 Apache HTTP Server (`httpd`)

---

## 🎯 1. What Is a Web Server?

A **web server** is software that accepts requests from clients and returns web content.

The client is usually:

* A web browser
* A mobile application
* Another server
* A command-line tool such as `curl`

The web server may return:

* HTML pages
* Images
* CSS files
* JavaScript
* Documents
* API responses
* Videos and other static files

> **Simple understanding:** A web server receives a request and sends back the requested web content.

---

# 🌍 2. Real-World Example

When a user enters:

```text
https://example.com
```

the following process occurs:

```text
Browser
   ↓
DNS resolves example.com
   ↓
Browser connects to the server
   ↓
Web server receives the request
   ↓
Web server finds the requested content
   ↓
Content is returned to the browser
```

A web server works like a restaurant:

| Restaurant | Web server                  |
| ---------- | --------------------------- |
| Customer   | Browser                     |
| Order      | HTTP request                |
| Waiter     | Apache                      |
| Kitchen    | Server files or application |
| Meal       | Web page or response        |

---

# 🧠 3. What Is Apache HTTP Server?

**Apache HTTP Server** is an open-source web server maintained by the Apache Software Foundation.

On RHEL and CentOS Stream, Apache is commonly called:

`httpd`

The name means:

**HTTP daemon**

A daemon is a background process that continuously waits for requests.

---

# 📦 4. Important Apache Components

| Item                     | Value                        |
| ------------------------ | ---------------------------- |
| Software                 | Apache HTTP Server           |
| Package                  | `httpd`                      |
| Service                  | `httpd`                      |
| Main configuration       | `/etc/httpd/conf/httpd.conf` |
| Additional configuration | `/etc/httpd/conf.d/`         |
| Default document root    | `/var/www/html`              |
| Default homepage         | `/var/www/html/index.html`   |
| Log directory            | `/var/log/httpd/`            |
| HTTP port                | `80`                         |
| HTTPS port               | `443`                        |

---

# 🔄 5. Apache Request Workflow

```text
User enters website address
            ↓
DNS returns server IP
            ↓
Browser connects to port 80 or 443
            ↓
Apache receives the HTTP request
            ↓
Apache checks its configuration
            ↓
Apache finds the requested file
            ↓
Apache returns an HTTP response
            ↓
Browser displays the page
```

---

# 🌐 6. HTTP vs HTTPS

## HTTP

HTTP stands for:

**Hypertext Transfer Protocol**

Default port:

`80`

HTTP traffic is not encrypted.

Example:

```text
http://192.168.1.12
```

---

## HTTPS

HTTPS means HTTP protected with TLS encryption.

Default port:

`443`

Example:

```text
https://example.com
```

HTTPS protects information exchanged between the browser and server.

---

## Important Correction

A correctly configured HTTPS website should not normally display a security warning.

Warnings usually appear because:

* The certificate is expired
* The certificate is self-signed
* The certificate name does not match the website
* The browser does not trust the certificate authority
* The certificate chain is incomplete

---

# 🆚 7. HTTP and HTTPS Comparison

| Feature                | HTTP      | HTTPS      |
| ---------------------- | --------- | ---------- |
| Default port           | `80`      | `443`      |
| Encryption             | No        | Yes        |
| Certificate required   | No        | Yes        |
| Suitable for passwords | No        | Yes        |
| URL prefix             | `http://` | `https://` |

---

# 🖥️ 8. Lab Goal

In this lab, you will:

1. Install Apache
2. Create a basic HTML page
3. Start the Apache service
4. Configure the firewall
5. Test the website
6. Check logs
7. Troubleshoot common issues

Example server IP:

```text
192.168.1.12
```

Use your own Linux machine’s actual IP address.

---

# 👤 9. Confirm Your User

`whoami`

Check detailed identity:

`id`

Become root when required:

`su -`

---

# 🌐 10. Check the Server IP Address

`ip a`

Show only one interface:

`ip addr show enp0s3`

Your interface may be named differently:

* `enp0s3`
* `ens33`
* `eth0`

A shorter way to display assigned addresses is:

`hostname -I`

---

# 📶 11. Test Network Connectivity

`ping -c 4 www.google.com`

This checks basic network and name-resolution connectivity.

Remember that ping does not test whether Apache is working.

---

# 🔍 12. Check Whether Apache Is Installed

`rpm -q httpd`

Another method:

`dnf list installed httpd`

A broader search:

`rpm -qa | grep httpd`

The direct `rpm -q httpd` command is usually clearer when checking one package.

---

# 📥 13. Install Apache

`dnf install httpd -y`

This installs:

* Apache HTTP Server
* Required dependencies
* Supporting utilities

Verify:

`rpm -q httpd`

---

# 🔎 14. Check the Installed Apache Version

`httpd -v`

Example output:

```text
Server version: Apache/2.4.x
```

Show more build information:

`httpd -V`

---

# 📂 15. Important Apache Directories

| Directory                    | Purpose                        |
| ---------------------------- | ------------------------------ |
| `/etc/httpd/`                | Apache configuration           |
| `/etc/httpd/conf/`           | Main configuration directory   |
| `/etc/httpd/conf.d/`         | Additional configuration files |
| `/etc/httpd/conf.modules.d/` | Module configuration           |
| `/var/www/html/`             | Default website content        |
| `/var/log/httpd/`            | Access and error logs          |
| `/var/cache/httpd/`          | Apache cache data              |
| `/run/httpd/`                | Runtime information            |

---

# ⚙️ 16. Main Configuration File

The main configuration file is:

`/etc/httpd/conf/httpd.conf`

Back it up before editing:

`cp /etc/httpd/conf/httpd.conf /etc/httpd/conf/httpd.conf.backup`

Open it:

`vi /etc/httpd/conf/httpd.conf`

---

# 🧩 17. Important Configuration Directives

## `ServerRoot`

Example:

```apache
ServerRoot "/etc/httpd"
```

This defines the base directory for Apache configuration files.

---

## `Listen`

Example:

```apache
Listen 80
```

This tells Apache to listen for HTTP connections on port 80.

---

## `DocumentRoot`

Example:

```apache
DocumentRoot "/var/www/html"
```

This defines where Apache looks for the main website’s files.

---

## Directory Permissions

Example:

```apache
<Directory "/var/www/html">
    AllowOverride None
    Require all granted
</Directory>
```

This controls access to the document-root directory.

---

## `DirectoryIndex`

Apache commonly uses `index.html` as the default page.

When a user requests:

```text
http://192.168.1.12/
```

Apache may automatically serve:

```text
/var/www/html/index.html
```

---

# 📁 18. What Is DocumentRoot?

`DocumentRoot` is the filesystem directory that represents the root of the website.

Default:

`/var/www/html`

Example mapping:

```text
Browser request:
http://192.168.1.12/index.html

Filesystem file:
/var/www/html/index.html
```

Another example:

```text
Browser request:
http://192.168.1.12/images/logo.png

Filesystem file:
/var/www/html/images/logo.png
```

---

# 🌍 19. Real-World DocumentRoot Example

Think of `/var/www/html` as a shop display window.

Files inside it can be shown to website visitors.

Files elsewhere on the server are not automatically available through Apache.

---

# 📝 20. Create Your First Website

Move to the default document root:

`cd /var/www/html`

Create the homepage:

`vi index.html`

Add:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My First Linux Website</title>
</head>
<body>
    <h1>Welcome to My First Website</h1>
    <p>This page is being served by Apache on Linux.</p>
</body>
</html>
```

Save and exit.

---

# 🧠 21. Understanding the HTML

## Document Type

```html
<!DOCTYPE html>
```

Tells the browser that the document uses modern HTML.

---

## HTML Element

```html
<html lang="en">
```

Begins the HTML document and identifies its language.

---

## Head Section

```html
<head>
```

Contains information about the page, such as:

* Title
* Character encoding
* Mobile display settings
* CSS references
* Metadata

---

## Body Section

```html
<body>
```

Contains content visible to the visitor.

---

## Heading

```html
<h1>Welcome to My First Website</h1>
```

Creates a top-level heading.

---

## Paragraph

```html
<p>This page is being served by Apache on Linux.</p>
```

Creates a paragraph.

---

# ⚠️ 22. HTML Tag Structure

Most HTML tags have:

* An opening tag
* Content
* A closing tag

Example:

```html
<h1>My Heading</h1>
```

The closing tag contains `/`.

Some elements, such as metadata elements, do not contain visible page content.

---

# ▶️ 23. Start Apache

`systemctl start httpd`

---

# 🔁 24. Enable Apache at Boot

`systemctl enable httpd`

---

# ⚡ 25. Start and Enable Together

`systemctl enable --now httpd`

This:

* Starts Apache immediately
* Enables Apache after future reboots

---

# 🔎 26. Check Apache Status

`systemctl status httpd`

Look for:

```text
Active: active (running)
```

A script-friendly check is:

`systemctl is-active httpd`

Check whether it starts at boot:

`systemctl is-enabled httpd`

---

# 🔄 27. Restart, Reload and Stop Apache

Restart:

`systemctl restart httpd`

Reload configuration without a full restart:

`systemctl reload httpd`

Stop:

`systemctl stop httpd`

Disable at boot:

`systemctl disable httpd`

---

## Restart vs Reload

| Command | Effect                                     |
| ------- | ------------------------------------------ |
| Restart | Stops and starts Apache                    |
| Reload  | Reloads configuration with less disruption |
| Stop    | Stops serving web requests                 |

For normal configuration updates, validate first and then reload.

---

# ✅ 28. Validate Apache Configuration

Before restarting or reloading:

`apachectl configtest`

Expected output:

```text
Syntax OK
```

Another valid command:

`httpd -t`

Do not restart Apache after editing configuration until the syntax test succeeds.

---

# 🧠 Workflow

```text
Edit
  ↓
Validate
  ↓
Reload
  ↓
Test
  ↓
Check logs
```

Commands:

`apachectl configtest`

`systemctl reload httpd`

---

# 🔥 29. Configure the Firewall Safely

Do not disable the entire firewall just to run a website.

Check firewall status:

`firewall-cmd --state`

Allow HTTP permanently:

`firewall-cmd --permanent --add-service=http`

Reload the firewall:

`firewall-cmd --reload`

Verify:

`firewall-cmd --list-services`

You should see:

```text
http
```

---

# 🔒 30. Allow HTTPS

When HTTPS is configured:

`firewall-cmd --permanent --add-service=https`

Reload:

`firewall-cmd --reload`

Verify:

`firewall-cmd --list-services`

---

# ⚠️ Why Not Disable `firewalld`?

Disabling the firewall exposes services unnecessarily.

A better approach is to allow only the traffic required:

* HTTP on port 80
* HTTPS on port 443
* SSH on port 22 when needed

This follows the principle of least privilege.

---

# 🧪 31. Test Locally with `curl`

From the Apache server:

`curl http://localhost`

You should see your HTML content.

Show only response headers:

`curl -I http://localhost`

Expected status:

```text
HTTP/1.1 200 OK
```

---

# 🧪 32. Test Through the Server IP

From the same server:

`curl http://192.168.1.12`

From a browser on another machine:

```text
http://192.168.1.12
```

Replace the example with your server’s actual IP.

---

# 📊 33. Common HTTP Status Codes

|  Code | Meaning               |
| ----: | --------------------- |
| `200` | Request succeeded     |
| `301` | Permanent redirect    |
| `302` | Temporary redirect    |
| `403` | Access forbidden      |
| `404` | Page not found        |
| `500` | Internal server error |
| `502` | Bad gateway           |
| `503` | Service unavailable   |

---

## Memory Trick

```text
2xx = Success
3xx = Redirect
4xx = Client-side problem
5xx = Server-side problem
```

---

# 📜 34. Apache Log Files

Default log directory:

`/var/log/httpd/`

Main logs:

| File                        | Purpose                     |
| --------------------------- | --------------------------- |
| `/var/log/httpd/access_log` | Records incoming requests   |
| `/var/log/httpd/error_log`  | Records warnings and errors |

---

# 👀 35. View Access Logs

`tail /var/log/httpd/access_log`

Follow new requests live:

`tail -f /var/log/httpd/access_log`

An access-log entry may show:

* Client IP
* Requested page
* Request time
* HTTP method
* Status code
* Response size

---

# 🚨 36. View Error Logs

`tail /var/log/httpd/error_log`

Follow errors live:

`tail -f /var/log/httpd/error_log`

Also inspect the systemd journal:

`journalctl -u httpd`

Show recent messages:

`journalctl -u httpd -n 50`

Follow messages:

`journalctl -u httpd -f`

---

# 🔎 37. Check Listening Ports

`ss -ltnp | grep :80`

For HTTPS:

`ss -ltnp | grep :443`

This confirms whether a process is listening on the expected port.

---

# 🧪 38. Check Apache Processes

`ps -ef | grep httpd`

You may see:

* A parent process running as root
* Worker processes running as the `apache` user

Do not normally terminate Apache using `kill`.

Use:

`systemctl stop httpd`

---

# 👤 39. Apache Service User

On RHEL and CentOS Stream, Apache worker processes normally run as:

`apache`

Check:

`ps -eo user,pid,cmd | grep httpd`

The parent process requires elevated privileges to bind to ports such as 80, while worker processes run with lower privileges.

---

# 🔐 40. File Permissions

The website files must be readable by Apache.

Check:

`ls -l /var/www/html`

A common file permission is:

`chmod 644 /var/www/html/index.html`

A common directory permission is:

`chmod 755 /var/www/html`

Avoid using:

`chmod 777`

World-writable permissions create unnecessary security risk.

---

# 🛡️ 41. SELinux and Apache

RHEL and CentOS Stream commonly run SELinux.

Apache content needs the correct SELinux context.

Check:

`ls -Z /var/www/html`

Restore the expected context:

`restorecon -Rv /var/www/html`

For content under the default document root, this is often sufficient.

---

# 📂 42. Serving Content from a Custom Directory

Suppose you want to use:

`/websites/mysite`

Create it:

`mkdir -p /websites/mysite`

Create content:

`echo '<h1>Custom Website</h1>' > /websites/mysite/index.html`

Apache configuration must grant access and define the directory as a document root or alias.

SELinux must also permit Apache to read it.

Set a persistent SELinux mapping:

`semanage fcontext -a -t httpd_sys_content_t "/websites/mysite(/.*)?"`

Apply it:

`restorecon -Rv /websites/mysite`

The `semanage` command may require an additional SELinux management package.

---

# ⚠️ 43. Do Not Disable SELinux as a Quick Fix

If Apache cannot read a file:

* Check Unix permissions
* Check SELinux context
* Check Apache configuration
* Check the error log

Do not immediately disable SELinux.

SELinux provides an important security layer.

---

# 🏷️ 44. Set a Server Name

Apache may warn that it cannot determine its fully qualified domain name.

For a lab, add:

```apache
ServerName server1.lab.local
```

You can place a custom configuration file in:

`/etc/httpd/conf.d/servername.conf`

Create it:

`echo 'ServerName server1.lab.local' > /etc/httpd/conf.d/servername.conf`

Validate:

`apachectl configtest`

Reload:

`systemctl reload httpd`

---

# 🌍 45. Access by Hostname Instead of IP

To access:

```text
http://server1.lab.local
```

the hostname must resolve to the server’s IP through:

* DNS
* `/etc/hosts`

Temporary client-side lab entry:

```text
192.168.1.12 server1.lab.local
```

On Linux, add it to:

`/etc/hosts`

Then test:

`getent hosts server1.lab.local`

---

# 🏢 46. Virtual Hosts

A virtual host allows one Apache server to host multiple websites.

Example:

```text
website1.lab.local
website2.lab.local
```

Both can use the same server IP.

---

## Example Virtual Host

Create:

`vi /etc/httpd/conf.d/website1.conf`

Configuration:

```apache
<VirtualHost *:80>
    ServerName website1.lab.local
    DocumentRoot /var/www/website1

    <Directory "/var/www/website1">
        Require all granted
    </Directory>

    ErrorLog /var/log/httpd/website1_error.log
    CustomLog /var/log/httpd/website1_access.log combined
</VirtualHost>
```

Create its document root:

`mkdir -p /var/www/website1`

Create a page:

`echo '<h1>Website One</h1>' > /var/www/website1/index.html`

Restore contexts:

`restorecon -Rv /var/www`

Validate:

`apachectl configtest`

Reload:

`systemctl reload httpd`

---

# 🔎 47. Display Virtual Host Configuration

`httpd -S`

This shows:

* Configured virtual hosts
* Server names
* Listening addresses
* Configuration file locations

---

# 🧩 48. Apache Modules

Apache uses modules to add features.

Examples:

* TLS support
* Proxying
* URL rewriting
* Authentication
* Compression
* HTTP/2

List loaded modules:

`httpd -M`

Search for one module:

`httpd -M | grep ssl`

---

# 🔒 49. Basic HTTPS Concepts

To enable HTTPS, Apache needs:

* TLS module
* Certificate
* Private key
* HTTPS virtual-host configuration
* Firewall access to port 443

Install the TLS module:

`dnf install mod_ssl -y`

This commonly creates or enables:

`/etc/httpd/conf.d/ssl.conf`

Validate:

`apachectl configtest`

Restart:

`systemctl restart httpd`

---

# ⚠️ 50. Self-Signed Certificates

A self-signed certificate can encrypt lab traffic, but browsers generally do not trust it automatically.

Therefore, a warning may appear.

For public websites, use a certificate issued by a trusted certificate authority.

Never expose a private key publicly.

---

# 🌐 51. A Local Website Is Not Automatically Public

Creating a website on your Linux VM makes it available only where the server is reachable.

For public internet access, you may also need:

* A public IP address
* Router port forwarding
* Cloud firewall rules
* Public DNS
* TLS certificate
* Server hardening
* Regular updates
* Backups
* Monitoring
* ISP permission
* Protection against attacks

A home internet provider may block inbound traffic or place users behind carrier-grade NAT.

> Installing Apache does not automatically publish a secure website to the whole internet.

---

# 🔐 52. Production Security Practices

A production web server should:

* Use HTTPS
* Keep Apache and the OS patched
* Keep `firewalld` enabled
* Keep SELinux enforcing
* Expose only required ports
* Avoid running applications as root
* Protect private keys
* Limit file permissions
* Monitor logs
* Back up configurations and content
* Disable unnecessary modules
* Use secure application code
* Avoid displaying sensitive server information

---

# 🧪 53. Complete Basic Lab

## Step 1: Check IP

`hostname -I`

---

## Step 2: Check package

`rpm -q httpd`

---

## Step 3: Install Apache

`dnf install httpd -y`

---

## Step 4: Create the homepage

`vi /var/www/html/index.html`

---

## Step 5: Restore SELinux context

`restorecon -Rv /var/www/html`

---

## Step 6: Validate configuration

`apachectl configtest`

---

## Step 7: Start and enable Apache

`systemctl enable --now httpd`

---

## Step 8: Allow HTTP through the firewall

`firewall-cmd --permanent --add-service=http`

---

## Step 9: Reload firewall

`firewall-cmd --reload`

---

## Step 10: Check Apache status

`systemctl status httpd`

---

## Step 11: Test locally

`curl -I http://localhost`

---

## Step 12: Test through the IP

`curl http://192.168.1.12`

---

## Step 13: Open in a browser

```text
http://192.168.1.12
```

---

## Step 14: Check logs

`tail -f /var/log/httpd/access_log`

---

# 🚨 54. Common Problems

| Problem                           | Possible cause                       | Solution                         |
| --------------------------------- | ------------------------------------ | -------------------------------- |
| Connection refused                | Apache stopped                       | Start `httpd`                    |
| Connection timed out              | Firewall or network                  | Allow HTTP and check routing     |
| Default page appears              | Wrong or missing `index.html`        | Check document root              |
| `403 Forbidden`                   | Permissions, Apache rule, or SELinux | Check permissions and context    |
| `404 Not Found`                   | Requested file missing               | Check URL and file location      |
| Apache fails to start             | Configuration syntax error           | Run `apachectl configtest`       |
| Changes do not appear             | Browser cache or wrong file          | Refresh and verify DocumentRoot  |
| Hostname does not work            | DNS missing                          | Configure DNS or `/etc/hosts`    |
| IP works but remote browser fails | Firewall/network mode                | Check firewall and VM networking |
| HTTPS warning                     | Untrusted or mismatched certificate  | Use a valid trusted certificate  |
| Port already in use               | Another service uses port 80         | Check with `ss -ltnp`            |

---

# 🧰 55. Troubleshooting Workflow

## Step 1: Check service

`systemctl status httpd`

---

## Step 2: Validate configuration

`apachectl configtest`

---

## Step 3: Check listening ports

`ss -ltnp | grep :80`

---

## Step 4: Test locally

`curl -I http://localhost`

---

## Step 5: Check firewall

`firewall-cmd --list-services`

---

## Step 6: Check website files

`ls -l /var/www/html`

---

## Step 7: Check SELinux context

`ls -Z /var/www/html`

---

## Step 8: Restore context

`restorecon -Rv /var/www/html`

---

## Step 9: Check error logs

`tail -n 50 /var/log/httpd/error_log`

---

## Step 10: Check system journal

`journalctl -u httpd -n 50`

---

## Step 11: Check server IP

`hostname -I`

---

## Step 12: Test from another machine

`curl -I http://SERVER_IP`

---

# 🧠 56. Memory Framework

Remember:

```text
httpd     = Package and service
httpd.conf = Main configuration
/var/www/html = Website files
Port 80   = HTTP
Port 443  = HTTPS
access_log = Requests
error_log  = Problems
```

workflow:

> **Install → Create → Validate → Start → Allow → Test → Monitor**

---

# 📋 57. Command Cheat Sheet

| Task                    | Command                                        |
| ----------------------- | ---------------------------------------------- |
| Check package           | `rpm -q httpd`                                 |
| Install Apache          | `dnf install httpd -y`                         |
| Check version           | `httpd -v`                                     |
| Main configuration      | `vi /etc/httpd/conf/httpd.conf`                |
| Default homepage        | `vi /var/www/html/index.html`                  |
| Validate configuration  | `apachectl configtest`                         |
| Alternative validation  | `httpd -t`                                     |
| Start Apache            | `systemctl start httpd`                        |
| Enable Apache           | `systemctl enable httpd`                       |
| Start and enable        | `systemctl enable --now httpd`                 |
| Restart Apache          | `systemctl restart httpd`                      |
| Reload Apache           | `systemctl reload httpd`                       |
| Check status            | `systemctl status httpd`                       |
| Allow HTTP              | `firewall-cmd --permanent --add-service=http`  |
| Allow HTTPS             | `firewall-cmd --permanent --add-service=https` |
| Reload firewall         | `firewall-cmd --reload`                        |
| Test page               | `curl http://localhost`                        |
| Test headers            | `curl -I http://localhost`                     |
| Check port 80           | `ss -ltnp \| grep :80`                         |
| Check modules           | `httpd -M`                                     |
| Check virtual hosts     | `httpd -S`                                     |
| Access log              | `tail -f /var/log/httpd/access_log`            |
| Error log               | `tail -f /var/log/httpd/error_log`             |
| Restore SELinux context | `restorecon -Rv /var/www/html`                 |

---

# 💼 58. Questions

## Q1. What is a web server?

A web server accepts HTTP requests and returns web content or application responses.

---

## Q2. What is Apache HTTP Server called on RHEL?

`httpd`

---

## Q3. What is the Apache package name?

`httpd`

---

## Q4. What is the Apache service name?

`httpd`

---

## Q5. Where is the main configuration file?

`/etc/httpd/conf/httpd.conf`

---

## Q6. What is the default document root?

`/var/www/html`

---

## Q7. What are the default HTTP and HTTPS ports?

HTTP uses port `80`, and HTTPS normally uses port `443`.

---

## Q8. How do you validate Apache configuration?

`apachectl configtest`

or:

`httpd -t`

---

## Q9. How do you start and enable Apache?

`systemctl enable --now httpd`

---

## Q10. How do you permit HTTP through `firewalld`?

`firewall-cmd --permanent --add-service=http`

Then:

`firewall-cmd --reload`

---

## Q11. Where are Apache logs stored?

`/var/log/httpd/`

---

## Q12. What is the difference between `access_log` and `error_log`?

`access_log` records requests, while `error_log` records errors and warnings.

---

## Q13. What is `DocumentRoot`?

It is the directory containing files served as website content.

---

## Q14. What is a virtual host?

It allows one Apache server to host multiple websites.

---

## Q15. Why might Apache return `403 Forbidden`?

Possible reasons include filesystem permissions, Apache access rules, or SELinux restrictions.

---

## Q16. What is the difference between restart and reload?

Restart stops and starts Apache. Reload applies configuration changes with less disruption.

---

## Q17. Why should you not disable the firewall?

The firewall protects other services. You should allow only the required HTTP or HTTPS traffic.

---

## Q18. Why does a self-signed HTTPS certificate show a warning?

Because the browser does not trust the certificate issuer by default.

---

## Q19. How do you check which Apache modules are loaded?

`httpd -M`

---

## Q20. How do you display parsed virtual-host settings?

`httpd -S`

---

# 📌 59. Ultra-Short Revision

* Web server = Serves web content
* Apache package = `httpd`
* Apache service = `httpd`
* Main config = `/etc/httpd/conf/httpd.conf`
* Additional config = `/etc/httpd/conf.d/`
* Document root = `/var/www/html`
* Homepage = `/var/www/html/index.html`
* HTTP = Port `80`
* HTTPS = Port `443`
* Validate = `apachectl configtest`
* Start and enable = `systemctl enable --now httpd`
* Allow HTTP = `firewall-cmd --permanent --add-service=http`
* Access log = `/var/log/httpd/access_log`
* Error log = `/var/log/httpd/error_log`
* Test locally = `curl -I http://localhost`
* Keep the firewall and SELinux enabled
* A local Apache page is not automatically public on the internet

---

# 🏆 60. Takeaway

A beginner installs Apache and creates `index.html`.

A strong Linux administrator understands:

* How HTTP requests flow from client to server
* The relationship between URLs and filesystem paths
* Apache configuration directives
* Service lifecycle management
* Configuration validation before reload
* Firewall rules instead of firewall disabling
* Unix permissions and SELinux contexts
* HTTP status codes
* Access and error log analysis
* Virtual-host configuration
* HTTP versus HTTPS
* The difference between a local lab and a secure public deployment

Apache does more than display HTML. It is a modular server that can host websites, secure connections, proxy applications, support multiple domains, and provide detailed operational logs.

---

# ✍️ Notes By Abhishek (Ez Abyss)
