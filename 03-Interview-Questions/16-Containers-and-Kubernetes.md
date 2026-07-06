# Containers & Kubernetes (Docker, ACR & AKS) – Interview Questions and Answers

---

# Table of Contents

1. Frequently Asked Interview Questions
2. Frequently Asked Scenario-Based Questions

---

# Part 1 – Frequently Asked Interview Questions

---

## Q1. What is Docker, and why is it used?

### Answer

**Definition**

**Docker** is a containerization platform that packages an application and its dependencies into a lightweight, portable **container**.

**Explanation**

- Implements **containerization**.
- Packages application with dependencies.
- Runs consistently across environments.
- Lightweight compared to Virtual Machines.
- Faster startup.
- Easy to deploy.
- Supports CI/CD pipelines.
- Improves portability.

**Real-world Example**

A Java application developed on a laptop runs without modification on Azure Kubernetes Service using the same Docker image.

**Azure Example**

Docker container deployed to Azure Container Registry and AKS.

**AWS Equivalent**

Amazon Elastic Container Registry (ECR) + Amazon ECS/EKS

**Important Interview Keywords**

**Docker**, **Containerization**, **Image**, **Container**, **Portability**

---

## Q2. What is the difference between a Docker Image and a Docker Container?

### Answer

**Definition**

A **Docker Image** is a read-only blueprint, while a **Docker Container** is a running instance of that image.

**Explanation**

| Docker Image | Docker Container |
|--------------|------------------|
| Blueprint | Running instance |
| Read-only | Writable |
| Stored in Registry | Runs on Host |
| Can create many containers | Executes application |

- Images are immutable.
- Containers are temporary.
- One image can create multiple containers.
- Images are versioned.

**Real-world Example**

A single Nginx image creates ten running web server containers.

**Azure Example**

Image stored in ACR → Container runs in AKS.

**AWS Equivalent**

ECR Image → ECS/EKS Container

**Important Interview Keywords**

**Image**, **Container**, **Immutable**, **Runtime**

---

## Q3. What is a Dockerfile?

### Answer

**Definition**

A **Dockerfile** is a text file containing instructions to build a Docker image.

**Explanation**

- Automates image creation.
- Uses layers.
- Supports version control.
- Reproducible builds.
- Defines application environment.
- Supports COPY, RUN, CMD, ENTRYPOINT.
- Used in CI/CD.

**Real-world Example**

A Dockerfile installs Java, copies a Spring Boot JAR, and starts the application.

**Azure Example**

Dockerfile builds image before pushing to ACR.

**AWS Equivalent**

Same Dockerfile used with ECR.

**Important Interview Keywords**

**Dockerfile**, **Build**, **Layers**, **CMD**, **ENTRYPOINT**

---

## Q4. What is Docker Compose?

### Answer

**Definition**

**Docker Compose** is a tool used to define and run multi-container applications using a YAML file.

**Explanation**

- Runs multiple containers.
- Uses `docker-compose.yml` (or `compose.yaml` in modern Compose).
- Defines networking.
- Defines volumes.
- Simplifies development.
- Good for local environments.
- Not used for production orchestration.

**Real-world Example**

Run a web application, MySQL database, and Redis cache together using one command.

**Azure Example**

Develop locally using Docker Compose before deploying to AKS.

**AWS Equivalent**

Docker Compose on EC2 or local development.

**Important Interview Keywords**

**Docker Compose**, **Multi-container**, **YAML**

---

## Q5. What is Azure Container Registry (ACR)?

### Answer

**Definition**

**Azure Container Registry (ACR)** is a private Docker image registry used to store and manage container images.

**Explanation**

- Stores Docker images.
- Private registry.
- Integrates with AKS.
- Supports image versioning.
- Supports RBAC.
- Supports image scanning (with integrations).
- Secure image storage.

**Real-world Example**

A CI/CD pipeline pushes application images into ACR before deployment.

**Azure Example**

Azure DevOps → ACR → AKS

**AWS Equivalent**

Amazon Elastic Container Registry (ECR)

**Important Interview Keywords**

**ACR**, **Container Registry**, **Private Registry**

---

## Q6. What is Azure Kubernetes Service (AKS)?

### Answer

**Definition**

**Azure Kubernetes Service (AKS)** is a managed Kubernetes service used to deploy, scale, and manage containerized applications.

**Explanation**

- Managed Kubernetes.
- Automatic upgrades.
- High availability.
- Autoscaling.
- Integrates with ACR.
- Supports monitoring.
- Supports RBAC.
- Simplifies cluster management.

