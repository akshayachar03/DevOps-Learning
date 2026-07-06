# Governance & Cost Management

## Definition

- Governance & Cost Management in Azure helps organizations control access, enforce standards, organize resources, and optimize cloud spending.
- It ensures Azure resources are secure, compliant, and cost-effective.
- Azure provides services like Management Groups, Azure Policy, Azure Cost Management, Azure Advisor, and Resource Tags.

---

## Why is it used?

- Control Azure resources.
- Enforce organizational standards.
- Optimize cloud costs.
- Improve compliance.
- Prevent accidental resource changes.
- Monitor cloud spending.

---

## Key Features

- Resource organization.
- Policy enforcement.
- Cost monitoring.
- Budget management.
- Resource tagging.
- Security recommendations.
- Cost optimization recommendations.

---

## Advantages

- Better governance.
- Reduced cloud costs.
- Improved compliance.
- Easier resource management.
- Better visibility into spending.

---

## Disadvantages

- Requires planning.
- Large organizations need governance strategies.
- Poor tagging affects reporting.

---

## Components

- Management Groups
- Azure Policy
- Resource Locks
- Tags
- Budgets
- Cost Analysis
- Azure Advisor
- Reservations
- Savings Plans

---

## Workflow

```text
Azure Resources
        ↓
Governance Services
        ↓
Policies + Tags + Locks
        ↓
Cost Management
        ↓
Reports & Recommendations
```

---

## Real-world Example

A company organizes subscriptions using Management Groups, enforces security policies with Azure Policy, applies tags for cost tracking, and uses Budgets to prevent overspending.

---

## Interview Tip

"Azure Governance ensures resources follow organizational standards, while Cost Management helps optimize cloud spending."

---

## Quick Revision

- Governance controls resources.
- Cost Management controls spending.
- Azure Policy enforces rules.
- Tags organize resources.
- Azure Advisor provides recommendations.
- Budgets prevent overspending.

---

## Important Interview Questions

1. What is Azure Governance?
2. Why is Cost Management important?
3. Which Azure services support governance?
4. How does Azure reduce cloud costs?
5. What is the purpose of Azure Advisor?

---

# Management Groups

## Definition

- Management Groups are containers used to organize multiple Azure subscriptions.
- They allow administrators to apply governance, policies, and RBAC across many subscriptions.

---

## Why is it used?

- Organize subscriptions.
- Apply policies centrally.
- Manage RBAC at scale.
- Simplify administration.
- Support enterprise governance.

---

## Key Features

- Hierarchical organization.
- Policy inheritance.
- RBAC inheritance.
- Supports multiple subscriptions.
- Centralized management.

---

## Advantages

- Easy enterprise management.
- Reduced administrative effort.
- Consistent governance.
- Scalable.

---

## Disadvantages

- Requires proper planning.
- Large hierarchies can become complex.

---

## Hierarchy

```text
Management Group
      ↓
Subscription
      ↓
Resource Group
      ↓
Resource
```

---

## Real-world Example

A company creates separate subscriptions for Development, Testing, and Production, all managed under one Management Group.

---

## Interview Tip

"Management Groups organize subscriptions and allow governance policies to be applied across the organization."

---

## Quick Revision

- Organizes subscriptions.
- Supports inheritance.
- Enterprise governance.
- Centralized management.
- Above subscriptions.

---

## Important Interview Questions

1. What is a Management Group?
2. Where do Management Groups fit in Azure hierarchy?
3. Why are Management Groups used?
4. Can RBAC be applied at the Management Group level?
5. Do policies inherit to subscriptions?

---

# Azure Policy

## Definition

- Azure Policy is a governance service that enforces organizational rules and evaluates Azure resources for compliance.
- It can allow, deny, audit, or automatically remediate resource configurations.

---

## Why is it used?

- Enforce standards.
- Prevent non-compliant deployments.
- Improve governance.
- Meet compliance requirements.
- Standardize Azure environments.

---

## Key Features

