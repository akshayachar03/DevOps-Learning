# AWS CI/CD Services & Security Services Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is AWS CodePipeline, and what role does it play in CI/CD?

**Answer**

AWS CodePipeline is a fully managed Continuous Integration and Continuous Delivery (CI/CD) service that automates the software release process.

A typical pipeline includes:
- Source stage
- Build stage
- Test stage
- Deploy stage

It integrates with services like CodeCommit, CodeBuild, CodeDeploy, GitHub, Jenkins, and Amazon S3.

**Explanation**

CodePipeline automates the movement of code from source control to production. Whenever code changes are committed, the pipeline automatically triggers the configured stages.

**Where it is used in Production**

- Automated software delivery
- DevOps pipelines
- Infrastructure deployment
- Continuous deployment

**Common Mistake**

Many candidates confuse CodePipeline with CodeBuild. CodePipeline orchestrates the workflow, while CodeBuild performs the build.

---

### Question 2

**Question**

What is AWS CodeCommit?

**Answer**

AWS CodeCommit is a fully managed Git-based source code repository service used to securely store application code.

Features include:
- Private Git repositories
- IAM integration
- Encryption at rest and in transit
- High availability
- Version control

**Explanation**

CodeCommit functions similarly to GitHub or GitLab but is hosted and managed by AWS.

**Where it is used in Production**

- Source code management
- Infrastructure as Code repositories
- CI/CD source stage

**Common Mistake**

Thinking CodeCommit automatically builds or deploys code. It only stores source code.

---

### Question 3

**Question**

What is AWS CodeBuild?

**Answer**

AWS CodeBuild is a fully managed build service that compiles source code, runs tests, and generates deployment artifacts.

It supports:
- Java
- Python
- Node.js
- .NET
- Docker
- Custom build environments

**Explanation**

CodeBuild eliminates the need to maintain dedicated build servers.

**Where it is used in Production**

- Application builds
- Unit testing
- Docker image creation
- CI pipelines

**Common Mistake**

Confusing CodeBuild with CodeDeploy. CodeBuild creates artifacts; CodeDeploy deploys them.

---

### Question 4

**Question**

What is AWS CodeDeploy?

**Answer**

AWS CodeDeploy automates application deployments to:

- Amazon EC2
- On-premises servers
- AWS Lambda
- Amazon ECS

It supports deployment strategies such as:
- In-place deployment
- Blue/Green deployment

**Explanation**

CodeDeploy minimizes deployment failures and reduces downtime through automated deployment strategies.

**Where it is used in Production**

- Production deployments
- Blue/Green releases
- Rolling deployments

---

### Question 5

**Question**

What is AWS KMS?

**Answer**

AWS Key Management Service (KMS) is a managed service used to create, store, rotate, and manage encryption keys.

It integrates with:
- Amazon S3
- Amazon EBS
- Amazon RDS
- AWS Secrets Manager
- CloudTrail

**Explanation**

KMS centralizes encryption key management and simplifies data protection across AWS services.

**Where it is used in Production**

- Encrypting storage
- Database encryption
- Application security
- Compliance

**Common Mistake**

Thinking KMS stores secrets. KMS manages encryption keys, not application credentials.

---

### Question 6

**Question**

What is AWS Secrets Manager?

**Answer**

AWS Secrets Manager securely stores, manages, and rotates sensitive information such as:

- Database passwords
- API keys
- Tokens
- SSH credentials

**Explanation**

Instead of hardcoding secrets in applications, developers retrieve them securely at runtime.

**Where it is used in Production**

- Database authentication
- API authentication
- Secure application configuration

**Common Mistake**

Storing passwords inside configuration files instead of Secrets Manager.

---

### Question 7

**Question**

What is AWS Systems Manager (SSM)?

**Answer**

AWS Systems Manager is a management service that helps administer AWS resources from a central location.

Capabilities include:
- Session Manager
- Run Command
- Patch Manager
- Parameter Store
- Inventory

**Explanation**

SSM reduces operational overhead by providing centralized server management without requiring SSH access.

**Where it is used in Production**

- Server administration
- Patch management
- Remote command execution
- Configuration management

---

### Question 8

**Question**

What is AWS WAF?

**Answer**

AWS Web Application Firewall (WAF) protects web applications from common web attacks.

It can block:
- SQL Injection
- Cross-Site Scripting (XSS)
- Malicious bots
- IP-based attacks
- Rate-based attacks

**Explanation**

WAF filters incoming HTTP requests before they reach the application.

**Where it is used in Production**

- Web applications
- APIs
- CloudFront distributions
- Application Load Balancers

**Common Mistake**

Assuming WAF protects the operating system. It protects HTTP and HTTPS traffic only.

---

### Question 9

**Question**

How do AWS CodeCommit, CodeBuild, CodeDeploy, and CodePipeline work together?

**Answer**

Typical workflow:

