# Kubernetes Troubleshooting Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is the first thing you should check when troubleshooting a Kubernetes Pod?

**Answer**

The first step is to check the Pod status using:

```bash
kubectl get pods
```

This command shows whether the Pod is:

- Running
- Pending
- CrashLoopBackOff
- ImagePullBackOff
- Completed
- Error

**Explanation**

The Pod status provides the initial indication of the problem and helps determine the next troubleshooting steps.

**Used in Production**

Engineers almost always begin Kubernetes troubleshooting with `kubectl get pods`.

**Common Mistake**

Jumping directly to logs without first checking the Pod status.

---

### Question 2

**Question**

What does the `CrashLoopBackOff` status mean?

**Answer**

`CrashLoopBackOff` indicates that the container starts, crashes, Kubernetes restarts it, and this cycle repeats continuously.

**Explanation**

Kubernetes waits progressively longer between restart attempts (backoff) to avoid constant restart loops.

Common causes include:

- Application bugs
- Incorrect environment variables
- Missing configuration files
- Database connection failures
- Invalid startup commands

**Used in Production**

One of the most common production issues.

**Common Mistake**

Assuming Kubernetes is faulty. In most cases, the application itself is failing.

---

### Question 3

**Question**

What does the `ImagePullBackOff` status indicate?

**Answer**

`ImagePullBackOff` means Kubernetes cannot pull the container image from the registry.

Common reasons include:

- Incorrect image name
- Invalid image tag
- Private registry authentication failure
- Registry unavailable
- Image does not exist

**Explanation**

The kubelet repeatedly attempts to download the image before entering a backoff state.

**Used in Production**

Frequently occurs after deployment configuration mistakes.

---

### Question 4

**Question**

Why do Pods remain in the `Pending` state?

**Answer**

A Pod remains in the Pending state because Kubernetes cannot schedule it onto a worker node.

Common causes include:

- Insufficient CPU
- Insufficient memory
- Missing Persistent Volume
- Node taints
- Resource constraints
- Unsatisfied node selectors

**Explanation**

The scheduler keeps trying until suitable resources become available.

**Common Mistake**

Assuming Pending means the application has failed. The application has not started yet.

---

### Question 5

**Question**

How do you view logs from a Kubernetes Pod?

**Answer**

Use:

```bash
kubectl logs <pod-name>
```

For multi-container Pods:

```bash
kubectl logs <pod-name> -c <container-name>
```

**Explanation**

Logs provide application-level information useful for diagnosing runtime failures.

**Used in Production**

Debugging startup failures, exceptions, and application crashes.

---

### Question 6

**Question**

What information does `kubectl describe pod` provide?

**Answer**

It provides detailed Pod information, including:

- Container status
- Events
- Scheduling details
- Mounted volumes
- Environment variables
- Restart count
- Probe failures

**Explanation**

Unlike `kubectl logs`, it includes Kubernetes-level information and recent cluster events.

**Used in Production**

Investigating scheduling and deployment issues.

---

### Question 7

**Question**

What are Kubernetes Events?

**Answer**

Events are chronological records of important actions performed by Kubernetes.

Examples include:

- Scheduled
- Pulled image
- Started container
- Failed scheduling
- Failed image pull
- Liveness probe failed

**Explanation**

Events help identify why a resource entered its current state.

**Used in Production**

Root cause analysis.

---

### Question 8

**Question**

When should you use `kubectl logs` versus `kubectl describe`?

**Answer**

| `kubectl logs` | `kubectl describe` |
|---------------|--------------------|
| Application logs | Kubernetes events |
| Runtime errors | Scheduling issues |
| Stack traces | Container status |
| Exceptions | Probe failures |

**Explanation**

Use both together for effective troubleshooting.

**Common Mistake**

Using only one command and missing critical diagnostic information.

---

### Question 9

**Question**

How can you determine why a container is restarting repeatedly?

**Answer**

Use:

```bash
kubectl describe pod <pod-name>

kubectl logs <pod-name>
```

Check:

- Restart count
- Exit code
- Probe failures
- Application errors

**Explanation**

These commands identify whether the issue is caused by Kubernetes or the application.

---

### Question 10

**Question**

What is the difference between Kubernetes-level issues and application-level issues?

**Answer**

Kubernetes-level issues include:

- Scheduling failures
- Image pull failures
- Resource constraints

Application-level issues include:

- Exceptions
- Database connection failures
- Configuration errors
- Application crashes

**Explanation**