- Built-in policies.
- Custom policies.
- Policy initiatives.
- Compliance dashboard.
- Automatic remediation.
- Deny and Audit effects.

---

## Advantages

- Prevents misconfiguration.
- Improves compliance.
- Easy governance.
- Centralized policy management.

---

## Disadvantages

- Incorrect policies may block valid deployments.
- Requires planning.

---

## Policy Effects

| Effect | Description |
|---------|-------------|
| Deny | Blocks deployment |
| Audit | Reports non-compliance |
| Append | Adds properties during deployment |
| Modify | Updates resource properties |
| DeployIfNotExists | Deploys required resources automatically |
| AuditIfNotExists | Reports missing configurations |

---

## Workflow

```text
Deploy Resource
        ↓
Azure Policy Evaluation
        ↓
Allow / Deny / Audit
```

---

## Real-world Example

An organization creates a policy allowing Virtual Machines only in approved Azure regions.

---

## Interview Tip

"Azure Policy enforces governance rules, while RBAC controls who can perform actions."

---

## Quick Revision

- Governance service.
- Built-in policies.
- Custom policies.
- Compliance reporting.
- Supports remediation.

---

## Important Interview Questions

1. What is Azure Policy?
2. What are Policy Effects?
3. What is the difference between Policy and RBAC?
4. Can Azure Policy block deployments?
5. What is a Policy Initiative?

---

# Resource Locks

## Definition

- Resource Locks prevent accidental deletion or modification of Azure resources.
- They provide an additional layer of protection beyond RBAC.

---

## Why is it used?

- Protect production resources.
- Prevent accidental deletion.
- Prevent unauthorized changes.
- Improve governance.

---

## Key Features

- CanNotDelete lock.
- ReadOnly lock.
- Can be applied at multiple scopes.
- Inherited by child resources.

---

## Advantages

- Protects important resources.
- Easy to configure.
- Prevents human error.

---

## Disadvantages

- May block legitimate administrative changes.
- Locks must be removed before some operations.

---

## Types

| Lock | Description |
|------|-------------|
| CanNotDelete | Prevents deletion |
| ReadOnly | Prevents deletion and modification |

---

## Workflow

```text
Resource
      ↓
Apply Lock
      ↓
Delete/Modify Attempt
      ↓
Operation Blocked
```

---

## Real-world Example

A production SQL Database has a CanNotDelete lock to prevent accidental removal.

---

## Interview Tip

"Resource Locks protect Azure resources even if users have sufficient RBAC permissions."

---

## Quick Revision

- CanNotDelete.
- ReadOnly.
- Prevent accidental deletion.
- Inherited.
- Extra protection.

---

## Important Interview Questions

1. What are Resource Locks?
2. What are the two lock types?
3. How are Resource Locks different from RBAC?
4. Can locks be inherited?
5. When should Resource Locks be used?

---

# Tags

## Definition

- Tags are name-value pairs added to Azure resources for organization, management, automation, and cost reporting.
- Tags do not affect resource functionality.

---

## Why is it used?

- Organize resources.
- Track costs.
- Simplify automation.
- Improve reporting.
- Identify resource ownership.

---

## Key Features

- Name-value pairs.
- Searchable.
- Used in billing reports.
- Supports automation.
- Easy resource organization.

---

## Common Tags

| Tag | Example |
|-----|---------|
| Environment | Production |
| Owner | DevOps Team |
| Department | Finance |
| Project | E-Commerce |
| CostCenter | IT001 |

---

## Advantages

- Better reporting.
- Easier management.
- Cost tracking.
- Automation support.

---

## Disadvantages

- Requires consistent naming.
- Missing tags reduce reporting accuracy.

---

## Workflow

```text
Create Resource
      ↓
Apply Tags
      ↓
Reports & Cost Tracking
```

---

## Real-world Example

A company tags every resource with Department=Finance and Environment=Production to generate department-wise cost reports.

---

## Interview Tip

"Tags organize Azure resources and improve cost tracking without affecting functionality."

---

## Quick Revision

