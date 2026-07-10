# AWS Containers & Serverless Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is Amazon ECR, and why is it used?

**Answer**

Amazon Elastic Container Registry (ECR) is a fully managed Docker container image registry that securely stores, manages, and distributes container images.

Key features:
- Private and public repositories
- Integration with ECS and EKS
- Image versioning
- IAM-based access control
- Image vulnerability scanning

**Explanation**

Before deploying containers, the application image must be stored somewhere. ECR serves as the central repository where container images are pushed after the build process and pulled during deployment.

**Where it is used in Production**

- CI/CD pipelines
- Kubernetes deployments
- ECS deployments
- Docker image storage

**Common Mistake**

Many candidates confuse ECR with ECS. ECR stores container images, whereas ECS runs the containers.

---

### Question 2

**Question**

What is Amazon ECS?

**Answer**

Amazon Elastic Container Service (ECS) is AWS's fully managed container orchestration service used to deploy, run, and manage Docker containers.

It supports:

- EC2 launch type
- AWS Fargate launch type
- Service discovery
- Auto Scaling
- Load balancing

**Explanation**

ECS removes the complexity of managing container orchestration infrastructure while providing high availability and scalability.

**Where it is used in Production**

- Microservices
- REST APIs
- Web applications
- Batch processing

**Common Mistake**

Assuming ECS and Kubernetes are the same. ECS is AWS-native, while Kubernetes is an open-source orchestration platform.

---

### Question 3

**Question**

What is Amazon EKS?

**Answer**

Amazon Elastic Kubernetes Service (EKS) is AWS's managed Kubernetes service that runs Kubernetes control plane components while AWS manages their availability and updates.

**Explanation**

EKS allows organizations to run Kubernetes without managing the Kubernetes master nodes themselves.

**Where it is used in Production**

- Kubernetes clusters
- Multi-container applications
- Enterprise microservices
- Hybrid Kubernetes deployments

**Common Mistake**

Thinking AWS manages worker nodes automatically. Unless using Fargate, worker nodes remain the customer's responsibility.

---

### Question 4

**Question**

What is the difference between Amazon ECS and Amazon EKS?

**Answer**

| ECS | EKS |
|-----|-----|
| AWS-native container service | Managed Kubernetes |
| Easier to learn | Kubernetes knowledge required |
| AWS-specific | Portable across clouds |
| Simpler management | More flexible ecosystem |

**Explanation**

Choose ECS for simple AWS-native deployments and EKS when Kubernetes compatibility or portability is required.

**Where it is used in Production**

Organizations select the service based on operational requirements and existing expertise.

---

### Question 5

**Question**

What is AWS Lambda?

**Answer**

AWS Lambda is a serverless compute service that executes code in response to events without requiring server management.

Features include:

- Automatic scaling
- Pay-per-use pricing
- Event-driven execution
- Supports multiple programming languages

**Explanation**

Developers upload code, configure triggers, and AWS automatically provisions the required infrastructure.

**Where it is used in Production**

- API backends
- Automation
- Event processing
- File processing
- Scheduled jobs

**Common Mistake**

Assuming Lambda runs continuously. It only executes when triggered.

---

### Question 6

**Question**

What is API Gateway?

**Answer**

Amazon API Gateway is a managed service used to create, publish, secure, monitor, and manage REST, HTTP, and WebSocket APIs.

**Explanation**

API Gateway acts as the entry point for client requests and commonly integrates with Lambda functions.

**Where it is used in Production**

- REST APIs
- Serverless applications
- Mobile backends
- Microservices

**Common Mistake**

Thinking API Gateway executes application logic. It routes requests to backend services such as Lambda.

---

### Question 7

**Question**

What are Lambda event triggers?

**Answer**

Event triggers automatically invoke Lambda functions when specific AWS events occur.

Common triggers include:

- S3 uploads
- API Gateway requests
- CloudWatch Events/EventBridge
- SNS
- SQS
- DynamoDB Streams

**Explanation**

Lambda follows an event-driven architecture where AWS services invoke functions automatically.

**Where it is used in Production**

- Image processing
- Notifications
- Log processing
- Scheduled automation

---

### Question 8

**Question**

How do Amazon ECR, ECS, and EKS work together?

**Answer**

Typical workflow:

1. Build Docker image.
2. Push image to Amazon ECR.
3. ECS or EKS pulls the image from ECR.
4. Containers are deployed and executed.

**Explanation**

ECR provides image storage, while ECS or EKS provides container execution.

**Where it is used in Production**

CI/CD pipelines for containerized applications.

---

### Question 9

**Question**

When would you choose Lambda instead of ECS or EKS?

**Answer**

Choose Lambda when:

- Workloads are event-driven.
- Execution is short-lived.
- Infrastructure management should be minimized.
- Traffic is unpredictable.

Choose ECS/EKS for:

- Long-running applications
- Containerized microservices
- Stateful workloads

**Explanation**