**Real-world Example**

An e-commerce application runs hundreds of containers across multiple nodes in AKS.

**Azure Example**

AKS cluster hosting microservices.

**AWS Equivalent**

Amazon Elastic Kubernetes Service (EKS)

**Important Interview Keywords**

**AKS**, **Managed Kubernetes**, **Cluster**, **Scaling**

---

## Q7. What is a Pod in Kubernetes?

### Answer

**Definition**

A **Pod** is the smallest deployable unit in Kubernetes that contains one or more containers.

**Explanation**

- Smallest Kubernetes object.
- Shares networking.
- Shares storage.
- Usually one container.
- Ephemeral.
- Scheduled on worker nodes.
- Managed by Deployments.

**Real-world Example**

A web application container runs inside a Pod.

**Azure Example**

AKS Pod running Nginx.

**AWS Equivalent**

Pod in Amazon EKS.

**Important Interview Keywords**

**Pod**, **Smallest Unit**, **Container**

---

## Q8. What are Deployments and ReplicaSets?

### Answer

**Definition**

A **Deployment** manages Pods and ReplicaSets, while a **ReplicaSet** ensures the desired number of Pod replicas are running.

**Explanation**

Deployment

- Manages application rollout.
- Supports rolling updates.
- Supports rollback.
- Creates ReplicaSets.

ReplicaSet

- Maintains desired Pod count.
- Automatically recreates failed Pods.

**Real-world Example**

Deployment maintains five web server Pods.

**Azure Example**

AKS Deployment.

**AWS Equivalent**

EKS Deployment.

**Important Interview Keywords**

**Deployment**, **ReplicaSet**, **Rolling Update**, **Rollback**

---

## Q9. What are Kubernetes Services and Ingress?

### Answer

**Definition**

A **Service** exposes Pods internally or externally, while **Ingress** manages HTTP/HTTPS routing.

**Explanation**

Service Types

- ClusterIP
- NodePort
- LoadBalancer

Ingress

- HTTP routing.
- SSL termination.
- Host-based routing.
- Path-based routing.

**Real-world Example**

Users access an application through an Ingress Controller instead of individual Pods.

**Azure Example**

AKS + Azure Application Gateway Ingress Controller.

**AWS Equivalent**

AWS Load Balancer Controller + ALB.

**Important Interview Keywords**

**Service**, **Ingress**, **LoadBalancer**, **Routing**

---

## Q10. What are ConfigMaps and Secrets?

### Answer

**Definition**

ConfigMaps store non-sensitive configuration, while Secrets store sensitive information.

**Explanation**

ConfigMap

- Environment variables.
- Configuration files.
- Non-sensitive values.

Secret

- Passwords.
- API Keys.
- Tokens.
- Certificates.

- Mounted as files or environment variables.
- Keeps configuration separate from code.

**Real-world Example**

Database URL → ConfigMap

Database Password → Secret

**Azure Example**

AKS ConfigMap and Secret.

**AWS Equivalent**

Kubernetes ConfigMap + AWS Secrets Manager.

**Important Interview Keywords**

**ConfigMap**, **Secret**, **Configuration**, **Sensitive Data**

---

## Q11. How does the deployment flow work in AKS?

### Answer

**Definition**

Applications move from source code to Kubernetes through a CI/CD pipeline.

**Explanation**

1. Developer writes code.
2. Dockerfile builds image.
3. Image pushed to ACR.
4. Kubernetes manifests applied.
5. AKS pulls image.
6. Pods created.
7. Service exposes application.

**Real-world Example**

GitHub → Azure DevOps → ACR → AKS.

**Azure Example**

Azure DevOps Pipeline.

**AWS Equivalent**

CodePipeline → ECR → EKS.

**Important Interview Keywords**

**CI/CD**, **ACR**, **AKS**, **Deployment**

---

## Q12. What are the best practices for Docker and AKS?

### Answer

**Definition**

Following best practices improves security, scalability, and maintainability.

**Explanation**

- Use small base images.
- Never run containers as root.
- Store secrets in Kubernetes Secrets or Azure Key Vault.
- Use resource limits.
- Use Health Probes.
- Use ReplicaSets.
- Enable autoscaling.
- Scan container images.
- Keep images updated.
- Use private registries.

**Real-world Example**

Production AKS cluster uses ACR, Key Vault, autoscaling, and monitoring.

**Azure Example**

AKS + ACR + Azure Monitor.

**AWS Equivalent**

EKS + ECR + CloudWatch.

