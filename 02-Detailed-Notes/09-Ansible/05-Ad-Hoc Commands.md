# Ad-Hoc Commands

## Overview

Ad-Hoc Commands are one-line Ansible commands used to execute a single task on one or more managed hosts without creating a Playbook.

They are commonly used for:

- Quick administration
- Troubleshooting
- Testing connectivity
- Installing packages
- Restarting services
- Copying files

Unlike Playbooks, Ad-Hoc Commands are **not reusable** and are intended for immediate execution.

> **Interview Tip**
>
> **Playbooks** are used for complex, repeatable automation, whereas **Ad-Hoc Commands** are used for quick, one-time tasks.

---

# Ping Hosts

## Overview

The `ping` module verifies whether Ansible can successfully connect and authenticate with managed hosts.

Unlike the traditional Linux `ping` command, Ansible's `ping` module **does not use ICMP**. It establishes an SSH connection, runs a small Python module on the remote host, and expects a response of `"pong"`.

---

## Why It Is Used

- Verify SSH connectivity
- Validate authentication
- Confirm Python availability
- Test inventory configuration
- Verify Ansible installation

---

## Architecture / Working

```mermaid
flowchart LR
    ControlNode -->|SSH| ManagedNode
    ManagedNode --> ExecutePingModule
    ExecutePingModule --> Pong
    Pong --> ControlNode
```

---

## Key Components

| Component | Purpose |
|-----------|---------|
| Control Node | Sends ping module |
| SSH | Secure connection |
| Python | Executes module |
| Managed Node | Returns pong |

---

## Types (if applicable)

- Ping all hosts
- Ping a host group
- Ping a specific host

---

## Lifecycle / Workflow

```mermaid
flowchart LR
    ReadInventory --> SSHConnect
    SSHConnect --> ExecutePing
    ExecutePing --> ReceivePong
```

---

## Configuration / Syntax (if applicable)

Ping All Hosts

```bash
ansible all -m ping
```

Ping Web Servers

```bash
ansible web -m ping
```

Ping Specific Host

```bash
ansible web1 -m ping
```

---

## Important Commands (if applicable)

```bash
ansible all -m ping

ansible web -m ping

ansible db -m ping
```

---

## Important Files (if applicable)

| File | Purpose |
|------|---------|
| inventory | Managed hosts |
| ansible.cfg | Default inventory configuration |

---

## Real-World Use Cases

- Verify newly added servers
- Test SSH configuration
- Validate inventory
- Confirm network connectivity

---

## Advantages

- Fast connectivity verification
- Simple troubleshooting
- Confirms authentication

---

## Limitations

- Does not test ICMP
- Requires Python on most Linux hosts
- SSH must be accessible

---

## Common Interview Questions (Concept Only)

- Does `ansible ping` use ICMP?
- What does the ping module verify?
- Why does the ping module return `"pong"`?

---

## Common Mistakes

- Assuming it works like Linux ping
- Firewall blocking SSH
- Incorrect inventory

---

## Troubleshooting

| Problem | Cause | Solution |
|----------|--------|----------|
| UNREACHABLE | SSH issue | Verify SSH connectivity |
| Authentication failed | Wrong credentials | Verify SSH keys or password |
| Python error | Python missing | Install Python |

Useful Commands

```bash
ansible all -m ping

ssh user@host
```

---

## Summary

The `ping` module verifies Ansible connectivity by testing SSH authentication and module execution. It is the first command administrators should run before executing automation.

---

# Execute Commands

## Overview

The `command` and `shell` modules execute commands on remote hosts.

These modules are frequently used for:

- Troubleshooting
- Viewing system information
- Running administrative commands
- Quick server management

> **Interview Tip**
>
> **command** is safer because it does not invoke a shell.
>
> **shell** is more flexible because it supports shell features like pipes, redirects, and environment variables.

---

## Why It Is Used

- Run Linux commands
- Gather system information
- Restart applications
- Execute scripts

---

## Architecture / Working

