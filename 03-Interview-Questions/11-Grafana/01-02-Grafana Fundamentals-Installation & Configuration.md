# Grafana Fundamentals & Installation & Configuration Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is Grafana, and why is it used?

**Answer**

Grafana is an open-source visualization and monitoring platform used to query, visualize, and analyze metrics, logs, and traces from multiple data sources. It helps teams monitor infrastructure, applications, and business metrics through interactive dashboards.

**Explanation**

Grafana itself does not collect metrics. It connects to data sources such as Prometheus, Elasticsearch, Loki, InfluxDB, Graphite, MySQL, PostgreSQL, and Azure Monitor to display data visually.

**Where it is used in Production**

- Infrastructure monitoring
- Application monitoring
- Kubernetes monitoring
- Cloud monitoring
- DevOps and SRE dashboards

**Common Mistake**

Many candidates think Grafana stores monitoring data. In reality, Grafana only visualizes data stored in external data sources.

---

### Question 2

**Question**

Explain the Grafana architecture.

**Answer**

Grafana architecture consists of:

- Grafana Server
- Data Sources
- Dashboards
- Panels
- Users and Organizations
- Alerting Engine

The Grafana server queries connected data sources and displays the returned data through dashboards and panels.

**Explanation**

Grafana acts as the visualization layer between users and monitoring systems. It sends queries to configured data sources instead of storing metrics itself.

**Where it is used in Production**

Organizations use Grafana as a centralized dashboard for monitoring servers, containers, cloud infrastructure, and applications.

---

### Question 3

**Question**

What is a dashboard in Grafana?

**Answer**

A dashboard is a collection of panels that displays related monitoring data on a single screen.

**Explanation**

Dashboards allow teams to monitor multiple metrics such as CPU, memory, disk usage, application latency, and request rates from one location.

**Where it is used in Production**

- Infrastructure dashboards
- Kubernetes dashboards
- Application dashboards
- Database monitoring dashboards

**Common Mistake**

Confusing dashboards with panels. A dashboard contains multiple panels.

---

### Question 4

**Question**

What is a panel in Grafana?

**Answer**

A panel is an individual visualization component within a dashboard.

Examples include:

- Time Series Graph
- Gauge
- Stat
- Bar Chart
- Table
- Pie Chart
- Heatmap

**Explanation**

Each panel executes its own query against a data source and visualizes the returned results independently.

**Where it is used in Production**

Displaying individual metrics such as CPU utilization, request count, or disk usage.

---

### Question 5

**Question**

What are data sources in Grafana?

**Answer**

Data sources are external systems from which Grafana retrieves monitoring data.

Common data sources include:

- Prometheus
- Loki
- Elasticsearch
- InfluxDB
- MySQL
- PostgreSQL
- Azure Monitor
- CloudWatch

**Explanation**

Grafana connects to these systems, executes queries, and visualizes the returned data.

**Where it is used in Production**

Centralized monitoring environments where multiple monitoring systems are integrated into a single dashboard.

---

### Question 6

**Question**

Can Grafana collect metrics by itself?

**Answer**

No.

Grafana is only a visualization platform. Metrics must be collected by monitoring systems such as Prometheus or exporters.

**Explanation**

Prometheus collects metrics, while Grafana queries Prometheus and displays the results.

**Where it is used in Production**

Prometheus + Grafana is one of the most common monitoring stacks.

**Common Mistake**

Many beginners assume Grafana performs monitoring. It only visualizes monitoring data.

---

### Question 7

**Question**

How do you install Grafana on Linux?

**Answer**

Typical installation steps are:

1. Install the Grafana package.
2. Enable the Grafana service.
3. Start the service.
4. Verify the service status.
5. Access Grafana through the browser using port **3000**.

**Explanation**

Grafana runs as a service and provides a web interface for administration and dashboard creation.

**Where it is used in Production**

Linux servers, cloud virtual machines, Kubernetes clusters, and Docker containers.

---

### Question 8

**Question**

What is the default port used by Grafana?

**Answer**

Grafana listens on **TCP Port 3000** by default.

**Explanation**

Users access the Grafana web interface using:

```
http://<server-ip>:3000
```

The port can be changed in the Grafana configuration file.

**Where it is used in Production**

Accessing the Grafana web UI.

---

### Question 9

**Question**

What happens during the initial Grafana setup?

**Answer**

During the first login:

- Login using the default administrator account.
- Change the default password.
- Configure data sources.
- Create organizations if required.
- Create dashboards.

**Explanation**

The initial setup prepares Grafana for connecting to monitoring systems.

**Where it is used in Production**

Every new Grafana installation.

---

### Question 10

**Question**

