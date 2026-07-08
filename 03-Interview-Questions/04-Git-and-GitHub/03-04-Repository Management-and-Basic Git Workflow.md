# Repository Management & Basic Git Workflow Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is a Git Repository?

**Answer**

A Git Repository (repo) is a directory that contains project files along with Git metadata required to track version history, branches, commits, and other repository information.

A repository can be:

- Local Repository
- Remote Repository

**Explanation**

A Git repository stores both the project files and their complete change history, enabling developers to collaborate efficiently.

**Used in Production**

Every software application, Infrastructure as Code (Terraform), Kubernetes manifests, CI/CD pipelines, and configuration files are stored in Git repositories.

**Common Mistake**

Many candidates think a repository only contains source code. It also contains Git metadata and version history.

---

### Question 2

**Question**

What is the purpose of the `git init` command?

**Answer**

`git init` initializes a new Git repository in the current directory.

Example:

```bash
git init
```

**Explanation**

The command creates a hidden `.git` directory that enables Git version control for the project.

**Used in Production**

Used when starting a new project or converting an existing project into a Git repository.

**Common Mistake**

Candidates often believe `git init` downloads code from GitHub. It only initializes a local repository.

---

### Question 3

**Question**

What is the difference between `git init` and `git clone`?

**Answer**

| `git init` | `git clone` |
|-------------|-------------|
| Creates a new empty repository | Copies an existing repository |
| No remote repository required | Requires an existing remote repository |
| Used for new projects | Used to join existing projects |

Example:

```bash
git init
```

```bash
git clone https://github.com/user/project.git
```

**Explanation**

`git init` starts version control from scratch, while `git clone` downloads an existing repository along with its history.

**Used in Production**

Most developers use `git clone` daily to work on existing projects.

---

### Question 4

**Question**

What does the `git clone` command do?

**Answer**

`git clone` creates a complete local copy of a remote repository, including:

- Source code
- Commit history
- Branches
- Tags
- Remote configuration

Example:

```bash
git clone https://github.com/user/project.git
```

**Explanation**

The cloned repository is immediately ready for development.

**Used in Production**

Developers clone repositories before contributing code.

---

### Question 5

**Question**

What is the purpose of the `.git` directory?

**Answer**

The `.git` directory stores Git metadata such as:

- Commit history
- Branch information
- Tags
- Configuration
- References
- Object database

**Explanation**

This directory is the core of the Git repository. Without it, Git cannot track project history.

**Used in Production**

Every Git repository contains a `.git` directory.

**Common Mistake**

Never manually edit or delete files inside `.git` unless you fully understand Git internals.

---

### Question 6

**Question**

What is the purpose of the `git status` command?

**Answer**

`git status` displays the current state of the repository.

Example:

```bash
git status
```

It shows:

- Modified files
- New files
- Deleted files
- Staged changes
- Current branch

**Explanation**

It helps developers understand what will be included in the next commit.

**Used in Production**

One of the most frequently executed Git commands.

---

### Question 7

**Question**

What is the purpose of the `git add` command?

**Answer**

`git add` moves changes from the Working Tree to the Staging Area.

Example:

```bash
git add app.py
```

Stage all files:

```bash
git add .
```

**Explanation**

Only staged files are included in the next commit.

**Used in Production**

Developers selectively stage changes before committing.

**Common Mistake**

Many candidates think `git add` permanently saves changes. It only stages them.

---

### Question 8

**Question**

What is the purpose of the `git commit` command?

**Answer**

`git commit` permanently records staged changes in the Local Repository.

Example:

```bash
git commit -m "Add login feature"
```

**Explanation**

Each commit represents a logical snapshot of the project.

**Used in Production**

Developers create meaningful commits throughout development.

**Common Mistake**

Attempting to commit without staging changes first.

---

### Question 9

**Question**

What is the purpose of the `git log` command?

**Answer**

`git log` displays commit history.

Example:

```bash
git log
```

Compact view:

```bash
git log --oneline
```

**Explanation**

The log helps developers review project history and identify previous changes.

**Used in Production**

Frequently used during debugging and code reviews.

---

### Question 10

**Question**

What is the purpose of the `git diff` command?

**Answer**

`git diff` shows differences between files or commits.

Example:

