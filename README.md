
# Nginx Load Balancer with Node.js Apps using Docker

This project demonstrates how to set up an Nginx reverse proxy with SSL, load-balancing multiple Node.js applications running in Docker containers.

![Architecture Diagram](./nginx-crash-course.png)

## 🧾 Overview

- **Nginx** is configured to:
  - Load balance 3 Node.js apps using `least_conn` strategy
  - Redirect HTTP (port 8080) to HTTPS (port 443)
  - Use a self-signed SSL certificate

- **Docker Compose** is used to:
  - Run 3 instances of a Node.js app on different ports (3001, 3002, 3003)

## 🗂 Structure

- `sample.nginx.conf`: Nginx configuration file
- `Dockerfile`: Builds a simple Node.js app
- `docker-compose.yml`: Spins up 3 app containers

## ⚙️ How to Use

1. **Generate Self-Signed SSL Certificate:**
   ```bash
   openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
   -keyout private.key -out cert.crt


2. **Update `sample.nginx.conf`** with your certificate paths:

   ```nginx
   ssl_certificate cert.crt;
   ssl_certificate_key private.key;
   ```

3. **Start Docker Containers:**

   ```bash
   docker-compose up --build
   ```

4. **Run Nginx (on host machine):**

   ```bash
   sudo nginx -c /path/to/sample.nginx.conf
   ```

## 🌐 Access

* Visit `https://localhost` to see the load-balanced app
* HTTP (`http://localhost:8080`) auto-redirects to HTTPS

---

Feel free to customize `server.js` or `index.html` as needed.
