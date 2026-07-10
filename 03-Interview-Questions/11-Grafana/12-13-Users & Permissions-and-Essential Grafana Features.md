# Users & Permissions, Essential Grafana Features Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What are Users, Teams, and Roles in Grafana?

**Answer**

- **Users** are individual accounts that can log in to Grafana.
- **Teams** are collections of users used for easier permission management.
- **Roles** define what actions users can perform within Grafana.

The default organization roles are:

- Viewer
- Editor
- Admin

**Explanation**

Grafana uses Role-Based Access Control (RBAC) to ensure users only have the permissions necessary for their responsibilities. Teams simplify permission management by assigning access to multiple users at once.

**Where it is used in Production**

- DevOps teams
- SRE teams
- Infrastructure teams
- Application teams

**Common Mistake**

Many candidates think Teams automatically grant permissions. Permissions must still be assigned to Teams, folders, or dashboards.

---

### Question 2

**Question**

What is the difference between Viewer, Editor, and Admin roles in Grafana?

**Answer**

- **Viewer** – Can only view dashboards.
- **Editor** – Can create and modify dashboards.
- **Admin** – Has full administrative control over users, data sources, dashboards, and settings.

**Explanation**

These predefined roles help organizations enforce least-privilege access while allowing collaboration.

**Where it is used in Production**

Organizations assign roles based on job responsibilities to prevent unauthorized changes.

---

### Question 3

**Question**

What are Teams in Grafana, and why are they useful?

**Answer**

Teams allow administrators to group multiple users and assign permissions collectively instead of configuring access for each user individually.

**Explanation**

Managing permissions through Teams simplifies administration and reduces configuration errors.

**Where it is used in Production**

Large organizations where multiple engineers require identical dashboard access.

---

### Question 4

**Question**

What are Folder Permissions in Grafana?

**Answer**

Folder Permissions control access to all dashboards stored within a folder.

Permissions can be granted to:

- Users
- Teams
- Roles

**Explanation**

Instead of assigning permissions to individual dashboards, administrators manage access at the folder level.

**Where it is used in Production**

- Production dashboards
- Development dashboards
- Team-specific monitoring folders

**Common Mistake**

Candidates often confuse folder permissions with dashboard permissions. Folder permissions apply to every dashboard inside that folder.

---

### Question 5

**Question**

What are Dashboard Permissions?

**Answer**

Dashboard Permissions provide access control for an individual dashboard.

You can specify who can:

- View
- Edit
- Administer

that specific dashboard.

**Explanation**

Dashboard-level permissions provide more granular access than folder-level permissions.

**Where it is used in Production**

Sensitive dashboards that should only be accessible by selected teams.

---

### Question 6

**Question**

What is the Explore feature in Grafana?

**Answer**

Explore is an interactive interface used to query metrics and logs without creating dashboards.

It supports data sources such as:

- Prometheus
- Loki
- Elasticsearch

**Explanation**

Explore is primarily used for troubleshooting and root cause analysis by allowing engineers to test queries quickly.

**Where it is used in Production**

Incident investigation and debugging production issues.

**Common Mistake**

Many candidates believe Explore is only for logs. It supports both metrics and logs.

---

### Question 7

**Question**

What is Dashboard Search in Grafana?

**Answer**

Dashboard Search allows users to quickly locate dashboards by:

- Name
- Folder
- Tags
- Keywords

**Explanation**

As organizations create hundreds of dashboards, search functionality helps engineers find relevant dashboards quickly.

**Where it is used in Production**

Large monitoring environments with numerous dashboards.

---

### Question 8

**Question**

What is the Time Picker in Grafana?

**Answer**

The Time Picker allows users to select the time range displayed on dashboards.

Examples:

- Last 5 minutes
- Last 1 hour
- Last 24 hours
- Last 7 days
- Custom range

**Explanation**

Changing the time range helps analyze both recent incidents and historical trends.

**Where it is used in Production**

Performance analysis and incident investigations.

---

### Question 9

**Question**

What are Refresh Intervals in Grafana?

**Answer**

Refresh Intervals automatically reload dashboard data at regular intervals.

Common intervals include:

- 5 seconds
- 30 seconds
- 1 minute
- 5 minutes

**Explanation**

Automatic refresh ensures dashboards always display current monitoring data.

**Where it is used in Production**

Network Operations Centers (NOC), SRE monitoring, and live production dashboards.

---

### Question 10

**Question**

What are Annotations in Grafana?

**Answer**

