# Security & User Management

## Overview

**Security & User Management** in Jenkins is the process of controlling **who can access Jenkins, what they can do, and how sensitive information (credentials) is protected**.

A secure Jenkins environment ensures that:

- Only authorized users can log in.
- Users have only the permissions they require.
- Sensitive credentials are stored securely.
- Pipelines do not expose secrets.
- Unauthorized modifications are prevented.

> **Interview Tip**
>
> Jenkins security is primarily based on three concepts:
>
> - **Authentication** → Who are you?
> - **Authorization** → What are you allowed to do?
> - **Credentials Management** → How are secrets securely stored and used?

---

## Why It Is Used

Security & User Management helps to:

- Protect CI/CD pipelines
- Prevent unauthorized access
- Secure production deployments
- Protect passwords, SSH keys, and API tokens
- Enforce least privilege access
- Improve compliance and auditing

---

## Architecture / Working

```mermaid
flowchart LR

User --> Authentication

Authentication --> Authorization

Authorization --> Jenkins Dashboard

Jenkins Dashboard --> Credentials Store

Credentials Store --> Pipeline

Pipeline --> External Services
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| User Management | Manage Jenkins users |
| Authentication | Verify user identity |
| Authorization | Control permissions |
| Credentials Store | Secure secret storage |
| Roles | Group permissions |
| Matrix Security | Fine-grained access control |

---

## Types (if applicable)

Authentication Methods

- Jenkins Internal User Database
- LDAP
- Active Directory
- GitHub OAuth
- Google OAuth
- SAML

Authorization Strategies

- Matrix-based Security
- Project-based Matrix Authorization
- Role-Based Authorization Strategy (RBAC)
- Logged-in Users Can Do Anything (Not recommended for production)

---

## Lifecycle / Workflow

```mermaid
flowchart LR

User

User --> Login

Login --> Authentication

Authentication --> Authorization

Authorization --> Dashboard

Dashboard --> Pipeline

Pipeline --> Credentials
```

---

## Configuration / Syntax (if applicable)

Security Configuration

```
Manage Jenkins

    → Security

        → Authentication

        → Authorization
```

Using Credentials in Pipeline

```groovy
withCredentials([
    usernamePassword(
        credentialsId: 'github-creds',
        usernameVariable: 'USERNAME',
        passwordVariable: 'PASSWORD'
    )
]) {

    sh 'git clone https://$USERNAME:$PASSWORD@github.com/company/repo.git'

}
```

Using Secret Text

```groovy
withCredentials([
    string(
        credentialsId: 'api-token',
        variable: 'TOKEN'
    )
]) {

    sh 'curl -H "Authorization: Bearer $TOKEN"'

}
```

---

## Important Commands (if applicable)

There are no dedicated Jenkins CLI commands commonly used for user management in interviews.

Useful Linux commands while troubleshooting:

```bash
whoami
id
groups
chmod
chown
```

---

## Important Files (if applicable)

| File | Purpose |
|------|----------|
| `JENKINS_HOME/config.xml` | Global Jenkins configuration |
| `JENKINS_HOME/users/` | User information |
| `credentials.xml` | Stored credentials (encrypted) |
| `Jenkinsfile` | Pipeline definition |

---

## Real-World Use Cases

- Multiple DevOps engineers accessing Jenkins
- Separate permissions for Developers and Administrators
- Secure deployment to production
- GitHub authentication
- SSH deployment
- Kubernetes authentication
- Docker Registry authentication
- Nexus authentication

---

## Advantages

- Secure pipeline execution
- Role-based access control
- Encrypted credential storage
- Prevents unauthorized changes
- Supports enterprise authentication systems

---

## Limitations

- Requires proper security planning
- Misconfigured permissions may block users
- Plugin compatibility issues
- Credentials require periodic rotation

---

## Common Interview Questions (Concept Only)

- What are Authentication and Authorization?
- How does Jenkins store credentials?
- Why should passwords never be hardcoded in Jenkinsfiles?
- What is Matrix Authorization?
- What is Role-Based Access Control (RBAC)?
- Which authentication methods does Jenkins support?
- How do pipelines securely access credentials?
- What is the difference between Username/Password and Secret Text credentials?

---

## Common Mistakes

- Hardcoding passwords inside Jenkinsfiles
- Giving all users Administrator permissions
- Sharing one account among multiple users
- Storing credentials inside Git repositories
- Printing secrets in Console Output
- Using weak passwords
- Forgetting to rotate credentials
- Not enabling Matrix or Role-Based Authorization

---

## Troubleshooting

| Problem | Solution |
|----------|----------|
| Cannot log in | Verify authentication configuration |
| Permission denied | Verify assigned roles and permissions |
| Credentials not found | Check Credentials ID |
| Secret exposed in logs | Use `withCredentials()` correctly |
| Git authentication failed | Verify Username/PAT or SSH Key |
| Pipeline cannot access credentials | Verify credential scope and permissions |

---

## Summary

Security & User Management ensures Jenkins remains secure by verifying user identity, controlling permissions, and securely managing sensitive credentials. Proper authentication, authorization, and credential management are essential for production-grade CI/CD pipelines.

---

# User Management

## Overview

**User Management** refers to creating, modifying, deleting, and maintaining Jenkins user accounts.

Each user can have different permissions based on organizational requirements.

> **Interview Tip**
>
> Production Jenkins environments should never use a single shared administrator account.

---

## Why It Is Used

User Management enables:

- Individual user accounts
- Activity auditing
- Permission management
- Secure access
- Accountability

---

## Architecture / Working

```mermaid
flowchart LR

