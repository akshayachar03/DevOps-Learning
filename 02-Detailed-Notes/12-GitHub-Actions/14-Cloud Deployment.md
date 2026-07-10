# Cloud Deployment

## Overview

GitHub Actions provides built-in integrations to automate deployments to cloud platforms. One of the most common production use cases is deploying applications to **Microsoft Azure**.

A typical Azure deployment workflow includes:

- Build the application
- Authenticate with Azure
- Deploy the application
- Verify deployment
- Monitor the application

GitHub Actions supports deployments to:

- Azure App Service
- Azure Kubernetes Service (AKS)
- Azure Virtual Machines
- Azure Container Apps
- Azure Functions
- Azure Static Web Apps

> **Interview Tip**
>
> The most common Azure deployment flow in interviews is:
>
> **Checkout → Build → Azure Login → Deploy → Verify**

---

## Why It Is Used

Cloud Deployment helps to:

- Automate application deployments
- Reduce manual deployment errors
- Support Continuous Deployment (CD)
- Deploy consistently across environments
- Enable faster software releases
- Integrate seamlessly with Azure services

---

## Architecture / Working

```mermaid
flowchart LR

    A[Developer Push]
    B[GitHub Actions Workflow]
    C[Build Application]
    D[Azure Authentication]
    E[Deploy to Azure]
    F[Application Running]

    A --> B
    B --> C
    C --> D
    D --> E
    E --> F
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| GitHub Actions | Executes deployment workflow |
| Azure Login Action | Authenticates with Azure |
| Azure Subscription | Deployment target |
| Azure Resource | Hosts application |
| GitHub Secrets | Stores Azure credentials |

---

## Types (if applicable)

Common Azure deployment targets

- Azure App Service
- Azure Kubernetes Service (AKS)
- Azure Virtual Machines
- Azure Functions
- Azure Container Apps
- Azure Static Web Apps

---

## Lifecycle / Workflow (if applicable)

```mermaid
flowchart LR

    A[Code Push]
    B[Checkout]
    C[Build]
    D[Azure Login]
    E[Deploy]
    F[Application Available]

    A --> B
    B --> C
    C --> D
    D --> E
    E --> F
```

---

## Configuration / Syntax (if applicable)

Typical deployment workflow

```yaml
steps:

- uses: actions/checkout@v4

- uses: azure/login@v2
  with:
    creds: ${{ secrets.AZURE_CREDENTIALS }}

- run: echo "Deploy Application"
```

---

## Important Commands (if applicable)

Azure CLI

```bash
az login

az account show

az webapp deploy

kubectl apply -f deployment.yaml
```

---

## Important Files (if applicable)

```
.github/
└── workflows/
      deploy.yml

Dockerfile
deployment.yaml
service.yaml
```

---

## Real-World Use Cases

- Deploy Web Applications
- Deploy APIs
- Deploy Containers
- Kubernetes deployments
- Enterprise CI/CD pipelines

---

## Advantages

- Fully automated deployments
- Faster releases
- Reduced manual effort
- Native Azure integration
- Secure authentication

---

## Limitations

- Azure credentials must be configured correctly.
- Deployment failures stop the pipeline.
- Incorrect permissions prevent deployments.

---

## Common Interview Questions (Concept Only)

- How does GitHub Actions deploy to Azure?
- What authentication method is commonly used?
- Which Azure services support GitHub Actions?
- Where are Azure credentials stored?

---

## Common Mistakes

- Hardcoding Azure credentials
- Missing Azure Login step
- Incorrect Resource Group
- Deploying to the wrong subscription
- Using expired credentials

---

## Troubleshooting

| Problem | Possible Cause | Solution |
|----------|----------------|----------|
| Azure login failed | Invalid credentials | Verify GitHub Secrets |
| Deployment failed | Incorrect resource | Verify Azure resource names |
| Unauthorized | Missing permissions | Check Azure RBAC roles |
| Resource not found | Wrong subscription | Verify subscription selection |

---

## Summary

GitHub Actions enables secure and automated deployments to Azure services using Azure Login and deployment actions.

> **Interview Tip**
>
> Production deployments generally follow:
>
> **Checkout → Build → Authenticate → Deploy → Verify**

---

# Azure Authentication

## Overview

Before deploying to Azure, GitHub Actions must authenticate with the Azure subscription.

The official GitHub Action used is:

```yaml
azure/login
```

Authentication uses a **Service Principal** stored securely in GitHub Secrets.

> **Interview Tip**
>
> GitHub Actions does **not** log in using your personal Azure account. It uses a **Service Principal** for secure, automated access.

---

## Why It Is Used

Azure Authentication enables GitHub Actions to:

- Access Azure resources
- Deploy applications
- Manage infrastructure
- Execute Azure CLI commands

---

## Architecture / Working

```mermaid
flowchart LR

    A[GitHub Secrets]
    B[Azure Login Action]
    C[Azure Service Principal]
    D[Azure Subscription]

    A --> B
    B --> C
    C --> D
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| Azure Login Action | Performs authentication |
| Service Principal | Azure identity |
| GitHub Secret | Stores credentials |
| Azure Subscription | Deployment target |

