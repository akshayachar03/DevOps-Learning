# Azure Repos Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is Azure Repos, and what is its purpose?

**Answer**

Azure Repos is the source code management service in Azure DevOps. It provides Git repositories and Team Foundation Version Control (TFVC) repositories to store, manage, version, and collaborate on source code.

Key features include:

- Git repositories
- Branching and merging
- Pull Requests
- Branch Policies
- Repository permissions
- Code reviews
- Commit history
- Integration with Azure Pipelines

**Explanation**

Azure Repos enables multiple developers to work on the same project without overwriting each other's changes. Every modification is tracked, making collaboration and rollback easier.

**Used in Production**

- Source code management
- Team collaboration
- Version control
- CI/CD integration

**Common Mistake**

Many candidates think Azure Repos only supports Git. It also supports TFVC, although Git is the preferred version control system for modern projects.

---

### Question 2

**Question**

What is the difference between Git and Azure Repos?

**Answer**

| Git | Azure Repos |
|------|-------------|
| Distributed Version Control System | Azure DevOps service that hosts Git repositories |
| Open-source tool | Cloud-hosted repository management platform |
| Manages source code locally | Provides collaboration, permissions, PRs, and policies |
| Can work without Azure DevOps | Uses Git as the underlying version control system |

**Explanation**

Git is the version control engine, while Azure Repos is a hosting platform that provides additional enterprise features around Git.

**Production Example**

Developers use Git commands (`clone`, `commit`, `push`, `pull`) while Azure Repos provides repository hosting, access control, and pull request workflows.

**Common Mistake**

Candidates often say Azure Repos is an alternative to Git. In reality, Azure Repos uses Git.

---

### Question 3

**Question**

What is a Git Repository?

**Answer**

A Git repository is a storage location that contains:

- Source code
- Commit history
- Branches
- Tags
- Configuration files

It tracks every change made to the project over time.

**Explanation**

Each repository maintains a complete history of the project, allowing developers to collaborate safely and restore previous versions when needed.

**Used in Production**

Each application or microservice generally has its own Git repository.

**Common Mistake**

Some candidates confuse a repository with a project. A project can contain multiple repositories.

---

### Question 4

**Question**

What is the purpose of cloning a repository?

**Answer**

Cloning creates a complete local copy of a remote Git repository, including:

- Source code
- Branches
- Commit history
- Tags

Example:

```bash
git clone https://dev.azure.com/organization/project/_git/app
```

**Explanation**

Developers work on the local copy and later push changes back to the remote repository.

**Used in Production**

Every developer clones the repository before starting development.

**Common Mistake**

Candidates often think cloning only downloads the latest files. It actually downloads the entire repository history.

---

### Question 5

**Question**

What is branching in Git, and why is it important?

**Answer**

A branch is an independent line of development.

It allows developers to:

- Develop new features
- Fix bugs
- Experiment safely
- Work simultaneously without affecting the main code

Common branches include:

