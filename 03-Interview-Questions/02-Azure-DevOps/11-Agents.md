# Azure DevOps Agents Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is an Agent in Azure DevOps?

**Answer**

An Agent is a machine or virtual machine that executes Azure DevOps pipeline jobs. It performs tasks such as building applications, running tests, publishing artifacts, and deploying applications.

An agent can execute tasks like:

- Download source code
- Restore dependencies
- Build applications
- Run tests
- Publish artifacts
- Deploy applications

**Explanation**

When a pipeline starts, Azure DevOps assigns the job to an available agent. The agent executes each task sequentially and reports the results back to Azure DevOps.

**Used in Production**

Every Azure DevOps Build or Release Pipeline requires an agent to execute its jobs.

**Common Mistake**

Many candidates think Azure DevOps itself performs the build. In reality, the agent performs the work.

---

### Question 2

**Question**

What are the different types of Agents in Azure DevOps?

**Answer**

Azure DevOps supports two primary agent types:

1. Microsoft-Hosted Agents
2. Self-Hosted Agents

**Microsoft-Hosted Agents**

- Managed by Microsoft
- Automatically maintained
- Fresh virtual machine for every job
- No infrastructure management

**Self-Hosted Agents**

- Managed by the organization
- Installed on user-managed machines
- Can contain custom software
- Reused across multiple jobs

**Explanation**

The choice depends on security requirements, customization needs, and infrastructure control.

**Used in Production**

Small and medium projects often use Microsoft-hosted agents, while enterprise organizations frequently use self-hosted agents.

---

### Question 3

**Question**

What is a Microsoft-Hosted Agent?

**Answer**

A Microsoft-Hosted Agent is a virtual machine provided and managed by Microsoft.

Characteristics:

- Automatically provisioned
- Automatically updated
- Pre-installed development tools
- Destroyed after every pipeline run
- No maintenance required

Supported operating systems include:

- Ubuntu
- Windows
- macOS

**Explanation**

Azure DevOps provisions a clean virtual machine for each pipeline execution and removes it afterward.

**Used in Production**

Microsoft-hosted agents are ideal for standard CI/CD workloads without special software requirements.

**Common Mistake**

Candidates often assume data remains on Microsoft-hosted agents after a build. Each run starts with a clean machine.

---

### Question 4

**Question**

What is a Self-Hosted Agent?

**Answer**

A Self-Hosted Agent is an agent installed and managed by the organization on its own infrastructure.

It can be installed on:

- Windows
- Linux
- macOS
- Virtual Machines
- Physical Servers

**Explanation**

Self-hosted agents provide complete control over installed software, hardware resources, and network access.

**Used in Production**

Organizations use self-hosted agents for:

- Internal network deployments
- Large builds
- Custom SDKs
- Licensed software
- Private infrastructure

**Common Mistake**

Thinking self-hosted agents are always faster. Performance depends on the underlying hardware and configuration.

---

### Question 5

**Question**

What is the difference between Microsoft-Hosted and Self-Hosted Agents?

**Answer**

| Microsoft-Hosted Agent | Self-Hosted Agent |
|-------------------------|------------------|
| Managed by Microsoft | Managed by the organization |
| Fresh VM for every run | Persistent machine |
| Limited customization | Fully customizable |
| Automatically updated | Manual maintenance |
| Suitable for general workloads | Suitable for custom or secure environments |

**Explanation**

Microsoft-hosted agents reduce operational overhead, while self-hosted agents offer greater flexibility and control.

**Used in Production**

Enterprise environments often use self-hosted agents to access private resources or specialized tools.

---

### Question 6

**Question**

What is an Agent Pool?

**Answer**

An Agent Pool is a collection of one or more agents that Azure DevOps uses to execute pipeline jobs.

Example:

```text
Linux Pool
   ├── Agent 1
   ├── Agent 2
   └── Agent 3

Windows Pool
   ├── Agent 1
   └── Agent 2
```

**Explanation**

When a pipeline starts, Azure DevOps selects an available agent from the specified Agent Pool.

**Used in Production**

Organizations create separate pools for Windows, Linux, production deployments, or specialized build environments.

**Common Mistake**

Many candidates think an Agent Pool contains only one agent. It can contain multiple agents.

---

### Question 7

**Question**

What are Agent Capabilities?

**Answer**

Agent Capabilities describe the software and tools available on an agent.

Examples:

- Java
- .NET SDK
- Docker
- Maven
- Node.js
- Python
- Terraform
- Azure CLI

Capabilities can be:

- System capabilities (automatically detected)
- User capabilities (manually added)

**Explanation**

Pipelines can target agents that have the required capabilities for the job.

**Used in Production**

Teams use capabilities to ensure builds run only on compatible agents.

---

### Question 8

**Question**

What are Agent Demands?

**Answer**

Agent Demands specify the capabilities required by a pipeline.

Example:

```yaml
pool:
  name: LinuxPool

demands:
- Docker
- Maven
```

**Explanation**

Azure DevOps assigns the job only to an agent that satisfies all specified demands.

**Used in Production**

Demands are commonly used when specific tools or software versions are required.

**Common Mistake**

Confusing Capabilities with Demands. Capabilities describe the agent, while Demands describe the pipeline's requirements.

---

### Question 9

**Question**

When should you use a Self-Hosted Agent instead of a Microsoft-Hosted Agent?

**Answer**

Use a Self-Hosted Agent when:

- Deploying to private networks
- Accessing on-premises resources
- Using custom software
- Using licensed software
- Requiring specialized hardware
- Running large or resource-intensive builds

