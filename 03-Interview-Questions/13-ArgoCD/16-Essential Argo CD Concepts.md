# Essential Argo CD Concepts Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is the GitOps workflow in Argo CD?

**Answer**

The GitOps workflow uses Git as the single source of truth for Kubernetes deployments. Developers commit changes to a Git repository, and Argo CD continuously monitors the repository and synchronizes the Kubernetes cluster with the desired state.

**Explanation**

The workflow is:

1. Developer updates Kubernetes manifests in Git.
2. Changes are committed and pushed.
3. Argo CD detects the change.
4. Argo CD compares Git with the cluster.
5. Argo CD synchronizes the cluster.
6. Kubernetes applies the changes.

**Where it is used in Production**

- Kubernetes Continuous Delivery
- Cloud-native deployments
- Enterprise GitOps platforms

**Common Mistake**

Many candidates think Argo CD pushes changes to Git. In reality, developers update Git, and Argo CD pulls the changes.

---

### Question 2

**Question**

How does Argo CD implement Continuous Delivery?

**Answer**

Argo CD continuously monitors Git repositories and deploys approved changes to Kubernetes clusters either automatically or through manual synchronization.

**Explanation**

Unlike Continuous Deployment, Continuous Delivery may require manual approval before synchronization.

**Where it is used in Production**

Production release management with approval workflows.

---

### Question 3

**Question**

Why are Kubernetes manifests important in Argo CD?

**Answer**

Kubernetes manifests define the desired state of the application that Argo CD deploys and manages.

**Explanation**

These manifests can be:

- Plain YAML
- Helm Charts
- Kustomize configurations

Argo CD continuously ensures that the cluster matches these manifests.

**Where it is used in Production**

Managing Deployments, Services, ConfigMaps, Secrets, Ingresses, and other Kubernetes resources.

---

### Question 4

**Question**

What is Drift Detection in Argo CD?

**Answer**

Drift Detection is the process of identifying differences between the desired state stored in Git and the actual state running in the Kubernetes cluster.

**Explanation**

If someone manually changes a Kubernetes resource using `kubectl`, Argo CD detects the difference and marks the application as **OutOfSync**.

**Where it is used in Production**

Configuration compliance and GitOps governance.

**Common Mistake**

Candidates often think Drift Detection monitors only Git commits. It primarily detects differences between Git and the cluster.

---

### Question 5

**Question**

What is Self-Healing in Argo CD?

**Answer**

Self-Healing automatically restores Kubernetes resources to the desired state defined in Git whenever unauthorized changes are detected.

**Explanation**

If a resource is modified manually, Argo CD reapplies the configuration from Git to eliminate configuration drift.

**Where it is used in Production**

Preventing configuration drift and maintaining environment consistency.

---

### Question 6

**Question**

What is Automated Synchronization (Auto Sync)?

**Answer**

Automated Synchronization allows Argo CD to automatically apply changes from Git to Kubernetes without requiring manual synchronization.

**Explanation**

Whenever Argo CD detects a new Git commit, it automatically synchronizes the cluster if Auto Sync is enabled.

**Where it is used in Production**

Continuous Deployment pipelines.

**Common Mistake**

Many candidates confuse Auto Sync with Self-Healing. Auto Sync applies new Git changes, while Self-Healing restores manually modified resources.

---

### Question 7

**Question**

What is the difference between Manual Sync and Automated Sync?

**Answer**

- **Manual Sync** requires a user to trigger synchronization.
- **Automated Sync** performs synchronization automatically when Git changes are detected.

**Explanation**

Organizations often use Manual Sync for production environments and Auto Sync for development environments.

**Where it is used in Production**

Environment-specific deployment strategies.

---

### Question 8

**Question**

How does Argo CD detect changes in Git?

**Answer**

Argo CD continuously monitors the configured Git repository and compares the latest commit with the deployed application state.

**Explanation**

When a difference is detected, Argo CD updates the application's synchronization status and optionally performs synchronization.

**Where it is used in Production**

GitOps Continuous Delivery.

---

### Question 9

**Question**

Why is Git considered the single source of truth in Argo CD?

**Answer**

Because Git stores the desired application configuration, and Argo CD continuously ensures the Kubernetes cluster matches it.

**Explanation**

This approach improves:

- Version control
- Auditing
- Rollback
- Collaboration
- Change tracking

**Where it is used in Production**

Enterprise Kubernetes deployments.

---

### Question 10

**Question**

How does Argo CD prevent configuration drift?

**Answer**

