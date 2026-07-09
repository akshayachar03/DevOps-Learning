# Networking

## Overview

Kubernetes Networking enables communication between Pods, Services, Nodes, and external clients. One of Kubernetes' core principles is that every Pod can communicate with every other Pod without Network Address Translation (NAT).

Unlike traditional networking, Kubernetes abstracts networking complexity and provides built-in Service Discovery, Load Balancing, and Network Security.

Kubernetes networking mainly consists of:

- Pod Networking
- Service Networking
- DNS
- Network Policies

> **Interview Tip**
>
> Kubernetes **defines** the networking model but does **not implement it**.
>
> Networking is implemented through **Container Network Interface (CNI)** plugins like:
>
> - Calico
> - Flannel
> - Cilium
> - Azure CNI
> - AWS VPC CNI

---

## Why It Is Used

Kubernetes Networking provides:

- Pod-to-Pod communication
- Service discovery
- Internal load balancing
- External application access
- High availability
- Secure communication
- Network isolation
- Scalable microservices communication

---

## Architecture / Working

```mermaid
flowchart TB

Client

↓

LoadBalancer

↓

Service

↓

kube-proxy

↓

Pod A

Pod B

Pod C

↓

Node Network

↓

Cluster Network
```

Internal Networking Flow

```mermaid
flowchart LR

Pod

↓

DNS Resolution

↓

Service

↓

Endpoints

↓

Target Pod
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| Pod Network | Communication between Pods |
| Service | Stable network endpoint |
| DNS (CoreDNS) | Service discovery |
| kube-proxy | Routes Service traffic |
| CNI Plugin | Implements networking |
| Network Policy | Controls network traffic |
| Endpoints | Actual Pod IPs behind a Service |

---

## Types (if applicable)

Networking Components

- Pod Networking
- Service Networking
- DNS
- Network Policies

---

## Lifecycle / Workflow

```mermaid
flowchart LR

Create Pod

↓

Assign Pod IP

↓

Create Service

↓

Assign Cluster IP

↓

Create DNS Record

↓

Route Traffic

↓

Apply Network Policies
```

---

## Configuration / Syntax (if applicable)

Example Service

```yaml
apiVersion: v1
kind: Service

metadata:
  name: nginx-service

spec:
  selector:
    app: nginx

  ports:
  - port: 80
    targetPort: 80
```

---

## Important Commands (if applicable)

View Pods with IP

```bash
kubectl get pods -o wide
```

View Services

```bash
kubectl get svc
```

View Endpoints

```bash
kubectl get endpoints
```

View DNS Pods

```bash
kubectl get pods -n kube-system
```

View Network Policies

```bash
kubectl get networkpolicy
```

Describe Service

```bash
kubectl describe svc nginx-service
```

---

## Important Files (if applicable)

| File | Purpose |
|------|----------|
| deployment.yaml | Pod networking |
| service.yaml | Service networking |
| networkpolicy.yaml | Network security |
| coredns ConfigMap | DNS configuration |

---

## Real-World Use Cases

- Microservices communication
- Database connectivity
- Internal APIs
- External application access
- Secure workloads
- Multi-tier applications
- Zero Trust networking

---

## Advantages

- Flat networking model
- Automatic service discovery
- Built-in load balancing
- Platform independent
- Supports network security
- Highly scalable

---

## Limitations

- Requires CNI plugin
- Network Policies require supported CNI
- Networking becomes complex in large clusters
- Pod IPs are temporary

---

## Common Interview Questions (Concept Only)

- Explain Kubernetes networking.
- Why does every Pod receive an IP?
- What is the role of CNI?
- What is kube-proxy?
- How does Service Discovery work?
- How does DNS work in Kubernetes?
- What is a Network Policy?
- Why shouldn't applications use Pod IPs?

---

## Common Mistakes

- Using Pod IPs directly
- Forgetting Services provide stable endpoints
- Assuming Kubernetes implements networking itself
- Ignoring DNS
- Assuming Network Policies work with every CNI

---

## Troubleshooting

| Problem | Cause | Solution |
|----------|--------|----------|
| Pod cannot communicate | CNI issue | Verify CNI |
| Service unreachable | Selector mismatch | Verify labels |
| DNS failure | CoreDNS issue | Check CoreDNS |
| Traffic blocked | Network Policy | Review rules |
| External access fails | Wrong Service type | Verify Service |

Useful Commands

```bash
kubectl get pods -o wide

kubectl get svc

kubectl get endpoints

kubectl get networkpolicy

kubectl exec -it <pod-name> -- nslookup kubernetes.default
```

---

## Summary

Kubernetes Networking provides seamless communication between Pods, Services, and external clients through Pod Networking, Service Networking, DNS, and Network Policies. It relies on CNI plugins to implement networking while Kubernetes manages routing, service discovery, and load balancing.

---

# Pod Networking

## Overview

Pod Networking enables communication between Pods across the Kubernetes cluster.

Every Pod receives:

- A unique IP address
- Direct network connectivity
- No NAT between Pods

Pods can communicate regardless of which Node they run on.

> **Interview Tip**
>
> Every Pod gets **one IP**, shared by all containers inside that Pod.

---

## Why It Is Used

Pod Networking enables:

- Microservices communication
- Backend communication
- Cross-node networking
- Container communication

---

## Architecture / Working

```mermaid
flowchart LR

