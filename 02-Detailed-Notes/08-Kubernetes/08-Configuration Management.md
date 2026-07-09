# Configuration Management

## Overview

Configuration Management in Kubernetes is the process of storing, managing, and providing application configuration separately from the application container image.

Instead of hardcoding configuration values (such as database URLs, API endpoints, or passwords) inside the application or Docker image, Kubernetes provides **ConfigMaps** and **Secrets** to manage configuration dynamically.

Configuration Management enables the same container image to be deployed across Development, Testing, and Production environments with different configurations.

> **Interview Tip**
>
> - **ConfigMap** → Non-sensitive configuration
> - **Secret** → Sensitive configuration (passwords, API keys, certificates)
> - Environment Variables and Volumes are the two primary ways to consume ConfigMaps and Secrets.

---

## Why It Is Used

Configuration Management is used to:

- Separate configuration from application code
- Avoid rebuilding container images for configuration changes
- Manage environment-specific settings
- Secure sensitive information
- Improve portability
- Simplify deployments
- Support DevOps and CI/CD practices

---

## Architecture / Working

```mermaid
flowchart LR

Developer

↓

ConfigMap / Secret

↓

Kubernetes API Server

↓

Pod

↓

Container

↓

Application
```

Configuration Delivery

```mermaid
flowchart LR

ConfigMap

--> Environment Variables

ConfigMap

--> Mounted Files

Secret

--> Environment Variables

Secret

--> Mounted Files
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| ConfigMap | Stores non-sensitive configuration |
| Secret | Stores sensitive information |
| Environment Variables | Pass configuration to containers |
| Volume Mount | Mount configuration files |
| Kubernetes API Server | Stores configuration objects |

---

## Types (if applicable)

### Configuration Sources

- ConfigMap
- Secret

### Configuration Delivery

- Environment Variables
- Volume Mounts

---

## Lifecycle /Workflow

```mermaid
flowchart LR

Create ConfigMap/Secret

↓

Store in API Server

↓

Deploy Pod

↓

Inject Configuration

↓

Application Uses Configuration
```

---

## Configuration / Syntax (if applicable)

ConfigMap

```yaml
apiVersion: v1
kind: ConfigMap

metadata:
  name: app-config

data:
  APP_ENV: production
  DB_HOST: mysql
```

Secret

```yaml
apiVersion: v1
kind: Secret

metadata:
  name: db-secret

type: Opaque

stringData:
  username: admin
  password: password123
```

Using ConfigMap

```yaml
env:
- name: APP_ENV
  valueFrom:
    configMapKeyRef:
      name: app-config
      key: APP_ENV
```

Using Secret

```yaml
env:
- name: DB_PASSWORD
  valueFrom:
    secretKeyRef:
      name: db-secret
      key: password
```

---

## Important Commands (if applicable)

Create ConfigMap

```bash
kubectl create configmap app-config \
--from-literal=APP_ENV=production
```

Create Secret

```bash
kubectl create secret generic db-secret \
--from-literal=password=password123
```

View ConfigMaps

```bash
kubectl get configmaps
```

View Secrets

```bash
kubectl get secrets
```

Describe ConfigMap

```bash
kubectl describe configmap app-config
```

Describe Secret

```bash
kubectl describe secret db-secret
```

View YAML

```bash
kubectl get configmap app-config -o yaml
```

Delete ConfigMap

```bash
kubectl delete configmap app-config
```

Delete Secret

```bash
kubectl delete secret db-secret
```

---

## Important Files (if applicable)

| File | Purpose |
|------|----------|
| configmap.yaml | ConfigMap definition |
| secret.yaml | Secret definition |
| deployment.yaml | Uses ConfigMaps and Secrets |
| pod.yaml | Inject configuration |

---

## Real-World Use Cases

- Database connection strings
- Application configuration
- API endpoints
- Feature flags
- Credentials
- TLS certificates
- Cloud authentication
- Environment-specific settings

---

## Advantages

- Separates configuration from code
- Reusable across environments
- Supports dynamic updates
- Improves security
- Simplifies deployments
- Enables immutable container images

---

## Limitations

- ConfigMaps are not encrypted
- Secrets are Base64 encoded by default (not encryption)
- Secret size is limited
- Pods may need restarting after configuration changes
- Improper Secret handling can expose sensitive data

---

## Common Interview Questions (Concept Only)

- What is Configuration Management?
- Why should configuration be separated from application code?
- What is the difference between ConfigMap and Secret?
- How are ConfigMaps consumed by Pods?
- How are Secrets injected into containers?
- Can ConfigMaps be updated without rebuilding images?
- Are Kubernetes Secrets encrypted?
- How can configuration be mounted as files?

---

## Common Mistakes

- Storing passwords inside ConfigMaps
- Hardcoding configuration in Docker images
- Confusing Base64 encoding with encryption
- Forgetting to restart Pods after configuration changes
- Storing sensitive information in Git repositories

---

## Troubleshooting

| Problem | Cause | Solution |
|----------|--------|----------|
| Pod can't read ConfigMap | Wrong name | Verify ConfigMap name |
| Secret not available | Incorrect key | Check Secret keys |
| Environment variable empty | Wrong reference | Verify `valueFrom` |
| Pod startup failure | Missing ConfigMap | Create missing resource |
| Secret exposed | Stored in Git | Use secure secret management |

Useful Commands

```bash
kubectl get configmaps