Administrator --> CreateUser

CreateUser --> Jenkins

Jenkins --> UserLogin
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| User | Jenkins account |
| Admin | User management |
| Groups | Organize users |

---

## Types (if applicable)

Common Users

- Administrator
- Developer
- QA Engineer
- DevOps Engineer
- Read-only User

---

## Lifecycle / Workflow

```mermaid
flowchart LR

CreateUser

CreateUser --> AssignRole

AssignRole --> Login

Login --> PipelineAccess
```

---

## Configuration / Syntax (if applicable)

```
Manage Jenkins

    → Manage Users

        → Create User
```

---

## Important Commands (if applicable)

Not Applicable

---

## Important Files (if applicable)

```
JENKINS_HOME/users/
```

---

## Real-World Use Cases

- Adding new developers
- Removing former employees
- Managing project access
- Team-based permissions

---

## Advantages

- Individual accountability
- Better security
- Easier auditing

---

## Limitations

- Requires ongoing administration
- Manual user management in smaller environments

---

## Common Interview Questions (Concept Only)

- How are users managed in Jenkins?
- Why should each engineer have a separate account?

---

## Common Mistakes

- Shared administrator account
- Inactive users not removed

---

## Troubleshooting

| Problem | Solution |
|----------|----------|
| User cannot log in | Verify account status |
| Missing permissions | Check assigned roles |

---

## Summary

User Management enables secure, accountable access to Jenkins by assigning individual user accounts and permissions.

---

# Roles

## Overview

A **Role** is a collection of permissions assigned to one or more users.

Rather than assigning permissions individually, administrators assign predefined roles.

Common roles include:

- Administrator
- Developer
- Release Manager
- Read-only User

> **Interview Tip**
>
> Role-Based Access Control (RBAC) follows the **Principle of Least Privilege**, granting users only the permissions they need.

---

## Why It Is Used

Roles help:

- Simplify permission management
- Improve security
- Reduce administrative effort
- Standardize user access

---

## Architecture / Working

```mermaid
flowchart LR

Administrator --> CreateRole

CreateRole --> AssignPermissions

AssignPermissions --> User

User --> Jenkins
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| Role | Permission set |
| User | Assigned role |
| Permissions | Allowed actions |

---

## Types (if applicable)

Typical Roles

| Role | Typical Permissions |
|------|----------------------|
| Administrator | Full access |
| Developer | Build and view jobs |
| QA Engineer | Execute and view jobs |
| Release Manager | Deploy releases |
| Viewer | Read-only access |

---

## Lifecycle / Workflow

```mermaid
flowchart LR

Role

Role --> Permissions

Permissions --> User