- Name-value pairs.
- Cost reporting.
- Resource organization.
- Automation.
- No impact on performance.

---

## Important Interview Questions

1. What are Azure Tags?
2. Why are Tags important?
3. Can Tags affect billing?
4. What are common Tag examples?
5. How do Tags improve governance?

---

# Budgets

## Definition

- Budgets allow organizations to define spending limits for Azure subscriptions or resource groups.
- Notifications are generated when spending reaches predefined thresholds.

---

## Why is it used?

- Prevent overspending.
- Monitor cloud costs.
- Improve financial planning.
- Control departmental budgets.

---

## Key Features

- Monthly budgets.
- Quarterly budgets.
- Threshold alerts.
- Integration with Action Groups.

---

## Advantages

- Cost control.
- Early notifications.
- Better financial planning.

---

## Disadvantages

- Budgets do not stop resource usage automatically.
- Require regular review.

---

## Workflow

```text
Create Budget
      ↓
Monitor Spending
      ↓
Threshold Reached
      ↓
Alert Sent
```

---

## Real-world Example

A company creates a monthly budget of $5,000 and receives alerts at 50%, 80%, and 100% usage.

---

## Interview Tip

"Budgets notify administrators when Azure spending reaches predefined limits."

---

## Quick Revision

- Spending limits.
- Alerts.
- Monthly budgets.
- Resource Group support.
- Subscription support.

---

## Important Interview Questions

1. What is an Azure Budget?
2. Does a Budget stop Azure resources?
3. What happens when the budget threshold is reached?
4. Where can Budgets be created?
5. How do Budgets reduce costs?

---

# Cost Analysis

## Definition

- Cost Analysis is a feature of Azure Cost Management that helps visualize, analyze, and understand Azure spending.

---

## Why is it used?

- Analyze cloud costs.
- Identify expensive resources.
- Forecast spending.
- Optimize cloud usage.

---

## Key Features

- Interactive reports.
- Daily spending.
- Monthly trends.
- Cost breakdown by service.
- Filtering and grouping.

---

## Advantages

- Better visibility.
- Spending trends.
- Resource-level cost analysis.
- Cost optimization.

---

## Disadvantages

- Historical data only.
- Requires tagging for detailed reporting.

---

## Workflow

```text
Azure Usage
      ↓
Cost Analysis
      ↓
Reports
      ↓
Optimization
```

---

## Real-world Example

A company discovers that idle Virtual Machines consume 30% of monthly costs and shuts them down during non-working hours.

---

## Interview Tip

"Cost Analysis helps identify where Azure money is being spent."

---

## Quick Revision

- Spending reports.
- Cost trends.
- Forecasting.
- Resource-level costs.
- Optimization.

---

## Important Interview Questions

1. What is Cost Analysis?
2. What information does Cost Analysis provide?
3. How does Cost Analysis reduce costs?
4. Can Cost Analysis forecast spending?
5. Why are Tags useful in Cost Analysis?

---

# Cost Alerts

## Definition

- Cost Alerts notify administrators when Azure spending exceeds predefined thresholds or budgets.

---

## Why is it used?

- Prevent overspending.
- Improve cost visibility.
- Notify finance teams.
- Track subscription spending.

---

## Key Features

- Budget alerts.
- Email notifications.
- Action Group integration.
- Threshold-based alerts.

---

## Advantages

- Early warning.
- Better budget control.
- Supports automation.

---

## Disadvantages

- Does not automatically stop resources.
- Depends on accurate budget configuration.

---

## Workflow

```text
Budget Threshold
       ↓
Cost Alert
       ↓
Email / Action Group
```

---

## Real-world Example

When monthly spending reaches 90%, Azure sends an alert to the Cloud Operations team.

---

## Interview Tip

"Cost Alerts notify administrators before cloud spending exceeds the planned budget."

---

## Quick Revision

- Budget thresholds.
- Email notifications.
- Action Groups.
- Spending alerts.

---

## Important Interview Questions

