# Networking

## Overview

Kubernetes Networking provides communication between Pods, Services, and external clients while abstracting the underlying network infrastructure.

Kubernetes follows a **flat networking model**, where every Pod receives its own IP address and can communicate directly with other Pods without Network Address Translation (NAT).

Kubernetes networking consists of four major components:

- Pod Networking
- Service Networking
- DNS
- Network Policies

> **Interview Tip**
>
> Kubernetes itself does **not implement networking**. It relies on a **Container Network Interface (CNI)** plugin such as Calico, Flannel, Cilium, or Azure CNI.

---

## Why It Is Used

Networking enables:

- Pod-to-Pod communication
- Service discovery
- Load balancing
- External application access
- Secure communication
- Network isolation
- Microservices communication

---

## Architecture / Working

```mermaid
flowchart TB

External User

↓

Service

↓

Pod A

Pod B

Pod C

↓

Node

↓

Cluster Network
```

Networking Flow

```mermaid
flowchart LR

Client

↓

Service

↓

Kube Proxy

↓

Pod

↓

Application
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| Pod Network | Communication between Pods |
| Service | Stable network endpoint |
| DNS | Service discovery |
| kube-proxy | Service routing |
| CNI Plugin | Network implementation |
| Network Policy | Traffic control |

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

Assign ClusterIP

↓

DNS Entry Created

↓

Traffic Routed
```

---

## Configuration / Syntax (if applicable)

Example Service

```yaml
kind: Service

spec:
  selector:
    app: nginx
```

Example Network Policy

```yaml
kind: NetworkPolicy
```

---

## Important Commands (if applicable)

View Pods

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

Describe Service

```bash
kubectl describe svc nginx
```

Check DNS

```bash
kubectl exec -it <pod-name> -- nslookup kubernetes.default
```

View Network Policies

```bash
kubectl get networkpolicy
```

---

## Important Files (if applicable)

| File | Purpose |
|------|----------|
| service.yaml | Service definition |
| networkpolicy.yaml | Network rules |
| deployment.yaml | Pod networking |

---

## Real-World Use Cases

- Microservices
- Internal APIs
- Database communication
- Load balancing
- Secure application communication
- Multi-tier applications

---

## Advantages

- Flat networking model
- Automatic service discovery
- Built-in load balancing
- Flexible routing
- Supports network isolation

---

## Limitations

- Requires CNI plugin
- Network Policies require supported CNI
- Networking complexity increases in large clusters

---

## Common Interview Questions (Concept Only)

- How does Kubernetes networking work?
- Does every Pod receive an IP address?
- What provides networking in Kubernetes?
- What is kube-proxy?
- What is Service Discovery?
- How do Pods communicate?
- What is a Network Policy?
- Which component provides DNS?

---

## Common Mistakes

- Assuming Pods keep the same IP forever
- Forgetting that Services provide stable endpoints
- Assuming Network Policies work without CNI support
- Using Pod IPs instead of Services

---

## Troubleshooting

| Problem | Cause | Solution |
|----------|--------|----------|
| Pod cannot communicate | Network issue | Check CNI |
| Service unreachable | Selector mismatch | Verify labels |
| DNS failure | CoreDNS issue | Check DNS Pods |
| Network Policy blocks traffic | Incorrect rules | Verify policies |
| External access fails | Wrong Service type | Verify Service configuration |

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

Kubernetes Networking enables communication between Pods, Services, and external clients using a flat networking model. It relies on CNI plugins for implementation and provides built-in service discovery, load balancing, and network security through Services, DNS, and Network Policies.

---

# Pod Networking

## Overview

Pod Networking defines how Pods communicate inside a Kubernetes cluster.

Each Pod receives:

- A unique IP address
- Direct connectivity to every other Pod

Unlike Docker bridge networking, Kubernetes Pods communicate without NAT.

> **Interview Tip**
>
> Pod IPs are **ephemeral** and change whenever Pods are recreated.

---

## Why It Is Used

Pod Networking enables:

- Pod-to-Pod communication
- Container communication
- Microservices architecture
- Cluster-wide networking

