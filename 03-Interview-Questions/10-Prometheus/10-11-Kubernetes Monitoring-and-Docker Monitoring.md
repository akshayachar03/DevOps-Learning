# Kubernetes Monitoring & Docker Monitoring Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

How does Prometheus monitor a Kubernetes cluster?

**Answer**

Prometheus monitors a Kubernetes cluster by scraping metrics exposed by Kubernetes components and applications. It collects metrics from components such as:

- kube-apiserver
- kubelet
- kube-state-metrics
- Node Exporter
- cAdvisor
- Application exporters

These targets are discovered automatically using Kubernetes Service Discovery.

**Explanation**

Prometheus periodically scrapes metrics from Kubernetes components and stores them in its Time-Series Database (TSDB). This enables monitoring of cluster health, workloads, and applications.

**Where it is used in Production**

- Kubernetes health monitoring
- Cluster capacity planning
- Performance monitoring
- Alert generation

**Common Mistake**

Attempting to monitor Kubernetes without configuring Service Discovery or required exporters.

---

### Question 2

**Question**

Which Kubernetes components are commonly monitored using Prometheus?

**Answer**

Commonly monitored components include:

- Kubernetes API Server
- Scheduler
- Controller Manager
- Kubelet
- kube-proxy
- etcd
- Node Exporter
- kube-state-metrics
- cAdvisor

**Explanation**

Each component exposes different operational metrics that help identify issues in cluster health and performance.

**Where it is used in Production**

Enterprise Kubernetes monitoring solutions.

---

### Question 3

**Question**

How do you monitor Kubernetes worker nodes using Prometheus?

**Answer**

Worker nodes are typically monitored using Node Exporter.

Node Exporter exposes metrics such as:

- CPU usage
- Memory utilization
- Disk usage
- Network statistics
- Load average
- Filesystem utilization

**Explanation**

Prometheus scrapes these metrics from every node, providing visibility into infrastructure health.

**Where it is used in Production**

Infrastructure monitoring and capacity planning.

---

### Question 4

**Question**

How do you monitor Pods in Kubernetes using Prometheus?

**Answer**

Pods can be monitored using:

- cAdvisor metrics
- kube-state-metrics
- Application-specific exporters

Metrics commonly monitored include:

- CPU usage
- Memory usage
- Restart count
- Running status
- Network traffic

**Explanation**

Pod-level monitoring helps detect resource exhaustion and application failures.

**Where it is used in Production**

Microservices monitoring and troubleshooting.

---

### Question 5

**Question**

How do you monitor Kubernetes Deployments?

**Answer**

Deployments are monitored using kube-state-metrics.

Common metrics include:

- Desired replicas
- Available replicas
- Updated replicas
- Unavailable replicas
- Deployment status

**Explanation**

These metrics indicate whether Deployments are healthy and successfully rolling out updates.

**Where it is used in Production**

Deployment health monitoring.

---

### Question 6

**Question**

What is kube-state-metrics?

**Answer**

kube-state-metrics is a Kubernetes component that exposes metrics about Kubernetes objects rather than resource usage.

Examples include:

- Pods
- Deployments
- StatefulSets
- ReplicaSets
- Nodes
- Namespaces

**Explanation**

Unlike cAdvisor, kube-state-metrics reports the desired and current state of Kubernetes resources.

**Where it is used in Production**

Monitoring Kubernetes object status and health.

---

### Question 7

**Question**

How does Prometheus monitor Docker containers?

**Answer**

Prometheus monitors Docker containers primarily through cAdvisor.

cAdvisor exposes metrics such as:

- CPU usage
- Memory usage
- Network usage
- Filesystem usage
- Container lifecycle information

**Explanation**

Prometheus periodically scrapes these metrics to monitor container performance.

**Where it is used in Production**

Docker hosts and Kubernetes worker nodes.

---

### Question 8

**Question**

What is cAdvisor?

**Answer**

cAdvisor (Container Advisor) is a monitoring tool that collects resource usage and performance metrics for running containers.

It provides metrics for:

- CPU
- Memory
- Disk I/O
- Network I/O
- Filesystem usage

**Explanation**

cAdvisor is integrated into the kubelet and is commonly used by Prometheus to monitor container performance.

**Where it is used in Production**

Docker environments and Kubernetes clusters.

---

### Question 9

**Question**

Which metrics are commonly collected from Docker containers?

**Answer**

Common metrics include:

- CPU utilization
- Memory consumption
- Container restarts
- Network traffic
- Disk I/O
- Filesystem usage
- Running container count

**Explanation**

These metrics help identify performance bottlenecks and resource issues.

**Where it is used in Production**

Container monitoring dashboards and alerting systems.

---

### Question 10

**Question**

Why are Node Exporter, cAdvisor, and kube-state-metrics all required for Kubernetes monitoring?

**Answer**

Each component provides different metrics:

