# Containers & Kubernetes

## Definition

- Containers package an application with all its dependencies so it runs consistently across different environments.
- Kubernetes is a container orchestration platform that automates deployment, scaling, networking, and management of containers.
- In Azure, **Azure Kubernetes Service (AKS)** provides a managed Kubernetes platform.

---

## Why is it used?

- Build portable applications.
- Simplify deployments.
- Scale applications automatically.
- Improve resource utilization.
- Support microservices architecture.
- Reduce environment-related issues.

---

## Key Features

- Lightweight virtualization.
- Fast startup.
- Platform independence.
- Automatic scaling.
- High availability.
- Self-healing.

---

## Advantages

- Faster deployments.
- Better resource utilization.
- Easy scalability.
- Consistent environments.
- Supports DevOps workflows.

---

## Disadvantages

- Kubernetes has a steep learning curve.
- Requires proper monitoring and networking.

---

## Components

- Docker
- Images
- Containers
- Dockerfile
- Docker Compose
- Azure Container Registry (ACR)
- Azure Kubernetes Service (AKS)

---

## Workflow

```text
Write Application
       ↓
Create Docker Image
       ↓
Push Image to ACR
       ↓
Deploy to AKS
       ↓
Users Access Application
```

---

## Real-world Example

A company packages its web application into a Docker image, stores it in Azure Container Registry, and deploys it to Azure Kubernetes Service.

---

## Interview Tip

"Docker packages applications into containers, while Kubernetes manages those containers at scale."

---

## Quick Revision

- Containers package applications.
- Docker creates containers.
- Kubernetes manages containers.
- AKS is Azure's managed Kubernetes service.
- ACR stores container images.
- Containers are lightweight.

---

## Important Interview Questions

1. What are containers?
2. What is Kubernetes?
3. What is the difference between Docker and Kubernetes?
4. What is AKS?
5. Why are containers popular?

---

# Docker Basics

## Definition

- Docker is a containerization platform that packages applications and their dependencies into containers.
- Containers run consistently across development, testing, and production environments.

---

## Why is it used?

- Package applications.
- Eliminate environment issues.
- Simplify deployments.
- Improve portability.
- Support CI/CD.

---

## Key Features

- Lightweight containers.
- Image-based deployment.
- Fast startup.
- Isolation.
- Cross-platform support.

---

## Advantages

- Portable.
- Fast.
- Efficient resource usage.
- Easy deployment.

---

## Disadvantages

- Containers share the host OS kernel.
- Requires image management.

---

## Workflow

```text
Application
      ↓
Dockerfile
      ↓
Docker Image
      ↓
Docker Container
```

---

## Real-world Example

A developer packages a Node.js application into a Docker container and runs it on Windows, Linux, and Azure without modification.

---

## Interview Tip

"Docker packages applications and dependencies into portable containers."

---

## Quick Revision

- Container platform.
- Portable.
- Fast startup.
- Uses Images.
- Uses Dockerfile.

---

## Important Interview Questions

1. What is Docker?
2. Why is Docker used?
3. What are Docker containers?
4. What is Docker Engine?
5. What is the difference between Docker and Virtual Machines?

---

# Docker Images

## Definition

- A Docker Image is a read-only template used to create Docker containers.
- It contains the application, runtime, libraries, and dependencies.

---

## Why is it used?

- Create containers.
- Package applications.
- Version application builds.
- Enable portability.

---

## Key Features

- Read-only.
- Layered architecture.
- Versioned using tags.
- Reusable.

---

## Advantages

- Easy deployment.
- Consistent environments.
- Lightweight.

---

## Disadvantages

- Large images increase deployment time.
- Poor image design increases storage usage.

---

## Workflow

```text
Dockerfile
      ↓
Docker Build
      ↓
Docker Image
      ↓
Docker Run
```

---

## Real-world Example

A company stores application images in Azure Container Registry before deploying them to AKS.

---

## Interview Tip

"A Docker Image is a blueprint used to create Docker containers."

---

## Quick Revision

- Read-only template.
- Layered.
- Tagged versions.
- Creates containers.

---

## Important Interview Questions

1. What is a Docker Image?
2. How is an Image created?
3. What are Image layers?
4. Where are Images stored?
5. What is the difference between an Image and a Container?

---

# Docker Containers

## Definition

- A Docker Container is a running instance of a Docker Image.
- It contains the application and executes it in an isolated environment.

---

## Why is it used?