---

## Architecture / Working

```mermaid
flowchart LR

Pod A

↔

Pod B

↔

Pod C
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| Pod IP | Unique Pod address |
| CNI Plugin | Network implementation |
| Node | Hosts Pods |

---

## Types (if applicable)

Common CNI Plugins

- Calico
- Flannel
- Cilium
- Azure CNI
- AWS VPC CNI

---

## Lifecycle / Workflow

Create Pod

↓

Assign IP

↓

Communicate

↓

Delete Pod

↓

IP Released

---

## Configuration / Syntax (if applicable)

No additional configuration required for basic Pod networking.

---

## Important Commands (if applicable)

```bash
kubectl get pods -o wide

kubectl exec -it <pod-name> -- ip addr
```

---

## Important Files (if applicable)

deployment.yaml

---

## Real-World Use Cases

- Backend communication
- Database access
- Microservices

---

## Advantages

- Simple networking
- Flat network
- No NAT between Pods

---

## Limitations

- Pod IP changes after recreation
- Cannot rely on Pod IP permanently

---

## Common Interview Questions (Concept Only)

- Does every Pod have an IP?
- Can Pods communicate directly?
- Why shouldn't applications use Pod IPs?

---

## Common Mistakes

- Using Pod IPs instead of Services

---

## Troubleshooting

```bash
kubectl get pods -o wide
```

---

## Summary

Pod Networking provides direct communication between Pods using unique Pod IP addresses assigned by the CNI plugin.

---

# Service Networking

## Overview

Services provide a stable network endpoint for Pods.

Since Pods are frequently recreated, Services ensure applications always have a consistent IP address and DNS name.

Services perform load balancing across matching Pods.

> **Interview Tip**
>
> Applications should communicate through **Services**, not directly to Pod IPs.

---

## Why It Is Used

Service Networking provides:

- Stable IP
- Load balancing
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
| Selector | Finds Pods |
| Endpoints | Matching Pods |
| kube-proxy | Traffic routing |

---

## Types (if applicable)

- ClusterIP
- NodePort
- LoadBalancer
- ExternalName

---

## Lifecycle / Workflow

Create Service

↓

Find Pods

↓

Create Endpoints

↓

Route Traffic

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

kubectl describe svc nginx
```

---

## Important Files (if applicable)

service.yaml

---

## Real-World Use Cases

- API services
- Backend communication
- Web applications

---

## Advantages

- Stable IP
- Load balancing
- Easy discovery

---

## Limitations

- Selector must match labels
- Service IP is cluster-internal unless exposed

---

## Common Interview Questions (Concept Only)

- Why use Services?
- How does Service routing work?

---

## Common Mistakes

- Wrong selectors
- Direct Pod communication

---

## Troubleshooting

```bash
kubectl get endpoints

kubectl describe svc nginx
```

---

## Summary

Services provide stable networking and load balancing for dynamic Pods.

---

# DNS

## Overview

Kubernetes DNS automatically assigns DNS names to Services and enables Pods to discover Services without knowing IP addresses.

DNS is typically provided by **CoreDNS**.

> **Interview Tip**
>
> Services automatically receive DNS names, but Pods generally should not be relied upon by name unless using specific features like StatefulSets.

---

## Why It Is Used

DNS enables:

- Service discovery
- Stable application communication
- Simplified configuration

---

## Architecture / Working

```mermaid
flowchart LR

Pod

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
| Service DNS | Stable hostname |
| Cluster Domain | cluster.local |

---

## Types (if applicable)

DNS Records

- Service DNS
- Pod DNS (limited use)

---

## Lifecycle / Workflow

Service Created

↓

DNS Record Generated

↓

Application Resolves Name

---

## Configuration / Syntax (if applicable)

Service Name

```
mysql.default.svc.cluster.local
```

Short Name

```
mysql
```

---

## Important Commands (if applicable)

Check DNS

```bash
kubectl exec -it <pod-name> -- nslookup kubernetes.default
```

View CoreDNS

```bash
kubectl get pods -n kube-system
```

---

## Important Files (if applicable)

coredns ConfigMap

---

## Real-World Use Cases

- Database access
- Internal APIs
- Service discovery

---

## Advantages

- Automatic discovery
- Stable names
- No hardcoded IPs

---

## Limitations

- Depends on CoreDNS availability
- DNS issues affect application communication

---

## Common Interview Questions (Concept Only)

- What provides DNS?
- What is CoreDNS?
- How does Service Discovery work?

---

## Common Mistakes

- Hardcoding Service IPs
- Ignoring DNS failures

---

## Troubleshooting

```bash
kubectl exec -it <pod-name> -- nslookup kubernetes.default

