# Monitoring & Troubleshooting Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

How do you monitor applications in Argo CD?

**Answer**

Applications can be monitored using the Argo CD Web UI, CLI, application health status, synchronization status, application events, and logs.

**Explanation**

Argo CD continuously compares the desired state in Git with the actual state in Kubernetes. It displays whether an application is healthy, synchronized, or requires attention.

**Where it is used in Production**

- Daily application monitoring
- Deployment verification
- Production health checks

**Common Mistake**

Many candidates think Argo CD only reports deployment status. It also monitors application health and configuration drift.

---

### Question 2

**Question**

What are Application Events in Argo CD?

**Answer**

Application Events are activity logs that record important operations such as synchronization, deployment, health changes, errors, and reconciliation events.

**Explanation**

Events help administrators understand what happened during deployments and identify failures.

**Where it is used in Production**

- Deployment auditing
- Troubleshooting failed deployments
- Root cause analysis

---

### Question 3

**Question**

What is a Sync Failure in Argo CD?

**Answer**

A Sync Failure occurs when Argo CD cannot successfully apply the desired Kubernetes resources to the target cluster.

**Explanation**

Common causes include:
- Invalid YAML
- Missing CRDs
- Kubernetes API errors
- Permission issues
- Repository problems

**Where it is used in Production**

During application deployment and updates.

**Common Mistake**

Candidates often assume every Sync Failure is caused by Git issues. Kubernetes resource validation errors are equally common.

---

### Question 4

**Question**

What can cause Repository Connection Issues in Argo CD?

**Answer**

Common causes include:

- Incorrect repository URL
- Invalid credentials
- Expired access tokens
- SSH key problems
- Network connectivity issues

**Explanation**

Argo CD must access the Git repository before it can synchronize applications.

**Where it is used in Production**

GitOps deployment pipelines.

---

### Question 5

**Question**

What are Kubernetes Resource Errors?

**Answer**

These are errors returned by the Kubernetes API when Argo CD attempts to create or update resources.

**Explanation**

Examples include:

- Invalid manifests
- Resource conflicts
- Missing namespaces
- Missing CRDs
- Insufficient permissions

**Where it is used in Production**

Application deployment troubleshooting.

---

### Question 6

**Question**

How do you view logs in Argo CD?

**Answer**

Logs can be viewed from the Argo CD server pods using Kubernetes commands or through centralized logging platforms.

Example:

```bash
kubectl logs deployment/argocd-application-controller -n argocd
```

**Explanation**

Logs provide detailed information about synchronization, reconciliation, authentication, and application errors.

**Where it is used in Production**

Investigating deployment failures and application synchronization issues.

---

### Question 7

**Question**

What does the Health Status of an application indicate?

**Answer**

Health Status indicates whether the deployed application is functioning correctly.

Common states include:

- Healthy
- Progressing
- Degraded
- Missing
- Suspended

**Explanation**

Argo CD evaluates Kubernetes resources and reports their operational state.

**Where it is used in Production**

Continuous monitoring of application health.

---

### Question 8

**Question**

What is the difference between Sync Status and Health Status?

**Answer**

- **Sync Status** shows whether Kubernetes matches the desired Git state.
- **Health Status** shows whether the deployed application is operating correctly.

**Explanation**

An application can be:

- Synced but Degraded
- OutOfSync but Healthy

These statuses represent different aspects of the deployment.

**Where it is used in Production**

Production monitoring dashboards.

**Common Mistake**

Candidates often think Sync Status automatically means the application is healthy.

---

### Question 9

**Question**

What should you check first when an application becomes Degraded?

**Answer**

Check:

- Application Events
- Application Logs
- Kubernetes Events
- Pod Status
- Deployment Status

**Explanation**

The degradation may be caused by container failures, configuration issues, missing dependencies, or Kubernetes resource errors.

**Where it is used in Production**

Production incident response.

---

### Question 10

**Question**

How can Argo CD help identify configuration drift?

**Answer**

Argo CD continuously compares Git with the Kubernetes cluster and marks applications as **OutOfSync** if differences are detected.

**Explanation**

Manual changes made using `kubectl` are detected during reconciliation.

**Where it is used in Production**