Node1

Pod A

↔

Pod B

↔

Pod C

Node2
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| Pod IP | Unique Pod address |
| CNI Plugin | Assigns IP and networking |
| Node Network | Connects Pods across Nodes |

---

## Types (if applicable)

Common CNI Plugins

| Plugin | Common Usage |
|----------|--------------|
| Calico | Security + Networking |
| Flannel | Simple networking |
| Cilium | eBPF networking |
| Azure CNI | AKS |
| AWS VPC CNI | EKS |

---

## Lifecycle / Workflow

```mermaid
flowchart LR

Pod Created

↓

CNI Assigns IP

↓

Pod Starts

↓

Pod Communicates

↓

Pod Deleted

↓

IP Released
```

---

## Configuration / Syntax (if applicable)

No YAML configuration required.

Networking is automatically configured by the CNI plugin.

---

## Important Commands (if applicable)

View Pod IPs

```bash
kubectl get pods -o wide
```

Check Pod Network

```bash
kubectl exec -it <pod-name> -- ip addr
```

Ping another Pod

```bash
kubectl exec -it <pod-name> -- ping <pod-ip>
```

---

## Important Files (if applicable)

| File | Purpose |
|------|----------|
| deployment.yaml | Pod definition |

---

## Real-World Use Cases

- Backend API communication
- Database connectivity
- Microservices
- Internal communication

---

## Advantages

- Direct Pod communication
- Flat networking
- No NAT
- Simple routing

---

## Limitations

- Pod IP changes after recreation
- Applications should not depend on Pod IPs

---

## Common Interview Questions (Concept Only)

- Does every Pod get an IP?
- Can Pods communicate across Nodes?
- Why are Pod IPs temporary?
- Who assigns Pod IPs?

---

## Common Mistakes

- Using Pod IPs permanently
- Assuming each container has a separate IP

---

## Troubleshooting

```bash
kubectl get pods -o wide

kubectl exec -it <pod-name> -- ip addr
```

---

## Summary

Pod Networking assigns every Pod a unique IP address, enabling direct communication across the Kubernetes cluster without NAT.

---

# Service Networking

## Overview

Pods are temporary and frequently recreated. Their IP addresses change over time.

A **Service** provides:

- Stable IP address
- Stable DNS name
- Load balancing
- Service discovery

Applications should communicate through Services instead of Pod IPs.

---

## Why It Is Used

Service Networking provides:

- Stable endpoints
- Internal load balancing
- Service discovery
- High availability

---

## Architecture / Working

```mermaid
flowchart LR

Client

↓

Service

↓

Pod1

Pod2

Pod3
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| Service | Stable endpoint |
| Selector | Select Pods |
| Endpoints | Matching Pods |
| kube-proxy | Routes traffic |

---

## Types (if applicable)

- ClusterIP
- NodePort
- LoadBalancer
- ExternalName

---

## Lifecycle / Workflow

```mermaid
flowchart LR

Create Service

↓

Find Matching Pods

↓

Create Endpoints

↓

Load Balance Requests
```

---

## Configuration / Syntax (if applicable)

```yaml
selector:
  app: nginx
```

---

## Important Commands (if applicable)

```bash
kubectl get svc

kubectl get endpoints

kubectl describe svc nginx-service
```

---

## Important Files (if applicable)

| File | Purpose |
|------|----------|
| service.yaml | Service definition |

---

## Real-World Use Cases

- Backend APIs
- Database Services
- Internal communication
- Web applications

---

## Advantages

- Stable networking
- Automatic load balancing
- Service discovery

---

## Limitations

- Incorrect selectors break routing
- Pod IP changes still occur

---

## Common Interview Questions (Concept Only)

- Why use Services?
- How does kube-proxy work?
- What are Endpoints?

---

## Common Mistakes

- Wrong selectors
- Accessing Pods directly

---

## Troubleshooting

```bash
kubectl get endpoints

kubectl describe svc nginx-service
```

---

## Summary

Service Networking provides stable networking for dynamic Pods through Services, Endpoints, and kube-proxy.

---

# DNS

## Overview

Kubernetes automatically creates DNS records for Services using **CoreDNS**.

Applications communicate using Service names rather than IP addresses.

Example:

```
mysql.default.svc.cluster.local
```

Short name:

```
mysql
```

---

## Why It Is Used

DNS provides:

- Automatic Service discovery
- Stable communication
- Simplified application configuration

---

## Architecture / Working

```mermaid
flowchart LR

Application

↓

CoreDNS

↓

Service

↓

