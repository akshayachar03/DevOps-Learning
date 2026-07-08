# Dockerfile Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is a Dockerfile?

**Answer**

A Dockerfile is a text file that contains a sequence of instructions used to automatically build a Docker image. Each instruction creates a new image layer, making image creation consistent, repeatable, and version-controlled.

**Explanation**

A Dockerfile acts as the blueprint for creating Docker images. Instead of manually configuring containers every time, Docker reads the Dockerfile from top to bottom and builds the image step by step.

**Used in Production**

- Building application images in CI/CD pipelines
- Standardizing application environments
- Automating deployments
- Version controlling infrastructure

**Common Mistake**

Many candidates think a Dockerfile creates containers. It actually creates **images**, from which containers are created.

---

### Question 2

**Question**

Explain the basic workflow of building a Docker image using a Dockerfile.

**Answer**

The typical workflow is:

1. Create a Dockerfile.
2. Add required instructions.
3. Build the image using:

```bash
docker build -t myapp:v1 .
```

4. Verify the image:

```bash
docker images
```

5. Run a container:

```bash
docker run myapp:v1
```

**Explanation**

Docker reads the Dockerfile sequentially, executes each instruction, creates image layers, and finally produces a reusable Docker image.

**Used in Production**

This workflow is used in almost every CI/CD pipeline.

---

### Question 3

**Question**

What is the purpose of the `FROM` instruction?

**Answer**

`FROM` specifies the base image on which the new image is built.

Example:

```dockerfile
FROM ubuntu:24.04
```

or

```dockerfile
FROM python:3.12
```

**Explanation**

Every Docker image starts with a base image unless using `FROM scratch`.

**Used in Production**

Applications are commonly built on official images such as:

- Ubuntu
- Alpine
- Python
- Node.js
- Nginx
- Java

**Common Mistake**

Forgetting the `FROM` instruction results in an invalid Dockerfile.

---

### Question 4

**Question**

What is the purpose of the `RUN` instruction?

**Answer**

`RUN` executes commands while building the image.

Example:

```dockerfile
RUN apt update && apt install -y nginx
```

**Explanation**

Commands run only during image creation, not when the container starts.

**Used in Production**

Common uses include:

- Installing packages
- Updating repositories
- Downloading dependencies
- Creating directories

**Common Mistake**

Candidates often confuse `RUN` with `CMD`. `RUN` executes during image build, while `CMD` executes when the container starts.

---

### Question 5

**Question**

What is the difference between `COPY` and `ADD`?

**Answer**

`COPY`

- Copies files from the local machine into the image.

Example:

```dockerfile
COPY app/ /app/
```

`ADD`

- Copies files
- Can automatically extract local tar archives
- Supports downloading files from URLs (not recommended for most cases)

Example:

```dockerfile
ADD archive.tar.gz /app
```

**Explanation**

For most use cases, `COPY` is preferred because it is simpler and more predictable.

**Used in Production**

Most Dockerfiles primarily use `COPY`.

**Common Mistake**

Using `ADD` unnecessarily when `COPY` is sufficient.

---

### Question 6

**Question**

What is the purpose of the `WORKDIR` instruction?

**Answer**

`WORKDIR` sets the working directory for subsequent instructions.

Example:

```dockerfile
WORKDIR /app
```

**Explanation**

After setting the working directory, commands like `COPY`, `RUN`, and `CMD` execute relative to that directory.

**Used in Production**

Almost every Dockerfile defines a working directory.

**Common Mistake**

Using multiple `cd` commands inside `RUN` instead of defining `WORKDIR`.

---

### Question 7

**Question**

What is the purpose of the `ENV` instruction?

**Answer**

`ENV` defines environment variables inside the image.

Example:

```dockerfile
ENV APP_ENV=production
```

**Explanation**

Environment variables are available to the application running inside the container.

**Used in Production**

Used for:

- Application configuration
- Runtime settings
- Default environment values

**Common Mistake**

Storing passwords or API keys using `ENV`. Sensitive data should be stored in Docker Secrets or external secret management solutions.

---

### Question 8

**Question**

What is the purpose of the `EXPOSE` instruction?

**Answer**

`EXPOSE` documents which network port the application listens on.

Example:

```dockerfile
EXPOSE 80
```

**Explanation**

`EXPOSE` does **not** publish the port.

Ports become accessible only when mapped using:

```bash
docker run -p 8080:80 image
```

**Used in Production**

Used as documentation and by orchestration tools.

**Common Mistake**

Believing that `EXPOSE` automatically opens firewall ports.

---

### Question 9

**Question**

What is the difference between `CMD` and `ENTRYPOINT`?

**Answer**

`CMD`

Provides the default command executed when the container starts.

Example:

```dockerfile
CMD ["python","app.py"]
```

`ENTRYPOINT`

Defines the main executable of the container.

Example:

```dockerfile
ENTRYPOINT ["python"]
CMD ["app.py"]
```

