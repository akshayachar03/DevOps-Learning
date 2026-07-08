# Git Troubleshooting Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is a Merge Conflict, and why does it occur?

**Answer**

A Merge Conflict occurs when Git cannot automatically merge changes because the same portion of a file has been modified differently in two branches.

Common causes include:

- Two developers modifying the same lines.
- One developer deletes a file while another modifies it.
- Simultaneous changes during a merge or pull operation.

**Explanation**

Git attempts to merge changes automatically. When it cannot determine which version should be kept, it marks the file as conflicted and requires manual resolution.

**Used in Production**

Merge conflicts are common in collaborative development and are expected in large teams.

**Common Mistake**

Many candidates believe merge conflicts indicate repository corruption. They are a normal part of team-based development.

---

### Question 2

**Question**

How do you resolve a Merge Conflict?

**Answer**

Steps:

1. Open the conflicted file.
2. Locate conflict markers:

```text
<<<<<<< HEAD
Current code
=======
Incoming code
>>>>>>> feature-branch
```

3. Choose or combine the correct code.
4. Remove the conflict markers.
5. Save the file.
6. Stage the resolved file:

```bash
git add filename
```

7. Complete the merge:

```bash
git commit
```

**Explanation**

Git pauses the merge process until conflicts are resolved manually.

**Used in Production**

Frequently performed during feature branch integration.

---

### Question 3

**Question**

What is a Detached HEAD state?

**Answer**

A Detached HEAD state occurs when HEAD points directly to a commit instead of a branch.

Example:

```bash
git checkout <commit-id>
```

In this state:

- You can inspect old commits.
- New commits are not attached to any branch.

**Explanation**

Git allows viewing historical commits without switching to a branch.

**Used in Production**

Useful for debugging or inspecting previous releases.

**Common Mistake**

Creating commits in a Detached HEAD state without creating a branch first can make those commits difficult to find later.

---

### Question 4

**Question**

How do you recover from a Detached HEAD state?

**Answer**

If you want to keep your work:

Create a new branch:

```bash
git switch -c recovery-branch
```

If you only want to return:

```bash
git switch main
```

**Explanation**

Creating a branch preserves commits made while in the Detached HEAD state.

---

### Question 5

**Question**

What are common Git Authentication Issues?

**Answer**

Common authentication problems include:

- Invalid Personal Access Token (PAT)
- Incorrect SSH key
- Missing SSH key registration
- Expired credentials
- Incorrect remote URL
- Repository permission issues

**Explanation**

Authentication failures usually occur before Git communicates with the repository.

**Used in Production**

Very common when configuring new developer machines.

---

### Question 6

**Question**

Why does Git display a "Push Rejected" error?

**Answer**

Common reasons include:

- Remote branch has newer commits.
- Branch protection rules.
- Permission issues.
- Non-fast-forward updates.

Typical solution:

```bash
git pull
```

Resolve conflicts if necessary, then:

```bash
git push
```

**Explanation**

Git prevents overwriting commits that exist only in the remote repository.

**Common Mistake**

Using `git push --force` without understanding its impact.

---

### Question 7

**Question**

Why do Pull Conflicts occur?

**Answer**

Pull conflicts occur when:

- Local changes conflict with remote changes.
- `git pull` performs a merge that Git cannot complete automatically.

**Explanation**

`git pull` is effectively:

```bash
git fetch
git merge
```

If merging fails, conflicts must be resolved manually.

**Used in Production**

Common after multiple developers modify the same files.

---

### Question 8

**Question**

How can you recover a lost commit?

**Answer**

Use:

```bash
git reflog
```

Locate the commit:

```bash
git checkout <commit-id>
```

or create a branch:

```bash
git switch -c recovered-work <commit-id>
```

**Explanation**

Git records recent HEAD movements in the reflog, allowing recovery of many "lost" commits.

**Used in Production**

Frequently used after accidental resets or branch deletions.

---

### Question 9

**Question**

What is `git reflog`, and when should you use it?

**Answer**

`git reflog` displays the history of HEAD movements.

Example:

```bash
git reflog
```

It helps recover:

- Lost commits
- Deleted branches
- Accidental resets
- Detached HEAD work

**Explanation**

Unlike `git log`, reflog includes commits that may no longer be referenced by branches.

---

### Question 10

**Question**

How can you identify the cause of a Git problem before attempting a fix?

**Answer**

Useful diagnostic commands:

```bash
git status
```

```bash
git log
```

```bash
git branch
```

```bash
git remote -v
```

```bash
git diff
```

**Explanation**

These commands provide information about the repository state, branch, remotes, and pending changes.

**Used in Production**

Experienced developers inspect the repository before making corrective changes.

---

### Question 11

**Question**

What are some best practices for avoiding common Git issues?

**Answer**

Best practices include:

- Pull frequently.
- Commit small, focused changes.
- Use feature branches.
- Resolve conflicts promptly.
- Never force-push to shared branches without approval.
- Review changes using `git diff`.
- Verify repository status using `git status`.
- Tag production releases.

**Explanation**

These practices reduce merge conflicts, accidental overwrites, and deployment errors.