Pod
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| CoreDNS | DNS server |
| Service Name | Hostname |
| Cluster Domain | cluster.local |

---

## Types (if applicable)

DNS Records

- Service DNS
- Headless Service DNS
- Pod DNS (limited use)

---

## Lifecycle / Workflow

```mermaid
flowchart LR

Service Created

↓

DNS Record Generated

↓

Application Resolves Name

↓

Traffic Routed
```

---

## Configuration / Syntax (if applicable)

Example

```
nginx.default.svc.cluster.local
```

---

## Important Commands (if applicable)

Test DNS

```bash
kubectl exec -it <pod-name> -- nslookup kubernetes.default
```

View CoreDNS

```bash
kubectl get pods -n kube-system
```

---

## Important Files (if applicable)

| File | Purpose |
|------|----------|
| coredns ConfigMap | DNS configuration |

---

## Real-World Use Cases

- Database connections
- Internal APIs
- Service discovery

---

## Advantages

- Automatic discovery
- No hardcoded IPs
- Stable communication

---

## Limitations

- Depends on CoreDNS
- DNS issues affect applications

---

## Common Interview Questions (Concept Only)

- What is CoreDNS?
- How does Service Discovery work?
- What is cluster.local?

---

## Common Mistakes

- Using Service IP instead of DNS
- Ignoring DNS failures

---

## Troubleshooting

```bash
kubectl exec -it <pod-name> -- nslookup kubernetes.default

kubectl get pods -n kube-system
```

---

## Summary

CoreDNS automatically creates DNS records for Services, enabling applications to communicate using stable hostnames instead of IP addresses.

---

# Network Policies

## Overview

Network Policies define how Pods communicate with each other and with external networks.

By default:

- All Pods can communicate with each other.
- Network Policies restrict this communication.

They provide **Layer 3 and Layer 4** traffic filtering (IP addresses, ports, and protocols).

> **Interview Tip**
>
> Network Policies require a CNI plugin that supports them (such as Calico, Cilium, or Azure CNI powered by Cilium). Without support from the CNI, creating a NetworkPolicy object has no effect.

---

## Why It Is Used

Network Policies help:

- Secure applications
- Isolate workloads
- Protect databases
- Enforce Zero Trust networking
- Meet compliance requirements

---

## Architecture / Working

```mermaid
flowchart LR

Pod A

-- Allow -->

Pod B

Pod C

-. Deny .->

Pod B
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| Pod Selector | Select Pods |
| Ingress | Incoming traffic rules |
| Egress | Outgoing traffic rules |
| Namespace Selector | Select namespaces |
| IP Block | External IP filtering |

---

## Types (if applicable)

| Policy Type | Description |
|-------------|-------------|
| Ingress | Controls incoming traffic |
| Egress | Controls outgoing traffic |
| Both | Controls both directions |

---

## Lifecycle / Workflow

```mermaid
flowchart LR

Create Policy

↓

Select Pods

↓

Apply Rules

↓

Traffic Allowed or Blocked
```

---

## Configuration / Syntax (if applicable)

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
```

---

## Important Commands (if applicable)

```bash
kubectl get networkpolicy

kubectl describe networkpolicy
```

---

## Important Files (if applicable)

| File | Purpose |
|------|----------|
| networkpolicy.yaml | Network security rules |

---

## Real-World Use Cases

- Secure databases
- Namespace isolation
- PCI-DSS compliance
- Financial applications
- Healthcare workloads
- Zero Trust networking

---

## Advantages

- Improves security
- Fine-grained traffic control
- Reduces attack surface
- Supports micro-segmentation

---

## Limitations

- Requires compatible CNI
- Can accidentally block legitimate traffic
- Does not provide encryption

---

## Common Interview Questions (Concept Only)

- What is a Network Policy?
- What is the difference between Ingress and Egress?
- Do Network Policies work without a CNI plugin?
- Are Pods isolated by default?
- How do Network Policies select Pods?

---

## Common Mistakes

- Forgetting DNS traffic
- Incorrect Pod selectors
- Assuming every CNI supports Network Policies
- Blocking application communication unintentionally

---

## Troubleshooting

| Problem | Cause | Solution |
|----------|--------|----------|
| Pod cannot reach another Pod | NetworkPolicy blocks traffic | Review ingress/egress rules |
| Policy has no effect | Unsupported CNI | Verify CNI supports NetworkPolicy |
| DNS resolution fails | DNS traffic blocked | Allow access to CoreDNS |
| Traffic unexpectedly denied | Selector mismatch | Verify labels and namespace selectors |

Useful Commands

```bash
kubectl get networkpolicy

kubectl describe networkpolicy

kubectl get pods --show-labels

kubectl exec -it <pod-name> -- nslookup kubernetes.default
```

---

## Summary

Network Policies secure Kubernetes networking by controlling ingress and egress traffic between Pods, namespaces, and external networks. Combined with a compatible CNI plugin, they enable fine-grained traffic control, workload isolation, and Zero Trust networking for production Kubernetes clusters.
