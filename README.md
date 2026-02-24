# 🚀 MEAN Stack CRUD Application – DevOps Deployment

## 📌 Project Overview

This project is a full-stack MEAN (MongoDB, Express, Angular, Node.js) CRUD application containerized using Docker and deployed on AWS EC2 with Nginx reverse proxy and CI/CD automation using GitHub Actions.

The goal of this project is to demonstrate:

- Containerization using Docker
- Multi-container orchestration using Docker Compose
- Cloud deployment on AWS EC2
- Reverse proxy setup using Nginx
- CI/CD pipeline using GitHub Actions
- Production-style deployment architecture

---

# 🏗️ Architecture Overview
---

# 🐳 Docker Setup

## Backend Dockerfile
- Node 18 base image
- Installs dependencies
- Exposes port 3000
- Starts application using `npm start`

## Frontend Dockerfile
- Multi-stage build
- Node image for build
- Nginx image for production serving
- Exposes port 80 inside container

---

# 📦 Docker Compose Configuration

The application uses 3 services:

- mongo
- backend
- frontend

```yaml
version: '3.8'

services:

  mongo:
    image: mongo:6
    container_name: mongo
    restart: always
    volumes:
      - mongo-data:/data/db

  backend:
    image: nithin4263/mean-backend:latest
    container_name: backend
    restart: always
    environment:
      - MONGO_URI=mongodb://mongo:27017/ddtask
    depends_on:
      - mongo

  frontend:
    image: nithin4263/mean-frontend:latest
    container_name: frontend
    restart: always
    depends_on:
      - backend

volumes:
  mongo-data:
☁️ AWS EC2 Deployment
EC2 Configuration
Instance Type: t2.micro
OS: Ubuntu 22.04 LTS
Security Group Ports Open:
22 (SSH)
80 (HTTP)
Steps Performed
Installed Docker & Docker Compose
Pulled images from Docker Hub
Started services using docker-compose
Installed and configured Nginx as reverse proxy
Exposed application via Port 80
Application URL:
http://107.20.44.254/
🌐 Nginx Reverse Proxy Configuration
Copy code

server {
    listen 80;

    location / {
        proxy_pass http://localhost:4200;
    }

    location /api/ {
        proxy_pass http://localhost:3000/;
    }
}
Nginx routes:
/ → Angular frontend
/api → Backend API
🔄 CI/CD Pipeline (GitHub Actions)
The CI/CD pipeline performs:
Trigger on push to main
Build backend Docker image
Build frontend Docker image
Push images to Docker Hub
SSH into EC2
Pull latest images
Restart containers automatically
Workflow file: .github/workflows/deploy.yml
🛠️ How to Run Locally
Bash
Copy code
git clone <repo-url>
cd project-folder
docker-compose up -d
Access:
Frontend: http://localhost:4200�
Backend: http://localhost:3000�
📸 Screenshots Included
Docker containers running
AWS EC2 instance configuration
Nginx configuration
GitHub Actions CI/CD execution
Application UI working
🔒 Production Considerations
Only port 80 exposed publicly
MongoDB not exposed publicly
Containers configured with restart policy
CI/CD ensures automatic deployment
🧠 Key DevOps Concepts Demonstrated
Containerization
Image registry (Docker Hub)
Infrastructure on Cloud
Reverse proxy configuration
CI/CD automation
Environment variable configuration
Multi-container architecture

---

# 🔥 What You Should Do Next

Now:

1️⃣ Replace `<EC2-Public-IP>` with your real IP  
2️⃣ Add screenshots (very important)  
3️⃣ Push README  
4️⃣ Test CI/CD one more time  

---

# 🎯 Optional Upgrade (Very Impressive)

Add these sections:

- Architecture Diagram Image
- Cost Optimization Explanation
- Future Improvements
- Security Improvements

---

If you want, I can now:

- 🔥 Make a next-level README (interview winning version)
- 🔥 Create architecture diagram image
- 🔥 Review your repository professionally
- 🔥 Prepare submission explanation for interview

Tell me what you want next 👌🔥
