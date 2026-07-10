# Visualization, Logs Integration & Monitoring Integrations Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What types of metrics are commonly visualized in Grafana?

**Answer**

Grafana commonly visualizes:

- CPU metrics
- Memory metrics
- Disk metrics
- Network metrics
- Application metrics
- Kubernetes metrics
- Container metrics
- Database metrics

**Explanation**

Grafana retrieves these metrics from monitoring systems like Prometheus and presents them through dashboards to help engineers monitor infrastructure and application health.

**Where it is used in Production**

- Infrastructure monitoring
- Cloud monitoring
- Kubernetes monitoring
- DevOps dashboards
- SRE operations

**Common Mistake**

Many candidates assume Grafana collects these metrics directly. Grafana only visualizes data retrieved from configured data sources.

---

### Question 2

**Question**

Which CPU metrics are commonly monitored in Grafana?

**Answer**

Common CPU metrics include:

- CPU utilization (%)
- CPU idle time
- CPU load average
- CPU usage per core
- CPU saturation

**Explanation**

These metrics help identify overloaded servers and applications experiencing high CPU consumption.

**Where it is used in Production**

Monitoring Linux servers, Kubernetes nodes, virtual machines, and cloud instances.

---

### Question 3

**Question**

Why are memory metrics important in Grafana?

**Answer**

Memory metrics help identify excessive memory usage, memory leaks, and insufficient available memory.

Common metrics include:

- Memory usage
- Available memory
- Cached memory
- Swap usage
- Memory utilization percentage

**Explanation**

Memory monitoring helps prevent application crashes caused by resource exhaustion.

**Where it is used in Production**

Application servers, Kubernetes clusters, databases, and virtual machines.

---

### Question 4

**Question**

Which disk and network metrics are commonly monitored?

**Answer**

**Disk Metrics**

- Disk utilization
- Disk I/O
- Disk latency
- Free disk space

**Network Metrics**

- Network throughput
- Bandwidth usage
- Packet loss
- Error rate
- Network latency

**Explanation**

These metrics help detect storage bottlenecks and network performance issues.

**Where it is used in Production**

Storage monitoring, cloud infrastructure, Kubernetes nodes, and application servers.

---

### Question 5

**Question**

What are application metrics?

**Answer**

Application metrics measure the health and performance of applications.

Examples include:

- HTTP request count
- Response time
- Error rate
- Active sessions
- Request latency
- Throughput

**Explanation**

Application metrics help identify performance bottlenecks and service degradation.

**Where it is used in Production**

Web applications, APIs, microservices, and enterprise applications.

---

### Question 6

**Question**

Which Kubernetes metrics are commonly visualized in Grafana?

**Answer**

Common Kubernetes metrics include:

- Node CPU utilization
- Node memory usage
- Pod status
- Pod restarts
- Deployment replicas
- Namespace resource usage
- Cluster health

**Explanation**

These metrics help monitor Kubernetes cluster health and application availability.

**Where it is used in Production**

AKS, EKS, GKE, OpenShift, and on-premises Kubernetes clusters.

---

### Question 7

**Question**

How does Grafana integrate with Loki?

**Answer**

Grafana connects to Loki as a data source and retrieves log data using LogQL queries.

**Explanation**

Loki stores logs efficiently using labels. Grafana provides an interface for searching, filtering, and visualizing these logs.

**Where it is used in Production**

- Kubernetes logging
- Docker logging
- Application troubleshooting
- Centralized log analysis

**Common Mistake**

Confusing Loki with Prometheus. Prometheus stores metrics, while Loki stores logs.

---

### Question 8

**Question**

What is Log Exploration in Grafana?

**Answer**

Log Exploration allows users to search, filter, and analyze logs interactively using Grafana's Explore feature.

**Explanation**

Engineers can investigate application errors, trace failures, and correlate logs with metrics during incidents.

**Where it is used in Production**

Troubleshooting production issues and root cause analysis.

---

### Question 9

**Question**

How does Grafana integrate with Prometheus?

**Answer**

Grafana connects to Prometheus using its HTTP API and retrieves metrics using PromQL queries.

**Explanation**

Prometheus stores time-series metrics, while Grafana provides visualization, dashboards, and alerting.

**Where it is used in Production**

Infrastructure monitoring, Kubernetes monitoring, cloud monitoring, and application monitoring.

---

### Question 10

**Question**

What is Node Exporter, and why is it important?

**Answer**

Node Exporter is a Prometheus exporter that collects hardware and operating system metrics from Linux servers.

It exposes metrics such as:

- CPU
- Memory
- Disk
- Network
- Filesystem

**Explanation**

Prometheus scrapes Node Exporter metrics, and Grafana visualizes them through dashboards.

**Where it is used in Production**

Linux server monitoring.

---

### Question 11