GitOps compliance and configuration management.

---

### Question 11

**Question**

Which CLI command displays detailed application information for troubleshooting?

**Answer**

```bash
argocd app get <application-name>
```

**Explanation**

The command displays:

- Sync Status
- Health Status
- Repository
- Target Revision
- Events
- Resource Tree

**Where it is used in Production**

Daily troubleshooting and deployment verification.

---

### Question 12

**Question**

What are the most common causes of Argo CD deployment failures?

**Answer**

Common causes include:

- Invalid Kubernetes manifests
- Repository authentication failures
- Cluster connectivity issues
- Missing namespaces
- RBAC permission problems
- Invalid Helm or Kustomize configurations

**Explanation**

These account for the majority of deployment failures encountered in production.

**Where it is used in Production**

Production deployment troubleshooting.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

An application is marked **OutOfSync** even though no developer has pushed new code. What is the most likely cause?

**Answer**

Someone manually modified Kubernetes resources using `kubectl`.

**Explanation**

Argo CD detected configuration drift between Git and the cluster.

---

### Scenario 2

**Question**

A synchronization fails with a "Permission Denied" error. What would you investigate first?

**Answer**

Check Kubernetes RBAC permissions and Argo CD service account permissions.

**Explanation**

Insufficient permissions commonly prevent resource creation or updates.

---

### Scenario 3

**Question**

An application remains **Degraded** after synchronization completes successfully. What should you check?

**Answer**

Inspect Pod status, Deployment status, Kubernetes events, and application logs.

**Explanation**

Synchronization only confirms deployment. Health depends on whether the application is running successfully.

---

### Scenario 4

**Question**

Argo CD reports that it cannot access the Git repository. What troubleshooting steps would you perform?

**Answer**

Verify:

- Repository URL
- Username/password or SSH key
- Personal Access Token
- Repository permissions
- Network connectivity

**Explanation**

Repository authentication failures are one of the most common GitOps deployment issues.

---

### Scenario 5

**Question**

A deployment fails because the namespace does not exist. How would you resolve it?

**Answer**

Create the namespace manually or configure Argo CD to create it automatically during synchronization if appropriate.

**Explanation**

Applications cannot be deployed into non-existent namespaces.

---

### Scenario 6

**Question**

Your application synchronization fails because a Custom Resource Definition (CRD) is missing. What should you do?

**Answer**

Deploy the required CRD before synchronizing the dependent Custom Resource.

**Explanation**

Kubernetes cannot create Custom Resources until the corresponding CRD exists.

---

### Scenario 7

**Question**

A developer reports that an application deployment succeeded, but users cannot access the application. How would you troubleshoot?

**Answer**

Verify:

- Health Status
- Pod status
- Service
- Ingress
- Application logs
- Kubernetes events

**Explanation**

Successful synchronization does not guarantee that the application is functioning correctly.

---

### Scenario 8

**Question**

Application Events show repeated synchronization attempts every few minutes. What could be happening?

**Answer**

Argo CD is continuously reconciling because the cluster state differs from the desired Git state.

**Explanation**

Configuration drift or external modifications can trigger repeated reconciliation.

---

### Scenario 9

**Question**

Your CI/CD pipeline completes successfully, but Argo CD does not deploy the latest changes. What would you check?

**Answer**

Verify:

- Repository revision
- Sync Status
- Auto Sync configuration
- Application Events
- Repository connectivity

**Explanation**

A successful pipeline does not guarantee that Argo CD has synchronized the latest Git commit.

---

### Scenario 10

**Question**

During an interview, you are asked how you would troubleshoot an Argo CD deployment failure. What would you answer?

**Answer**

I would follow a structured approach:

1. Check the application's Sync Status and Health Status.
2. Review Application Events.
3. Examine the output of `argocd app get`.
4. Verify repository connectivity and credentials.
5. Inspect Kubernetes events and resource status.
6. Review Argo CD controller logs.
7. Check Pod logs for application-specific issues.
8. Validate manifests, Helm values, or Kustomize configuration.

**Explanation**

This systematic workflow helps isolate whether the issue originates from Git, Argo CD, Kubernetes, or the application itself and reflects the troubleshooting process commonly used in production environments.