**Important Interview Keywords**

**Security**, **Autoscaling**, **Health Probes**, **ACR**

---

# Part 2 – Frequently Asked Scenario-Based Questions

---

## Scenario 1

### Question

Your development team says, "The application works on my machine but not on production." How would Docker solve this?

### Answer

### Step-by-Step Solution

1. Create a Dockerfile.
2. Build a Docker image.
3. Test the image.
4. Push the image to ACR.
5. Deploy the same image to AKS.

### Why this approach?

- Same environment everywhere.
- Eliminates dependency issues.

### Azure Implementation

- Docker
- ACR
- AKS

### AWS Equivalent

- Docker
- ECR
- EKS

### Best Practices

- Version images.
- Use official base images.
- Keep images lightweight.

### Common Mistakes

- Building images manually.
- Different environments for development and production.

### Interview Conclusion

Docker ensures consistent application behavior across development, testing, and production environments.

---

## Scenario 2

### Question

Your company wants to host a scalable microservices application. Which Azure service would you recommend?

### Answer

### Step-by-Step Solution

1. Containerize applications.
2. Push images to ACR.
3. Deploy to AKS.
4. Configure autoscaling.
5. Monitor workloads.

### Why this approach?

- High scalability.
- Easy orchestration.
- Self-healing.

### Azure Implementation

- AKS
- ACR

### AWS Equivalent

- Amazon EKS

### Best Practices

- Separate microservices.
- Use namespaces.
- Enable monitoring.

### Common Mistakes

- Running microservices on VMs.
- No autoscaling.

### Interview Conclusion

AKS is the preferred platform for running scalable, production-grade containerized applications.

---

## Scenario 3

### Question

Your production application must always have five running instances. How would Kubernetes achieve this?

### Answer

### Step-by-Step Solution

1. Create a Deployment.
2. Set replicas to five.
3. Deploy the application.
4. Monitor Pods.
5. Kubernetes recreates failed Pods automatically.

### Why this approach?

- High availability.
- Self-healing.

### Azure Implementation

- Deployment
- ReplicaSet

### AWS Equivalent

- EKS Deployment

### Best Practices

- Configure readiness and liveness probes.
- Use rolling updates.

### Common Mistakes

- Deploying standalone Pods.
- No replica configuration.

### Interview Conclusion

Deployments and ReplicaSets ensure the desired number of application instances remain available automatically.

---

## Scenario 4

### Question

Your application must expose HTTP traffic to the internet. Which Kubernetes component would you use?

### Answer

### Step-by-Step Solution

1. Create a Deployment.
2. Create a Service.
3. Configure an Ingress.
4. Configure DNS.
5. Enable HTTPS.

### Why this approach?

- Simplifies routing.
- Supports SSL termination.

### Azure Implementation

- Service
- Ingress
- Application Gateway

### AWS Equivalent

- ALB Ingress Controller

### Best Practices

- Use HTTPS.
- Configure health probes.
- Enable load balancing.

### Common Mistakes

- Exposing Pods directly.
- Ignoring SSL.

### Interview Conclusion

Ingress provides centralized HTTP/HTTPS routing and is the preferred way to expose applications in Kubernetes.

---

## Scenario 5

### Question

Your application needs a database password. Where should you store it?

### Answer

### Step-by-Step Solution

1. Create a Kubernetes Secret.
2. Mount it into the Pod.
3. Avoid hardcoding credentials.
4. Restrict access.
5. Rotate secrets periodically.

### Why this approach?

- Improves security.
- Separates configuration from code.

### Azure Implementation

- Kubernetes Secret
- Azure Key Vault (recommended for enterprise integrations)

### AWS Equivalent

- AWS Secrets Manager

### Best Practices

- Encrypt secrets.
- Rotate credentials.
- Use least privilege.

### Common Mistakes

- Hardcoding passwords.
- Storing secrets in ConfigMaps.

### Interview Conclusion

Sensitive data should always be stored in Secrets or integrated secret management services like Azure Key Vault.

---

## Scenario 6

### Question

A developer changes an environment variable frequently without rebuilding the image. What Kubernetes feature would you use?

### Answer

### Step-by-Step Solution

1. Create a ConfigMap.
2. Store configuration values.
3. Mount the ConfigMap.
4. Restart Pods if required.
5. Validate the application.

### Why this approach?

- Decouples configuration.
- Simplifies maintenance.

### Azure Implementation

- ConfigMap

### AWS Equivalent

- Kubernetes ConfigMap on EKS

### Best Practices

