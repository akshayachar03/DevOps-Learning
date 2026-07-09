# Ansible Fundamentals Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is Ansible, and why is it widely used in DevOps?

**Answer**

Ansible is an open-source IT automation and configuration management tool used to automate server provisioning, software installation, configuration management, application deployment, and orchestration.

**Explanation**

Ansible automates repetitive administrative tasks using simple YAML-based playbooks. It communicates with managed nodes over SSH (Linux) or WinRM (Windows), eliminating the need to install agents on target machines.

**Used in Production**

- Server provisioning
- Configuration management
- Application deployment
- Patch management
- Infrastructure automation
- CI/CD pipelines

**Common Mistake**

Many candidates think Ansible is only a deployment tool. In reality, it is a comprehensive automation platform used throughout the infrastructure lifecycle.

---

### Question 2

**Question**

What is Configuration Management, and how does Ansible help achieve it?

**Answer**

Configuration Management is the process of maintaining servers in a consistent, desired configuration.

Ansible automates this process by ensuring that servers are configured identically according to predefined playbooks.

**Explanation**

Instead of manually configuring each server, administrators define the desired configuration once in a playbook. Ansible then applies the same configuration across all target systems, reducing configuration drift.

**Used in Production**

- Installing packages
- Creating users
- Managing services
- Updating configuration files
- Maintaining consistent environments

**Common Mistake**

Candidates often confuse configuration management with provisioning. Provisioning creates infrastructure, while configuration management configures it after creation.

---

### Question 3

**Question**

What does Agentless Architecture mean in Ansible?

**Answer**

Agentless Architecture means Ansible does not require any software agent to be installed on managed nodes.

**Explanation**

The Ansible Control Node connects to managed nodes using SSH (Linux) or WinRM (Windows), executes tasks remotely, and disconnects after completion.

**Used in Production**

Organizations prefer Ansible because it minimizes maintenance overhead and reduces security risks associated with installing agents.

**Common Mistake**

Some candidates incorrectly state that Ansible installs temporary agents. It does not install persistent agents.

---

### Question 4

**Question**

Why is Ansible called a Push-Based Automation tool?

**Answer**

Ansible is push-based because the Control Node initiates connections and pushes tasks to managed nodes whenever automation is executed.

**Explanation**

Unlike pull-based tools, managed nodes do not periodically check for configuration updates. The administrator controls when automation runs.

**Used in Production**

Operations teams execute automation manually or trigger it from CI/CD pipelines whenever changes are required.

**Common Mistake**

Candidates often confuse Ansible with Puppet or Chef, which primarily use pull-based models.

---

### Question 5

**Question**

What is the difference between Push-Based and Pull-Based Configuration Management?

**Answer**

| Push-Based (Ansible) | Pull-Based (Puppet/Chef) |
|-----------------------|--------------------------|
| Control node initiates execution | Agents periodically pull configurations |
| No agent required | Agent required |
| Immediate execution | Runs on scheduled intervals |
| Easier to manage | Better for continuous enforcement |

**Explanation**

Push-based automation gives administrators direct control, while pull-based systems continuously enforce configurations.

**Used in Production**

Ansible is commonly chosen for infrastructure automation due to its simplicity.

---

### Question 6

**Question**

What is the Ansible Control Node?

**Answer**

The Control Node is the machine where Ansible is installed and from which automation tasks are executed.

**Explanation**

It stores:

- Inventory files
- Playbooks
- Roles
- Modules
- Configuration files

The Control Node connects to managed nodes and executes automation tasks.

**Used in Production**

Typically, a dedicated Linux server or CI/CD runner acts as the Control Node.

**Common Mistake**

Candidates sometimes think the Control Node manages services continuously. It only executes automation when instructed.

---

### Question 7

**Question**

What are Managed Nodes in Ansible?

**Answer**

Managed Nodes are the target servers or machines on which Ansible executes automation tasks.

**Explanation**

Managed nodes can be:

- Linux servers
- Windows servers
- Cloud virtual machines
- Containers
- Network devices

They only require SSH or WinRM connectivity.

**Used in Production**

Web servers, database servers, application servers, and cloud instances are common managed nodes.

---

### Question 8

**Question**

What is an Inventory in Ansible?

**Answer**

An Inventory is a list of managed nodes that Ansible controls.

**Explanation**

The inventory specifies:

- Hostnames
- IP addresses
- Groups
- Connection details

Example:

```ini
[webservers]
192.168.1.10
192.168.1.11

[dbservers]
192.168.1.20
```

**Used in Production**

Large organizations organize hundreds or thousands of servers into logical inventory groups.

**Common Mistake**

Candidates sometimes confuse the inventory with playbooks. The inventory defines *where* tasks run, while playbooks define *what* tasks run.

---

### Question 9

**Question**

What is the purpose of the `ansible.cfg` file?

**Answer**

