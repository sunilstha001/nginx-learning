# Reverse Proxy with Node.js using NGINX (EC2 Deployment)

In production environments, Node.js applications are usually deployed behind **NGINX reverse proxy**.

Instead of exposing the Node.js server directly to the internet, **NGINX handles incoming requests and forwards them to the Node.js application**.

```
User (Browser)
      │
      ▼
NGINX Reverse Proxy (EC2 Server)
      │
      ▼
Node.js Application (Port 3000)
```

This setup improves **security, scalability, and performance**.

---

# Step 1: Connect to EC2 Server

First connect to your EC2 instance using SSH.

```
ssh -i your-key.pem ubuntu@your-ec2-public-ip
```

Example:

```
ssh -i myserver.pem ubuntu@3.110.25.10
```

---

# Step 2: Update the Server

Before installing software, update the packages.

```
sudo apt update
sudo apt upgrade -y
```

---

# Step 3: Install Node.js

Install Node.js and npm.

```
sudo apt install nodejs npm -y
```

Check installation:

```
node -v
npm -v
```

---

# Step 4: Create Node.js Application

Create a new project directory.

```
mkdir node-app
cd node-app
```

Initialize the project.

```
npm init -y
```

Install Express.

```
npm install express
```

---

# Step 5: Create Node.js Server

Create a file called:

```
server.js
```

Example server:

```javascript
const express = require("express");
const app = express();

app.get("/", (req, res) => {
  res.send("Hello from Node.js running on EC2");
});

app.listen(3000, () => {
  console.log("Server running on port 3000");
});
```

Start the server:

```
node server.js
```

Your Node.js server will run on:

```
http://your-ec2-ip:3000
```

But exposing this port publicly is **not recommended for production**, so we use **NGINX reverse proxy**.

---

# Step 6: Install NGINX

Install NGINX on the EC2 instance.

```
sudo apt install nginx -y
```

Check status:

```
sudo systemctl status nginx
```

Start NGINX:

```
sudo systemctl start nginx
```

Enable auto start:

```
sudo systemctl enable nginx
```

Now visiting your EC2 IP should show the **NGINX welcome page**.

```
http://your-ec2-ip
```

---

# Step 7: Configure Reverse Proxy

Edit the NGINX configuration file.

```
sudo nano /etc/nginx/sites-available/default
```

Update the server block:

```
server {
    listen 80;

    server_name _;

    location / {
        proxy_pass http://localhost:3000;

        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

Explanation:

| Directive          | Purpose                            |
| ------------------ | ---------------------------------- |
| proxy_pass         | forwards request to Node.js server |
| proxy_set_header   | keeps original request headers     |
| proxy_http_version | ensures proper HTTP version        |

---

# Step 8: Test NGINX Configuration

Before restarting NGINX, test the configuration.

```
sudo nginx -t
```

If successful, restart NGINX.

```
sudo systemctl restart nginx
```

---

# Step 9: Test the Reverse Proxy

Now open your browser and visit:

```
http://your-ec2-ip
```

Request flow:

```
User → NGINX (port 80) → Node.js (port 3000)
```

You should see:

```
Hello from Node.js running on EC2
```

---

# Production Architecture Example

In real production systems, multiple Node.js servers run behind NGINX.

```
                ┌── Node.js Server 1
User → NGINX ───┼── Node.js Server 2
                └── Node.js Server 3
```

NGINX distributes traffic between servers to handle high traffic loads.

---

# Summary

Using NGINX as a reverse proxy on EC2 provides:

* better security
* improved performance
* centralized request handling
* scalable architecture
* production-ready deployment

This setup is commonly used in **cloud infrastructure and DevOps environments**.
