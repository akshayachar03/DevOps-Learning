# Permissions & Security & Common Workflow Commands Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is the `GITHUB_TOKEN` in GitHub Actions?

**Answer**

`GITHUB_TOKEN` is an automatically generated authentication token that GitHub provides to every workflow run. It allows workflows to securely interact with the repository without requiring a Personal Access Token (PAT).

Common uses include:

- Cloning repositories
- Creating releases
- Updating pull requests
- Uploading artifacts
- Accessing GitHub APIs

**Explanation**

The token is created automatically for each workflow execution and expires when the workflow completes. Its permissions can be restricted or expanded based on workflow requirements.

**Where it is used in Production**

- CI/CD automation
- Repository management
- Release automation

**Common Mistake**

Many candidates believe `GITHUB_TOKEN` is permanent. It is temporary and exists only during the workflow execution.

---

### Question 2

**Question**

What are Workflow Permissions in GitHub Actions?

**Answer**

Workflow Permissions define what the `GITHUB_TOKEN` is allowed to do during a workflow run.

Permissions can include:

- Read repository contents
- Write repository contents
- Manage pull requests
- Deploy packages
- Manage issues

**Explanation**

Applying the principle of least privilege improves workflow security by granting only the required permissions.

**Where it is used in Production**

Enterprise organizations restrict workflow permissions to reduce security risks.

---

### Question 3

**Question**

What are Repository Permissions?

**Answer**

Repository Permissions determine what users, teams, applications, and workflows can access within a GitHub repository.

Examples include:

- Read
- Write
- Maintain
- Admin

**Explanation**

Repository permissions control who can modify code, manage workflows, or administer repository settings.

**Where it is used in Production**

Access control for development teams and CI/CD pipelines.

---

### Question 4

**Question**

What is a Personal Access Token (PAT)?

**Answer**

A Personal Access Token (PAT) is a user-generated authentication token that can access GitHub resources when additional permissions beyond `GITHUB_TOKEN` are required.

**Explanation**

PATs are commonly used when workflows interact with external repositories or require elevated GitHub permissions.

**Where it is used in Production**

- Cross-repository access
- GitHub API automation
- Private repository access

**Common Mistake**

Candidates often use PATs even when `GITHUB_TOKEN` is sufficient. Prefer `GITHUB_TOKEN` whenever possible because it is temporary and more secure.

---

### Question 5

**Question**

When should you use `GITHUB_TOKEN` instead of a Personal Access Token (PAT)?

**Answer**

Use `GITHUB_TOKEN` whenever the workflow only needs to access its own repository.

Use a PAT only when:

- Accessing another repository
- Performing operations not permitted by `GITHUB_TOKEN`
- Integrating with external GitHub resources

**Explanation**

`GITHUB_TOKEN` is automatically managed by GitHub and reduces credential management overhead.

**Where it is used in Production**

Standard CI/CD workflows.

---

### Question 6

**Question**

What is the purpose of the `actions/checkout` action?

**Answer**

`actions/checkout` downloads the repository source code onto the GitHub Actions runner.

Example:

```yaml
uses: actions/checkout@v4
```

**Explanation**

Without checking out the repository, workflow steps cannot access project files.

**Where it is used in Production**

Nearly every GitHub Actions workflow begins with this action.

---

### Question 7

**Question**

What is the purpose of `actions/setup-node`?

**Answer**

`actions/setup-node` installs and configures a specific version of Node.js on the runner.

**Explanation**

This ensures workflows use a consistent Node.js version across all executions.

**Where it is used in Production**

Node.js application build and test pipelines.

---

### Question 8

**Question**

What is the purpose of `actions/setup-java`?

**Answer**

`actions/setup-java` installs and configures a Java Development Kit (JDK) for Java-based projects.

**Explanation**

It allows Java applications to be compiled and tested during workflow execution.

**Where it is used in Production**

- Spring Boot applications
- Maven builds
- Gradle builds

---

### Question 9

**Question**

What is the purpose of `actions/cache`?

**Answer**

`actions/cache` stores reusable dependencies so they can be restored during future workflow runs.

Examples include:

- npm packages
- Maven dependencies
- Gradle cache
- pip packages

**Explanation**

Caching significantly reduces workflow execution time by avoiding repeated dependency downloads.

**Where it is used in Production**

Almost every enterprise CI/CD pipeline.

