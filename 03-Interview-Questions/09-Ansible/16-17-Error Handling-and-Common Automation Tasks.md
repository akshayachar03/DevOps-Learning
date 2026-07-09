# Error Handling & Common Automation Tasks Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is error handling in Ansible?

**Answer**

Error handling in Ansible allows you to control how playbooks respond when a task fails. Instead of stopping the entire playbook, you can define conditions to ignore, customize, or detect failures.

**Explanation**

By default, Ansible stops executing tasks on a host when a task fails. Error handling features provide flexibility for production automation where certain failures are expected or should not interrupt the workflow.

**Used in Production**

- Optional package installation
- Cleanup operations
- Multi-server deployments
- Rolling deployments

**Common Mistake**

Using `ignore_errors` for critical tasks, which can hide genuine problems and lead to inconsistent system states.

---

### Question 2

**Question**

What is the purpose of `ignore_errors`?

**Answer**

`ignore_errors: yes` tells Ansible to continue executing the playbook even if the task fails.

Example:

```yaml
- name: Install package
  apt:
    name: nginx
    state: present
  ignore_errors: yes
```

**Explanation**

This is useful when a failed task should not stop the remaining automation.

**Used in Production**

- Cleanup tasks
- Optional software installation
- Non-critical validation steps

**Common Mistake**

Applying `ignore_errors` to important deployment or configuration tasks where failures should halt execution.

---

### Question 3

**Question**

What is `failed_when` in Ansible?

**Answer**

`failed_when` allows you to define your own condition for determining whether a task should fail.

Example:

```yaml
failed_when: result.rc != 0
```

**Explanation**

Instead of relying on the module's default behavior, you can define custom failure logic.

**Used in Production**

- Script execution
- Command validation
- Application health verification

---

### Question 4

**Question**

What is `changed_when`?

**Answer**

`changed_when` allows you to control when Ansible reports a task as "changed."

Example:

```yaml
changed_when: false
```

**Explanation**

Some commands always report changes even when nothing has actually changed. `changed_when` helps produce accurate playbook reports.

**Used in Production**

- Health checks
- Validation scripts
- Read-only commands

**Common Mistake**

Ignoring inaccurate "changed" status, making reports misleading.

---

### Question 5

**Question**

Why are `failed_when` and `changed_when` important?

**Answer**

They allow automation to accurately represent task results instead of relying solely on default module behavior.

**Explanation**

Custom conditions improve reporting accuracy and prevent false failures or false changes.

**Used in Production**

CI/CD pipelines, validation scripts, monitoring, and compliance checks.

---

### Question 6

**Question**

How is package installation automated in Ansible?

**Answer**

Using package management modules such as:

- `apt`
- `yum`
- `package`

Example:

```yaml
- name: Install Nginx
  package:
    name: nginx
    state: present
```

**Explanation**

Ansible automatically selects the appropriate package manager when using the `package` module.

**Used in Production**

Installing web servers, databases, Docker, Kubernetes, monitoring agents, and utilities.

---

### Question 7

**Question**

How is user management performed in Ansible?

**Answer**

Using the `user` module.

Example:

```yaml
- name: Create user
  user:
    name: devops
    state: present
```

**Explanation**

The module creates, modifies, or removes Linux user accounts.

**Used in Production**

- Creating deployment users
- Managing service accounts
- User onboarding and offboarding

---

### Question 8

**Question**

How is file management handled in Ansible?

**Answer**

Using modules such as:

- `copy`
- `template`
- `file`

**Explanation**

These modules create directories, copy files, deploy templates, modify permissions, and manage ownership.

**Used in Production**

- Configuration deployment
- SSL certificates
- Application files
- Directory creation

---

### Question 9

**Question**

How is service management automated in Ansible?

**Answer**

Using the `service` module.

Example:

```yaml
- name: Start Nginx
  service:
    name: nginx
    state: started
```

**Explanation**

The module starts, stops, restarts, reloads, or enables services.

**Used in Production**

Managing Apache, Nginx, Docker, MySQL, PostgreSQL, SSH, and other services.

---

### Question 10

**Question**