Lambda excels at short-lived functions, while ECS and EKS handle continuously running applications.

**Where it is used in Production**

Architecture decisions based on workload characteristics.

---

### Question 10

**Question**

What are the benefits of serverless computing?

**Answer**

Benefits include:

- No server management
- Automatic scaling
- High availability
- Lower operational overhead
- Pay only for execution time

**Explanation**

Serverless allows developers to focus on application code rather than infrastructure.

**Where it is used in Production**

- APIs
- Automation
- Data processing
- Event-driven applications

---

### Question 11

**Question**

What is the difference between containers and serverless?

**Answer**

| Containers | Serverless |
|------------|------------|
| Long-running applications | Event-driven execution |
| You manage container images | No container management required |
| Greater flexibility | Simpler operations |
| Suitable for complex workloads | Suitable for lightweight functions |

**Explanation**

Containers provide more control, whereas serverless minimizes infrastructure management.

**Where it is used in Production**

Many organizations combine both approaches within the same architecture.

---

### Question 12

**Question**

How does a typical container CI/CD pipeline work in AWS?

**Answer**

Typical workflow:

1. Developer pushes code.
2. CI pipeline builds Docker image.
3. Image is pushed to Amazon ECR.
4. ECS or EKS deploys the updated image.
5. Health checks verify deployment.

**Explanation**

This automates software delivery while ensuring consistent deployments.

**Where it is used in Production**

DevOps pipelines using GitHub Actions, Jenkins, AWS CodePipeline, or Azure DevOps.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

Your ECS service fails to deploy because it cannot pull the Docker image. What would you check?

**Answer**

Verify:

- Image exists in ECR.
- Repository permissions.
- ECS task execution role.
- Image tag.
- Network connectivity.
- ECR authentication.

**Explanation**

Deployment failures commonly occur due to missing images or insufficient IAM permissions.

---

### Scenario 2

**Question**

A Lambda function is not being triggered after a file is uploaded to an S3 bucket. How would you troubleshoot?

**Answer**

Check:

- S3 event notification configuration.
- Lambda permissions.
- Bucket name and prefix filters.
- CloudWatch Logs.
- Lambda execution role.

**Explanation**

Most issues are caused by incorrect event configuration or missing permissions.

---

### Scenario 3

**Question**

Users report API failures after deploying a Lambda-backed API Gateway. What would you investigate?

**Answer**

Review:

- API Gateway configuration.
- Lambda execution logs.
- IAM permissions.
- Integration settings.
- HTTP status codes.

**Explanation**

API Gateway or Lambda integration issues are common causes of failed requests.

---

### Scenario 4

**Question**

Your ECS application becomes slow during peak traffic. How would you improve availability?

**Answer**

Configure:

- ECS Service Auto Scaling.
- Application Load Balancer.
- CloudWatch Alarms.
- Additional task replicas.

**Explanation**

Auto Scaling adjusts container capacity based on demand.

---

### Scenario 5

**Question**

A newly deployed Docker image contains a bug. How would you roll back?

**Answer**

Deploy the previous stable image tag from Amazon ECR and update the ECS service or Kubernetes deployment.

**Explanation**

Versioned container images simplify rollback operations.

---

### Scenario 6

**Question**

Your DevOps team wants to eliminate server management for a file-processing application. What AWS service would you recommend?

**Answer**

AWS Lambda with Amazon S3 event triggers.

**Explanation**

Lambda automatically executes when files are uploaded, eliminating the need for dedicated servers.

---

### Scenario 7

**Question**

Your organization wants to adopt Kubernetes while reducing operational overhead. Which AWS service would you recommend?

**Answer**

Amazon EKS.

**Explanation**

AWS manages the Kubernetes control plane, allowing engineers to focus on application workloads.

---

### Scenario 8

**Question**

An image push to Amazon ECR fails during the CI/CD pipeline. What would you verify?

**Answer**

Check:

- Docker login authentication.
- IAM permissions.
- Repository existence.
- AWS Region.
- Repository URI.
- Network connectivity.

**Explanation**

Authentication and incorrect repository configuration are the most common causes.

---

### Scenario 9

**Question**

A Lambda function times out while processing large files. How would you resolve the issue?

**Answer**

Increase the Lambda timeout and memory, optimize the code, split processing into smaller tasks, or use ECS/EKS for long-running workloads.

**Explanation**

Lambda has execution limits and is best suited for short-lived processing tasks.

---

### Scenario 10

**Question**

A company needs to deploy hundreds of containerized microservices with automated scaling and centralized image management. What AWS services would you recommend?

**Answer**

Use:

- Amazon ECR for image storage.
- Amazon ECS or Amazon EKS for orchestration.
- Application Load Balancer for traffic distribution.
- CloudWatch for monitoring.
- Auto Scaling for elasticity.

**Explanation**

This architecture provides scalable, highly available, and production-ready container deployments commonly used in enterprise environments.
