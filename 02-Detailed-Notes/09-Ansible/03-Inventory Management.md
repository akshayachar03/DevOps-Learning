# Inventory Management

## Overview

Inventory Management is the process of organizing and managing the systems (hosts) that Ansible controls.

The Inventory acts as the **source of truth** for Ansible by defining:

- Managed hosts
- Host groups
- Child groups
- Variables
- Connection information

A well-structured inventory makes automation scalable, reusable, and easier to maintain, especially in large environments.

> **Interview Tip**
>
> The Inventory tells **Ansible where to execute tasks**, while the Playbook tells **Ansible what tasks to execute**.

---

# Inventory Structure

## Overview

The Inventory Structure defines how managed hosts are organized within an Inventory file.

A well-designed inventory improves:

- Readability
- Scalability
- Reusability
- Environment separation

Inventory can be written in:

- INI format (most common for beginners)
- YAML format (recommended for larger projects)

---

## Why It Is Used

A proper inventory structure helps:

- Organize servers logically
- Separate environments
- Reduce duplication
- Simplify playbook execution

---

## Architecture / Working

```mermaid
flowchart LR
    Inventory --> WebGroup
    Inventory --> AppGroup
    Inventory --> DatabaseGroup

    WebGroup --> Web1
    WebGroup --> Web2

    AppGroup --> App1
    AppGroup --> App2

    DatabaseGroup --> DB1
```

---

## Key Components

| Component | Purpose |
|-----------|---------|
| Inventory File | Stores host definitions |
| Host | Individual managed server |
| Group | Collection of hosts |
| Variables | Host or group configuration |

---

## Types (if applicable)

Inventory Formats

- INI Inventory
- YAML Inventory

---

## Lifecycle / Workflow

```mermaid
flowchart LR
    Inventory --> ReadHosts
    ReadHosts --> LoadVariables
    LoadVariables --> ExecutePlaybook
```

---

## Configuration / Syntax (if applicable)

INI Example

```ini
[web]
web1
web2

[database]
db1
```

YAML Example

```yaml
all:
  children:
    web:
      hosts:
        web1:
        web2:
```

---

## Important Commands (if applicable)

Display Inventory

```bash
ansible-inventory --list
```

Display Inventory Graph

```bash
ansible-inventory --graph
```

---

## Important Files (if applicable)

| File | Purpose |
|------|---------|
| inventory | Host definitions |
| ansible.cfg | References inventory |

---

## Real-World Use Cases

- Organize production servers
- Separate environments
- Multi-tier application management

---

## Advantages

- Organized infrastructure
- Easy maintenance
- Supports scalability

---

## Limitations

- Poor structure makes automation difficult to maintain
- Static inventories require manual updates

---

## Common Interview Questions (Concept Only)

- What is an Inventory Structure?
- Why should hosts be grouped?
- Which inventory formats does Ansible support?

---

## Common Mistakes

- Mixing unrelated servers in one group
- Poor naming conventions
- Duplicate host entries

---

## Troubleshooting

| Problem | Cause | Solution |
|----------|--------|----------|
| Host missing | Incorrect inventory | Verify inventory structure |
| Group not found | Invalid group | Check group names |

Useful Commands

```bash
ansible-inventory --graph

ansible-inventory --list
```

---

## Summary

A well-designed Inventory Structure organizes managed hosts into logical groups, making Ansible automation scalable, maintainable, and easier to manage.

---

# Host Groups

## Overview

A Host Group is a logical collection of managed hosts.

Instead of running automation against individual servers, Ansible executes tasks against an entire group.

For example:

- Web Servers
- Database Servers
- Application Servers

> **Interview Tip**
>
> Playbooks usually target **groups**, not individual hosts.

---

## Why It Is Used

Host Groups help:

- Execute tasks on multiple servers
- Organize infrastructure
- Reduce duplicated configuration
- Improve automation

---

## Architecture / Working

```mermaid
flowchart LR
    WebGroup --> Web1
    WebGroup --> Web2
    WebGroup --> Web3
```

---

## Key Components

| Component | Purpose |
|-----------|---------|
| Group | Collection of hosts |
| Host | Managed server |

