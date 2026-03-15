# Reverse Proxy for React App using NGINX (EC2 Deployment)

In production, React applications are usually built into **static files** and served by **NGINX**.
When deploying on an EC2 server, NGINX acts as a **web server and reverse proxy**.

```
User (Browser)
       │
       ▼
NGINX (EC2 Server)
       │
       ▼
React Build Files (Static)
```

NGINX serves the React application efficiently and can also forward API requests to backend services.

---

# Step 1: Connect to EC2 Instance

Connect to your EC2 server using SSH.

```
ssh -i your-key.pem ubuntu@your-ec2-public-ip
```

Example:

```
ssh -i myserver.pem ubuntu@18.205.22.100
```

---

# Step 2: Update the Server

Update system packages before installing anything.

```
sudo apt update
sudo apt upgrade -y
```

---

# Step 3: Install Node.js and npm

React applications require Node.js to build the project.

```
sudo apt install nodejs npm -y
```

Verify installation:

```
node -v
npm -v
```

---

# Step 4: Upload or Clone React Project

You can upload your project or clone it from GitHub.

Example using Git:

```
git clone https://github.com/your-username/react-app.git
cd react-app
```

Install dependencies:

```
npm install
```

---

# Step 5: Build the React Application

React must be compiled into optimized static files.

```
npm run build
```

This command creates a **build folder** containing:

```
build/
 ├── index.html
 ├── static/
 └── assets
```

These files are ready for production deployment.

---

# Step 6: Install NGINX

Install NGINX on the EC2 server.

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

Enable auto-start:

```
sudo systemctl enable nginx
```

---

# Step 7: Move React Build Files

Copy the React build files to the NGINX web directory.

```
sudo rm -rf /var/www/html/*
sudo cp -r build/* /var/www/html/
```

This directory is where NGINX serves website files.

---

# Step 8: Configure NGINX for React

Edit the default NGINX configuration.

```
sudo nano /etc/nginx/sites-available/default
```

Update the server configuration:

```
server {
    listen 80;

    server_name _;

    root /var/www/html;
    index index.html;

    location / {
        try_files $uri /index.html;
    }
}
```

Explanation:

| Directive | Purpose                             |
| --------- | ----------------------------------- |
| root      | location of React build files       |
| index     | main entry file                     |
| try_files | ensures React Router works properly |

React applications use **client-side routing**, so this configuration ensures all routes return `index.html`.

---

# Step 9: Test NGINX Configuration

Before restarting NGINX, test the configuration.

```
sudo nginx -t
```

If the configuration is correct, restart NGINX.

```
sudo systemctl restart nginx
```

---

# Step 10: Access the React App

Open your browser and visit:

```
http://your-ec2-public-ip
```

Your React application should now load.

---

# React + Backend Reverse Proxy (Optional)

If your React app needs to communicate with a backend (Node.js API), NGINX can proxy API requests.

Example configuration:

```
server {
    listen 80;

    root /var/www/html;
    index index.html;

    location / {
        try_files $uri /index.html;
    }

    location /api {
        proxy_pass http://localhost:3000;
    }
}
```

Request flow:

```
User → NGINX → React Static Files
User → NGINX → Node.js API
```

This allows React frontend and backend APIs to run on the same server.

---

# Production Architecture Example

```
User
  │
  ▼
NGINX (EC2)
  │
  ├── React Static Files
  └── Node.js Backend API
```

NGINX acts as the **main entry point** for the application.

---

# Summary

Deploying React with NGINX on EC2 provides:

* fast static file serving
* better performance
* secure architecture
* easy integration with backend APIs
* scalable production deployment

This architecture is commonly used in **MERN stack deployments and cloud infrastructure**.
