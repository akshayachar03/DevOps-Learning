# Python Working with APIs & Automation with Python Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is an API, and why is it important for DevOps engineers?

**Answer**

An API (Application Programming Interface) allows applications to communicate with each other. DevOps engineers use APIs to automate cloud services, CI/CD pipelines, monitoring tools, container platforms, and infrastructure management.

**Explanation**

Instead of manually performing tasks through web interfaces, Python scripts interact with APIs to create resources, deploy applications, retrieve monitoring data, and manage cloud infrastructure.

**Where it is used in Production**

- Azure REST API
- AWS APIs
- Kubernetes API
- GitHub API
- Jenkins API
- Prometheus API

**Common Mistake**

Confusing REST APIs with web pages. APIs exchange structured data (typically JSON), not HTML.

---

### Question 2

**Question**

Why is the `requests` library commonly used in Python?

**Answer**

The `requests` library simplifies sending HTTP requests such as GET, POST, PUT, and DELETE.

Example:

```python
import requests

response = requests.get("https://api.github.com")
```

**Explanation**

It provides a simple interface for communicating with REST APIs without manually handling sockets or HTTP protocols.

**Where it is used in Production**

- Cloud automation
- CI/CD integrations
- Monitoring systems
- Infrastructure provisioning

**Common Mistake**

Forgetting to install the package using:

```bash
pip install requests
```

---

### Question 3

**Question**

What is the difference between GET and POST requests?

**Answer**

- **GET** retrieves data from a server.
- **POST** sends data to the server to create or process a resource.

**Explanation**

GET is read-only, whereas POST is commonly used to submit data such as deployment requests or API payloads.

**Where it is used in Production**

- GET: Retrieve VM details, pipeline status, metrics
- POST: Trigger builds, create resources, deploy applications

---

### Question 4

**Question**

How do you send a GET request using the `requests` library?

**Answer**

Example:

```python
import requests

response = requests.get("https://api.example.com/users")
```

**Explanation**

The server processes the request and returns a response containing status code, headers, and data.

**Where it is used in Production**

Reading:

- Cloud resources
- Monitoring metrics
- Kubernetes objects
- Repository information

---

### Question 5

**Question**

How do you send a POST request with JSON data?

**Answer**

Example:

```python
import requests

data = {"name": "server1"}

response = requests.post(url, json=data)
```

**Explanation**

The `json=` parameter automatically converts the Python dictionary into JSON before sending it.

**Where it is used in Production**

- Creating cloud resources
- Triggering deployments
- Creating users
- Updating configurations

---

### Question 6

**Question**

How do you handle JSON responses from an API?

**Answer**

Use:

```python
response.json()
```

Example:

```python
data = response.json()
print(data["name"])
```

**Explanation**

Most REST APIs return JSON. The `json()` method converts the response into a Python dictionary or list.

**Where it is used in Production**

- Azure APIs
- GitHub APIs
- Kubernetes APIs
- Monitoring APIs

**Common Mistake**

Trying to parse JSON manually instead of using `response.json()`.

---

### Question 7

**Question**

How do you check whether an API request was successful?

**Answer**

Check the HTTP status code.

Example:

```python
if response.status_code == 200:
    print("Success")
```

**Explanation**

HTTP status codes indicate whether the request succeeded or failed.

Common codes:

- 200 OK
- 201 Created
- 400 Bad Request
- 401 Unauthorized
- 404 Not Found
- 500 Internal Server Error

**Where it is used in Production**

Every API integration script.

---

### Question 8

**Question**

What is file automation in Python?

**Answer**

File automation involves automatically creating, reading, modifying, deleting, or organizing files.

**Explanation**

Python can process thousands of files without manual intervention.

**Where it is used in Production**

- Backup automation
- Log management
- Configuration generation
- Report generation

---

### Question 9

**Question**

How can Python automate directory operations?

**Answer**

Using modules like:

- `os`
- `pathlib`
- `shutil`

Example:

```python
import os

os.mkdir("backup")
```

**Explanation**

These modules help create, rename, copy, move, and delete directories.

**Where it is used in Production**

- Backup automation
- Deployment automation
- Log archival

---

### Question 10

