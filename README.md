# 🚀 DevOps Docker EC2 Project

Dockerized static web application deployed on AWS EC2

---

## 📌 Objective

The objective of this project is to deploy a simple static web application inside a Docker container on a Linux-based AWS EC2 instance and expose it to the internet for external access. This validates understanding of Linux, Docker, networking, and basic infrastructure setup.

---

## 🧱 Architecture

```
Client (Browser)
↓
Internet
↓
Public IP (52.63.222.35:8080)
↓
AWS EC2 (Ubuntu Linux Server)
↓
Docker Engine
↓
Container (nginx)
↓
Static HTML Page
```

---

## 🖥️ System Requirements

* AWS Account with billing enabled
* EC2 instance (Ubuntu 22.04/24.04)
* SSH client (PowerShell / Terminal)
* Internet connection
* Basic knowledge of Linux commands

---

## ⚙️ Setup and Execution Steps

### 1. Launch EC2 Instance

* Platform: AWS EC2
* OS: Ubuntu
* Instance Type: t3.micro

---

### 2. Configure Security Group

Allow the following inbound rules:

| Port | Purpose         |
| ---- | --------------- |
| 22   | SSH Access      |
| 8080 | Web Application |

---

### 3. Connect via SSH

```bash
ssh -i devops-key.pem ubuntu@<public-ip>
```

---

### 4. Install Docker

```bash
sudo apt update
sudo apt install docker.io -y
sudo systemctl start docker
```

---

### 5. Create Application Files

```bash
mkdir app
cd app
nano index.html
```

---

### 6. Create Dockerfile

```bash
nano Dockerfile
```

---

### 7. Build Docker Image

```bash
sudo docker build -t devops-app .
```

---

### 8. Run Docker Container

```bash
sudo docker run -d -p 8080:80 --name myapp devops-app
```

---

### 9. Verify Deployment

```bash
sudo docker ps
sudo docker images
```

---

## 🌐 Access the Application

Open in browser:

```
http://<public-ip>:8080
```

---

## 📊 Evidence

### Running Containers

```bash
docker ps
```

### Available Images

```bash
docker images
```

### Local Access Test

```bash
curl http://localhost:8080
```

### Public Access Test

```bash
curl http://<public-ip>:8080
```

### Container Logs

```bash
docker logs myapp
```

---

## 🌐 Networking Explanation

The application runs inside a Docker container on port **80**. This port is mapped to port **8080** on the EC2 host using Docker port mapping (`-p 8080:80`).

The AWS Security Group allows inbound traffic on port **8080**, enabling external access through the public IP address.

---

## 🔄 Request Flow

```
Browser → Internet → EC2 Public IP → Port 8080 → Docker → nginx → HTML Page
```

---

## ⚖️ Architecture Decision

AWS EC2 was chosen over tunneling tools like ngrok because it provides a persistent, production-like environment with full control over networking and infrastructure. Docker ensures portability and consistency of the application.

---

## 🛠️ Troubleshooting

### 1. SSH Connection Timeout

* Cause: Port 22 blocked
* Solution: Enable SSH in security group

### 2. Application Not Accessible

* Cause: Port 8080 not open
* Solution: Add inbound rule for port 8080

### 3. Docker Permission Denied

* Cause: User not in docker group
* Solution:

```bash
sudo docker run ...
```

### 4. Container Not Running

```bash
docker logs myapp
```

---

## ⚖️ Tradeoffs

### AWS vs ngrok

* AWS → Persistent, scalable, real-world infrastructure
* ngrok → Temporary, less control

### VM vs Local Machine

* VM → External accessibility and isolation
* Local → Limited exposure

### nginx vs Custom Server

* nginx → Lightweight, fast, optimized for static content
* Custom server → Flexible but adds unnecessary complexity

---

## 📚 Key Learnings

* Understanding of cloud infrastructure using AWS EC2
* Hands-on experience with Linux command-line operations
* Practical knowledge of Docker (images, containers, Dockerfile)
* Understanding of networking concepts such as ports and IP addressing
* Experience deploying and exposing applications to the internet

---

## 🚀 Future Improvements

* Use Docker Compose for multi-container applications
* Implement HTTPS using SSL certificates
* Deploy using Kubernetes for scalability
* Automate deployment using CI/CD pipelines
* Attach a custom domain name

---

## 🔑 Access Details

* Public IP: 52.63.222.35
* Port: 8080
* URL: http://52.63.222.35:8080

---

## 📌 Conclusion

Successfully deployed a containerized static web application on AWS EC2 and exposed it to the internet. This project demonstrates foundational DevOps skills including cloud provisioning, containerization, networking, and deployment.
