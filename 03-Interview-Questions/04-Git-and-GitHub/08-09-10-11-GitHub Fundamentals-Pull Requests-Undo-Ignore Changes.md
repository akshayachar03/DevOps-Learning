# GitHub Fundamentals, Pull Requests, Undoing Changes & Ignoring Files Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is GitHub, and how is it different from Git?

**Answer**

Git is a distributed version control system used to track code changes locally.

GitHub is a cloud-based platform that hosts Git repositories and provides collaboration features such as:

- Remote repositories
- Pull Requests
- Code Reviews
- Issue Tracking
- Branch Protection
- CI/CD Integrations

**Explanation**

Git manages version control, while GitHub provides a collaborative platform built around Git.

**Used in Production**

Almost every modern software team uses GitHub, Azure Repos, GitLab, or Bitbucket for collaboration.

**Common Mistake**

Many candidates incorrectly use Git and GitHub interchangeably.

---

### Question 2

**Question**

What is a GitHub Repository?

**Answer**

A GitHub Repository is a remote Git repository hosted on GitHub.

It stores:

- Source code
- Commit history
- Branches
- Pull Requests
- Issues
- Releases
- Documentation

**Explanation**

It acts as the central collaboration point for a development team.

**Used in Production**

All developers synchronize their local repositories with GitHub repositories.

---

### Question 3

**Question**

What is the difference between Public and Private Repositories?

**Answer**

| Public Repository | Private Repository |
|-------------------|-------------------|
| Anyone can view the code | Only authorized users can access |
| Suitable for open-source projects | Suitable for enterprise projects |
| Public collaboration | Restricted collaboration |

**Explanation**

Repository visibility determines who can access the source code.

**Used in Production**

Most enterprise repositories are private.

---

### Question 4

**Question**

What is the difference between Forking and Cloning?

**Answer**

| Fork | Clone |
|------|-------|
| Creates your own copy on GitHub | Creates a local copy on your computer |
| Happens on GitHub | Happens on your local machine |
| Used for contributing to external projects | Used for local development |

Clone example:

```bash
git clone https://github.com/user/project.git
```

**Explanation**

Forking creates a new remote repository under your account, while cloning downloads a repository locally.

**Used in Production**

Forks are common in open-source development.

**Common Mistake**

Many candidates confuse forks with branches.

---

### Question 5

**Question**

What is a Pull Request (PR)?

**Answer**

A Pull Request is a request to merge changes from one branch into another after review.

It includes:

- Code changes
- Discussion
- Review comments
- Approval status
- CI/CD results

**Explanation**

Pull Requests enable collaboration and code quality checks before merging.

**Used in Production**

Most enterprise teams require Pull Requests before merging into the main branch.

---

### Question 6

**Question**

What is the typical Pull Request review process?

**Answer**

Typical workflow:

1. Create feature branch.
2. Commit changes.
3. Push branch.
4. Create Pull Request.
5. Code review.
6. CI/CD validation.
7. Approval.
8. Merge.
9. Delete feature branch.

**Explanation**

The review process improves code quality and knowledge sharing.

**Used in Production**

Mandatory in most enterprise Git workflows.

---

### Question 7

**Question**

How do you merge a Pull Request?

**Answer**

After approval:

- Review changes.
- Ensure CI/CD passes.
- Click **Merge Pull Request**.
- Delete the feature branch if no longer needed.

**Explanation**

GitHub merges the approved branch into the target branch.

**Used in Production**

Merges typically require successful builds and approvals.

---

### Question 8

**Question**

What is the difference between `git restore`, `git reset`, and `git revert`?

**Answer**

| Command | Purpose |
|----------|---------|
| `git restore` | Restore file changes |
| `git reset` | Move HEAD and optionally unstage/remove commits |
| `git revert` | Create a new commit that reverses an earlier commit |

Examples:

```bash
git restore file.txt
```

```bash
git reset HEAD file.txt
```

```bash
git revert HEAD
```

**Explanation**

Each command serves a different purpose when undoing changes.

**Used in Production**

`git revert` is preferred for shared branches because it preserves commit history.

**Common Mistake**

Using `git reset` on shared branches can rewrite history and disrupt collaborators.

---

### Question 9

**Question**

What is the purpose of `git commit --amend`?

**Answer**

`git commit --amend` modifies the most recent commit.

Example:

```bash
git commit --amend
```

It can:

- Change the commit message.
- Include forgotten staged changes.

**Explanation**

Useful for correcting the latest commit before it is shared.

**Used in Production**

Frequently used before pushing commits.

---

### Question 10

**Question**

What is the purpose of the `.gitignore` file?

**Answer**

`.gitignore` specifies files and directories that Git should not track.

Example:

