# GitHub Actions Fundamentals & Workflow Basics Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is GitHub Actions?

**Answer**

GitHub Actions is GitHub's built-in CI/CD and automation platform that allows developers to automate software development workflows such as building, testing, and deploying applications directly from a GitHub repository.

**Explanation**

GitHub Actions listens for repository events (such as push or pull request), executes workflows on runners, and automates repetitive development tasks.

**Where it is used in Production**

- Continuous Integration (CI)
- Continuous Delivery (CD)
- Automated testing
- Code quality checks
- Infrastructure automation
- Deployment pipelines

**Common Mistake**

Many candidates think GitHub Actions is only for CI/CD. It can automate almost any repository-related task.

---

### Question 2

**Question**

What is Continuous Integration (CI), and how is GitHub Actions used for it?

**Answer**

Continuous Integration (CI) is the practice of automatically building and testing code whenever developers commit changes. GitHub Actions automates this process using workflows triggered by repository events.

**Explanation**

CI detects integration issues early by validating every code change before it reaches production.

**Where it is used in Production**

Every enterprise development team uses CI to ensure code quality before merging changes.

---

### Question 3

**Question**

What are the main components of GitHub Actions architecture?

**Answer**

The major components are:

- Repository
- Workflow
- Events
- Jobs
- Steps
- Actions
- Runners

**Explanation**

A workflow is triggered by an event, executed by a runner, and consists of one or more jobs. Each job contains multiple steps that execute actions or commands.

**Where it is used in Production**

Every GitHub Actions pipeline follows this architecture.

---

### Question 4

**Question**

What is a Workflow in GitHub Actions?

**Answer**

A Workflow is an automated process defined in a YAML file that specifies when and how automation tasks should run.

**Explanation**

A workflow defines triggers, jobs, execution order, environment, and deployment logic.

**Where it is used in Production**

- Build pipelines
- Test pipelines
- Deployment pipelines
- Security scans

---

### Question 5

**Question**

What are Events in GitHub Actions?

**Answer**

Events are activities that trigger workflow execution.

Common events include:

- push
- pull_request
- workflow_dispatch
- schedule
- release

**Explanation**

GitHub monitors repository activities and starts workflows when configured events occur.

**Where it is used in Production**

Automatically starting CI/CD pipelines after code changes.

**Common Mistake**

Candidates often confuse events with jobs. Events trigger workflows, while jobs perform the actual work.

---

### Question 6

**Question**

What are GitHub Actions Runners?

**Answer**

Runners are machines that execute workflow jobs.

GitHub supports:

- GitHub-hosted runners
- Self-hosted runners

**Explanation**

When a workflow starts, GitHub assigns the job to an available runner.

**Where it is used in Production**

Running builds, tests, deployments, and automation tasks.

---

### Question 7

**Question**

Where are GitHub Actions workflow files stored?

**Answer**

Workflow files are stored inside:

```text
.github/workflows/
```

Each workflow is written as a YAML file.

**Explanation**

GitHub automatically detects YAML files placed inside this directory.

**Where it is used in Production**

Every GitHub Actions project follows this directory structure.

---

### Question 8

**Question**

Why does GitHub Actions use YAML files?

**Answer**

YAML provides a simple and human-readable format for defining workflows.

It specifies:

- Triggers
- Jobs
- Steps
- Environment
- Actions

**Explanation**

GitHub parses the YAML file and executes the workflow accordingly.

**Where it is used in Production**

All GitHub Actions pipelines are defined using YAML.

---

### Question 9

**Question**

What is the basic structure of a GitHub Actions workflow?

**Answer**

A workflow generally contains:

- name
- on
- jobs
- steps

Example:

```yaml
name: CI Pipeline

on:
  push:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
```

**Explanation**

These sections define the workflow name, trigger, execution environment, and tasks.

**Where it is used in Production**

Every GitHub Actions workflow.

---

### Question 10

**Question**

What are Workflow Triggers?

**Answer**

Workflow Triggers determine when a workflow should execute.

Examples include:

- push
- pull_request
- workflow_dispatch
- schedule

**Explanation**

Triggers automate CI/CD by responding to repository events.

**Where it is used in Production**

Automatic deployments, testing, and release automation.

---

### Question 11

**Question**

