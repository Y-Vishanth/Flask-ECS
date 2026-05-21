
# 🚀 Flask Application Deployment on Amazon ECS using GitHub Actions

This project demonstrates a complete production-style CI/CD pipeline for deploying a Dockerized Flask application to Amazon ECS (Fargate) using GitHub Actions and Amazon ECR.

The project includes:
- Docker containerization
- Amazon ECR image storage
- ECS Fargate deployment
- Application Load Balancer integration
- Automated CI/CD pipeline with GitHub Actions

---

# 📌 Architecture Overview

```text
Developer Pushes Code to GitHub
              ↓
GitHub Actions CI/CD Pipeline
              ↓
Docker Image Build
              ↓
Push Image to Amazon ECR
              ↓
Register New ECS Task Definition Revision
              ↓
Deploy Updated Task to ECS Service
              ↓
Application Load Balancer Routes Traffic
              ↓
Flask Application Becomes Live
````

---

# 🛠️ Tech Stack

| Component               | Technology                      |
| ----------------------- | ------------------------------- |
| Backend Application     | Flask (Python)                  |
| Containerization        | Docker                          |
| CI/CD                   | GitHub Actions                  |
| Cloud Provider          | AWS                             |
| Container Registry      | Amazon ECR                      |
| Container Orchestration | Amazon ECS (Fargate)            |
| Load Balancer           | Application Load Balancer (ALB) |

---

# 📂 Project Structure

```text
Flask-ECS/
│
├── app.py
├── requirements.txt
├── Dockerfile
├── ecs-task-def.json
│
├── .github/
│   └── workflows/
│       └── deploy.yaml
│
└── README.md
```

---

# ⚙️ Features

* Automated deployment on every push to `main`
* Docker image build and push to ECR
* ECS task definition revision updates
* Automatic ECS service deployment
* Application Load Balancer integration
* Health checks with rollback support
* Production-style deployment workflow

---

# 🔐 AWS Resources Used

## Amazon ECS

Used to run containerized Flask application using Fargate.

## Amazon ECR

Stores Docker images built by GitHub Actions.

## Application Load Balancer (ALB)

Routes incoming HTTP traffic to healthy ECS tasks.

## GitHub Actions

Handles CI/CD automation pipeline.

---

# 🐳 Docker Workflow

The Flask application is containerized using Docker.

## Build Docker Image

```bash
docker build -t my-flask-app .
```

## Run Docker Container Locally

```bash
docker run -p 5000:5000 my-flask-app
```

---

# 🚀 CI/CD Workflow

The deployment pipeline is defined in:

```text
.github/workflows/deploy.yaml
```

Pipeline steps:

1. Checkout source code
2. Configure AWS credentials
3. Login to Amazon ECR
4. Build Docker image
5. Push image to ECR
6. Fetch ECS task definition
7. Update image URI
8. Register new ECS task revision
9. Deploy updated revision to ECS service

---

# 🔑 GitHub Secrets Required

Go to:

```text
GitHub Repository
→ Settings
→ Secrets and variables
→ Actions
```

Add the following secrets:

| Secret Name           | Description    |
| --------------------- | -------------- |
| AWS_ACCESS_KEY_ID     | AWS access key |
| AWS_SECRET_ACCESS_KEY | AWS secret key |
| AWS_ACCOUNT_ID        | AWS account ID |

---

# ☁️ AWS Infrastructure Setup

## ECS Cluster

Example:

```text
flask-cluster1
```

## ECS Service

Example:

```text
flask-task-service
```

## ECR Repository

Example:

```text
my-flask-app
```

## Task Definition

Example:

```text
flask-task
```

---

# 🌐 Load Balancer Configuration

Application Load Balancer is configured with:

* HTTP Listener on Port 80
* ECS Target Group
* Health Checks Enabled
* Multiple Availability Zones
* Public Subnets Attached

---

# 🔥 Deployment Trigger

## Automatic Deployment

Every push to `main` branch triggers deployment automatically.

```bash
git push origin main
```

---

# 📊 ECS Deployment Features

* Rolling deployments
* Automatic health checks
* Automatic rollback on failure
* Target group validation
* Load balancer integration

---

# 🧠 Issues Faced During Deployment

During deployment, the ECS service initially rolled back because:

```text
Target is in an Availability Zone that is not enabled for the load balancer
```

### Root Cause

The Application Load Balancer was not attached to all ECS subnets.

### Fix

Added all ECS service subnets to the ALB Availability Zones configuration.

After fixing networking configuration:

* ECS deployment succeeded
* Health checks passed
* Load balancer started routing traffic correctly

---

# ✅ Successful Deployment Verification

Deployment was verified by checking:

* ECS task health
* ECS service events
* ALB target group health
* ECS task revisions
* GitHub Actions logs
* Live application access through ALB DNS

---

# 🌍 Access Application

Access the Flask application using:

```text
http://<ALB-DNS-NAME>
```

Example:

```text
http://ecs-alb-xxxxxxxx.us-east-1.elb.amazonaws.com
```

---

# 🏆 Key Learnings

This project helped in understanding:

* Docker containerization
* ECS Fargate deployments
* GitHub Actions CI/CD
* ECR image management
* Application Load Balancer
* ECS task definitions
* Health checks and rollbacks
* AWS networking and subnets
* Production deployment debugging

---

# 📌 Future Improvements

* HTTPS with ACM
* Custom domain with Route53
* Terraform Infrastructure as Code
* ECS Auto Scaling
* Multi-environment deployment (Dev/QA/Prod)
* Blue-Green deployment strategy

---

# 👨‍💻 Author

Vishanth

```
```