Annotations are markers displayed on graphs that indicate important events such as:

- Deployments
- Incidents
- Restarts
- Configuration changes

**Explanation**

Annotations help correlate monitoring data with operational events.

**Where it is used in Production**

Incident analysis and deployment tracking.

**Common Mistake**

Candidates often think annotations modify metrics. They only add contextual information to visualizations.

---

### Question 11

**Question**

Why is Role-Based Access Control (RBAC) important in Grafana?

**Answer**

RBAC restricts access based on user responsibilities, improving security and preventing unauthorized changes.

**Explanation**

Proper access control reduces operational risks while allowing collaboration across multiple teams.

**Where it is used in Production**

Enterprise monitoring environments with multiple DevOps, SRE, and application teams.

---

### Question 12

**Question**

How do Folder Permissions and Dashboard Permissions work together?

**Answer**

Folder Permissions define access for all dashboards within a folder, while Dashboard Permissions can override or provide more granular control for individual dashboards.

**Explanation**

Organizations typically use Folder Permissions for team-wide access and Dashboard Permissions for exceptions.

**Where it is used in Production**

Managing both shared dashboards and restricted dashboards efficiently.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

A developer can log in to Grafana but cannot edit dashboards. What would you check?

**Answer**

I would verify:

- User role
- Team membership
- Folder permissions
- Dashboard permissions

**Explanation**

Editors require both the appropriate role and sufficient permissions on the dashboard or folder.

---

### Scenario 2

**Question**

Your organization has separate DevOps, Development, and QA teams. How would you manage dashboard access?

**Answer**

I would:

- Create separate Teams.
- Organize dashboards into folders.
- Assign Folder Permissions to each Team.
- Use Dashboard Permissions only when exceptions are needed.

**Explanation**

This approach simplifies permission management and follows security best practices.

---

### Scenario 3

**Question**

A production dashboard should only be visible to the SRE team. How would you configure this?

**Answer**

I would:

- Place the dashboard in a secured folder.
- Grant Folder Permissions only to the SRE Team.
- Remove access for other users or teams.

**Explanation**

Folder-level permissions provide centralized access management for sensitive dashboards.

---

### Scenario 4

**Question**

A user reports that a dashboard displays outdated metrics. What would you investigate?

**Answer**

I would check:

- Dashboard Refresh Interval
- Time Picker settings
- Data source connectivity
- Query execution
- Prometheus scrape status

**Explanation**

Outdated dashboards are often caused by incorrect refresh settings or stale data from the monitoring system.

---

### Scenario 5

**Question**

During a production incident, you need to investigate logs quickly without modifying any dashboard. Which Grafana feature would you use?

**Answer**

I would use **Explore**.

**Explanation**

Explore allows engineers to run ad hoc metric and log queries for troubleshooting without affecting existing dashboards.

---

### Scenario 6

**Question**

A manager asks you to identify exactly when an application deployment caused increased error rates. Which Grafana feature would help?

**Answer**

I would use **Annotations**.

**Explanation**

Annotations display deployment events alongside monitoring graphs, making it easy to correlate operational changes with system behavior.

---

### Scenario 7

**Question**

Your Grafana environment contains hundreds of dashboards. A developer cannot locate the required dashboard. What feature would you recommend?

**Answer**

I would recommend using **Dashboard Search** with dashboard names, tags, or folder filters.

**Explanation**

Dashboard Search significantly reduces the time required to locate monitoring dashboards.

---

### Scenario 8

**Question**

Your NOC team wants dashboards to update automatically every 15 seconds. How would you configure this?

**Answer**

I would configure the dashboard's **Refresh Interval** to 15 seconds.

**Explanation**

Automatic refresh ensures operators always view the latest monitoring data without manually reloading dashboards.

---

### Scenario 9

**Question**

An engineer accidentally modified a production dashboard. How could you reduce the risk of similar incidents?

**Answer**

I would:

- Assign Viewer access to most users.
- Restrict Editor access to authorized engineers.
- Use Team-based permissions.
- Protect production folders with Folder Permissions.

**Explanation**

Following the principle of least privilege reduces accidental modifications.

---

### Scenario 10

**Question**

A DevOps engineer wants to compare application performance before and after yesterday's deployment. Which Grafana features would you use?

**Answer**

I would use:

- **Time Picker** to select the relevant time window.
- **Annotations** to identify the deployment time.
- **Explore** for additional investigation if needed.

**Explanation**

Combining these features allows engineers to correlate deployments with performance changes and quickly investigate production issues.
