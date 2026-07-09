# Cluster Architecture Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What are the major components of Kubernetes Cluster Architecture?

**Answer**

A Kubernetes cluster consists of two main parts:

**Control Plane Components**
- API Server
- etcd
- Scheduler
- Controller Manager

**Worker Node Components**
- Kubelet
- Kube Proxy
- Container Runtime
- Pods

**Explanation**

The Control Plane manages the cluster, while Worker Nodes run application workloads. Each component has a dedicated responsibility, ensuring the cluster remains scalable, fault-tolerant, and self-healing.

**Used in Production**

Every Kubernetes cluster, whether on-premises or in cloud platforms like AKS, EKS, and GKE.

**Common Mistake**

Many candidates think Kubelet or Kube Proxy are Control Plane components. They actually run on Worker Nodes.

---

### Question 2

**Question**

What is the Kubernetes API Server, and why is it considered the heart of the cluster?

**Answer**

The API Server is the central management component of Kubernetes.

Its responsibilities include:

- Receiving all Kubernetes requests
- Authenticating users
- Authorizing requests
- Validating resource definitions
- Updating cluster state in etcd
- Communicating with all other Kubernetes components

**Explanation**

Every operation performed using `kubectl`, dashboards, CI/CD pipelines, or REST APIs goes through the API Server. No component communicates directly with etcd without the API Server.

**Used in Production**

Every deployment, scaling operation, configuration change, and monitoring request.

**Common Mistake**

Some candidates believe `kubectl` communicates directly with Worker Nodes. It always communicates through the API Server.

---

### Question 3

**Question**

What is etcd, and what information does it store?

**Answer**

etcd is a distributed key-value database that stores the entire state of the Kubernetes cluster.

It stores:

- Nodes
- Pods
- Services
- Deployments
- Secrets
- ConfigMaps
- Cluster configuration
- Desired state

**Explanation**

The Control Plane relies on etcd as the source of truth. Every cluster change is stored in etcd so Kubernetes can continuously compare the desired state with the actual state.

**Used in Production**

Cluster recovery, scheduling, scaling, and maintaining cluster consistency.

**Common Mistake**

Thinking etcd stores application data. It stores cluster metadata, not application databases.

---

### Question 4

**Question**

What is the role of the Kubernetes Scheduler?

**Answer**

The Scheduler selects the most appropriate Worker Node for newly created Pods.

It considers:

- CPU availability
- Memory availability
- Resource requests
- Node affinity
- Taints and tolerations
- Node labels
- Scheduling policies

**Explanation**

The Scheduler only decides where a Pod should run. It does not create or start the Pod.

**Used in Production**

Every Pod deployment.

**Common Mistake**

Many candidates think the Scheduler creates Pods. The Kubelet actually starts the Pods.

---

### Question 5

**Question**

What is the Controller Manager in Kubernetes?

**Answer**

The Controller Manager runs controllers that continuously monitor the cluster and ensure it matches the desired state.

Common controllers include:

- Node Controller
- ReplicaSet Controller
- Deployment Controller
- Job Controller
- Endpoint Controller

**Explanation**

If the actual cluster state differs from the desired state, the Controller Manager initiates corrective actions, such as creating new Pods or replacing failed ones.

**Used in Production**

Automatic recovery, scaling, and maintaining application availability.

**Common Mistake**

Confusing the Controller Manager with the Scheduler. Controllers monitor state, while the Scheduler assigns Pods to nodes.

---

### Question 6

**Question**

What is Kubelet?

**Answer**

Kubelet is the primary agent running on every Worker Node.

Its responsibilities include:

- Registering the node with the Control Plane
- Receiving Pod assignments
- Starting containers through the Container Runtime
- Monitoring Pod health
- Reporting node status

**Explanation**

Kubelet ensures that the containers described in the Pod specification are running correctly on its node.

**Used in Production**

Every Worker Node.

**Common Mistake**

Candidates sometimes think Kubelet decides where Pods run. Scheduling is handled by the Scheduler.

---

### Question 7

**Question**

What is Kube Proxy?

**Answer**

Kube Proxy is the networking component that manages communication between Pods and Services.

It performs:

- Network routing
- Service load balancing
- Traffic forwarding
- iptables/IPVS rule management

**Explanation**

Kube Proxy ensures that traffic sent to a Service reaches one of its healthy backend Pods.

**Used in Production**

Internal application communication and Service networking.

**Common Mistake**

Confusing Kube Proxy with an external reverse proxy like Nginx. Kube Proxy manages cluster networking, not HTTP request routing.

---

### Question 8

**Question**

What is the Container Runtime?

**Answer**

The Container Runtime is the software responsible for running containers.

Common runtimes include:

- containerd
- CRI-O

Docker is no longer used directly by Kubernetes as a runtime in modern versions.

**Explanation**

The Kubelet communicates with the Container Runtime using the Container Runtime Interface (CRI) to create, start, stop, and remove containers.

**Used in Production**

Every Worker Node.

**Common Mistake**

Many candidates still answer "Docker." Modern Kubernetes commonly uses containerd or CRI-O.

---

### Question 9

**Question**

How do the API Server, Scheduler, Kubelet, and Container Runtime work together when deploying a Pod?

**Answer**

The workflow is:

1. User runs `kubectl apply`.
2. API Server validates the request.
3. etcd stores the desired state.
4. Scheduler selects a Worker Node.
5. Kubelet receives the Pod assignment.
6. Container Runtime creates the containers.
7. Pod becomes operational.

