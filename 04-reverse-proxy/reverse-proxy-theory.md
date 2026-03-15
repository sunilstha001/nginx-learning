# Reverse Proxy (Theory)

## What is a Reverse Proxy?

A **Reverse Proxy** is a server that sits between **clients (users)** and **backend servers**.

Instead of users directly contacting the backend server, they send requests to the **reverse proxy server**.
The reverse proxy then forwards the request to the appropriate backend server and returns the response back to the user.

```
Client (Browser)
        │
        ▼
Reverse Proxy (NGINX)
        │
        ▼
Backend Server (Node.js / Python / Java)
```

Example flow:

1. A user opens a website: `example.com`
2. The request first reaches **NGINX reverse proxy**
3. NGINX forwards the request to the backend server
4. Backend server processes the request
5. The response goes back through NGINX to the user

The user never directly interacts with the backend server.

---

# Why Reverse Proxy is Used

## 1. Security

The backend servers are hidden from the public internet.

Users cannot directly access the backend server, which protects it from attacks.

Example:

```
User → NGINX → Backend Server
```

The backend server's IP address remains hidden.

---

## 2. Load Balancing

If a website receives heavy traffic, one server may not be enough.

A reverse proxy can distribute traffic across multiple servers.

Example:

```
          ┌── Server 1
User → NGINX
          ├── Server 2
          └── Server 3
```

This improves performance and reliability.

---

## 3. SSL Termination

Handling HTTPS encryption is expensive for backend servers.

A reverse proxy can manage **SSL/TLS encryption**.

Example:

```
User (HTTPS)
      │
      ▼
NGINX (handles SSL)
      │
      ▼
Backend Server (HTTP)
```

This reduces load on backend servers.

---

## 4. Caching

Reverse proxies can store frequently requested data in memory.

If the same request comes again, the proxy serves the cached response instead of contacting the backend server.

Benefits:

* Faster response
* Reduced backend load

---

## 5. Single Entry Point

All traffic goes through one place.

This makes it easier to manage:

* security rules
* routing
* logging
* monitoring

---

# Reverse Proxy vs Forward Proxy

| Feature         | Reverse Proxy          | Forward Proxy         |
| --------------- | ---------------------- | --------------------- |
| Who it protects | Servers                | Clients               |
| Used by         | Website infrastructure | Users                 |
| Example         | NGINX                  | VPN / corporate proxy |

Forward proxy hides **clients**, while reverse proxy hides **servers**.

---

# Popular Reverse Proxy Software

Some commonly used reverse proxy tools include:

* NGINX
* HAProxy
* Apache HTTP Server
* Traefik

Among these, **NGINX** is one of the most widely used reverse proxies due to its high performance and scalability.

---

# Real World Example

When you open a large website like Netflix or Amazon:

```
User → Reverse Proxy → Multiple Backend Servers
```

The reverse proxy decides which backend server should handle the request.

This allows large websites to handle **millions of users**.

---

# Summary

A reverse proxy is an important part of modern web infrastructure.

Key benefits:

* hides backend servers
* improves security
* distributes traffic
* handles SSL
* improves performance through caching

Reverse proxies are widely used in production systems and cloud infrastructure.
