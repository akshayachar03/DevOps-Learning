# Projects & Deployment Strategies Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is an AppProject in Argo CD?

**Answer**

An **AppProject** is a logical boundary that controls which applications can access specific Git repositories, Kubernetes clusters, namespaces, and resources.

**Explanation**

AppProjects provide multi-tenancy and security by defining what an application is allowed to deploy.

It can restrict:
- Source repositories
- Destination clusters
- Destination namespaces
- Kubernetes resource types

**Where it is used in Production**

- Multi-team Kubernetes environments
- Enterprise GitOps platforms
- Shared Argo CD installations

**Common Mistake**

Many candidates think an AppProject is simply a folder for grouping applications. Its primary purpose is access control and policy enforcement.

---

### Question 2

**Question**

Why are AppProjects important in enterprise environments?

**Answer**

AppProjects prevent unauthorized deployments by restricting where and what applications can deploy.

**Explanation**

Without AppProjects, any application could potentially deploy to any cluster or namespace, increasing security risks.

**Where it is used in Production**

Organizations with:
- Multiple development teams
- Production and non-production clusters
- Shared Kubernetes platforms

---

### Question 3

**Question**

What are Source Repository Restrictions in an AppProject?

**Answer**

Source Repository Restrictions specify which Git repositories an application is allowed to use.

**Explanation**

Only approved repositories can be deployed, preventing unauthorized or untrusted code from reaching Kubernetes.

**Where it is used in Production**

- Security compliance
- Enterprise Git governance
- Regulated environments

**Common Mistake**

Candidates often think Argo CD can deploy from any Git repository regardless of project configuration.

---

### Question 4

**Question**

What are Destination Restrictions?

**Answer**

Destination Restrictions define which Kubernetes clusters and namespaces an application can deploy to.

**Explanation**

Administrators specify approved deployment destinations, preventing accidental deployments to unauthorized environments.

**Where it is used in Production**

- Production access control
- Multi-cluster environments
- Team isolation

---

### Question 5

**Question**

What are Resource Permissions in an AppProject?

**Answer**

Resource Permissions control which Kubernetes resource types an application can create or modify.

**Explanation**

Administrators can allow or deny resources such as:

- Deployments
- Services
- ConfigMaps
- Secrets
- ClusterRoles
- Namespaces

**Where it is used in Production**

Enterprise security and least-privilege deployments.

---

### Question 6

**Question**

What is Declarative Deployment in Argo CD?

**Answer**

Declarative Deployment means the desired application state is defined as code in Git rather than executed through manual commands.

**Explanation**

Argo CD continuously reads Kubernetes manifests or Helm charts from Git and ensures the cluster matches them.

**Where it is used in Production**

GitOps-based Continuous Delivery.

**Common Mistake**

Many candidates confuse declarative deployment with imperative commands like `kubectl create`.

---

### Question 7

**Question**

How does Argo CD support Rolling Updates?

**Answer**

Argo CD applies Kubernetes manifests, while Kubernetes performs the rolling update according to the Deployment strategy.

**Explanation**

Argo CD does not implement rolling updates itself. It relies on Kubernetes Deployment controllers.

**Where it is used in Production**

Zero-downtime application deployments.

---

### Question 8

**Question**

How can you perform a rollback using Argo CD?

**Answer**

Rollback is typically performed by reverting the Git repository to a previous commit and synchronizing the application.

**Explanation**

Since Git is the source of truth, reverting Git automatically restores the previous application version.

**Where it is used in Production**

Production incident recovery.

**Common Mistake**

Candidates often think rollback happens directly in Kubernetes instead of through Git.

---

### Question 9

**Question**

What are Sync Waves in Argo CD?

**Answer**

Sync Waves control the order in which Kubernetes resources are deployed during synchronization.

**Explanation**

Resources with lower wave numbers are deployed first, followed by higher-numbered waves.

Example:

- Wave 0 → Namespace
- Wave 1 → ConfigMaps
- Wave 2 → Deployments
- Wave 3 → Services

**Where it is used in Production**

Complex multi-resource deployments.

---

### Question 10

**Question**

