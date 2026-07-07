# Azure DevOps Infrastructure Deployment Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is Infrastructure Deployment in Azure DevOps?

**Answer**

Infrastructure Deployment is the process of automatically provisioning, updating, and managing infrastructure resources using Azure DevOps pipelines instead of creating them manually.

Infrastructure can include:

- Resource Groups
- Virtual Machines
- Virtual Networks
- Storage Accounts
- Azure App Services
- Azure Kubernetes Service (AKS)
- Azure SQL Database
- Load Balancers

**Explanation**

Infrastructure Deployment follows the **Infrastructure as Code (IaC)** approach, where infrastructure is defined in code and deployed automatically through CI/CD pipelines.

**Used in Production**

Organizations use Azure DevOps to automate infrastructure provisioning for Development, QA, UAT, and Production environments.

**Common Mistake**

Many candidates think Azure DevOps can only deploy applications. It is also widely used to provision and manage infrastructure.

---

### Question 2

**Question**

What is Infrastructure as Code (IaC), and why is it important?

**Answer**

Infrastructure as Code (IaC) is the practice of defining and managing infrastructure using code instead of manual configuration.

Benefits include:

- Automation
- Consistency
- Version control
- Repeatability
- Faster deployments
- Reduced manual errors
- Easier disaster recovery

**Explanation**

IaC allows infrastructure to be deployed in the same way every time, eliminating configuration drift and improving reliability.

**Used in Production**

Most modern cloud environments use IaC tools such as ARM Templates, Bicep, or Terraform.

**Common Mistake**

Treating infrastructure provisioning as a manual activity instead of automating it.

---

### Question 3

**Question**

What is an ARM Template?

**Answer**

An Azure Resource Manager (ARM) Template is a JSON-based Infrastructure as Code template used to deploy Azure resources.

Example resources include:

- Virtual Machines
- Storage Accounts
- Virtual Networks
- App Services
- SQL Databases

**Explanation**

ARM Templates describe the desired Azure infrastructure declaratively. Azure Resource Manager creates or updates resources to match the template.

**Used in Production**

Many organizations use ARM Templates to standardize Azure infrastructure deployments.

**Common Mistake**

Editing Azure resources manually after deployment instead of updating the ARM Template.

---

### Question 4

**Question**

What is Bicep?

**Answer**

Bicep is Microsoft's domain-specific language (DSL) for deploying Azure resources. It provides a simpler syntax than ARM Templates and compiles into ARM JSON.

Example:

```bicep
resource storage 'Microsoft.Storage/storageAccounts@2023-01-01' = {
  name: 'mystorageaccount'
  location: resourceGroup().location
  sku: {
    name: 'Standard_LRS'
  }
  kind: 'StorageV2'
}
```

**Explanation**

Bicep improves readability and maintainability while using Azure Resource Manager as the deployment engine.

**Used in Production**

Many organizations now prefer Bicep for Azure-native infrastructure deployments.

**Common Mistake**

Assuming Bicep replaces ARM. Bicep is an abstraction that compiles into ARM Templates.

---

### Question 5

**Question**

What is Terraform, and how does it integrate with Azure DevOps?

**Answer**

Terraform is an Infrastructure as Code tool developed by HashiCorp that supports multiple cloud providers.

Azure DevOps integrates with Terraform by:

- Running `terraform init`
- Running `terraform plan`
- Running `terraform apply`
- Managing infrastructure through pipelines

**Explanation**

Unlike ARM and Bicep, Terraform is cloud-agnostic and can provision resources across Azure, AWS, Google Cloud, and other platforms.

**Used in Production**

Organizations with multi-cloud environments commonly use Terraform with Azure DevOps.

**Common Mistake**

Thinking Terraform is Azure-specific. It supports many infrastructure providers.

---

### Question 6

**Question**

What is the difference between ARM Templates, Bicep, and Terraform?

**Answer**

