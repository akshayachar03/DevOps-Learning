# Branching & Merging Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is a Git Branch, and why is it used?

**Answer**

A Git branch is an independent line of development that allows developers to work on new features, bug fixes, or experiments without affecting the main codebase.

Key benefits:

- Isolates development work
- Enables parallel development
- Reduces the risk of breaking production code
- Simplifies collaboration
- Supports feature-based workflows

**Explanation**

A branch acts as a pointer to a series of commits. Each branch maintains its own commit history until it is merged into another branch.

**Used in Production**

Teams create separate branches for features, bug fixes, releases, and hotfixes.

**Common Mistake**

Many candidates think a branch creates a copy of the entire project. Git branches are lightweight pointers, not full copies.

---

### Question 2

**Question**

How do you create a new branch in Git?

**Answer**

Create a branch:

```bash
git branch feature-login
```

Create and switch in one command:

```bash
git checkout -b feature-login
```

or (modern command)

```bash
git switch -c feature-login
```

**Explanation**

Creating a branch allows developers to work independently without modifying the main branch.

**Used in Production**

Every new feature typically starts with a dedicated branch.

---

### Question 3

**Question**

How do you switch between branches?

**Answer**

Using the modern command:

```bash
git switch feature-login
```

Using the older command:

```bash
git checkout feature-login
```

**Explanation**

Switching changes the working directory to match the selected branch.

**Used in Production**

Developers switch between feature, release, and hotfix branches multiple times a day.

---

### Question 4

**Question**

How do you rename a Git branch?

**Answer**

Rename the current branch:

```bash
git branch -m new-name
```

Rename another branch:

```bash
git branch -m old-name new-name
```

**Explanation**

Renaming improves consistency and follows branch naming standards.

**Used in Production**

Teams rename branches to match issue IDs or project conventions.

---

### Question 5

**Question**

How do you delete a Git branch?

**Answer**

Delete a merged branch:

```bash
git branch -d feature-login
```

Force delete:

```bash
git branch -D feature-login
```

**Explanation**

Deleting old branches keeps repositories organized.

**Used in Production**

Feature branches are commonly deleted after successful merges.

**Common Mistake**

Using `-D` without understanding that it deletes unmerged work.

---

### Question 6

**Question**

How do you list all Git branches?

**Answer**

List local branches:

```bash
git branch
```

List remote branches:

```bash
git branch -r
```

List both:

```bash
git branch -a
```

**Explanation**

Listing branches helps developers identify available development streams.

**Used in Production**

Developers frequently verify branch names before switching or merging.

---

### Question 7

**Question**

What is a Fast-Forward Merge?

**Answer**

A Fast-Forward Merge occurs when the target branch has no new commits since the feature branch was created.

Example:

```bash
git merge feature-login
```

Git simply moves the branch pointer forward.

**Explanation**

No merge commit is created because the history is linear.

**Used in Production**

Common when feature branches are merged immediately after development.

---

### Question 8

**Question**

What is a Three-Way Merge?

**Answer**

A Three-Way Merge occurs when both branches have new commits.

Git combines:

- Common ancestor
- Target branch
- Feature branch

A merge commit is created.

**Explanation**

This preserves the complete development history.

**Used in Production**

Frequently occurs when multiple developers work simultaneously.

---

### Question 9

**Question**

What is a Merge Conflict?

**Answer**

A Merge Conflict occurs when Git cannot automatically combine changes because the same section of a file was modified differently in two branches.

**Explanation**

Git pauses the merge and requires manual conflict resolution.

**Used in Production**

Merge conflicts are common in collaborative development environments.

**Common Mistake**

Many candidates think merge conflicts indicate Git failure. They are a normal part of collaborative development.

---

### Question 10

**Question**

How do you resolve a Merge Conflict?

**Answer**

Typical process:

1. Identify conflicted files.
2. Open the file.
3. Review conflict markers.
4. Keep the correct changes.
5. Remove conflict markers.
6. Save the file.
7. Stage the resolved file.

```bash
git add filename
```

8. Complete the merge.

```bash
git commit
```

**Explanation**

Manual review ensures the correct version of the code is preserved.

**Used in Production**

Developers regularly resolve conflicts during feature integration.

---

### Question 11

**Question**

What are some best practices for Git branching and merging?

**Answer**

Best practices include:

- Create a branch for every feature.
- Keep branches short-lived.
- Commit frequently.
- Pull the latest changes before merging.
- Use meaningful branch names.
- Delete merged branches.
- Review code before merging.
- Resolve conflicts carefully.
- Avoid committing directly to the main branch.
- Test thoroughly before merging.

**Explanation**

Following these practices reduces merge conflicts and improves collaboration.

**Used in Production**

Most organizations enforce these practices through branch policies and code reviews.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

Your manager assigns you a new feature while the main branch contains production code. How should you begin development?

**Answer**

Create a new feature branch:

```bash
git switch -c feature-payment
```

**Explanation**

Feature branches isolate development and protect the production branch.

---

### Scenario 2

**Question**

You accidentally started development on the main branch. What should you do?

**Answer**

Create a new branch immediately:

```bash
git switch -c feature-login
```

Continue development there before making further commits.

**Explanation**

Feature work should not continue directly on the main branch.

---

### Scenario 3

**Question**

You finished developing a feature, and the main branch has not changed since you created the feature branch. What type of merge will occur?

**Answer**

A Fast-Forward Merge.

**Explanation**

Git simply moves the branch pointer without creating a merge commit.

---

### Scenario 4

**Question**

Two developers modify the same section of the same file in different branches. What happens when the branches are merged?

**Answer**

Git reports a Merge Conflict.

**Explanation**

Manual conflict resolution is required because Git cannot determine which changes should be kept.

---

### Scenario 5

**Question**

A merged feature branch is no longer needed. Which command should you use?

**Answer**

Delete the branch:

```bash
git branch -d feature-login
```

**Explanation**

Removing merged branches keeps the repository clean.

---

### Scenario 6

**Question**

You attempt to delete a branch, but Git reports that it has not been fully merged. Why?

**Answer**

Git protects unmerged commits from accidental deletion.

If deletion is intentional:

```bash
git branch -D feature-login
```

**Explanation**

Force deletion should only be used after confirming the branch is no longer required.

---

### Scenario 7

**Question**

Your teammate asks which branches currently exist in the repository. Which command would you use?

**Answer**

List all local branches:

```bash
git branch
```

List all branches:

```bash
git branch -a
```

**Explanation**

These commands display available local and remote branches.

---

### Scenario 8

**Question**

A feature branch has become outdated because several new commits were added to the main branch. What should you do before merging?

**Answer**

Switch to the main branch, pull the latest changes, then merge or rebase the feature branch as per the team's workflow.

**Explanation**

Updating the branch before merging reduces the likelihood of conflicts and ensures compatibility with the latest codebase.

---

### Scenario 9

**Question**

While resolving a merge conflict, you notice conflict markers such as `<<<<<<<` and `>>>>>>>` in the file. What do they indicate?

**Answer**

They indicate sections where Git found conflicting changes between branches.

You should:

- Review both versions.
- Keep the correct code.
- Remove the conflict markers.
- Stage the resolved file.
- Complete the merge.

**Explanation**

Conflict markers are temporary indicators used during manual conflict resolution.

---

### Scenario 10

**Question**

Your team has completed development for a feature, and the branch has already been merged into the main branch. What housekeeping task should be performed?

**Answer**

Delete the merged feature branch:

```bash
git branch -d feature-name
```

Optionally delete the remote branch if it is no longer needed.

**Explanation**

Cleaning up merged branches keeps the repository organized and reduces confusion.

---

### Scenario 11

**Question**

Your team follows a feature-branch workflow. You are assigned a new feature while several other developers are simultaneously working on different features. Describe the complete Git workflow from creating the branch until the feature is merged into the main branch.

**Answer**

A typical workflow includes:

1. Update the local main branch.
2. Create a new feature branch:

```bash
git switch -c feature-payment
```

3. Develop the feature.
4. Commit changes regularly:

```bash
git add .
git commit -m "Implement payment feature"
```

5. Periodically synchronize with the latest changes from the main branch to minimize conflicts.
6. After development and testing are complete, merge the feature branch into the main branch.
7. If no new commits exist on the main branch, Git performs a Fast-Forward Merge; otherwise, it performs a Three-Way Merge.
8. Resolve any merge conflicts if they occur.
9. Verify the application after the merge.
10. Delete the merged feature branch:

```bash
git branch -d feature-payment
```

**Explanation**

This workflow reflects the standard development process used by DevOps, Cloud, Platform, and Software Engineering teams. Understanding branch creation, switching, merging strategies, conflict resolution, and branch cleanup is a core expectation in Git interviews because these activities are performed daily in collaborative software development.