---

### Question 10

**Question**

What are `upload-artifact` and `download-artifact` actions used for?

**Answer**

- `upload-artifact` stores workflow outputs.
- `download-artifact` retrieves those outputs in later jobs.

**Explanation**

Artifacts allow build outputs such as binaries, reports, and logs to be shared between jobs.

**Where it is used in Production**

- Build pipelines
- Test pipelines
- Deployment pipelines

---

### Question 11

**Question**

Why should third-party GitHub Actions be version pinned?

**Answer**

Version pinning ensures workflows always execute a known, trusted version of an action.

Example:

```yaml
uses: actions/checkout@v4
```

**Explanation**

Pinning prevents unexpected behavior caused by breaking changes in newer versions.

**Where it is used in Production**

All enterprise GitHub Actions workflows.

---

### Question 12

**Question**

What security best practices should be followed in GitHub Actions workflows?

**Answer**

Best practices include:

- Use `GITHUB_TOKEN` whenever possible.
- Store credentials in GitHub Secrets.
- Grant least-privilege permissions.
- Pin action versions.
- Avoid hardcoding secrets.
- Review third-party actions before using them.

**Explanation**

These practices reduce security risks and protect CI/CD pipelines from unauthorized access.

**Where it is used in Production**

Enterprise DevSecOps environments.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

Your workflow fails when trying to push changes back to the repository with a permission denied error. What would you check?

**Answer**

I would verify:

- `GITHUB_TOKEN` permissions
- Workflow permission settings
- Branch protection rules
- Repository write permissions

**Explanation**

The workflow may only have read permission or be blocked by repository policies.

---

### Scenario 2

**Question**

Your workflow needs to clone a private repository from another organization. Will `GITHUB_TOKEN` work?

**Answer**

Usually no.

I would use a Personal Access Token (PAT) or another supported authentication method with permission to access the external repository.

**Explanation**

`GITHUB_TOKEN` is generally scoped to the current repository.

---

### Scenario 3

**Question**

A workflow fails because Node.js is not installed on the runner. How would you fix it?

**Answer**

I would add the `actions/setup-node` action before installing dependencies or building the application.

**Explanation**

The runner must have the required runtime before executing project commands.

---

### Scenario 4

**Question**

Your Java application fails during compilation because the required JDK version is unavailable. What would you do?

**Answer**

I would configure `actions/setup-java` with the required Java version before the build stage.

**Explanation**

Using the correct JDK version ensures consistent builds across environments.

---

### Scenario 5

**Question**

Your workflow takes several minutes downloading dependencies during every execution. What optimization would you implement?

**Answer**

I would use `actions/cache` to cache dependency directories.

**Explanation**

Caching significantly reduces workflow duration by restoring previously downloaded dependencies.

---

### Scenario 6

**Question**

Your deployment job cannot find the build package created in an earlier job. What is the most likely issue?

**Answer**

The build job did not upload the package as an artifact, or the deployment job did not download it.

**Explanation**

Artifacts must be explicitly uploaded and downloaded between jobs.

---

### Scenario 7

**Question**

Your security team finds that API keys are hardcoded in the workflow file. How would you correct this?

**Answer**

I would move all sensitive values into GitHub Secrets and reference them using the `secrets` context.

**Explanation**

Secrets are encrypted and hidden from workflow logs, making them the recommended method for storing credentials.

---

### Scenario 8

**Question**

Your organization requires workflows to have only the minimum permissions necessary. How would you implement this?

**Answer**

I would explicitly configure workflow permissions and grant only the required scopes instead of using broad default permissions.

**Explanation**

Applying the principle of least privilege reduces the impact of compromised workflows.

---

### Scenario 9

**Question**

A third-party GitHub Action introduces a breaking change that causes your workflow to fail. How could this have been prevented?

**Answer**

I would pin the action to a specific stable version instead of always using the latest release.

**Explanation**

Version pinning provides predictable workflow behavior and avoids unexpected changes.

---

### Scenario 10

**Question**

Your workflow builds successfully but later jobs cannot access the generated reports. How would you resolve the issue?

**Answer**

I would upload the reports using `upload-artifact` in the build job and retrieve them using `download-artifact` in the later jobs.

**Explanation**

Artifacts are the recommended mechanism for sharing workflow outputs between jobs in GitHub Actions.
