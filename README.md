# 🚀 AWS CI/CD Pipeline

![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Java](https://img.shields.io/badge/java-%23ED8B00.svg?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white)

A production-ready **CI/CD pipeline** built on AWS that automates the build, test, and deployment lifecycle of a Spring Boot microservice. Designed to demonstrate real-world DevOps practices including containerization, infrastructure-as-code, and automated deployments.

---

## 📐 Architecture Overview

```
Developer Push → GitHub → GitHub Actions → Docker Build → ECR → ECS Fargate
                                ↓
                                                         Unit & Integration Tests
                                                                                         ↓
                                                                                                             AWS CodePipeline (optional stage)
                                                                                                                                             ↓
                                                                                                                                                                  Deploy to ECS / Elastic Beanstalk
                                                                                                                                                                  ```
                                                                                                                                                                  
                                                                                                                                                                  ---
                                                                                                                                                                  
                                                                                                                                                                  ## 🛠️ Tech Stack
                                                                                                                                                                  
                                                                                                                                                                  | Layer | Technology |
                                                                                                                                                                  |---|---|
                                                                                                                                                                  | Application | Java 17, Spring Boot 3.x |
                                                                                                                                                                  | Containerization | Docker |
                                                                                                                                                                  | Container Registry | AWS ECR |
                                                                                                                                                                  | Orchestration | AWS ECS Fargate |
                                                                                                                                                                  | CI/CD | GitHub Actions |
                                                                                                                                                                  | Infrastructure | AWS CloudFormation / Terraform |
                                                                                                                                                                  | Monitoring | AWS CloudWatch |
                                                                                                                                                                  | Secrets | AWS Secrets Manager |
                                                                                                                                                                  
                                                                                                                                                                  ---
                                                                                                                                                                  
                                                                                                                                                                  ## ✨ Features
                                                                                                                                                                  
                                                                                                                                                                  - ✅ Automated build and test on every push
                                                                                                                                                                  - ✅ Docker image build and push to AWS ECR
                                                                                                                                                                  - ✅ Zero-downtime rolling deployment to ECS Fargate
                                                                                                                                                                  - ✅ Environment-based configuration (dev / staging / prod)
                                                                                                                                                                  - ✅ CloudWatch logs and alarms integration
                                                                                                                                                                  - ✅ Secrets managed via AWS Secrets Manager
                                                                                                                                                                  
                                                                                                                                                                  ---
                                                                                                                                                                  
                                                                                                                                                                  ## 🚦 Pipeline Stages
                                                                                                                                                                  
                                                                                                                                                                  1. **Source** – Code pushed to GitHub triggers the pipeline
                                                                                                                                                                  2. **Build** – Maven builds the JAR; Docker image is created
                                                                                                                                                                  3. **Test** – Unit tests and integration tests run automatically
                                                                                                                                                                  4. **Push** – Docker image tagged and pushed to AWS ECR
                                                                                                                                                                  5. **Deploy** – ECS service updated with new task definition (rolling update)
                                                                                                                                                                  
                                                                                                                                                                  ---
                                                                                                                                                                  
                                                                                                                                                                  ## 🏁 Getting Started
                                                                                                                                                                  
                                                                                                                                                                  ### Prerequisites
                                                                                                                                                                  
                                                                                                                                                                  - Java 17+
                                                                                                                                                                  - Docker
                                                                                                                                                                  - AWS CLI configured (`aws configure`)
                                                                                                                                                                  - An AWS account with ECS, ECR, and IAM permissions
                                                                                                                                                                  
                                                                                                                                                                  ### Local Setup
                                                                                                                                                                  
                                                                                                                                                                  ```bash
                                                                                                                                                                  # Clone the repository
                                                                                                                                                                  git clone https://github.com/ShashiReddy5/aws-cicd-pipeline.git
                                                                                                                                                                  cd aws-cicd-pipeline
                                                                                                                                                                  
                                                                                                                                                                  # Build the project
                                                                                                                                                                  mvn clean install
                                                                                                                                                                  
                                                                                                                                                                  # Run locally with Docker
                                                                                                                                                                  docker build -t aws-cicd-pipeline .
                                                                                                                                                                  docker run -p 8080:8080 aws-cicd-pipeline
                                                                                                                                                                  ```
                                                                                                                                                                  
                                                                                                                                                                  ### Deploy to AWS
                                                                                                                                                                  
                                                                                                                                                                  ```bash
                                                                                                                                                                  # Push image to ECR
                                                                                                                                                                  aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <account-id>.dkr.ecr.us-east-1.amazonaws.com
                                                                                                                                                                  docker tag aws-cicd-pipeline:latest <account-id>.dkr.ecr.us-east-1.amazonaws.com/aws-cicd-pipeline:latest
                                                                                                                                                                  docker push <account-id>.dkr.ecr.us-east-1.amazonaws.com/aws-cicd-pipeline:latest
                                                                                                                                                                  ```
                                                                                                                                                                  
                                                                                                                                                                  ---
                                                                                                                                                                  
                                                                                                                                                                  ## 📁 Project Structure
                                                                                                                                                                  
                                                                                                                                                                  ```
                                                                                                                                                                  aws-cicd-pipeline/
                                                                                                                                                                  ├── src/
                                                                                                                                                                  │   ├── main/java/com/shashi/pipeline/
                                                                                                                                                                  │   └── test/
                                                                                                                                                                  ├── .github/
                                                                                                                                                                  │   └── workflows/
                                                                                                                                                                  │       └── ci-cd.yml          # GitHub Actions pipeline definition
                                                                                                                                                                  ├── Dockerfile
                                                                                                                                                                  ├── buildspec.yml              # AWS CodeBuild spec
                                                                                                                                                                  ├── taskdef.json               # ECS Task Definition
                                                                                                                                                                  └── README.md
                                                                                                                                                                  ```
                                                                                                                                                                  
                                                                                                                                                                  ---
                                                                                                                                                                  
                                                                                                                                                                  ## 👤 Author
                                                                                                                                                                  
                                                                                                                                                                  **Shashidhar Reddy**
                                                                                                                                                                  - GitHub: [@ShashiReddy5](https://github.com/ShashiReddy5)
                                                                                                                                                                  - LinkedIn: [linkedin.com/in/shashidhar-reddy](https://linkedin.com/in/shashidhar-reddy)
                                                                                                                                                                  
                                                                                                                                                                  ---
                                                                                                                                                                  
                                                                                                                                                                  ⭐ If you find this project useful, please give it a star!