- Run applications.
- Isolate workloads.
- Improve portability.
- Simplify deployment.

---

## Key Features

- Lightweight.
- Isolated.
- Fast startup.
- Share host OS kernel.

---

## Advantages

- Portable.
- Efficient.
- Easy scaling.
- Consistent.

---

## Disadvantages

- Depends on container runtime.
- Containers are ephemeral unless persistent storage is used.

---

## Workflow

```text
Docker Image
      ↓
docker run
      ↓
Container Running
```

---

## Real-world Example

An Nginx Docker container serves a company's website inside AKS.

---

## Interview Tip

"A container is a running instance of a Docker Image."

---

## Quick Revision

- Running Image.
- Lightweight.
- Isolated.
- Portable.
- Fast startup.

---

## Important Interview Questions

1. What is a Docker Container?
2. How is a Container different from an Image?
3. Why are Containers lightweight?
4. What happens when a container stops?
5. Can multiple containers use the same image?

---

# Dockerfile

## Definition

- A Dockerfile is a text file containing instructions to build a Docker Image.
- Each instruction creates a new image layer.

---

## Why is it used?

- Automate image creation.
- Standardize builds.
- Version container configuration.
- Support CI/CD.

---

## Common Instructions

```dockerfile
FROM
RUN
COPY
ADD
WORKDIR
EXPOSE
ENV
CMD
ENTRYPOINT
```

---

## Workflow

```text
Dockerfile
      ↓
docker build
      ↓
Docker Image
```

---

## Real-world Example

A Java application uses a Dockerfile to install Java, copy the application, and start it automatically.

---

## Interview Tip

"A Dockerfile defines how a Docker Image is built."

---

## Quick Revision

- Build instructions.
- Text file.
- Creates Images.
- Layer-based.
- Used in CI/CD.

---

## Important Interview Questions

1. What is a Dockerfile?
2. What is the FROM instruction?
3. Difference between CMD and ENTRYPOINT?
4. What is docker build?
5. Why use Dockerfiles?

---

# Docker Compose

## Definition

- Docker Compose is a tool used to define and run multiple Docker containers using a single YAML file.

---

## Why is it used?

- Run multi-container applications.
- Simplify local development.
- Define application architecture.
- Start all containers together.

---

## Key Features

- YAML configuration.
- Multiple services.
- Network creation.
- Volume management.
- One-command deployment.

---

## Advantages

- Easy development.
- Simple configuration.
- Faster testing.

---

## Disadvantages

- Intended mainly for single-host environments.
- Not suitable for production orchestration like Kubernetes.

---

## Workflow

```text
docker-compose.yml
        ↓
docker compose up
        ↓
Multiple Containers Running
```

---

## Real-world Example

A developer runs a web application, MySQL database, and Redis cache together using Docker Compose.

---

## Interview Tip

"Docker Compose manages multiple containers on a single host using one YAML file."

---

## Quick Revision

- Multi-container.
- YAML file.
- Local development.
- Single host.
- Simple deployment.

---

## Important Interview Questions

1. What is Docker Compose?
2. Why is Docker Compose used?
3. What file does Docker Compose use?
4. Is Docker Compose used in Kubernetes?
5. Difference between Docker and Docker Compose?

---

# Azure Container Registry (ACR)

## Definition

- Azure Container Registry (ACR) is a private Azure registry used to store and manage Docker and OCI container images.

---

## Why is it used?

- Store private images.
- Secure image distribution.
- Integrate with AKS.
- Support CI/CD pipelines.

---

## Key Features

- Private registry.
- Image versioning.
- Azure AD authentication.
- Geo-replication.
- Webhooks.
- Vulnerability scanning integration.

---

## Advantages

- Secure.
- Azure integration.
- High availability.
- Private image storage.

---

## Disadvantages

- Storage cost.
- Requires image lifecycle management.

---

## Workflow

```text
Docker Build
      ↓
Push Image to ACR
      ↓
AKS Pulls Image
```

---

## Real-world Example

A DevOps pipeline builds a Docker image and pushes it to Azure Container Registry before deploying to AKS.

---

## Interview Tip

"Azure Container Registry securely stores container images for Azure deployments."

---

## Quick Revision

- Private registry.
- Stores Docker images.
- Integrates with AKS.
- Supports CI/CD.
- Azure-native.

---

## Important Interview Questions

1. What is Azure Container Registry?
2. Why use ACR?
3. How does AKS use ACR?
4. What is image versioning?
5. Can ACR store Helm charts?

