# Linux Disk & File System Management Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is Disk & File System Management in Linux, and why is it important?

**Answer**

Disk & File System Management involves monitoring, organizing, and managing storage devices and file systems in Linux.

Common administrative tasks include:

- Checking disk usage
- Monitoring available space
- Viewing mounted file systems
- Managing storage devices
- Mounting and unmounting file systems
- Troubleshooting storage issues

Common commands:

- `df`
- `du`
- `lsblk`
- `mount`
- `umount`

**Explanation**

Proper disk management prevents storage-related failures, application downtime, and performance issues.

**Used in Production**

DevOps engineers routinely monitor disk usage to prevent application outages caused by full disks.

**Common Mistake**

Many candidates confuse disk usage (`df`) with directory usage (`du`).

---

### Question 2

**Question**

What is the `df` command?

**Answer**

`df` (Disk Free) displays disk space usage for mounted file systems.

Example:

```bash
df -h
```

Sample output:

```text
Filesystem      Size  Used Avail Use%
/dev/sda1        50G   20G   28G   42%
```

Useful option:

- `-h` → Human-readable format

**Explanation**

`df` reports the total, used, and available space on each mounted file system.

**Used in Production**

Administrators use `df` to monitor storage capacity and identify file systems approaching full utilization.

---

### Question 3

**Question**

What is the `du` command?

**Answer**

`du` (Disk Usage) displays the amount of space used by files and directories.

Examples:

Check directory size:

```bash
du -sh /var/log
```

Display subdirectory sizes:

```bash
du -h /home
```

Useful options:

- `-s` → Summary
- `-h` → Human-readable

**Explanation**

Unlike `df`, `du` identifies which directories consume disk space.

**Used in Production**

Administrators use `du` to locate large directories when storage is running low.

---

### Question 4

**Question**

What is the difference between `df` and `du`?

**Answer**

| `df` | `du` |
|------|------|
| Shows file system usage | Shows directory/file usage |
| Reports available disk space | Reports space used by files |
| Useful for storage monitoring | Useful for identifying large directories |

Example:

```bash
df -h
```

```bash
du -sh /var
```

**Explanation**

`df` answers **"How much disk space is available?"**, while `du` answers **"What is using the space?"**

**Used in Production**

Both commands are commonly used together during disk space investigations.

**Common Mistake**

Using only `df` when trying to identify which directory is consuming storage.

---

### Question 5

**Question**

What is the `lsblk` command?

**Answer**

`lsblk` lists storage devices and their partition structure.

Example:

```bash
lsblk
```

Sample output:

```text
sda
├── sda1
├── sda2
└── sda3
```

**Explanation**

`lsblk` provides a hierarchical view of disks, partitions, and mount points.

**Used in Production**

Administrators use `lsblk` after adding new disks or troubleshooting storage devices.

---

### Question 6

**Question**

What is the `mount` command?

**Answer**

`mount` attaches a file system to a directory so it becomes accessible.

Example:

```bash
sudo mount /dev/sdb1 /mnt/data
```

View mounted file systems:

```bash
mount
```

**Explanation**

A storage device must be mounted before its contents can be accessed.

**Used in Production**

Administrators mount new disks, cloud volumes, network shares, and backup storage.

---

### Question 7

**Question**

What is the `umount` command?

**Answer**

`umount` safely detaches a mounted file system.

Example:

```bash
sudo umount /mnt/data
```

or

```bash
sudo umount /dev/sdb1
```

**Explanation**

Unmounting ensures all pending writes are completed before the device is removed.

**Used in Production**

Administrators unmount storage before maintenance or removing disks.

**Common Mistake**

Removing a storage device without unmounting it first, risking data corruption.

---

### Question 8

**Question**

What is a Mount Point?

**Answer**

A mount point is a directory where a file system becomes accessible.

Example:

```text
/mnt/data
```

After mounting:

```text
/dev/sdb1
      │
      ▼
/mnt/data
```

**Explanation**

Linux accesses storage devices through mount points rather than drive letters.

**Used in Production**

Additional storage is commonly mounted under directories such as `/mnt`, `/media`, or application-specific paths.

---

### Question 9

**Question**

How can you identify which directory is consuming the most disk space?

**Answer**

Run:

```bash
du -sh /*
```

or

```bash
du -h /var
```

Sort results if needed:

```bash
du -sh * | sort -h
```

**Explanation**

`du` reports directory sizes, helping identify storage-heavy locations.

**Used in Production**

Administrators use this approach when investigating storage alerts.

---

### Question 10

**Question**

How do you verify that a new disk has been detected by Linux?

**Answer**

Use:

```bash
lsblk
```

or

```bash
fdisk -l
```

Then verify whether the disk is mounted:

```bash
mount
```

**Explanation**

Detecting the device is the first step before partitioning, formatting, and mounting it.

**Used in Production**

Cloud administrators frequently verify newly attached volumes using these commands.

