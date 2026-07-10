# Python Common Modules & Regular Expressions Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

Why are Python Standard Library modules important in DevOps automation?

**Answer**

Python Standard Library modules provide built-in functionality for interacting with the operating system, files, processes, dates, logging, JSON, CSV files, and command-line arguments without installing external packages.

**Explanation**

Instead of writing complex code from scratch, DevOps engineers use standard modules to automate common infrastructure and system administration tasks.

**Where it is used in Production**

- Server automation
- Log analysis
- Backup scripts
- CI/CD pipelines
- Cloud automation

**Common Mistake**

Using third-party libraries when the required functionality already exists in the Python Standard Library.

---

### Question 2

**Question**

What is the purpose of the `os` module?

**Answer**

The `os` module provides functions for interacting with the operating system.

Common uses:

- Environment variables
- Directory operations
- File operations
- Executing OS-related tasks

Example:

```python
import os

print(os.getcwd())
```

**Explanation**

It provides a portable way to work with files, directories, and environment variables across operating systems.

**Where it is used in Production**

- Reading environment variables
- Creating directories
- Managing file paths
- Automation scripts

---

### Question 3

**Question**

What is the difference between the `os` module and the `pathlib` module?

**Answer**

- `os` provides procedural functions for interacting with the operating system.
- `pathlib` provides an object-oriented approach for handling file system paths.

**Explanation**

`pathlib` makes path manipulation cleaner and more readable.

**Where it is used in Production**

Managing configuration files, deployment directories, backup locations, and log paths.

---

### Question 4

**Question**

Why is the `subprocess` module commonly used in DevOps?

**Answer**

The `subprocess` module allows Python scripts to execute external system commands.

Example:

```python
import subprocess

subprocess.run(["kubectl", "get", "pods"])
```

**Explanation**

Many DevOps tools such as Docker, Kubernetes, Git, and Azure CLI are executed from Python using `subprocess`.

**Where it is used in Production**

- Running shell commands
- Executing Kubernetes commands
- Running Docker commands
- Triggering deployment scripts

**Common Mistake**

Using `os.system()` instead of the more secure and flexible `subprocess` module.

---

### Question 5

**Question**

What is the purpose of the `json` module?

**Answer**

The `json` module converts JSON data to Python objects and vice versa.

Example:

```python
import json
```

**Explanation**

Most cloud APIs communicate using JSON, making this module essential for DevOps automation.

**Where it is used in Production**

- REST APIs
- Cloud SDKs
- Configuration files
- Infrastructure automation

---

### Question 6

**Question**

When would you use the `csv` module?

**Answer**

The `csv` module reads and writes CSV files.

Example:

```python
import csv
```

**Explanation**

Many inventories, reports, and exported cloud resources are stored as CSV files.

**Where it is used in Production**

- Inventory management
- Report generation
- Asset tracking
- Automation outputs

---

### Question 7

**Question**

Why should DevOps engineers use the `logging` module instead of `print()`?

**Answer**

The `logging` module provides structured logging with different severity levels such as INFO, WARNING, ERROR, and DEBUG.

**Explanation**

Unlike `print()`, logging supports timestamps, log files, filtering, and centralized monitoring.

**Where it is used in Production**

- Deployment logs
- Monitoring scripts
- Troubleshooting
- Automation frameworks

**Common Mistake**

Using `print()` statements for production logging.

---

### Question 8

**Question**

What is the purpose of the `argparse` module?

**Answer**

`argparse` allows Python scripts to accept command-line arguments.

Example:

```bash
python deploy.py --env prod
```

**Explanation**

It makes automation scripts flexible by allowing users to provide input without modifying the code.

**Where it is used in Production**

Deployment scripts, backup scripts, monitoring utilities, and cloud automation.

---

### Question 9

**Question**

Why is the `datetime` module frequently used in DevOps?

**Answer**

The `datetime` module works with dates and times.

Example:

