# AWS Amazon EC2 Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is Amazon EC2, and why is it used?

**Answer**

Amazon Elastic Compute Cloud (EC2) is a web service that provides scalable virtual servers (instances) in the AWS Cloud. It allows users to launch, manage, and terminate virtual machines on demand.

**Explanation**

EC2 eliminates the need to purchase physical servers and provides flexible compute capacity. Users can choose different operating systems, CPU, memory, storage, and networking configurations based on workload requirements.

**Where it is used in Production**

- Hosting web applications
- Running APIs and microservices
- CI/CD servers (Jenkins, GitHub Runners)
- Application servers
- Database servers
- Kubernetes worker nodes

**Common Mistake**

Many candidates confuse EC2 with a container service. EC2 provides virtual machines, while containers run inside services like ECS, EKS, or Docker on EC2.

---

### Question 2

**Question**

What are EC2 Instance Types?

**Answer**

EC2 Instance Types define the CPU, memory, storage, and networking capacity of an EC2 instance.

Common instance families include:

- General Purpose (T, M)
- Compute Optimized (C)
- Memory Optimized (R, X)
- Storage Optimized (I, D)
- Accelerated Computing (P, G, Inf)

**Explanation**

Different workloads require different hardware configurations. AWS provides specialized instance families to optimize cost and performance.

**Where it is used in Production**

- T3/T4g for development servers
- M5/M6 for application servers
- C5/C6 for compute-intensive workloads
- R5/R6 for databases
- G5/P4 for machine learning

**Common Mistake**

Selecting the largest instance instead of choosing one that matches workload requirements.

---

### Question 3

**Question**

What is an Amazon Machine Image (AMI)?

**Answer**

An AMI is a preconfigured template used to launch EC2 instances.

It contains:

- Operating System
- Installed Software
- Configuration
- Root Volume
- Application Packages (optional)

**Explanation**

Instead of installing software manually each time, an AMI allows identical EC2 instances to be launched quickly and consistently.

**Where it is used in Production**

- Auto Scaling Groups
- Golden Images
- Standardized application servers

**Common Mistake**

Confusing an AMI with an EC2 instance. An AMI is a template, while an EC2 instance is a running virtual machine.

---

### Question 4

**Question**

What are Amazon EBS Volumes?

**Answer**

Amazon Elastic Block Store (EBS) provides persistent block-level storage for EC2 instances.

Common volume types include:

- gp3
- gp2
- io1/io2
- st1
- sc1

**Explanation**

Unlike instance store storage, EBS volumes persist even after an EC2 instance is stopped.

**Where it is used in Production**

- Operating System disks
- Databases
- Application data
- Log storage

**Common Mistake**

Assuming all EC2 storage is deleted after stopping an instance.

---

### Question 5

**Question**

What is an EC2 Key Pair?

**Answer**

A Key Pair consists of:

- Public Key (stored by AWS)
- Private Key (stored securely by the user)

It is used for secure SSH authentication to Linux EC2 instances.

**Explanation**

Instead of passwords, AWS recommends using SSH key-based authentication for improved security.

**Where it is used in Production**

- Linux administration
- Automation servers
- Bastion hosts

**Common Mistake**

Losing the private key, making SSH access impossible without recovery steps.

---

### Question 6

**Question**

What is a Security Group in AWS?

**Answer**

A Security Group is a virtual firewall that controls inbound and outbound traffic to EC2 instances.

It supports rules based on:

- Protocol
- Port
- Source/Destination
- CIDR Range
- Security Group

**Explanation**

Security Groups are stateful, meaning return traffic is automatically allowed.

**Where it is used in Production**

Protecting EC2 instances from unauthorized access.

**Common Mistake**

Opening SSH (22) or RDP (3389) to `0.0.0.0/0` unnecessarily.

---

### Question 7

**Question**

What is an Elastic IP Address?

**Answer**

An Elastic IP is a static public IPv4 address that can be associated with an EC2 instance.

**Explanation**

Unlike normal public IPs, Elastic IPs remain allocated to your AWS account and can be reassigned to another instance during failures.

**Where it is used in Production**

- Bastion Hosts
- Public Web Servers
- NAT Instances

**Common Mistake**

Allocating Elastic IPs and leaving them unused, which incurs charges.

---

### Question 8

**Question**

What is EC2 User Data?

**Answer**

User Data is a script executed automatically when an EC2 instance launches for the first time.

Common tasks include:

- Installing packages
- Updating OS
- Configuring applications
- Starting services

**Explanation**

User Data enables automated instance initialization without manual intervention.

**Where it is used in Production**

- Bootstrapping web servers
- Installing Docker
- Installing monitoring agents
- CI/CD automation

**Common Mistake**

Expecting User Data to run automatically after every reboot without additional configuration.

---

### Question 9

**Question**

What are the different EC2 instance states?

**Answer**

The EC2 lifecycle includes:

- Pending
- Running
- Stopping
- Stopped
- Shutting-down
- Terminated