It continuously compares the Kubernetes cluster with Git and identifies differences using Drift Detection. If Self-Healing is enabled, it automatically restores the desired state.

**Explanation**

This ensures manual changes do not permanently modify the production environment.

**Where it is used in Production**

Secure GitOps environments.

---

### Question 11

**Question**

What happens when a developer commits new Kubernetes manifests to Git?

**Answer**

Argo CD detects the new commit, compares it with the running cluster, updates the Sync Status, and synchronizes the application if Auto Sync is enabled or when manually triggered.

**Explanation**

This forms the core GitOps deployment workflow.

**Where it is used in Production**

Automated Kubernetes deployments.

---

### Question 12

**Question**

What are the main benefits of using Argo CD for GitOps?

**Answer**

The major benefits include:

- Git as the single source of truth
- Automated Continuous Delivery
- Drift Detection
- Self-Healing
- Easy rollback
- Deployment consistency
- Improved auditability

**Explanation**

These capabilities simplify Kubernetes deployments while improving reliability and operational consistency.

**Where it is used in Production**

Modern cloud-native DevOps environments.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

A Kubernetes administrator manually changes the number of replicas using `kubectl scale`, but the replica count later returns to its previous value. Why?

**Answer**

Argo CD detected configuration drift and restored the replica count defined in Git using Self-Healing.

**Explanation**

Git remains the desired state, so manual changes are automatically reverted when Self-Healing is enabled.

---

### Scenario 2

**Question**

A developer pushes updated Kubernetes manifests to Git, but no changes appear in the cluster. What would you investigate?

**Answer**

Verify whether Auto Sync is enabled. If it is disabled, perform a manual synchronization.

**Explanation**

Without Auto Sync, Argo CD detects the change but waits for a manual sync operation.

---

### Scenario 3

**Question**

An application is marked **OutOfSync**, but it is still functioning correctly. What does this indicate?

**Answer**

The running Kubernetes resources differ from the desired configuration stored in Git.

**Explanation**

OutOfSync indicates configuration drift, not necessarily an application failure.

---

### Scenario 4

**Question**

Your organization requires every production deployment to be approved before release. Should you enable Auto Sync?

**Answer**

No. Use Manual Synchronization so deployments occur only after approval.

**Explanation**

Manual Sync provides better control over production releases.

---

### Scenario 5

**Question**

A developer accidentally deletes a Deployment from Kubernetes using `kubectl delete deployment`. What happens if Self-Healing is enabled?

**Answer**

Argo CD detects the missing resource and recreates it from the Git repository.

**Explanation**

Self-Healing continuously restores deleted or modified resources to the desired state.

---

### Scenario 6

**Question**

Your security team discovers unauthorized manual changes in the production cluster. Which Argo CD feature would help detect them?

**Answer**

Drift Detection.

**Explanation**

Drift Detection compares the running cluster with Git and marks applications as **OutOfSync** when differences are found.

---

### Scenario 7

**Question**

An application deployment should occur automatically whenever developers merge code into the main branch. Which Argo CD feature enables this?

**Answer**

Automated Synchronization (Auto Sync).

**Explanation**

Auto Sync continuously deploys approved Git changes without manual intervention.

---

### Scenario 8

**Question**

A new engineer asks why Git is called the "single source of truth." How would you explain it?

**Answer**

Git stores the desired application configuration, and Argo CD ensures the Kubernetes cluster always matches what is defined in Git.

**Explanation**

This prevents configuration drift and provides a reliable, version-controlled deployment process.

---

### Scenario 9

**Question**

Your application is synchronized successfully, but users report issues after deployment. Does this mean Argo CD failed?

**Answer**

No. Synchronization only confirms that Kubernetes resources match Git. The application itself may still have runtime issues.

**Explanation**

Health Status, pod logs, Kubernetes events, and application logs should be investigated to identify runtime problems.

---

### Scenario 10

**Question**

During an interview, you are asked to explain the complete GitOps workflow using Argo CD. What would you answer?

**Answer**

The workflow is:

1. Developers update Kubernetes manifests in Git.
2. Git stores the desired application state.
3. Argo CD continuously monitors the repository.
4. Argo CD detects new commits or configuration drift.
5. Argo CD compares Git with the Kubernetes cluster.
6. If differences exist, it synchronizes the cluster manually or automatically.
7. If unauthorized manual changes occur, Drift Detection identifies them, and Self-Healing restores the desired state if enabled.

**Explanation**

This workflow demonstrates how Argo CD automates Kubernetes Continuous Delivery while ensuring the cluster always matches the version-controlled configuration stored in Git.