---

# Azure Kubernetes Service (AKS)

## Definition

- Azure Kubernetes Service (AKS) is Microsoft's managed Kubernetes service.
- Azure manages the Kubernetes control plane, while users manage worker nodes and applications.

---

## Why is it used?

- Deploy containers.
- Scale applications.
- Automate deployments.
- Improve availability.
- Simplify Kubernetes management.

---

## Key Features

- Managed Kubernetes.
- Automatic upgrades.
- Auto Scaling.
- Self-healing.
- Azure AD integration.
- Azure Monitor integration.

---

## Advantages

- Managed control plane.
- High availability.
- Easy scaling.
- Azure integration.

---

## Disadvantages

- Kubernetes knowledge required.
- Networking can be complex.

---

## Components

- Control Plane (Managed by Azure)
- Worker Nodes
- Pods
- Deployments
- Services
- Ingress

---

## Workflow

```text
Docker Image
      ↓
Azure Container Registry
      ↓
AKS Cluster
      ↓
Pods Running
```

---

## Real-world Example

A banking application runs hundreds of containers across multiple AKS nodes with automatic scaling.

---

## Interview Tip

"AKS is a managed Kubernetes service where Azure manages the control plane."

---

## Quick Revision

- Managed Kubernetes.
- Uses Pods.
- Uses Deployments.
- Uses Services.
- Auto Scaling.
- Self-healing.

---

## Important Interview Questions

1. What is AKS?
2. What does Azure manage in AKS?
3. Why use AKS instead of self-managed Kubernetes?
4. How does AKS scale?
5. How does AKS integrate with ACR?

---

# Kubernetes Pods

## Definition

- A Pod is the smallest deployable unit in Kubernetes.
- It contains one or more tightly coupled containers that share networking and storage.

---

## Why is it used?

- Run containers.
- Share storage.
- Share networking.
- Deploy applications.

---

## Key Features

- Smallest Kubernetes object.
- Shared IP address.
- Shared volumes.
- Ephemeral by nature.

---

## Real-world Example

A Pod runs an Nginx web server container along with a sidecar container for log collection.

---

## Interview Tip

"A Pod is the smallest deployment unit in Kubernetes and usually contains one application container."

---

## Quick Revision

- Smallest Kubernetes object.
- Contains containers.
- Shared IP.
- Ephemeral.

---

## Important Interview Questions

1. What is a Pod?
2. Can a Pod contain multiple containers?
3. Why are Pods ephemeral?
4. What resources do containers in a Pod share?
5. Is a Pod permanent?

---

# Kubernetes Deployments

## Definition

- A Deployment manages Pods and ensures the desired number of Pod replicas are running.

---

## Why is it used?

- Deploy applications.
- Perform rolling updates.
- Roll back deployments.
- Maintain desired state.

---

## Key Features

- Rolling updates.
- Rollbacks.
- Replica management.
- Self-healing.

---

## Workflow

```text
Deployment
      ↓
ReplicaSet
      ↓
Pods
```

---

## Real-world Example

A Deployment maintains five running web server Pods even if one Pod crashes.

---

## Interview Tip

"A Deployment manages Pods and ensures the desired application state."

---

## Quick Revision

- Manages Pods.
- Rolling updates.
- Rollbacks.
- Uses ReplicaSets.

---

## Important Interview Questions

1. What is a Deployment?
2. What is a rolling update?
3. Can Deployments perform rollbacks?
4. How are Pods managed?
5. What is the relationship between Deployment and ReplicaSet?

---

# ReplicaSets

## Definition

- A ReplicaSet ensures that the specified number of Pod replicas are always running.

---

## Why is it used?

- Maintain application availability.
- Replace failed Pods.
- Scale applications.

---

## Key Features

- Self-healing.
- Replica management.
- Automatic Pod recreation.

---

## Workflow

```text
ReplicaSet
      ↓
Desired Pods
      ↓
Failed Pod
      ↓
New Pod Created
```

---

## Real-world Example

If one Pod crashes, ReplicaSet immediately creates another Pod.

---

## Interview Tip

"ReplicaSets maintain the desired number of running Pods."

---

## Quick Revision

- Maintains replicas.
- Self-healing.
- Managed by Deployments.
- Recreates failed Pods.

---

## Important Interview Questions

