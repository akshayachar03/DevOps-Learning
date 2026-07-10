# AWS Troubleshooting Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What are the most common causes of IAM permission issues in AWS?

**Answer**

Common causes include:

- Missing IAM permissions
- Explicit Deny in IAM policies
- Missing resource-based permissions
- Incorrect IAM Role assignment
- Service Control Policies (SCPs) restricting access
- Permission Boundary restrictions

**Explanation**

AWS evaluates all applicable policies before granting access. If any policy contains an explicit **Deny**, access is denied even if another policy allows it. IAM permission issues are among the most common problems encountered in AWS environments.

**Where it is used in Production**

- EC2 access
- S3 access
- Lambda execution
- CI/CD deployments
- Cross-service integrations

**Common Mistake**

Candidates often assume adding `AdministratorAccess` is the solution instead of identifying the missing permission.

---

### Question 2

**Question**

How do you troubleshoot an EC2 instance that is unreachable via SSH?

**Answer**

Check the following:

- EC2 instance is running
- Correct public IP or Elastic IP
- Security Group allows port 22
- Network ACL allows SSH traffic
- Internet Gateway is attached
- Route Table has a route to the Internet Gateway
- Correct SSH key pair
- SSH service is running

**Explanation**

EC2 connectivity depends on networking, firewall rules, routing, and the operating system. Missing configuration in any layer can prevent SSH access.

**Where it is used in Production**

Daily server administration and troubleshooting.

**Common Mistake**

Only checking the Security Group while ignoring route tables or Internet Gateway configuration.

---

### Question 3

**Question**

What is the role of Security Groups in AWS?

**Answer**

Security Groups are stateful virtual firewalls attached to EC2 instances that control inbound and outbound traffic.

**Explanation**

Security Groups evaluate traffic based on defined rules. Since they are stateful, return traffic is automatically allowed without requiring separate rules.

**Where it is used in Production**

- EC2
- Load Balancers
- RDS
- ECS
- EKS

**Common Mistake**

Confusing Security Groups with Network ACLs. Security Groups are stateful, whereas Network ACLs are stateless.

---

### Question 4

**Question**

How do Route Tables affect network connectivity in AWS?

**Answer**

Route Tables determine where network traffic is directed.

Typical routes include:

- Internet Gateway for internet access
- NAT Gateway for private subnet outbound traffic
- VPC Peering
- Transit Gateway
- VPN

**Explanation**

Even if Security Groups allow traffic, incorrect routing can prevent communication between resources.

**Where it is used in Production**

VPC network design and connectivity troubleshooting.

**Common Mistake**

Checking only firewall rules without verifying the route configuration.

---

### Question 5

**Question**

Why might an EC2 instance be unable to access the internet?

**Answer**

Possible reasons include:

- Missing Internet Gateway
- Incorrect Route Table
- No public IP assigned
- Security Group restrictions
- Network ACL restrictions
- Incorrect subnet placement

**Explanation**

Internet access requires proper routing, networking components, and firewall rules working together.

**Where it is used in Production**

EC2 deployment troubleshooting.

---

### Question 6

**Question**

What are the common causes of S3 Access Denied errors?

**Answer**

Common causes include:

- Missing IAM permissions
- Bucket Policy restrictions
- Explicit Deny statements
- Missing KMS permissions
- Object ownership issues

**Explanation**

S3 permissions are evaluated using IAM policies, Bucket Policies, ACLs (if enabled), and KMS permissions.

**Where it is used in Production**

Application storage, backups, and CI/CD artifact storage.

**Common Mistake**

Checking only IAM policies while ignoring Bucket Policies.

---

### Question 7

**Question**

How does Amazon CloudWatch help with troubleshooting?

**Answer**

CloudWatch provides:

- Metrics
- Logs
- Alarms
- Dashboards
- Performance monitoring

**Explanation**

CloudWatch collects operational data that helps identify performance issues, application failures, and infrastructure problems.

**Where it is used in Production**

- Server monitoring
- Application monitoring
- Infrastructure health
- Performance analysis

---

### Question 8

**Question**

What information can you obtain from CloudWatch Logs?

**Answer**

CloudWatch Logs can contain:

- Application logs
- System logs
- Lambda logs
- Custom logs
- Error messages
- Stack traces

**Explanation**

Logs help identify the exact cause of failures and provide detailed information that metrics alone cannot.

**Where it is used in Production**

Production debugging and incident analysis.

---

### Question 9

**Question**

What is the purpose of Load Balancer health checks?

**Answer**

Health checks determine whether backend targets are healthy enough to receive traffic.

If a target fails health checks, the Load Balancer stops routing requests to it.

**Explanation**

This improves application availability by automatically directing traffic only to healthy instances.

**Where it is used in Production**

- ALB
- NLB
- Auto Scaling Groups

---

### Question 10

**Question**

What happens if an EC2 instance continuously fails Load Balancer health checks?

**Answer**

