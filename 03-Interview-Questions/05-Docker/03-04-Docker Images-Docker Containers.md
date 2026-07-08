# Docker Images & Containers Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is a Docker Image?

**Answer**

A Docker Image is a read-only template used to create Docker containers. It contains:

- Application code
- Runtime
- Libraries
- Dependencies
- Environment configuration
- Metadata

A Docker image is immutable, meaning it cannot be modified after it is built.

**Explanation**

An image acts as a blueprint for creating one or more containers.

**Used in Production**

Images are stored in container registries such as Docker Hub, Azure Container Registry (ACR), and Amazon ECR, then deployed to servers or Kubernetes clusters.

**Common Mistake**

Many candidates think an image is a running application. An image is only the template; the running instance is called a container.

---

### Question 2

**Question**

What are Docker Image Layers?

**Answer**

Docker images are built using multiple read-only layers.

Each instruction in a Dockerfile (such as `FROM`, `RUN`, `COPY`, or `ADD`) creates a new layer.

Benefits include:

- Faster builds
- Layer caching
- Efficient storage
- Faster image downloads
- Shared layers between images

**Explanation**

Docker reuses unchanged layers, making builds and deployments more efficient.

**Used in Production**

Layer caching significantly reduces CI/CD pipeline execution time.

**Common Mistake**

Candidates often assume every image is stored independently. Docker shares common layers across images.

---

### Question 3

**Question**

How do you pull an image from Docker Hub?

**Answer**

Pull an image:

```bash
docker pull nginx
```

Pull a specific version:

```bash
docker pull nginx:1.27
```

**Explanation**

Docker downloads the image from Docker Hub if it is not already available locally.

**Used in Production**

Pulling images is one of the first steps before running containers.

---

### Question 4

**Question**

How do you list, search, and remove Docker images?

**Answer**

List images:

```bash
docker images
```

Search Docker Hub:

```bash
docker search nginx
```

Remove an image:

```bash
docker rmi nginx
```

Remove by Image ID:

```bash
docker rmi IMAGE_ID
```

**Explanation**

These commands help manage locally stored images.

**Used in Production**

Image cleanup prevents unnecessary disk usage.

---

### Question 5

**Question**

What are Docker Image Tags?

**Answer**

Tags identify different versions of an image.

Examples:

```
nginx:latest
nginx:1.27
ubuntu:24.04
```

Pull a tagged image:

```bash
docker pull nginx:1.27
```

**Explanation**

Tags allow multiple versions of the same image to coexist.

**Used in Production**

Production environments should use version-specific tags instead of `latest`.

**Common Mistake**

Using the `latest` tag in production can result in unexpected deployments.

---

### Question 6

**Question**

What is a Docker Container?

**Answer**

A Docker Container is a running instance of a Docker image.

It includes:

- Application process
- Writable layer
- Isolated filesystem
- Network configuration

Containers are lightweight and share the host operating system kernel.

**Explanation**

Multiple containers can be created from the same image.

**Used in Production**

Applications, databases, web servers, and microservices commonly run inside containers.

---

### Question 7

**Question**

How do you create and run Docker containers?

**Answer**

Run a container:

```bash
docker run nginx
```

Run in detached mode:

```bash
docker run -d nginx
```

Run with port mapping:

```bash
docker run -d -p 8080:80 nginx
```

**Explanation**

`docker run` creates and starts a new container.

**Used in Production**

Containers are typically started with networking, environment variables, and mounted volumes.

---

### Question 8

**Question**

What is the difference between Interactive Mode and Detached Mode?

**Answer**

| Interactive Mode | Detached Mode |
|------------------|---------------|
| Terminal attached | Runs in background |
| Used for debugging | Used for production |
| Container exits when terminal closes (unless process continues) | Continues running independently |

Interactive:

```bash
docker run -it ubuntu bash
```

Detached:

```bash
docker run -d nginx
```

**Explanation**

Interactive mode is useful for troubleshooting, while detached mode is used for long-running services.

---

### Question 9

**Question**

How do you manage container lifecycle operations?

**Answer**

Start:

```bash
docker start container_name
```

Stop:

```bash
docker stop container_name
```

Restart:

```bash
docker restart container_name
```

Pause:

```bash
docker pause container_name
```

Unpause:

```bash
docker unpause container_name
```

Remove:

```bash
docker rm container_name
```

**Explanation**

These commands control container execution.

**Used in Production**

Used daily for container administration.

---

### Question 10

**Question**

How do you inspect a container and view its logs?

**Answer**

Inspect container:

```bash
docker inspect container_name
```

View logs:

```bash
docker logs container_name
```

Follow logs:

```bash
docker logs -f container_name
```

**Explanation**

