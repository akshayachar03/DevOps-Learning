# Essential Prometheus Commands Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

How do you start the Prometheus server?

**Answer**

The Prometheus server is started using the following command:

```bash
prometheus --config.file=prometheus.yml
```

If the configuration file is stored in another location:

```bash
prometheus --config.file=/etc/prometheus/prometheus.yml
```

When running with Docker:

```bash
docker run -p 9090:9090 prom/prometheus
```

**Explanation**

This command starts the Prometheus server, loads the configuration file, initializes the Time-Series Database (TSDB), and begins scraping configured targets.

**Where it is used in Production**

- Linux servers
- Docker containers
- Kubernetes deployments
- CI/CD testing environments

**Common Mistake**

Starting Prometheus with an incorrect configuration file path or syntax errors in `prometheus.yml`.

---

### Question 2

**Question**

How do you reload the Prometheus configuration without restarting the server?

**Answer**

Configuration can be reloaded by sending an HTTP POST request:

```bash
curl -X POST http://localhost:9090/-/reload
```

Alternatively, send a SIGHUP signal:

```bash
kill -HUP <prometheus_pid>
```

**Explanation**

Reloading applies configuration changes (such as new scrape targets or alert rules) without stopping metric collection.

**Where it is used in Production**

Whenever `prometheus.yml` or rule files are updated.

**Common Mistake**

Editing the configuration file but forgetting to reload Prometheus.

---

### Question 3

**Question**

How do you check whether Prometheus is successfully scraping targets?

**Answer**

Open the Prometheus web UI:

```
http://<prometheus-server>:9090/targets
```

or navigate to:

**Status → Targets**

**Explanation**

The Targets page displays:

- Target status (UP/DOWN)
- Last scrape time
- Scrape duration
- Endpoint URL
- Error messages

**Where it is used in Production**

Verifying exporters, applications, Kubernetes services, and infrastructure monitoring.

---

### Question 4

**Question**

What does an "UP" target indicate in Prometheus?

**Answer**

An **UP** target means Prometheus successfully scraped metrics from the endpoint during the last scrape interval.

**Explanation**

If a target is DOWN, Prometheus cannot retrieve metrics because of issues such as:

- Network connectivity
- Incorrect endpoint
- Exporter not running
- Firewall restrictions
- Authentication failures

**Where it is used in Production**

Health verification of monitored systems.

---

### Question 5

**Question**

How do you verify that metrics are being collected by Prometheus?

**Answer**

Use the Prometheus Expression Browser:

```
http://<prometheus-server>:9090
```

Enter a metric name, for example:

```promql
up
```

or

```promql
node_cpu_seconds_total
```

**Explanation**

If the metric returns values, Prometheus is successfully collecting it.

**Where it is used in Production**

Verifying newly added exporters and applications.

---

### Question 6

**Question**

How do you query metrics in Prometheus?

**Answer**

Metrics are queried using PromQL in the Expression Browser.

Example:

```promql
up
```

Example:

```promql
node_memory_MemAvailable_bytes
```

**Explanation**

PromQL retrieves current or historical metric values stored in the TSDB.

**Where it is used in Production**

- Troubleshooting
- Dashboards
- Alert creation
- Capacity planning

---

### Question 7

**Question**

How do you verify whether a newly added exporter is working?

**Answer**

Steps:

1. Open **Status → Targets**
2. Verify the exporter status is **UP**
3. Query one of its metrics

Example:

```promql
node_cpu_seconds_total
```

**Explanation**

A successful scrape confirms that Prometheus is collecting metrics from the exporter.

**Where it is used in Production**

Validating Node Exporter, cAdvisor, Blackbox Exporter, and application exporters.

---

### Question 8

**Question**

How do you verify that a Prometheus configuration change has been applied?

**Answer**

After reloading the configuration:

- Open **Status → Configuration**
- Verify the updated configuration
- Check the Targets page for newly added scrape jobs

**Explanation**

This confirms that Prometheus successfully loaded the updated configuration.

**Where it is used in Production**

Adding exporters, applications, Kubernetes services, or alert rules.

---

### Question 9

**Question**

Which PromQL query is commonly used to verify target health?

**Answer**

```promql
up
```

**Explanation**

The `up` metric returns:

- **1** → Target is reachable.
- **0** → Target is unreachable.

It is the quickest way to verify scrape health.

**Where it is used in Production**

Routine monitoring and troubleshooting.

---

### Question 10

**Question**

What are the most commonly used Prometheus operational tasks performed by DevOps engineers?

**Answer**

Common tasks include:

- Starting Prometheus
- Reloading configuration
- Checking scrape targets
- Verifying collected metrics
- Running PromQL queries
- Reviewing alerts
- Monitoring server health
- Validating exporters

