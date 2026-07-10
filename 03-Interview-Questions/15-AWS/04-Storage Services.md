# AWS Storage Services Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is Amazon S3, and what are its primary use cases?

**Answer**

Amazon Simple Storage Service (S3) is an object storage service that provides highly durable, scalable, and secure storage for files (objects).

Common use cases include:

- Static website hosting
- Backup and archival
- Log storage
- Media storage
- Data lakes
- CI/CD artifact storage

**Explanation**

S3 stores data as objects inside buckets rather than as files in a traditional file system. It is designed for virtually unlimited scalability and provides 99.999999999% (11 nines) durability.

**Where it is used in Production**

- Application backups
- Jenkins build artifacts
- Static website hosting
- Terraform state files
- Log storage
- Media content

**Common Mistake**

Confusing S3 object storage with block storage (EBS) or file storage (EFS).

---

### Question 2

**Question**

What are the different Amazon S3 Storage Classes?

**Answer**

Common S3 Storage Classes include:

- S3 Standard
- S3 Intelligent-Tiering
- S3 Standard-IA
- S3 One Zone-IA
- S3 Glacier Instant Retrieval
- S3 Glacier Flexible Retrieval
- S3 Glacier Deep Archive

**Explanation**

Each storage class is optimized for different access patterns and costs. Frequently accessed data uses Standard, while infrequently accessed or archived data uses IA or Glacier classes.

**Where it is used in Production**

- Frequently accessed application data
- Backup storage
- Long-term compliance archives
- Disaster recovery

**Common Mistake**

Choosing Glacier for frequently accessed data, resulting in retrieval delays and additional costs.

---

### Question 3

**Question**

What is an S3 Bucket Policy?

**Answer**

A Bucket Policy is a resource-based JSON policy that controls access permissions to an S3 bucket and its objects.

**Explanation**

Bucket Policies allow or deny access based on:

- IAM users or roles
- AWS accounts
- IP addresses
- VPC endpoints
- Specific actions

They are commonly used for centralized access management.

**Where it is used in Production**

- Public website hosting
- Cross-account access
- Restricting bucket access
- Secure application access

**Common Mistake**

Making buckets publicly accessible unintentionally by using overly permissive policies.

---

### Question 4

**Question**

What is S3 Object Versioning?

**Answer**

Object Versioning keeps multiple versions of an object in the same bucket.

**Explanation**

Whenever an object is modified or deleted, S3 stores previous versions instead of permanently replacing them. This protects against accidental deletion and overwrites.

**Where it is used in Production**

- Backup protection
- Recovery from accidental deletion
- Compliance
- Terraform state management

**Common Mistake**

Assuming deleted files are permanently removed when versioning is enabled.

---

### Question 5

**Question**

What are S3 Lifecycle Policies?

**Answer**

Lifecycle Policies automatically transition or delete objects based on predefined rules.

Examples include:

- Move objects to Glacier after 90 days
- Delete logs after one year
- Transition to Standard-IA after 30 days

**Explanation**

Lifecycle policies reduce storage costs by automatically managing object lifecycles.

**Where it is used in Production**

- Log retention
- Backup management
- Compliance storage
- Cost optimization

**Common Mistake**

Manually moving old files instead of automating lifecycle management.

---

### Question 6

**Question**

What is Amazon EBS?

**Answer**

Amazon Elastic Block Store (EBS) is a persistent block storage service for EC2 instances.

**Explanation**

EBS behaves like a virtual hard disk attached to an EC2 instance. Data persists even if the instance is stopped.

**Where it is used in Production**

- Operating system disks
- Databases
- Application storage
- Boot volumes

**Common Mistake**

Assuming EBS can be shared simultaneously by multiple EC2 instances (except Multi-Attach-supported volumes).

---

### Question 7

**Question**

What is Amazon EFS?

**Answer**

Amazon Elastic File System (EFS) is a fully managed, scalable network file system that can be mounted by multiple EC2 instances simultaneously.

**Explanation**

EFS uses the NFS protocol and provides shared file storage across multiple Availability Zones.

**Where it is used in Production**

- Shared application files
- Kubernetes persistent storage
- CMS applications
- Home directories
- Web server shared content

**Common Mistake**

Using EFS when block storage (EBS) is more appropriate.

---

### Question 8

**Question**

What is the difference between Amazon S3, EBS, and EFS?

**Answer**

| Service | Storage Type | Used For |
|----------|-------------|----------|
| Amazon S3 | Object Storage | Files, backups, static content |
| Amazon EBS | Block Storage | EC2 operating systems, databases |
| Amazon EFS | File Storage | Shared files across multiple EC2 instances |

**Explanation**

Each storage service is optimized for different workloads:

- S3 stores objects
- EBS provides block storage
- EFS provides shared network file storage

**Where it is used in Production**

Selecting the correct storage service based on application requirements.

---

### Question 9

**Question**

When would you choose Amazon EFS instead of Amazon EBS?

**Answer**

Choose EFS when multiple EC2 instances need concurrent access to the same files.