kubectl get secrets

kubectl describe configmap app-config

kubectl describe secret db-secret

kubectl exec -it <pod-name> -- env
```

---

## Summary

Configuration Management enables Kubernetes applications to separate configuration from application code. ConfigMaps store non-sensitive configuration, while Secrets securely store sensitive information. These configurations can be injected into containers through Environment Variables or mounted as files, making applications portable, secure, and easier to manage across different environments.

---

# ConfigMaps

## Overview

A **ConfigMap** is a Kubernetes object used to store **non-sensitive configuration data** as key-value pairs.

Applications retrieve configuration from ConfigMaps instead of embedding it inside the container image.

> **Interview Tip**
>
> ConfigMaps should never contain passwords or API keys.

---

## Why It Is Used

ConfigMaps are used to store:

- Application settings
- Database hostnames
- URLs
- Port numbers
- Feature flags
- Configuration files

---

## Architecture / Working

```mermaid
flowchart LR

ConfigMap

↓

Pod

↓

Container

↓

Application
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| Name | ConfigMap identifier |
| Data | Key-value pairs |
| Keys | Configuration names |
| Values | Configuration values |

---

## Types (if applicable)

ConfigMaps can be consumed as:

- Environment Variables
- Mounted Volumes
- Command-line arguments

---

## Lifecycle / Workflow

```mermaid
flowchart LR

Create ConfigMap

↓

Deploy Pod

↓

Inject Configuration

↓

Application Reads Values
```

---

## Configuration / Syntax (if applicable)

Example

```yaml
apiVersion: v1
kind: ConfigMap

metadata:
  name: app-config

data:
  APP_ENV: production
  LOG_LEVEL: info
```

---

## Important Commands (if applicable)

Create

```bash
kubectl create configmap app-config \
--from-literal=APP_ENV=production
```

View

```bash
kubectl get configmaps
```

Describe

```bash
kubectl describe configmap app-config
```

Delete

```bash
kubectl delete configmap app-config
```

---

## Important Files (if applicable)

| File | Purpose |
|------|----------|
| configmap.yaml | ConfigMap definition |

---

## Real-World Use Cases

- Application configuration
- Logging configuration
- Database hostname
- Feature flags
- Environment-specific values

---

## Advantages

- Easy configuration management
- Environment independent
- Reusable
- No image rebuild required

---

## Limitations

- Not secure for sensitive data
- Limited object size
- Configuration changes may require Pod restart

---

## Common Interview Questions (Concept Only)

- What is a ConfigMap?
- What data should be stored in ConfigMaps?
- Can ConfigMaps store passwords?
- How are ConfigMaps consumed?

---

## Common Mistakes

- Storing secrets in ConfigMaps
- Hardcoding configuration in Docker images
- Incorrect ConfigMap references

---

## Troubleshooting

```bash
kubectl describe configmap app-config

kubectl exec -it <pod-name> -- env
```

---

## Summary

ConfigMaps store non-sensitive application configuration separately from container images, allowing the same image to be reused across multiple environments.

---

# Secrets

## Overview

A **Secret** is a Kubernetes object used to securely store sensitive information such as passwords, API keys, tokens, and certificates.

Secrets help prevent sensitive data from being embedded in application code or container images.

> **Interview Tip**
>
> Kubernetes Secrets are **Base64 encoded**, **not encrypted by default**. Encryption at rest must be enabled separately.

---

## Why It Is Used

Secrets are used to store:

- Passwords
- Database credentials
- API keys
- OAuth tokens
- SSH keys
- TLS certificates

---

## Architecture / Working

```mermaid
flowchart LR

Secret

↓

Pod

↓

Container

↓

Application
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| Secret | Stores sensitive data |
| Key | Secret identifier |
| Value | Base64-encoded value |

---

## Types (if applicable)

| Secret Type | Purpose |
|-------------|----------|
| Opaque | Generic secrets |
| kubernetes.io/tls | TLS certificates |
| kubernetes.io/dockerconfigjson | Docker registry credentials |
| kubernetes.io/basic-auth | Username/password |

---

## Lifecycle / Workflow

```mermaid
flowchart LR

Create Secret

↓

Store in API Server

↓

Inject into Pod

↓

Application Uses Secret
```

---

## Configuration / Syntax (if applicable)

```yaml
apiVersion: v1
kind: Secret

metadata:
  name: db-secret

type: Opaque

