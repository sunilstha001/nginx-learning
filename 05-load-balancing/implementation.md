# NGINX Load Balancing Implementation Guide

## 1. Install NGINX

### Ubuntu/Debian:

```bash
sudo apt update
sudo apt install nginx
```

### Check Status:

```bash
sudo systemctl status nginx
```

---

## 2. Configuration File Location

Main config:

```bash
/etc/nginx/nginx.conf
```

Additional configs:

```bash
/etc/nginx/conf.d/
```

---

## 3. Basic Load Balancing (Round Robin)

```nginx
http {
    upstream backend {
        server 127.0.0.1:3000;
        server 127.0.0.1:3001;
    }

    server {
        listen 80;

        location / {
            proxy_pass http://backend;
        }
    }
}
```

✔ Default method = Round Robin

---

## 4. Least Connections Method

```nginx
upstream backend {
    least_conn;
    server 127.0.0.1:3000;
    server 127.0.0.1:3001;
}
```

✔ Sends request to least busy server

---

## 5. IP Hash (Sticky Sessions)

```nginx
upstream backend {
    ip_hash;
    server 127.0.0.1:3000;
    server 127.0.0.1:3001;
}
```

✔ Same client → same server

---

## 6. Weighted Load Balancing

```nginx
upstream backend {
    server 127.0.0.1:3000 weight=3;
    server 127.0.0.1:3001 weight=1;
}
```

✔ Server with higher weight gets more traffic

---

## 7. Failover Handling

```nginx
upstream backend {
    server 127.0.0.1:3000 max_fails=3 fail_timeout=30s;
    server 127.0.0.1:3001;
}
```

* `max_fails`: number of failed attempts
* `fail_timeout`: time before retry

---

## 8. Proxy Headers (Important)

```nginx
location / {
    proxy_pass http://backend;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
}
```

✔ Preserves client request information

---

## 9. Reload NGINX

```bash
sudo nginx -t     # test configuration
sudo systemctl reload nginx
```

---

## 10. Testing Load Balancing

Start backend servers:

```bash
node app1.js   # runs on port 3000
node app2.js   # runs on port 3001
```

Test:

```bash
curl http://localhost
```

✔ Response should switch between servers

---

## 11. Logging

```nginx
access_log /var/log/nginx/access.log;
```

✔ Helps in debugging and monitoring

---

## 12. Timeout Configuration

```nginx
proxy_connect_timeout 5s;
proxy_read_timeout 10s;
```

✔ Prevents hanging requests

---

## 13. Connection Limiting

```nginx
limit_conn_zone $binary_remote_addr zone=addr:10m;
```

✔ Protects from overload / DDoS

---

## 14. Common Errors & Fixes

| Problem             | Solution                    |
| ------------------- | --------------------------- |
| 502 Bad Gateway     | Backend server not running  |
| Config error        | Run `nginx -t`              |
| Port already in use | Change port or stop process |

---

## 15. Production Tips

* Use HTTPS (SSL setup)
* Use Docker or Kubernetes
* Monitor using Prometheus + Grafana
* Scale backend servers dynamically

---

## 16. Summary

Steps:

1. Install NGINX
2. Configure upstream servers
3. Choose load balancing method
4. Add proxy settings
5. Reload NGINX

✔ Your load balancer is ready 
