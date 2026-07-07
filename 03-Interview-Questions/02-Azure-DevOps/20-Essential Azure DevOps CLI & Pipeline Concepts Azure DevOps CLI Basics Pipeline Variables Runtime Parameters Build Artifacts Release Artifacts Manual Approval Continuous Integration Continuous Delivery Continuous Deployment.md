# Azure DevOps CLI & Essential Pipeline Concepts Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is the Azure DevOps CLI?

**Answer**

The Azure DevOps CLI is a command-line extension for the Azure CLI that allows you to manage Azure DevOps resources directly from the terminal.

Common operations include:

- Create Projects
- Create Repositories
- Manage Pipelines
- Manage Variable Groups
- Manage Work Items
- Manage Pull Requests
- Manage Service Connections
- Manage Users

Example:

```bash
az extension add --name azure-devops
```

**Explanation**

The Azure DevOps CLI helps automate Azure DevOps administration and can be integrated into scripts and CI/CD pipelines.

**Used in Production**

DevOps engineers use the CLI to automate repetitive Azure DevOps administration tasks.

**Common Mistake**

Many candidates confuse the Azure CLI with the Azure DevOps CLI. The Azure CLI manages Azure resources, while the Azure DevOps CLI manages Azure DevOps services.

---

### Question 2

**Question**

Why is the Azure DevOps CLI useful?

**Answer**

Benefits include:

- Automation
- Scriptable administration
- Faster project setup
- Reduced manual effort
- Repeatable operations
- CI/CD integration

**Explanation**

The CLI eliminates repetitive portal-based tasks and enables infrastructure and DevOps processes to be automated.

**Used in Production**

Organizations use the Azure DevOps CLI to automate project creation, repository management, and pipeline administration.

---

### Question 3

**Question**

What are Pipeline Variables?

**Answer**

Pipeline Variables are reusable key-value pairs used throughout Azure DevOps pipelines.

Example:

```yaml
variables:
  Environment: Production
```

Variables commonly store:

- Environment names
- Build configurations
- Application versions
- Resource names
- URLs

**Explanation**

Variables improve maintainability by replacing hardcoded values.

**Used in Production**

Nearly every production pipeline uses variables for configuration management.

---

### Question 4

**Question**

What are Runtime Parameters?

**Answer**

Runtime Parameters allow users to provide values when manually starting a pipeline.

Example:

```yaml
parameters:
- name: environment
  type: string
  default: Development
```

Possible values:

- Development
- QA
- Production

**Explanation**

Parameters are evaluated before pipeline execution and enable reusable pipelines without modifying YAML.

**Used in Production**

Organizations commonly use Runtime Parameters to choose deployment environments or deployment options.

**Common Mistake**

Confusing Runtime Parameters with Pipeline Variables. Parameters are evaluated before execution, while variables are available during execution and can change at runtime.

---

### Question 5

**Question**

What are Build Artifacts?

**Answer**

Build Artifacts are the output produced by a successful Build Pipeline.

Examples include:

- ZIP files
- DLL files
- JAR files
- WAR files
- Docker images
- Static website files

Artifacts are published after the build completes successfully.

**Explanation**

Build Artifacts allow deployments to use the exact output produced during the build stage.

**Used in Production**

Every deployment should use published Build Artifacts rather than rebuilding the application.

---

### Question 6

**Question**

What are Release Artifacts?

**Answer**

Release Artifacts are Build Artifacts consumed by deployment stages or Release Pipelines.

Workflow:

```text
Build Pipeline
      │
      ▼
Publish Artifact
      │
      ▼
Release Pipeline
      │
      ▼
Deploy Application
```

**Explanation**

The deployment pipeline downloads Build Artifacts and deploys them without recompiling the application.

**Used in Production**

This approach ensures consistent deployments across Development, QA, and Production.

---

### Question 7

**Question**

What is Manual Approval in Azure DevOps?

**Answer**

Manual Approval requires an authorized user to approve a deployment before the pipeline continues.

Typical approval flow:

```text
Development
      │
      ▼
QA
      │
      ▼
Manager Approval
      │
      ▼
Production
```

**Explanation**

Manual approvals prevent unauthorized or accidental deployments to critical environments.

**Used in Production**

Production deployments commonly require approval from Release Managers, Product Owners, or DevOps Engineers.

**Common Mistake**

Allowing production deployments without any approval process.

---

### Question 8

**Question**

What is Continuous Integration (CI)?

**Answer**

Continuous Integration (CI) is the practice of automatically building and testing code whenever developers commit changes.

Typical CI workflow:

```text
Developer Commit
        │
        ▼
Build
        │
        ▼
Run Tests
        │
        ▼
Publish Artifacts
```

Benefits include:

- Early bug detection
- Faster feedback
- Improved code quality
- Reduced integration issues

**Explanation**

CI ensures that code changes are validated automatically before they are merged or deployed.

**Used in Production**

Most software development teams implement CI for every repository.

---

### Question 9

**Question**

What is Continuous Delivery (CD)?

**Answer**

Continuous Delivery automatically prepares applications for deployment after a successful build.

Typical workflow:

```text
Build
      │
      ▼
Test
      │
      ▼
Publish Artifact
      │
      ▼
Ready for Deployment
```

Deployment to Production usually requires manual approval.

**Explanation**

Continuous Delivery ensures the application is always in a deployable state while allowing controlled production releases.

**Used in Production**

Many enterprise organizations use Continuous Delivery for production environments.

---

### Question 10

**Question**

What is Continuous Deployment?

**Answer**

