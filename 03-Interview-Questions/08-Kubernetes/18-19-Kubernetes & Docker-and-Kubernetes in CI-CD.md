# Kubernetes & Docker Integration and Kubernetes in CI/CD Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

How are Docker and Kubernetes related?

**Answer**

Docker (or another container runtime) is used to build and package applications into container images, while Kubernetes is used to deploy, manage, scale, and orchestrate those containers across a cluster.

**Explanation**

Docker focuses on container creation, whereas Kubernetes focuses on container orchestration.

**Used in Production**

- Building images using Docker
- Deploying images on Kubernetes clusters
- Managing application lifecycle

**Common Mistake**

Many candidates say Kubernetes replaces Docker. Kubernetes replaces container orchestration, not container image creation.

---

### Question 2

**Question**

What is a container image in Kubernetes?

**Answer**

A container image is a read-only package containing:

- Application code
- Runtime
- Libraries
- Dependencies
- Configuration required to run the application

Kubernetes uses these images to create containers inside Pods.

**Explanation**

Images are immutable and ensure applications run consistently across environments.

**Used in Production**

Every Kubernetes workload references a container image.

---

### Question 3

**Question**

What is an Image Registry?

**Answer**

An Image Registry stores and distributes container images.

Common registries include:

- Docker Hub
- Azure Container Registry (ACR)
- Amazon Elastic Container Registry (ECR)
- Google Artifact Registry
- Harbor

**Explanation**

Before Kubernetes starts a container, it pulls the required image from a registry.

**Used in Production**

Private registries are commonly used to store enterprise application images.

---

### Question 4

**Question**

What is the Image Pull Policy in Kubernetes?

**Answer**

Image Pull Policy determines when Kubernetes pulls a container image.

Available options:

- `Always`
- `IfNotPresent`
- `Never`

**Explanation**

- **Always** – Pull every time the Pod starts.
- **IfNotPresent** – Pull only if the image is not available locally.
- **Never** – Use only local images.

**Used in Production**

`IfNotPresent` is commonly used for stable releases, while `Always` is often used during development.

**Common Mistake**

Using the `latest` tag with `IfNotPresent`, which may prevent updated images from being downloaded.

---

### Question 5

**Question**

Why should image tags be used instead of the `latest` tag?

**Answer**

Versioned image tags provide predictable deployments and make rollbacks easier.

Example:

```text
myapp:v1.2.0
```

instead of

```text
myapp:latest
```

**Explanation**

Specific tags ensure every deployment uses the intended application version.

**Used in Production**

All production deployments use versioned image tags.

---

### Question 6

**Question**

How does Kubernetes deploy an application?

**Answer**

The typical deployment process is:

1. Build the application.
2. Create a Docker image.
3. Push the image to a registry.
4. Update the Deployment YAML.
5. Apply the manifest using `kubectl apply`.

**Explanation**

Kubernetes creates Pods based on the Deployment specification and continuously maintains the desired state.

---

### Question 7

**Question**

How do you update an application image in Kubernetes?

**Answer**

Update the Deployment with the new image.

Example:

```bash
kubectl set image deployment/web-app web-app=myrepo/web-app:v2
```

or modify the YAML manifest and run:

```bash
kubectl apply -f deployment.yaml
```

**Explanation**

Kubernetes performs a Rolling Update by default.

**Used in Production**

CI/CD pipelines commonly update images automatically after successful builds.

---

### Question 8

**Question**

What is a Rolling Deployment?

**Answer**

A Rolling Deployment gradually replaces old Pods with new Pods without downtime.

**Explanation**

New Pods are created before old Pods are terminated, ensuring application availability during updates.

**Used in Production**

Standard deployment strategy for production workloads.

---

### Question 9

**Question**

How do you verify whether a deployment completed successfully?

**Answer**

Common commands include:

```bash
kubectl rollout status deployment <deployment-name>

kubectl get pods

kubectl get deployments
```

**Explanation**

These commands confirm that all replicas are running and the rollout has completed successfully.

---

### Question 10

**Question**

What is a typical Kubernetes CI/CD deployment workflow?

**Answer**

1. Developer pushes code to Git.
2. CI tool builds the application.
3. Docker image is created.
4. Image is pushed to the registry.
5. Kubernetes Deployment is updated.
6. Rolling Update begins.
7. Deployment is verified.