Why are Sync Waves useful?

**Answer**

They ensure dependent resources are deployed in the correct order.

**Explanation**

For example:

- ConfigMaps should exist before Pods start.
- CRDs should exist before Custom Resources are created.

**Where it is used in Production**

Large Kubernetes applications with multiple dependencies.

---

### Question 11

**Question**

Can multiple applications belong to the same AppProject?

**Answer**

Yes.

**Explanation**

An AppProject can contain multiple applications that share the same deployment policies and security restrictions.

**Where it is used in Production**

Applications managed by the same development team or business unit.

---

### Question 12

**Question**

What is the relationship between GitOps and Declarative Deployment?

**Answer**

Declarative Deployment is one of the core principles of GitOps.

**Explanation**

Git stores the desired state, while Argo CD continuously reconciles the Kubernetes cluster to match that state.

**Where it is used in Production**

Modern Kubernetes Continuous Delivery platforms.

**Common Mistake**

Candidates sometimes think GitOps requires manual deployment after every Git commit. With Auto Sync enabled, deployments can occur automatically.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

A development team accidentally deploys an application to the production namespace. How could AppProjects have prevented this?

**Answer**

The AppProject should have restricted deployments to only approved namespaces.

**Explanation**

Destination Restrictions prevent deployments outside authorized environments.

---

### Scenario 2

**Question**

An application attempts to deploy from an unknown Git repository and Argo CD blocks it. Why?

**Answer**

The repository is not included in the AppProject's Source Repository Restrictions.

**Explanation**

Only approved Git repositories are permitted for deployments.

---

### Scenario 3

**Question**

A deployment fails because a ConfigMap is created after the Pods start. How would you solve this in Argo CD?

**Answer**

Use Sync Waves so the ConfigMap is deployed before the Deployment.

**Explanation**

Deploying dependent resources in the correct order prevents startup failures.

---

### Scenario 4

**Question**

A production deployment introduced a bug. What is the recommended rollback approach in Argo CD?

**Answer**

Revert the Git repository to the previous stable version and synchronize the application.

**Explanation**

Git remains the single source of truth, making rollbacks simple and auditable.

---

### Scenario 5

**Question**

Your organization wants developers to deploy only to development namespaces while the DevOps team manages production. How would you configure Argo CD?

**Answer**

Create separate AppProjects with Destination Restrictions for each team.

**Explanation**

This enforces environment isolation and access control.

---

### Scenario 6

**Question**

A team needs to deploy Deployments and Services but should not be allowed to create ClusterRoles or Namespaces. Which AppProject feature should be used?

**Answer**

Resource Permissions.

**Explanation**

Resource Permissions allow administrators to whitelist or blacklist Kubernetes resource types.

---

### Scenario 7

**Question**

An application shows **OutOfSync** after someone manually updates a Deployment using `kubectl edit`. What will happen after synchronization?

**Answer**

Argo CD will overwrite the manual changes and restore the Deployment to the version stored in Git.

**Explanation**

GitOps eliminates configuration drift by reconciling the cluster with Git.

---

### Scenario 8

**Question**

Your deployment consists of CRDs and Custom Resources. How should you ensure successful deployment?

**Answer**

Deploy CRDs in an earlier Sync Wave and Custom Resources in a later Sync Wave.

**Explanation**

Custom Resources cannot be created until their CRDs exist.

---

### Scenario 9

**Question**

A company manages applications across multiple Kubernetes clusters. How can Argo CD ensure that each application is deployed only to its assigned cluster?

**Answer**

Configure Destination Restrictions within the appropriate AppProject.

**Explanation**

Destination Restrictions specify which clusters and namespaces an application is allowed to target.

---

### Scenario 10

**Question**

During an interview, you are asked how Argo CD performs rolling deployments without implementing its own deployment mechanism. What would you answer?

**Answer**

Argo CD applies the desired Kubernetes manifests to the cluster, and the Kubernetes Deployment controller performs the rolling update based on the Deployment strategy defined in the manifest.

**Explanation**

Argo CD focuses on synchronization and reconciliation, while Kubernetes is responsible for executing the rolling update process.
