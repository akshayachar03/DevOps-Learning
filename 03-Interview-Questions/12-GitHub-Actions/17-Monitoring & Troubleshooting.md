# Monitoring & Troubleshooting Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

How do you monitor GitHub Actions workflow execution?

**Answer**

GitHub Actions provides a workflow execution page where you can monitor:

- Workflow status
- Job status
- Step execution
- Execution time
- Logs
- Artifacts

**Explanation**

Each workflow run records detailed execution information, making it easy to identify where failures occur.

**Where it is used in Production**

DevOps engineers monitor workflows after every code commit, pull request, or deployment.

**Common Mistake**

Candidates often check only the final workflow status instead of identifying the specific job or step that failed.

---

### Question 2

**Question**

What are Workflow Logs in GitHub Actions?

**Answer**

Workflow Logs contain detailed output generated during workflow execution.

They include:

- Commands executed
- Build output
- Test results
- Deployment logs
- Error messages

**Explanation**

Logs are the primary source for troubleshooting workflow failures.

**Where it is used in Production**

Every CI/CD pipeline relies on workflow logs for debugging failed builds and deployments.

---

### Question 3

**Question**

How do you troubleshoot a failed GitHub Actions job?

**Answer**

A systematic approach is:

1. Identify the failed job.
2. Open the job logs.
3. Locate the failed step.
4. Read the error message.
5. Verify configuration, commands, and dependencies.
6. Fix the issue and rerun the workflow.

**Explanation**

Jobs consist of multiple steps. Finding the exact failed step significantly reduces troubleshooting time.

**Where it is used in Production**

Daily CI/CD troubleshooting.

---

### Question 4

**Question**

What is the difference between a Failed Job and a Failed Step?

**Answer**

A **Failed Step** is an individual task that encounters an error.

A **Failed Job** occurs when one or more critical steps fail, causing the entire job to fail.

**Explanation**

Since jobs execute steps sequentially, a failure in one step typically stops the remaining steps unless configured otherwise.

**Where it is used in Production**

Build, test, and deployment workflows.

---

### Question 5

**Question**

What is Debug Logging in GitHub Actions?

**Answer**

Debug Logging provides additional execution details beyond standard logs, helping diagnose complex workflow issues.

**Explanation**

Debug logs display more detailed information about workflow execution, environment variables (excluding secrets), action execution, and command processing.

**Where it is used in Production**

Troubleshooting intermittent or difficult-to-diagnose workflow failures.

---

### Question 6

**Question**

When should you enable Debug Logging?

**Answer**

Debug Logging should be enabled when:

- Normal logs are insufficient.
- Workflow behavior is inconsistent.
- Third-party actions fail unexpectedly.
- Environment-related issues occur.

**Explanation**

Debug logging should be used only during troubleshooting because it generates significantly more log output.

**Where it is used in Production**

Temporary troubleshooting during incident investigations.

---

### Question 7

**Question**

What is the purpose of Re-run Workflow in GitHub Actions?

**Answer**

Re-run Workflow executes the same workflow again without requiring another code commit.

**Explanation**

This feature is useful when failures are caused by temporary issues such as network interruptions or unavailable external services.

**Where it is used in Production**

Recovering from transient infrastructure failures.

**Common Mistake**

Candidates often rerun workflows repeatedly without first identifying the root cause.

---

### Question 8

**Question**

What are some common GitHub Actions workflow errors?

**Answer**

Common errors include:

- YAML syntax errors
- Authentication failures
- Missing secrets
- Permission issues
- Dependency installation failures
- Build failures
- Test failures
- Missing artifacts
- Incorrect workflow paths

**Explanation**

Most workflow failures fall into one of these categories.

**Where it is used in Production**

Daily CI/CD troubleshooting.

---

### Question 9

**Question**

How can you identify the root cause of a workflow failure?

**Answer**

The best approach is to:

- Review workflow logs.
- Identify the failed step.
- Read the exact error message.
- Verify workflow configuration.
- Validate environment variables and secrets.
- Reproduce the issue if necessary.

**Explanation**

The first reported error is usually the actual root cause, while later errors are often secondary failures.

**Where it is used in Production**

Incident response and CI/CD maintenance.

---

### Question 10

**Question**

What should you check if a workflow suddenly starts failing after previously working correctly?

**Answer**

Check for:

- Recent code changes
- Workflow changes
- Secret updates
- Permission changes
- Third-party action updates
- Dependency updates
- External service availability

**Explanation**

