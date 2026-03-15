# NGINX Directory Structure

When NGINX is installed on a Linux server (Ubuntu / EC2), several folders and files are created.
These directories contain **configuration files, website files, and logs**.

Understanding these directories is important when working with NGINX.

---

# Main NGINX Directories

## 1. Main Configuration File

Location:

```bash
/etc/nginx/nginx.conf
```

This is the **main configuration file of NGINX**.

It controls:

* Global settings
* Worker processes
* Logging
* HTTP configuration
* Including other configuration files

Example:

```nginx
worker_processes auto;

events {
    worker_connections 1024;
}

http {
    include /etc/nginx/mime.types;
}
```

---

# 2. sites-available Directory

Location:

```bash
/etc/nginx/sites-available
```

This folder stores **configuration files for all websites**.

Each website usually has its own configuration file.

Example:

```
/etc/nginx/sites-available/mywebsite
```

Example configuration:

```nginx
server {
    listen 80;
    server_name mywebsite.com;

    root /var/www/mywebsite;
    index index.html;
}
```

---

# 3. sites-enabled Directory

Location:

```bash
/etc/nginx/sites-enabled
```

This folder contains **symbolic links to active websites**.

Only the sites inside **sites-enabled** are actually used by NGINX.

Example:

```
/etc/nginx/sites-enabled/mywebsite
```

To enable a site:

```bash
sudo ln -s /etc/nginx/sites-available/mywebsite /etc/nginx/sites-enabled/
```

---

# 4. Default Website Directory

Location:

```bash
/var/www/html
```

This is the **default folder where website files are stored**.

It usually contains:

* HTML files
* CSS
* JavaScript
* Images

Example structure:

```
/var/www/html
   ├── index.html
   ├── style.css
   └── script.js
```

When you open the server IP in a browser, NGINX serves files from this folder.

---

# 5. NGINX Logs Directory

Location:

```bash
/var/log/nginx
```

This folder stores **NGINX log files**.

Important logs:

```
access.log
error.log
```

### access.log

Records all incoming requests.

Example:

```
192.168.1.10 - - [10/Mar/2026] "GET /index.html HTTP/1.1"
```

### error.log

Stores server errors.

Example:

```
File not found error
```

Logs help developers **debug issues**.

---

# 6. MIME Types File

Location:

```bash
/etc/nginx/mime.types
```

This file tells NGINX how to handle different file types.

Example:

```
text/html
image/png
application/javascript
```

---

# 7. Modules Directory

Location:

```bash
/usr/lib/nginx/modules
```

This directory contains **NGINX modules** that extend functionality.

Examples:

* HTTP modules
* Stream modules
* Mail modules

---

# Complete Directory Overview

```
/etc/nginx
   ├── nginx.conf
   ├── sites-available
   ├── sites-enabled
   └── mime.types

/var/www
   └── html

/var/log/nginx
   ├── access.log
   └── error.log
```

---

# Example Request Flow

```
User Request
     |
     v
NGINX Server
     |
     |---- Configuration → /etc/nginx/nginx.conf
     |
     |---- Website Files → /var/www/html
     |
     |---- Logs → /var/log/nginx
```

---

# Summary

Important NGINX directories:

| Directory                  | Purpose                 |
| -------------------------- | ----------------------- |
| /etc/nginx/nginx.conf      | Main configuration file |
| /etc/nginx/sites-available | Website configurations  |
| /etc/nginx/sites-enabled   | Active websites         |
| /var/www/html              | Website files           |
| /var/log/nginx             | Log files               |

Understanding the directory structure helps you **configure and manage NGINX servers easily**.

---