How is configuration deployment performed in Ansible?

**Answer**

Using the `template` module together with Jinja2 templates.

**Explanation**

Templates generate dynamic configuration files by replacing variables with environment-specific values before deployment.

**Used in Production**

- Nginx
- Apache
- HAProxy
- Application configuration
- Database configuration

---

### Question 11

**Question**

How is application deployment automated in Ansible?

**Answer**

Applications are deployed using combinations of modules such as:

- `git`
- `copy`
- `template`
- `service`
- `unarchive`

**Explanation**

Typical deployment includes:

- Download application
- Deploy files
- Update configuration
- Restart service
- Verify deployment

**Used in Production**

Web applications, Java applications, Node.js applications, Python applications, and microservices.

---

### Question 12

**Question**

Why is Ansible widely used for common automation tasks?

**Answer**

Because it provides reusable, idempotent, and agentless automation that works consistently across many servers.

**Explanation**

Instead of executing commands manually, engineers define the desired state in playbooks, allowing Ansible to perform repeatable and reliable automation.

**Used in Production**

- Server provisioning
- Application deployment
- Configuration management
- Patch management
- Infrastructure maintenance

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

A package installation fails on one server, but you want the remaining tasks to continue because the package is optional. How would you handle this?

**Answer**

Use `ignore_errors: yes` for the package installation task.

**Explanation**

This allows the playbook to continue executing while preventing a non-critical failure from stopping the deployment.

---

### Scenario 2

**Question**

A custom shell script returns exit code 1 even though the operation completed successfully. How would you prevent Ansible from marking the task as failed?

**Answer**

Use `failed_when` to define the correct success condition.

**Explanation**

Custom failure conditions ensure Ansible interprets command results accurately.

---

### Scenario 3

**Question**

A validation command always appears as "changed" even though it only checks system status. How would you fix this?

**Answer**

Use:

```yaml
changed_when: false
```

**Explanation**

This ensures reports correctly show that the task performed validation without modifying the system.

---

### Scenario 4

**Question**

Your team needs to create fifty Linux users across hundreds of servers. How would you automate this?

**Answer**

Use the `user` module together with a `loop`.

**Explanation**

The `user` module manages accounts efficiently while loops eliminate repetitive tasks.

---

### Scenario 5

**Question**

A new version of your application needs to be deployed on all web servers with updated configuration files. How would you automate the deployment?

**Answer**

Use modules such as `git`, `template`, `copy`, and `service` to deploy the application, update configuration files, and restart the service.

**Explanation**

This provides a repeatable deployment process with minimal manual intervention.

---

### Scenario 6

**Question**

Your Nginx configuration differs between Development and Production. Which Ansible feature would you use?

**Answer**

Deploy the configuration using the `template` module with Jinja2 variables.

**Explanation**

Templates generate environment-specific configuration files from a single reusable source.

---

### Scenario 7

**Question**

A service must restart only after its configuration file changes. How would you implement this?

**Answer**

Deploy the configuration using the `template` or `copy` module and notify a handler that restarts the service only when a change occurs.

**Explanation**

Handlers prevent unnecessary service restarts, improving application availability.

---

### Scenario 8

**Question**

You need to deploy an application from a Git repository to multiple servers. What Ansible modules would you use?

**Answer**

Use the `git` module to clone or update the repository, followed by the `template`, `copy`, and `service` modules as required.

**Explanation**

This automates the complete deployment process from source code retrieval to service restart.

---

### Scenario 9

**Question**

A deployment creates application files but fails to start the service because the configuration is invalid. How would you improve the playbook?

**Answer**

Validate the configuration before restarting the service and use `failed_when` if custom validation logic is required.

**Explanation**

Validating configurations before restarting services prevents application downtime.

---

### Scenario 10

**Question**

Your organization wants a standardized playbook for installing software, creating users, deploying configuration files, and managing services on all Linux servers. How would you design it?

**Answer**

Create reusable Roles containing package installation, user management, file management, configuration deployment, and service management tasks, then reuse these roles across all environments.

**Explanation**

Roles improve modularity, maintainability, and consistency while supporting enterprise-scale automation.