| ARM Templates | Bicep | Terraform |
|--------------|--------|-----------|
| JSON-based | Simplified Azure DSL | Multi-cloud IaC tool |
| Azure only | Azure only | Multi-cloud |
| Verbose syntax | Cleaner syntax | HCL language |
| Managed by Azure Resource Manager | Compiles to ARM Templates | Uses Terraform provider plugins |

**Explanation**

Choose the tool based on project requirements:

- ARM: Existing Azure JSON templates.
- Bicep: Preferred Azure-native deployments.
- Terraform: Multi-cloud infrastructure.

**Used in Production**

Many Azure-only organizations adopt Bicep, while enterprises with multiple cloud providers often standardize on Terraform.

---

### Question 7

**Question**

How can Azure CLI be used for infrastructure deployment?

**Answer**

Azure CLI can create and manage Azure resources using command-line commands.

Example:

```bash
az group create --name DemoRG --location eastus
```

Other common operations include:

- Deploy ARM Templates
- Deploy Bicep files
- Create Resource Groups
- Manage Storage Accounts
- Manage Virtual Machines

**Explanation**

Azure CLI provides imperative commands for infrastructure automation within Azure DevOps pipelines.

**Used in Production**

Azure CLI is commonly used for deployment scripts and automation tasks.

---

### Question 8

**Question**

What are the typical stages of an Infrastructure Deployment Pipeline?

**Answer**

A typical Infrastructure Deployment Pipeline includes:

```text
Source Code
      │
      ▼
Validate Template
      │
      ▼
Authenticate to Azure
      │
      ▼
Deploy Infrastructure
      │
      ▼
Verify Deployment
      │
      ▼
Publish Results
```

**Explanation**

Each stage ensures infrastructure is validated before being deployed.

**Used in Production**

Organizations often include template validation, security scanning, and post-deployment verification.

---

### Question 9

**Question**

Why should infrastructure deployments be automated?

**Answer**

Automation provides:

- Faster deployments
- Consistency
- Reduced manual errors
- Easier rollback
- Version control
- Repeatable deployments
- Improved compliance

**Explanation**

Manual infrastructure changes often lead to configuration drift and inconsistent environments.

**Used in Production**

Most enterprise cloud teams automate infrastructure provisioning through CI/CD pipelines.

---

### Question 10

**Question**

What is the role of an Azure Service Connection in infrastructure deployment?

**Answer**

An Azure Service Connection securely authenticates Azure DevOps with Azure so pipelines can deploy infrastructure.

It is commonly used with:

- ARM Templates
- Bicep
- Terraform
- Azure CLI
- Azure PowerShell

**Explanation**

Without a Service Connection, Azure DevOps cannot authenticate to Azure resources.

**Used in Production**

Every infrastructure deployment pipeline typically uses an ARM Service Connection.

**Common Mistake**

Using personal Azure accounts instead of Service Principals through Service Connections.

---

### Question 11

**Question**

What are some best practices for Infrastructure Deployment?

**Answer**

Best practices include:

- Use Infrastructure as Code.
- Store templates in Git.
- Use Pull Requests for infrastructure changes.
- Validate templates before deployment.
- Separate Development, QA, and Production deployments.
- Use Service Connections with least-privilege access.
- Parameterize environment-specific values.
- Review deployment logs and history.

**Explanation**

Following these practices improves reliability, traceability, and governance while reducing operational risk.

**Used in Production**

Enterprise DevOps teams manage infrastructure using version-controlled IaC and automated deployment pipelines.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

An ARM Template deployment fails with a validation error. How would you troubleshoot it?

**Answer**

Check:

1. ARM Template syntax.
2. Parameter values.
3. Required resources.
4. Azure deployment logs.
5. Azure Resource Manager validation output.
6. Resource naming constraints.

**Explanation**

Validation errors usually occur before Azure attempts to create resources, making them easier to identify and fix.

---

### Scenario 2

**Question**

A Bicep deployment succeeds in Development but fails in Production. What would you investigate?

**Answer**

Verify:

- Parameter files.
- Service Connection.
- Azure RBAC permissions.
- Subscription selection.
- Resource quotas.
- Environment-specific configuration.