---

## Types (if applicable)

Authentication methods

- Service Principal (Most Common)
- OpenID Connect (OIDC)
- Managed Identity (Azure-hosted scenarios)

> **Interview Tip**
>
> **Service Principal** is the most frequently asked authentication method.
>
> **OIDC** is the modern, recommended approach because it avoids storing long-lived secrets.

---

## Lifecycle / Workflow (if applicable)

```mermaid
flowchart LR

    A[Workflow]
    B[Read GitHub Secret]
    C[Authenticate]
    D[Azure Access]

    A --> B
    B --> C
    C --> D
```

---

## Configuration / Syntax (if applicable)

```yaml
- uses: azure/login@v2
  with:
    creds: ${{ secrets.AZURE_CREDENTIALS }}
```

---

## Important Commands (if applicable)

```bash
az login

az account show

az group list
```

---

## Important Files (if applicable)

Workflow YAML

---

## Real-World Use Cases

- Azure CLI automation
- Resource deployment
- AKS deployments
- App Service deployment

---

## Advantages

- Secure authentication
- Supports automation
- Integrates with Azure CLI

---

## Limitations

- Requires Azure configuration
- Credentials must be maintained securely

---

## Common Interview Questions (Concept Only)

- What is Azure Login Action?
- What is a Service Principal?
- Where should Azure credentials be stored?
- What is OIDC authentication?

---

## Common Mistakes

- Hardcoding credentials
- Incorrect JSON credentials
- Missing Azure permissions

---

## Troubleshooting

| Problem | Cause | Solution |
|----------|--------|----------|
| Login failed | Invalid credentials | Update GitHub Secrets |
| Permission denied | Missing RBAC role | Assign correct Azure role |

---

## Summary

Azure Authentication securely connects GitHub Actions to Azure using a Service Principal or OIDC.

---

# Deploy to Azure

## Overview

After authentication, GitHub Actions can deploy applications to various Azure services.

Deployment methods depend on the target resource.

---

## Why It Is Used

Deploying to Azure enables:

- Continuous Deployment
- Automated releases
- Infrastructure automation
- Scalable cloud hosting

---

## Architecture / Working

```mermaid
flowchart LR

    A[Workflow]
    B[Azure Login]
    C[Deployment Action]
    D[Azure Resource]

    A --> B
    B --> C
    C --> D
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| Workflow | Executes deployment |
| Azure Login | Authentication |
| Azure Resource | Deployment target |

---

## Types (if applicable)

Deployment targets

- App Service
- AKS
- Functions
- Virtual Machines

---

## Lifecycle / Workflow (if applicable)

```mermaid
flowchart LR

    A[Build]
    B[Authenticate]
    C[Deploy]
    D[Verify]

    A --> B
    B --> C
    C --> D
```

---

## Configuration / Syntax (if applicable)

```yaml
- uses: azure/login@v2
```

---

## Important Commands (if applicable)

```bash
az webapp deploy
az aks get-credentials
```

---

## Important Files (if applicable)

Deployment workflow

---

## Real-World Use Cases

- Web applications
- APIs
- Microservices

---

## Advantages

- Automated releases
- Faster deployments
- Cloud-native integration

---

## Limitations

- Azure permissions required

---

## Common Interview Questions (Concept Only)

- How does GitHub Actions deploy to Azure?
- Which Azure services are commonly used?

---

## Common Mistakes

- Wrong subscription
- Missing authentication

---

## Troubleshooting

| Problem | Cause | Solution |
|----------|--------|----------|
| Deployment failed | Authentication issue | Verify Azure Login |

---

## Summary

GitHub Actions automates deployments across Azure services using deployment actions and Azure CLI.

---

# Deploy to Azure App Service

## Overview

Azure App Service is a Platform as a Service (PaaS) offering for hosting web applications, REST APIs, and backend services.

GitHub Actions can automatically deploy applications to App Service after each successful build.

---

## Why It Is Used

Azure App Service provides:

- Managed hosting
- Automatic scaling
- HTTPS support
- Easy deployments
- CI/CD integration

---

## Architecture / Working

```mermaid
flowchart LR

    A[Workflow]
    B[Azure Login]
    C[Azure WebApp Deploy]
    D[Azure App Service]

    A --> B
    B --> C
    C --> D
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| App Service | Hosts application |
| Deployment Action | Publishes application |
| Azure Login | Authentication |

---

## Types (if applicable)

Hosting options

- Windows
- Linux
- Containers

---

## Lifecycle / Workflow (if applicable)

```mermaid
flowchart LR

    A[Build]
    B[Package]
    C[Deploy]
    D[Application Running]

    A --> B
    B --> C
    C --> D
```

---

## Configuration / Syntax (if applicable)

```yaml
- uses: azure/webapps-deploy@v3
  with:
    app-name: myapp
    package: .
```

---

## Important Commands (if applicable)

```bash
az webapp deploy
```

---

## Important Files (if applicable)

Workflow YAML

---

## Real-World Use Cases