**Explanation**

This automated workflow reduces manual intervention and ensures consistent deployments.

**Used in Production**

Widely implemented using Jenkins, GitHub Actions, Azure DevOps, GitLab CI, or similar tools.

---

### Question 11

**Question**

Why should application images be stored in a registry instead of on worker nodes?

**Answer**

A registry provides:

- Centralized image storage
- Version control
- High availability
- Secure distribution
- Consistent deployments across clusters

**Explanation**

Worker nodes pull images from the registry whenever required.

---

### Question 12

**Question**

Which commands are commonly used after deploying an application to Kubernetes?

**Answer**

```bash
kubectl get deployments

kubectl get pods

kubectl rollout status deployment

kubectl describe deployment

kubectl logs <pod-name>
```

**Explanation**

These commands verify deployment success and help identify any issues immediately after deployment.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

A developer builds a new Docker image but Kubernetes continues running the old application version. What would you check?

**Answer**

Verify:

- Deployment image tag
- Image Pull Policy
- Deployment rollout status
- Whether the new image was pushed successfully

**Explanation**

Kubernetes cannot deploy a new version if the Deployment still references the old image or the image was not pulled.

---

### Scenario 2

**Question**

Your Deployment uses the `latest` image tag, but the application does not update after deployment. What is the likely cause?

**Answer**

The node may already have the `latest` image cached and the Image Pull Policy may be `IfNotPresent`.

**Explanation**

Using explicit version tags with appropriate pull policies avoids this issue.

---

### Scenario 3

**Question**

Your CI pipeline successfully builds a Docker image. What should happen next in a Kubernetes deployment pipeline?

**Answer**

1. Push the image to the registry.
2. Update the Deployment image.
3. Apply the Deployment.
4. Verify the rollout.

**Explanation**

These steps ensure Kubernetes deploys the newly built application version.

---

### Scenario 4

**Question**

After deploying version 2 of your application, users report errors. How can you quickly restore the previous version?

**Answer**

Run:

```bash
kubectl rollout undo deployment <deployment-name>
```

**Explanation**

Rollback restores the previous Deployment revision with minimal downtime.

---

### Scenario 5

**Question**

Your Deployment fails because Kubernetes cannot download the application image. What should you investigate?

**Answer**

Check:

- Image name
- Image tag
- Registry availability
- Image pull secret
- Registry authentication

**Explanation**

Most deployment failures involving images are caused by incorrect registry configuration or authentication.

---

### Scenario 6

**Question**

A Deployment reports success, but only some Pods are running while others are still being replaced. Is this expected?

**Answer**

Yes.

This is normal behavior during a Rolling Deployment.

**Explanation**

Kubernetes gradually replaces old Pods with new ones to minimize downtime.

---

### Scenario 7

**Question**

You need to confirm that the new application version has been successfully deployed after a CI/CD pipeline finishes. Which commands would you use?

**Answer**

```bash
kubectl rollout status deployment <deployment-name>

kubectl get pods

kubectl get deployments
```

**Explanation**

These commands verify rollout completion and confirm the desired number of updated Pods are running.

---

### Scenario 8

**Question**

A developer accidentally pushed an image with an incorrect tag. What impact can this have on Kubernetes deployments?

**Answer**

Kubernetes may fail with an `ImagePullBackOff` error because it cannot locate the specified image.

**Explanation**

Image tags in the Deployment must exactly match the tags available in the registry.

---

### Scenario 9

**Question**

Your organization wants every application deployment to be fully automated after code is merged into the main branch. What is the recommended workflow?

**Answer**

Implement a CI/CD pipeline that:

1. Builds the application.
2. Runs tests.
3. Builds the Docker image.
4. Pushes the image to the registry.
5. Updates the Kubernetes Deployment.
6. Performs a Rolling Update.
7. Verifies the deployment.

**Explanation**

This workflow enables reliable, repeatable, and automated software delivery.

---

### Scenario 10

**Question**

During a production deployment, some users continue accessing the old application version while others receive the new version. Is this expected?

**Answer**

Yes.

This behavior is expected during a Rolling Deployment because Kubernetes gradually replaces Pods while maintaining application availability.

**Explanation**

Traffic is served by both old and new Pods until the rollout completes successfully, ensuring minimal or zero downtime.
