# AWS Monitoring & Logging and IAC Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is Amazon CloudWatch, and what is it used for?

**Answer**

Amazon CloudWatch is AWS's monitoring and observability service used to collect and monitor metrics, logs, and events from AWS resources and applications.

It helps you:

- Monitor resource health
- Track performance metrics
- Collect application logs
- Create alarms
- Build dashboards
- Automate actions based on events

**Explanation**

CloudWatch provides real-time visibility into AWS resources. It enables engineers to identify performance issues, monitor infrastructure, and automate operational tasks.

**Where it is used in Production**

- Monitoring EC2 instances
- Tracking application performance
- Monitoring Lambda functions
- Infrastructure health monitoring
- Alerting operations teams

**Common Mistake**

Many candidates think CloudWatch only collects logs. It monitors metrics, logs, events, alarms, and dashboards.

---

### Question 2

**Question**

What are CloudWatch Metrics?

**Answer**

Metrics are time-ordered data points that measure the performance or utilization of AWS resources.

Examples include:

- CPU Utilization
- Memory Usage (custom metric)
- Network In/Out
- Disk Read/Write
- Request Count
- Latency

**Explanation**

Metrics help engineers understand resource behavior over time and identify abnormal patterns.

**Where it is used in Production**

- Performance monitoring
- Capacity planning
- Auto Scaling
- Troubleshooting

**Common Mistake**

Assuming CloudWatch automatically collects every metric. Some metrics, such as memory utilization on EC2, require the CloudWatch Agent.

---

### Question 3

**Question**

What are CloudWatch Logs?

**Answer**

CloudWatch Logs is a service used to collect, centralize, store, search, and analyze logs from AWS resources and applications.

It can collect logs from:

- EC2
- Lambda
- ECS
- EKS
- CloudTrail
- Custom applications

**Explanation**

Logs provide detailed information for troubleshooting application and infrastructure issues.

**Where it is used in Production**

- Debugging applications
- Security investigations
- Compliance auditing
- Performance troubleshooting

---

### Question 4

**Question**

What is a CloudWatch Alarm?

**Answer**

A CloudWatch Alarm monitors a metric and performs an action when a threshold is crossed.

Possible actions include:

- Send SNS notification
- Trigger Auto Scaling
- Stop EC2 instance
- Reboot EC2 instance
- Invoke Lambda

**Explanation**

Alarms automate responses to operational events and reduce manual monitoring.

**Where it is used in Production**

- CPU alerts
- Disk usage alerts
- High latency notifications
- Auto Scaling triggers

**Common Mistake**

Confusing CloudWatch Alarms with CloudWatch Logs. Alarms work with metrics, not directly with logs.

---

### Question 5

**Question**

What are CloudWatch Dashboards?

**Answer**

CloudWatch Dashboards provide a customizable visual view of AWS resources using charts, graphs, and metrics.

**Explanation**

Dashboards allow engineers to monitor the health of multiple AWS services from a single interface.

**Where it is used in Production**

- NOC monitoring
- DevOps dashboards
- Executive reporting
- Infrastructure monitoring

---

### Question 6

**Question**

What is Amazon CloudTrail?

**Answer**

Amazon CloudTrail records AWS API calls and account activities for auditing, governance, compliance, and security.

It records:

- Who performed an action
- What action was performed
- When it occurred
- Source IP address
- AWS service used

**Explanation**

CloudTrail tracks account activity rather than application performance.

**Where it is used in Production**

- Security auditing
- Compliance
- Incident investigation
- Change tracking

**Common Mistake**

Confusing CloudTrail with CloudWatch. CloudTrail records API activity, while CloudWatch monitors operational metrics and logs.

---

### Question 7

**Question**

What is the difference between CloudWatch and CloudTrail?

**Answer**

| CloudWatch | CloudTrail |
|------------|------------|
| Monitors resources | Records API activity |
| Tracks metrics and logs | Tracks user actions |
| Used for monitoring | Used for auditing |
| Supports alarms | Supports compliance |

**Explanation**

CloudWatch answers "How is my application performing?" while CloudTrail answers "Who made this change?"

**Where it is used in Production**

Organizations typically use both services together.

---

### Question 8

**Question**

What is AWS CloudFormation?

**Answer**

AWS CloudFormation is an Infrastructure as Code (IaC) service that provisions AWS resources using JSON or YAML templates.

**Explanation**

Instead of manually creating resources, engineers define infrastructure in code and deploy it consistently.

**Where it is used in Production**

- Infrastructure deployment
- Environment provisioning
- Disaster recovery
- Infrastructure version control

**Common Mistake**

Treating CloudFormation as a configuration management tool rather than an infrastructure provisioning service.

---

### Question 9

**Question**

What are the benefits of using CloudFormation?

**Answer**

Benefits include:

- Infrastructure as Code
- Repeatable deployments
- Version control
- Automated provisioning
- Reduced manual errors
- Consistent environments

**Explanation**

CloudFormation ensures environments remain consistent across development, testing, and production.

