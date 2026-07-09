# Roles & Ansible Galaxy Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What are Roles in Ansible?

**Answer**

Roles are a way to organize Ansible playbooks into reusable, modular components. A role groups related tasks, variables, handlers, templates, files, and defaults into a standardized directory structure.

**Explanation**

Roles promote code reuse, simplify maintenance, and make automation projects easier to scale. Instead of keeping everything in a single playbook, each application or service can have its own role.

**Used in Production**

- Installing Nginx
- Configuring Apache
- Deploying Docker
- Database installation
- User management

**Common Mistake**

Many beginners create one large playbook containing hundreds of tasks instead of separating them into reusable roles.

---

### Question 2

**Question**

Why are Roles preferred over large playbooks?

**Answer**

Roles improve:

- Reusability
- Readability
- Maintainability
- Scalability
- Collaboration among teams

**Explanation**

Large playbooks become difficult to manage as infrastructure grows. Roles divide automation into logical units that can be reused across multiple projects.

**Used in Production**

Enterprise DevOps teams create separate roles for web servers, databases, monitoring agents, Docker, Kubernetes, and security configurations.

---

### Question 3

**Question**

What is the standard directory structure of an Ansible Role?

**Answer**

A typical role structure is:

```text
roles/
└── nginx/
    ├── defaults/
    ├── files/
    ├── handlers/
    ├── meta/
    ├── tasks/
    ├── templates/
    ├── vars/
    └── README.md
```

**Explanation**

Each directory serves a specific purpose:

- **tasks/** – Main automation tasks
- **handlers/** – Restart or reload services
- **templates/** – Jinja2 templates
- **files/** – Static files
- **vars/** – Variables
- **defaults/** – Default variable values
- **meta/** – Role dependencies and metadata

**Common Mistake**

Placing all tasks in one file instead of organizing them within the role structure.

---

### Question 4

**Question**

What is the purpose of the `tasks` directory in a Role?

**Answer**

The `tasks` directory contains the automation tasks executed by the role.

The entry point is:

```text
tasks/main.yml
```

**Explanation**

When a role is executed, Ansible automatically starts with `tasks/main.yml`.

**Used in Production**

Installing software, configuring services, creating users, deploying applications, and updating configuration files.

---

### Question 5

**Question**

How do you use a Role in a playbook?

**Answer**

Specify the role under the `roles` section.

Example:

```yaml
- hosts: webservers
  roles:
    - nginx
```

**Explanation**

Ansible automatically loads all required components of the role, including tasks, handlers, variables, templates, and files.

**Used in Production**

Application deployment pipelines where multiple reusable roles are executed in sequence.

---

### Question 6

**Question**

What are Role Variables?

**Answer**

Role Variables are variables defined specifically for a role.

Common locations:

```text
defaults/main.yml
```

or

```text
vars/main.yml
```

**Explanation**

These variables customize the behavior of the role without modifying its tasks.

**Used in Production**

Changing package names, ports, configuration paths, service names, and environment-specific settings.

---

### Question 7

**Question**

What is the difference between `defaults` and `vars` in a Role?

**Answer**

| defaults | vars |
|----------|------|
| Lowest variable precedence | Higher variable precedence |
| Easily overridden | Difficult to override |
| Used for configurable values | Used for fixed internal values |

**Explanation**

Default values allow users to customize a role without editing its source code.

**Common Mistake**

Placing configurable values in `vars`, making them harder to override.

---

### Question 8

**Question**

What is Ansible Galaxy?

**Answer**

Ansible Galaxy is the official repository for sharing and downloading reusable Ansible Roles and Collections.

**Explanation**

Instead of writing every role from scratch, teams can install community-maintained roles from Galaxy.

**Used in Production**

Installing:

- Docker
- Nginx
- Apache
- MySQL
- PostgreSQL
- Kubernetes
- Monitoring tools

---

### Question 9

**Question**

How do you install a Role from Ansible Galaxy?

**Answer**

Use:

```bash
ansible-galaxy install <role_name>
```

Example:

```bash
ansible-galaxy install geerlingguy.nginx
```

**Explanation**

The role is downloaded into the configured roles directory and can be referenced directly in playbooks.

**Used in Production**

Rapid deployment of commonly used infrastructure components.

---

### Question 10

**Question**

How do you use an Ansible Galaxy Role in a playbook?

**Answer**

After installation:

```yaml
- hosts: webservers
  roles:
    - geerlingguy.nginx
```

**Explanation**

Ansible loads the downloaded role exactly like a locally developed role.

**Used in Production**

Organizations often combine community roles with their own custom roles.

---

### Question 11

**Question**

What are the benefits of using Ansible Galaxy Roles?

**Answer**

Benefits include:

- Faster development
- Reusable automation
- Community-tested code
- Reduced manual effort
- Standardized deployments

**Explanation**

Galaxy provides prebuilt automation for many common technologies, allowing engineers to focus on customization rather than starting from scratch.

**Common Mistake**

Blindly using community roles in production without reviewing their tasks and security implications.

---

### Question 12

**Question**

When should you create your own Role instead of using an Ansible Galaxy Role?

**Answer**

Create your own role when:

- Company-specific standards are required
- Custom application deployment is needed
- Security policies differ from community defaults
- Existing Galaxy roles do not meet business requirements

**Explanation**

Community roles are excellent starting points, but enterprise environments often require custom automation.

**Used in Production**

Internal application deployments, organization-specific security hardening, and compliance automation.

---

# Scenario-Based Interview Questions

### Scenario 1

**Question**

Your playbook has grown to over 500 lines and is difficult to maintain. How would you improve it?

**Answer**

Break the playbook into reusable Ansible Roles.

**Explanation**

Roles separate functionality into logical units, improving readability, maintainability, and reusability.

---

### Scenario 2

**Question**

Your team needs to install Nginx on hundreds of servers across multiple projects. How would you avoid duplicating code?

**Answer**

Create an `nginx` Role and reuse it across all playbooks.

**Explanation**

A reusable role eliminates duplicate tasks and ensures consistent deployments.

---

### Scenario 3

**Question**

You need to deploy Docker on multiple environments, but package versions differ between Development and Production. How would you design the role?

**Answer**

Store configurable values in `defaults/main.yml` and override them using inventory or playbook variables.

**Explanation**

This keeps the role reusable while allowing environment-specific customization.

---

### Scenario 4

**Question**

Your organization wants to deploy Apache quickly without writing automation from scratch. What would you do?

**Answer**

Install a trusted Apache Role from Ansible Galaxy.

**Explanation**

Galaxy provides tested community roles that significantly reduce implementation time.

---

### Scenario 5

**Question**

A downloaded Galaxy Role installs unnecessary packages that violate your organization's standards. What should you do?

**Answer**

Review the role's source code, customize it if necessary, or create a company-specific role.

**Explanation**

Community roles should always be reviewed before production use to ensure they align with organizational policies.

---

### Scenario 6

**Question**

You need to deploy the same application across Development, QA, and Production with different configuration values. How would you design the automation?

**Answer**

Create a reusable Role and provide environment-specific variables through inventory or variable files.

**Explanation**

This approach separates logic from configuration, making deployments consistent and easier to maintain.

---

### Scenario 7

**Question**

Your team uses the same Docker installation tasks in five different playbooks. What improvement would you suggest?

**Answer**

Move the common tasks into a Docker Role and reference it from each playbook.

**Explanation**

Roles eliminate duplicated code and simplify updates because changes only need to be made in one place.

---

### Scenario 8

**Question**

A Galaxy Role was updated with breaking changes, causing deployment failures. How would you prevent this in the future?

**Answer**

Pin the role to a tested version, review release notes before upgrading, and validate changes in a non-production environment.

**Explanation**

Version pinning and testing prevent unexpected behavior from affecting production deployments.

---

### Scenario 9

**Question**

A teammate stores all configurable values in `vars/main.yml`, making overrides difficult. What would you recommend?

**Answer**

Move user-configurable values to `defaults/main.yml` and reserve `vars/main.yml` for values that should rarely change.

**Explanation**

Using `defaults` for configurable settings makes roles more flexible and reusable across environments.

---

### Scenario 10

**Question**

Your organization wants every DevOps engineer to use the same automation for installing monitoring agents. How would you implement this?

**Answer**

Develop a standardized internal Role or maintain a shared Ansible Galaxy repository containing approved Roles.

**Explanation**

Centralized, reusable roles ensure consistent configurations, simplify maintenance, and reduce deployment errors across all teams.