1. Developer pushes code to CodeCommit.
2. CodePipeline detects the change.
3. CodeBuild compiles and tests the application.
4. CodeDeploy deploys the application.
5. Production environment is updated.

**Explanation**

Each service performs a dedicated role within the CI/CD pipeline.

**Where it is used in Production**

Enterprise software delivery pipelines.

---

### Question 10

**Question**

What is the difference between AWS KMS and AWS Secrets Manager?

**Answer**

| AWS KMS | AWS Secrets Manager |
|---------|---------------------|
| Manages encryption keys | Stores secrets |
| Used for encryption | Used for credentials |
| Encrypts AWS resources | Rotates secrets automatically |
| Integrates with many AWS services | Integrates with applications |

**Explanation**

KMS secures data through encryption, while Secrets Manager securely stores sensitive application credentials.

**Where it is used in Production**

Organizations commonly use both services together.

---

### Question 11

**Question**

Why is AWS Systems Manager preferred over SSH for server administration?

**Answer**

Benefits include:

- No public SSH ports required
- IAM-based access control
- Session logging
- Audit trails
- Improved security

**Explanation**

SSM Session Manager enables secure remote access without exposing servers to the internet.

**Where it is used in Production**

Secure EC2 administration in private subnets.

**Common Mistake**

Continuing to use SSH for all server management when SSM offers a more secure alternative.

---

### Question 12

**Question**

How can you secure a CI/CD pipeline in AWS?

**Answer**

Best practices include:

- Store secrets in AWS Secrets Manager.
- Encrypt data using AWS KMS.
- Apply least-privilege IAM policies.
- Enable CloudTrail logging.
- Scan code before deployment.
- Use secure artifact storage.

**Explanation**

A secure pipeline protects source code, credentials, deployment artifacts, and production environments.

**Where it is used in Production**

Enterprise DevOps environments.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

A developer commits code, but the deployment pipeline never starts. How would you troubleshoot?

**Answer**

Verify:

- CodeCommit repository
- CodePipeline source stage
- IAM permissions
- Pipeline status
- CloudWatch Events/EventBridge triggers

**Explanation**

Most pipeline failures originate from source integration or permissions.

---

### Scenario 2

**Question**

A CodeBuild project fails during the build stage. What would you investigate?

**Answer**

Check:

- Build logs
- buildspec.yml
- IAM role
- Environment variables
- Dependency installation
- Docker image (if applicable)

**Explanation**

Build logs usually identify the exact command causing the failure.

---

### Scenario 3

**Question**

Your deployment fails during CodeDeploy. How would you troubleshoot?

**Answer**

Review:

- Deployment logs
- AppSpec file
- EC2 deployment agent
- IAM permissions
- Target instance health

**Explanation**

Deployment failures commonly result from configuration errors or unhealthy target instances.

---

### Scenario 4

**Question**

A security audit finds database passwords hardcoded in application code. How would you resolve this?

**Answer**

Move all credentials to AWS Secrets Manager and retrieve them securely at runtime.

**Explanation**

Secrets Manager centralizes secret management and supports automatic rotation.

---

### Scenario 5

**Question**

Your organization wants all S3 buckets encrypted using centrally managed keys. Which AWS service would you use?

**Answer**

AWS KMS.

**Explanation**

KMS manages encryption keys that integrate directly with Amazon S3.

---

### Scenario 6

**Question**

Administrators currently access EC2 instances using SSH over the internet. How can security be improved?

**Answer**

Use AWS Systems Manager Session Manager.

**Explanation**

SSM eliminates the need for public SSH access and provides IAM-based authentication and auditing.

---

### Scenario 7

**Question**

Your company's public web application is receiving SQL Injection attempts. Which AWS service would you implement?

**Answer**

AWS WAF.

**Explanation**

WAF can detect and block SQL Injection attacks before they reach the application.

---

### Scenario 8

**Question**

A new application release causes production failures. How can AWS services help automate rollback?

**Answer**

Use AWS CodeDeploy with Blue/Green deployment or automatic rollback based on deployment health.

**Explanation**

Automatic rollback minimizes downtime and quickly restores the previous stable version.

---

### Scenario 9

**Question**

Your DevOps team wants every code commit to automatically trigger build, test, and deployment. Which AWS services would you combine?

**Answer**

- CodeCommit
- CodePipeline
- CodeBuild
- CodeDeploy

**Explanation**

These services together provide a fully automated AWS-native CI/CD pipeline.

---

### Scenario 10

**Question**

An engineer accidentally deletes an IAM policy used by the CI/CD pipeline, causing deployment failures. How would you investigate?

**Answer**

Review:

- AWS CloudTrail logs
- IAM policy history
- CodePipeline execution logs
- CloudWatch logs
- IAM permissions

**Explanation**

CloudTrail records all IAM API activity, making it possible to identify who deleted the policy and when the action occurred.
