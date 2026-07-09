# Terraform Core Commands & Data Sources Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is the purpose of the `terraform init` command?

**Answer**

`terraform init` initializes a Terraform working directory by downloading required providers, configuring the backend, and installing modules.

```bash
terraform init
```

**Explanation**

This is the first command executed in any Terraform project. It prepares the working directory before validation, planning, or deployment.

It performs the following tasks:

- Downloads provider plugins
- Configures the backend
- Downloads modules
- Creates the `.terraform` directory

**Used in Production**

- Starting new Terraform projects
- After changing providers
- After modifying the backend configuration
- Before running CI/CD pipelines

**Common Mistake**

Attempting to run `terraform plan` or `terraform apply` before running `terraform init`.

---

### Question 2

**Question**

What does the `terraform validate` command do?

**Answer**

`terraform validate` checks whether Terraform configuration files are syntactically correct and internally consistent.

```bash
terraform validate
```

**Explanation**

It verifies:

- HCL syntax
- Required arguments
- Resource references
- Variable declarations

It does **not** connect to the cloud provider or create infrastructure.

**Used in Production**

Executed in CI/CD pipelines before deployment to catch configuration errors early.

**Common Mistake**

Assuming `terraform validate` checks cloud resources. It only validates the configuration.

---

### Question 3

**Question**

What is the purpose of the `terraform fmt` command?

**Answer**

`terraform fmt` automatically formats Terraform configuration files according to HashiCorp's recommended style.

```bash
terraform fmt
```

**Explanation**

It:

- Aligns indentation
- Standardizes spacing
- Improves readability
- Ensures consistent formatting across teams

**Used in Production**

Often executed before committing code to Git repositories.

**Common Mistake**

Ignoring formatting standards, leading to inconsistent code reviews.

---

### Question 4

**Question**

What does the `terraform plan` command do?

**Answer**

`terraform plan` creates an execution plan showing what Terraform will create, update, or destroy without making any changes.

```bash
terraform plan
```

**Explanation**

Terraform compares:

- Current configuration
- Current state
- Existing infrastructure

It then displays the proposed changes.

Example output:

```
+ Create
~ Update
- Destroy
```

**Used in Production**

Mandatory review step before applying infrastructure changes.

**Common Mistake**

Skipping `terraform plan` and directly running `terraform apply`, increasing the risk of unintended changes.

---

### Question 5

**Question**

What is the purpose of the `terraform apply` command?

**Answer**

`terraform apply` executes the changes identified in the execution plan and provisions or updates infrastructure.

```bash
terraform apply
```

**Explanation**

Terraform:

1. Generates an execution plan.
2. Requests confirmation (unless `-auto-approve` is used).
3. Creates, updates, or deletes resources.
4. Updates the state file.

**Used in Production**

Deploying infrastructure to Development, QA, and Production environments.

**Common Mistake**

Using `-auto-approve` in production without proper review or approvals.

---

### Question 6

**Question**

What does the `terraform destroy` command do?

**Answer**

`terraform destroy` removes all infrastructure managed by the current Terraform configuration.

```bash
terraform destroy
```

**Explanation**

Terraform:

- Identifies managed resources
- Deletes them in dependency order
- Updates the state file

**Used in Production**

- Removing test environments
- Cleaning up temporary infrastructure
- Cost optimization

**Common Mistake**

Running `terraform destroy` in the wrong environment without verifying the workspace or backend.

---

### Question 7

**Question**

What is the purpose of the `terraform show` command?

**Answer**

`terraform show` displays detailed information about the current Terraform state or a saved execution plan.

```bash
terraform show
```

**Explanation**

It provides information such as:

- Resource attributes
- Resource IDs
- Configuration details
- State contents

**Used in Production**

Troubleshooting deployments and inspecting managed resources.

---

### Question 8

**Question**

What does the `terraform output` command do?

**Answer**

`terraform output` displays values defined in Terraform output blocks.

```bash
terraform output
```

Example:

```hcl
output "vm_ip" {
  value = azurerm_public_ip.vm.ip_address
}
```

Output:

```
vm_ip = 20.50.100.10
```

**Explanation**

Outputs expose useful deployment information without manually querying the cloud.

**Used in Production**

CI/CD pipelines, deployment scripts, and infrastructure automation.

**Common Mistake**

Forgetting to define outputs and manually retrieving resource information.

---

### Question 9

**Question**

What is a Data Source in Terraform?

**Answer**

A Data Source allows Terraform to read information about existing infrastructure without creating or managing it.

Example:

```hcl
data "azurerm_resource_group" "rg" {
  name = "production-rg"
}
```

**Explanation**

Unlike resources, data sources only retrieve existing information.

**Used in Production**

- Existing Resource Groups
- Existing Virtual Networks
- Existing Images
- Existing Storage Accounts

