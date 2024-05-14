https://drive.google.com/file/d/1Ob1zEvFRrUxDd0gpcVgNE8eJKudO8vjK/view?usp=sharing

![Alt-text](https://github.com/SFrank80/docker-project-2024-rentzone-app/blob/cbb0a87f769f284ab25b7a4e99adce65bc5ae938/Dynamic%20Rentzone%20Website%20with%20Docker%20ECR%20and%20ECS%20Completed.JPG)

![Alt-text](https://github.com/SFrank80/docker-project-2024-rentzone-app/blob/be1f31eb646e106a056537f45e9d0866a01657ad/Docker.Rent%20Zone.App%20Reference%20Architecture.JPG)

---

# Hosting a Dynamic Web Application on AWS with Docker

## Project Overview

This repository documents the deployment of a dynamic web application on Amazon Web Services (AWS), leveraging Docker for containerization and various AWS services for orchestration, scaling, and management. The architecture is designed to provide high availability, scalability, and resilience through AWS's robust cloud infrastructure.

## Architecture Summary

The application is hosted within a well-architected AWS environment that uses:

- **Amazon ECS (Elastic Container Service)** for managing Docker containers in a highly scalable manner.
- **Amazon RDS (Relational Database Service)** for a managed database experience, ensuring durability and high availability.
- **Amazon EFS (Elastic File System)** to provide scalable file storage for containers.
- **AWS Fargate** for running containers without having to manage servers or clusters.
- **Application Load Balancer (ALB)** to distribute incoming application traffic across multiple containers.
- **Auto Scaling** to adjust capacity to maintain steady, predictable performance at the lowest possible cost.
- **Amazon Route 53** for DNS management and user-friendly URL configurations.
- **AWS Certificate Manager** for handling SSL/TLS certificates.
- **IAM Roles** for secure AWS service access.
- **Security Groups** to control inbound and outbound traffic to AWS resources.

### Detailed Component Interaction:

- **Developers** push code changes to GitHub, triggering CI/CD pipelines that build Docker images using **Docker** and push them to **Amazon ECR (Elastic Container Registry)**.
- The updated Docker images are then pulled by **AWS ECS**, managed by **Fargate** for serverless operation.
- **Database migrations** are handled using **Flyway**, ensuring that the **Amazon RDS** database schema is up-to-date with the latest application changes.
- **Amazon Route 53** manages the application's domain, directing users to the ALB, which routes requests to the appropriate container instances based on traffic and health status.
- **Security and encryption** are managed via **AWS Certificate Manager** and **Security Groups**, ensuring that all communication is secure and that only authorized traffic can access the network resources.

## Deployment Process

The deployment process utilizes a mix of AWS CLI commands, Docker commands, and custom scripts to manage the infrastructure and application lifecycle.

### Key Scripts and Commands

- **Dockerfile**: Defines the Docker container configuration, specifying the base image, commands, and file copies required for the application.
- **Build Image Script (`build_image.ps1`)**: Automates the building of Docker images and pushing them to ECR.
- **Flyway Configuration (`flyway.conf`)**: Manages database migration configurations and version control.

```dockerfile
# Dockerfile example snippet
FROM node:14
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 3000
CMD ["node", "app.js"]
```

```bash
# Build and push Docker image
docker build -t myapp .
docker tag myapp 123456789.dkr.ecr.us-east-1.amazonaws.com/myapp
docker push 123456789.dkr.ecr.us-east-1.amazonaws.com/myapp
```

## Monitoring and Logging

- **AWS CloudWatch** is used for monitoring the performance of ECS services, RDS instances, and application logging.
- Alerts and notifications are managed via **AWS SNS (Simple Notification Service)**, keeping the development team informed of critical issues or operational metrics.

## Security Considerations

- All traffic is routed through HTTPS using certificates managed by AWS Certificate Manager.
- IAM policies and roles are strictly defined to follow the principle of least privilege.
- Security groups are configured to allow only necessary traffic to and from the application and database servers.

## How to Get Started

To deploy this project in your AWS environment:
1. Clone the repository.
2. Ensure AWS CLI is configured with the correct permissions.
3. Run the deployment scripts located in the `scripts` directory.
4. Follow the setup instructions in the deployment guide to configure additional AWS services and Docker.


