# Events (Triggers) & Jobs & Steps Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What are Events (Triggers) in GitHub Actions?

**Answer**

Events are GitHub activities that automatically start a workflow.

Common events include:

- `push`
- `pull_request`
- `workflow_dispatch`
- `schedule`
- `release`

**Explanation**

GitHub continuously monitors repository events. When an event matches the workflow configuration, it automatically starts the workflow.

**Where it is used in Production**

- CI pipelines
- Automated deployments
- Scheduled maintenance
- Release automation

**Common Mistake**

Candidates often confuse events with jobs. Events trigger workflows, while jobs perform the actual work.

---

### Question 2

**Question**

What is the difference between the `push` and `pull_request` events?

**Answer**

- **push** triggers when code is pushed to a repository.
- **pull_request** triggers when a pull request is opened, synchronized, or updated.

**Explanation**

`push` is commonly used for branch builds, while `pull_request` validates code before it is merged into the target branch.

**Where it is used in Production**

- `push` for Continuous Integration.
- `pull_request` for code review validation.

---

### Question 3

**Question**

What is the `workflow_dispatch` event?

**Answer**

`workflow_dispatch` allows workflows to be started manually from the GitHub Actions interface.

**Explanation**

This trigger is useful for deployments, maintenance tasks, and production releases that should not run automatically.

**Where it is used in Production**

- Manual production deployments
- Database migrations
- Infrastructure updates

---

### Question 4

**Question**

What is the `schedule` event in GitHub Actions?

**Answer**

The `schedule` event runs workflows automatically based on a cron expression.

Example:

```yaml
on:
  schedule:
    - cron: "0 2 * * *"
```

**Explanation**

Scheduled workflows automate recurring tasks without user interaction.

**Where it is used in Production**

- Nightly builds
- Backup jobs
- Security scans
- Dependency updates

**Common Mistake**

Candidates often assume scheduled workflows run exactly at the specified time. Actual execution may be delayed depending on GitHub workload.

---

### Question 5

**Question**

What is the `release` event?

**Answer**

The `release` event triggers workflows when a GitHub Release is published, edited, or deleted.

**Explanation**

This event automates release-related tasks such as packaging applications and deploying production artifacts.

**Where it is used in Production**

- Production deployments
- Publishing release artifacts
- Version tagging

---

### Question 6

**Question**

What is a Job in GitHub Actions?

**Answer**

A Job is a collection of steps executed on the same runner.

Each workflow can contain one or more jobs.

**Explanation**

Jobs organize related tasks within a workflow, such as building, testing, and deploying an application.

**Where it is used in Production**

Every GitHub Actions workflow contains one or more jobs.

---

### Question 7

**Question**

What is a Step in GitHub Actions?

**Answer**

A Step is an individual task inside a job.

Examples include:

- Running shell commands
- Executing scripts
- Calling reusable actions

**Explanation**

Steps execute sequentially within a job and share the same execution environment.

**Where it is used in Production**

Every build, test, deployment, or automation task.

---

### Question 8

**Question**

What are Job Dependencies in GitHub Actions?

**Answer**

Job dependencies define the order in which jobs execute using the `needs` keyword.

Example:

```yaml
deploy:
  needs: build
```

**Explanation**

The dependent job starts only after the required job completes successfully.

**Where it is used in Production**

Build → Test → Deploy pipelines.

---

### Question 9

**Question**

What are Parallel Jobs?

**Answer**

Parallel Jobs execute simultaneously when there are no dependencies between them.

**Explanation**

Running independent jobs in parallel reduces overall pipeline execution time.

**Where it is used in Production**

Running:

- Unit tests
- Security scans
- Code quality checks

at the same time.

---

### Question 10

**Question**

What are Sequential Jobs?

**Answer**

Sequential Jobs execute one after another using job dependencies.

**Explanation**

A downstream job starts only after the previous job completes successfully.

**Where it is used in Production**

Typical deployment pipeline:

Build → Test → Package → Deploy