User --> Jenkins
```

---

## Configuration / Syntax (if applicable)

Commonly implemented using the **Role-Based Authorization Strategy Plugin**.

---

## Important Commands (if applicable)

Not Applicable

---

## Important Files (if applicable)

Role configuration stored in Jenkins configuration.

---

## Real-World Use Cases

- Separate DevOps and Developer permissions
- Production deployment control
- Read-only auditors

---

## Advantages

- Easier permission management
- Better security
- Supports large teams

---

## Limitations

- Requires RBAC plugin
- Additional administrative effort

---

## Common Interview Questions (Concept Only)

- What is RBAC?
- Why use Roles instead of assigning permissions individually?

---

## Common Mistakes

- Giving Administrator role unnecessarily
- Creating too many custom roles

---

## Troubleshooting

| Problem | Solution |
|----------|----------|
| User missing permissions | Verify assigned role |
| Role not working | Verify authorization strategy |

---

## Summary

Roles simplify permission management by grouping related permissions and assigning them to users.

---

# Authentication

## Overview

**Authentication** is the process of verifying a user's identity before granting access to Jenkins.

It answers the question:

> **Who are you?**

Without successful authentication, a user cannot access Jenkins.

---

## Why It Is Used

Authentication helps:

- Prevent unauthorized access
- Verify user identity
- Integrate enterprise identity providers

---

## Architecture / Working

```mermaid
flowchart LR

User --> Login

Login --> Authentication

Authentication --> Dashboard
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| Username | User identity |
| Password | Verification |
| Identity Provider | User authentication |

---

## Types (if applicable)

Supported Authentication

- Jenkins Internal Database
- LDAP
- Active Directory
- GitHub OAuth
- Google OAuth
- SAML

---

## Lifecycle / Workflow

```mermaid
flowchart LR

Login --> Verify

Verify --> Success

Verify --> Failure
```

---

## Configuration / Syntax (if applicable)

```
Manage Jenkins

    → Security

        → Authentication
```

---

## Important Commands (if applicable)

Not Applicable

---

## Important Files (if applicable)

```
config.xml
```

---

## Real-World Use Cases

- Enterprise Single Sign-On
- GitHub Login
- Corporate Active Directory

---

## Advantages

- Improved security
- Centralized authentication
- Easier user management

---

## Limitations

- External provider dependency
- Misconfiguration can prevent login

---

## Common Interview Questions (Concept Only)

- What is Authentication?
- Difference between Authentication and Authorization?
- Which authentication methods does Jenkins support?

---

## Common Mistakes

- Weak passwords
- Shared accounts
- No MFA (where supported)

---

## Troubleshooting

| Problem | Solution |
|----------|----------|
| Login failed | Verify credentials |
| LDAP issue | Check LDAP configuration |
| OAuth failed | Verify client configuration |

---

## Summary

Authentication verifies user identity before allowing access to Jenkins.

---

# Authorization

## Overview

**Authorization** determines what an authenticated user is allowed to do.

It answers the question:

> **What are you allowed to do?**

Authorization is evaluated **after successful authentication**.

---

## Why It Is Used

Authorization helps:

- Restrict sensitive operations
- Protect production jobs
- Implement least privilege
- Separate duties

---

## Architecture / Working

```mermaid
flowchart LR

Authentication --> Authorization

Authorization --> AccessGranted

Authorization --> AccessDenied
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| Permission | Allowed action |
| Role | Permission group |
| User | Assigned permissions |

---

## Types (if applicable)

Authorization Strategies

- Matrix Authorization
- Project Matrix
- Role-Based Authorization

---

## Lifecycle / Workflow

```mermaid
flowchart LR

Login

Login --> Authenticate

Authenticate --> Authorize

Authorize --> Jenkins
```

---

## Configuration / Syntax (if applicable)

```
Manage Jenkins

    → Security

        → Authorization