**Explanation**

Understanding instance states helps administrators manage billing, maintenance, and automation.

**Where it is used in Production**

Managing EC2 infrastructure and troubleshooting.

---

### Question 10

**Question**

What is the difference between stopping and terminating an EC2 instance?

**Answer**

Stopping:

- Instance can be restarted
- EBS volume persists
- Instance ID remains
- Public IP changes (unless Elastic IP)

Terminating:

- Instance is permanently deleted
- Root volume is usually deleted
- Instance cannot be recovered

**Explanation**

Stopping temporarily saves compute costs, while termination permanently removes the instance.

**Where it is used in Production**

Managing development and production environments.

**Common Mistake**

Terminating an instance instead of stopping it.

---

### Question 11

**Question**

How do Security Groups differ from Network ACLs?

**Answer**

| Security Group | Network ACL |
|---------------|-------------|
| Instance level | Subnet level |
| Stateful | Stateless |
| Allow rules only | Allow and Deny rules |
| Automatically allows return traffic | Return traffic must be explicitly allowed |

**Explanation**

Security Groups protect instances, while Network ACLs protect subnets.

**Where it is used in Production**

Layered network security.

---

### Question 12

**Question**

Why is EC2 User Data important in DevOps?

**Answer**

User Data automates server configuration during instance launch, ensuring consistency and reducing manual effort.

**Explanation**

It enables Infrastructure as Code (IaC) practices by automatically configuring instances at startup.

**Where it is used in Production**

- Auto Scaling Groups
- Blue-Green Deployments
- Immutable Infrastructure
- CI/CD pipelines

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

You launched an EC2 instance but cannot SSH into it. What would you check?

**Answer**

I would verify:

- Security Group allows port 22
- Correct Key Pair is being used
- Instance is running
- Public IP or Elastic IP exists
- Route Table and Internet Gateway configuration
- Network ACL rules
- SSH service is running

**Explanation**

SSH failures are usually caused by networking, Security Group, or authentication issues.

---

### Scenario 2

**Question**

Your application server must keep the same public IP even after replacement during maintenance. What would you use?

**Answer**

Use an Elastic IP Address.

**Explanation**

Elastic IPs can be detached from one EC2 instance and attached to another, minimizing downtime.

---

### Scenario 3

**Question**

Your Auto Scaling Group launches new EC2 instances, but the application is not installed automatically. How would you solve this?

**Answer**

Use EC2 User Data to install required packages, configure the application, and start services during instance launch.

**Explanation**

User Data automates instance initialization, ensuring every new instance is configured consistently.

---

### Scenario 4

**Question**

A developer accidentally terminated a production EC2 instance. How could this have been prevented?

**Answer**

Enable termination protection, implement IAM least-privilege policies, and use Auto Scaling Groups with backup AMIs.

**Explanation**

Termination protection prevents accidental deletion, while IAM restricts destructive actions.

---

### Scenario 5

**Question**

An application requires high CPU performance but minimal memory. Which EC2 instance family would you choose?

**Answer**

Choose a Compute Optimized instance, such as the C-series (e.g., C6i or C7g).

**Explanation**

Compute Optimized instances provide more vCPUs relative to memory, making them ideal for CPU-intensive workloads.

---

### Scenario 6

**Question**

Your organization wants to launch identical application servers across multiple environments. What AWS feature would you use?

**Answer**

Create a custom Amazon Machine Image (AMI) with the required operating system and application preinstalled.

**Explanation**

Using a custom AMI ensures consistency, reduces deployment time, and supports immutable infrastructure.

---

### Scenario 7

**Question**

A production EC2 instance runs a database. Which storage option would you choose and why?

**Answer**

Use an Amazon EBS volume, preferably gp3 or io2 depending on performance requirements.

**Explanation**

EBS provides persistent, durable block storage suitable for databases, unlike ephemeral instance store volumes.

---

### Scenario 8

**Question**

An EC2 instance was stopped overnight to save costs. The next morning, the application is unreachable because its public IP changed. How would you prevent this?

**Answer**

Associate an Elastic IP with the EC2 instance.

**Explanation**

Elastic IPs remain associated with your AWS account and retain the same public IP after stop/start cycles.

---

### Scenario 9

**Question**

Your security audit reveals that SSH (port 22) is open to `0.0.0.0/0` on all EC2 instances. What would you recommend?

**Answer**

Restrict SSH access to trusted IP ranges or use a Bastion Host or AWS Systems Manager Session Manager for secure administration.

**Explanation**

Limiting SSH exposure significantly reduces the attack surface and aligns with security best practices.

---

### Scenario 10

**Question**

A deployment script fails because the EC2 instance does not have the required software installed. How would you automate future deployments?

**Answer**

Use EC2 User Data or a custom AMI to install and configure the required software during instance launch.

**Explanation**

Automating server configuration ensures every instance is consistently prepared for application deployment, reducing manual effort and deployment errors.