**Explanation**

- `CMD` can be overridden easily.
- `ENTRYPOINT` is intended to always run.

**Used in Production**

Applications that should always execute a specific program commonly use `ENTRYPOINT`.

**Common Mistake**

Confusing the roles of `CMD` and `ENTRYPOINT`.

---

### Question 10

**Question**

How do you build a Docker image?

**Answer**

Build the image:

```bash
docker build -t myapp:v1 .
```

Build with a specific Dockerfile:

```bash
docker build -f Dockerfile.prod -t myapp:v1 .
```

**Explanation**

Docker reads the Dockerfile from the current directory and builds the image.

**Used in Production**

CI/CD pipelines automatically execute `docker build`.

---

### Question 11

**Question**

What are Docker image tags, and why are they important?

**Answer**

Tags identify different versions of an image.

Examples:

```
myapp:v1
myapp:v2
myapp:latest
```

Apply a tag:

```bash
docker tag myapp:v1 myrepo/myapp:v1
```

**Explanation**

Tags enable version control and make deployments predictable.

**Used in Production**

Teams typically use version numbers, Git commit hashes, or build numbers as tags.

**Common Mistake**

Using only the `latest` tag for production deployments, which can lead to unintended upgrades.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

Your Docker image build fails because the base image cannot be found. Which instruction should you investigate first?

**Answer**

Check the `FROM` instruction to ensure the image name and tag are correct.

**Explanation**

An incorrect base image prevents Docker from building subsequent layers.

---

### Scenario 2

**Question**

Your application cannot find its source code after the image is built. Which Dockerfile instruction is most likely responsible?

**Answer**

Inspect the `COPY` or `ADD` instruction to verify that the correct files and paths are being copied into the image.

**Explanation**

Incorrect source or destination paths are a common cause of missing application files.

---

### Scenario 3

**Question**

A container starts successfully but exits immediately. Which Dockerfile instruction would you check first?

**Answer**

Review the `CMD` or `ENTRYPOINT` instruction to ensure the correct application or executable is being started.

**Explanation**

If the main process exits, Docker stops the container.

---

### Scenario 4

**Question**

Your application fails because it cannot locate configuration files after changing directories in multiple `RUN` commands. How would you improve the Dockerfile?

**Answer**

Use the `WORKDIR` instruction instead of repeatedly changing directories with `cd`.

Example:

```dockerfile
WORKDIR /app
```

**Explanation**

`WORKDIR` makes the Dockerfile cleaner, more readable, and less error-prone.

---

### Scenario 5

**Question**

Your development team stores database passwords using the `ENV` instruction. Is this a good practice?

**Answer**

No.

Sensitive information should not be stored in the Dockerfile because anyone with access to the image can inspect it.

**Explanation**

Use Docker Secrets, Kubernetes Secrets, Azure Key Vault, or runtime environment variables instead.

---

### Scenario 6

**Question**

Your application listens on port 8080, but users cannot access it even though the Dockerfile contains:

```dockerfile
EXPOSE 8080
```

What is the problem?

**Answer**

`EXPOSE` only documents the listening port. You must publish the port when starting the container.

Example:

```bash
docker run -p 8080:8080 myapp
```

**Explanation**

Many beginners incorrectly assume `EXPOSE` automatically makes the port accessible.

---

### Scenario 7

**Question**

Your CI/CD pipeline rebuilds the Docker image from scratch every time, making builds slow. How can you improve performance?

**Answer**

Optimize the Dockerfile to maximize layer caching by placing frequently changing instructions (such as `COPY . .`) near the end and stable instructions (such as package installation) earlier.

**Explanation**

Docker reuses unchanged layers, significantly reducing build time.

---

### Scenario 8

**Question**

A developer accidentally builds an image with the tag `latest` instead of the release version. What issue can this cause?

**Answer**

Production systems may deploy the wrong image version because `latest` is not a reliable version identifier.

**Explanation**

Use explicit version tags such as:

```
myapp:v2.1.0
```

or Git commit SHA tags.

---

### Scenario 9

**Question**

Your application requires a newer version of Python than the current image provides. Which Dockerfile instruction should be updated?

**Answer**

Update the base image in the `FROM` instruction.

Example:

```dockerfile
FROM python:3.12
```

**Explanation**

Changing the base image updates the runtime environment for the application.

---

### Scenario 10

**Question**

You need to distribute the same application image to development, testing, and production environments without rebuilding it. How would you achieve this?

**Answer**

Build the image once, assign appropriate version tags, push it to a registry, and deploy the same tagged image across all environments.

Example:

```bash
docker build -t myapp:v1.0 .
docker tag myapp:v1.0 myrepo/myapp:v1.0
docker push myrepo/myapp:v1.0
```

**Explanation**

Building once and promoting the same image through environments ensures consistency, reduces deployment errors, and aligns with CI/CD best practices.