```

---

## Important Commands (if applicable)

Not Applicable

---

## Important Files (if applicable)

Authorization configuration stored in Jenkins configuration.

---

## Real-World Use Cases

- Restrict production deployments
- Limit plugin installation
- Allow read-only users

---

## Advantages

- Fine-grained security
- Better compliance
- Reduced risk

---

## Limitations

- Complex permission structures
- Requires careful planning

---

## Common Interview Questions (Concept Only)

- What is Authorization?
- What is Matrix Authorization?
- What is RBAC?

---

## Common Mistakes

- Excessive permissions
- Missing least privilege

---

## Troubleshooting

| Problem | Solution |
|----------|----------|
| Access denied | Verify permissions |
| Missing job visibility | Check project permissions |

---

## Summary

Authorization controls user actions within Jenkins after successful authentication.

---

# Credentials Security

## Overview

**Credentials Security** is the practice of securely storing and managing sensitive information used by Jenkins pipelines.

Instead of hardcoding secrets inside Jenkinsfiles or scripts, Jenkins stores them in its **Credentials Store** in encrypted form and injects them into builds only when required.

Common credentials include:

- Username & Password
- SSH Keys
- Secret Text (API Tokens)
- Secret Files
- Certificates

> **Interview Tip**
>
> Never hardcode passwords, tokens, or private keys in a Jenkinsfile. Use the **Credentials Store** and access them with `withCredentials()`.

---

## Why It Is Used

Credentials Security helps to:

- Protect sensitive information
- Avoid exposing secrets in source code
- Centralize credential management
- Secure access to external systems
- Support secret rotation

---

## Architecture / Working

```mermaid
flowchart LR

CredentialsStore --> Jenkins

Jenkins --> Pipeline

Pipeline --> ExternalService
```

---

## Key Components

| Component | Purpose |
|-----------|----------|
| Credentials Store | Secure secret storage |
| Credentials ID | Unique identifier |
| withCredentials() | Secure injection into pipeline |
| External Service | GitHub, Docker, Kubernetes, Nexus, Cloud APIs |

---

## Types (if applicable)

| Credential Type | Usage |
|-----------------|------|
| Username & Password | Git, Nexus |
| SSH Key | Linux Servers, Git SSH |
| Secret Text | API Tokens |
| Secret File | Certificates |
| Certificate | HTTPS Authentication |

---

## Lifecycle / Workflow

```mermaid
flowchart LR

CreateCredential

CreateCredential --> Store

Store --> Pipeline

Pipeline --> TemporaryEnvironment

TemporaryEnvironment --> ExternalService
```

---

## Configuration / Syntax (if applicable)

Secret Text

```groovy
withCredentials([
    string(
        credentialsId: 'github-token',
        variable: 'TOKEN'
    )
]) {

    sh 'curl -H "Authorization: Bearer $TOKEN"'

}
```

SSH Key

```groovy
withCredentials([
    sshUserPrivateKey(
        credentialsId: 'server-key',
        keyFileVariable: 'KEY'
    )
]) {

    sh 'ssh -i $KEY user@server'

}
```

---

## Important Commands (if applicable)

No dedicated commands.

Typical integrations:

```bash
ssh
git
docker login
kubectl
curl
```

---

## Important Files (if applicable)

| File | Purpose |
|------|----------|
| `credentials.xml` | Encrypted credentials database |
| `config.xml` | Jenkins configuration |

---

## Real-World Use Cases

- GitHub authentication
- Docker Hub login
- Nexus upload
- Kubernetes deployment
- Azure CLI authentication
- AWS CLI authentication
- Linux SSH deployment

---

## Advantages

- Encrypted secret storage
- Secure pipeline execution
- Centralized credential management
- Supports multiple credential types
- Prevents secret exposure in source control

---

## Limitations

- Credentials must be managed and rotated regularly
- Misconfigured permissions may expose credentials
- Backup security is essential

---

## Common Interview Questions (Concept Only)

- What is the Jenkins Credentials Store?
- Why should secrets never be hardcoded?
- What is `withCredentials()`?
- Which credential types does Jenkins support?
- How are credentials injected into pipelines?

---

## Common Mistakes

- Printing secrets to the console
- Committing credentials to Git
- Using Administrator credentials for all pipelines
- Reusing the same credentials across environments
- Forgetting to rotate API tokens and SSH keys

---

## Troubleshooting

| Problem | Solution |
|----------|----------|
| Credential not found | Verify Credentials ID |
| Authentication failed | Check username, password, or key |
| Secret visible in logs | Ensure `withCredentials()` is used correctly |
| Pipeline cannot access credentials | Verify credential scope and permissions |

---

## Summary

Credentials Security is a fundamental Jenkins security feature that enables encrypted storage and controlled use of passwords, SSH keys, tokens, and certificates. Proper credential management is essential for secure, production-ready CI/CD pipelines.