- main
- develop
- feature/*
- release/*
- hotfix/*

**Explanation**

Branches isolate changes until they are tested and reviewed.

**Used in Production**

Feature development, bug fixes, release management, and hotfixes all rely on branching.

**Common Mistake**

Developers sometimes commit directly to the `main` branch instead of using feature branches.

---

### Question 6

**Question**

What is a commit in Git?

**Answer**

A commit is a snapshot of the project at a specific point in time.

Each commit contains:

- Modified files
- Commit message
- Author
- Timestamp
- Unique commit ID (SHA)

Example:

```bash
git commit -m "Fix login authentication issue"
```

**Explanation**

Commits record incremental changes, making it possible to track and revert modifications.

**Used in Production**

Developers create commits after completing logical units of work.

**Common Mistake**

Making very large commits with unrelated changes instead of small, meaningful commits.

---

### Question 7

**Question**

What is a Pull Request (PR)?

**Answer**

A Pull Request is a request to merge changes from one branch into another after review.

A typical PR includes:

- Code changes
- Review comments
- Approval status
- Build validation
- Merge option

**Explanation**

Pull Requests enforce code reviews and quality checks before merging code into shared branches.

**Used in Production**

Most organizations require all changes to `main` or `develop` to go through Pull Requests.

**Common Mistake**

Many candidates say PR merges code automatically. It is a review process; merging occurs only after approval and successful validations.

---

### Question 8

**Question**

What are Branch Policies in Azure Repos?

**Answer**

Branch Policies enforce quality and governance before allowing code to be merged.

Common policies include:

- Minimum reviewers
- Build validation
- Required approvals
- Linked work items
- Comment resolution
- Merge strategy restrictions

**Explanation**

These policies ensure that only reviewed and validated code reaches important branches.

**Used in Production**

Organizations commonly protect `main`, `master`, and `release` branches with branch policies.

**Common Mistake**

Candidates assume branch policies apply to all branches. They are configured per branch.

---

### Question 9

**Question**

What are Repository Permissions in Azure Repos?

**Answer**

Repository permissions control what users can do within a repository.

Examples include:

- Read
- Contribute
- Create branch
- Delete branch
- Force push
- Create tag
- Manage permissions

Permissions are typically assigned through security groups.

**Explanation**

Repository permissions help secure source code and prevent unauthorized changes.

**Used in Production**

Developers receive contributor access, while administrators have elevated permissions.

**Common Mistake**

Granting Force Push or Delete Repository permissions to all developers.

---

### Question 10

**Question**

What is the difference between Push and Pull in Git?

**Answer**

| Push | Pull |
|------|------|
| Uploads local changes to the remote repository | Downloads remote changes to the local repository |
| Local → Remote | Remote → Local |
| Shares your work | Synchronizes with teammates' work |

**Explanation**

Developers typically pull the latest changes before starting work and push their commits after completing tasks.

**Production Example**

```bash
git pull origin main
git push origin feature/login
```

**Common Mistake**

Pushing without first pulling the latest changes can result in merge conflicts.

---

### Question 11

**Question**

Why are code reviews important in Azure Repos?

**Answer**

Code reviews help:

- Detect bugs early
- Improve code quality
- Share knowledge
- Enforce coding standards
- Reduce production issues
- Ensure security best practices

They are usually performed through Pull Requests.

**Explanation**

A second set of eyes often identifies issues the original developer may have overlooked.

**Used in Production**

Most enterprise teams require at least one or two reviewers before merging code into protected branches.

**Common Mistake**

Treating code reviews as a formality instead of providing meaningful feedback.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

A developer accidentally commits directly to the `main` branch. How can this be prevented?

**Answer**

Implement branch policies by:

- Restricting direct pushes
- Requiring Pull Requests
- Enforcing reviewer approvals
- Enabling build validation
- Limiting permissions on the `main` branch

**Explanation**

Protected branches reduce the risk of unreviewed or unstable code reaching production.

---

### Scenario 2

**Question**

A developer cannot push code to Azure Repos and receives a permission error. What would you check?

**Answer**

Verify:

1. Repository permissions
2. Branch permissions
3. User's security group
4. Authentication (PAT or Entra ID)
5. Repository access
6. Branch policies preventing direct pushes

**Explanation**

Push failures are commonly caused by insufficient permissions or protected branch configurations.

---

### Scenario 3

**Question**

Two developers modified the same file and Git reports a merge conflict. How would you resolve it?

**Answer**

- Pull the latest changes.
- Review conflicting sections.
- Merge the correct changes manually.
- Test the application.
- Commit the resolved file.
- Push the updated branch.

**Explanation**

Merge conflicts occur when Git cannot automatically combine changes to the same lines of code.

---

### Scenario 4

**Question**

A Pull Request cannot be completed because build validation has failed. What should you do?

**Answer**

- Review the pipeline logs.
- Identify the failing build or test.
- Fix the issue.
- Commit the changes.
- Allow the pipeline to run again.
- Merge only after successful validation.

**Explanation**

Build validation ensures only compilable and tested code is merged.

---

### Scenario 5

**Question**

Your team has 50 developers working on the same application. How would you organize branching?

**Answer**

Use a branching strategy such as:

- main
- develop
- feature/*
- release/*
- hotfix/*

Require Pull Requests and branch policies for protected branches.

**Explanation**

A structured branching model improves collaboration and reduces integration issues.

---

### Scenario 6

**Question**

A developer accidentally deletes an important branch. How would you recover it?

**Answer**

- Check if the branch still exists remotely.
- Use the commit history or reflog to locate the latest commit.
- Recreate the branch from the last valid commit.
- Restore branch protections if necessary.

**Explanation**

Git stores commit history, making branch recovery possible if the commits still exist.

---

### Scenario 7

**Question**

Your organization wants every code change to be reviewed by at least two developers before merging. How would you implement this?

**Answer**

Configure branch policies to:

- Require a minimum of two reviewers.
- Require comments to be resolved.
- Enforce successful build validation.
- Block direct pushes to protected branches.

**Explanation**

This ensures consistent code quality and reduces production defects.

---

### Scenario 8

**Question**

A developer force-pushes to a shared branch and overwrites other developers' work. How can this be prevented?

**Answer**

- Remove Force Push permissions.
- Protect shared branches.
- Require Pull Requests.
- Limit administrative access.
- Educate developers on safe Git workflows.

**Explanation**

Force pushing rewrites commit history and can permanently remove teammates' work if misused.

---

### Scenario 9

**Question**

A developer says they cloned the repository yesterday, but today their code is outdated. What should they do?

**Answer**

They should synchronize with the remote repository by:

```bash
git pull origin main
```

or update the appropriate working branch before starting new work.

**Explanation**

Cloning is a one-time operation. Afterward, developers must regularly pull the latest changes to stay in sync.

---

### Scenario 10

**Question**

A junior developer opens a Pull Request containing 2,000 changed files. What feedback would you provide?

**Answer**

Recommend:

- Splitting work into smaller feature branches.
- Creating smaller, focused Pull Requests.
- Using meaningful commit messages.
- Submitting incremental changes.

**Explanation**

Large Pull Requests are difficult to review, increase the chance of defects, and slow down the development process.

---

### Scenario 11

**Question**

Your security team reports that several developers have Contributor access to repositories they do not work on. How would you address this?

**Answer**

- Review repository permissions.
- Audit security groups.
- Remove unnecessary access.
- Apply the principle of least privilege.
- Perform periodic permission reviews.
- Document repository ownership.

**Explanation**

Limiting repository access reduces the risk of accidental changes and strengthens source code security. Regular access reviews are a common governance practice in enterprise environments.