**Question**

What is cAdvisor, and how is it used with Grafana?

**Answer**

cAdvisor collects container-level resource metrics such as:

- CPU usage
- Memory usage
- Filesystem usage
- Network usage

Grafana visualizes these metrics through Prometheus.

**Explanation**

It provides visibility into Docker and Kubernetes container performance.

**Where it is used in Production**

Containerized applications and Kubernetes environments.

---

### Question 12

**Question**

How does Grafana support Docker and Kubernetes monitoring?

**Answer**

Grafana integrates with Prometheus, Node Exporter, kube-state-metrics, and cAdvisor to monitor:

- Docker containers
- Kubernetes nodes
- Pods
- Deployments
- Cluster resources

**Explanation**

Grafana provides centralized dashboards that combine infrastructure, container, and application metrics.

**Where it is used in Production**

Modern DevOps, SRE, and cloud-native environments.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

A manager reports that server CPU usage has suddenly increased. How would you investigate using Grafana?

**Answer**

I would:

1. Open the CPU dashboard.
2. Check the Time Series graph.
3. Compare CPU usage across servers.
4. Identify the affected host.
5. Correlate CPU metrics with logs if necessary.

**Explanation**

Time-series visualization helps identify when the spike occurred and whether it affects one or multiple servers.

---

### Scenario 2

**Question**

An application is responding slowly, but CPU utilization is low. What metrics would you investigate next?

**Answer**

I would check:

- Memory usage
- Disk I/O
- Network latency
- HTTP response time
- Application error rate

**Explanation**

Performance issues are not always CPU-related. Other system resources or application bottlenecks may be responsible.

---

### Scenario 3

**Question**

A Kubernetes pod is repeatedly restarting. How would you troubleshoot it using Grafana?

**Answer**

I would:

- Check pod restart metrics.
- Review CPU and memory usage.
- Analyze pod logs through Loki.
- Verify deployment health.
- Review Kubernetes events.

**Explanation**

Combining metrics and logs provides faster root cause identification.

---

### Scenario 4

**Question**

Your manager wants to investigate application errors that occurred at 2:00 PM yesterday. How would you proceed?

**Answer**

I would:

- Open Grafana Explore.
- Query Loki logs for the affected time range.
- Filter logs by application or namespace.
- Correlate the logs with application metrics.

**Explanation**

Time-based log analysis helps identify the exact cause of production incidents.

---

### Scenario 5

**Question**

Node Exporter metrics suddenly disappear from Grafana dashboards. What would you check?

**Answer**

I would verify:

- Node Exporter service status.
- Prometheus target status.
- Network connectivity.
- Firewall rules.
- Prometheus scrape configuration.

**Explanation**

Missing metrics are commonly caused by exporter failures or Prometheus scrape issues.

---

### Scenario 6

**Question**

Docker container metrics are no longer visible in Grafana. How would you troubleshoot the issue?

**Answer**

I would check:

- cAdvisor status.
- Prometheus scrape targets.
- Container health.
- Dashboard queries.
- Data source connectivity.

**Explanation**

Container monitoring depends on cAdvisor successfully exposing metrics to Prometheus.

---

### Scenario 7

**Question**

A dashboard shows extremely high memory usage across all Kubernetes nodes. What would you investigate?

**Answer**

I would:

- Verify dashboard queries.
- Check Node Exporter metrics.
- Review pod resource consumption.
- Identify memory-intensive workloads.
- Correlate with application logs.

**Explanation**

High node memory usage often results from applications consuming excessive resources.

---

### Scenario 8

**Question**

A developer wants to see both application metrics and logs on a single dashboard. Is this possible?

**Answer**

Yes.

Grafana can combine Prometheus metrics and Loki logs within the same dashboard, allowing users to correlate performance metrics with log events.

**Explanation**

This significantly improves troubleshooting during production incidents.

---

### Scenario 9

**Question**

A newly added Kubernetes node is not visible on the monitoring dashboard. What would you verify?

**Answer**

I would check:

- Node Exporter installation.
- Prometheus target discovery.
- Kubernetes service discovery.
- Dashboard filters.
- Network connectivity.

**Explanation**

The node must expose metrics and be successfully scraped before Grafana can display it.

---

### Scenario 10

**Question**

Your manager asks you to create a production dashboard that displays infrastructure, Kubernetes, Docker, and application health on one screen. How would you design it?

**Answer**

I would create a dashboard with separate panels for:

- CPU utilization
- Memory usage
- Disk usage
- Network traffic
- Kubernetes node health
- Pod status
- Docker container metrics
- HTTP response time
- Error rate
- Recent application logs from Loki

**Explanation**

Combining infrastructure metrics, container metrics, Kubernetes health, application metrics, and logs provides a comprehensive operational view for DevOps and SRE teams.