**Explanation**

These activities are part of daily Prometheus administration.

**Where it is used in Production**

Production monitoring environments and DevOps operations.

---

### Question 11

**Question**

How do you troubleshoot when Prometheus is not collecting metrics?

**Answer**

Check:

- Prometheus service status
- `prometheus.yml`
- Targets page
- Exporter status
- Firewall rules
- Network connectivity
- Prometheus logs

**Explanation**

Most collection issues result from configuration errors, exporter failures, or network problems.

**Where it is used in Production**

Daily monitoring operations.

**Common Mistake**

Assuming Prometheus is faulty when the exporter itself is not running.

---

### Question 12

**Question**

Why is understanding basic Prometheus commands important for DevOps engineers?

**Answer**

These commands enable engineers to:

- Verify monitoring is functioning
- Troubleshoot monitoring issues
- Validate new exporters
- Confirm configuration changes
- Investigate production incidents

**Explanation**

Basic operational commands form the foundation of day-to-day Prometheus administration.

**Where it is used in Production**

Every production environment using Prometheus.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

You add a new Node Exporter to Prometheus, but it does not appear in Grafana. What steps would you perform?

**Answer**

I would:

- Check the exporter is running.
- Verify the scrape configuration.
- Reload Prometheus.
- Open **Status → Targets**.
- Query:

```promql
up
```

**Explanation**

These steps verify the entire metric collection pipeline.

---

### Scenario 2

**Question**

After modifying `prometheus.yml`, your new scrape job is not working. What is the most likely reason?

**Answer**

The configuration was updated but not reloaded.

I would reload Prometheus using:

```bash
curl -X POST http://localhost:9090/-/reload
```

**Explanation**

Prometheus does not automatically reload configuration changes.

---

### Scenario 3

**Question**

One exporter shows a DOWN status on the Targets page. How would you troubleshoot?

**Answer**

I would verify:

- Exporter service is running.
- Correct IP and port.
- Network connectivity.
- Firewall settings.
- Exporter endpoint (`/metrics`).
- Prometheus scrape configuration.

**Explanation**

A DOWN target indicates Prometheus cannot successfully scrape metrics.

---

### Scenario 4

**Question**

Your manager asks whether Prometheus is collecting CPU metrics from every server. How would you verify this?

**Answer**

I would query:

```promql
node_cpu_seconds_total
```

and confirm metrics are returned for every server instance.

**Explanation**

If all instances appear in the query results, Prometheus is collecting CPU metrics successfully.

---

### Scenario 5

**Question**

A newly added application exporter appears as UP, but no application metrics are visible. What would you check?

**Answer**

I would verify:

- The application exposes metrics.
- Metric names are correct.
- The `/metrics` endpoint contains the expected metrics.
- Prometheus is scraping the endpoint successfully.

**Explanation**

The exporter may be reachable but not exposing the required metrics.

---

### Scenario 6

**Question**

Prometheus starts successfully, but some targets disappear after editing the configuration. How would you investigate?

**Answer**

I would:

- Validate the configuration syntax.
- Review **Status → Configuration**.
- Review **Status → Targets**.
- Check Prometheus logs.
- Verify scrape job definitions.

**Explanation**

Configuration errors often remove or invalidate scrape jobs.

---

### Scenario 7

**Question**

A DevOps engineer reports that every target is DOWN after restarting Prometheus. What would you verify first?

**Answer**

I would verify:

- Prometheus loaded the correct configuration file.
- Exporters are running.
- Network connectivity.
- Firewall settings.

**Explanation**

A configuration issue or network problem commonly affects all targets simultaneously.

---

### Scenario 8

**Question**

You suspect Prometheus is no longer scraping metrics after a configuration update. Which page would you open first?

**Answer**

I would open:

**Status → Targets**

**Explanation**

The Targets page immediately shows whether scraping is succeeding and displays any associated errors.

---

### Scenario 9

**Question**

Your application team asks you to confirm that Prometheus is collecting HTTP request metrics. What would you do?

**Answer**

I would query the application's HTTP metric, for example:

```promql
http_requests_total
```

and verify that current values are returned.

**Explanation**

A successful query confirms that Prometheus is collecting the application's metrics.

---

### Scenario 10

**Question**

A production alert indicates that Prometheus is not monitoring one server. How would you diagnose the issue?

**Answer**

I would:

1. Check **Status → Targets**.
2. Verify the `up` metric.
3. Confirm the exporter is running.
4. Test network connectivity.
5. Review Prometheus logs.
6. Validate the scrape configuration.

**Explanation**

These steps systematically identify whether the issue is caused by the exporter, network, or Prometheus configuration.
