# Linux Networking Commands Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

Why are Linux Networking Commands important for DevOps and Cloud Engineers?

**Answer**

Linux networking commands help administrators configure, monitor, and troubleshoot network connectivity between systems.

Common networking commands include:

- `ip`
- `ping`
- `curl`
- `wget`
- `ssh`
- `scp`
- `ss`
- `netstat`
- `hostname`

These commands help verify:

- Network connectivity
- IP configuration
- Remote access
- Service availability
- Port status
- File transfer
- DNS resolution

**Explanation**

Most production issues involve networking. Understanding these commands is essential for troubleshooting servers, cloud resources, containers, and applications.

**Used in Production**

DevOps engineers use networking commands daily to verify connectivity, deploy applications, and troubleshoot production incidents.

**Common Mistake**

Many candidates memorize commands but cannot explain when or why they should be used.

---

### Question 2

**Question**

What is the `ip` command, and why is it preferred over `ifconfig`?

**Answer**

The `ip` command is the modern Linux networking utility used to configure and display network interfaces, IP addresses, routing tables, and network information.

Display IP addresses:

```bash
ip addr
```

Display routing table:

```bash
ip route
```

Display interfaces:

```bash
ip link
```

**Explanation**

The `ip` command is part of the `iproute2` package and replaces older tools such as `ifconfig`.

**Used in Production**

Administrators use `ip` to verify interface configuration and troubleshoot routing issues.

---

### Question 3

**Question**

What is the purpose of the `ping` command?

**Answer**

`ping` checks network connectivity between two systems using ICMP Echo Requests.

Example:

```bash
ping google.com
```

Limit requests:

```bash
ping -c 4 google.com
```

**Explanation**

`ping` confirms whether a remote host is reachable and measures network latency.

**Used in Production**

Administrators verify basic connectivity between servers, clients, and cloud resources.

**Common Mistake**

Assuming a failed `ping` always means the server is down. Many servers block ICMP traffic using firewalls.

---

### Question 4

**Question**

What is the `curl` command?

**Answer**

`curl` transfers data to or from a server using protocols such as HTTP, HTTPS, FTP, and others.

Example:

```bash
curl https://example.com
```

Display only headers:

```bash
curl -I https://example.com
```

**Explanation**

`curl` is commonly used to test APIs, web servers, and application endpoints.

**Used in Production**

DevOps engineers use `curl` to verify REST APIs, health endpoints, authentication, and web services.

---

### Question 5

**Question**

What is the `wget` command?

**Answer**

`wget` downloads files from the internet or network locations.

Download a file:

```bash
wget https://example.com/file.zip
```

**Explanation**

Unlike `curl`, `wget` is primarily designed for downloading files and supports download resumption.

**Used in Production**

Administrators download installation packages, configuration files, and software updates.

---

### Question 6

**Question**

What is SSH, and why is it important?

**Answer**

SSH (Secure Shell) provides encrypted remote access to Linux systems.

Connect to a remote server:

```bash
ssh user@server-ip
```

Connect using a private key:

```bash
ssh -i key.pem user@server-ip
```

**Explanation**

SSH encrypts communication, making remote administration secure.

**Used in Production**

SSH is the primary method for managing Linux servers, cloud virtual machines, and network devices.

**Common Mistake**

Using password authentication instead of SSH keys for production environments.

---

### Question 7

**Question**

What is the `scp` command?

**Answer**

`scp` securely copies files between systems using SSH.

Copy a file to a remote server:

```bash
scp file.txt user@server:/home/user/
```

Copy a file from a remote server:

```bash
scp user@server:/home/user/file.txt .
```

**Explanation**

`scp` encrypts file transfers using SSH.

**Used in Production**

Administrators transfer configuration files, backups, scripts, and deployment packages.

---

### Question 8

**Question**

What are the `netstat` and `ss` commands?

**Answer**

Both commands display network connections and listening ports.

Modern command:

```bash
ss -tuln
```

Older command:

```bash
netstat -tuln
```

Information displayed:

- Listening ports
- Active connections
- Protocols
- Local and remote addresses

**Explanation**

`ss` is faster and more efficient than `netstat` and is recommended on modern Linux systems.

**Used in Production**

Administrators verify whether applications are listening on the expected ports.

---

### Question 9

**Question**

What is the `hostname` command?

**Answer**

`hostname` displays or sets the system hostname.

Display hostname:

```bash
hostname
```

Display detailed hostname information:

```bash
hostnamectl
```

**Explanation**

The hostname uniquely identifies a system on the network.

**Used in Production**

Administrators verify server identity before performing maintenance or deployments.

---

### Question 10

**Question**

How would you verify whether a web application is accessible from a Linux server?

**Answer**

Use:

```bash
curl -I https://example.com
```

or

```bash
wget --spider https://example.com
```

You can also verify basic network connectivity using:

```bash
ping example.com
```

**Explanation**

