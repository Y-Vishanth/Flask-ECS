# 🚀 Flask-ECS Deployment

This repository demonstrates how to deploy a **Flask application** to **Amazon ECS (Fargate)** using **GitHub Actions** and **Amazon ECR**.

---

## ⚙️ Overview

- **Continuous Deployment**: Every push to the `main` branch triggers a build and deploy.
- **Manual Trigger**: You can also run the workflow manually from the GitHub Actions tab.
- **Containerization**: The app is packaged into a Docker image and stored in Amazon ECR.
- **Deployment**: ECS service is updated with the new task definition.

---

## 📂 Workflow

The full pipeline is defined in:
.github/workflows/deploy.yaml

Refer to this file for the exact steps (checkout, AWS credentials, ECR login, Docker build/push, ECS deploy).

---

## 🛠️ Requirements

- **AWS Setup**
  - ECS cluster (e.g., `flask-cluster`)
  - ECS service (e.g., `flask-service`)
  - ECR repository (e.g., `my-flask-app`)
  - IAM user with:
    - `AmazonECS_FullAccess`
    - `AmazonEC2ContainerRegistryFullAccess`

- **GitHub Secrets**
  - `AWS_ACCESS_KEY_ID`
  - `AWS_SECRET_ACCESS_KEY`

- **Task Definition**
  - Commit a valid `ecs-task-def.json` file in the repo root.

---

## 💻 Tech Stack

- **Application**: [Flask](https://flask.palletsprojects.com/) (Python web framework)  
- **Containerization**: [Docker](https://www.docker.com/)  
- **Cloud Provider**: [Amazon Web Services (AWS)](https://aws.amazon.com/)  
- **Container Registry**: [Amazon ECR](https://aws.amazon.com/ecr/)  
- **Orchestration**: [Amazon ECS (Fargate)](https://aws.amazon.com/ecs/)  
- **CI/CD**: [GitHub Actions](https://docs.github.com/en/actions)  
- **Infrastructure**: Task definitions (`ecs-task-def.json`) for ECS service updates  

---

## ✅ Usage

1. Push changes to `main` → workflow runs automatically.
2. Or trigger manually → go to **Actions → Deploy to ECS → Run workflow**.
3. ECS service updates with the new Docker image.

---

### 🎯 With this setup, your Flask app is continuously deployed to ECS with every commit.
