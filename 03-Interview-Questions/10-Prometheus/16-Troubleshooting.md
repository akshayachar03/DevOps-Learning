# Troubleshooting Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What are the most common reasons for a Prometheus target showing as **DOWN**?

**Answer**

A target may show as **DOWN** due to:

- Exporter or application not running
- Incorrect IP address or port
- Wrong scrape configuration
- Firewall blocking access
- Network connectivity issues
- Incorrect `/metrics` endpoint
- Authentication or TLS issues

**Explanation**

A DOWN status means Prometheus attempted to scrape the target but could not retrieve metrics successfully.

**Where it is used in Production**

Daily monitoring of servers, Kubernetes clusters, Docker containers, and applications.

**Common Mistake**

Restarting Prometheus immediately without checking whether the exporter or application is actually running.

---

### Question 2

**Question**

How do you troubleshoot a target that is marked as DOWN?

**Answer**

Follow these steps:

1. Open **Status → Targets**.
2. Review the error message.
3. Verify the exporter or application is running.
4. Check IP address and port.
5. Test network connectivity.
6. Verify firewall rules.
7. Confirm the `/metrics` endpoint is accessible.

**Explanation**

The Targets page usually provides the exact reason for the scrape failure, making it the first place to investigate.

**Where it is used in Production**

Resolving monitoring failures for infrastructure and applications.

---

### Question 3

**Question**

What are scrape failures in Prometheus?

**Answer**

Scrape failures occur when Prometheus cannot collect metrics from a configured target.

Common causes include:

- Network issues
- Exporter failure
- Invalid endpoint
- Timeout
- Authentication failure
- Incorrect scrape configuration

**Explanation**

Scrape failures prevent Prometheus from storing updated metrics for the affected target.

**Where it is used in Production**

Infrastructure monitoring and application monitoring.

---

### Question 4

**Question**

Why might Prometheus not collect metrics even though the exporter is running?

**Answer**

Possible reasons include:

- Incorrect scrape configuration
- Wrong metrics endpoint
- Firewall restrictions
- Prometheus configuration not reloaded
- Incorrect labels
- TLS or authentication issues

**Explanation**

A running exporter alone does not guarantee successful metric collection; Prometheus must be able to reach and scrape the endpoint.

**Where it is used in Production**

Adding new exporters and applications to monitoring.

**Common Mistake**

Assuming the exporter is functioning correctly without verifying the `/metrics` endpoint.

---

### Question 5

**Question**

How do you troubleshoot missing metrics in Prometheus?

**Answer**

I would verify:

- The target status is **UP**.
- The exporter exposes the required metrics.
- The metric name is correct.
- PromQL query is correct.
- Prometheus has successfully scraped the target.
- Labels are not filtering out the metric.

**Explanation**

Missing metrics may result from incorrect instrumentation, scrape failures, or query errors.

**Where it is used in Production**

Application onboarding and dashboard troubleshooting.

---

### Question 6

**Question**

What are common configuration errors in `prometheus.yml`?

**Answer**

Common errors include:

- YAML syntax mistakes
- Incorrect indentation
- Wrong target IP or port
- Invalid scrape interval
- Incorrect job names
- Missing configuration sections

**Explanation**

Prometheus relies on a valid YAML configuration file. Syntax or structural errors can prevent configuration from loading correctly.

**Where it is used in Production**

Whenever new scrape jobs or alert rules are added.

---

### Question 7

**Question**

How do you verify whether a configuration error exists?

**Answer**

I would:

- Check Prometheus logs.
- Open **Status → Configuration**.
- Reload the configuration.
- Verify new targets appear.
- Check the Targets page for errors.

**Explanation**

Prometheus logs and the Configuration page help identify configuration-related issues.

**Where it is used in Production**

Routine maintenance and troubleshooting.

---

### Question 8

**Question**

Why might a Prometheus alert rule fail to trigger?

**Answer**

Possible reasons include:

- Incorrect PromQL expression
- Wrong metric name
- Incorrect labels
- Alert condition not satisfied
- `for` duration not completed
- Alertmanager not configured

**Explanation**

Alert generation depends on successful metric collection, rule evaluation, and Alertmanager integration.

**Where it is used in Production**

Production alerting systems.

---

### Question 9

**Question**

How do you troubleshoot Alert Rule issues?

**Answer**

I would verify:

- The metric exists.
- The PromQL query returns results.
- The alert rule syntax is correct.
- The alert state (Inactive, Pending, or Firing).
- Alertmanager connectivity.
- Notification routing configuration.

**Explanation**

An issue in any stage of the alerting pipeline can prevent notifications.

**Where it is used in Production**

Critical infrastructure monitoring.

---

### Question 10

**Question**

What are common exporter-related issues?

**Answer**

Common issues include:

- Exporter service not running
- Wrong listening port
- Missing permissions
- Incorrect endpoint
- Version incompatibility
- Firewall restrictions

**Explanation**

Exporters expose metrics for Prometheus. If they fail, Prometheus cannot collect data.