---

## Types (if applicable)

Common Groups

- web
- database
- application
- monitoring
- production
- development

---

## Lifecycle / Workflow

```mermaid
flowchart LR
    Group --> Hosts
    Hosts --> ExecuteTasks
```

---

## Configuration / Syntax (if applicable)

```ini
[web]
web1
web2
web3
```

Run Against Group

```bash
ansible web -m ping
```

---

## Important Commands (if applicable)

```bash
ansible web -m ping

ansible web -a "uptime"
```

---

## Important Files (if applicable)

inventory

---

## Real-World Use Cases

- Restart web servers
- Install Apache
- Deploy applications
- Patch Linux servers

---

## Advantages

- Simplifies automation
- Improves scalability
- Eases infrastructure management

---

## Limitations

- Incorrect grouping may execute tasks on unintended servers

---

## Common Interview Questions (Concept Only)

- What is a Host Group?
- Why use Host Groups?
- How do you execute a playbook on a group?

---

## Common Mistakes

- Poor group naming
- Adding hosts to incorrect groups

---

## Troubleshooting

```bash
ansible-inventory --graph

ansible web -m ping
```

---

## Summary

Host Groups allow administrators to automate multiple servers simultaneously, improving scalability and simplifying infrastructure management.

---

# Child Groups

## Overview

A Child Group is a group that contains one or more other groups.

It enables hierarchical organization of infrastructure.

Example:

```
Production
   ├── Web
   ├── Database
   └── Application
```

Instead of targeting each group separately, administrators can target the parent group.

> **Interview Tip**
>
> Child Groups improve scalability and are commonly used in enterprise environments.

---

## Why It Is Used

Child Groups provide:

- Hierarchical organization
- Simplified automation
- Easier environment management

---

## Architecture / Working

```mermaid
flowchart TD
    Production --> Web
    Production --> Database
    Production --> App

    Web --> Web1
    Web --> Web2

    Database --> DB1

    App --> App1
```

---

## Key Components

| Component | Purpose |
|-----------|---------|
| Parent Group | Contains child groups |
| Child Group | Contains hosts |

---

## Types (if applicable)

Hierarchy Example

- Production
- Development
- Testing

---

## Lifecycle / Workflow

```mermaid
flowchart LR
    ParentGroup --> ChildGroups
    ChildGroups --> Hosts
```

---

## Configuration / Syntax (if applicable)

```ini
[web]
web1
web2

[db]
db1

[production:children]
web
db
```

---

## Important Commands (if applicable)

```bash
ansible production -m ping
```

---

## Important Files (if applicable)

inventory

---

## Real-World Use Cases

- Multi-tier applications
- Enterprise environments
- Environment grouping

---

## Advantages

- Hierarchical organization
- Easier automation
- Reduced duplication

---

## Limitations

- Poor hierarchy increases complexity
- Deep nesting can make inventories harder to understand

---

## Common Interview Questions (Concept Only)

- What are Child Groups?
- Why use Child Groups?
- Difference between Host Groups and Child Groups?

---

## Common Mistakes

- Circular group definitions
- Excessive nesting

---

## Troubleshooting

```bash
ansible-inventory --graph
```

---

## Summary

Child Groups organize multiple host groups into a hierarchy, making enterprise inventories easier to manage and automate.

---

# Host Variables

## Overview

Host Variables are variables assigned to individual hosts.

They customize configuration for specific servers.

Examples:

- Hostname
- SSH user
- IP address
- Custom application settings

Host variables override group variables when both define the same variable.

> **Interview Tip**
>
> **Host Variables have higher precedence than Group Variables.**

---

## Why It Is Used

Host Variables enable:

- Server-specific configuration
- Flexible automation
- Reduced duplication

---

## Architecture / Working

```mermaid
flowchart LR
    HostVariables --> Web1
    HostVariables --> DB1
```

---

## Key Components

| Component | Purpose |
|-----------|---------|
| Variable | Stores host-specific data |
| Host | Uses variable |

---

## Types (if applicable)

Examples

- ansible_host
- ansible_user
- ansible_port
- custom variables

