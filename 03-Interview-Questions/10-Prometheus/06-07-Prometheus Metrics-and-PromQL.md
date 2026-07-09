# Prometheus Metrics & PromQL Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What are Prometheus metrics, and why are they important?

**Answer**

Prometheus metrics are numerical measurements collected over time that represent the health and performance of systems and applications.

Examples include:

- CPU utilization
- Memory usage
- HTTP request count
- Disk I/O
- Network traffic
- Application response time

**Explanation**

Metrics are the foundation of Prometheus monitoring. They are stored as time-series data and queried using PromQL for dashboards, alerting, and troubleshooting.

**Where it is used in Production**

- Infrastructure monitoring
- Application monitoring
- Kubernetes monitoring
- Capacity planning
- Performance analysis

**Common Mistake**

Confusing metrics with logs. Metrics are numerical values tracked over time, while logs are detailed event records.

---

### Question 2

**Question**

What are the four metric types supported by Prometheus?

**Answer**

Prometheus supports four metric types:

- Counter
- Gauge
- Histogram
- Summary

**Explanation**

Each metric type is designed for a different monitoring scenario.

| Metric Type | Used For |
|-------------|----------|
|Counter|Values that only increase|
|Gauge|Values that increase and decrease|
|Histogram|Distribution of values|
|Summary|Latency quantiles and totals|

**Where it is used in Production**

Monitoring applications, infrastructure, APIs, and microservices.

---

### Question 3

**Question**

What is a Counter metric? Give an example.

**Answer**

A Counter is a cumulative metric whose value only increases or resets to zero after a restart.

Examples:

- Total HTTP requests
- Total API calls
- Total login attempts
- Total errors

Example metric:

```text
http_requests_total
```

**Explanation**

Counters are ideal for tracking events that continually accumulate over time.

**Where it is used in Production**

- API request counting
- Error tracking
- Transaction counting
- Login statistics

**Common Mistake**

Using Counters for values like CPU or memory utilization, which should use Gauges instead.

---

### Question 4

**Question**

What is a Gauge metric? Give an example.

**Answer**

A Gauge represents values that can increase or decrease.

Examples:

- CPU utilization
- Memory usage
- Temperature
- Active users
- Queue length

Example metric:

```text
node_memory_MemAvailable_bytes
```

**Explanation**

Gauges represent the current state of a system rather than cumulative events.

**Where it is used in Production**

Monitoring real-time infrastructure and application resource utilization.

---

### Question 5

**Question**

What is a Histogram metric, and when should it be used?

**Answer**

A Histogram measures the distribution of observed values by grouping them into predefined buckets.

Example:

- HTTP request duration
- API latency
- Database query execution time

It provides:

- Bucket counts
- Total observations
- Sum of observations

**Explanation**

Histograms are useful for calculating percentiles and understanding how values are distributed.

**Where it is used in Production**

Performance monitoring, latency analysis, and SLA measurement.

---

### Question 6

**Question**

What is a Summary metric?

**Answer**

A Summary measures observed values and calculates configurable quantiles such as:

- 50th percentile
- 90th percentile
- 95th percentile
- 99th percentile

It also provides:

- Total count
- Total sum

**Explanation**

Summaries calculate quantiles directly on the client side before exposing the metrics.

**Where it is used in Production**

Application response time monitoring.

**Common Mistake**

Confusing Histograms and Summaries. Histograms calculate quantiles at query time, while Summaries calculate them during metric collection.

---

### Question 7

**Question**

What is PromQL?

**Answer**

PromQL (Prometheus Query Language) is the query language used to retrieve, analyze, and aggregate Prometheus metrics.

Example:

```promql
node_cpu_seconds_total
```

**Explanation**

PromQL enables engineers to build dashboards, create alerts, analyze historical trends, and troubleshoot production issues.

**Where it is used in Production**

- Grafana dashboards
- Alert rules
- Capacity planning
- Performance analysis

---

### Question 8

**Question**

What is the difference between Instant Queries and Range Queries?

**Answer**

| Instant Query | Range Query |
|---------------|-------------|
|Returns current metric value|Returns historical values|
|Single timestamp|Multiple timestamps|
|Used for current status|Used for trends and graphs|

Example Instant Query:

```promql
up
```

Example Range Query:

```promql
rate(http_requests_total[5m])
```

**Explanation**

Instant Queries evaluate metrics at a single point in time, while Range Queries evaluate metrics over a specified time interval.

**Where it is used in Production**

- Instant Queries → Alerting and troubleshooting
- Range Queries → Dashboards and trend analysis

---

### Question 9

**Question**

What are Selectors in PromQL?

**Answer**

Selectors filter metrics using labels.

Example:

