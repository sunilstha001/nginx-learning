# Install NGINX on AWS EC2 (Linux)

This guide explains how to install **NGINX on an AWS EC2 instance**.

NGINX will be used as a **web server or reverse proxy** for your applications.

---

# Prerequisites

Before installing NGINX, you need:

* An AWS account
* An EC2 instance running (Ubuntu or Amazon Linux)
* SSH access to the EC2 instance
* Port **80 (HTTP)** allowed in the **Security Group**

---

# Step 1: Connect to EC2 Instance

Connect to your EC2 instance using SSH.

Example:

```bash
ssh -i your-key.pem ubuntu@your-ec2-public-ip
```

Example:

```bash
ssh -i mykey.pem ubuntu@13.233.xxx.xxx
```

Now you are connected to your EC2 server.

---

# Step 2: Update System Packages

Update the system packages before installing NGINX.

```bash
sudo apt update
```

This ensures the system installs the latest packages.

---

# Step 3: Install NGINX

Install NGINX using the package manager.

```bash
sudo apt install nginx -y
```

The `-y` flag automatically confirms installation.

---

# Step 4: Start NGINX

Start the NGINX service.

```bash
sudo systemctl start nginx
```

Enable NGINX to start automatically when the server starts.

```bash
sudo systemctl enable nginx
```

---

# Step 5: Check NGINX Status

Check whether NGINX is running.

```bash
sudo systemctl status nginx
```

You should see:

```
active (running)
```

---

# Step 6: Allow HTTP Traffic in Security Group

Go to **AWS Console → EC2 → Security Groups**.

Add an **Inbound Rule**:

Type:

```
HTTP
```

Port:

```
80
```

Source:

```
0.0.0.0/0
```

This allows users to access your server.

---

# Step 7: Open NGINX in Browser

Copy your **EC2 Public IP**.

Example:

```
http://your-ec2-public-ip
```

Example:

```
http://13.233.xxx.xxx
```

If NGINX is installed correctly, you will see the **NGINX Welcome Page**.

---

# Useful NGINX Commands

Start NGINX

```bash
sudo systemctl start nginx
```

Stop NGINX

```bash
sudo systemctl stop nginx
```

Restart NGINX

```bash
sudo systemctl restart nginx
```

Reload Configuration

```bash
sudo systemctl reload nginx
```

---

# Check NGINX Version

```bash
nginx -v
```

Example output:

```
nginx version: nginx/1.24.0
```

---

# Default NGINX Files

Important directories:

```
/etc/nginx/nginx.conf      → Main configuration file
/etc/nginx/sites-available → Website configuration
/etc/nginx/sites-enabled   → Enabled websites
/var/www/html              → Default website folder
/var/log/nginx             → Log files
```

---

# Simple Architecture

```
User → Internet → EC2 Server → NGINX → Application
```

Example application:

* Node.js
* Python
* Java
* Go

---

# Summary

Steps to install NGINX on EC2:

1. Launch EC2 instance
2. Connect using SSH
3. Update packages
4. Install NGINX
5. Start NGINX service
6. Allow port 80 in Security Group
7. Access server using public IP

Now NGINX is running on your **AWS EC2 server**.

---