These commands help distinguish between network connectivity issues and application availability issues.

**Used in Production**

DevOps engineers routinely validate application health after deployments.

---

### Question 11

**Question**

What are some best practices for troubleshooting Linux networking?

**Answer**

Best practices include:

- Verify the server hostname.
- Check IP configuration with `ip addr`.
- Confirm routing using `ip route`.
- Test connectivity with `ping`.
- Verify application availability with `curl`.
- Check listening ports using `ss`.
- Use SSH key authentication.
- Verify firewalls and security groups when connectivity fails.

**Explanation**

A structured troubleshooting approach reduces resolution time and avoids unnecessary configuration changes.

**Used in Production**

Network troubleshooting is one of the most common operational tasks performed by DevOps engineers.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

You cannot SSH into a Linux server. How would you troubleshoot the issue?

**Answer**

Check:

1. Basic connectivity:

```bash
ping server-ip
```

2. SSH port:

```bash
ss -tuln
```

3. SSH service status.
4. Firewall rules.
5. Security group or network ACL configuration.
6. SSH key or credentials.

**Explanation**

SSH failures may result from network issues, firewall restrictions, authentication problems, or the SSH service not running.

---

### Scenario 2

**Question**

A web application is inaccessible after deployment. How would you verify whether the application is running?

**Answer**

Check:

```bash
curl -I http://localhost
```

Verify listening ports:

```bash
ss -tuln
```

Review application logs if necessary.

**Explanation**

A successful network connection does not guarantee that the application itself is responding.

---

### Scenario 3

**Question**

A new virtual machine has no internet connectivity. What would you investigate?

**Answer**

Check:

- IP address:

```bash
ip addr
```

- Routing:

```bash
ip route
```

- Connectivity:

```bash
ping 8.8.8.8
```

- DNS configuration.
- Firewall and cloud networking settings.

**Explanation**

Connectivity problems may result from incorrect IP configuration, routing, DNS, or cloud network policies.

---

### Scenario 4

**Question**

You need to copy a deployment package securely to a production server. Which command would you use?

**Answer**

Run:

```bash
scp application.tar.gz user@server:/opt/
```

**Explanation**

`scp` securely transfers files over SSH.

---

### Scenario 5

**Question**

An application team reports that the web server is running, but clients cannot connect. What would you verify?

**Answer**

Check:

```bash
ss -tuln
```

Confirm the application is listening on the expected port.

Then verify firewall rules, security groups, and load balancer configuration.

**Explanation**

Applications may be running without listening on the correct network interface or port.

---

### Scenario 6

**Question**

A developer uses `ping` to determine whether a server is down, but the command fails. Does this always indicate that the server is unavailable?

**Answer**

No.

Many production environments block ICMP traffic. Verify the application using:

```bash
curl
```

or test SSH connectivity if appropriate.

**Explanation**

A blocked `ping` does not necessarily indicate a failed server.

---

### Scenario 7

**Question**

You need to download an installation package from the internet onto a Linux server. Which command would you use?

**Answer**

Run:

```bash
wget https://example.com/package.rpm
```

**Explanation**

`wget` is designed for downloading files and supports download resumption.

---

### Scenario 8

**Question**

A server has multiple network interfaces, and you need to verify their IP addresses. Which command would you use?

**Answer**

Run:

```bash
ip addr
```

**Explanation**

The `ip` command displays all configured interfaces and assigned IP addresses.

---

### Scenario 9

**Question**

You suspect an application is listening on the wrong port. How would you verify it?

**Answer**

Run:

```bash
ss -tuln
```

Review the listening ports and confirm they match the application configuration.

**Explanation**

The `ss` command provides real-time information about active sockets and listening services.

---

### Scenario 10

**Question**

A production deployment succeeds, but users still cannot access the application. What troubleshooting steps would you perform?

**Answer**

1. Verify application status.
2. Test the endpoint using:

```bash
curl
```

3. Verify listening ports:

```bash
ss -tuln
```

4. Check firewall rules.
5. Verify DNS configuration.
6. Review load balancer and reverse proxy settings.

**Explanation**

Successful deployment does not guarantee that the application is reachable from the network.

---

### Scenario 11

**Question**

After migrating an application to a new server, users report that the application is unreachable. How would you systematically troubleshoot the issue?

**Answer**

1. Verify the hostname:

```bash
hostname
```

2. Check network interfaces:

```bash
ip addr
```

3. Verify routing:

```bash
ip route
```

4. Test connectivity:

```bash
ping
```

5. Verify application availability:

```bash
curl
```

6. Confirm the application is listening on the expected port:

```bash
ss -tuln
```

7. Review firewall rules, DNS records, load balancer configuration, and security groups.

**Explanation**

Production networking issues often involve multiple layers, including IP configuration, routing, firewalls, DNS, application configuration, and cloud networking. Following a structured troubleshooting process helps identify the root cause efficiently while minimizing downtime.