```promql
node_cpu_seconds_total{instance="server01"}
```

Multiple labels:

```promql
http_requests_total{
job="api",
environment="production"
}
```

**Explanation**

Selectors help retrieve only the metrics relevant to a specific application, server, or environment.

**Where it is used in Production**

Filtering metrics for dashboards, alerts, and troubleshooting.

---

### Question 10

**Question**

What are Aggregation Functions in PromQL?

**Answer**

Aggregation functions combine multiple metric values into a single result.

Common functions include:

- sum()
- avg()
- min()
- max()
- count()

Example:

```promql
sum(node_memory_MemAvailable_bytes)
```

**Explanation**

Aggregation functions help summarize metrics across multiple servers, containers, or applications.

**Where it is used in Production**

Infrastructure dashboards, capacity planning, and cluster-wide monitoring.

---

### Question 11

**Question**

What are Rate Functions in PromQL, and when are they used?

**Answer**

Rate functions calculate the rate of change for Counter metrics.

Common functions:

- rate()
- irate()

Example:

```promql
rate(http_requests_total[5m])
```

**Explanation**

Since Counters only increase, rate functions calculate how quickly the value is increasing over a specific period.

**Where it is used in Production**

- Request rate monitoring
- Error rate monitoring
- Traffic analysis
- Throughput measurement

**Common Mistake**

Using `rate()` on Gauge metrics. It should only be used with Counter metrics.

---

### Question 12

**Question**

How can you filter metrics using PromQL?

**Answer**

PromQL supports label filtering.

Examples:

Exact match:

```promql
up{job="node"}
```

Not equal:

```promql
up{job!="node"}
```

Regex:

```promql
up{instance=~"server.*"}
```

Negative regex:

```promql
up{instance!~"test.*"}
```

**Explanation**

Filtering allows engineers to retrieve only the metrics relevant to a particular environment, application, or server.

**Where it is used in Production**

Dashboards, alerting rules, troubleshooting, and environment-specific monitoring.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

Your manager wants to monitor the total number of API requests processed by an application. Which metric type would you use?

**Answer**

I would use a **Counter**.

**Explanation**

API requests continually increase over time, making Counter the correct metric type.

---

### Scenario 2

**Question**

You need to monitor current memory utilization on a Linux server. Which metric type is appropriate?

**Answer**

I would use a **Gauge**.

**Explanation**

Memory usage continuously increases and decreases, making Gauge the correct choice.

---

### Scenario 3

**Question**

Your application team wants to analyze API response time distribution. Which metric type would you recommend?

**Answer**

I would recommend a **Histogram**.

**Explanation**

Histograms measure latency distributions and support percentile calculations.

---

### Scenario 4

**Question**

Users report that API traffic suddenly increased. Which PromQL function would you use to determine the request rate?

**Answer**

I would use:

```promql
rate(http_requests_total[5m])
```

**Explanation**

`rate()` calculates the per-second increase of Counter metrics over a specified time window.

---

### Scenario 5

**Question**

You want to display the average CPU utilization across all Kubernetes worker nodes. Which PromQL function would you use?

**Answer**

I would use:

```promql
avg(...)
```

**Explanation**

Aggregation functions summarize metrics across multiple targets.

---

### Scenario 6

**Question**

Your dashboard displays CPU utilization for every server, but management wants to see only production servers. How would you achieve this?

**Answer**

I would use a label selector such as:

```promql
node_cpu_seconds_total{environment="production"}
```

**Explanation**

Selectors filter metrics using labels, allowing dashboards to display only the desired data.

---

### Scenario 7

**Question**

A developer mistakenly implemented CPU utilization as a Counter metric. Why is this incorrect?

**Answer**

CPU utilization can increase and decrease over time, so it should be implemented as a **Gauge**.

**Explanation**

Counters are only suitable for cumulative values that never decrease.

---

### Scenario 8

**Question**

You need to create a Grafana graph showing request rates for the past one hour. Should you use an Instant Query or a Range Query?

**Answer**

I would use a **Range Query**.

**Explanation**

Graphs require historical data collected over a time interval rather than a single point in time.

---

### Scenario 9

**Question**

Your PromQL query returns metrics from every environment, but you only need staging metrics. How would you modify the query?

**Answer**

I would add a label selector:

```promql
{environment="staging"}
```

**Explanation**

Selectors restrict the query to metrics matching the specified labels.

---

### Scenario 10

**Question**

An alert based on `rate()` is returning incorrect results. What would you verify first?

**Answer**

I would verify that:

- The metric is a **Counter**
- The selected time window is appropriate
- The metric is increasing correctly
- The query syntax is valid

**Explanation**

`rate()` is designed for Counter metrics. Using it with Gauges produces inaccurate or meaningless results.
