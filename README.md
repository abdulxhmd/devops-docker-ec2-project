# devops-docker-ec2-project
Dockerized static web application deployed on AWS EC2

## 📌 Objective
The objective of this project is to deploy a simple static web application inside a Docker container on a Linux-based AWS EC2 instance and expose it to the internet for external access.

## 🧱 Architecture
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

---

## 🖥️ System Requirements
- AWS Account with billing enabled
- EC2 instance (Ubuntu 22.04/24.04)
- SSH client (PowerShell / Terminal)
- Internet connection
- Basic knowledge of Linux commands

---

## ⚙️ Setup and Execution Steps

###1. Launch EC2 Instance
- Platform: AWS EC2
- OS: Ubuntu
- Instance Type: t3.micro

###2. Configure Security Group
Allow the following inbound rules:

| Port | Purpose |
|------|--------|
| 22   | SSH Access |
| 8080 | Web Application |

---

###3. Connect via SSH
```bash
ssh -i devops-key.pem ubuntu@<public-ip>

---

### 4. Install Docker
sudo apt update
sudo apt install docker.io -y
sudo systemctl start docker

---

### 5. Create Application Files
mkdir app
cd app
nano index.html

---

### 6. Create Dockerfile
nano Dockerfile

---

### 7. Build Docker Image
sudo docker build -t devops-app .

---

### 8. Run Docker Container
sudo docker run -d -p 8080:80 --name myapp devops-app

---

### 9. Verify Deployment
sudo docker ps
sudo docker images

---

## 🌐 Access the Application
Open in browser : http://<public-ip>:8080

---

## 📊 Evidence
### Running Containers
docker ps

---

## Available Images
docker images

---

## 🌐 Networking Explanation
The application runs inside a Docker container on port 80. This port is mapped to port 8080 on the EC2 host machine using Docker port mapping. The AWS security group allows inbound traffic on port 8080, enabling external access via the public IP address.

---

## 🔄 Request Flow
Browser → Internet → EC2 Public IP → Port 8080 → Docker → nginx → HTML Page

---

## 🛠️ Troubleshooting
1. SSH Connection Timeout
Cause: Port 22 blocked
Solution: Enable SSH in security group
2. Application Not Accessible
Cause: Port 8080 not open
Solution: Add inbound rule for port 8080
3. Docker Permission Denied
Cause: User not in docker group
Solution: sudo docker run ...
4. Container Not Running
Solution: docker logs <container-id>

---

## ⚖️ Tradeoffs
AWS vs ngrok
AWS provides persistent infrastructure and real-world deployment
ngrok is temporary and not production-ready
VM vs Local Machine
VM provides isolation and production-like environment
Local setup lacks external accessibility
nginx vs Custom Server
nginx is optimized for static content and high performance
Custom server provides flexibility but adds complexity

---

## 📚 Key Learnings
Understanding of cloud infrastructure using AWS EC2
Hands-on experience with Linux command-line operations
Practical knowledge of Docker (images, containers, Dockerfile)
Understanding of networking concepts like ports and IP addressing
Experience with deploying and exposing applications to the internet

---

## 🚀 Future Improvements
Use Docker Compose for multi-container applications
Implement HTTPS using SSL certificates
Deploy using Kubernetes for scalability
Automate deployment using CI/CD pipelines
Attach a custom domain name

---

## 📌 Conclusion
Successfully deployed a containerized static web application on AWS EC2 and exposed it to the internet. This project demonstrates foundational DevOps skills including cloud provisioning, containerization, networking, and deployment.
