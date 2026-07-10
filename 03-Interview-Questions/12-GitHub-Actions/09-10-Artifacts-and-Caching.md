# Artifacts & Caching Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What are Artifacts in GitHub Actions?

**Answer**

Artifacts are files or directories generated during a workflow that can be uploaded and stored after a job completes. They can be downloaded later or shared with other jobs in the same workflow.

Examples include:

- Build binaries
- Test reports
- Coverage reports
- Log files
- Deployment packages

**Explanation**

Artifacts preserve workflow outputs beyond the lifetime of the runner. They help developers inspect build results, debug failures, and pass generated files between stages of a CI/CD pipeline.

**Where it is used in Production**

- Sharing build packages between Build and Deploy stages
- Storing test reports
- Saving logs for troubleshooting
- Archiving release binaries

**Common Mistake**

Candidates often confuse artifacts with caches. Artifacts store workflow outputs, while caches store reusable dependencies to speed up builds.

---

### Question 2

**Question**

How do you upload artifacts in GitHub Actions?

**Answer**

Artifacts are uploaded using the `actions/upload-artifact` action.

Example:

```yaml
- name: Upload Build
  uses: actions/upload-artifact@v4
  with:
    name: build-files
    path: build/
```

**Explanation**

The upload action stores specified files after a job completes, making them available for download or use in later jobs.

**Where it is used in Production**

- Uploading compiled applications
- Saving deployment packages
- Storing generated reports

---

### Question 3

**Question**

How do you download artifacts in GitHub Actions?

**Answer**

Artifacts are downloaded using the `actions/download-artifact` action.

Example:

```yaml
- name: Download Build
  uses: actions/download-artifact@v4
  with:
    name: build-files
```

**Explanation**

Downloading artifacts allows subsequent jobs, such as deployment jobs, to reuse files generated during earlier stages.

**Where it is used in Production**

- Build → Test
- Build → Security Scan
- Build → Deployment

---

### Question 4

**Question**

What is Artifact Retention in GitHub Actions?

**Answer**

Artifact retention determines how long uploaded artifacts remain available before GitHub automatically deletes them.

**Explanation**

Retention policies help manage storage usage while ensuring important workflow outputs remain available for debugging or auditing.

**Where it is used in Production**

Organizations configure different retention periods for:

- Release builds
- Test reports
- Deployment packages
- Logs

---

### Question 5

**Question**

What is Dependency Caching in GitHub Actions?

**Answer**

Dependency caching stores downloaded dependencies so they can be reused in future workflow runs instead of downloading them again.

Examples include:

- npm packages
- Maven dependencies
- Gradle cache
- pip packages

**Explanation**

Caching significantly reduces workflow execution time by avoiding repeated downloads.

**Where it is used in Production**

Nearly every CI/CD pipeline uses dependency caching.

**Common Mistake**

Candidates often think caches should be used for build outputs. Build outputs belong in artifacts, not caches.

---

### Question 6

**Question**

How do you implement caching in GitHub Actions?

**Answer**

Caching is implemented using the `actions/cache` action.

Example:

```yaml
uses: actions/cache@v4
```

**Explanation**

The cache action stores dependency directories and restores them during future workflow runs when a matching cache key exists.

**Where it is used in Production**

- Node.js
- Java
- Python
- .NET
- Go projects

---

### Question 7

**Question**

What are Cache Keys?

**Answer**

Cache Keys uniquely identify cached data.

A cache is restored only when the key matches.

**Explanation**

Keys ensure workflows use the correct dependency cache and avoid using outdated packages.

**Where it is used in Production**

Projects commonly generate cache keys using dependency lock files such as:

- package-lock.json
- pom.xml
- requirements.txt

---

### Question 8

**Question**

What is Restore Cache in GitHub Actions?

**Answer**

Restore Cache retrieves a previously saved cache if a matching cache key exists.

If no match exists, dependencies are downloaded normally.

**Explanation**

Cache restoration speeds up workflow execution while maintaining correctness.

**Where it is used in Production**

Every CI/CD pipeline using dependency caching.

---

### Question 9

**Question**

What is the difference between Artifacts and Caching?

**Answer**

Artifacts store workflow outputs for later use or download.

Caching stores reusable dependencies to improve workflow performance.

**Explanation**