**Common Mistake**

Developers often work on outdated branches for extended periods, increasing the likelihood of conflicts.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

You attempt to merge your feature branch into `main`, and Git reports a merge conflict. What steps would you take?

**Answer**

1. Open the conflicted files.
2. Review the conflict markers.
3. Keep or combine the appropriate code.
4. Remove the markers.
5. Stage the resolved files:

```bash
git add filename
```

6. Complete the merge:

```bash
git commit
```

**Explanation**

Manual conflict resolution ensures both developers' changes are correctly integrated.

---

### Scenario 2

**Question**

You accidentally checked out an old commit and now Git reports that you are in a Detached HEAD state. How do you continue working safely?

**Answer**

Create a branch:

```bash
git switch -c feature-recovery
```

**Explanation**

This attaches future commits to a branch and preserves your work.

---

### Scenario 3

**Question**

When pushing your branch, Git displays:

```text
! [rejected] non-fast-forward
```

How would you resolve this?

**Answer**

Update your local branch:

```bash
git pull
```

Resolve any conflicts.

Push again:

```bash
git push
```

**Explanation**

The remote repository contains commits that your local branch does not.

---

### Scenario 4

**Question**

GitHub suddenly rejects your HTTPS authentication, even though it worked yesterday. What would you investigate?

**Answer**

Check:

- PAT validity
- PAT expiration
- Repository permissions
- Remote URL
- Credential manager

**Explanation**

Authentication failures are usually caused by expired credentials or permission changes.

---

### Scenario 5

**Question**

After running `git pull`, Git reports merge conflicts. What should you do next?

**Answer**

Resolve the conflicts manually.

Then:

```bash
git add .
git commit
```

**Explanation**

Git pauses the merge until all conflicts are resolved.

---

### Scenario 6

**Question**

You accidentally deleted a branch containing important commits. Can the work still be recovered?

**Answer**

Yes.

Run:

```bash
git reflog
```

Locate the commit.

Recover it:

```bash
git switch -c recovered-work <commit-id>
```

**Explanation**

The reflog maintains a history of recent HEAD movements, allowing recovery in many cases.

---

### Scenario 7

**Question**

A teammate force-pushed changes to the shared branch, and your local history no longer matches the remote repository. How would you investigate the issue?

**Answer**

Use:

```bash
git fetch
```

Compare branches:

```bash
git log
```

Review repository history before deciding how to synchronize your branch.

**Explanation**

Fetching first prevents accidental overwriting of history.

---

### Scenario 8

**Question**

You accidentally committed work while in a Detached HEAD state and then switched back to `main`. How can you recover those commits?

**Answer**

Run:

```bash
git reflog
```

Find the detached commit.

Create a branch:

```bash
git switch -c recovered-feature <commit-id>
```

**Explanation**

Reflog records detached HEAD commits, allowing recovery before garbage collection.

---

### Scenario 9

**Question**

A junior developer wants to solve every push rejection by using:

```bash
git push --force
```

Would you recommend this approach?

**Answer**

No.

Force-pushing should only be used with caution and according to team policies because it can overwrite shared history and remove teammates' commits.

The preferred approach is to pull, review, resolve conflicts, and push normally.

**Explanation**

Force-pushing to shared branches is one of the most common causes of lost work in collaborative repositories.

---

### Scenario 10

**Question**

Your merge conflicts are becoming frequent because developers work on long-lived feature branches. What would you recommend?

**Answer**

- Pull frequently.
- Keep feature branches short-lived.
- Merge changes regularly.
- Commit small, focused changes.
- Encourage continuous integration.

**Explanation**

Frequent synchronization significantly reduces the likelihood and complexity of merge conflicts.

---

### Scenario 11

**Question**

You are working on a feature branch when several Git issues occur in succession: your `git pull` results in merge conflicts, you accidentally enter a Detached HEAD state while investigating an older commit, your subsequent push is rejected because the remote branch has new commits, and you later realize an important local commit appears to be missing. Describe how you would troubleshoot and recover from each problem.

**Answer**

A systematic troubleshooting approach is:

1. Resolve the merge conflicts by editing the conflicted files, removing conflict markers, staging the resolved files, and completing the merge:

```bash
git add .
git commit
```

2. If you enter a Detached HEAD state and need to preserve new work, immediately create a branch:

```bash
git switch -c recovery-branch
```

3. Before pushing, synchronize with the remote repository:

```bash
git fetch
git pull
```

Resolve any additional conflicts, then push again:

```bash
git push
```

4. If an important commit appears to be lost, inspect the reflog:

```bash
git reflog
```

Locate the commit and recover it by creating a new branch:

```bash
git switch -c recovered-work <commit-id>
```

5. Throughout the process, use diagnostic commands such as:

```bash
git status
git log
git diff
git branch
git remote -v
```

to understand the repository state before making corrective changes.

**Explanation**

This scenario reflects several of the most common production Git issues encountered by DevOps and Cloud engineers. Interviewers use questions like this to evaluate whether a candidate follows a structured troubleshooting process, understands Git internals, and can recover safely without risking repository history or losing code.