- Separate configuration from application code.
- Version configuration changes.

### Common Mistakes

- Rebuilding images for configuration changes.
- Storing passwords in ConfigMaps.

### Interview Conclusion

ConfigMaps provide flexible, reusable configuration management without rebuilding container images.

---

## Scenario 7

### Question

Your DevOps pipeline must automatically deploy a new application version to AKS. How would you design the workflow?

### Answer

### Step-by-Step Solution

1. Build the Docker image.
2. Push the image to ACR.
3. Update the Deployment manifest.
4. Deploy using CI/CD.
5. Verify rollout status.

### Why this approach?

- Automated deployments.
- Repeatable releases.

### Azure Implementation

- Azure DevOps
- ACR
- AKS

### AWS Equivalent

- CodePipeline
- ECR
- EKS

### Best Practices

- Version images.
- Use rolling updates.
- Validate deployments.

### Common Mistakes

- Using the `latest` tag in production.
- Manual deployments.

### Interview Conclusion

A CI/CD pipeline integrated with ACR and AKS provides reliable and automated application deployments.

---

## Scenario 8

### Question

One Pod crashes unexpectedly. What happens in Kubernetes?

### Answer

### Step-by-Step Solution

1. Kubernetes detects the failure.
2. ReplicaSet notices the missing Pod.
3. A new Pod is scheduled.
4. Service routes traffic to healthy Pods.
5. Application remains available.

### Why this approach?

- Self-healing.
- High availability.

### Azure Implementation

- AKS
- ReplicaSet

### AWS Equivalent

- EKS

### Best Practices

- Configure health probes.
- Monitor Pod health.
- Use multiple replicas.

### Common Mistakes

- Running only one Pod.
- Ignoring health checks.

### Interview Conclusion

Kubernetes automatically replaces failed Pods, ensuring application availability without manual intervention.

---

## Scenario 9

### Question

Your application experiences a sudden increase in traffic. How would AKS handle it?

### Answer

### Step-by-Step Solution

1. Enable Horizontal Pod Autoscaler (HPA).
2. Define CPU or memory thresholds.
3. Scale Pods automatically.
4. Use Cluster Autoscaler if additional nodes are required.
5. Monitor performance.

### Why this approach?

- Handles traffic spikes.
- Improves availability.
- Optimizes costs.

### Azure Implementation

- AKS
- HPA
- Cluster Autoscaler

### AWS Equivalent

- EKS
- HPA
- Cluster Autoscaler

### Best Practices

- Set realistic scaling thresholds.
- Monitor resource utilization.
- Test autoscaling.

### Common Mistakes

- No autoscaling.
- Overprovisioning resources.

### Interview Conclusion

Horizontal Pod Autoscaler and Cluster Autoscaler enable AKS to scale applications automatically based on workload demand.

---

## Scenario 10

### Question

Your enterprise wants a production-ready container platform on Azure. What architecture would you recommend?

### Answer

### Step-by-Step Solution

1. Containerize applications using Docker.
2. Store images in Azure Container Registry.
3. Deploy workloads to Azure Kubernetes Service.
4. Use Deployments and ReplicaSets for high availability.
5. Expose applications using Services and Ingress.
6. Store configuration in ConfigMaps.
7. Store sensitive data in Secrets or Azure Key Vault.
8. Enable autoscaling and monitoring.
9. Automate deployments using Azure DevOps or GitHub Actions.

### Why this approach?

- Highly scalable.
- Self-healing.
- Secure.
- Supports CI/CD.
- Suitable for enterprise workloads.

### Azure Implementation

- Docker
- ACR
- AKS
- Ingress
- Azure Monitor
- Azure DevOps

### AWS Equivalent

- Docker
- ECR
- EKS
- ALB Ingress Controller
- CloudWatch
- CodePipeline

### Best Practices

- Use private registries.
- Enable image scanning.
- Configure readiness and liveness probes.
- Avoid using the `latest` image tag in production.
- Store secrets securely.
- Enable autoscaling and monitoring.

### Common Mistakes

- Running containers as root.
- Hardcoding configuration and secrets.
- Deploying standalone Pods instead of Deployments.
- Not configuring health probes.
- Ignoring image versioning and security scanning.

### Interview Conclusion

A production-grade Azure container platform combines Docker, Azure Container Registry, and Azure Kubernetes Service with Deployments, Services, Ingress, ConfigMaps, Secrets, autoscaling, and CI/CD automation. This architecture delivers scalability, resilience, security, and operational efficiency for modern cloud-native applications.

---
