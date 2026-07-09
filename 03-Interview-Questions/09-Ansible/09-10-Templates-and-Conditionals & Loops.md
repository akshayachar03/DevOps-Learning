# Templates, Conditionals & Loops Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What are Jinja2 Templates in Ansible?

**Answer**

Jinja2 Templates are dynamic configuration files that use variables and expressions to generate customized files for different servers or environments.

Example:

```jinja2
server_name={{ inventory_hostname }}
listen={{ web_port }}
```

**Explanation**

Instead of maintaining multiple static configuration files, a single template can generate different configurations using variables.

**Used in Production**

- Nginx configuration
- Apache Virtual Hosts
- Application configuration files
- Database configuration
- Kubernetes manifests

**Common Mistake**

Many beginners use the `copy` module instead of templates for files that contain environment-specific values.

---

### Question 2

**Question**

What is the purpose of the `template` module?

**Answer**

The `template` module copies a Jinja2 template from the control node to the managed node after replacing variables with their actual values.

Example:

```yaml
- name: Deploy nginx config
  template:
    src: nginx.conf.j2
    dest: /etc/nginx/nginx.conf
```

**Explanation**

Unlike the `copy` module, the `template` module renders the file before transferring it.

**Used in Production**

Deploying dynamic configuration files across Development, Testing, and Production environments.

---

### Question 3

**Question**

What is the difference between the `copy` module and the `template` module?

**Answer**

| copy | template |
|------|----------|
| Copies file exactly as it is | Replaces variables before copying |
| Static files | Dynamic files |
| No Jinja2 support | Full Jinja2 support |

**Explanation**

Use the `copy` module for static files and the `template` module for files requiring variable substitution.

**Common Mistake**

Using `copy` for configuration files that contain environment-specific settings.

---

### Question 4

**Question**

How are variables used inside Jinja2 templates?

**Answer**

Variables are referenced using double curly braces.

Example:

```jinja2
server_name={{ inventory_hostname }}
```

or

```jinja2
listen={{ web_port }}
```

**Explanation**

During playbook execution, Ansible replaces the placeholders with actual values.

**Used in Production**

Dynamic application configurations for multiple environments.

---

### Question 5

**Question**

What is the purpose of the `when` statement in Ansible?

**Answer**

The `when` statement executes a task only if a specified condition evaluates to true.

Example:

```yaml
- name: Install Apache
  apt:
    name: apache2
    state: present
  when: ansible_os_family == "Debian"
```

**Explanation**

Conditional execution allows one playbook to support multiple operating systems and environments.

**Used in Production**

- OS-specific tasks
- Environment-specific deployments
- Conditional package installation

---

### Question 6

**Question**

Can you use Facts with the `when` condition?

**Answer**

Yes.

Example:

```yaml
when: ansible_distribution == "Ubuntu"
```

**Explanation**

Facts provide system information that allows conditional execution based on operating system, hostname, memory, CPU, and many other attributes.

**Used in Production**

Deploying different software packages depending on the target server.

---

### Question 7

**Question**

What is the purpose of the `loop` keyword?

**Answer**

The `loop` keyword repeats the same task for multiple values.

Example:

```yaml
loop:
  - git
  - nginx
  - curl
```

**Explanation**

Instead of writing multiple similar tasks, one task processes each item in the list.

**Used in Production**

- Installing packages
- Creating users
- Copying files
- Creating directories

---

### Question 8

**Question**

What is `with_items`?

**Answer**

`with_items` is the older looping syntax used before the introduction of `loop`.

Example:

```yaml
with_items:
  - nginx
  - git
```

**Explanation**

Modern Ansible recommends using `loop` because it is simpler and more consistent.

**Common Mistake**

Some candidates think `with_items` is deprecated and unsupported. It still works but `loop` is preferred for new playbooks.

---

### Question 9

**Question**

What are the advantages of using loops?

**Answer**

Loops help to:

- Reduce duplicate code
- Improve readability
- Simplify maintenance
- Handle multiple resources efficiently

**Explanation**

