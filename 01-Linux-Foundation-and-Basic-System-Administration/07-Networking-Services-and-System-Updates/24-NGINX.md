# ⭐ NGINX

## 1. What is NGINX?

NGINX (pronounced **Engine-X**) is an open-source, high-performance web
server.

It can work as:

-   Web Server
-   Reverse Proxy
-   Load Balancer
-   HTTP Cache
-   Mail Proxy
-   API Gateway

Unlike Apache, NGINX uses an **event-driven asynchronous architecture**,
allowing it to handle thousands of simultaneous connections efficiently.

------------------------------------------------------------------------

## 2. History

**Created by:** Igor Sysoev

**Released:** October 2004

**Purpose:** Solve the **C10K Problem**

**Meaning:** Handle **10,000 simultaneous client connections** on one
server.

------------------------------------------------------------------------

## 3. Why NGINX Became Popular

-   ✅ Very fast
-   ✅ Low memory usage
-   ✅ Excellent for static files
-   ✅ Reverse proxy
-   ✅ Load balancing
-   ✅ SSL termination
-   ✅ High scalability

------------------------------------------------------------------------

## 4. Apache vs NGINX

  Apache                          |NGINX
  ------------------------------- | -----------------------
  Process/Thread based            | Event driven
  Better dynamic modules          | Better reverse proxy
  Higher memory usage             | Lower memory usage
  Excellent `.htaccess` support   | No `.htaccess`
  Great compatibility             | Excellent performance

------------------------------------------------------------------------

## 5. Common Uses

NGINX can:

-   Host websites
-   Serve static files
-   Reverse proxy applications
-   Load balance servers
-   Cache content
-   SSL termination
-   API Gateway
-   Kubernetes Ingress Controller

------------------------------------------------------------------------

## 6. NGINX Architecture

``` text
Internet
      │
      ▼
+----------------+
|     NGINX      |
+----------------+
       │
 ┌─────┴─────┐
 ▼           ▼
App 1      App 2
```

NGINX receives requests and forwards them to backend servers when acting
as a reverse proxy.

------------------------------------------------------------------------

## 7. Important Files

  Purpose              | Location
  -------------------- | ----------------------------------------
  Main configuration   | `/etc/nginx/nginx.conf`
  Virtual hosts        | `/etc/nginx/conf.d/`
  Website files        | `/usr/share/nginx/html` or `/var/www/`
  Logs                 | `/var/log/nginx/`
  Error log            | `/var/log/nginx/error.log`
  Access log           | `/var/log/nginx/access.log`

------------------------------------------------------------------------

## 8. Install

### Check package

``` bash
rpm -q nginx
```

### Install

``` bash
dnf install nginx
```

### Verify

``` bash
rpm -q nginx
```

### Version

``` bash
nginx -v
```

### Detailed version

``` bash
nginx -V
```

------------------------------------------------------------------------

## 9. Start Service

``` bash
systemctl start nginx
systemctl enable nginx
systemctl enable --now nginx
systemctl status nginx
```

------------------------------------------------------------------------

## 10. Service Management

``` bash
systemctl restart nginx
systemctl reload nginx
systemctl stop nginx
systemctl disable nginx
```

------------------------------------------------------------------------

## 11. Validate Configuration

Always before restarting:

``` bash
nginx -t
```

Expected:

``` text
syntax is ok
test is successful
```

------------------------------------------------------------------------

## 12. Main Configuration Structure

``` nginx
events { }

http {

    server {

    }

}
```

------------------------------------------------------------------------

## 13. Basic Server Block

``` nginx
server {

    listen 80;

    server_name example.com;

    root /var/www/example/html;

    index index.html;

}
```

------------------------------------------------------------------------

## 14. Create Website

``` bash
mkdir -p /var/www/mywebsite/html
vi index.html
```

Example:

``` html
<!DOCTYPE html>
<html>
<head>
<title>My First Website</title>
</head>
<body>
<h1>Hello Linux!</h1>
</body>
</html>
```

------------------------------------------------------------------------

## 15. Firewall

Instead of disabling **firewalld**:

``` bash
firewall-cmd --permanent --add-service=http
firewall-cmd --reload
firewall-cmd --permanent --add-service=https
```

------------------------------------------------------------------------

## 16. SELinux

``` bash
restorecon -Rv /var/www
```

For custom directories:

``` bash
semanage fcontext -a -t httpd_sys_content_t "/mywebsite(/.*)?"
restorecon -Rv /mywebsite
```

------------------------------------------------------------------------

## 17. Reverse Proxy

Example:

``` nginx
location / {

    proxy_pass http://192.168.1.162;

}
```

``` text
Browser
   ↓
NGINX
   ↓
Backend Server
   ↓
Response
   ↓
Browser
```

------------------------------------------------------------------------

## 18. Important Proxy Headers

``` nginx
proxy_set_header Host $host;
proxy_set_header X-Real-IP $remote_addr;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
proxy_set_header X-Forwarded-Proto $scheme;
```

These preserve the original client information for the backend
application.

------------------------------------------------------------------------

## 19. Load Balancing

``` nginx
upstream backend {

server 192.168.1.101;

server 192.168.1.102;

server 192.168.1.103;

}

proxy_pass http://backend;
```

------------------------------------------------------------------------

## 20. Check Listening Ports

``` bash
ss -ltnp | grep nginx
```

or

``` bash
ss -ltnp | grep :80
```

------------------------------------------------------------------------

## 21. Logs

Access:

``` bash
tail -f /var/log/nginx/access.log
```

Errors:

``` bash
tail -f /var/log/nginx/error.log
```

------------------------------------------------------------------------

## 22. Common HTTP Errors

-   200 OK
-   404 Not Found
-   403 Forbidden
-   500 Internal Server Error
-   502 Bad Gateway
-   503 Service Unavailable
-   504 Gateway Timeout

------------------------------------------------------------------------

## 23. Why 502 Bad Gateway Happens

Common causes:

-   Backend server stopped
-   Wrong IP
-   Wrong port
-   SELinux blocking
-   Firewall blocking backend
-   Backend timeout
-   Application crashed

------------------------------------------------------------------------

## 24. Troubleshooting Workflow

``` text
systemctl status nginx
        ↓
nginx -t
        ↓
ss -ltnp
        ↓
tail error.log
        ↓
firewall-cmd
        ↓
SELinux
        ↓
Backend running?
```

------------------------------------------------------------------------

## 25. Questions

**What is NGINX?**

A high-performance web server and reverse proxy.

**Who created NGINX?**

Igor Sysoev.

**What problem did NGINX solve?**

The C10K Problem.

**Main configuration file?**

`/etc/nginx/nginx.conf`

**Virtual host directory?**

`/etc/nginx/conf.d/`

**Test configuration?**

``` bash
nginx -t
```

**Reload service?**

``` bash
systemctl reload nginx
```

**Logs location?**

`/var/log/nginx/`

**Default HTTP port?**

`80`

**HTTPS port?**

`443`

**Difference between Web Server and Reverse Proxy?**

-   A web server serves content directly to clients.
-   A reverse proxy receives client requests and forwards them to one or
    more backend servers.

**Difference between Reverse Proxy and Load Balancer?**

-   Reverse proxy forwards requests.
-   Load balancer distributes requests across multiple backend servers.

------------------------------------------------------------------------

## 26. Summary

Remember this sequence:

> **Install → Configure → Validate (`nginx -t`) → Reload → Allow
> Firewall → Test → Monitor Logs → Troubleshoot**


---

✍️ **Notes By Abhishek (Ez Abyss)**