- ASP.NET applications
- Node.js APIs
- Java applications
- Python web applications

---

## Advantages

- Easy deployment
- Fully managed hosting
- Supports multiple languages

---

## Limitations

- Limited control over the underlying infrastructure
- Pricing depends on selected App Service plan

---

## Common Interview Questions (Concept Only)

- What is Azure App Service?
- Which action deploys to App Service?
- Why use App Service instead of VMs?

---

## Common Mistakes

- Wrong application name
- Deploying to the wrong slot
- Missing publish profile or authentication

---

## Troubleshooting

| Problem | Cause | Solution |
|----------|--------|----------|
| Deployment failed | Wrong app name | Verify App Service name |
| Unauthorized | Authentication failure | Verify Azure credentials |

---

## Summary

Azure App Service provides an easy-to-manage platform for deploying web applications using GitHub Actions.

---

# Deploy to Azure Kubernetes Service (AKS)

## Overview

Azure Kubernetes Service (AKS) is Microsoft's managed Kubernetes service.

GitHub Actions can automatically deploy Docker containers to AKS after building and pushing container images.

> **Interview Tip**
>
> The standard AKS deployment flow is:
>
> **Build Image → Push to Azure Container Registry (ACR) → Authenticate → Configure kubectl → Deploy to AKS**

---

## Why It Is Used

Deploying to AKS provides:

- Container orchestration
- High availability
- Auto scaling
- Rolling updates
- Self-healing applications

---

## Architecture / Working

```mermaid
flowchart LR

    A[Build Docker Image]
    B[Push to Azure Container Registry]
    C[Azure Login]
    D[AKS Cluster]
    E[Kubernetes Deployment]

    A --> B
    B --> C
    C --> D
    D --> E
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| AKS Cluster | Runs containers |
| Azure Container Registry | Stores Docker images |
| kubectl | Deploys Kubernetes resources |
| Deployment YAML | Kubernetes deployment |

---

## Types (if applicable)

Common Kubernetes resources

- Deployment
- Service
- Ingress
- ConfigMap
- Secret

---

## Lifecycle / Workflow (if applicable)

```mermaid
flowchart LR

    A[Build Image]
    B[Push Image]
    C[Authenticate]
    D[Deploy YAML]
    E[Pods Running]

    A --> B
    B --> C
    C --> D
    D --> E
```

---

## Configuration / Syntax (if applicable)

Get cluster credentials

```yaml
- run: az aks get-credentials --resource-group myRG --name myAKS
```

Deploy application

```yaml
- run: kubectl apply -f deployment.yaml
```

---

## Important Commands (if applicable)

```bash
az aks get-credentials

kubectl get nodes

kubectl get pods

kubectl apply -f deployment.yaml

kubectl rollout status deployment/myapp
```

---

## Important Files (if applicable)

```
deployment.yaml

service.yaml

ingress.yaml

Dockerfile

.github/workflows/deploy.yml
```

---

## Real-World Use Cases

- Microservices deployments
- Enterprise Kubernetes platforms
- Containerized APIs
- Scalable web applications

---

## Advantages

- Managed Kubernetes
- High availability
- Auto scaling
- Rolling updates
- Native Azure integration

---

## Limitations

- Kubernetes has a steeper learning curve than App Service.
- Cluster management adds operational complexity.
- Proper RBAC and networking configuration are required.

---

## Common Interview Questions (Concept Only)

- What is Azure Kubernetes Service?
- How does GitHub Actions deploy to AKS?
- Why use Azure Container Registry with AKS?
- What command connects to an AKS cluster?
- Which Kubernetes resources are commonly deployed?

---

## Common Mistakes

- Forgetting Azure authentication
- Not retrieving AKS credentials
- Incorrect Kubernetes manifests
- Wrong container image tag
- Missing Azure Container Registry permissions

---

## Troubleshooting

| Problem | Cause | Solution |
|----------|--------|----------|
| kubectl cannot connect | Cluster credentials missing | Run `az aks get-credentials` |
| ImagePullBackOff | Image not available or registry access issue | Verify image tag and ACR permissions |
| Deployment failed | YAML errors | Validate Kubernetes manifests |
| Pods not starting | Container failure | Check pod logs with `kubectl logs` |
| Unauthorized | Missing RBAC permissions | Assign correct Azure role |

---

## Summary

GitHub Actions provides seamless integration with Azure, enabling automated deployments to Azure App Service and Azure Kubernetes Service (AKS).

> **Interview Tip**
>
> Remember these key deployment flows:
>
> **Azure App Service**
>
> `Checkout → Build → Azure Login → Deploy to App Service`
>
> **Azure Kubernetes Service (AKS)**
>
> `Checkout → Build Docker Image → Push to ACR → Azure Login → Get AKS Credentials → kubectl Apply → Verify Deployment`
>
> Also remember:
>
> - **Azure Login Action:** `azure/login`
> - **App Service Deployment Action:** `azure/webapps-deploy`
> - **AKS Deployment Tool:** `kubectl`
> - **Secure Credential Storage:** GitHub Secrets or OpenID Connect (OIDC)
