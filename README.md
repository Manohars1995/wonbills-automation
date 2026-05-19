# 🚀 Sample Billing Application Multi-Cloud DevOps Automation Setup Guide

## 🌐 Project Overview

**Sample Billing Application** is a cloud-based billing and business management platform deployed using a modern **Multi-Cloud DevOps Architecture**.

This project demonstrates:

* ✅ AWS Primary Infrastructure
* ✅ Azure Backup Infrastructure
* ✅ Jenkins CI/CD Automation
* ✅ GitHub Webhooks
* ✅ Docker Container Deployments
* ✅ SNS Email Notifications
* ✅ Route53 Failover Architecture
* ✅ Disaster Recovery (DR) Setup
* ✅ Multi-Cloud High Availability

---

# 🏗️ Architecture Overview

```text
Developer Push Code
        ↓
GitHub Repository
        ↓
GitHub Webhook Trigger
        ↓
Jenkins Pipeline
        ↓
Docker Build & Deployment
        ↓
AWS Primary Environment
        ↓
Azure Backup Environment
        ↓
SNS Email Notifications
        ↓
Route53 Health Monitoring
        ↓
Automatic Failover Ready
```

---

# ☁️ Technologies Used

| Technology | Purpose                         |
| ---------- | ------------------------------- |
| AWS EC2    | Primary Production Server       |
| Azure VM   | Backup Disaster Recovery Server |
| Jenkins    | CI/CD Automation                |
| Docker     | Containerization                |
| GitHub     | Source Code Management          |
| Route53    | DNS & Failover Routing          |
| AWS SNS    | Email Notifications             |
| Node.js    | Backend Runtime                 |
| React/Vite | Frontend Application            |
| Nginx      | Reverse Proxy                   |

---

# 📁 GitHub Repository Structure

```text
YOUR-PROJECT-NAME/
│
├── your-backend-service/
│   ├── Dockerfile
│   ├── package.json
│   ├── src/
│   └── .env
│
├── your-frontend-service/
│   ├── Dockerfile
│   ├── package.json
│   ├── src/
│   └── vite.config.js
│
├── Jenkinsfile-backend
├── Jenkinsfile-frontend
└── README.md
```

---

# 🔥 STEP 1 — Create AWS Primary Infrastructure

## ✅ Create EC2 Instance

### Configuration

| Setting        | Value                                    |
| -------------- | ---------------------------------------- |
| OS             | Ubuntu 22.04                             |
| Instance Type  | t2.medium                                |
| Storage        | 30 GB                                    |
| Security Group | Open Ports 22, 80, 443, 8080, 8014, 5176 |

---

## ✅ Install Required Software

```bash
sudo apt update && sudo apt upgrade -y

sudo apt install docker.io docker-compose git nginx nodejs npm openjdk-17-jdk awscli -y
```

---

## ✅ Install Jenkins

```bash
wget https://pkg.jenkins.io/debian-stable/binary/jenkins_2.504.1_all.deb

sudo dpkg -i jenkins_2.504.1_all.deb

sudo apt --fix-broken install -y
```

---

## ✅ Start Jenkins

```bash
sudo systemctl enable jenkins
sudo systemctl start jenkins
```

---

## ✅ Open Jenkins

```text
http://YOUR_AWS_PUBLIC_IP:8080
```

---

# 🔥 STEP 2 — Configure GitHub Webhook

## ✅ Create GitHub Repository

Example:

```text
https://github.com/your-organization/your-project
```

---

## ✅ Add Jenkins Webhook

GitHub Repository:

```text
Settings
 → Webhooks
 → Add Webhook
```

### Payload URL

```text
http://YOUR_AWS_PUBLIC_IP:8080/github-webhook/
```

### Content Type

```text
application/json
```

### Events

```text
Just push events
```

---

# 🔥 STEP 3 — Create Jenkins Pipeline

## ✅ Backend Pipeline

Features:

* Automatic code checkout
* Docker image build
* Container deployment
* Health check
* SNS notifications

---

## ✅ Frontend Pipeline

Features:

* Frontend Docker build
* Frontend container deployment
* Container verification
* Deployment notifications

---

# 🔥 STEP 4 — Docker Deployment

## ✅ Build Backend Docker Image

```bash
docker build -t your-backend-service .
```

---

## ✅ Run Backend Container

```bash
docker run -d \
--name your-backend-service \
-p 8014:8014 \
--restart unless-stopped \
your-backend-service
```

