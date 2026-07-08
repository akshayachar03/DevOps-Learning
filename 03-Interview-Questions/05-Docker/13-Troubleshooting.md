# Docker Troubleshooting Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

How do you troubleshoot a Docker container that is not working as expected?

**Answer**

A structured troubleshooting approach is:

1. Check whether the container is running.
2. View container logs.
3. Inspect the container configuration.
4. Verify port mappings.
5. Check mounted volumes.
6. Verify the application process inside the container.
7. Review Docker daemon logs if necessary.

Useful commands:

```bash
docker ps -a
docker logs <container>
docker inspect <container>
docker exec -it <container> sh
```

**Explanation**

Docker troubleshooting should begin by identifying whether the issue is related to the application, container configuration, networking, storage, or the Docker engine itself.

**Used in Production**

This is the standard troubleshooting workflow followed by DevOps and SRE teams.

**Common Mistake**

Restarting or recreating containers without checking logs first, which may hide the original cause of the issue.

---

### Question 2

**Question**

How do you view logs of a Docker container?

**Answer**

Use:

```bash
docker logs <container_name>
```

View logs continuously:

```bash
docker logs -f <container_name>
```

Show the last 100 lines:

```bash
docker logs --tail 100 <container_name>
```

**Explanation**

Docker captures everything written to **stdout** and **stderr** by the application.

Logs usually reveal:

- Startup failures
- Configuration errors
- Missing files
- Database connection failures
- Runtime exceptions

**Used in Production**

Viewing logs is usually the first troubleshooting step when a container fails.

**Common Mistake**

Assuming an application writes logs inside the container instead of stdout.

---

### Question 3

**Question**

What information does the `docker inspect` command provide?

**Answer**

Example:

```bash
docker inspect mycontainer
```

It provides detailed JSON information including:

- Container ID
- Image used
- Environment variables
- Network configuration
- Mounted volumes
- Port mappings
- Restart policy
- Container state
- IP address

**Explanation**

`docker inspect` provides complete runtime configuration of Docker objects.

**Used in Production**

It is frequently used to troubleshoot networking, storage, and deployment issues.

**Common Mistake**

Using `docker inspect` only for containers—it also works for images, networks, and volumes.

---

### Question 4

**Question**

What causes Docker port conflicts?

**Answer**

A port conflict occurs when another application or container is already using the requested host port.

Example:

```bash
docker run -p 80:80 nginx
```

Error:

```
Bind for 0.0.0.0:80 failed
```

**Explanation**

Only one process can bind to a specific host port.

Resolve by:

- Using another host port
- Stopping the conflicting service
- Removing the conflicting container

**Used in Production**

Common when multiple web servers or containers use the same host.

**Common Mistake**

Assuming Docker assigns ports automatically.

---

### Question 5

**Question**

How do you troubleshoot Docker volume-related issues?

**Answer**

Verify mounted volumes:

```bash
docker inspect container
```

List available volumes:

```bash
docker volume ls
```

Inspect a volume:

```bash
docker volume inspect volume_name
```

**Explanation**

Most volume issues occur because of:

- Wrong mount path
- Missing directories
- Incorrect permissions
- Mounting the wrong volume

**Used in Production**

Frequently encountered when containers cannot read or write application data.

---

### Question 6

**Question**

What are common reasons for Docker image pull failures?

**Answer**

Common causes include:

- Incorrect image name
- Wrong tag
- Authentication failure
- Private repository access
- Network issues
- Docker Hub rate limits

Example:

```bash
docker pull nginx:latest
```

**Explanation**

Docker checks the registry for the requested repository and tag.

If either is incorrect, the pull operation fails.

**Used in Production**

Common in CI/CD pipelines.

**Common Mistake**

Using `latest` when the repository only contains version-specific tags.

---

### Question 7

**Question**

Why does a Docker container immediately exit after starting?

**Answer**

Common reasons include:

- Application crashed
- Main process completed
- Configuration error
- Missing environment variables
- Missing dependencies

Troubleshoot using:

```bash
docker logs container_name
```

**Explanation**

A container remains running only while its primary process is active.

If the main process exits, Docker stops the container.

**Used in Production**

One of the most common Docker interview questions.

**Common Mistake**

Assuming Docker itself crashed rather than the application.

---

### Question 8

**Question**

How do you access a running Docker container for troubleshooting?

**Answer**

```bash
docker exec -it container_name bash
```

or

```bash
docker exec -it container_name sh
```

**Explanation**

This opens an interactive shell inside the running container.

Useful for:

- Checking files
- Viewing configuration
- Testing network connectivity
- Running application commands

**Used in Production**

Frequently used by DevOps engineers during incident investigation.

---

### Question 9

**Question**

What is the difference between `docker logs` and `docker exec`?

**Answer**

**docker logs**

Displays application output.