---

### Question 11

**Question**

Can multiple steps inside a job run in parallel?

**Answer**

No.

Steps inside a job always execute sequentially.

Only separate jobs can execute in parallel.

**Explanation**

Since all steps share the same runner environment, they execute one after another.

**Where it is used in Production**

Every GitHub Actions workflow.

**Common Mistake**

Many candidates incorrectly believe that steps inside a job can execute simultaneously.

---

### Question 12

**Question**

Why are Job Dependencies important in CI/CD pipelines?

**Answer**

Job dependencies ensure that critical stages execute in the correct order.

For example:

- Build succeeds before testing.
- Tests pass before deployment.
- Deployment occurs only after successful validation.

**Explanation**

Dependencies prevent invalid deployments and improve pipeline reliability.

**Where it is used in Production**

Every enterprise CI/CD pipeline.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

You want to automatically run tests whenever a developer opens a Pull Request. Which event would you use?

**Answer**

I would use:

```yaml
on:
  pull_request:
```

**Explanation**

The `pull_request` event validates changes before they are merged into the target branch.

---

### Scenario 2

**Question**

Your organization wants production deployments to start only when a Release is published. Which trigger would you configure?

**Answer**

I would configure:

```yaml
on:
  release:
    types: [published]
```

**Explanation**

This ensures deployments occur only for official releases.

---

### Scenario 3

**Question**

You need to run a security scan every night at 2:00 AM. Which trigger should you use?

**Answer**

I would configure the `schedule` event using a cron expression.

Example:

```yaml
on:
  schedule:
    - cron: "0 2 * * *"
```

**Explanation**

Scheduled workflows automate recurring operational tasks.

---

### Scenario 4

**Question**

Your deployment job starts even though the build job failed. How would you prevent this?

**Answer**

I would make the deployment job dependent on the build job using:

```yaml
needs: build
```

**Explanation**

Job dependencies ensure downstream jobs execute only after successful completion of required jobs.

---

### Scenario 5

**Question**

Your pipeline contains Build, Test, Security Scan, and Deploy jobs. Which jobs can run in parallel?

**Answer**

- Build runs first.
- Test and Security Scan can run in parallel after Build.
- Deploy waits for both jobs to complete.

**Explanation**

Independent jobs should execute concurrently to reduce pipeline duration.

---

### Scenario 6

**Question**

A manager wants to manually approve production deployments instead of deploying automatically after every push. Which trigger would you recommend?

**Answer**

I would use:

```yaml
workflow_dispatch
```

**Explanation**

This allows engineers to manually start deployments from the GitHub Actions interface.

---

### Scenario 7

**Question**

Your workflow starts successfully, but the deployment job never executes. What would you investigate?

**Answer**

I would verify:

- Job dependencies (`needs`)
- Previous job status
- Conditional statements (`if`)
- Runner availability
- Workflow logs

**Explanation**

Deployment jobs often skip execution because a dependent job failed or a condition was not satisfied.

---

### Scenario 8

**Question**

A workflow takes too long because testing and security scanning execute one after another. How would you optimize it?

**Answer**

I would separate them into independent jobs so they execute in parallel.

**Explanation**

Parallel execution reduces overall pipeline time and improves CI efficiency.

---

### Scenario 9

**Question**

Your organization wants builds to run after every code push but deployments only after manual approval. How would you design the workflow?

**Answer**

I would:

- Trigger Build using `push`.
- Trigger Deployment using `workflow_dispatch`.

**Explanation**

This provides automatic validation while keeping production deployments under manual control.

---

### Scenario 10

**Question**

A workflow executes successfully, but one step inside the Build job fails. What happens?

**Answer**

By default:

- The remaining steps in that job stop executing.
- Dependent jobs do not start.
- The workflow is marked as failed.

**Explanation**

GitHub Actions stops execution after a failed step unless error-handling options such as `continue-on-error` are explicitly configured. This prevents unreliable artifacts from progressing through the pipeline.
