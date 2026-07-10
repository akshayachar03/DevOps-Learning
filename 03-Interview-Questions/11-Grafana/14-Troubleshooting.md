# Troubleshooting Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

A Grafana dashboard is displaying **"No Data"**. What are the possible causes?

**Answer**

Common causes include:

- Data source is unreachable.
- Incorrect query.
- Wrong time range selected.
- No metrics are being collected.
- Labels or filters do not match any metrics.
- Prometheus target is down.

**Explanation**

Grafana only visualizes data returned by the data source. If the query returns no results or the data source cannot provide data, the panel displays "No Data."

**Where it is used in Production**

One of the most common issues encountered while monitoring production systems.

**Common Mistake**

Many candidates immediately blame Grafana instead of first verifying the data source and query.

---

### Question 2

**Question**

How do you troubleshoot Data Source Connection Issues in Grafana?

**Answer**

I would check:

- Data source URL
- Network connectivity
- Authentication credentials
- Firewall rules
- TLS/SSL configuration
- Data source health using **Save & Test**
- Logs of both Grafana and the monitoring system

**Explanation**

Grafana must successfully communicate with the backend monitoring system before dashboards can retrieve metrics.

**Where it is used in Production**

Whenever a new monitoring system is integrated or dashboards suddenly stop displaying data.

---

### Question 3

**Question**

How do you troubleshoot Query Errors in Grafana?

**Answer**

I would:

- Verify query syntax.
- Test the query in Explore.
- Check metric names.
- Verify label filters.
- Ensure the selected time range contains data.
- Review data source logs.

**Explanation**

Most query failures occur because of incorrect syntax, invalid metric names, or label mismatches.

**Where it is used in Production**

During dashboard development and troubleshooting.

---

### Question 4

**Question**

How do you verify whether a Grafana data source is working correctly?

**Answer**

Use the **Save & Test** button in the data source configuration.

A successful test confirms:

- Network connectivity
- Authentication
- API communication

**Explanation**

Grafana performs a connectivity test with the configured backend before confirming the data source is operational.

**Where it is used in Production**

Immediately after configuring or modifying a data source.

---

### Question 5

**Question**

Why might Grafana alerts fail to trigger?

**Answer**

Possible reasons include:

- Incorrect alert rule
- Query returns no data
- Evaluation interval is too long
- Notification policy misconfiguration
- Contact point issues
- Data source unavailable

**Explanation**

Alerting depends on successful query execution and proper notification configuration.

**Where it is used in Production**

Monitoring production infrastructure and applications.

**Common Mistake**

Candidates often check only the notification channel instead of verifying the alert rule itself.

---

### Question 6

**Question**

What can cause Dashboard Loading Issues in Grafana?

**Answer**

Common causes include:

- Slow database queries
- Large dashboards
- Network latency
- Browser cache issues
- Heavy PromQL queries
- Backend performance problems

**Explanation**

Dashboard performance depends on query execution speed, browser rendering, and backend response time.

**Where it is used in Production**

Large enterprise monitoring environments.

---

### Question 7

**Question**

How do you troubleshoot Permission Issues in Grafana?

**Answer**

Check:

- User role
- Team membership
- Folder permissions
- Dashboard permissions
- Organization membership

**Explanation**

Grafana uses Role-Based Access Control (RBAC). A user may authenticate successfully but still lack authorization to access dashboards.

**Where it is used in Production**

Multi-team enterprise environments.

---

### Question 8

**Question**

How can you determine whether the issue is in Grafana or the data source?

**Answer**

I would:

- Open Explore.
- Execute a simple query.
- Test the data source.
- Check backend metrics directly.
- Review Grafana logs.

If the backend returns data, the issue is likely with the dashboard or query.

**Explanation**

Separating frontend and backend issues helps reduce troubleshooting time.

**Where it is used in Production**

Daily monitoring operations.

---

### Question 9

**Question**

Why is selecting the correct time range important in Grafana?

**Answer**

If the selected time range does not include available metrics, panels will display "No Data."

**Explanation**

Grafana only queries data within the selected time window.

**Where it is used in Production**

Incident analysis and historical troubleshooting.

**Common Mistake**

Candidates frequently overlook the time picker while troubleshooting dashboards.

---

### Question 10

**Question**

What logs would you check while troubleshooting Grafana?

**Answer**

I would check:

- Grafana server logs
- Prometheus logs
- Loki logs (if applicable)
- Reverse proxy logs
- Browser Developer Console

**Explanation**

Logs provide valuable information about authentication failures, query errors, and connectivity issues.

**Where it is used in Production**

