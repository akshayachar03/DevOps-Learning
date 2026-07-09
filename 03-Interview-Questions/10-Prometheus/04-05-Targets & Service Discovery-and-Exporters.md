# Targets & Service Discovery & Exporters Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What are Targets in Prometheus?

**Answer**

Targets are the endpoints from which Prometheus collects metrics. A target exposes metrics over an HTTP endpoint (typically `/metrics`) that Prometheus periodically scrapes.

Examples of targets include:

- Linux servers
- Kubernetes nodes
- Applications
- Databases
- Exporters

**Explanation**

Targets are the actual systems being monitored. Prometheus sends HTTP requests to each configured target based on the configured scrape interval and stores the collected metrics in its TSDB.

**Where it is used in Production**

Every Prometheus deployment uses targets to monitor servers, applications, databases, Kubernetes clusters, and cloud resources.

**Common Mistake**

Many candidates think Prometheus automatically discovers every target. In reality, targets must be configured manually or discovered using Service Discovery.

---

### Question 2

**Question**

What is the difference between Static Targets and Service Discovery?

**Answer**

| Static Targets | Service Discovery |
|----------------|------------------|
|Configured manually|Automatically discovered|
|Suitable for small environments|Suitable for dynamic environments|
|Requires manual updates|Automatically updates target list|
|Simple configuration|Supports cloud-native infrastructure|

**Explanation**

Static Targets are manually listed in `prometheus.yml`, whereas Service Discovery automatically detects new or removed systems from supported platforms like Kubernetes, Azure, AWS, or Consul.

**Where it is used in Production**

- Static Targets → Development and small server environments
- Service Discovery → Kubernetes, Azure, AWS, Docker, cloud-native infrastructures

**Common Mistake**

Using Static Targets in environments where servers are frequently created or destroyed.

---

### Question 3

**Question**

What is Service Discovery, and why is it important?

**Answer**

Service Discovery is a mechanism that automatically finds monitoring targets without manually updating the Prometheus configuration.

Supported discovery methods include:

- Kubernetes
- AWS EC2
- Azure
- Docker
- Consul
- DNS
- File-based discovery

**Explanation**

Modern infrastructures are highly dynamic. Service Discovery ensures Prometheus always monitors the correct resources without requiring manual configuration changes.

**Where it is used in Production**

Cloud platforms, Kubernetes clusters, auto-scaling groups, and containerized environments.

---

### Question 4

**Question**

What are Target Labels in Prometheus?

**Answer**

Target Labels are key-value pairs that identify and categorize metrics.

Examples:

```text
job="node-exporter"
instance="server01"
environment="production"
region="eastus"
```

**Explanation**

Labels provide metadata for metrics, making it easier to filter, group, aggregate, and query data using PromQL.

**Where it is used in Production**

- Environment separation
- Region-based monitoring
- Team ownership
- Application identification

**Common Mistake**

Creating too many unique labels, resulting in high-cardinality metrics and increased storage consumption.

---

### Question 5

**Question**

How do you verify whether a target is healthy in Prometheus?

**Answer**

Navigate to:

```
Status → Targets
```

Verify:

- Target state (UP or DOWN)
- Last scrape time
- Scrape duration
- Error messages

**Explanation**

The Targets page displays the health of every monitored endpoint and is the first place engineers check during monitoring issues.

**Where it is used in Production**

Daily monitoring, onboarding new targets, and troubleshooting failed metric collection.

---

### Question 6

**Question**

What is Node Exporter?

**Answer**

Node Exporter is an exporter that exposes Linux operating system metrics in Prometheus format.

It provides metrics such as:

- CPU utilization
- Memory usage
- Disk usage
- Filesystem information
- Network traffic
- Load average

Default port:

```text
9100
```

**Explanation**

Node Exporter runs as a service on Linux systems and exposes operating system metrics through the `/metrics` endpoint.

**Where it is used in Production**

Monitoring Linux servers, Kubernetes worker nodes, virtual machines, and cloud instances.

**Common Mistake**

Assuming Node Exporter monitors applications. It only collects operating system metrics.

---

### Question 7

**Question**

What is cAdvisor, and what metrics does it collect?

**Answer**

cAdvisor (Container Advisor) collects container-level performance metrics.

It monitors:

- CPU usage
- Memory usage
- Network traffic
- Filesystem usage
- Container lifecycle information

**Explanation**

cAdvisor provides detailed visibility into Docker and Kubernetes containers, allowing engineers to monitor container resource utilization.

**Where it is used in Production**

Docker environments and Kubernetes clusters.

---

### Question 8

**Question**

What is the Blackbox Exporter?

**Answer**

Blackbox Exporter performs external probes to verify service availability.

Supported probe types include:

- HTTP
- HTTPS
- TCP
- ICMP (Ping)
- DNS

**Explanation**

Unlike Node Exporter, which exposes internal system metrics, Blackbox Exporter actively tests whether services are reachable and functioning correctly.

**Where it is used in Production**

- Website monitoring
- API monitoring
- SSL certificate validation
- Network connectivity checks

**Common Mistake**

Confusing Blackbox Exporter with Node Exporter. One checks service availability, while the other exposes system metrics.

---

### Question 9

**Question**

What are Application Exporters?

**Answer**

Application Exporters expose metrics specific to an application or service.

Examples include:

- MySQL Exporter
- PostgreSQL Exporter
- Redis Exporter
- NGINX Exporter
- Apache Exporter
- HAProxy Exporter

**Explanation**

