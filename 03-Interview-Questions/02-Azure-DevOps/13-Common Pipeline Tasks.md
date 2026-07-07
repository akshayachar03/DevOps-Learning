# Azure DevOps Common Pipeline Tasks Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What are Pipeline Tasks in Azure DevOps?

**Answer**

Pipeline Tasks are predefined or custom actions that perform specific operations during pipeline execution.

Common tasks include:

- Checkout Source Code
- Install Dependencies
- Build Application
- Run Tests
- Publish Artifacts
- Download Artifacts
- Azure CLI
- PowerShell
- Bash
- Copy Files

Example:

```yaml
steps:
- task: AzureCLI@2
```

**Explanation**

Tasks are the building blocks of Azure DevOps pipelines. Each task performs one specific operation in the CI/CD process.

**Used in Production**

Every Build and Deployment Pipeline consists of multiple tasks executed in sequence.

**Common Mistake**

Many candidates confuse **Tasks** with **Steps**. Every task is a step, but not every step is a predefined task (a step can also be a script).

---

### Question 2

**Question**

What is the Checkout Source Code task?

**Answer**

The Checkout task downloads the source code from the configured repository to the build agent.

Example:

```yaml
steps:
- checkout: self
```

Supported repositories include:

- Azure Repos
- GitHub
- Bitbucket
- GitLab

**Explanation**

Without checking out the source code, the pipeline has no application files to build or test.

**Used in Production**

Almost every Build Pipeline starts with a checkout step.

**Common Mistake**

Candidates often assume the agent already contains the source code. The pipeline downloads it during execution.

---

### Question 3

**Question**

Why is installing dependencies an important pipeline task?

**Answer**

Applications depend on external packages that must be downloaded before building.

Examples:

- npm install
- dotnet restore
- mvn install
- pip install

**Explanation**

Dependency installation ensures that all required libraries are available before compilation or testing.

**Used in Production**

Dependency restoration is one of the first steps in every CI pipeline.

---

### Question 4

**Question**

What is the Build task?

**Answer**

The Build task compiles the application and generates executable or deployable files.

Examples:

- dotnet build
- mvn package
- npm run build
- gradle build

**Explanation**

The Build task validates the source code and creates binaries that can be deployed.

**Used in Production**

Every CI pipeline contains a build stage before artifact generation.

**Common Mistake**

Thinking Build tasks also deploy applications. Building and deployment are separate phases.

---

### Question 5

**Question**

Why should automated tests be executed in a pipeline?

**Answer**

Automated tests verify that the application functions correctly before deployment.

Common test types:

- Unit Tests
- Integration Tests
- Smoke Tests

Benefits:

- Detect bugs early
- Prevent regressions
- Improve software quality
- Increase deployment confidence

**Explanation**

If required tests fail, the pipeline should fail to prevent unstable code from being deployed.

**Used in Production**

Automated testing is a standard part of enterprise CI pipelines.

---

### Question 6

**Question**

What is the Publish Artifacts task?

**Answer**

The Publish Artifacts task uploads the build output so it can be used by later stages or Release Pipelines.

Example:

```yaml
- task: PublishBuildArtifacts@1
```

Published artifacts may include:

- ZIP files
- JAR files
- DLL files
- Docker images
- Static website files

**Explanation**

Publishing artifacts allows the application to be deployed without rebuilding.

**Used in Production**

Build Pipelines publish artifacts after successful compilation and testing.

**Common Mistake**

Publishing source code instead of the compiled application.

---

### Question 7

**Question**

What is the Download Artifacts task?

**Answer**

The Download Artifacts task retrieves previously published build artifacts for deployment.

Example:

```yaml
- task: DownloadPipelineArtifact@2
```

**Explanation**

Release Pipelines or deployment stages use this task to retrieve the application package before deployment.

**Used in Production**

Deployments always use downloaded artifacts rather than rebuilding the application.

---

### Question 8

**Question**

What is the Azure CLI Task?

**Answer**

The Azure CLI Task executes Azure CLI commands within a pipeline.

Example:

```yaml
- task: AzureCLI@2
```

Typical uses:

- Deploy Azure resources
- Create Resource Groups
- Deploy ARM/Bicep templates
- Manage Azure Storage
- Manage Azure App Services
- Deploy AKS resources

**Explanation**

The Azure CLI Task automates Azure resource management directly from Azure DevOps.

**Used in Production**

Infrastructure provisioning and application deployments commonly use Azure CLI.

**Common Mistake**

Forgetting to configure the required Azure Service Connection.

---

### Question 9

**Question**

What is the PowerShell Task?

**Answer**

The PowerShell Task executes PowerShell scripts during pipeline execution.

Example:

```yaml
- task: PowerShell@2
```

Typical uses:

- Windows administration
- Azure automation
- File management
- Configuration updates
- Deployment scripting

**Explanation**

PowerShell tasks are commonly used for Windows-based automation.

**Used in Production**

Organizations automate administrative tasks and deployments using PowerShell.

---

### Question 10

**Question**

What is the Bash Task?

**Answer**