```bash
git diff
```

Compare staged changes:

```bash
git diff --staged
```

**Explanation**

It allows developers to review modifications before committing.

**Used in Production**

Helps prevent accidental commits and improves code quality.

---

### Question 11

**Question**

What is the purpose of the `git show` command?

**Answer**

`git show` displays detailed information about a commit.

Example:

```bash
git show
```

View a specific commit:

```bash
git show <commit-id>
```

It displays:

- Commit message
- Author
- Date
- File changes
- Code differences

**Explanation**

Useful for understanding exactly what changed in a commit.

**Used in Production**

Developers use it to inspect recent commits and troubleshoot issues.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

Your manager gives you an existing GitHub repository and asks you to start working on it. Which command would you use?

**Answer**

Clone the repository:

```bash
git clone https://github.com/company/project.git
```

**Explanation**

Cloning downloads the complete repository, including its history and branches.

---

### Scenario 2

**Question**

You have created a new application on your local machine and want to start tracking changes with Git. Which command would you use?

**Answer**

Initialize the repository:

```bash
git init
```

**Explanation**

This creates the `.git` directory and enables version control.

---

### Scenario 3

**Question**

You modified several files and want to know which ones have changed before committing. Which command would you use?

**Answer**

Run:

```bash
git status
```

**Explanation**

It shows modified, staged, and untracked files.

---

### Scenario 4

**Question**

You accidentally modified a configuration file and want to review the changes before committing. Which command would you use?

**Answer**

Run:

```bash
git diff
```

**Explanation**

Reviewing differences helps prevent accidental commits.

---

### Scenario 5

**Question**

A teammate asks whether a file has already been staged for commit. How would you verify this?

**Answer**

Run:

```bash
git status
```

**Explanation**

The output clearly separates staged and unstaged changes.

---

### Scenario 6

**Question**

Your commit command reports "nothing to commit." What is the most likely reason?

**Answer**

Possible reasons include:

- No files were modified.
- Changes were not staged.
- All changes have already been committed.

Check:

```bash
git status
```

**Explanation**

`git status` provides the current repository state.

---

### Scenario 7

**Question**

A developer wants to review all previous commits before debugging a production issue. Which command should they use?

**Answer**

Run:

```bash
git log
```

or

```bash
git log --oneline
```

**Explanation**

The commit history helps identify when changes were introduced.

---

### Scenario 8

**Question**

You need to inspect the exact changes introduced by a specific commit. Which command would you use?

**Answer**

Run:

```bash
git show <commit-id>
```

**Explanation**

This displays the commit metadata and code differences.

---

### Scenario 9

**Question**

A new developer accidentally deletes the `.git` directory while cleaning the project folder. What happens?

**Answer**

The project files remain, but Git version control information—including commit history, branches, and configuration—is lost.

**Explanation**

The `.git` directory is essential because it stores all Git metadata.

---

### Scenario 10

**Question**

You staged multiple files but realized one contains incomplete work. How would you identify the staged files before committing?

**Answer**

Run:

```bash
git status
```

Optionally review staged changes:

```bash
git diff --staged
```

**Explanation**

These commands help verify exactly what will be included in the next commit.

---

### Scenario 11

**Question**

You join a DevOps project where the application source code is stored in GitHub. Your task is to download the repository, review its current status, make code changes, inspect those changes, stage them, create a commit, and verify the commit history before pushing. Describe the complete workflow.

**Answer**

A typical workflow is:

1. Clone the repository:

```bash
git clone https://github.com/company/project.git
```

2. Move into the project directory.

3. Check repository status:

```bash
git status
```

4. Modify the required files.

5. Review changes:

```bash
git diff
```

6. Stage the desired files:

```bash
git add .
```

or

```bash
git add filename
```

7. Create a commit:

```bash
git commit -m "Implement new feature"
```

8. Review commit history:

```bash
git log --oneline
```

9. Inspect the latest commit if needed:

```bash
git show
```

**Explanation**

This sequence represents the standard daily Git workflow followed by developers, DevOps engineers, and platform engineers. Interviewers frequently ask candidates to explain this end-to-end workflow because it demonstrates a practical understanding of repository management, staging, committing, and reviewing changes before collaboration with the rest of the team.