Production incident investigations.

---

### Question 11

**Question**

How does the Explore feature help in troubleshooting?

**Answer**

Explore allows engineers to execute ad hoc queries without modifying dashboards.

It helps verify:

- Metric availability
- Query correctness
- Label values
- Time ranges

**Explanation**

Explore isolates query issues from dashboard configuration problems.

**Where it is used in Production**

Root cause analysis during production incidents.

---

### Question 12

**Question**

What is your general troubleshooting approach when a Grafana dashboard is not working?

**Answer**

I follow this sequence:

1. Check dashboard time range.
2. Verify data source health.
3. Test queries in Explore.
4. Verify metric availability.
5. Review logs.
6. Check user permissions.
7. Confirm backend monitoring system is healthy.

**Explanation**

Following a structured troubleshooting process avoids unnecessary debugging and reduces incident resolution time.

**Where it is used in Production**

Standard DevOps and SRE troubleshooting workflow.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

A production dashboard suddenly displays "No Data" for every panel. How would you troubleshoot it?

**Answer**

I would:

- Verify the time range.
- Test the data source.
- Check Prometheus targets.
- Run queries in Explore.
- Review Grafana logs.
- Verify network connectivity.

**Explanation**

Most "No Data" incidents originate from backend monitoring failures or incorrect queries rather than Grafana itself.

---

### Scenario 2

**Question**

After adding a new Prometheus data source, every dashboard fails to load metrics. What would you check?

**Answer**

I would verify:

- Prometheus URL
- Network connectivity
- Firewall rules
- Authentication
- Save & Test result
- Prometheus `/targets` page

**Explanation**

A data source must be reachable before dashboards can retrieve metrics.

---

### Scenario 3

**Question**

A dashboard loads successfully, but one panel shows an error while others work correctly. What is your approach?

**Answer**

I would:

- Check the panel query.
- Test it in Explore.
- Verify metric names.
- Check labels.
- Confirm the selected time range.

**Explanation**

Panel-specific issues usually indicate query or metric problems.

---

### Scenario 4

**Question**

Grafana alerts are configured, but notifications are never received. What would you investigate?

**Answer**

I would verify:

- Alert rule evaluation
- Alert state
- Notification policy
- Contact point configuration
- SMTP/Slack/Webhook settings
- Alertmanager integration (if used)

**Explanation**

Successful alert evaluation alone does not guarantee notification delivery.

---

### Scenario 5

**Question**

A user can log in but receives "Access Denied" when opening a dashboard. What would you check?

**Answer**

I would verify:

- User role
- Team membership
- Folder permissions
- Dashboard permissions
- Organization assignment

**Explanation**

Authentication confirms identity, while authorization determines resource access.

---

### Scenario 6

**Question**

Dashboard loading has become very slow after adding multiple panels. What would you do?

**Answer**

I would:

- Optimize PromQL queries.
- Reduce dashboard refresh frequency.
- Minimize expensive aggregations.
- Split large dashboards.
- Check backend performance.

**Explanation**

Large dashboards with complex queries increase rendering time.

---

### Scenario 7

**Question**

A developer says the PromQL query works in Prometheus but fails in Grafana. What would you investigate?

**Answer**

I would check:

- Data source selection
- Dashboard variables
- Time range
- Query syntax modifications
- Label filters

**Explanation**

The query itself may be correct, but dashboard variables or filters can change the result.

---

### Scenario 8

**Question**

After upgrading Grafana, dashboards are not loading correctly. How would you troubleshoot?

**Answer**

I would:

- Review Grafana logs.
- Check plugin compatibility.
- Verify data source connections.
- Clear browser cache.
- Test dashboards individually.

**Explanation**

Version upgrades can introduce plugin compatibility or configuration issues.

---

### Scenario 9

**Question**

Some dashboards work, while newly created dashboards always show "No Data." What is your approach?

**Answer**

I would verify:

- Correct data source selection.
- Query syntax.
- Metric names.
- Labels.
- Dashboard variables.
- Time range.

**Explanation**

New dashboards commonly fail due to incorrect queries rather than infrastructure issues.

---

### Scenario 10

**Question**

During a production incident, management reports that monitoring dashboards are unavailable. What would you do first?

**Answer**

I would:

1. Check Grafana service status.
2. Verify data source availability.
3. Review Grafana logs.
4. Confirm network connectivity.
5. Test queries in Explore.
6. Verify Prometheus health.

**Explanation**

This structured workflow quickly determines whether the issue lies with Grafana, the monitoring backend, or the underlying infrastructure, minimizing production downtime.