Artifacts support sharing generated files between jobs, while caches reduce build times by avoiding repeated downloads.

**Where it is used in Production**

- Artifacts → Build outputs
- Cache → Dependencies

---

### Question 10

**Question**

Why is dependency caching important in CI/CD pipelines?

**Answer**

Dependency caching:

- Reduces workflow duration
- Saves bandwidth
- Improves developer productivity
- Reduces infrastructure costs

**Explanation**

Large projects may download hundreds of megabytes of dependencies. Caching avoids repeating these downloads.

**Where it is used in Production**

Large enterprise projects with frequent builds.

---

### Question 11

**Question**

Can artifacts be shared between jobs?

**Answer**

Yes.

Artifacts uploaded in one job can be downloaded by another job within the same workflow.

**Explanation**

This enables separation of build, test, security scan, and deployment stages while avoiding rebuilding the application.

**Where it is used in Production**

Build once, deploy many pipelines.

---

### Question 12

**Question**

When should you use Artifacts instead of Caching?

**Answer**

Use Artifacts when you need to preserve generated files such as build packages or reports.

Use Caching when you want to speed up workflows by reusing dependencies.

**Explanation**

Choosing the correct mechanism improves workflow efficiency and reduces unnecessary storage usage.

**Where it is used in Production**

All enterprise CI/CD pipelines.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

Your Build job creates a JAR file, and your Deploy job needs the same file. How would you transfer it?

**Answer**

I would upload the JAR as an artifact in the Build job and download it in the Deploy job.

**Explanation**

Artifacts are designed to share workflow outputs between jobs without rebuilding the application.

---

### Scenario 2

**Question**

Your Node.js workflow spends several minutes downloading npm packages during every execution. How would you optimize it?

**Answer**

I would implement dependency caching using the `actions/cache` action.

**Explanation**

Caching downloaded packages significantly reduces workflow execution time.

---

### Scenario 3

**Question**

Your workflow is downloading dependencies even though caching is configured. What would you check first?

**Answer**

I would verify:

- Cache key
- Dependency path
- Lock file changes
- Cache hit status
- Workflow logs

**Explanation**

An incorrect cache key is the most common reason for cache misses.

---

### Scenario 4

**Question**

Your security team requires build logs and test reports to be available for seven days after every deployment. Which feature would you use?

**Answer**

I would upload them as artifacts and configure the appropriate artifact retention period.

**Explanation**

Artifacts preserve workflow outputs for auditing and troubleshooting.

---

### Scenario 5

**Question**

Your deployment job fails because it cannot find the application package created during the build stage. What is the likely issue?

**Answer**

The build job probably did not upload the package as an artifact, or the deployment job did not download it.

**Explanation**

Artifacts must be explicitly uploaded and downloaded between jobs.

---

### Scenario 6

**Question**

Your workflow restores an outdated dependency cache after updating `package-lock.json`. Why might this happen?

**Answer**

The cache key is likely not based on the lock file, causing old caches to be reused.

**Explanation**

Cache keys should include dependency files so caches are refreshed when dependencies change.

---

### Scenario 7

**Question**

A developer stores compiled application binaries in the cache instead of using artifacts. Is this the correct approach?

**Answer**

No.

Compiled binaries should be stored as artifacts, while caches should only store reusable dependencies.

**Explanation**

Caches are intended for performance optimization, not for transferring build outputs.

---

### Scenario 8

**Question**

A workflow uploads artifacts successfully, but they are unavailable after several weeks. What is the most likely reason?

**Answer**

The artifact retention period has expired, and GitHub automatically deleted the artifacts.

**Explanation**

Artifacts are retained only for the configured retention duration.

---

### Scenario 9

**Question**

Your Build, Security Scan, and Deployment jobs all need the same compiled package. What is the most efficient solution?

**Answer**

Build the application once, upload it as an artifact, and download it in the Security Scan and Deployment jobs.

**Explanation**

This follows the "build once, deploy many" principle used in production CI/CD pipelines.

---

### Scenario 10

**Question**

Your manager asks you to reduce GitHub Actions workflow execution time without changing the application code. What optimization would you implement first?

**Answer**

I would implement dependency caching and verify that cache keys are properly configured.

**Explanation**

Dependency downloads are one of the most common performance bottlenecks in CI/CD pipelines, and caching provides significant time savings with minimal configuration.
