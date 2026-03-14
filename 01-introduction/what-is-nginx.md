# NGINX Beginner Guide

## What is NGINX?

**NGINX (pronounced: engine-x)** is a software used to **run websites and manage internet traffic**.

It can work as:

* Web Server
* Reverse Proxy
* Load Balancer
* API Gateway

NGINX is popular because it is **very fast and can handle many users at the same time**.

Many big companies use NGINX, such as:

* Netflix
* Airbnb
* Instagram
* Dropbox

---

# Why Do We Use NGINX?

NGINX helps websites **handle large traffic easily**.

### Benefits of NGINX

* Very fast
* Uses less memory
* Can handle thousands of users at the same time
* Improves website performance
* Makes systems more scalable

---

# Main Uses of NGINX

## 1. Web Server

NGINX can serve **static files** like:

* HTML
* CSS
* JavaScript
* Images

Example:

```
User → NGINX → Website Files
```

When a user opens a website, NGINX sends the website files to the browser.

---

## 2. Reverse Proxy

A **reverse proxy** means NGINX sits between the **user and backend server**.

Example:

```
User → NGINX → Backend Server (Node.js / Python / Java)
```

NGINX receives the request and forwards it to the backend server.

### Benefits

* Protects backend servers
* Improves performance
* Hides server details

---

## 3. Load Balancer

NGINX can distribute traffic across **multiple servers**.

Example:

```
           → Server 1
User → NGINX
           → Server 2
           → Server 3
```

### Benefits

* Prevents server overload
* Improves system reliability
* Handles high traffic

---

## 4. API Gateway

NGINX can route API requests to different services.

Example:

```
User → NGINX → Auth Service
             → Product Service
             → Payment Service
```

---

# How NGINX Works

NGINX uses two types of processes.

## Master Process

The master process:

* Reads configuration files
* Starts worker processes
* Manages the system

## Worker Processes

Worker processes:

* Handle user requests
* Process network connections

Example:

```
Master Process
      |
      |---- Worker 1
      |---- Worker 2
      |---- Worker 3
```

Each worker can handle **many connections at the same time**.

---

# NGINX vs Apache

| Feature      | NGINX        | Apache        |
| ------------ | ------------ | ------------- |
| Speed        | Very Fast    | Moderate      |
| Memory Usage | Low          | Higher        |
| Architecture | Event-driven | Process-based |

---

# Simple Example of Website Flow

When a user opens a website:

```
User → NGINX → Backend Server → Database
```

NGINX receives the request and sends it to the correct server.

---

# Summary

NGINX is a powerful and widely used tool in modern web infrastructure.

It helps to:

* Serve websites
* Manage traffic
* Balance load between servers
* Improve performance
* Increase scalability

Because of its **speed and efficiency**, NGINX is used by many large companies and modern cloud systems.

---