`ansible.cfg` is Ansible's main configuration file used to customize Ansible's behavior.

**Explanation**

It can define:

- Inventory location
- Remote user
- SSH settings
- Default module paths
- Timeout values
- Logging options

**Used in Production**

Organizations use `ansible.cfg` to standardize automation across projects.

---

### Question 10

**Question**

What is a Static Inventory in Ansible?

**Answer**

A Static Inventory is a manually created inventory file containing a fixed list of managed nodes.

**Explanation**

It is typically written in INI or YAML format and is suitable for environments where server information changes infrequently.

**Used in Production**

Development, testing, and small production environments commonly use static inventories.

**Common Mistake**

Candidates often assume all inventories are static. Cloud environments frequently use dynamic inventories.

---

### Question 11

**Question**

How do you install Ansible on a Linux system?

**Answer**

On Ubuntu:

```bash
sudo apt update
sudo apt install ansible
```

Verify installation:

```bash
ansible --version
```

**Explanation**

Installing Ansible also installs the required Python dependencies.

**Used in Production**

Ansible is typically installed on dedicated automation servers or CI/CD runners.

---

### Question 12

**Question**

What are the main components involved when Ansible executes a task?

**Answer**

The execution flow is:

1. Control Node
2. Inventory
3. SSH/WinRM Connection
4. Managed Node
5. Ansible Module Execution
6. Result Returned to Control Node

**Explanation**

The Control Node reads the inventory, connects to target systems, executes the required modules, collects results, and reports success or failure.

**Used in Production**

Every Ansible automation follows this workflow.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

Your company has 100 Linux servers that all need the same package installed. How would you accomplish this using Ansible?

**Answer**

Create an inventory containing all servers and execute an Ansible playbook that installs the package on every managed node.

**Explanation**

Ansible performs the task in parallel, ensuring consistency across all servers while eliminating manual effort.

---

### Scenario 2

**Question**

A security team asks you to install an agent on all managed servers before using an automation tool. Why would this not be necessary with Ansible?

**Answer**

Ansible is agentless. It communicates using SSH or WinRM and does not require software agents on managed nodes.

**Explanation**

This simplifies deployment, reduces maintenance, and minimizes the attack surface.

---

### Scenario 3

**Question**

You run an Ansible command, but some servers are skipped. What would you check first?

**Answer**

Verify:

- Inventory entries
- SSH connectivity
- Hostnames/IP addresses
- SSH credentials
- Network accessibility

**Explanation**

Most connectivity issues originate from incorrect inventory configuration or SSH problems.

---

### Scenario 4

**Question**

You update the inventory file with a new server. What additional configuration is typically required before Ansible can manage it?

**Answer**

Ensure:

- SSH access is working
- Correct authentication is configured
- Python is available on the managed node (for most Ansible modules)

**Explanation**

Once connectivity is established, the server can be managed immediately.

---

### Scenario 5

**Question**

Your production environment contains separate Web, Application, and Database servers. How would you organize them in Ansible?

**Answer**

Create inventory groups such as:

```ini
[webservers]
...

[appservers]
...

[dbservers]
...
```

**Explanation**

Grouping simplifies targeted automation and improves playbook organization.

---

### Scenario 6

**Question**

A developer accidentally edits configuration files manually on several servers. How can Ansible help?

**Answer**

Run the configuration management playbook again to restore the desired configuration.

**Explanation**

Ansible enforces consistency across servers, reducing configuration drift.

---

### Scenario 7

**Question**

Ansible cannot connect to one managed node, but other servers work correctly. How would you troubleshoot?

**Answer**

Check:

- SSH service
- Firewall rules
- Network connectivity
- Inventory configuration
- User permissions
- SSH keys

**Explanation**

Since other servers are reachable, the issue is likely specific to that managed node.

---

### Scenario 8

**Question**

Your organization provisions new cloud VMs every day. Is a static inventory always the best option?

**Answer**

No.

For dynamic cloud environments, Dynamic Inventory is generally preferred because it automatically discovers new resources.

**Explanation**

Static inventories require manual updates and become difficult to maintain in rapidly changing environments.

---

### Scenario 9

**Question**

A team member asks why Ansible is preferred over manually logging into every server. What would you say?

**Answer**

Ansible provides:

- Automation
- Consistency
- Speed
- Reduced human error
- Centralized management
- Scalability

**Explanation**

Instead of repeating manual tasks across hundreds of servers, administrators execute automation once from the Control Node.

---

### Scenario 10

**Question**

Your CI/CD pipeline needs to deploy configuration changes to multiple Linux servers after every successful build. How would Ansible fit into this workflow?

**Answer**

The CI/CD pipeline triggers an Ansible playbook on the Control Node, which connects to the managed servers and applies the required configuration changes.

**Explanation**

This enables automated, repeatable, and reliable deployments, ensuring all servers remain in the desired state with minimal manual intervention.

```
