# Inventory Management & SSH Authentication Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is an Inventory in Ansible, and why is it important?

**Answer**

An Inventory is a file that contains the list of managed hosts (servers) and groups that Ansible manages. It tells Ansible where to execute automation tasks.

**Explanation**

Every Ansible command or playbook requires an inventory to identify the target systems. The inventory can contain hostnames, IP addresses, groups, and connection-related variables.

**Used in Production**

- Managing web servers
- Managing database servers
- Managing cloud VMs
- Organizing large infrastructures

**Common Mistake**

Many candidates think the inventory only stores IP addresses. It can also store variables, SSH users, ports, and group information.

---

### Question 2

**Question**

What is the typical structure of an Ansible Inventory?

**Answer**

An inventory is organized into hosts and groups.

Example:

```ini
[webservers]
192.168.1.10
192.168.1.11

[appservers]
192.168.1.20

[dbservers]
192.168.1.30
```

**Explanation**

Grouping hosts allows administrators to execute the same automation on multiple servers simultaneously.

**Used in Production**

Production environments commonly separate servers into:

- Web Servers
- Application Servers
- Database Servers
- Monitoring Servers

**Common Mistake**

Candidates sometimes create one inventory entry per server instead of organizing related servers into groups.

---

### Question 3

**Question**

What are Host Groups in Ansible?

**Answer**

Host Groups are logical collections of managed nodes that perform the same function.

**Explanation**

Instead of targeting individual hosts, administrators can execute automation against an entire group.

Example:

```bash
ansible webservers -m ping
```

This command runs against every server in the `webservers` group.

**Used in Production**

Host groups simplify large-scale automation across hundreds of servers.

---

### Question 4

**Question**

What are Child Groups in Ansible?

**Answer**

Child Groups allow multiple groups to be combined into a parent group.

Example:

```ini
[webservers]
web1
web2

[appservers]
app1
app2

[production:children]
webservers
appservers
```

**Explanation**

Executing a playbook against the `production` group automatically targets all child groups.

**Used in Production**

Useful for organizing environments such as:

- Production
- Development
- Testing
- Staging

**Common Mistake**

Many candidates think child groups contain hosts directly. Instead, they reference other groups.

---

### Question 5

**Question**

What are Host Variables in Ansible?

**Answer**

Host Variables are variables assigned to a specific managed node.

Example:

```ini
web1 ansible_host=192.168.1.10 ansible_user=ubuntu
```

**Explanation**

Host variables customize configurations for individual servers.

**Used in Production**

Commonly used for:

- SSH usernames
- Ports
- Application versions
- Environment-specific settings

---

### Question 6

**Question**

What are Group Variables in Ansible?

**Answer**

Group Variables apply the same configuration to every host within a group.

Example:

```ini
[webservers]
web1
web2

[webservers:vars]
ansible_user=ubuntu
```

**Explanation**

Instead of repeating variables for every host, group variables define them once.

**Used in Production**

Ideal for configuring common settings shared by multiple servers.

**Common Mistake**

Candidates often duplicate identical host variables instead of using group variables.

---

### Question 7

**Question**

How does Ansible connect to managed nodes?

**Answer**

Ansible primarily uses SSH for Linux systems and WinRM for Windows systems.

**Explanation**

The Control Node establishes a secure SSH connection, executes modules remotely, collects the results, and disconnects.

**Used in Production**

SSH is the standard communication method for Linux automation.

---

### Question 8

**Question**

Why are SSH Keys preferred over password authentication?

**Answer**

SSH Keys provide stronger security, enable passwordless authentication, and support automation.

**Explanation**

A public key is stored on the managed node, while the private key remains on the Control Node. Authentication occurs without transmitting passwords.

**Used in Production**

Most enterprise automation relies on SSH key-based authentication.

**Common Mistake**

Using passwords in production automation is discouraged because they are less secure and difficult to manage.

---

### Question 9

**Question**

Can Ansible use password authentication?

**Answer**

Yes.

Ansible supports password authentication using the `--ask-pass` option or inventory variables.

Example:

```bash
ansible all -m ping --ask-pass
```

**Explanation**

Although supported, password authentication is generally used only in testing or small environments.