```bash
docker logs container
```

**docker exec**

Allows executing commands inside the running container.

```bash
docker exec -it container bash
```

**Explanation**

Logs help identify application errors, while exec allows deeper investigation inside the container.

**Used in Production**

Both commands are used together during troubleshooting.

---

### Question 10

**Question**

Which Docker commands are most commonly used during troubleshooting?

**Answer**

Common commands include:

```bash
docker ps -a
docker logs
docker inspect
docker exec
docker images
docker network ls
docker volume ls
docker stats
docker events
```

**Explanation**

These commands provide visibility into:

- Container status
- Logs
- Resource usage
- Networking
- Storage
- Runtime configuration

**Used in Production**

These are the core commands every Docker engineer should know.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

A Docker container exits immediately after startup. How would you troubleshoot it?

**Answer**

1. Check container status.

```bash
docker ps -a
```

2. View logs.

```bash
docker logs container_name
```

3. Inspect configuration.

```bash
docker inspect container_name
```

4. Verify environment variables.

5. Check whether the application process exited.

**Explanation**

Most immediate exits occur because the main application process failed to start.

---

### Scenario 2

**Question**

Your application is running inside a container, but users cannot access it through the browser. What would you check?

**Answer**

Verify:

- Container is running.
- Port mapping.

```bash
docker ps
```

Inspect ports:

```bash
docker inspect container
```

Check application logs.

```bash
docker logs container
```

Ensure firewall and security group rules allow the port.

**Explanation**

Most connectivity problems are caused by incorrect port mapping or the application not listening on the expected port.

---

### Scenario 3

**Question**

Your application cannot save uploaded files after the container restarts. How would you resolve it?

**Answer**

Check whether a Docker volume is mounted.

```bash
docker volume ls
```

Inspect:

```bash
docker inspect container
```

Create a persistent volume if needed.

**Explanation**

Container files are ephemeral. Persistent data should always be stored in Docker volumes or bind mounts.

---

### Scenario 4

**Question**

A deployment pipeline fails while pulling an image from Docker Hub. What would you verify?

**Answer**

Check:

- Image name
- Tag
- Internet connectivity
- Docker login
- Repository permissions
- Registry availability

Retry:

```bash
docker login
docker pull image:tag
```

**Explanation**

Authentication and incorrect image names are among the most common causes of pull failures.

---

### Scenario 5

**Question**

You receive the error:

```
Bind for 0.0.0.0:8080 failed
```

How would you resolve it?

**Answer**

Identify which process is already using the port.

Linux:

```bash
ss -tulpn
```

or

```bash
netstat -tulpn
```

Stop the conflicting process or run the container on another port.

Example:

```bash
docker run -p 8081:80 nginx
```

**Explanation**

Docker cannot bind to a host port that is already occupied.

---

### Scenario 6

**Question**

A container is running, but the application behaves unexpectedly. How would you investigate?

**Answer**

1. Check logs.

```bash
docker logs container
```

2. Enter the container.

```bash
docker exec -it container bash
```

3. Verify configuration files.

4. Check mounted volumes.

5. Test application connectivity.

**Explanation**

This approach determines whether the issue is related to configuration, dependencies, or runtime behavior.

---

### Scenario 7

**Question**

A container cannot connect to another container in the same application. What would you check?

**Answer**

Verify:

```bash
docker network ls
```

Inspect the network:

```bash
docker network inspect network_name
```

Ensure both containers are attached to the same Docker network.

**Explanation**

Containers communicate using Docker networks rather than localhost.

---

### Scenario 8

**Question**

Your container repeatedly restarts every few seconds. How would you troubleshoot it?

**Answer**

Check:

```bash
docker logs container
```

Inspect restart policy:

```bash
docker inspect container
```

Verify:

- Application startup
- Configuration
- Environment variables
- Database connectivity

**Explanation**

Continuous restarts usually indicate application startup failures combined with a restart policy such as `always`.

---

### Scenario 9

**Question**

You accidentally deleted a running container, but the application image still exists. How would you recover?

**Answer**

Verify the image:

```bash
docker images
```

Create a new container:

```bash
docker run -d image_name
```

Reconnect volumes and networks if required.

**Explanation**

Containers are disposable. As long as the image and persistent data exist, the container can be recreated.

---

### Scenario 10

**Question**

A production deployment fails after a new Docker image is released. What troubleshooting steps would you follow?

**Answer**

1. Verify the image exists in the registry.
2. Pull the image manually.

```bash
docker pull image:tag
```

3. Inspect container logs.

```bash
docker logs container
```

4. Verify environment variables.
5. Check port mappings.
6. Verify mounted volumes.
7. Compare configuration with the previous working version.

**Explanation**

This systematic approach isolates whether the failure is caused by the image, application configuration, networking, storage, or deployment process.