**Explanation**

Production deployments often use different subscriptions, permissions, or configuration values than Development.

---

### Scenario 3

**Question**

Your organization uses Azure and AWS. Would you recommend ARM Templates or Terraform?

**Answer**

Recommend **Terraform** because it supports multiple cloud providers while allowing a consistent Infrastructure as Code approach across Azure and AWS.

**Explanation**

Terraform simplifies multi-cloud infrastructure management by using a single workflow and language.

---

### Scenario 4

**Question**

A Terraform deployment fails because the state file is locked. What would you investigate?

**Answer**

Check:

- Whether another Terraform deployment is running.
- Remote backend availability.
- State lock status.
- Storage account or backend connectivity.
- Pipeline execution history.

Release the lock only after confirming no active deployment is using the state.

**Explanation**

Terraform locks the state file to prevent concurrent modifications that could corrupt infrastructure state.

---

### Scenario 5

**Question**

A deployment pipeline creates duplicate Azure resources every time it runs. What could be the reason?

**Answer**

Possible causes include:

- Incorrect resource names.
- Missing unique identifiers where required.
- Imperative Azure CLI scripts creating resources without checking existence.
- Terraform state issues.
- Incorrect deployment mode or logic.

**Explanation**

Infrastructure deployments should be idempotent, meaning repeated executions should not create unintended duplicate resources.

---

### Scenario 6

**Question**

Your manager wants infrastructure changes to follow the same approval process as application deployments. How would you implement this?

**Answer**

Configure:

- Pull Request reviews for IaC code.
- Build validation.
- Environment approvals.
- Production deployment approvals.
- Separate deployment stages for each environment.

**Explanation**

Infrastructure changes can have significant production impact and should follow the same governance as application releases.

---

### Scenario 7

**Question**

A deployment pipeline reports "Authorization Failed" while creating Azure resources. What would you check?

**Answer**

Verify:

- Azure Service Connection.
- Service Principal permissions.
- Azure RBAC role assignments.
- Subscription selection.
- Resource Group permissions.
- Deployment logs.

**Explanation**

Authorization failures indicate that the deployment identity lacks the required permissions.

---

### Scenario 8

**Question**

Your team currently creates Azure resources manually through the Azure Portal. What would you recommend?

**Answer**

Recommend moving to Infrastructure as Code using:

- Bicep (Azure-native)
- ARM Templates
- Terraform

Store the code in Git and deploy through Azure DevOps pipelines.

**Explanation**

IaC improves consistency, traceability, automation, and disaster recovery while reducing manual configuration errors.

---

### Scenario 9

**Question**

A deployment succeeds, but the expected Azure resource is missing. How would you troubleshoot?

**Answer**

Check:

- Deployment logs.
- Template conditions.
- Parameter values.
- Deployment scope.
- Azure Resource Group.
- Deployment outputs.

**Explanation**

Resources may not be created because of conditional logic, incorrect parameters, or deployment targeting the wrong scope.

---

### Scenario 10

**Question**

Your organization wants to review all infrastructure changes before deployment. How would you implement this?

**Answer**

Store infrastructure code in Git and require:

- Feature branches.
- Pull Requests.
- Code reviews.
- Build validation.
- Approval before deployment.

**Explanation**

Version-controlling infrastructure enables collaboration, auditing, and controlled change management.

---

### Scenario 11

**Question**

A production infrastructure deployment accidentally deletes critical resources because of an incorrect Infrastructure as Code change. How could this risk be reduced in the future?

**Answer**

Implement the following practices:

- Validate templates before deployment.
- Review changes through Pull Requests.
- Use deployment previews (such as `terraform plan` or ARM/Bicep validation).
- Test changes in Development and QA before Production.
- Use environment approvals for Production.
- Apply least-privilege access to deployment identities.
- Maintain backups and recovery procedures for critical resources.

**Explanation**

Infrastructure deployments can affect production availability. Validation, review, staged deployments, and approval workflows significantly reduce the risk of destructive changes reaching production.