1. What is a ReplicaSet?
2. Why use ReplicaSets?
3. Does Deployment create ReplicaSets?
4. How does ReplicaSet recover failed Pods?
5. Difference between Deployment and ReplicaSet?

---

# Kubernetes Services

## Definition

- A Service provides a stable network endpoint for accessing Pods.
- It enables communication between applications inside and outside the cluster.

---

## Why is it used?

- Expose applications.
- Load balance traffic.
- Enable service discovery.
- Decouple applications from Pod IP changes.

---

## Types

- ClusterIP
- NodePort
- LoadBalancer
- ExternalName

---

## Workflow

```text
User
      ↓
Service
      ↓
Pods
```

---

## Real-world Example

A LoadBalancer Service exposes an e-commerce application to internet users.

---

## Interview Tip

"A Service provides a stable IP and DNS name for accessing Pods."

---

## Quick Revision

- Stable networking.
- Load balancing.
- Service discovery.
- Multiple service types.

---

## Important Interview Questions

1. What is a Kubernetes Service?
2. What are Service types?
3. Why do Pods need Services?
4. What is ClusterIP?
5. What is LoadBalancer Service?

---

# Kubernetes Ingress

## Definition

- Ingress manages external HTTP and HTTPS access to services within a Kubernetes cluster.
- It provides Layer 7 routing based on hostnames and URL paths.

---

## Why is it used?

- Route HTTP traffic.
- Support multiple applications.
- SSL termination.
- Centralized routing.

---

## Key Features

- URL routing.
- Host-based routing.
- TLS termination.
- Single external IP.

---

## Workflow

```text
Internet
      ↓
Ingress Controller
      ↓
Service
      ↓
Pods
```

---

## Real-world Example

An Ingress routes `/api` to an API service and `/shop` to a shopping service.

---

## Interview Tip

"Ingress manages HTTP/HTTPS traffic and routes requests to Kubernetes Services."

---

## Quick Revision

- HTTP routing.
- URL-based routing.
- Host-based routing.
- SSL termination.

---

## Important Interview Questions

1. What is Kubernetes Ingress?
2. What is an Ingress Controller?
3. Why use Ingress instead of LoadBalancer?
4. What routing methods are supported?
5. Does Ingress work at Layer 7?

---

# ConfigMaps

## Definition

- ConfigMaps store non-sensitive configuration data separately from container images.

---

## Why is it used?

- Separate configuration from code.
- Reuse configuration.
- Simplify deployments.

---

## Key Features

- Key-value pairs.
- Mounted as files or environment variables.
- Easy updates.

---

## Real-world Example

A ConfigMap stores the application's database hostname.

---

## Interview Tip

"ConfigMaps store configuration data that is not sensitive."

---

## Quick Revision

- Configuration.
- Non-sensitive.
- Key-value.
- Environment variables.

---

## Important Interview Questions

1. What is a ConfigMap?
2. Why use ConfigMaps?
3. How are ConfigMaps used?
4. Can ConfigMaps store passwords?
5. How are ConfigMaps mounted?

---

# Kubernetes Secrets

## Definition

- Secrets store sensitive information such as passwords, API keys, certificates, and tokens.
- Kubernetes stores Secrets separately from application configuration.

---

## Why is it used?

- Protect sensitive data.
- Secure credentials.
- Manage certificates.
- Avoid storing passwords in code.

---

## Key Features

- Base64-encoded storage.
- Mounted as files or environment variables.
- Access controlled.
- Supports encryption at rest (when enabled).

---

## Advantages

- Improves security.
- Separates credentials from code.
- Easy integration with Pods.

---

## Disadvantages

- Base64 encoding is **not encryption** by itself.
- Additional encryption should be enabled for production clusters.

---

## Workflow

```text
Create Secret
      ↓
Mount into Pod
      ↓
Application Reads Secret
```

---

## Real-world Example

A web application retrieves its database password from a Kubernetes Secret instead of storing it in the source code.

---

## Interview Tip

"ConfigMaps store non-sensitive configuration, while Secrets store sensitive information like passwords and API keys."

---

## Quick Revision

- Sensitive data.
- Passwords.
- API Keys.
- Certificates.
- Mounted into Pods.
- Base64 encoded.

---

## Important Interview Questions

1. What is a Kubernetes Secret?
2. What is the difference between ConfigMaps and Secrets?
3. How are Secrets used by Pods?
4. Are Kubernetes Secrets encrypted by default?
5. Why shouldn't passwords be stored in container images?