**Explanation**

Each component performs a specific task, resulting in a fully automated deployment process.

**Used in Production**

Every Kubernetes deployment.

---

### Question 10

**Question**

Which Kubernetes components run on the Control Plane and which run on Worker Nodes?

**Answer**

**Control Plane**

- API Server
- Scheduler
- Controller Manager
- etcd

**Worker Node**

- Kubelet
- Kube Proxy
- Container Runtime
- Pods

**Explanation**

Separating management components from workload components improves scalability, fault isolation, and cluster management.

**Used in Production**

Every Kubernetes architecture.

**Common Mistake**

Mixing Control Plane and Worker Node components during interviews.

---

### Question 11

**Question**

What happens if one of the Control Plane components becomes unavailable?

**Answer**

The impact depends on the failed component.

- API Server → Cluster management stops.
- etcd → Cluster state becomes unavailable.
- Scheduler → New Pods cannot be scheduled.
- Controller Manager → Self-healing and reconciliation stop.

Existing running Pods generally continue to serve traffic unless they require new scheduling or management actions.

**Explanation**

The Control Plane manages the cluster but does not directly execute application workloads.

**Used in Production**

High-availability Control Plane deployments use multiple replicas to minimize downtime.

---

### Question 12

**Question**

Why is understanding Kubernetes cluster architecture important for DevOps engineers?

**Answer**

Understanding cluster architecture helps engineers:

- Troubleshoot deployments
- Debug scheduling failures
- Diagnose networking issues
- Identify component failures
- Optimize cluster performance
- Perform disaster recovery

**Explanation**

Most production Kubernetes issues can be traced to one or more cluster components. Knowing how these components interact enables faster troubleshooting.

**Used in Production**

Daily Kubernetes administration, monitoring, and incident response.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

A developer deploys a Pod, but it remains in the Pending state. Which Kubernetes component should you investigate first?

**Answer**

Investigate the **Scheduler**.

Check:

- Available CPU and memory
- Node availability
- Taints and tolerations
- Node selectors
- Scheduling events using:

```bash
kubectl describe pod <pod-name>
```

**Explanation**

A Pending Pod usually indicates that the Scheduler cannot find a suitable Worker Node.

---

### Scenario 2

**Question**

Users report that `kubectl` commands are timing out, but existing applications continue running. Which component is most likely affected?

**Answer**

The **API Server**.

**Explanation**

Running Pods continue operating, but management operations fail because all cluster requests go through the API Server.

---

### Scenario 3

**Question**

After a Worker Node crashes, application Pods automatically start running on another node. Which Kubernetes components made this possible?

**Answer**

The recovery involves:

- Controller Manager detects missing Pods.
- Scheduler selects a healthy Worker Node.
- Kubelet starts replacement Pods.
- Container Runtime launches the containers.

**Explanation**

This demonstrates Kubernetes' self-healing capability.

---

### Scenario 4

**Question**

A Pod has been scheduled successfully, but it never starts running. Which Worker Node components should you investigate?

**Answer**

Check:

- Kubelet status
- Container Runtime status
- Node health
- Pod events
- Container logs

**Explanation**

Once scheduling is complete, the Kubelet and Container Runtime are responsible for creating and starting the containers.

---

### Scenario 5

**Question**

Your Service is reachable, but traffic is not being forwarded to backend Pods. Which Kubernetes component should you investigate?

**Answer**

Investigate **Kube Proxy**.

Check:

- Service endpoints
- iptables/IPVS rules
- Kube Proxy logs
- Pod readiness

**Explanation**

Kube Proxy manages Service networking and forwards traffic to healthy Pods.

---

### Scenario 6

**Question**

An engineer accidentally deletes the etcd database. What will happen?

**Answer**

The cluster loses its stored configuration and desired state. Existing containers may continue running temporarily, but the Control Plane cannot reliably manage the cluster until etcd is restored from backup.

**Explanation**

etcd is the single source of truth for Kubernetes.

---

### Scenario 7

**Question**

Your deployment request reaches the API Server, but no Pod is created. Which Control Plane component should you investigate next?

**Answer**

Check the **Scheduler** and **Controller Manager**.

Verify:

- Deployment events
- ReplicaSet status
- Scheduler logs
- Cluster resource availability

**Explanation**

The API Server accepts the request, but controllers and the Scheduler are responsible for creating and placing Pods.

---

### Scenario 8

**Question**

A Worker Node reports `NotReady` in the cluster. Which component running on that node is most likely responsible?

**Answer**

Investigate the **Kubelet**.

Check:

```bash
systemctl status kubelet
journalctl -u kubelet
```

**Explanation**

Kubelet reports node health to the Control Plane. If it fails, the node is typically marked `NotReady`.

---

### Scenario 9

**Question**

A Pod was scheduled successfully, but container creation repeatedly fails with runtime errors. Which component should you investigate?

**Answer**

Investigate the **Container Runtime**.

Check:

- Runtime service status
- Image availability
- Runtime logs
- Container events

**Explanation**

The Container Runtime is responsible for creating and running containers after receiving instructions from the Kubelet.

---

### Scenario 10

**Question**

During a production outage, applications remain available, but no new Pods can be scheduled after a deployment. Which Kubernetes component is most likely causing the issue?

**Answer**

The **Scheduler**.

**Explanation**

Without a functioning Scheduler, Kubernetes cannot assign newly created Pods to Worker Nodes. Existing Pods continue running, but new deployments and scaling operations remain in the Pending state until the Scheduler is restored.