Without loops, identical tasks must be repeated multiple times, making playbooks longer and harder to maintain.

**Used in Production**

Managing dozens of users, packages, directories, or configuration files.

---

### Question 10

**Question**

Can `when` and `loop` be used together?

**Answer**

Yes.

Example:

```yaml
- name: Install packages
  package:
    name: "{{ item }}"
    state: present
  loop:
    - nginx
    - git
  when: ansible_os_family == "RedHat"
```

**Explanation**

The loop iterates through each item, while the `when` condition determines whether the task should execute.

**Used in Production**

Installing packages only on specific operating systems.

---

### Question 11

**Question**

Why are Templates, Conditionals, and Loops considered essential Ansible features?

**Answer**

They make automation:

- Dynamic
- Reusable
- Environment-independent
- Easier to maintain

**Explanation**

These features eliminate repetitive code and allow one playbook to manage hundreds of servers with different configurations.

**Used in Production**

Nearly every enterprise Ansible project relies on templates, conditions, and loops.

---

### Question 12

**Question**

How do templates improve infrastructure automation?

**Answer**

Templates allow one configuration file to generate different outputs using variables.

**Explanation**

Instead of storing separate files for Development, QA, and Production, a single template generates all required configurations automatically.

**Used in Production**

- Web servers
- Load balancers
- Application servers
- Database configuration

**Common Mistake**

Maintaining multiple nearly identical configuration files instead of using a single reusable template.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

Your organization has Development, QA, and Production environments with different database hostnames. How would you manage the configuration files?

**Answer**

Create one Jinja2 template and use variables for the database hostname.

**Explanation**

This avoids maintaining multiple configuration files and reduces configuration errors.

---

### Scenario 2

**Question**

You need to install Apache only on Ubuntu servers and HTTPD only on RHEL servers. How would you implement this?

**Answer**

Use the `when` condition with Ansible Facts.

**Explanation**

Conditional execution allows a single playbook to support multiple operating systems.

---

### Scenario 3

**Question**

You need to install five packages on every server. Would you create five separate tasks?

**Answer**

No.

Use a `loop` with the package module.

**Explanation**

Loops reduce repetition and simplify maintenance.

---

### Scenario 4

**Question**

A configuration file contains the server hostname and IP address, which differ on every server. Which module should you use?

**Answer**

Use the `template` module.

**Explanation**

Templates dynamically generate configuration files using host-specific variables.

---

### Scenario 5

**Question**

A developer uses the `copy` module for an Nginx configuration that contains environment-specific values. What would you recommend?

**Answer**

Replace the `copy` module with the `template` module.

**Explanation**

Templates automatically substitute variables, making the configuration reusable across environments.

---

### Scenario 6

**Question**

Your playbook should restart a service only if the operating system is Ubuntu. How would you implement this?

**Answer**

Use the `when` condition with the appropriate Ansible Fact.

**Explanation**

The task executes only on matching systems, preventing unnecessary or unsupported operations.

---

### Scenario 7

**Question**

You need to create ten Linux users. What is the most efficient approach?

**Answer**

Use the `user` module with a `loop`.

**Explanation**

One task can create multiple users, improving readability and maintainability.

---

### Scenario 8

**Question**

Your template file is deployed successfully, but the variables appear literally as `{{ variable_name }}` in the destination file. What is the likely cause?

**Answer**

The file was copied using the `copy` module instead of the `template` module, or the source file does not have the correct Jinja2 syntax.

**Explanation**

Only the `template` module renders Jinja2 expressions before copying the file.

---

### Scenario 9

**Question**

A playbook installs Docker only when the variable `install_docker` is set to `true`. Which feature enables this behavior?

**Answer**

The `when` conditional.

**Explanation**

Conditional execution allows tasks to run only when specified criteria are met.

---

### Scenario 10

**Question**

Your playbook must create identical directories on fifty servers. How would you write the playbook efficiently?

**Answer**

Use the `file` module with a `loop`.

**Explanation**

Loops eliminate repetitive tasks, making the playbook shorter, cleaner, and easier to maintain.
