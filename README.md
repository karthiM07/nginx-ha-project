Here’s a clean, professional **README.md** you can use for your Git repo:

---

# 🚀 NGINX High Availability Setup with Docker

This project demonstrates a **high availability (HA) web architecture** using Docker, simulating a real-world cloud setup similar to AWS.

It uses:

* **NGINX as a Load Balancer**
* **Multiple backend NGINX servers**
* **Docker Compose for orchestration**

---

## 📌 Architecture Overview

```
Browser
   │
NGINX Load Balancer (container)
   │
 ┌───────────────┬───────────────┐
 │               │
NGINX Server 1   NGINX Server 2
(container)     (container)
Serving HTML    Serving HTML
```

* Requests are distributed between backend servers.
* If one server goes down, traffic is automatically routed to the other.

---

## 📁 Project Structure

```
nginx-ha-project
│
├── docker-compose.yml
│
├── loadbalancer
│   └── nginx.conf
│
├── nginx1
│   └── index.html
│
└── nginx2
    └── index.html
```

---

## ⚙️ Setup Instructions

### 1. Clone the Repository

```bash
git clone <your-repo-url>
cd nginx-ha-project
```

---

### 2. Start the Application

```bash
docker compose up -d
```

---

### 3. Access the Application

Open your browser and go to:

```
http://localhost:8080
```

Refresh multiple times to see load balancing in action.

---

## 🔁 Load Balancing Behavior

* Requests are distributed between:

  * **NGINX Server 1**
  * **NGINX Server 2**
* Default strategy: **Round Robin**

---

## 🧪 High Availability Test

### Step 1: Stop one backend server

```bash
docker stop nginx-server-1
```

### Step 2: Refresh browser

* The application will still work.
* Traffic will be routed to **NGINX Server 2**.

---

## 🧠 How It Works

### Load Balancer Config (`nginx.conf`)

```nginx
upstream backend_servers {
    server nginx1:80;
    server nginx2:80;
}

server {
    listen 80;

    location / {
        proxy_pass http://backend_servers;
    }
}
```

* `upstream` defines backend servers
* `proxy_pass` forwards incoming requests

---

## ☁️ AWS Architecture Mapping

| Docker Component    | AWS Equivalent            |
| ------------------- | ------------------------- |
| Docker Network      | VPC                       |
| NGINX Load Balancer | Application Load Balancer |
| nginx1 / nginx2     | EC2 Instances             |
| HTML Volume         | EBS / Instance Storage    |
| localhost:8080      | ALB Public DNS            |

---

## 🌍 Real-World Equivalent Architecture

```
User Browser
     │
DNS (Route53)
     │
Application Load Balancer
     │
Target Group
     │
 ┌───────────────┬───────────────┐
 │               │
EC2 Instance 1  EC2 Instance 2
NGINX           NGINX
Website         Website
```

---

## 📦 Technologies Used

* Docker
* Docker Compose
* NGINX

---

## ✅ Key Concepts Demonstrated

* Load Balancing
* High Availability
* Reverse Proxy
* Container Networking
* Microservice Simulation

---

## 🚀 Future Improvements

* Add health checks
* Implement auto-scaling simulation
* Use HTTPS with SSL
* Add monitoring (Prometheus + Grafana)

---