What is an Organization in Grafana?

**Answer**

An Organization is a logical separation of users, dashboards, folders, and data source permissions.

**Explanation**

Organizations allow multiple teams to use the same Grafana instance while keeping their dashboards isolated.

**Where it is used in Production**

Large enterprises supporting multiple teams or business units.

---

### Question 11

**Question**

How does user authentication work in Grafana?

**Answer**

Grafana supports:

- Local user authentication
- LDAP
- OAuth
- Active Directory
- SAML
- GitHub authentication
- Google authentication

**Explanation**

Authentication determines who can access Grafana, while authorization determines what users can access.

**Where it is used in Production**

Enterprise identity management.

---

### Question 12

**Question**

Which basic configuration settings are commonly modified in Grafana?

**Answer**

Common configurations include:

- Server port
- Admin credentials
- SMTP settings
- Authentication methods
- Data source configuration
- Alerting configuration

**Explanation**

These settings are managed through the Grafana configuration file and web interface.

**Where it is used in Production**

Initial deployment and ongoing administration.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

You install Grafana successfully, but you cannot access the web interface. How would you troubleshoot the issue?

**Answer**

I would:

- Verify the Grafana service is running.
- Check whether port 3000 is listening.
- Verify firewall rules.
- Check Grafana logs.
- Confirm the server IP address.
- Test connectivity from another machine.

**Explanation**

Most access issues are caused by stopped services, blocked ports, or firewall restrictions.

---

### Scenario 2

**Question**

A dashboard displays "No Data" even though Prometheus is running. What would you check?

**Answer**

I would verify:

- Prometheus data source connection.
- Prometheus target health.
- Query correctness.
- Dashboard time range.
- Metric availability.

**Explanation**

A healthy Grafana installation depends on a properly configured data source.

---

### Scenario 3

**Question**

A developer cannot see a dashboard that another team created. What is the likely reason?

**Answer**

The dashboard may belong to a different organization or the user lacks the required permissions.

**Explanation**

Organizations and role-based permissions isolate dashboards between teams.

---

### Scenario 4

**Question**

After changing the Grafana configuration file, your changes are not reflected. What would you do?

**Answer**

I would:

- Verify the configuration syntax.
- Restart the Grafana service.
- Check the service logs.
- Confirm the correct configuration file was edited.

**Explanation**

Most configuration changes require a service restart to take effect.

---

### Scenario 5

**Question**

Your manager asks you to create a dashboard showing CPU, memory, and disk usage for Linux servers. How would you approach it?

**Answer**

I would:

1. Configure Prometheus as the data source.
2. Verify Node Exporter metrics are available.
3. Create a new dashboard.
4. Add separate panels for CPU, memory, and disk metrics.
5. Save and organize the dashboard.

**Explanation**

Grafana dashboards combine multiple related panels into a single monitoring view.

---

### Scenario 6

**Question**

A new Prometheus server has been deployed, but Grafana still shows old metrics. What would you verify?

**Answer**

I would:

- Check the configured data source.
- Verify the Prometheus URL.
- Test the connection.
- Save the updated configuration.
- Refresh the dashboard.

**Explanation**

Grafana always retrieves data from the configured data source.

---

### Scenario 7

**Question**

Several users accidentally modified a production dashboard. How can this be prevented?

**Answer**

I would:

- Use Viewer roles for most users.
- Grant Editor access only where necessary.
- Restrict Admin permissions.
- Organize dashboards into folders with appropriate permissions.

**Explanation**

Role-based access control prevents unauthorized dashboard modifications.

---

### Scenario 8

**Question**

A user reports that Grafana loads slowly. What would you investigate?

**Answer**

I would check:

- Data source response time.
- Complex dashboard queries.
- Server CPU and memory usage.
- Network latency.
- Browser performance.

**Explanation**

Slow dashboards are often caused by expensive queries or slow data sources rather than Grafana itself.

---

### Scenario 9

**Question**

Your company wants multiple teams to use a single Grafana instance without sharing dashboards. How would you implement this?

**Answer**

I would create separate Organizations or use folder-based permissions with appropriate user roles.

**Explanation**

Grafana supports logical isolation for different teams while using a single server.

---

### Scenario 10

**Question**

A production dashboard suddenly displays blank panels after a monitoring upgrade. How would you troubleshoot the issue?

**Answer**

I would:

1. Verify the data source connection.
2. Test the queries directly.
3. Check metric names for changes.
4. Review Grafana logs.
5. Verify dashboard variables.
6. Confirm Prometheus is returning data.

**Explanation**

Dashboard failures after upgrades are commonly caused by changed metric names, broken queries, or data source configuration issues.