**Question**

How do you execute Linux commands from Python?

**Answer**

Using the `subprocess` module.

Example:

```python
import subprocess

subprocess.run(["ls", "-l"])
```

**Explanation**

Python executes external programs and captures their output.

**Where it is used in Production**

- Docker automation
- Kubernetes automation
- Git commands
- Shell scripting replacement

**Common Mistake**

Using `os.system()` instead of `subprocess`, which provides better security and control.

---

### Question 11

**Question**

What is log parsing, and why is it important in DevOps?

**Answer**

Log parsing is the process of extracting useful information from log files.

**Explanation**

Python reads logs, filters errors, generates reports, and sends alerts.

**Where it is used in Production**

- Application monitoring
- Incident analysis
- Security auditing
- Troubleshooting

**Common Mistake**

Reading entire large log files into memory instead of processing them line by line.

---

### Question 12

**Question**

How does Python help automate repetitive DevOps tasks?

**Answer**

Python automates repetitive tasks such as:

- File management
- API calls
- Deployments
- Monitoring
- Backup
- Report generation
- Command execution

**Explanation**

Automation reduces manual effort, improves consistency, and minimizes human error.

**Where it is used in Production**

Nearly every DevOps workflow, including CI/CD pipelines, cloud provisioning, infrastructure management, and monitoring.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

Your team needs to retrieve the status of all Azure Virtual Machines every hour. How would you automate this?

**Answer**

Use the `requests` library to send GET requests to the Azure REST API and process the JSON response.

**Explanation**

Automating API calls eliminates manual checks and enables scheduled monitoring.

---

### Scenario 2

**Question**

A Jenkins pipeline must trigger another deployment service after a successful build. How would Python accomplish this?

**Answer**

Send a POST request using the `requests` library with the required JSON payload.

**Explanation**

Many CI/CD platforms expose REST APIs for triggering jobs and deployments.

---

### Scenario 3

**Question**

Your automation script receives a JSON response containing hundreds of servers. How would you extract only the server names?

**Answer**

Convert the response using `response.json()` and iterate through the returned dictionary or list.

**Explanation**

JSON parsing enables easy access to structured API data.

---

### Scenario 4

**Question**

A deployment script must create backup directories automatically before copying application files. Which Python modules would you use?

**Answer**

Use `os`, `pathlib`, or `shutil`.

**Explanation**

These modules simplify directory creation and file management in deployment automation.

---

### Scenario 5

**Question**

Your automation script needs to execute `kubectl get pods` and capture the output. Which module would you use?

**Answer**

Use the `subprocess` module.

**Explanation**

`subprocess.run()` executes external commands and returns their output for further processing.

---

### Scenario 6

**Question**

A log file grows to several gigabytes. What is the most efficient way to parse it?

**Answer**

Read the file line by line instead of loading the entire file into memory.

**Explanation**

Streaming large files reduces memory usage and improves performance.

---

### Scenario 7

**Question**

Your API script returns HTTP status code 401. What does it indicate, and how would you troubleshoot it?

**Answer**

A 401 status indicates an authentication failure. Verify API tokens, credentials, headers, and permissions.

**Explanation**

Most REST APIs require valid authentication before allowing access.

---

### Scenario 8

**Question**

Your backup automation should archive configuration files every night. Which Python modules would you choose?

**Answer**

Use `shutil` for copying or archiving files along with `datetime` for timestamped backup names.

**Explanation**

These modules provide reliable file operations and organized backup management.

---

### Scenario 9

**Question**

A monitoring script should retrieve metrics from a Prometheus API and save them to a JSON file. How would you implement this?

**Answer**

Use `requests.get()` to retrieve the metrics, parse the response using `response.json()`, and write the data to a file using the `json` module.

**Explanation**

This approach is commonly used for exporting monitoring data and generating reports.

---

### Scenario 10

**Question**

Your deployment automation executes several Linux commands. One command fails, but the remaining tasks continue running. How would you improve the script?

**Answer**

Capture command results using `subprocess`, check return codes, and implement proper exception handling to stop or handle failures appropriately.

**Explanation**

Validating command execution prevents incomplete deployments and improves the reliability of automation scripts.
