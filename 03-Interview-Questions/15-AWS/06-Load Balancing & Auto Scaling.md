# AWS Load Balancing & Auto Scaling Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is Elastic Load Balancer (ELB), and why is it used?

**Answer**

Elastic Load Balancer (ELB) is an AWS service that automatically distributes incoming application traffic across multiple targets such as EC2 instances, containers, and IP addresses.

Its benefits include:

- High Availability
- Fault Tolerance
- Improved Scalability
- Better Performance
- Automatic Health Checks

**Explanation**

Instead of sending all traffic to a single server, ELB distributes requests among multiple healthy targets. If one instance fails, ELB automatically routes traffic to healthy instances.

**Where it is used in Production**

- Highly available web applications
- Microservices
- Kubernetes (EKS)
- Multi-AZ deployments

**Common Mistake**

Assuming ELB automatically scales EC2 instances. ELB distributes traffic, while Auto Scaling manages the number of instances.

---

### Question 2

**Question**

What are the different types of Elastic Load Balancers in AWS?

**Answer**

AWS provides four types of load balancers:

- Application Load Balancer (ALB)
- Network Load Balancer (NLB)
- Gateway Load Balancer (GWLB)
- Classic Load Balancer (CLB - Legacy)

**Explanation**

Each load balancer is optimized for different workloads:

- ALB → HTTP/HTTPS applications
- NLB → TCP/UDP traffic with very high performance
- GWLB → Network virtual appliances
- CLB → Legacy applications

**Where it is used in Production**

ALB is the most commonly used load balancer for web applications.

**Common Mistake**

Using an NLB for Layer 7 routing requirements such as path-based routing.

---

### Question 3

**Question**

What is an Application Load Balancer (ALB)?

**Answer**

An Application Load Balancer operates at Layer 7 (HTTP/HTTPS) and intelligently routes requests based on application-level information.

**Explanation**

ALB supports:

- Path-based routing
- Host-based routing
- SSL termination
- WebSocket support
- Target Groups

**Where it is used in Production**

- Microservices
- REST APIs
- Kubernetes Ingress
- Multi-service web applications

**Common Mistake**

Confusing ALB with NLB, which operates at Layer 4.

---

### Question 4

**Question**

What is an Auto Scaling Group (ASG)?

**Answer**

An Auto Scaling Group automatically launches or terminates EC2 instances based on demand or health checks.

**Explanation**

ASG maintains the desired number of healthy EC2 instances and scales the infrastructure automatically based on CloudWatch metrics.

**Where it is used in Production**

- Web servers
- Application servers
- Kubernetes worker nodes
- Stateless applications

**Common Mistake**

Creating an ASG without defining proper scaling policies.

---

### Question 5

**Question**

What is a Launch Template?

**Answer**

A Launch Template defines the configuration used to launch EC2 instances.

It includes:

- AMI
- Instance Type
- Security Groups
- IAM Role
- Key Pair
- User Data
- Storage Configuration

**Explanation**

Launch Templates provide reusable instance configurations for Auto Scaling Groups and EC2 launches.

**Where it is used in Production**

- Auto Scaling
- Standardized deployments
- Infrastructure automation

**Common Mistake**

Modifying existing instances instead of updating the Launch Template version.

---

### Question 6

**Question**

How do Health Checks work in an Auto Scaling Group?

**Answer**

Auto Scaling continuously monitors instance health using EC2 and optionally ELB health checks.

If an instance becomes unhealthy, it is automatically terminated and replaced.

**Explanation**

Health checks ensure that only healthy instances remain part of the Auto Scaling Group.

**Where it is used in Production**

- High Availability
- Self-healing infrastructure
- Production web applications

**Common Mistake**

Using only EC2 health checks when application-level health checks are required.

---

### Question 7

**Question**

What is the relationship between ALB and Auto Scaling?

**Answer**

ALB distributes incoming traffic among EC2 instances, while Auto Scaling adds or removes EC2 instances based on demand.

**Explanation**

Together they provide:

- High availability
- Automatic scaling
- Fault tolerance
- Improved performance

**Where it is used in Production**

Almost every production web application uses ALB together with Auto Scaling.

---

### Question 8

**Question**

What are Target Groups in an Application Load Balancer?

**Answer**

Target Groups are collections of backend resources that receive traffic from the load balancer.

Targets can include:

- EC2 instances
- IP addresses
- Lambda functions

**Explanation**

ALB forwards requests to healthy targets within a Target Group.

**Where it is used in Production**

- Microservices
- Blue-Green deployments
- Multi-application hosting

**Common Mistake**

Registering instances without configuring health check endpoints.

---

### Question 9

**Question**

What scaling policies are commonly used with Auto Scaling?

**Answer**

Common scaling policies include:

- Target Tracking Scaling
- Step Scaling
- Simple Scaling
- Scheduled Scaling

**Explanation**

These policies determine when new EC2 instances should be launched or terminated based on demand.

**Where it is used in Production**