```python
from datetime import datetime
```

**Explanation**

Automation tasks often require timestamps, scheduling, logging, and report generation.

**Where it is used in Production**

- Log timestamps
- Backup filenames
- Scheduled jobs
- Audit reports

---

### Question 10

**Question**

What is a regular expression (Regex)?

**Answer**

A regular expression is a sequence of characters used to search, validate, or manipulate text using patterns.

Example:

```python
import re
```

**Explanation**

Regex simplifies searching and extracting information from logs, configuration files, and text data.

**Where it is used in Production**

- Log analysis
- Input validation
- Parsing configuration files
- Monitoring

---

### Question 11

**Question**

What is the difference between `search()`, `match()`, and `findall()` in the `re` module?

**Answer**

- `match()` checks only the beginning of the string.
- `search()` searches the entire string.
- `findall()` returns all matching occurrences.

**Explanation**

Each function serves a different purpose depending on how text needs to be searched.

**Where it is used in Production**

Log parsing, configuration validation, and pattern extraction.

---

### Question 12

**Question**

How do you replace text using regular expressions?

**Answer**

Use `re.sub()`.

Example:

```python
import re

text = re.sub("ERROR", "WARNING", log)
```

**Explanation**

`re.sub()` replaces matching text using regular expression patterns.

**Where it is used in Production**

Sanitizing logs, modifying configuration files, masking sensitive information, and text processing.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

Your deployment script must execute `kubectl apply -f deployment.yaml`. Which Python module would you use?

**Answer**

Use the `subprocess` module.

**Explanation**

`subprocess` safely executes external commands and captures their output.

---

### Scenario 2

**Question**

Your automation receives a JSON response from the Azure REST API. Which module should you use to process it?

**Answer**

Use the `json` module.

**Explanation**

The module converts JSON data into Python dictionaries for easy access.

---

### Scenario 3

**Question**

Your script should create a timestamped backup file such as:

```text
backup_20260710.zip
```

Which module would you use?

**Answer**

Use the `datetime` module.

**Explanation**

It generates formatted date and time values for filenames and reports.

---

### Scenario 4

**Question**

A deployment script should accept the target environment from the command line instead of modifying the source code. Which module is most appropriate?

**Answer**

Use `argparse`.

**Explanation**

Command-line arguments make scripts reusable and easier to integrate into CI/CD pipelines.

---

### Scenario 5

**Question**

Your monitoring script currently uses dozens of `print()` statements. How would you improve it?

**Answer**

Replace `print()` with the `logging` module.

**Explanation**

Logging supports timestamps, severity levels, log files, and centralized monitoring.

---

### Scenario 6

**Question**

A log file contains thousands of entries, and you need to extract all IP addresses. Which Python feature would you use?

**Answer**

Use regular expressions with `re.findall()`.

**Explanation**

`findall()` returns every matching pattern efficiently.

---

### Scenario 7

**Question**

You need to verify whether a server hostname starts with `"web"`. Which regex function is most appropriate?

**Answer**

Use `re.match()`.

**Explanation**

`match()` checks only the beginning of the string, making it suitable for prefix validation.

---

### Scenario 8

**Question**

A deployment script should replace every occurrence of `"localhost"` with `"prod-server"` inside a configuration file. Which regex function would you use?

**Answer**

Use `re.sub()`.

**Explanation**

`sub()` replaces matching text using regular expression patterns.

---

### Scenario 9

**Question**

Your automation must copy log files to a backup directory while preserving metadata. Which module would you use?

**Answer**

Use the `shutil` module.

**Explanation**

`shutil` provides high-level file operations such as copying, moving, and archiving files.

---

### Scenario 10

**Question**

Your script processes configuration files located in different operating systems. How would you avoid hardcoding file paths?

**Answer**

Use the `pathlib` module.

**Explanation**

`pathlib` provides an operating system-independent way to work with file paths, improving portability and readability.
