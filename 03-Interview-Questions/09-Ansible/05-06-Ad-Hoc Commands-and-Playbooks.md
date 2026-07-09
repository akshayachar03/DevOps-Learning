# Ad-Hoc Commands & Playbooks Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What are Ad-Hoc Commands in Ansible?

**Answer**

Ad-Hoc Commands are one-line Ansible commands used to execute simple tasks on managed nodes without creating a playbook.

Example:

```bash
ansible all -m ping
```

**Explanation**

Ad-Hoc Commands are ideal for quick administrative tasks such as checking connectivity, restarting services, copying files, or installing packages. For repetitive or complex automation, playbooks are the preferred approach.

**Used in Production**

- Connectivity checks
- Quick troubleshooting
- Service restarts
- Package installation
- File copying

**Common Mistake**

Many candidates think Ad-Hoc Commands replace playbooks. In reality, they are intended only for quick, one-time operations.

---

### Question 2

**Question**

How do you verify connectivity between the Ansible Control Node and managed nodes?

**Answer**

Use the Ansible Ping module.

Example:

```bash
ansible all -m ping
```

**Explanation**

The `ping` module verifies SSH connectivity and confirms that Ansible can successfully execute Python modules on the managed node. It does not send ICMP network ping requests.

**Used in Production**

Typically executed before running playbooks to ensure all target hosts are reachable.

**Common Mistake**

Candidates often assume the `ping` module sends ICMP echo requests like the Linux `ping` command.

---

### Question 3

**Question**

How do you execute a Linux command on multiple servers using Ansible?

**Answer**

Use the `command` module.

Example:

```bash
ansible webservers -m command -a "uptime"
```

**Explanation**

The command runs on every target host in the specified inventory group.

**Used in Production**

Commonly used for:

- Checking uptime
- Viewing disk usage
- Checking memory
- Running administrative commands

**Common Mistake**

Many candidates confuse the `command` module with the `shell` module. The `command` module does not process shell features such as pipes or redirection.

---

### Question 4

**Question**

How do you copy a file to multiple managed nodes?

**Answer**

Use the `copy` module.

Example:

```bash
ansible webservers -m copy -a "src=index.html dest=/var/www/html/index.html"
```

**Explanation**

The `copy` module transfers files from the Control Node to managed nodes.

**Used in Production**

- Deploying configuration files
- Deploying static web content
- Updating scripts
- Copying certificates

---

### Question 5

**Question**

How can you install a package using an Ad-Hoc Command?

**Answer**

For Ubuntu:

```bash
ansible webservers -m apt -a "name=nginx state=present" --become
```

For RHEL/CentOS:

```bash
ansible webservers -m yum -a "name=httpd state=present" --become
```

**Explanation**

Package modules automatically determine whether installation is required, making the operation idempotent.

**Used in Production**

Installing web servers, databases, monitoring agents, and utilities.

**Common Mistake**

Forgetting to use `--become` when administrative privileges are required.

---

### Question 6

**Question**

How do you manage Linux services using Ansible?

**Answer**

Use the `service` module.

Example:

```bash
ansible webservers -m service -a "name=nginx state=started" --become
```

**Explanation**

The module can:

- Start services
- Stop services
- Restart services
- Enable services
- Disable services

**Used in Production**

Managing services after deployments or configuration changes.

---

### Question 7

**Question**

What is an Ansible Playbook?

**Answer**

A Playbook is a YAML file containing one or more plays that define automated tasks to execute on managed nodes.

**Explanation**

Unlike Ad-Hoc Commands, playbooks support reusable, version-controlled, and repeatable automation.

**Used in Production**

- Application deployment
- Server configuration
- Multi-step automation
- Infrastructure provisioning

**Common Mistake**

Some candidates think playbooks execute only one task. A playbook can contain hundreds of tasks organized into multiple plays.

---

### Question 8

**Question**

Why does Ansible use YAML for Playbooks?

**Answer**

YAML is human-readable, simple to write, and uses indentation instead of brackets or braces.

Example:

```yaml
---
- hosts: webservers
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present
```

**Explanation**

YAML improves readability and simplifies infrastructure automation.

**Used in Production**

All Ansible playbooks are written using YAML syntax.

**Common Mistake**

Using tabs instead of spaces. YAML only supports spaces for indentation.

---

### Question 9

**Question**

What are the main components of an Ansible Playbook?

**Answer**

A typical playbook contains:

- Hosts
- Become
- Variables
- Tasks
- Handlers