Inspection provides detailed metadata, while logs help troubleshoot running applications.

**Used in Production**

These are among the most frequently used troubleshooting commands.

---

### Question 11

**Question**

How do you execute commands inside a running container?

**Answer**

Open an interactive shell:

```bash
docker exec -it container_name bash
```

Execute a command:

```bash
docker exec container_name ls
```

**Explanation**

`docker exec` runs commands inside an already running container without restarting it.

**Used in Production**

Used for debugging, configuration verification, and troubleshooting.

**Common Mistake**

Many candidates confuse `docker exec` with `docker run`. `docker run` creates a new container, whereas `docker exec` uses an existing one.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

A developer says, "I have an image, so my application is already running." Is this correct?

**Answer**

No.

A Docker image is only a template. The application runs only after a container is created from that image.

**Explanation**

Images are static; containers are the running instances.

---

### Scenario 2

**Question**

You need to deploy version 1.25 of Nginx instead of the latest version. How would you do it?

**Answer**

Pull and run the specific version:

```bash
docker pull nginx:1.25
```

```bash
docker run -d nginx:1.25
```

**Explanation**

Using version-specific tags ensures consistent deployments.

---

### Scenario 3

**Question**

A running web application suddenly becomes inaccessible. How would you verify whether the Docker container is still running?

**Answer**

Check running containers:

```bash
docker ps
```

Check all containers:

```bash
docker ps -a
```

**Explanation**

These commands reveal whether the container has stopped or exited unexpectedly.

---

### Scenario 4

**Question**

A container exits immediately after you start it. What should you investigate first?

**Answer**

View the logs:

```bash
docker logs container_name
```

Inspect the container:

```bash
docker inspect container_name
```

**Explanation**

Logs typically reveal startup errors such as configuration issues, missing files, or application failures.

---

### Scenario 5

**Question**

You need to troubleshoot an application inside a running container. How would you access it?

**Answer**

Open a shell:

```bash
docker exec -it container_name bash
```

If Bash is unavailable:

```bash
docker exec -it container_name sh
```

**Explanation**

`docker exec` provides direct access without restarting the container.

---

### Scenario 6

**Question**

Your server is running out of disk space because of unused Docker images. How would you identify and remove them?

**Answer**

List images:

```bash
docker images
```

Remove unused images:

```bash
docker image prune
```

Remove a specific image:

```bash
docker rmi IMAGE_ID
```

**Explanation**

Cleaning unused images helps recover disk space on Docker hosts.

---

### Scenario 7

**Question**

A developer accidentally removes a running container. Can it be restarted?

**Answer**

No.

Once a container is removed using:

```bash
docker rm
```

it cannot be restarted. A new container must be created from the image.

**Explanation**

Containers are disposable runtime instances.

---

### Scenario 8

**Question**

Your manager wants a web server to continue running after you close the terminal. Which Docker mode should you use?

**Answer**

Run the container in detached mode:

```bash
docker run -d nginx
```

**Explanation**

Detached mode allows services to run in the background.

---

### Scenario 9

**Question**

A production container is consuming excessive CPU, and you need to inspect its configuration without stopping it. Which command would you use?

**Answer**

```bash
docker inspect container_name
```

**Explanation**

`docker inspect` provides runtime details such as networking, mounts, environment variables, and resource configuration.

---

### Scenario 10

**Question**

Your application is running inside a container, but you need to monitor its live output while users are accessing it. Which command would you use?

**Answer**

```bash
docker logs -f container_name
```

**Explanation**

The `-f` option follows the log output in real time, making it useful for production troubleshooting.

---

### Scenario 11

**Question**

You are deploying a containerized web application on a Linux server. Describe the complete workflow from obtaining the image to troubleshooting the running container.

**Answer**

A typical workflow is:

1. Search for the required image:

```bash
docker search nginx
```

2. Pull the desired version:

```bash
docker pull nginx:1.27
```

3. Verify the image:

```bash
docker images
```

4. Run the container in detached mode with port mapping:

```bash
docker run -d -p 8080:80 --name webserver nginx:1.27
```

5. Verify that the container is running:

```bash
docker ps
```

6. Inspect its configuration:

```bash
docker inspect webserver
```

7. Monitor application logs:

```bash
docker logs -f webserver
```

8. Access the container if troubleshooting is required:

```bash
docker exec -it webserver bash
```

9. Restart the container if needed:

```bash
docker restart webserver
```

10. Remove the container when it is no longer required:

```bash
docker stop webserver
docker rm webserver
```

**Explanation**

This workflow represents the day-to-day operations performed by DevOps and Cloud engineers. It demonstrates image management, container lifecycle operations, troubleshooting, logging, and runtime inspection—topics that are frequently covered in Docker interviews.