kubectl get pods -n kube-system
```

---

## Summary

CoreDNS provides automatic DNS-based Service discovery, allowing applications to communicate using stable names instead of changing IP addresses.

---

# Network Policies

## Overview

Network Policies define how Pods are allowed to communicate with other Pods and external networks.

By default, Kubernetes allows unrestricted Pod-to-Pod communication.

Network Policies implement **micro-segmentation** by allowing or denying traffic based on labels and rules.

> **Interview Tip**
>
> Network Policies only work if the cluster's CNI plugin supports them (for example, Calico or Cilium).

---

## Why It Is Used

Network Policies are used to:

- Restrict Pod communication
- Improve security
- Isolate applications
- Implement Zero Trust networking
- Protect sensitive workloads

---

## Architecture / Working

```mermaid
flowchart LR

Pod A

-- Allowed -->

Pod B

Pod C

-. Blocked .->

Pod B
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| Pod Selector | Selects Pods |
| Ingress Rules | Incoming traffic |
| Egress Rules | Outgoing traffic |
| Namespace Selector | Selects Namespaces |
| IP Block | External IP filtering |

---

## Types (if applicable)

| Type | Purpose |
|------|----------|
| Ingress | Incoming traffic |
| Egress | Outgoing traffic |
| Both | Bidirectional control |

---

## Lifecycle / Workflow

Create Policy

↓

Select Pods

↓

Apply Rules

↓

Traffic Allowed or Denied

---

## Configuration / Syntax (if applicable)

```yaml
kind: NetworkPolicy
```

---

## Important Commands (if applicable)

List Policies

```bash
kubectl get networkpolicy
```

Describe Policy

```bash
kubectl describe networkpolicy
```

---

## Important Files (if applicable)

| File | Purpose |
|------|----------|
| networkpolicy.yaml | Network policy definition |

---

## Real-World Use Cases

- Database protection
- Namespace isolation
- PCI compliance
- Financial applications
- Zero Trust networking

---

## Advantages

- Improves security
- Limits attack surface
- Supports application isolation
- Fine-grained traffic control

---

## Limitations

- Requires compatible CNI
- Incorrect policies can block application traffic
- Does not encrypt network traffic

---

## Common Interview Questions (Concept Only)

- What is a Network Policy?
- Why are Network Policies needed?
- What is the difference between Ingress and Egress rules?
- Do Network Policies work without a compatible CNI plugin?
- What happens if no Network Policy exists?

---

## Common Mistakes

- Assuming Network Policies work with every CNI
- Blocking required application traffic
- Forgetting DNS access in restrictive policies
- Using incorrect Pod selectors

---

## Troubleshooting

| Problem | Cause | Solution |
|----------|--------|----------|
| Pod cannot communicate | Policy blocks traffic | Review ingress/egress rules |
| Policy has no effect | Unsupported CNI | Verify CNI capabilities |
| DNS resolution fails | DNS traffic blocked | Allow CoreDNS traffic |
| Service unreachable | Incorrect selectors | Verify Pod labels and policy selectors |

Useful Commands

```bash
kubectl get networkpolicy

kubectl describe networkpolicy

kubectl get pods --show-labels

kubectl exec -it <pod-name> -- ping <service-name>
```

---

## Summary

Network Policies provide security by controlling Pod-to-Pod and Pod-to-external communication. They define ingress and egress rules based on Pod labels, namespaces, and IP addresses, enabling secure, production-ready Kubernetes networking when supported by the cluster's CNI plugin.