**Where it is used in Production**

Node Exporter, cAdvisor, Blackbox Exporter, and application exporters.

---

### Question 11

**Question**

Which tools or pages are commonly used to troubleshoot Prometheus issues?

**Answer**

Common troubleshooting tools include:

- **Status → Targets**
- **Status → Configuration**
- **Expression Browser**
- Prometheus logs
- Exporter logs
- Alertmanager UI
- Grafana dashboards

**Explanation**

These tools help identify failures in metric collection, querying, configuration, and alerting.

**Where it is used in Production**

Daily monitoring operations.

---

### Question 12

**Question**

What is a systematic approach to troubleshooting Prometheus issues?

**Answer**

A recommended workflow is:

1. Verify Prometheus is running.
2. Check the Targets page.
3. Review Prometheus logs.
4. Test the exporter endpoint.
5. Validate `prometheus.yml`.
6. Query the metric.
7. Verify Alertmanager (if alerts are affected).
8. Confirm Grafana dashboards (if visualization is affected).

**Explanation**

Following a structured troubleshooting process minimizes downtime and speeds up issue resolution.

**Where it is used in Production**

Enterprise monitoring environments.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

A newly added Node Exporter appears as **DOWN** in Prometheus. How would you troubleshoot the issue?

**Answer**

I would:

- Verify the Node Exporter service is running.
- Check the configured IP address and port.
- Test access to the `/metrics` endpoint.
- Verify firewall rules.
- Review the Targets page for specific errors.

**Explanation**

Most Node Exporter issues are caused by service failures, incorrect endpoints, or network restrictions.

---

### Scenario 2

**Question**

Prometheus is scraping a target successfully, but Grafana displays **No Data**. What would you investigate?

**Answer**

I would verify:

- The metric exists in Prometheus.
- The PromQL query is correct.
- The Grafana data source is configured properly.
- Dashboard filters and time range.

**Explanation**

Successful scraping does not guarantee that Grafana queries are correct.

---

### Scenario 3

**Question**

After editing `prometheus.yml`, several targets disappear. What steps would you take?

**Answer**

I would:

- Check the YAML syntax.
- Review Prometheus logs.
- Verify the configuration was reloaded.
- Open **Status → Configuration**.
- Confirm the scrape jobs still exist.

**Explanation**

Configuration errors commonly remove or invalidate scrape jobs.

---

### Scenario 4

**Question**

Your manager reports that no CPU metrics are visible for a server. How would you investigate?

**Answer**

I would:

- Verify Node Exporter is running.
- Confirm the target status is **UP**.
- Query:

```promql
node_cpu_seconds_total
```

- Check the `/metrics` endpoint.

**Explanation**

These steps confirm whether CPU metrics are being exposed and collected.

---

### Scenario 5

**Question**

An alert should fire when CPU usage exceeds 90%, but no notification is received. What would you check?

**Answer**

I would verify:

- The metric exists.
- The alert expression is correct.
- The alert is in the Firing state.
- Alertmanager connectivity.
- Notification routing.

**Explanation**

The problem may be in the alert rule, Alertmanager, or notification configuration.

---

### Scenario 6

**Question**

Prometheus reports frequent scrape timeouts for several exporters. What could be the cause?

**Answer**

Possible causes include:

- Slow exporter response
- Network latency
- High server load
- Low scrape timeout value
- Resource constraints

**Explanation**

If an exporter cannot respond before the configured timeout, the scrape fails.

---

### Scenario 7

**Question**

A developer says a newly deployed application is not exposing metrics. How would you verify this?

**Answer**

I would:

- Access the `/metrics` endpoint directly.
- Verify application instrumentation.
- Confirm the exporter is configured.
- Check Prometheus scrape configuration.

**Explanation**

The issue may be with the application rather than Prometheus.

---

### Scenario 8

**Question**

All targets suddenly become DOWN after a firewall update. What is the most likely cause?

**Answer**

The firewall is likely blocking Prometheus from accessing the exporters.

I would verify:

- Firewall rules
- Network connectivity
- Exporter ports

**Explanation**

Prometheus requires network access to scrape metrics.

---

### Scenario 9

**Question**

A dashboard shows outdated metrics even though Prometheus is running. How would you troubleshoot?

**Answer**

I would verify:

- Scrape intervals
- Target health
- Prometheus logs
- Grafana refresh interval
- PromQL query
- Exporter status

**Explanation**

Stale dashboards can result from failed scrapes, delayed refreshes, or incorrect queries.

---

### Scenario 10

**Question**

Your organization experiences a monitoring outage after a Prometheus configuration change. What troubleshooting approach would you follow?

**Answer**

I would:

1. Review the recent configuration changes.
2. Check Prometheus logs.
3. Validate the configuration syntax.
4. Reload or restore the previous configuration if necessary.
5. Verify Targets are UP.
6. Confirm metrics are being collected.
7. Verify Alertmanager and Grafana functionality.

**Explanation**

A structured rollback and verification process minimizes downtime and restores monitoring services quickly.
