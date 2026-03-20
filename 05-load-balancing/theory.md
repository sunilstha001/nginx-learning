# NGINX Load Balancing (Basic to Intermediate)

## 1. What is Load Balancing?

Load balancing is the process of distributing incoming network traffic across multiple servers to:
- Improve performance
- Increase reliability
- Avoid server overload

Instead of sending all requests to one server, a load balancer spreads them across multiple backend servers.

---

## 2. Why Use Load Balancing?

- 🚀 Better performance (parallel request handling)
- 🔄 High availability (if one server fails, others take over)
- 📈 Scalability (add/remove servers easily)
- 🛡️ Fault tolerance

---

## 3. What is NGINX?

NGINX is a high-performance:
- Web server
- Reverse proxy
- Load balancer

It is widely used because it is:
- Lightweight
- Fast
- Efficient with concurrent connections

---

## 4. How NGINX Works as a Load Balancer

Client → NGINX → Backend Servers

NGINX acts as a **reverse proxy**:
- Receives requests
- Forwards them to backend servers
- Sends response back to client

---

## 5. Load Balancing Methods in NGINX

### 5.1 Round Robin (Default)
- Requests are distributed sequentially
- Example:
  - Req1 → Server1
  - Req2 → Server2

✔ Simple and widely used

---

### 5.2 Least Connections
- Sends request to server with least active connections

✔ Best when requests have different processing times

---

### 5.3 IP Hash
- Same client IP always goes to same server

✔ Useful for session persistence (sticky sessions)

---

### 5.4 Weighted Load Balancing
- Assign weight to servers based on capacity

Example:
- Server1 (weight=3)
- Server2 (weight=1)

✔ Server1 gets more traffic

---

## 6. Key Concepts

### Upstream Block
Defines backend servers.

### Reverse Proxy
NGINX forwards requests instead of serving directly.

### Health Checks
Detects failed servers (basic in open source, advanced in NGINX Plus).

---

## 7. Session Persistence (Sticky Sessions)

Ensures:
- Same user → same server

Methods:
- IP Hash
- Cookies (advanced)

---

## 8. Failover Handling

If a server fails:
- NGINX automatically routes traffic to other servers

Parameters:
- max_fails
- fail_timeout

---

## 9. When to Use Which Method?

| Scenario | Method |
|--------|--------|
| Equal servers | Round Robin |
| Heavy/uneven load | Least Connections |
| User session required | IP Hash |
| Different server capacity | Weighted |

---

## 10. Summary

NGINX Load Balancing:
- Distributes traffic efficiently
- Improves performance and uptime
- Supports multiple algorithms
- Easy to configure and scale