---

## ✅ Build Frontend Docker Image

```bash
docker build -t your-frontend-service .
```

---

## ✅ Run Frontend Container

```bash
docker run -d \
--name your-frontend-container \
-p 5176:5176 \
--restart unless-stopped \
your-frontend-service
```

---

# ☁️ STEP 5 — Create Azure Backup Infrastructure

## ✅ Create Azure VM

### Configuration

| Setting | Value                         |
| ------- | ----------------------------- |
| OS      | Ubuntu 22.04                  |
| VM Size | B1s                           |
| Ports   | 22, 80, 443, 8080, 8014, 5176 |

---

## ✅ Install Software

```bash
sudo apt update && sudo apt upgrade -y

sudo apt install docker.io docker-compose git nginx nodejs npm openjdk-17-jdk -y
```

---

## ✅ Install Jenkins in Azure

```bash
wget https://pkg.jenkins.io/debian-stable/binary/jenkins_2.504.1_all.deb

sudo dpkg -i jenkins_2.504.1_all.deb

sudo apt --fix-broken install -y
```

---

# 🔔 STEP 6 — Configure SNS Notifications

## ✅ Create SNS Topics

Topics Created:

```text
your-critical-alert-topic
your-dr-alert-topic
```

---

## ✅ Configure Email Subscriptions

```text
SNS
 → Topics
 → Create Subscription
```

### Protocol

```text
Email
```

### Notifications Sent

| Notification       | Purpose                   |
| ------------------ | ------------------------- |
| Deployment Started | Deployment initiated      |
| Deployment Success | Deployment completed      |
| Deployment Failed  | Deployment issue detected |
| AWS Failure        | AWS unhealthy             |
| Azure Activated    | DR environment activated  |

---

# 🌍 STEP 7 — Configure Route53 Failover

## ✅ Create Primary DNS Record

```text
your-domain.com → AWS IP
```

---

## ✅ Create Secondary DNS Record

```text
your-domain.com → Azure IP
```

---

## ✅ Configure Failover Routing

### Primary

```text
AWS Infrastructure
```

### Secondary

```text
Azure Backup Infrastructure
```

---

# ❤️ STEP 8 — Route53 Health Check

## ✅ Create Health Check

```text
https://your-domain.com/health
```

### Purpose

* Detect AWS failures
* Monitor application availability
* Prepare failover activation

---

# 🔄 Disaster Recovery Workflow

```text
AWS Healthy
    ↓
Traffic → AWS

AWS Failure
    ↓
Health Check Detects Failure
    ↓
Traffic → Azure Backup
    ↓
SNS Alerts Sent
```

---

# 📬 Professional Notification Flow

## Deployment Started

```text
Production deployment pipeline initiated successfully.
```

## Deployment Successful

```text
Production deployment completed successfully.
```

## Deployment Failed

```text
Production deployment failed. Immediate investigation required.
```

## AWS Failure

```text
AWS infrastructure failure detected.
```

## Azure DR Activated

```text
Azure backup environment activated successfully.
```

---

# 🔐 Security Best Practices

## Recommended Improvements

* Use AWS Secrets Manager
* Store secrets in Jenkins Credentials
* Enable HTTPS using Certbot
* Configure Nginx Reverse Proxy
* Restrict Security Group Access
* Enable CloudWatch Monitoring

---

# 📊 Project Features

| Feature                        | Status |
| ------------------------------ | ------ |
| AWS Production                 | ✅      |
| Azure Backup                   | ✅      |
| Jenkins Automation             | ✅      |
| Docker Deployment              | ✅      |
| GitHub Webhooks                | ✅      |
| SNS Notifications              | ✅      |
| Route53 Failover               | ✅      |
| Health Monitoring              | ✅      |
| Disaster Recovery Architecture | ✅      |

---

# 🚀 Final Result

This project demonstrates a complete enterprise-grade:

* Multi-Cloud Deployment Architecture
* DevOps CI/CD Automation
* High Availability Infrastructure
* Disaster Recovery Setup
* Auto Deployment System
* DNS Failover Architecture
* Cloud Monitoring & Notifications

---

# 👨‍💻 Author

**DevOps Cloud Team**

---

# ⭐ GitHub Showcase

This project can be used as a reference implementation for:

* DevOps Learning
* Multi-Cloud Architecture
* Jenkins Automation
* Disaster Recovery Design
* Production Deployment Pipelines
* Enterprise Infrastructure Setup