The Load Balancer removes the instance from service, and if it belongs to an Auto Scaling Group, the unhealthy instance may be terminated and replaced.

**Explanation**

Health checks ensure that only healthy servers handle client requests, improving application reliability.

**Where it is used in Production**

Highly available web applications.

---

### Question 11

**Question**

How do you troubleshoot an unhealthy target behind an Application Load Balancer?

**Answer**

Verify:

- Application is running
- Correct health check path
- Correct health check port
- Security Group rules
- Target Group configuration
- Application response codes

**Explanation**

Most unhealthy target issues are caused by incorrect health check paths or application failures.

**Where it is used in Production**

Application deployment troubleshooting.

---

### Question 12

**Question**

What is a systematic approach to troubleshooting AWS issues?

**Answer**

A common approach is:

1. Identify the affected service.
2. Review CloudWatch metrics and logs.
3. Check IAM permissions.
4. Verify Security Groups and Network ACLs.
5. Verify Route Tables.
6. Validate application configuration.
7. Review recent infrastructure changes.

**Explanation**

Following a structured troubleshooting process reduces downtime and prevents overlooking critical configuration issues.

**Where it is used in Production**

Daily DevOps and Cloud Operations activities.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

A developer receives an **Access Denied** error while uploading files to an S3 bucket. How would you troubleshoot?

**Answer**

Check:

- IAM policy
- Bucket Policy
- Explicit Deny statements
- KMS permissions
- Object ownership settings

**Explanation**

S3 authorization is influenced by multiple policy layers. Reviewing all applicable permissions helps identify the root cause.

---

### Scenario 2

**Question**

You cannot SSH into an EC2 instance. What would you investigate?

**Answer**

Verify:

- Instance state
- Public IP or Elastic IP
- Internet Gateway
- Route Table
- Security Group
- Network ACL
- SSH service
- Key pair

**Explanation**

SSH failures are commonly caused by networking issues or incorrect firewall configuration.

---

### Scenario 3

**Question**

An EC2 instance can communicate with other instances but cannot access the internet. What could be wrong?

**Answer**

Check:

- Internet Gateway
- Route Table
- Public IP assignment
- Subnet configuration
- NAT Gateway (for private subnets)

**Explanation**

Internal communication may work while internet access fails due to missing routing components.

---

### Scenario 4

**Question**

Your application is deployed successfully, but the Application Load Balancer reports all targets as unhealthy. How would you troubleshoot?

**Answer**

Verify:

- Health check endpoint
- Application status
- Target Group configuration
- Security Group rules
- Listening port
- HTTP response code

**Explanation**

Health check configuration errors are one of the most common causes of unhealthy targets.

---

### Scenario 5

**Question**

A Jenkins deployment pipeline suddenly fails with IAM permission errors even though it worked yesterday. What would you check?

**Answer**

Investigate:

- Recent IAM policy changes
- IAM Role assignment
- Permission Boundary
- Service Control Policies
- Credential expiration

**Explanation**

Permission changes are a common cause of unexpected CI/CD failures.

---

### Scenario 6

**Question**

CloudWatch shows that CPU utilization is consistently above 95% on an EC2 instance. How would you respond?

**Answer**

Actions include:

- Analyze running processes
- Review application logs
- Scale vertically or horizontally
- Configure Auto Scaling
- Optimize the application

**Explanation**

High CPU utilization may indicate increased traffic, inefficient code, or insufficient instance capacity.

---

### Scenario 7

**Question**

Your application cannot connect to an RDS database after deployment. What networking components would you verify?

**Answer**

Check:

- Security Groups
- Network ACLs
- Route Tables
- Database endpoint
- Database port
- VPC configuration

**Explanation**

Database connectivity problems are usually caused by blocked network access or incorrect endpoint configuration.

---

### Scenario 8

**Question**

Users report intermittent application failures even though all EC2 instances appear healthy. What would you investigate?

**Answer**

Review:

- CloudWatch metrics
- Application logs
- Load Balancer logs
- Health check configuration
- CPU and memory utilization
- Network latency

**Explanation**

Intermittent failures often require correlating metrics and logs to identify transient issues.

---

### Scenario 9

**Question**

A new Security Group rule was added, but traffic is still blocked. What additional components would you check?

**Answer**

Verify:

- Network ACLs
- Route Tables
- Target service port
- Application firewall
- Instance operating system firewall

**Explanation**

Security Groups are only one layer of network security. Other components may still block traffic.

---

### Scenario 10

**Question**

Your production application suddenly becomes unavailable after a deployment. How would you troubleshoot?

**Answer**

Follow a structured approach:

1. Check Load Balancer health.
2. Review CloudWatch metrics.
3. Analyze CloudWatch Logs.
4. Verify EC2 instance health.
5. Review deployment changes.
6. Validate networking configuration.
7. Roll back if necessary.

**Explanation**

A systematic troubleshooting process helps quickly isolate the root cause and restore service while minimizing downtime.