```text
*.log
node_modules/
.env
```

**Explanation**

It prevents unnecessary or sensitive files from being committed.

**Used in Production**

Commonly ignores:

- Build artifacts
- Logs
- Temporary files
- Secrets
- Dependency directories

---

### Question 11

**Question**

What is a Global Git Ignore File?

**Answer**

A Global Ignore File applies ignore rules across all Git repositories on a developer's machine.

Example configuration:

```bash
git config --global core.excludesfile ~/.gitignore_global
```

**Explanation**

Useful for ignoring editor files and operating system files across every repository.

**Used in Production**

Developers often ignore:

- `.DS_Store`
- `Thumbs.db`
- IDE configuration files

**Common Mistake**

Candidates often confuse repository-specific `.gitignore` files with global ignore files.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

Your company wants only employees to access the application source code. Which repository visibility should you choose?

**Answer**

A Private Repository.

**Explanation**

Private repositories restrict access to authorized users.

---

### Scenario 2

**Question**

You want to contribute to an open-source project but do not have write access. What should you do?

**Answer**

Fork the repository, clone your fork locally, make changes, and create a Pull Request.

**Explanation**

Forking allows contributors to work independently before proposing changes.

---

### Scenario 3

**Question**

Your feature is complete, and your company requires code review before merging into the `main` branch. What should you do?

**Answer**

Create a Pull Request and request reviewers.

**Explanation**

The review process ensures code quality and team collaboration.

---

### Scenario 4

**Question**

A reviewer requests changes to your Pull Request. Can you update the existing PR?

**Answer**

Yes.

Make the required changes, commit them, and push to the same branch. The Pull Request updates automatically.

**Explanation**

There is no need to create a new Pull Request.

---

### Scenario 5

**Question**

You accidentally modified a local file but have not committed it. You want to discard the changes. Which command should you use?

**Answer**

```bash
git restore filename
```

**Explanation**

`git restore` discards uncommitted changes in the working directory.

---

### Scenario 6

**Question**

You accidentally staged the wrong file but have not committed it yet. Which command should you use?

**Answer**

```bash
git reset HEAD filename
```

**Explanation**

This removes the file from the staging area without deleting the local changes.

---

### Scenario 7

**Question**

A faulty commit has already been pushed to the shared repository. What is the safest way to undo it?

**Answer**

Use:

```bash
git revert <commit-id>
```

**Explanation**

`git revert` creates a new commit that reverses the earlier changes while preserving history, making it the preferred approach for shared repositories.

---

### Scenario 8

**Question**

You notice a spelling mistake in your most recent commit message, and the commit has not been pushed yet. What should you do?

**Answer**

Run:

```bash
git commit --amend
```

**Explanation**

This updates the latest commit without creating a new one.

---

### Scenario 9

**Question**

Your application contains a `.env` file with production credentials. How can you prevent it from being committed?

**Answer**

Add it to `.gitignore`:

```text
.env
```

**Explanation**

Sensitive configuration files should never be tracked by Git.

---

### Scenario 10

**Question**

Every repository on your workstation contains unnecessary IDE configuration files that you never want Git to track. What is the best solution?

**Answer**

Configure a Global Git Ignore File:

```bash
git config --global core.excludesfile ~/.gitignore_global
```

**Explanation**

Global ignore rules automatically apply to every repository on your machine.

---

### Scenario 11

**Question**

You are contributing a new feature to your company's GitHub repository. Your workflow requires you to clone the repository, create a feature branch, implement changes, submit them for review, address reviewer feedback, merge the approved Pull Request, and ensure sensitive files are not committed. Describe the complete workflow.

**Answer**

A typical workflow includes:

1. Clone the repository:

```bash
git clone https://github.com/company/project.git
```

2. Create a feature branch:

```bash
git switch -c feature-payment
```

3. Develop the feature.

4. Stage and commit changes:

```bash
git add .
git commit -m "Implement payment feature"
```

5. Push the branch:

```bash
git push -u origin feature-payment
```

6. Create a Pull Request.

7. Respond to review comments by making additional commits and pushing them to the same branch.

8. After approvals and successful CI/CD validation, merge the Pull Request.

9. Delete the feature branch.

10. Ensure sensitive or unnecessary files such as `.env`, logs, and build artifacts are listed in `.gitignore` before committing.

11. If a mistake is discovered after sharing the code, prefer `git revert` over `git reset` to safely undo changes on shared branches.

**Explanation**

This workflow reflects the standard enterprise GitHub collaboration model used by DevOps, Cloud, Platform, and Software Engineering teams. It demonstrates practical knowledge of repository management, Pull Requests, collaborative reviews, safe methods for undoing changes, and proper use of `.gitignore` to protect sensitive files and maintain clean repositories.