Continuous Deployment automatically deploys every successful build to the target environment without manual intervention.

Workflow:

```text
Commit
      │
      ▼
Build
      │
      ▼
Test
      │
      ▼
Deploy Automatically
```

**Explanation**

Unlike Continuous Delivery, Continuous Deployment does not require manual approval before deployment.

**Used in Production**

Continuous Deployment is commonly used for Development and QA environments. Production deployments often include approval gates depending on organizational requirements.

**Common Mistake**

Confusing Continuous Delivery with Continuous Deployment. Continuous Delivery prepares software for release, while Continuous Deployment automatically performs the release.

---

### Question 11

**Question**

What is the difference between Continuous Integration, Continuous Delivery, and Continuous Deployment?

**Answer**

| Continuous Integration | Continuous Delivery | Continuous Deployment |
|------------------------|--------------------|----------------------|
| Automatically builds and tests code | Automatically prepares releases | Automatically deploys releases |
| Validates every code change | Usually includes manual approval before Production | Deploys without manual approval |
| Produces Build Artifacts | Produces Release Artifacts | Deploys to target environment automatically |

**Explanation**

These practices build upon each other to create a complete CI/CD workflow.

**Used in Production**

Many organizations use:

- CI for every repository.
- Continuous Delivery for Production.
- Continuous Deployment for Development or QA environments.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

Your Build Pipeline completes successfully, but the deployment pipeline cannot find the application package. What would you investigate?

**Answer**

Check:

1. Publish Build Artifacts task.
2. Artifact name.
3. Download Artifacts task.
4. Build completion.
5. Artifact retention settings.
6. Pipeline permissions.

**Explanation**

Deployments rely on published artifacts. Missing or incorrectly referenced artifacts prevent successful deployments.

---

### Scenario 2

**Question**

Your organization wants developers to choose the deployment environment when manually starting a pipeline. How would you implement this?

**Answer**

Use **Runtime Parameters** to allow users to select the environment (for example, Development, QA, or Production) before pipeline execution.

**Explanation**

Runtime Parameters provide flexibility while allowing a single pipeline definition to support multiple deployment targets.

---

### Scenario 3

**Question**

A Production deployment occurs automatically immediately after a successful build, but company policy requires manager approval. How would you fix this?

**Answer**

Configure:

- Azure DevOps Environment approvals.
- Manual approval checks.
- Deployment stages requiring authorized approvers before Production.

**Explanation**

Manual approvals provide governance and reduce the risk of unintended production deployments.

---

### Scenario 4

**Question**

Your manager wants to automate Azure DevOps project creation for every new customer. What tool would you use?

**Answer**

Use the **Azure DevOps CLI** within scripts or automation workflows to create projects, repositories, and related resources.

**Explanation**

The Azure DevOps CLI is designed for automating Azure DevOps administration tasks.

---

### Scenario 5

**Question**

A pipeline deploys to the wrong environment because the environment name is hardcoded in multiple places. What would you recommend?

**Answer**

Replace hardcoded values with **Pipeline Variables** or **Runtime Parameters**, depending on whether the value should be fixed or selected during execution.

**Explanation**

Centralizing configuration improves maintainability and reduces deployment mistakes.

---

### Scenario 6

**Question**

A developer asks whether Production should use Continuous Deployment. What would you recommend?

**Answer**

It depends on organizational requirements.

For many enterprise environments:

- Use Continuous Deployment for Development and QA.
- Use Continuous Delivery with approvals for Production.

**Explanation**

Production environments often require governance, compliance, or business approvals before deployment.

---

### Scenario 7

**Question**

A deployment uses artifacts generated from an old build instead of the latest successful build. What would you investigate?

**Answer**

Check:

- Artifact version.
- Build number.
- Release configuration.
- Pipeline variables.
- Artifact source selection.
- Deployment history.

**Explanation**

Incorrect artifact selection is a common cause of outdated deployments.

---

### Scenario 8

**Question**

Your organization wants every code commit to be automatically validated before merging into the `main` branch. Which practice would you recommend?

**Answer**

Implement **Continuous Integration (CI)** with:

- Automatic builds.
- Automated testing.
- Build validation.
- Branch Policies requiring successful builds before merge.

**Explanation**

CI detects issues early and prevents unstable code from reaching protected branches.

---

### Scenario 9

**Question**

A Runtime Parameter is expected to change during pipeline execution, but its value remains unchanged. Why?

**Answer**

Runtime Parameters are evaluated before pipeline execution begins and cannot be modified while the pipeline is running.

If the value must change during execution, use a Pipeline Variable or Runtime Variable instead.

**Explanation**

Understanding when parameters and variables are evaluated helps avoid pipeline design issues.

---

### Scenario 10

**Question**

Your organization wants to ensure that the same application package is deployed to Development, QA, and Production. How would you achieve this?

**Answer**

Build the application once, publish the Build Artifact, and use the same artifact for every deployment stage.

**Explanation**

Building once and deploying the same artifact eliminates inconsistencies between environments.

---

### Scenario 11

**Question**

A production release fails after deployment, and the business requests an immediate rollback. How does using Build Artifacts and Release Artifacts help?

**Answer**

Because the previously deployed Build Artifact is preserved, the deployment pipeline can redeploy the last known stable artifact without rebuilding the application.

This provides:

- Faster rollback.
- Consistent deployments.
- Reduced deployment risk.
- Better traceability.

**Explanation**

Separating the build process from deployment ensures that deployments and rollbacks use tested, immutable artifacts, which is a common best practice in enterprise CI/CD pipelines.