**Common Mistake**

Confusing a data source with a resource block.

---

### Question 10

**Question**

What is the purpose of the `data` block?

**Answer**

The `data` block retrieves information from existing infrastructure.

Example:

```hcl
data "aws_vpc" "default" {
  default = true
}
```

**Explanation**

Terraform reads the existing resource and makes its attributes available for use elsewhere in the configuration.

**Used in Production**

Integrating new infrastructure with existing cloud resources.

---

### Question 11

**Question**

When should you use a Data Source instead of a Resource?

**Answer**

Use a **Resource** when Terraform should create and manage infrastructure.

Use a **Data Source** when the infrastructure already exists and only needs to be referenced.

**Explanation**

| Resource | Data Source |
|----------|-------------|
| Creates infrastructure | Reads existing infrastructure |
| Managed by Terraform | Not managed by Terraform |
| Changes state | Read-only |

**Used in Production**

Reading existing VNets, Subnets, Resource Groups, IAM Roles, AMIs, and DNS Zones.

**Common Mistake**

Attempting to recreate existing infrastructure instead of referencing it.

---

### Question 12

**Question**

How do Resource References work in Terraform?

**Answer**

Resource references allow one resource to use attributes from another resource.

Example:

```hcl
resource_group_name = azurerm_resource_group.rg.name
```

General syntax:

```hcl
resource_type.resource_name.attribute
```

**Explanation**

References:

- Eliminate hardcoded values
- Create automatic dependencies
- Improve maintainability
- Reduce configuration errors

**Used in Production**

Connecting virtual machines to resource groups, subnets, storage accounts, and load balancers.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

A teammate attempts to deploy infrastructure immediately after cloning the repository and receives provider-related errors. What is the likely cause?

**Answer**

They did not run:

```bash
terraform init
```

**Explanation**

`terraform init` downloads providers, configures the backend, and prepares the working directory before any Terraform operations.

---

### Scenario 2

**Question**

Your CI pipeline should detect Terraform syntax errors before deployment. Which command would you use?

**Answer**

```bash
terraform validate
```

**Explanation**

It checks configuration correctness without contacting the cloud provider, making it ideal for early validation.

---

### Scenario 3

**Question**

Your manager wants to review infrastructure changes before deployment. Which Terraform command should be included in the approval process?

**Answer**

```bash
terraform plan
```

**Explanation**

The execution plan shows all proposed changes, allowing reviewers to verify them before applying.

---

### Scenario 4

**Question**

A Terraform deployment accidentally creates resources in the wrong environment. How could this have been prevented?

**Answer**

Review the output of:

```bash
terraform plan
```

before executing:

```bash
terraform apply
```

**Explanation**

The plan would reveal unexpected resource creations or modifications before they occur.

---

### Scenario 5

**Question**

Your team has an existing Azure Resource Group created manually. A new Terraform project must deploy resources into it. What should you do?

**Answer**

Use a data source:

```hcl
data "azurerm_resource_group" "rg" {
  name = "production-rg"
}
```

**Explanation**

The Resource Group already exists, so Terraform should reference it rather than attempt to create another one.

---

### Scenario 6

**Question**

A deployment script requires the public IP address of a newly created VM after `terraform apply`. How can Terraform provide it?

**Answer**

Create an output block:

```hcl
output "vm_public_ip" {
  value = azurerm_public_ip.vm.ip_address
}
```

Retrieve it with:

```bash
terraform output
```

**Explanation**

Outputs expose resource information for automation and CI/CD pipelines.

---

### Scenario 7

**Question**

A developer manually copies a Resource Group name into multiple resource blocks. What would you recommend?

**Answer**

Use resource references:

```hcl
azurerm_resource_group.rg.name
```

**Explanation**

References eliminate hardcoded values, create automatic dependencies, and improve maintainability.

---

### Scenario 8

**Question**

Your Terraform files have inconsistent indentation and formatting across the team. Which command should be added to the development workflow?

**Answer**

```bash
terraform fmt
```

**Explanation**

Consistent formatting improves readability, code reviews, and collaboration.

---

### Scenario 9

**Question**

A temporary test environment is no longer needed, and the organization wants to avoid unnecessary cloud costs. Which Terraform command should be used?

**Answer**

```bash
terraform destroy
```

**Explanation**

It safely removes all infrastructure managed by the current Terraform configuration.

---

### Scenario 10

**Question**

A DevOps engineer accidentally defines a new Resource Group resource even though it already exists in Azure. What is the correct approach?

**Answer**

Replace the resource block with a data source and reference the existing Resource Group.

**Explanation**

Data sources are intended for reading existing infrastructure, while resource blocks are used to create and manage new infrastructure. Using the correct approach avoids deployment failures and duplicate resources.