**Used in Production**

SSH key authentication is the recommended approach.

---

### Question 10

**Question**

What is Become in Ansible?

**Answer**

Become is Ansible's privilege escalation feature that allows tasks to execute as another user, typically the root user.

**Explanation**

Instead of logging in directly as root, administrators log in using a normal user and elevate privileges only when required.

Example:

```yaml
become: true
```

**Used in Production**

Installing packages, modifying system files, and managing services typically require elevated privileges.

**Common Mistake**

Many candidates think Become is only for root access. It can switch to any user.

---

### Question 11

**Question**

What is the relationship between Become and sudo?

**Answer**

Become uses privilege escalation methods such as `sudo` to execute administrative tasks.

Example:

```yaml
become: true
become_method: sudo
```

**Explanation**

Ansible authenticates using a regular user account and uses sudo whenever elevated privileges are required.

**Used in Production**

This follows the security principle of least privilege.

---

### Question 12

**Question**

How would you securely authenticate Ansible to production Linux servers?

**Answer**

Use:

- SSH key authentication
- Non-root user accounts
- Become (sudo) for privileged tasks
- Inventory variables for connection details
- Secure private key storage

**Explanation**

This approach improves security while allowing fully automated infrastructure management.

**Used in Production**

Nearly all enterprise Ansible environments follow this authentication model.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

Your organization has 50 Web servers and 20 Database servers. How would you organize the inventory?

**Answer**

Create separate host groups:

```ini
[webservers]
...

[dbservers]
...
```

**Explanation**

Grouping simplifies automation by allowing playbooks to target all related servers together.

---

### Scenario 2

**Question**

A playbook needs to run only on production servers. How would you organize your inventory?

**Answer**

Create a parent group using child groups.

Example:

```ini
[production:children]
webservers
dbservers
```

**Explanation**

Running the playbook against `production` automatically targets every production server.

---

### Scenario 3

**Question**

Ansible reports "Permission denied (publickey)" while connecting to a server. What would you check first?

**Answer**

Verify:

- SSH key exists
- Public key is installed on the target server
- Private key permissions
- SSH user
- SSH service
- Inventory configuration

**Explanation**

This error usually indicates an SSH authentication issue.

---

### Scenario 4

**Question**

Your playbook fails while installing packages with a "Permission denied" error. What is the likely cause?

**Answer**

The task requires administrative privileges, but `become: true` is missing.

**Explanation**

Package installation typically requires root or sudo access.

---

### Scenario 5

**Question**

Different servers require different SSH usernames. How would you configure this?

**Answer**

Use Host Variables.

Example:

```ini
web1 ansible_user=ubuntu
db1 ansible_user=ec2-user
```

**Explanation**

Host variables allow each server to use its own connection settings.

---

### Scenario 6

**Question**

All web servers use the same SSH username. How can you avoid repeating the configuration?

**Answer**

Use Group Variables.

Example:

```ini
[webservers:vars]
ansible_user=ubuntu
```

**Explanation**

Group variables reduce duplication and simplify maintenance.

---

### Scenario 7

**Question**

Your security team disables password-based SSH login. Will Ansible still work?

**Answer**

Yes.

Configure SSH key authentication for the managed nodes.

**Explanation**

SSH keys are the recommended authentication method for Ansible.

---

### Scenario 8

**Question**

An inventory contains 500 servers. Why is using host groups better than targeting individual hosts?

**Answer**

Host groups simplify management, improve readability, reduce duplication, and allow automation to run against logical server categories.

**Explanation**

Grouping makes large infrastructures significantly easier to manage.

---

### Scenario 9

**Question**

A playbook must restart services on all application servers but not on database servers. How would you accomplish this?

**Answer**

Execute the playbook only against the `appservers` group.

**Explanation**

Host groups allow precise targeting of automation tasks.

---

### Scenario 10

**Question**

Your company follows the security policy that direct root SSH login is prohibited. How would Ansible perform administrative tasks?

**Answer**

Connect using a normal user account with SSH keys and use `become: true` (sudo) for tasks requiring elevated privileges.

**Explanation**

This is the standard enterprise approach because it improves security, supports auditing, and follows the principle of least privilege.