```mermaid
flowchart LR
    ControlNode --> SSH
    SSH --> ManagedNode
    ManagedNode --> ExecuteCommand
    ExecuteCommand --> ReturnOutput
```

---

## Key Components

| Component | Purpose |
|-----------|---------|
| command module | Executes commands directly |
| shell module | Executes commands through a shell |

---

## Types (if applicable)

- command
- shell

---

## Lifecycle / Workflow

```mermaid
flowchart LR
    SSH --> ExecuteCommand
    ExecuteCommand --> ReturnResult
```

---

## Configuration / Syntax (if applicable)

Run Command

```bash
ansible all -a "uptime"
```

Using command Module

```bash
ansible all -m command -a "hostname"
```

Using shell Module

```bash
ansible all -m shell -a "df -h | grep /"
```

---

## Important Commands (if applicable)

```bash
ansible all -a "hostname"

ansible all -m command -a "date"

ansible all -m shell -a "free -m"
```

---

## Important Files (if applicable)

Inventory

---

## Real-World Use Cases

- Check disk usage
- View uptime
- Verify services
- Collect system information

---

## Advantages

- Fast execution
- Simple syntax
- Useful for troubleshooting

---

## Limitations

- Not ideal for repeatable automation
- Shell module may introduce security risks if input is not validated

---

## Common Interview Questions (Concept Only)

- Difference between command and shell modules?
- When should shell be used?
- Why is command considered safer?

---

## Common Mistakes

- Using shell unnecessarily
- Executing destructive commands on all hosts
- Forgetting host groups

---

## Troubleshooting

```bash
ansible all -m command -a "hostname"

ansible all -m shell -a "whoami"
```

---

## Summary

The `command` and `shell` modules execute commands remotely. Use `command` whenever possible and use `shell` only when shell features are required.

---

# Copy Files

## Overview

The `copy` module transfers files from the Control Node to Managed Nodes.

It is one of the most frequently used Ansible modules for:

- Configuration deployment
- Script distribution
- Application deployment
- Certificate management

---

## Why It Is Used

- Copy configuration files
- Deploy scripts
- Distribute certificates
- Transfer application files

---

## Architecture / Working

```mermaid
flowchart LR
    ControlNode --> CopyModule
    CopyModule --> ManagedNode
    ManagedNode --> DestinationFile
```

---

## Key Components

| Component | Purpose |
|-----------|---------|
| Source | Local file |
| Destination | Remote location |
| Copy Module | Transfers file |

---

## Types (if applicable)

- File copy
- Content copy
- Directory copy

---

## Lifecycle / Workflow

```mermaid
flowchart LR
    SelectFile --> Transfer
    Transfer --> Verify
```

---

## Configuration / Syntax (if applicable)

Copy File

```bash
ansible web -m copy -a "src=index.html dest=/var/www/html/index.html"
```

Copy Script

```bash
ansible all -m copy -a "src=script.sh dest=/tmp/script.sh mode=0755"
```

---

## Important Commands (if applicable)

```bash
ansible all -m copy -a "src=file.txt dest=/tmp/file.txt"
```

---

## Important Files (if applicable)

Source File

Destination File

---

## Real-World Use Cases

- Deploy web pages
- Copy SSL certificates
- Transfer configuration files
- Deploy shell scripts

---

## Advantages

- Simple
- Secure
- Idempotent
- Supports permissions

---

## Limitations

- Not ideal for very large files
- Source file must exist on the Control Node

---

## Common Interview Questions (Concept Only)

- Which module copies files?
- Can directories be copied?
- How do you set file permissions during copy?

---

## Common Mistakes

- Incorrect destination path
- Missing source file
- Incorrect permissions

---

## Troubleshooting

```bash
ansible all -m copy -a "src=test.txt dest=/tmp/test.txt"
```

---

## Summary

The `copy` module securely transfers files from the Control Node to Managed Nodes and is widely used for configuration and application deployment.

---

# Manage Packages

## Overview

The `package` module installs, updates, or removes software packages on managed hosts.

It provides a unified interface for different package managers such as:

- apt
- yum
- dnf
- zypper