1. What are Cost Alerts?
2. How are Cost Alerts different from Budgets?
3. When are Cost Alerts triggered?
4. Can Action Groups be used?
5. Do Cost Alerts stop Azure resources?

---

# Azure Advisor

## Definition

- Azure Advisor is a recommendation service that analyzes Azure resources and suggests improvements.
- Recommendations cover cost, performance, reliability, security, and operational excellence.

---

## Why is it used?

- Reduce cloud costs.
- Improve performance.
- Increase security.
- Improve availability.
- Optimize Azure resources.

---

## Key Features

- Cost recommendations.
- Performance recommendations.
- Security recommendations.
- Reliability recommendations.
- Operational Excellence recommendations.

---

## Advantages

- Free recommendations.
- Easy optimization.
- Improves cloud efficiency.
- Supports best practices.

---

## Disadvantages

- Recommendations require administrator review.
- Not all recommendations apply to every workload.

---

## Categories

| Category | Purpose |
|----------|----------|
| Cost | Reduce spending |
| Security | Improve security |
| Reliability | Increase availability |
| Performance | Optimize performance |
| Operational Excellence | Improve operational efficiency |

---

## Workflow

```text
Azure Resources
      ↓
Azure Advisor
      ↓
Analysis
      ↓
Recommendations
```

---

## Real-world Example

Azure Advisor recommends resizing an underutilized Virtual Machine from D4s_v5 to D2s_v5, reducing monthly costs.

---

## Interview Tip

"Azure Advisor provides best-practice recommendations to improve cost, security, reliability, performance, and operational excellence."

---

## Quick Revision

- Free service.
- Cost optimization.
- Performance improvement.
- Security recommendations.
- Reliability recommendations.

---

## Important Interview Questions

1. What is Azure Advisor?
2. What recommendation categories does Azure Advisor provide?
3. How does Azure Advisor reduce costs?
4. Is Azure Advisor free?
5. Does Azure Advisor make changes automatically?

---

# Reservations & Savings Plans

## Definition

- Azure Reservations and Azure Savings Plans reduce Azure costs by committing to long-term usage.
- Reservations apply to specific resource types, while Savings Plans provide more flexibility across eligible compute services.

---

## Why is it used?

- Reduce cloud costs.
- Optimize long-term workloads.
- Predict infrastructure expenses.
- Improve budgeting.

---

## Key Features

### Azure Reservations

- 1-year or 3-year commitment.
- Discounts on reserved resources.
- Best for predictable workloads.

### Azure Savings Plan

- Commit to an hourly spend.
- Flexible across eligible compute resources.
- Automatically applies discounts.

---

## Advantages

- Significant cost savings.
- Predictable billing.
- No infrastructure changes.
- Easy cost optimization.

---

## Disadvantages

- Long-term commitment.
- Less suitable for unpredictable workloads.

---

## Comparison

| Feature | Reservations | Savings Plan |
|----------|--------------|--------------|
| Commitment | Resource-specific | Hourly spending commitment |
| Flexibility | Lower | Higher |
| Best For | Stable workloads | Changing workloads |
| Duration | 1 or 3 Years | 1 or 3 Years |
| Discount | Higher for specific resources | Broad discounts across eligible compute |

---

## Workflow

```text
Analyze Usage
      ↓
Purchase Reservation
or Savings Plan
      ↓
Azure Applies Discount
```

---

## Real-world Example

A company runs the same production Virtual Machines 24×7 for several years. It purchases a 3-year Reserved VM Instance and reduces compute costs significantly.

---

## Interview Tip

"Reservations are ideal for predictable workloads, while Savings Plans provide flexible discounts across eligible compute services."

---

## Quick Revision

- Reservations reduce costs.
- Savings Plans are more flexible.
- 1-year or 3-year commitment.
- Best for long-running workloads.
- Improve cloud cost optimization.

---

## Important Interview Questions

1. What are Azure Reservations?
2. What is an Azure Savings Plan?
3. What is the difference between Reservations and Savings Plans?
4. When should Reservations be used?
5. How do Reservations reduce Azure costs?