---

### Question 11

**Question**

What are some best practices for Linux Disk & File System Management?

**Answer**

Best practices include:

- Monitor disk usage regularly with `df`.
- Identify large directories using `du`.
- Verify new disks using `lsblk`.
- Always unmount storage before removal.
- Monitor log growth.
- Configure automated disk usage alerts.
- Maintain adequate free space.
- Test backups and recovery procedures.

**Explanation**

Regular monitoring helps prevent storage-related outages and simplifies capacity planning.

**Used in Production**

Enterprise environments continuously monitor storage utilization to avoid service interruptions.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

A production server reports "No space left on device." How would you troubleshoot the issue?

**Answer**

1. Check overall disk usage:

```bash
df -h
```

2. Identify large directories:

```bash
du -sh /*
```

3. Investigate log files, temporary files, or backups consuming excessive space.
4. Remove or archive unnecessary data after verifying it is safe to do so.

**Explanation**

`df` identifies the affected file system, while `du` identifies what is consuming the space.

---

### Scenario 2

**Question**

A new disk has been attached to a Linux server, but it is not visible in the application. What would you check?

**Answer**

Verify:

```bash
lsblk
```

Confirm the disk is detected, partitioned if necessary, formatted, and mounted to the expected mount point.

**Explanation**

A newly attached disk cannot be used until it is mounted.

---

### Scenario 3

**Question**

A directory under `/var` continues growing and filling the disk. How would you investigate?

**Answer**

Run:

```bash
du -sh /var/*
```

Identify the largest subdirectories and determine whether log files, cache files, or application data are responsible.

**Explanation**

Large directories often indicate excessive logging or temporary file accumulation.

---

### Scenario 4

**Question**

You need to temporarily mount a backup disk. Which command would you use?

**Answer**

Run:

```bash
sudo mount /dev/sdb1 /mnt/backup
```

Verify successful mounting:

```bash
df -h
```

**Explanation**

The disk must be mounted before its contents can be accessed.

---

### Scenario 5

**Question**

Before disconnecting an external storage device, what should you do?

**Answer**

Unmount it safely:

```bash
sudo umount /mnt/backup
```

Verify that no processes are using the device before removing it.

**Explanation**

Unmounting flushes pending writes and reduces the risk of data corruption.

---

### Scenario 6

**Question**

An application team claims their application is consuming too much disk space. How would you verify this?

**Answer**

Run:

```bash
du -sh /opt/application
```

Review subdirectory usage if necessary:

```bash
du -h /opt/application
```

**Explanation**

`du` reports the storage consumed by application files and directories.

---

### Scenario 7

**Question**

Your monitoring system reports that disk usage is 95%, but the development team wants to know exactly which directories are responsible. Which command would you use?

**Answer**

Use:

```bash
du -sh /*
```

or investigate the affected file system in more detail using:

```bash
du -h /path
```

**Explanation**

`df` identifies the full file system, while `du` identifies the directories consuming space.

---

### Scenario 8

**Question**

A mounted backup volume is missing after a server reboot. What would you investigate?

**Answer**

Check:

- Whether the disk is detected:

```bash
lsblk
```

- Current mounted file systems:

```bash
mount
```

- Persistent mount configuration in:

```text
/etc/fstab
```

**Explanation**

Storage that is not configured in `/etc/fstab` may not mount automatically after a reboot.

---

### Scenario 9

**Question**

You accidentally attempt to unmount a busy file system and receive a "target is busy" error. What could be the cause?

**Answer**

One or more processes are still using the mounted file system.

Investigate which processes are accessing the mount point, stop or relocate those processes if appropriate, and then retry the unmount operation.

**Explanation**

Linux prevents unmounting active file systems to protect data integrity.

---

### Scenario 10

**Question**

A cloud administrator adds a new storage volume to a virtual machine, but the operating system does not appear to use it. What additional steps are required?

**Answer**

After verifying the disk with `lsblk`, complete the remaining steps:

1. Partition the disk if required.
2. Create a file system.
3. Mount the file system.
4. Configure persistent mounting if needed.

**Explanation**

Attaching a disk alone does not make it usable by the operating system.

---

### Scenario 11

**Question**

During a production incident, application performance degrades because the root file system reaches 100% utilization. How would you troubleshoot and resolve the issue?

**Answer**

1. Identify the affected file system:

```bash
df -h
```

2. Locate large directories:

```bash
du -sh /*
```

3. Investigate logs, temporary files, backups, or application-generated data.
4. Archive or remove unnecessary files after verification.
5. If required, add additional storage, mount it appropriately, and move large data directories.
6. Implement monitoring and log rotation to prevent recurrence.

**Explanation**

Running out of disk space can prevent applications, databases, and services from functioning correctly. A structured investigation using `df`, `du`, `lsblk`, and mount information helps identify the root cause and restore normal operation while preventing future incidents.
