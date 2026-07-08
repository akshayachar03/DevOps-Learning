# Docker Registry & Container Lifecycle Management Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is a Docker Registry?

**Answer**

A Docker Registry is a repository that stores and distributes Docker images. It enables developers and DevOps engineers to share, version, and deploy container images across different environments.

Common registries include:

- Docker Hub
- Azure Container Registry (ACR)
- Amazon Elastic Container Registry (ECR)
- Google Artifact Registry
- Harbor

**Explanation**

Docker images are built locally and then pushed to a registry. Other users or deployment pipelines can pull these images whenever required.

**Used in Production**

Docker Registries are the central source for application images in CI/CD pipelines and Kubernetes deployments.

**Common Mistake**

Many candidates confuse a Docker Registry with Docker Engine. The registry stores images, while Docker Engine runs containers.

---

### Question 2

**Question**

What is Docker Hub?

**Answer**

Docker Hub is Docker's public cloud-based registry that hosts millions of container images.

It provides:

- Official images
- Public repositories
- Private repositories
- Image versioning
- Team collaboration

Example:

```bash
docker pull nginx
```

**Explanation**

Docker Hub is the default registry used when no registry is specified.

**Used in Production**

Organizations commonly pull official base images such as Ubuntu, Nginx, Python, and Node.js from Docker Hub.

**Common Mistake**

Using public images without verifying their authenticity or version.

---

### Question 3

**Question**

How do you log in and log out of Docker Hub?

**Answer**

Login:

```bash
docker login
```

Logout:

```bash
docker logout
```

**Explanation**

Authentication allows Docker to push images to private repositories and pull private images.

**Used in Production**

CI/CD pipelines authenticate using service accounts or access tokens.

**Common Mistake**

Hardcoding Docker Hub credentials in scripts instead of using secure secret management.

---

### Question 4

**Question**

How do you push a Docker image to Docker Hub?

**Answer**

Step 1: Build the image

```bash
docker build -t myapp:v1 .
```

Step 2: Tag the image

```bash
docker tag myapp:v1 username/myapp:v1
```

Step 3: Login

```bash
docker login
```

Step 4: Push

```bash
docker push username/myapp:v1
```

**Explanation**

Images must follow the repository naming convention before they can be pushed.

**Used in Production**

CI/CD pipelines automatically push versioned images after successful builds.

---

### Question 5

**Question**

How do you pull Docker images from a registry?

**Answer**

Pull latest version:

```bash
docker pull nginx
```

Pull a specific version:

```bash
docker pull nginx:1.27
```

Pull from a private repository:

```bash
docker pull username/myapp:v1
```

**Explanation**

Docker downloads the image from the specified registry if it does not exist locally.

**Used in Production**

Deployment servers and Kubernetes clusters pull images during deployments.

---

### Question 6

**Question**

Why are Repository Tags important?

**Answer**

Repository tags identify different versions of an image.

Examples:

```
myapp:v1
myapp:v2
myapp:latest
```

**Explanation**

Tags enable version control and predictable deployments.

**Used in Production**

Organizations commonly use:

- Semantic versions
- Git commit hashes
- Build numbers

**Common Mistake**

Using only the `latest` tag in production, which may lead to unexpected deployments.

---

### Question 7

**Question**

What are the different Docker Container States?

**Answer**

Common container states include:

- Created
- Running
- Restarting
- Paused
- Exited
- Dead

View container status:

```bash
docker ps -a
```

**Explanation**

Containers transition between states based on lifecycle events.

**Used in Production**

Monitoring container states helps identify failed or unhealthy applications.

---

### Question 8

**Question**

How do you perform Docker Resource Cleanup?

**Answer**

Remove stopped containers:

```bash
docker container prune
```

Remove unused images:

```bash
docker image prune
```

Remove unused volumes:

```bash
docker volume prune
```

Remove unused networks:

```bash
docker network prune
```

Remove everything unused:

```bash
docker system prune
```

**Explanation**

Cleanup commands reclaim disk space by removing unused Docker resources.

**Used in Production**

Regular cleanup prevents storage exhaustion on Docker hosts.

---

### Question 9

**Question**

Why should containers be given meaningful names?

**Answer**

Container names simplify management and communication.

Example:

```bash
docker run --name web-server nginx
```

instead of relying on randomly generated names.

**Explanation**

Named containers are easier to identify, monitor, and connect with other containers.

**Used in Production**

Container names are commonly referenced in logs, monitoring tools, and Docker networking.

---

### Question 10

**Question**

What are Docker Restart Policies?

**Answer**

Restart policies control how Docker handles container failures.

Common policies:

```
no
always
unless-stopped
on-failure
```

Example:

```bash
docker run \
--restart unless-stopped \
nginx
```