**Explanation**

Self-hosted agents provide greater flexibility and can access resources unavailable to Microsoft-hosted agents.

**Used in Production**

Large enterprise environments commonly rely on self-hosted agents.

---

### Question 10

**Question**

How does Azure DevOps select an Agent for a pipeline?

**Answer**

Azure DevOps:

1. Reads the configured Agent Pool.
2. Evaluates any specified demands.
3. Finds an available agent that satisfies the demands.
4. Assigns the job to that agent.

**Explanation**

Agent selection is automatic and based on pool membership, availability, and capabilities.

**Used in Production**

Multiple agents in a pool improve scalability and reduce pipeline wait times.

---

### Question 11

**Question**

What are some best practices for managing Azure DevOps Agents?

**Answer**

Best practices include:

- Use Microsoft-hosted agents for standard workloads.
- Use self-hosted agents only when necessary.
- Organize agents into logical pools.
- Keep self-hosted agents updated.
- Monitor agent health.
- Use agent demands only when required.
- Avoid installing unnecessary software.
- Secure self-hosted agents using least-privilege principles.

**Explanation**

Proper agent management improves pipeline reliability, security, and performance.

**Used in Production**

Enterprise DevOps teams regularly monitor agent utilization, updates, and health.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

A pipeline remains in the queue for a long time and never starts. What would you check?

**Answer**

Verify:

1. Agent availability.
2. Agent Pool status.
3. Offline agents.
4. Running jobs occupying all agents.
5. Agent demands.
6. Pipeline configuration.

**Explanation**

Pipelines typically remain queued when no suitable agent is available.

---

### Scenario 2

**Question**

A pipeline fails because Docker is not installed on the selected agent. How would you resolve this?

**Answer**

- Install Docker on the self-hosted agent, or
- Use a Microsoft-hosted agent image that includes Docker, or
- Configure agent demands to select only agents with Docker installed.

**Explanation**

The agent must have all required software before executing pipeline tasks.

---

### Scenario 3

**Question**

Your deployment pipeline must access an internal server that is not reachable from the internet. Which type of agent would you use?

**Answer**

Use a **Self-Hosted Agent** installed within the organization's private network.

**Explanation**

Microsoft-hosted agents cannot directly access private on-premises infrastructure unless specific networking solutions are implemented.

---

### Scenario 4

**Question**

Your organization has separate Windows and Linux applications. How would you organize the agents?

**Answer**

Create separate Agent Pools, for example:

- Windows Pool
- Linux Pool

Configure each pipeline to use the appropriate pool.

**Explanation**

Separating pools simplifies management and ensures pipelines run on compatible operating systems.

---

### Scenario 5

**Question**

A Build Pipeline suddenly fails because the required .NET SDK is missing. What would you investigate?

**Answer**

Check:

- Agent capabilities.
- SDK installation.
- Agent updates.
- Pipeline configuration.
- Hosted agent image changes (if using Microsoft-hosted agents).

**Explanation**

Pipeline failures often occur when required software is unavailable on the selected agent.

---

### Scenario 6

**Question**

A Self-Hosted Agent stops accepting new jobs. How would you troubleshoot?

**Answer**

Verify:

- Agent service status.
- Network connectivity.
- Disk space.
- CPU and memory usage.
- Agent logs.
- Azure DevOps connectivity.

Restart the agent service if necessary after identifying the root cause.

**Explanation**

Infrastructure or agent service issues commonly prevent self-hosted agents from accepting new work.

---

### Scenario 7

**Question**

Your manager wants faster pipeline execution during business hours. What improvements would you suggest?

**Answer**

- Add more agents to the Agent Pool.
- Enable parallel jobs.
- Separate build and deployment pools.
- Optimize long-running tasks.
- Remove unnecessary pipeline steps.

**Explanation**

Increasing available agents reduces queue times and improves throughput.

---

### Scenario 8

**Question**

A pipeline specifies a demand for Terraform, but no agents satisfy the requirement. What will happen?

**Answer**

The pipeline remains queued until an agent with the required capability becomes available or the demand is removed.

**Explanation**

Azure DevOps assigns jobs only to agents that meet all specified demands.

---

### Scenario 9

**Question**

A developer installs custom software directly on a Microsoft-hosted agent during a build. Will it be available in the next pipeline run?

**Answer**

No.

Microsoft-hosted agents are temporary virtual machines. Any software installed during a pipeline run is discarded after the job completes.

**Explanation**

Each Microsoft-hosted pipeline execution starts with a fresh VM.

---

### Scenario 10

**Question**

Your organization wants to use a single Self-Hosted Agent for both Development and Production deployments. Would you recommend this?

**Answer**

Generally, no.

Use separate Agent Pools or dedicated self-hosted agents for Development and Production to improve security, reduce risk, and isolate workloads.

**Explanation**

Separating environments minimizes the impact of configuration changes and strengthens security controls.

---

### Scenario 11

**Question**

During a production deployment, Azure DevOps reports that no agent satisfies the specified demands. How would you resolve the issue?

**Answer**

- Review the pipeline's configured demands.
- Check the capabilities of agents in the selected Agent Pool.
- Install the missing software or add the required user capability to an appropriate agent.
- Ensure the correct Agent Pool is referenced.
- Re-run the pipeline after verifying the agent configuration.

**Explanation**

Demand mismatches are a common cause of queued or failed pipeline jobs. Ensuring that agent capabilities align with pipeline requirements allows Azure DevOps to assign the job successfully.