The Bash Task executes Bash shell scripts during pipeline execution.

Example:

```yaml
- task: Bash@3
```

Typical uses:

- Linux administration
- Docker automation
- Kubernetes deployment
- File operations
- Shell scripting

**Explanation**

Bash tasks are widely used in Linux-based CI/CD environments.

**Used in Production**

Most Linux-based deployment pipelines use Bash for automation.

---

### Question 11

**Question**

How would you decide whether to use Azure CLI, PowerShell, or Bash in a pipeline?

**Answer**

| Task | Best Used For |
|------|---------------|
| Azure CLI | Managing Azure resources across Windows, Linux, and macOS |
| PowerShell | Windows administration, Azure automation, and PowerShell scripting |
| Bash | Linux administration, shell scripting, Docker, Kubernetes, and general Linux automation |

**Explanation**

The choice depends on the operating system, target platform, and existing automation scripts.

**Used in Production**

Many enterprise pipelines combine these tasks depending on deployment requirements.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

A pipeline fails immediately because it cannot find the application source code. What would you check?

**Answer**

Verify:

1. Checkout task configuration.
2. Repository connection.
3. Repository permissions.
4. Branch name.
5. Pipeline logs.
6. Repository availability.

**Explanation**

Most build failures at the beginning of a pipeline occur because the source code was not checked out successfully.

---

### Scenario 2

**Question**

The Build task fails because required packages are missing. How would you troubleshoot?

**Answer**

Check:

- Dependency installation task.
- Package feed access.
- Authentication.
- Internet connectivity.
- Package versions.
- Build agent configuration.

**Explanation**

Missing dependencies are one of the most common causes of build failures.

---

### Scenario 3

**Question**

A Build Pipeline succeeds, but the Release Pipeline cannot find the application package. What would you investigate?

**Answer**

Check:

- Publish Artifacts task.
- Artifact name.
- Build logs.
- Artifact retention policy.
- Download Artifacts configuration.
- Pipeline permissions.

**Explanation**

Deployment pipelines depend on published artifacts. If artifacts are not published correctly, deployments cannot proceed.

---

### Scenario 4

**Question**

Your Azure CLI task fails with an authentication error. What would you check?

**Answer**

Verify:

- Azure Service Connection.
- Service Principal credentials.
- Azure RBAC permissions.
- Subscription selection.
- Azure CLI command syntax.
- Pipeline logs.

**Explanation**

Authentication and permission issues are common causes of Azure CLI task failures.

---

### Scenario 5

**Question**

A PowerShell script works on your local machine but fails in the pipeline. What could be the reasons?

**Answer**

Possible causes include:

- Missing PowerShell modules.
- Different PowerShell version.
- Missing permissions.
- Incorrect file paths.
- Missing environment variables.
- Execution policy restrictions.

**Explanation**

The pipeline agent environment may differ significantly from a local development machine.

---

### Scenario 6

**Question**

A Bash script fails during deployment because a required command is missing. How would you resolve this?

**Answer**

- Verify the command exists on the agent.
- Install the required tool if using a self-hosted agent.
- Select an appropriate Microsoft-hosted image if available.
- Update the pipeline to install the dependency before execution if necessary.

**Explanation**

Pipeline agents must contain all required software before executing Bash scripts.

---

### Scenario 7

**Question**

Your manager wants every deployment to use the exact same build output that passed testing. What pipeline tasks make this possible?

**Answer**

Use:

1. **Publish Artifacts** in the Build Pipeline.
2. **Download Artifacts** in the Deployment Pipeline.

**Explanation**

Publishing and downloading artifacts ensures that the same validated application package is deployed across all environments.

---

### Scenario 8

**Question**

A deployment task must create a new Azure Resource Group before deploying the application. Which task would you use?

**Answer**

Use the **Azure CLI Task** with an appropriate Azure Service Connection.

Example command:

```bash
az group create --name MyRG --location eastus
```

**Explanation**

Azure CLI provides native support for Azure resource management and automation.

---

### Scenario 9

**Question**

Your team manages Windows servers for deployments. Would you recommend Bash or PowerShell?

**Answer**

Use **PowerShell**.

PowerShell integrates naturally with Windows administration and provides extensive support for Windows system management and Azure automation.

**Explanation**

Choosing tools that align with the target operating system simplifies automation and maintenance.

---

### Scenario 10

**Question**

The Test task fails because one unit test is failing. Should the pipeline continue to publish artifacts?

**Answer**

No.

The pipeline should stop until the failing test is corrected and the build passes successfully.

**Explanation**

Publishing artifacts from an unsuccessful build increases the risk of deploying unstable or defective software.

---

### Scenario 11

**Question**

Your organization has multiple pipelines that all perform checkout, dependency installation, build, testing, and artifact publishing in the same way. How would you reduce duplication?

**Answer**

Create reusable YAML templates that include the common pipeline tasks and reference those templates from each pipeline.

**Explanation**

Using templates standardizes CI/CD processes, reduces maintenance effort, and ensures consistent build behavior across projects while avoiding duplicated pipeline code.