**Explanation**

Restart policies improve application availability by automatically restarting failed containers.

**Used in Production**

Most production services use either:

- `always`
- `unless-stopped`

**Common Mistake**

Not configuring restart policies, causing applications to remain stopped after server reboots or crashes.

---

### Question 11

**Question**

What are the best practices for Docker Registries and Container Lifecycle Management?

**Answer**

Best practices include:

- Use version-specific image tags.
- Avoid using `latest` in production.
- Push images only after successful CI builds.
- Use meaningful container names.
- Configure restart policies.
- Regularly clean unused Docker resources.
- Authenticate securely using tokens or service accounts.
- Store images in private registries for production workloads.

**Explanation**

These practices improve reliability, security, and maintainability in containerized environments.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

Your deployment server cannot pull a private Docker image from Docker Hub. What should you check first?

**Answer**

Verify that the server is authenticated using:

```bash
docker login
```

and confirm that the account has permission to access the private repository.

**Explanation**

Private repositories require authentication before images can be pulled.

---

### Scenario 2

**Question**

Your CI/CD pipeline builds Docker images successfully but fails while pushing them to Docker Hub. What is the most likely cause?

**Answer**

Possible causes include:

- Incorrect repository name
- Missing `docker login`
- Invalid credentials
- Insufficient permissions

**Explanation**

Pushing images requires both authentication and a correctly tagged repository.

---

### Scenario 3

**Question**

A deployment accidentally pulls a newer image than expected because the pipeline uses the `latest` tag. How can this be prevented?

**Answer**

Use explicit version tags.

Example:

```
myapp:v2.1.0
```

instead of:

```
latest
```

**Explanation**

Versioned tags ensure predictable deployments and easier rollbacks.

---

### Scenario 4

**Question**

Your Docker host runs out of disk space because hundreds of stopped containers and unused images remain after multiple deployments. How would you clean the system?

**Answer**

Run:

```bash
docker system prune
```

Optionally clean specific resources:

```bash
docker container prune
docker image prune
docker volume prune
```

**Explanation**

Removing unused resources frees storage while leaving active containers unaffected.

---

### Scenario 5

**Question**

Your application container exits after a crash and never restarts automatically. What configuration is missing?

**Answer**

A restart policy.

Example:

```bash
docker run \
--restart unless-stopped \
myapp
```

**Explanation**

Restart policies automatically recover containers after failures or host reboots.

---

### Scenario 6

**Question**

A teammate launches multiple containers without assigning names. Later, troubleshooting becomes difficult. What would you recommend?

**Answer**

Assign descriptive names using:

```bash
docker run --name api-server myapp
```

**Explanation**

Meaningful names simplify container management, monitoring, and networking.

---

### Scenario 7

**Question**

Your production deployment requires the exact same image that passed testing. How should the CI/CD pipeline handle image publishing?

**Answer**

Build the image once, assign a version-specific tag, push it to the registry, and deploy that same tag to all environments.

Example:

```bash
docker tag myapp:v1.2.0 company/myapp:v1.2.0
docker push company/myapp:v1.2.0
```

**Explanation**

Promoting the same immutable image ensures consistency across development, testing, and production.

---

### Scenario 8

**Question**

A server reboots unexpectedly, but none of the application containers start automatically. What should you investigate?

**Answer**

Verify whether restart policies were configured.

Example:

```bash
docker inspect container_name
```

Check:

```
RestartPolicy
```

**Explanation**

Without a restart policy, containers remain stopped after a reboot.

---

### Scenario 9

**Question**

Your DevOps team wants to keep Docker Hub organized by separating development, testing, and production images. How would you recommend tagging images?

**Answer**

Use structured tags such as:

```
myapp:dev
myapp:test
myapp:staging
myapp:v2.1.0
```

or combine semantic versions with Git commit hashes.

**Explanation**

Consistent tagging improves traceability, rollback capability, and deployment automation.

---

### Scenario 10

**Question**

You are implementing a CI/CD pipeline for a microservices application. The pipeline should build Docker images, store them centrally, deploy version-specific releases, automatically recover containers after server reboots, and prevent disk space issues on Docker hosts. How would you design the solution?

**Answer**

- Build Docker images during the CI stage.
- Tag images using semantic versions or Git commit hashes.
- Push images to a registry such as Docker Hub or a private registry.
- Deploy applications using version-specific image tags.
- Configure containers with `unless-stopped` or `always` restart policies.
- Assign meaningful container names.
- Schedule regular cleanup using commands such as:

```bash
docker system prune
```

to remove unused resources.

**Explanation**

This approach follows Docker production best practices by providing centralized image management, reliable deployments, automatic recovery, and efficient resource utilization. It reflects a workflow commonly used in enterprise DevOps environments.