---

## Lifecycle / Workflow

```mermaid
flowchart LR
    Inventory --> LoadVariables
    LoadVariables --> ExecuteTasks
```

---

## Configuration / Syntax (if applicable)

```ini
web1 ansible_host=192.168.1.10 ansible_user=ubuntu
```

---

## Important Commands (if applicable)

Display Variables

```bash
ansible-inventory --list
```

---

## Important Files (if applicable)

| File | Purpose |
|------|---------|
| inventory | Host variables |
| host_vars/ | Host-specific variable files |

---

## Real-World Use Cases

- Different SSH users
- Different IP addresses
- Custom application ports

---

## Advantages

- Flexible configuration
- Host customization
- Easy management

---

## Limitations

- Large numbers of host variables become difficult to maintain
- Variable conflicts if naming is inconsistent

---

## Common Interview Questions (Concept Only)

- What are Host Variables?
- Where are Host Variables stored?
- Which takes precedence: Host Variables or Group Variables?

---

## Common Mistakes

- Defining duplicate variables
- Hardcoding sensitive values

---

## Troubleshooting

```bash
ansible-inventory --list
```

---

## Summary

Host Variables allow administrators to define server-specific configuration values, making automation flexible while maintaining reusable playbooks.

---

# Group Variables

## Overview

Group Variables are variables shared by every host in a Host Group.

Instead of repeating the same configuration for every server, the variable is defined once and automatically inherited by all group members.

> **Interview Tip**
>
> Use Group Variables for settings common to multiple servers, such as package names, application versions, or environment-specific values.

---

## Why It Is Used

Group Variables provide:

- Reduced duplication
- Consistent configuration
- Easier maintenance
- Better scalability

---

## Architecture / Working

```mermaid
flowchart LR
    GroupVariables --> WebGroup
    WebGroup --> Web1
    WebGroup --> Web2
    WebGroup --> Web3
```

---

## Key Components

| Component | Purpose |
|-----------|---------|
| Group Variable | Shared configuration |
| Host Group | Receives variables |
| Hosts | Inherit variables |

---

## Types (if applicable)

Examples

- Application version
- Package name
- Environment
- Time zone

---

## Lifecycle / Workflow

```mermaid
flowchart LR
    GroupVariables --> Group
    Group --> Hosts
    Hosts --> ExecuteTasks
```

---

## Configuration / Syntax (if applicable)

Inventory Example

```ini
[web]
web1
web2

[web:vars]
ansible_user=ubuntu
http_port=80
```

Directory Structure Example

```
group_vars/
└── web.yml
```

---

## Important Commands (if applicable)

View Variables

```bash
ansible-inventory --list
```

---

## Important Files (if applicable)

| File | Purpose |
|------|---------|
| inventory | Group variables |
| group_vars/ | Group variable files |

---

## Real-World Use Cases

- Common SSH user
- Web server configuration
- Shared application version
- Environment settings

---

## Advantages

- Eliminates duplicate configuration
- Simplifies management
- Improves consistency
- Easy to maintain

---

## Limitations

- Overridden by Host Variables when the same variable is defined
- Poor variable organization can make troubleshooting more difficult

---

## Common Interview Questions (Concept Only)

- What are Group Variables?
- Where are Group Variables stored?
- Difference between Host Variables and Group Variables?
- Which has higher precedence?

---

## Common Mistakes

- Defining identical variables in multiple locations
- Storing sensitive information in plain text instead of using Ansible Vault
- Using Group Variables for host-specific settings

---

## Troubleshooting

| Problem | Cause | Solution |
|----------|--------|----------|
| Variable not applied | Wrong group | Verify host membership |
| Unexpected value | Overridden by Host Variable | Check variable precedence |
| Variable not found | Incorrect file location | Verify `group_vars` structure |

Useful Commands

```bash
ansible-inventory --list

ansible-inventory --graph
```

---

## Summary

Group Variables define configuration shared by all hosts in a group, reducing duplication and improving consistency. They are ideal for common settings, while Host Variables should be used only for server-specific values. In Ansible's variable precedence, Host Variables override Group Variables when both define the same variable.