Most unexpected failures are caused by recent changes rather than GitHub Actions itself.

**Where it is used in Production**

Production release troubleshooting.

---

### Question 11

**Question**

Why should workflow logs be reviewed before rerunning a failed workflow?

**Answer**

Logs often reveal the root cause of the failure. Simply rerunning without understanding the issue may waste time and resources.

**Explanation**

Only transient issues should be resolved by rerunning. Configuration or code issues require fixes before rerunning.

**Where it is used in Production**

Efficient CI/CD incident resolution.

---

### Question 12

**Question**

What are some best practices for troubleshooting GitHub Actions workflows?

**Answer**

Best practices include:

- Read workflow logs carefully.
- Identify the exact failed step.
- Verify secrets and permissions.
- Validate YAML syntax.
- Pin action versions.
- Test changes in a non-production branch.
- Enable debug logging only when necessary.

**Explanation**

Following a structured troubleshooting process reduces downtime and speeds up issue resolution.

**Where it is used in Production**

Enterprise DevOps teams handling CI/CD pipelines.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

Your workflow fails during the build stage. How would you troubleshoot it?

**Answer**

I would:

1. Open the workflow logs.
2. Identify the failed job.
3. Locate the failed step.
4. Review the build error.
5. Verify dependencies and build commands.
6. Fix the issue before rerunning the workflow.

**Explanation**

The workflow logs provide the most accurate information about the failure.

---

### Scenario 2

**Question**

Your workflow suddenly fails with a "Permission Denied" error after working successfully for months. What would you check?

**Answer**

I would verify:

- Workflow permissions
- `GITHUB_TOKEN` permissions
- Repository settings
- Branch protection rules
- Secret availability

**Explanation**

Permission-related configuration changes are a common cause of previously working workflows failing.

---

### Scenario 3

**Question**

A workflow fails because a secret cannot be found. How would you resolve it?

**Answer**

I would verify:

- Secret name
- Repository or environment scope
- Workflow reference
- Secret permissions

**Explanation**

Secrets are case-sensitive and must exist in the correct scope.

---

### Scenario 4

**Question**

Your workflow reports a YAML syntax error before executing any jobs. What would you do?

**Answer**

I would validate the workflow YAML file by checking indentation, formatting, and syntax before committing the fix.

**Explanation**

YAML parsing errors prevent workflow execution entirely.

---

### Scenario 5

**Question**

A workflow fails while downloading dependencies because an external package repository is temporarily unavailable. What would you do?

**Answer**

After confirming the failure is temporary, I would rerun the workflow.

**Explanation**

Transient network or service outages often resolve without requiring code changes.

---

### Scenario 6

**Question**

Your deployment job cannot find the build artifact generated earlier. What is the most likely cause?

**Answer**

The artifact was either not uploaded during the build job or was not downloaded in the deployment job.

**Explanation**

Artifacts must be explicitly uploaded and downloaded between jobs.

---

### Scenario 7

**Question**

A workflow passes locally but fails only in GitHub Actions. What would you investigate?

**Answer**

I would compare:

- Runner operating system
- Installed software versions
- Environment variables
- Secrets
- Dependency versions
- Workflow configuration

**Explanation**

Differences between local and runner environments commonly cause this issue.

---

### Scenario 8

**Question**

A workflow fails intermittently with no obvious error. What troubleshooting approach would you take?

**Answer**

I would enable debug logging, review detailed logs, identify patterns, and check external dependencies or network reliability.

**Explanation**

Intermittent failures often require additional diagnostic information.

---

### Scenario 9

**Question**

Your team repeatedly reruns failed workflows without reviewing the logs. Why is this a poor practice?

**Answer**

Repeated reruns may temporarily hide issues but do not resolve configuration or code problems. Reviewing logs first helps identify and fix the root cause.

**Explanation**

Effective troubleshooting focuses on identifying the underlying issue rather than repeatedly retrying the workflow.

---

### Scenario 10

**Question**

Your manager asks you to reduce the average time spent troubleshooting GitHub Actions failures. What best practices would you recommend?

**Answer**

I would recommend:

- Review workflow logs before rerunning.
- Identify the exact failed step.
- Use descriptive job and step names.
- Validate YAML before committing.
- Pin action versions.
- Store secrets securely.
- Enable debug logging only when required.
- Document common workflow failures and their resolutions.

**Explanation**

A structured troubleshooting process improves reliability, reduces downtime, and enables faster incident resolution across CI/CD pipelines.