**Explanation**

Unlike EBS, EFS supports shared access from multiple servers and automatically scales as storage requirements grow.

**Where it is used in Production**

- Web farms
- Kubernetes clusters
- Shared application data
- CI/CD shared workspaces

**Common Mistake**

Using EBS for workloads requiring simultaneous multi-instance access.

---

### Question 10

**Question**

How does S3 achieve high durability?

**Answer**

S3 automatically stores multiple copies of data across multiple devices and Availability Zones within an AWS Region.

**Explanation**

This replication architecture provides 99.999999999% (11 nines) durability and protects against hardware failures.

**Where it is used in Production**

- Critical backups
- Application data
- Long-term storage
- Disaster recovery

---

### Question 11

**Question**

How do Lifecycle Policies help reduce AWS costs?

**Answer**

Lifecycle Policies automatically move less frequently accessed data to lower-cost storage classes or delete obsolete data.

**Explanation**

This eliminates manual storage management while optimizing storage expenses.

**Where it is used in Production**

- Backup retention
- Log archival
- Compliance data
- Long-term storage

**Common Mistake**

Keeping all objects in the Standard storage class regardless of access frequency.

---

### Question 12

**Question**

Can an S3 bucket be accessed without IAM permissions?

**Answer**

Yes, if the bucket policy explicitly grants public or cross-account access.

However, by default, S3 buckets are private.

**Explanation**

Access is determined by the combined evaluation of IAM policies, bucket policies, ACLs (legacy), and Block Public Access settings.

**Where it is used in Production**

- Static website hosting
- Cross-account access
- Public software downloads

**Common Mistake**

Ignoring Block Public Access settings while troubleshooting bucket access.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

Your company stores application logs in S3. Logs older than 90 days are rarely accessed but must be retained for one year. How would you optimize storage costs?

**Answer**

Create an S3 Lifecycle Policy to transition objects to S3 Glacier Flexible Retrieval after 90 days and delete them after one year.

**Explanation**

Lifecycle policies automate storage optimization, reducing costs while meeting retention requirements.

---

### Scenario 2

**Question**

A user accidentally deleted an important file from an S3 bucket. How could this have been prevented?

**Answer**

Enable S3 Versioning so previous object versions remain available for recovery.

**Explanation**

Versioning protects against accidental deletions and overwrites by preserving earlier versions.

---

### Scenario 3

**Question**

Your application runs on five EC2 instances that all need access to the same uploaded files. Which AWS storage service would you choose?

**Answer**

Amazon EFS.

**Explanation**

EFS allows multiple EC2 instances to mount and share the same file system simultaneously.

---

### Scenario 4

**Question**

A database running on an EC2 instance requires high-performance persistent storage. Which AWS storage service would you choose?

**Answer**

Amazon EBS, preferably a gp3 or io2 volume depending on performance requirements.

**Explanation**

EBS provides low-latency block storage suitable for databases and operating system disks.

---

### Scenario 5

**Question**

Your security audit reports that an S3 bucket containing sensitive data is publicly accessible. What would you do?

**Answer**

- Enable Block Public Access
- Review Bucket Policies
- Remove unnecessary public permissions
- Apply least-privilege IAM policies
- Enable logging for auditing

**Explanation**

Public buckets are a common security risk. Restricting access minimizes the chance of unauthorized data exposure.

---

### Scenario 6

**Question**

Your backup files are stored in S3 Standard, but they are rarely accessed. How would you reduce storage costs?

**Answer**

Move the backup files to S3 Standard-IA, Intelligent-Tiering, or Glacier using Lifecycle Policies.

**Explanation**

Using lower-cost storage classes significantly reduces expenses for infrequently accessed data.

---

### Scenario 7

**Question**

A team needs to host a static company website without managing web servers. Which AWS service would you recommend?

**Answer**

Amazon S3 Static Website Hosting.

**Explanation**

S3 can serve static HTML, CSS, JavaScript, and image files directly, eliminating the need for EC2 instances.

---

### Scenario 8

**Question**

An application stores large media files in Amazon EBS, causing storage costs to increase rapidly. What would you recommend?

**Answer**

Move the media files to Amazon S3 and keep only the application and operating system data on EBS.

**Explanation**

S3 is designed for scalable object storage and is significantly more cost-effective for large media files.

---

### Scenario 9

**Question**

A DevOps engineer accidentally overwrote a Terraform state file stored in S3. How could this issue be avoided in the future?

**Answer**

Enable S3 Versioning and optionally MFA Delete for the bucket storing the Terraform state file.

**Explanation**

Versioning allows previous state files to be restored, preventing data loss from accidental overwrites.

---

### Scenario 10

**Question**

Your application requires storage that automatically grows without provisioning additional disks and is shared across multiple EC2 instances. Which AWS service would you choose?

**Answer**

Amazon EFS.

**Explanation**

EFS automatically scales as files are added or removed and supports concurrent access from multiple EC2 instances, making it ideal for shared application storage.