---

## Why It Is Used

- Install software
- Remove packages
- Upgrade applications
- Standardize server configuration

---

## Architecture / Working

```mermaid
flowchart LR
    ControlNode --> PackageModule
    PackageModule --> PackageManager
    PackageManager --> ManagedNode
```

---

## Key Components

| Component | Purpose |
|-----------|---------|
| package module | Generic package manager |
| apt | Debian package manager |
| yum/dnf | RHEL package manager |

---

## Types (if applicable)

- Install
- Upgrade
- Remove

---

## Lifecycle / Workflow

```mermaid
flowchart LR
    Package --> InstallOrRemove --> Verify
```

---

## Configuration / Syntax (if applicable)

Install Package

```bash
ansible all -m package -a "name=git state=present" -b
```

Remove Package

```bash
ansible all -m package -a "name=httpd state=absent" -b
```

---

## Important Commands (if applicable)

```bash
ansible all -m package -a "name=vim state=present" -b
```

---

## Important Files (if applicable)

Package repositories

---

## Real-World Use Cases

- Install Git
- Install Apache
- Install Docker
- Patch servers

---

## Advantages

- Cross-platform
- Idempotent
- Easy automation

---

## Limitations

- Requires package repositories
- Internet or local repository access may be needed

---

## Common Interview Questions (Concept Only)

- Which module manages packages?
- Difference between package and apt modules?
- What does `state=present` mean?

---

## Common Mistakes

- Forgetting privilege escalation
- Wrong package name
- Missing repositories

---

## Troubleshooting

```bash
ansible all -m package -a "name=git state=present" -b
```

---

## Summary

The `package` module provides a consistent way to install, update, and remove software across different Linux distributions.

---

# Manage Services

## Overview

The `service` module starts, stops, restarts, reloads, and enables system services.

It is one of the most commonly used modules for server administration.

---

## Why It Is Used

- Start services
- Stop services
- Restart services
- Enable services at boot
- Check service status

---

## Architecture / Working

```mermaid
flowchart LR
    ControlNode --> ServiceModule
    ServiceModule --> SystemService
```

---

## Key Components

| Component | Purpose |
|-----------|---------|
| service module | Service management |
| systemd | Linux service manager |

---

## Types (if applicable)

Service States

- started
- stopped
- restarted
- reloaded

---

## Lifecycle / Workflow

```mermaid
flowchart LR
    Connect --> ManageService --> Verify
```

---

## Configuration / Syntax (if applicable)

Start Service

```bash
ansible web -m service -a "name=nginx state=started" -b
```

Restart Service

```bash
ansible web -m service -a "name=nginx state=restarted" -b
```

Enable Service

```bash
ansible web -m service -a "name=nginx enabled=yes" -b
```

---

## Important Commands (if applicable)

```bash
ansible all -m service -a "name=sshd state=restarted" -b
```

---

## Important Files (if applicable)

Systemd service files

---

## Real-World Use Cases

- Restart Apache
- Start Docker
- Enable SSH
- Restart application services

---

## Advantages

- Simple service management
- Cross-platform abstraction
- Idempotent operations

---

## Limitations

- Requires administrative privileges
- Service name differs across Linux distributions

---

## Common Interview Questions (Concept Only)

- Which module manages services?
- Difference between started and restarted?
- How do you enable a service at boot?

---

## Common Mistakes

- Forgetting `-b` (become)
- Using incorrect service names
- Restarting services unnecessarily

---

## Troubleshooting

| Problem | Cause | Solution |
|----------|--------|----------|
| Service not found | Incorrect service name | Verify using `systemctl list-units` |
| Permission denied | Missing sudo privileges | Run with `-b` |
| Service failed to start | Configuration issue | Check service logs |

Useful Commands

```bash
ansible all -m service -a "name=nginx state=started" -b

systemctl status nginx
```

---

## Summary

The `service` module is used to manage system services across Linux servers. It supports starting, stopping, restarting, reloading, and enabling services, making it an essential module for infrastructure automation and day-to-day administration.
