# Python YAML & JSON | Working with Linux Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What are JSON and YAML, and why are they widely used in DevOps?

**Answer**

JSON (JavaScript Object Notation) and YAML (YAML Ain't Markup Language) are structured data formats used to store and exchange configuration data.

- **JSON** is lightweight, machine-friendly, and commonly used in APIs.
- **YAML** is human-readable and commonly used for configuration files such as Kubernetes manifests, Ansible playbooks, Docker Compose files, and GitHub Actions workflows.

**Explanation**

Python can easily read and write both formats, making automation scripts capable of interacting with cloud services, CI/CD pipelines, and infrastructure configuration files.

**Where it is used in Production**

- Kubernetes YAML manifests
- Ansible Playbooks
- Docker Compose
- GitHub Actions workflows
- REST API responses

**Common Mistake**

Assuming YAML and JSON are interchangeable in every situation. YAML supports comments and is more readable, while JSON is stricter and primarily used for data exchange.

---

### Question 2

**Question**

How do you read a JSON file in Python?

**Answer**

Use the built-in `json` module.

Example:

```python
import json

with open("config.json") as f:
    data = json.load(f)

print(data)
```

**Explanation**

`json.load()` converts JSON data into Python objects such as dictionaries and lists.

**Where it is used in Production**

- Reading application configuration
- Processing API responses
- Automation scripts

**Common Mistake**

Using `json.loads()` instead of `json.load()` for file input.

---

### Question 3

**Question**

How do you write data to a JSON file?

**Answer**

Use `json.dump()`.

Example:

```python
import json

data = {"server": "web01"}

with open("config.json", "w") as f:
    json.dump(data, f, indent=4)
```

**Explanation**

Python converts dictionaries into JSON format before writing them to the file.

**Where it is used in Production**

- Configuration generation
- Report generation
- Automation outputs

---

### Question 4

**Question**

How do you read a YAML file in Python?

**Answer**

Using the `PyYAML` library.

Example:

```python
import yaml

with open("config.yaml") as f:
    data = yaml.safe_load(f)
```

**Explanation**

`safe_load()` safely converts YAML into Python objects.

**Where it is used in Production**

- Kubernetes manifests
- Docker Compose
- GitHub Actions
- Ansible inventories

**Common Mistake**

Using `yaml.load()` instead of `yaml.safe_load()`, which can introduce security risks.

---

### Question 5

**Question**

Why is YAML preferred for infrastructure configuration?

**Answer**

YAML is easier for humans to read and write because it uses indentation instead of braces and brackets.

**Explanation**

Infrastructure-as-Code tools prefer YAML because configuration files become easier to maintain.

**Where it is used in Production**

- Kubernetes
- Ansible
- GitHub Actions
- Azure Pipelines

---

### Question 6

**Question**

How does Python parse configuration files?

**Answer**

Python reads configuration files using modules such as:

- `json`
- `yaml`
- `configparser`

The parsed data becomes Python dictionaries or objects for use within automation scripts.

**Explanation**

Configuration files allow scripts to run in different environments without modifying the source code.

**Where it is used in Production**

- Dev
- Test
- Staging
- Production deployments

---

### Question 7

**Question**

How do you execute shell commands from Python?

**Answer**

Using the `subprocess` module.

Example:

```python
import subprocess

subprocess.run(["ls", "-l"])
```

**Explanation**

`subprocess` executes external Linux commands while allowing Python to capture output and exit status.

**Where it is used in Production**

- Docker automation
- Git automation
- Kubernetes management
- Server administration

**Common Mistake**

Using `os.system()` instead of `subprocess`, which provides less control and weaker error handling.

---

### Question 8

**Question**

How can Python access Linux environment variables?

**Answer**

Using the `os` module.

Example:

```python
import os

print(os.getenv("HOME"))
```

**Explanation**

Environment variables store configuration values such as API keys, database URLs, and credentials.

**Where it is used in Production**

- CI/CD pipelines
- Cloud deployments
- Docker containers
- Kubernetes Secrets

**Common Mistake**

Hardcoding sensitive values instead of using environment variables.

---

### Question 9

**Question**

How do you manage file permissions in Python?

**Answer**

Using `os.chmod()`.

Example:

```python
import os

os.chmod("script.sh", 0o755)
```

**Explanation**

Python changes Linux file permissions programmatically.

**Where it is used in Production**

- Deployment automation
- Backup scripts
- Executable scripts

---

### Question 10

**Question**

How can Python manage Linux processes?

**Answer**

Using modules such as:

- `subprocess`
- `os`
- `signal`

Example:

```python
import subprocess

process = subprocess.Popen(["sleep", "30"])
process.terminate()
```

**Explanation**

Python can start, monitor, stop, and restart Linux processes.

**Where it is used in Production**

- Service management
- Monitoring
- Automation
- CI/CD

---

### Question 11

**Question**

Why are environment variables preferred over hardcoded values?

**Answer**

Environment variables improve security and flexibility.

**Explanation**

Scripts remain portable across multiple environments without modifying source code.

**Where it is used in Production**

- Cloud credentials
- Database passwords
- API tokens
- Deployment environments

**Common Mistake**

Committing secrets directly into Git repositories.

---

### Question 12

**Question**

Why is the `subprocess` module preferred over `os.system()`?

**Answer**

`subprocess` provides:

- Better security
- Better error handling
- Output capture
- Exit status checking
- Process control

**Explanation**

It is the recommended way to execute external programs in modern Python.

**Where it is used in Production**

Nearly every DevOps automation script that interacts with Linux utilities.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

Your deployment configuration is stored in a YAML file. How would your Python script use it?

**Answer**

Use `yaml.safe_load()` to parse the YAML file into a Python dictionary and access configuration values.

**Explanation**

Separating configuration from code improves maintainability and allows different configurations for different environments.

---

### Scenario 2

**Question**

A cloud API returns a JSON response containing hundreds of virtual machines. How would you process it?

**Answer**

Use `response.json()` or `json.load()` to convert the JSON into Python dictionaries and iterate over the required fields.

**Explanation**

JSON parsing enables automation scripts to filter and process API data efficiently.

---

### Scenario 3

**Question**

Your automation script must execute `kubectl get pods` and capture the output. Which module would you use?

**Answer**

Use the `subprocess` module.

**Explanation**

`subprocess.run()` executes Linux commands and captures stdout and stderr for further processing.

---

### Scenario 4

**Question**

Your deployment script requires an API key that must not be stored in the source code. How would you handle it?

**Answer**

Store the API key in an environment variable and retrieve it using `os.getenv()`.

**Explanation**

This approach improves security and follows DevOps best practices.

---

### Scenario 5

**Question**

A shell script generated by your automation cannot be executed because of permission issues. How would you resolve it?

**Answer**

Use `os.chmod()` to assign executable permissions, such as `755`.

**Explanation**

Linux requires execute permission before a script can run.

---

### Scenario 6

**Question**

Your Python script must automatically generate a JSON report after deployment. Which module would you use?

**Answer**

Use the built-in `json` module with `json.dump()`.

**Explanation**

JSON reports can be consumed by monitoring tools, dashboards, or APIs.

---

### Scenario 7

**Question**

Your automation script starts a backup process but needs to terminate it after a timeout. How would you implement this?

**Answer**

Start the process using `subprocess.Popen()` and terminate it using `process.terminate()` or `process.kill()` if necessary.

**Explanation**

Process management ensures automation does not leave orphaned or long-running processes.

---

### Scenario 8

**Question**

Your application has separate configuration files for development, testing, and production. How would your Python script support all environments?

**Answer**

Read the appropriate YAML or JSON configuration file based on an environment variable.

**Explanation**

Environment-specific configuration avoids modifying source code between deployments.

---

### Scenario 9

**Question**

A Python automation script fails because a configuration file contains invalid YAML syntax. How would you troubleshoot it?

**Answer**

Validate the YAML file for proper indentation and syntax, then reload it using `yaml.safe_load()` while handling parsing exceptions.

**Explanation**

Incorrect indentation is one of the most common causes of YAML parsing failures.

---

### Scenario 10

**Question**

Your deployment automation executes several Linux commands, and one command fails unexpectedly. How would you identify the issue?

**Answer**

Use `subprocess.run(..., capture_output=True, text=True)` to capture stdout, stderr, and the return code, then log the error for troubleshooting.

**Explanation**

Capturing command output and exit codes makes debugging significantly easier and improves the reliability of automation scripts.