stringData:
  username: admin
  password: password123
```

---

## Important Commands (if applicable)

Create

```bash
kubectl create secret generic db-secret \
--from-literal=password=password123
```

View

```bash
kubectl get secrets
```

Describe

```bash
kubectl describe secret db-secret
```

Delete

```bash
kubectl delete secret db-secret
```

---

## Important Files (if applicable)

| File | Purpose |
|------|----------|
| secret.yaml | Secret definition |

---

## Real-World Use Cases

- Database passwords
- Cloud credentials
- SSH keys
- TLS certificates
- Registry credentials

---

## Advantages

- Keeps credentials separate from code
- Supports secure application deployment
- Can be mounted or injected
- RBAC can restrict access

---

## Limitations

- Base64 encoding is not encryption
- Limited size
- Requires proper RBAC configuration
- Sensitive data can still be exposed if mishandled

---

## Common Interview Questions (Concept Only)

- What is a Secret?
- Difference between ConfigMap and Secret?
- Are Secrets encrypted?
- How are Secrets consumed by Pods?

---

## Common Mistakes

- Assuming Base64 encoding is encryption
- Committing Secrets to Git
- Using ConfigMaps instead of Secrets for credentials

---

## Troubleshooting

```bash
kubectl get secrets

kubectl describe secret db-secret

kubectl exec -it <pod-name> -- env
```

---

## Summary

Secrets securely store sensitive information required by applications. They improve security by separating credentials from application code and container images.

---

# Environment Variables

## Overview

Environment Variables are one of the most common ways to provide configuration to containers running inside Pods.

Values can come from:

- Static values
- ConfigMaps
- Secrets

Applications read these values at runtime without modifying the application image.

---

## Why It Is Used

Environment Variables are used to:

- Configure applications
- Inject credentials
- Provide runtime configuration
- Support multiple environments
- Avoid hardcoded values

---

## Architecture / Working

```mermaid
flowchart LR

ConfigMap / Secret

↓

Environment Variables

↓

Container

↓

Application
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| env | Define environment variables |
| value | Static value |
| valueFrom | Read from ConfigMap or Secret |

---

## Types (if applicable)

| Type | Description |
|------|-------------|
| Static | Hardcoded value |
| ConfigMap | Non-sensitive configuration |
| Secret | Sensitive configuration |

---

## Lifecycle / Workflow

```mermaid
flowchart LR

Create ConfigMap/Secret

↓

Reference in Pod

↓

Pod Starts

↓

Environment Variables Available
```

---

## Configuration / Syntax (if applicable)

Static Value

```yaml
env:
- name: APP_ENV
  value: production
```

ConfigMap

```yaml
env:
- name: APP_ENV
  valueFrom:
    configMapKeyRef:
      name: app-config
      key: APP_ENV
```

Secret

```yaml
env:
- name: PASSWORD
  valueFrom:
    secretKeyRef:
      name: db-secret
      key: password
```

---

## Important Commands (if applicable)

View Environment Variables

```bash
kubectl exec -it <pod-name> -- env
```

Describe Pod

```bash
kubectl describe pod <pod-name>
```

---

## Important Files (if applicable)

| File | Purpose |
|------|----------|
| deployment.yaml | Environment variables |
| pod.yaml | Runtime configuration |

---

## Real-World Use Cases

- Database connections
- Application mode
- API endpoints
- Logging levels
- Feature flags
- Cloud credentials

---

## Advantages

- Easy configuration
- Environment-specific deployment
- Works with ConfigMaps and Secrets
- No image rebuild required

---

## Limitations

- Values are fixed when the container starts
- Changes typically require Pod restart
- Environment variables may be visible to processes inside the container

---

## Common Interview Questions (Concept Only)

- How do you pass environment variables to a Pod?
- Can ConfigMaps populate environment variables?
- Can Secrets populate environment variables?
- Which is better: Environment Variables or Volume Mounts?

---

## Common Mistakes

- Hardcoding sensitive values
- Incorrect `valueFrom` references
- Forgetting to restart Pods after updates
- Exposing secrets through application logs

---

## Troubleshooting

| Problem | Cause | Solution |
|----------|--------|----------|
| Variable missing | Incorrect reference | Verify `valueFrom` configuration |
| Empty value | Wrong key name | Check ConfigMap or Secret keys |
| Pod startup failure | Missing ConfigMap or Secret | Create or correct the resource |
| Configuration not updated | Existing Pod still running | Restart the Pod or rollout the Deployment |

Useful Commands

```bash
kubectl exec -it <pod-name> -- env

kubectl describe pod <pod-name>

kubectl get configmaps

kubectl get secrets
```

---

## Summary

Environment Variables provide runtime configuration to Kubernetes containers and are commonly populated from ConfigMaps or Secrets. They enable flexible, environment-specific deployments without modifying container images and are one of the most frequently used configuration mechanisms in production Kubernetes environments.