What is the difference between GitHub-hosted and Self-hosted runners?

**Answer**

GitHub-hosted runners are managed by GitHub, while Self-hosted runners are managed by the organization.

**Explanation**

GitHub-hosted runners require no maintenance. Self-hosted runners provide more control, custom software, and access to private infrastructure.

**Where it is used in Production**

- GitHub-hosted runners for general CI/CD
- Self-hosted runners for enterprise deployments

**Common Mistake**

Many candidates assume self-hosted runners are always faster. Performance depends on the organization's infrastructure.

---

### Question 12

**Question**

How does a GitHub Actions workflow execute after a developer pushes code?

**Answer**

The sequence is:

1. Developer pushes code.
2. GitHub detects the configured event.
3. Matching workflow starts.
4. A runner is assigned.
5. Jobs execute.
6. Results are reported back to GitHub.

**Explanation**

GitHub automates the entire workflow without manual intervention.

**Where it is used in Production**

Every automated CI/CD pipeline.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

A developer pushes code, but the GitHub Actions workflow does not start. How would you troubleshoot?

**Answer**

I would check:

- Workflow file location (`.github/workflows`)
- YAML syntax
- Trigger configuration
- Branch filters
- GitHub Actions settings
- Repository permissions

**Explanation**

Most workflow execution failures occur due to incorrect triggers or improperly placed workflow files.

---

### Scenario 2

**Question**

Your workflow should run only when code is pushed to the `main` branch. How would you configure it?

**Answer**

Use the `push` event with a branch filter:

```yaml
on:
  push:
    branches:
      - main
```

**Explanation**

Branch filters prevent unnecessary workflow executions on other branches.

---

### Scenario 3

**Question**

A workflow works correctly in one repository but not in another. What would you investigate?

**Answer**

I would verify:

- Workflow location
- Repository permissions
- Actions settings
- Branch names
- YAML syntax
- Runner availability

**Explanation**

Repository configuration differences often cause workflow failures.

---

### Scenario 4

**Question**

Your organization wants developers to manually trigger deployments instead of deploying after every push. Which trigger would you use?

**Answer**

I would use:

```yaml
workflow_dispatch
```

**Explanation**

`workflow_dispatch` allows users to manually start workflows from the GitHub interface.

---

### Scenario 5

**Question**

Your workflow remains in the "Waiting" state for several minutes. What could be the reason?

**Answer**

Possible causes include:

- No available runner
- Offline self-hosted runner
- High GitHub-hosted runner usage
- Concurrency limits

**Explanation**

Jobs cannot start until a runner becomes available.

---

### Scenario 6

**Question**

Your team needs to deploy applications to an internal server that GitHub-hosted runners cannot access. Which runner would you choose?

**Answer**

I would configure a **Self-hosted Runner**.

**Explanation**

Self-hosted runners can access private networks and internal infrastructure.

---

### Scenario 7

**Question**

A workflow fails immediately with a YAML parsing error. What would you check?

**Answer**

I would verify:

- Indentation
- Missing colons
- Invalid keys
- Incorrect spacing
- YAML syntax

**Explanation**

YAML is indentation-sensitive, making formatting errors a common cause of workflow failures.

---

### Scenario 8

**Question**

Your organization wants code to be automatically tested whenever a pull request is created. Which event would you configure?

**Answer**

I would configure:

```yaml
on:
  pull_request:
```

**Explanation**

This ensures all pull requests are validated before merging.

---

### Scenario 9

**Question**

A workflow executes successfully but does not perform the expected tasks. What would you investigate?

**Answer**

I would check:

- Workflow steps
- Job execution logs
- Conditions (`if`)
- Action versions
- Environment variables

**Explanation**

A successful workflow status does not necessarily mean every intended operation was performed.

---

### Scenario 10

**Question**

During a production release, management asks how GitHub Actions automates deployments from code commit to execution. How would you explain it?

**Answer**

I would explain the workflow as follows:

1. Developer pushes code.
2. GitHub detects the configured event.
3. Workflow starts automatically.
4. Runner executes jobs.
5. Build and tests run.
6. Deployment is performed if all stages succeed.
7. Results are reported in GitHub.

**Explanation**

This automated pipeline ensures consistent, repeatable, and reliable software delivery while reducing manual intervention.