- CPU-based scaling
- Memory-based scaling (using CloudWatch Agent)
- Scheduled business-hour scaling

---

### Question 10

**Question**

What CloudWatch metrics are commonly used for Auto Scaling?

**Answer**

Common metrics include:

- CPU Utilization
- Network In
- Network Out
- Request Count
- Custom Metrics
- ALB Request Count Per Target

**Explanation**

Auto Scaling monitors these metrics and adjusts the number of EC2 instances automatically.

**Where it is used in Production**

Production environments use CPU utilization and ALB request count most frequently.

---

### Question 11

**Question**

Why are Load Balancers deployed across multiple Availability Zones?

**Answer**

Deploying across multiple Availability Zones improves availability and fault tolerance.

**Explanation**

If one Availability Zone becomes unavailable, traffic is automatically routed to healthy targets in another Availability Zone.

**Where it is used in Production**

- High Availability applications
- Disaster recovery
- Production web services

**Common Mistake**

Deploying resources in only one Availability Zone.

---

### Question 12

**Question**

Can an Auto Scaling Group replace a failed EC2 instance automatically?

**Answer**

Yes.

If an instance becomes unhealthy, the Auto Scaling Group automatically terminates it and launches a replacement.

**Explanation**

This self-healing capability helps maintain the desired capacity and application availability.

**Where it is used in Production**

- Highly available web applications
- Production APIs
- Kubernetes worker nodes

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

Your web application experiences high CPU utilization during business hours. How would you ensure it handles the increased traffic automatically?

**Answer**

Deploy the application behind an Application Load Balancer and configure an Auto Scaling Group with Target Tracking Scaling based on CPU utilization.

**Explanation**

The ALB distributes incoming traffic, while Auto Scaling launches additional EC2 instances when CPU usage exceeds the configured threshold.

---

### Scenario 2

**Question**

One EC2 instance behind an Application Load Balancer becomes unhealthy. What happens?

**Answer**

The ALB stops routing traffic to the unhealthy instance, and the Auto Scaling Group terminates and replaces it if health checks fail.

**Explanation**

This provides automatic failover without manual intervention.

---

### Scenario 3

**Question**

Your application must support sudden traffic spikes during product launches. How would you design the infrastructure?

**Answer**

Use:

- Application Load Balancer
- Auto Scaling Group
- Launch Template
- CloudWatch scaling policies
- Multi-AZ deployment

**Explanation**

This architecture automatically scales based on demand while maintaining high availability.

---

### Scenario 4

**Question**

Users report intermittent application failures even though EC2 instances appear healthy. What would you investigate?

**Answer**

Check:

- ALB Target Group health
- Health Check path
- Application logs
- Security Groups
- Web server status
- Target Group registration

**Explanation**

EC2 health checks verify the instance, while ALB health checks verify that the application itself is responding correctly.

---

### Scenario 5

**Question**

A new EC2 instance launched by Auto Scaling is not receiving traffic. What could be the cause?

**Answer**

Possible causes include:

- Failed ALB health checks
- Incorrect Target Group
- Security Group restrictions
- Application not running
- Wrong health check path

**Explanation**

Only healthy targets registered with the Target Group receive traffic.

---

### Scenario 6

**Question**

Your application receives very little traffic overnight. How can AWS reduce infrastructure costs automatically?

**Answer**

Configure Auto Scaling policies to terminate unnecessary EC2 instances when demand decreases.

**Explanation**

Auto Scaling reduces costs by matching infrastructure capacity with actual workload requirements.

---

### Scenario 7

**Question**

A deployment introduces an application bug, causing all health checks to fail. What happens?

**Answer**

The Application Load Balancer marks the instances as unhealthy and stops sending traffic to them. If configured, the Auto Scaling Group replaces the failed instances, but the new instances will also fail if they use the same faulty application version.

**Explanation**

Health checks improve availability but cannot fix application defects. The deployment must be rolled back.

---

### Scenario 8

**Question**

Your application serves multiple websites from the same load balancer. Which AWS load balancer should you use?

**Answer**

Application Load Balancer (ALB).

**Explanation**

ALB supports host-based and path-based routing, allowing multiple websites or services to share one load balancer.

---

### Scenario 9

**Question**

A company wants every newly launched EC2 instance to have the same AMI, Security Groups, User Data, and IAM Role. What AWS feature should be used?

**Answer**

Launch Templates.

**Explanation**

Launch Templates standardize EC2 configuration, ensuring every Auto Scaling instance is created consistently.

---

### Scenario 10

**Question**

Your production application must remain available even if an entire Availability Zone fails. How would you design the solution?

**Answer**

Deploy:

- Application Load Balancer across multiple Availability Zones
- Auto Scaling Group spanning multiple Availability Zones
- EC2 instances distributed across those Availability Zones
- Appropriate health checks and scaling policies

**Explanation**

This architecture provides high availability, fault tolerance, and automatic recovery by routing traffic to healthy instances in surviving Availability Zones and replacing failed instances automatically.