Example:

```yaml
- hosts: webservers
  become: true
  vars:
    package: nginx

  tasks:
    - name: Install package
      apt:
        name: "{{ package }}"
        state: present
```

**Explanation**

Each component serves a specific purpose, making playbooks modular and maintainable.

---

### Question 10

**Question**

What is the difference between a Play and a Task?

**Answer**

A Play maps hosts to automation tasks.

A Task is an individual action performed using an Ansible module.

**Explanation**

One play contains multiple tasks executed sequentially.

**Used in Production**

A deployment play might contain tasks for:

- Installing packages
- Copying configuration files
- Restarting services

---

### Question 11

**Question**

What are Handlers in Ansible?

**Answer**

Handlers are special tasks that run only when notified by another task after a change occurs.

Example:

```yaml
notify: Restart Nginx
```

**Explanation**

Handlers prevent unnecessary service restarts by executing only when required.

**Used in Production**

Restarting:

- Nginx
- Apache
- MySQL
- Docker
- Kubernetes services

**Common Mistake**

Candidates often think handlers execute every time. They run only when triggered by a changed task.

---

### Question 12

**Question**

How are Variables used in Ansible Playbooks?

**Answer**

Variables store reusable values that can be referenced throughout a playbook.

Example:

```yaml
vars:
  package_name: nginx
```

Usage:

```yaml
name: "{{ package_name }}"
```

**Explanation**

Variables improve flexibility and reduce duplication.

**Used in Production**

Commonly used for:

- Package names
- Ports
- File paths
- Environment-specific values
- Usernames

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

You need to verify SSH connectivity to 200 Linux servers before deploying an application. What would you do?

**Answer**

Run:

```bash
ansible all -m ping
```

**Explanation**

The `ping` module quickly confirms that Ansible can communicate with every managed node.

---

### Scenario 2

**Question**

A configuration file has changed on 50 web servers. How would you deploy it?

**Answer**

Use the `copy` module in a playbook or an Ad-Hoc Command, followed by a handler to restart the web service only if the file changes.

**Explanation**

Handlers ensure services restart only when necessary, reducing unnecessary downtime.

---

### Scenario 3

**Question**

Your manager asks you to restart Apache on every web server immediately. Which approach would you use?

**Answer**

Use an Ad-Hoc Command:

```bash
ansible webservers -m service -a "name=httpd state=restarted" --become
```

**Explanation**

Ad-Hoc Commands are ideal for quick operational tasks.

---

### Scenario 4

**Question**

You need to install Nginx on 100 new servers. Would you use an Ad-Hoc Command or a Playbook?

**Answer**

Use a Playbook.

**Explanation**

Installing software across many servers is a repeatable task that benefits from version control, documentation, and reusability.

---

### Scenario 5

**Question**

After updating a configuration file, your playbook restarts Nginx even when the file hasn't changed. How can this be improved?

**Answer**

Use a Handler triggered only when the configuration file changes.

**Explanation**

Handlers avoid unnecessary service interruptions.

---

### Scenario 6

**Question**

A playbook fails with a YAML syntax error. What is the most common cause?

**Answer**

Incorrect indentation, especially using tabs instead of spaces.

**Explanation**

YAML relies entirely on consistent space-based indentation.

---

### Scenario 7

**Question**

A package installation task fails with a "Permission denied" error. What would you check?

**Answer**

Verify that the play or task uses:

```yaml
become: true
```

or execute the Ad-Hoc Command using:

```bash
--become
```

**Explanation**

Installing packages requires administrative privileges.

---

### Scenario 8

**Question**

You need to install different packages in Development and Production environments. How can you avoid duplicating the playbook?

**Answer**

Store the package names in variables and reference them within the playbook.

**Explanation**

Variables make playbooks reusable across multiple environments.

---

### Scenario 9

**Question**

Your deployment requires multiple sequential steps: install software, copy configuration files, start services, and verify the deployment. Which Ansible feature is best suited for this?

**Answer**

An Ansible Playbook.

**Explanation**

Playbooks organize multiple tasks into a structured, repeatable automation workflow.

---

### Scenario 10

**Question**

During troubleshooting, you need to quickly check disk usage on every application server without creating a playbook. What would you do?

**Answer**

Run an Ad-Hoc Command:

```bash
ansible appservers -m command -a "df -h"
```

**Explanation**

Ad-Hoc Commands are the fastest option for one-time operational checks and troubleshooting tasks.