These exporters collect application-specific metrics and expose them in Prometheus format for scraping.

**Where it is used in Production**

Monitoring databases, web servers, caches, message brokers, and other applications.

---

### Question 10

**Question**

How do exporters work with Prometheus?

**Answer**

Workflow:

```text
Operating System / Application
            │
            ▼
        Exporter
            │
     /metrics Endpoint
            │
            ▼
    Prometheus Server
```

**Explanation**

Exporters collect metrics from systems or applications and expose them through an HTTP endpoint. Prometheus periodically scrapes these endpoints and stores the metrics in its TSDB.

**Where it is used in Production**

Monitoring operating systems, databases, containers, applications, and cloud services.

---

### Question 11

**Question**

How do you add a new Linux server to Prometheus monitoring?

**Answer**

Steps:

1. Install Node Exporter on the server.
2. Verify the `/metrics` endpoint is accessible.
3. Add the server to `prometheus.yml` or enable Service Discovery.
4. Reload Prometheus.
5. Confirm the target status is **UP**.

**Explanation**

A server becomes a monitoring target only after its metrics endpoint is reachable and Prometheus is configured to scrape it.

**Where it is used in Production**

Common during server provisioning and infrastructure expansion.

---

### Question 12

**Question**

Which exporter would you choose for the following scenarios?

- Linux server
- Docker containers
- Website uptime
- MySQL database

**Answer**

| Requirement | Exporter |
|------------|----------|
|Linux Server|Node Exporter|
|Docker Containers|cAdvisor|
|Website Monitoring|Blackbox Exporter|
|MySQL Monitoring|MySQL Exporter|

**Explanation**

Each exporter is designed for a specific monitoring purpose, ensuring specialized metrics are collected efficiently.

**Where it is used in Production**

Enterprise monitoring environments with multiple infrastructure components.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

A newly added Linux server appears as **DOWN** in Prometheus. How would you troubleshoot?

**Answer**

I would:

- Verify Node Exporter is running.
- Check port **9100**.
- Test:

```bash
curl http://server-ip:9100/metrics
```

- Verify firewall rules.
- Check network connectivity.
- Verify the target configuration.
- Reload Prometheus.

**Explanation**

Most **DOWN** targets are caused by exporter failures, network connectivity issues, or configuration errors.

---

### Scenario 2

**Question**

Your company uses Kubernetes, where pods are constantly created and destroyed. Would you configure Static Targets or Service Discovery?

**Answer**

I would use **Service Discovery**.

**Explanation**

Kubernetes environments are dynamic. Service Discovery automatically detects new pods and removes terminated ones without manual intervention.

---

### Scenario 3

**Question**

Your manager wants to monitor CPU and memory usage for 300 Linux servers. Which exporter would you deploy?

**Answer**

I would deploy **Node Exporter** on every Linux server.

**Explanation**

Node Exporter exposes operating system metrics such as CPU, memory, disk, and network usage.

---

### Scenario 4

**Question**

Users report that your website is inaccessible, but CPU and memory metrics look normal. Which exporter would help identify the issue?

**Answer**

I would use the **Blackbox Exporter**.

**Explanation**

Blackbox Exporter performs HTTP, HTTPS, TCP, DNS, and ICMP probes to verify service availability from an external perspective.

---

### Scenario 5

**Question**

A Docker container is consuming excessive memory. Which exporter would you use to investigate?

**Answer**

I would use **cAdvisor**.

**Explanation**

cAdvisor provides detailed container-level metrics, including CPU, memory, filesystem, and network usage.

---

### Scenario 6

**Question**

Prometheus cannot scrape a target after a firewall update. How would you identify the issue?

**Answer**

I would:

- Verify firewall rules.
- Confirm the exporter port is open.
- Test connectivity using `curl` or `telnet`.
- Check Prometheus target status.
- Review Prometheus logs.

**Explanation**

Firewall changes commonly block access to exporter endpoints, causing targets to appear **DOWN**.

---

### Scenario 7

**Question**

You notice that your Prometheus server is storing significantly more data than expected. What could be the cause?

**Answer**

Possible causes include:

- Excessive target labels
- High-cardinality metrics
- Monitoring unnecessary targets
- Short scrape intervals

**Explanation**

High-cardinality labels dramatically increase the number of stored time-series, consuming more storage and memory.

---

### Scenario 8

**Question**

Your company deploys new virtual machines every hour using an auto-scaling group. How should Prometheus monitor these systems?

**Answer**

I would configure **Service Discovery** using the cloud provider's discovery mechanism.

**Explanation**

Automatically discovered targets eliminate the need to manually update the Prometheus configuration whenever infrastructure changes.

---

### Scenario 9

**Question**

A database administrator asks you to monitor MySQL performance. Which exporter would you recommend?

**Answer**

I would recommend the **MySQL Exporter**.

**Explanation**

It exposes database-specific metrics such as connections, queries, buffer pool usage, replication status, and transaction statistics.

---

### Scenario 10

**Question**

A newly configured exporter exposes metrics correctly, but Prometheus still does not display them. What troubleshooting steps would you perform?

**Answer**

I would:

1. Verify the `/metrics` endpoint.
2. Confirm the exporter port.
3. Check the scrape configuration.
4. Validate `prometheus.yml`.
5. Reload Prometheus.
6. Verify the target status.
7. Review Prometheus logs.

**Explanation**

The issue may exist in the exporter, configuration, connectivity, or Prometheus itself. A systematic approach helps isolate the root cause efficiently.