**Where it is used in Production**

- Automated AWS deployments
- CI/CD pipelines
- Multi-environment provisioning

---

### Question 10

**Question**

How does Terraform integrate with AWS?

**Answer**

Terraform uses the AWS Provider to provision AWS infrastructure through Infrastructure as Code.

Terraform can create resources such as:

- EC2
- VPC
- IAM
- S3
- RDS
- Load Balancers

**Explanation**

Terraform communicates with AWS APIs to create and manage infrastructure.

**Where it is used in Production**

- Multi-cloud deployments
- Infrastructure automation
- DevOps pipelines

**Common Mistake**

Assuming Terraform is AWS-specific. Terraform supports multiple cloud providers.

---

### Question 11

**Question**

What is the difference between CloudFormation and Terraform?

**Answer**

| CloudFormation | Terraform |
|----------------|-----------|
| AWS-only | Multi-cloud |
| Native AWS service | Third-party tool |
| JSON/YAML templates | HCL language |
| Tight AWS integration | Supports multiple providers |

**Explanation**

CloudFormation is preferred for AWS-native environments, while Terraform is commonly chosen for multi-cloud infrastructure.

**Where it is used in Production**

Organizations may use either tool depending on cloud strategy.

---

### Question 12

**Question**

Why is Infrastructure as Code important in DevOps?

**Answer**

Infrastructure as Code enables infrastructure to be:

- Version controlled
- Automated
- Reproducible
- Auditable
- Easily recoverable

**Explanation**

IaC eliminates manual provisioning, reduces configuration drift, and enables faster deployments.

**Where it is used in Production**

- CI/CD pipelines
- Automated infrastructure provisioning
- Disaster recovery
- Environment replication

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

Your production EC2 instance suddenly reaches 100% CPU utilization. How would you monitor and respond to this automatically?

**Answer**

Create a CloudWatch Alarm for CPU Utilization and configure it to:

- Send an SNS notification
- Trigger Auto Scaling
- Invoke a Lambda function if needed

**Explanation**

CloudWatch continuously monitors CPU metrics and automatically executes configured actions when thresholds are exceeded.

---

### Scenario 2

**Question**

An application is crashing intermittently, but CPU and memory appear normal. What AWS service would you check first?

**Answer**

CloudWatch Logs.

**Explanation**

Application logs often reveal exceptions, stack traces, or configuration issues that metrics alone cannot identify.

---

### Scenario 3

**Question**

A security team wants to know who deleted an S3 bucket yesterday. Which AWS service would you use?

**Answer**

Amazon CloudTrail.

**Explanation**

CloudTrail records AWS API calls, including the user, timestamp, IP address, and action performed.

---

### Scenario 4

**Question**

Your manager wants a single screen showing CPU, network traffic, EC2 health, and application requests. Which AWS feature would you use?

**Answer**

CloudWatch Dashboards.

**Explanation**

Dashboards consolidate multiple metrics into a single visual interface for operations teams.

---

### Scenario 5

**Question**

A company manually provisions AWS infrastructure for every new project, causing inconsistencies. How would you improve this process?

**Answer**

Implement Infrastructure as Code using AWS CloudFormation or Terraform.

**Explanation**

IaC creates consistent, repeatable infrastructure deployments and minimizes manual errors.

---

### Scenario 6

**Question**

Your DevOps team needs to provision identical environments for Development, QA, and Production. What approach would you recommend?

**Answer**

Use CloudFormation templates or Terraform modules.

**Explanation**

Infrastructure templates ensure all environments are deployed with the same configuration.

---

### Scenario 7

**Question**

A developer accidentally changes a security group's rules. How would you determine who made the change?

**Answer**

Review Amazon CloudTrail logs.

**Explanation**

CloudTrail records every API call, allowing administrators to identify who modified AWS resources.

---

### Scenario 8

**Question**

Your application experiences traffic spikes during business hours. How would you monitor this trend?

**Answer**

Use CloudWatch Metrics and Dashboards to monitor request count, CPU utilization, and network traffic.

**Explanation**

Historical metrics help identify usage patterns and support capacity planning.

---

### Scenario 9

**Question**

Your team wants infrastructure deployments to be included in the CI/CD pipeline. Which tools would you recommend?

**Answer**

Use Terraform or AWS CloudFormation integrated with Jenkins, GitHub Actions, or AWS CodePipeline.

**Explanation**

Infrastructure changes become version-controlled and automatically deployed as part of the release process.

---

### Scenario 10

**Question**

After deploying infrastructure using Terraform, an EC2 instance fails to start correctly. How would you troubleshoot the issue?

**Answer**

Review:

- Terraform output
- Terraform state
- EC2 instance status
- CloudWatch Metrics
- CloudWatch Logs
- CloudTrail events
- Security Groups
- IAM permissions

**Explanation**

Troubleshooting should verify both infrastructure provisioning and runtime behavior to identify whether the issue is related to Terraform, AWS configuration, or the application itself.