- **Node Exporter** → Node operating system metrics
- **cAdvisor** → Container resource metrics
- **kube-state-metrics** → Kubernetes object state metrics

**Explanation**

Using all three provides complete visibility into infrastructure, containers, and Kubernetes resources.

**Where it is used in Production**

Production Kubernetes monitoring stacks.

**Common Mistake**

Expecting one exporter to provide every type of Kubernetes metric.

---

### Question 11

**Question**

How are Kubernetes metrics visualized after Prometheus collects them?

**Answer**

Metrics are visualized using Grafana dashboards.

Grafana queries Prometheus using PromQL to display:

- Cluster health
- Node utilization
- Pod status
- Deployment status
- Container resource usage

**Explanation**

Grafana provides interactive dashboards for analyzing Prometheus metrics.

**Where it is used in Production**

Operations dashboards and NOC monitoring.

---

### Question 12

**Question**

What are the benefits of monitoring Kubernetes and Docker using Prometheus?

**Answer**

Benefits include:

- Real-time infrastructure visibility
- Faster troubleshooting
- Capacity planning
- Alert generation
- Resource optimization
- High availability monitoring
- Historical performance analysis

**Explanation**

Continuous monitoring improves system reliability and helps identify issues before they impact users.

**Where it is used in Production**

Cloud-native platforms, Kubernetes clusters, and containerized applications.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

Several Pods are restarting repeatedly in production. How would you investigate using Prometheus?

**Answer**

I would check:

- Pod restart metrics
- CPU usage
- Memory usage
- Container logs
- Grafana dashboards
- Alert history

**Explanation**

Resource exhaustion or application failures often cause repeated Pod restarts.

---

### Scenario 2

**Question**

One Kubernetes node becomes slow, affecting multiple applications. How would you identify the problem?

**Answer**

I would examine Node Exporter metrics for:

- CPU utilization
- Memory utilization
- Disk usage
- Load average
- Network traffic

**Explanation**

Node-level metrics help determine whether the issue is caused by resource exhaustion or hardware problems.

---

### Scenario 3

**Question**

A Deployment shows only two available replicas when five are expected. Which metrics would you check?

**Answer**

I would use kube-state-metrics to verify:

- Desired replicas
- Available replicas
- Updated replicas
- Unavailable replicas

**Explanation**

These metrics quickly indicate deployment rollout problems.

---

### Scenario 4

**Question**

Your Docker container suddenly starts consuming excessive memory. How would Prometheus help?

**Answer**

I would review cAdvisor memory metrics and historical Grafana graphs to identify when the memory usage increased and correlate it with deployments or traffic changes.

**Explanation**

Historical metrics help identify memory leaks and abnormal behavior.

---

### Scenario 5

**Question**

Management wants a dashboard showing CPU utilization for every Kubernetes node. Which exporter would you use?

**Answer**

I would use Node Exporter.

**Explanation**

Node Exporter provides operating system metrics, including CPU utilization for each worker node.

---

### Scenario 6

**Question**

Your application team wants container-level CPU usage rather than node-level CPU usage. Which exporter provides this information?

**Answer**

cAdvisor.

**Explanation**

cAdvisor exposes CPU, memory, network, and filesystem metrics for individual containers.

---

### Scenario 7

**Question**

Prometheus is successfully scraping Node Exporter, but Pod metrics are missing. What would you check?

**Answer**

I would verify:

- cAdvisor availability
- kubelet metrics endpoint
- Scrape configuration
- Target health
- Service Discovery configuration

**Explanation**

Pod metrics are typically collected through cAdvisor or kubelet endpoints rather than Node Exporter.

---

### Scenario 8

**Question**

A DevOps engineer wants alerts when any Kubernetes node exceeds 90% CPU utilization for more than five minutes. How would you implement this?

**Answer**

I would create a Prometheus alert rule using Node Exporter CPU metrics with a `for: 5m` condition and send alerts through Alertmanager.

**Explanation**

Using the `for` field prevents alerts caused by temporary CPU spikes.

---

### Scenario 9

**Question**

A newly deployed application is not appearing in Grafana dashboards. What would you investigate?

**Answer**

I would verify:

- The application exposes Prometheus metrics.
- Prometheus is scraping the application.
- Service Discovery is working.
- The target is UP.
- The Grafana dashboard uses the correct PromQL query.

**Explanation**

Missing dashboards are usually caused by missing metrics, incorrect scrape configuration, or incorrect queries.

---

### Scenario 10

**Question**

Your manager asks for a dashboard showing cluster health, node utilization, deployment status, and container resource usage. Which monitoring components would you deploy?

**Answer**

I would deploy:

- Prometheus Server
- Node Exporter
- kube-state-metrics
- cAdvisor
- Alertmanager
- Grafana

**Explanation**

Together, these components provide complete monitoring for Kubernetes infrastructure, workloads, containers, alerting, and visualization.