`kubectl describe` typically identifies Kubernetes issues, while `kubectl logs` identifies application issues.

---

### Question 11

**Question**

Which commands are most commonly used for Kubernetes troubleshooting?

**Answer**

```bash
kubectl get pods

kubectl describe pod <pod-name>

kubectl logs <pod-name>

kubectl get events

kubectl exec -it <pod-name> -- /bin/bash
```

**Explanation**

These commands form the core troubleshooting workflow used by DevOps and SRE engineers.

---

### Question 12

**Question**

What should you examine in the output of `kubectl describe pod`?

**Answer**

Focus on:

- Pod Conditions
- Container State
- Restart Count
- Events
- Scheduling Messages
- Image Information
- Resource Requests and Limits
- Probe Results

**Explanation**

These sections often reveal the root cause of deployment failures.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

A Pod is showing the status `CrashLoopBackOff`. How would you troubleshoot it?

**Answer**

Run:

```bash
kubectl describe pod <pod-name>

kubectl logs <pod-name>
```

Review:

- Application logs
- Exit codes
- Restart count
- Liveness probe failures
- Environment variables

**Explanation**

Most CrashLoopBackOff issues originate from application startup failures or configuration problems.

---

### Scenario 2

**Question**

Your deployment shows `ImagePullBackOff`. What would you check?

**Answer**

Verify:

- Image name
- Image tag
- Registry credentials
- Registry availability
- Secret configuration

**Explanation**

Image pull failures are usually caused by incorrect image references or authentication problems.

---

### Scenario 3

**Question**

A Pod remains in the Pending state for several minutes. What commands would you use?

**Answer**

```bash
kubectl describe pod <pod-name>

kubectl get nodes

kubectl describe node <node-name>
```

**Explanation**

These commands reveal scheduling failures such as insufficient resources or node constraints.

---

### Scenario 4

**Question**

Users report that a deployed application is unavailable, but the Pod status is Running. What should you investigate?

**Answer**

Check:

```bash
kubectl logs <pod-name>

kubectl describe pod <pod-name>
```

Also verify:

- Readiness Probe
- Service configuration
- Endpoint availability

**Explanation**

A Running Pod does not necessarily mean the application is ready to receive traffic.

---

### Scenario 5

**Question**

Your application exits immediately after startup. Which command should you execute first?

**Answer**

```bash
kubectl logs <pod-name>
```

**Explanation**

Application logs usually contain the startup error responsible for the crash.

---

### Scenario 6

**Question**

A Pod is repeatedly restarting because the application cannot connect to the database. Which Pod status is most likely displayed?

**Answer**

`CrashLoopBackOff`

**Explanation**

The application starts, fails due to the database connection issue, exits, and Kubernetes repeatedly restarts it.

---

### Scenario 7

**Question**

A developer says, "The Pod is not working." Which commands would you execute first to perform a structured investigation?

**Answer**

```bash
kubectl get pods

kubectl describe pod <pod-name>

kubectl logs <pod-name>

kubectl get events
```

**Explanation**

This sequence provides Pod status, Kubernetes events, and application logs, covering the most common failure causes.

---

### Scenario 8

**Question**

The `kubectl logs` output is empty, but the Pod is still failing to start. What should you check next?

**Answer**

Run:

```bash
kubectl describe pod <pod-name>
```

Review the **Events** section for scheduling issues, image pull failures, or probe errors.

**Explanation**

If the container never starts successfully, there may be no application logs, making Kubernetes events the primary source of information.

---

### Scenario 9

**Question**

A Pod is continuously restarting due to failed Liveness Probes. Where would you identify this issue?

**Answer**

Use:

```bash
kubectl describe pod <pod-name>
```

Check the **Events** section and the container status.

**Explanation**

`kubectl describe` reports probe failures and restart events, making it the best tool for diagnosing health check issues.

---

### Scenario 10

**Question**

During a production incident, you have only five minutes to identify why an application is unavailable. What is your troubleshooting workflow?

**Answer**

1. Check Pod status:

```bash
kubectl get pods
```

2. Describe the Pod:

```bash
kubectl describe pod <pod-name>
```

3. View application logs:

```bash
kubectl logs <pod-name>
```

4. Check cluster events:

```bash
kubectl get events
```

5. If needed, inspect the container:

```bash
kubectl exec -it <pod-name> -- /bin/bash
```

**Explanation**

This structured workflow quickly distinguishes between scheduling issues, infrastructure problems, and application-level failures, making it the standard troubleshooting approach used by DevOps and SRE engineers in production.
