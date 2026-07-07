# File Compression & Archiving

## Overview

File Compression & Archiving are common Linux operations used to:

- Combine multiple files into a single archive
- Reduce file size
- Create backups
- Transfer files efficiently
- Package applications
- Store logs

In Linux, **archiving** and **compression** are different concepts:

- **Archiving** combines multiple files into one file.
- **Compression** reduces the size of files.

> **Interview Point**
>
> **`tar` archives files but does not compress them by default.**
>
> Compression is achieved by combining `tar` with tools such as `gzip`.

---

## Why It Is Used

Compression and archiving help to:

- Save disk space
- Simplify backups
- Transfer files over networks
- Archive application logs
- Package deployment artifacts

---

## Architecture / Working

```mermaid
flowchart LR

Files --> tar

tar --> Archive

Archive --> gzip

gzip --> CompressedArchive

CompressedArchive --> Transfer
```

---

## Key Components

| Component | Purpose |
|------------|----------|
| tar | Archive files |
| gzip | Compress files |
| gunzip | Decompress gzip files |
| zip | Archive and compress |
| unzip | Extract ZIP archives |

---

## Types

### Archiving

- tar

### Compression

- gzip
- zip

### Decompression

- gunzip
- unzip

---

## Lifecycle / Workflow

```mermaid
flowchart LR

Files

Files --> Archive

Archive --> Compress

Compress --> Transfer

Transfer --> Decompress

Decompress --> Extract
```

---

## Configuration / Syntax

Common workflow

```bash
tar

gzip

gunzip

zip

unzip
```

---

## Important Commands

```bash
tar

gzip

gunzip

zip

unzip
```

---

## Important Files

| Extension | Description |
|------------|-------------|
| .tar | Archive |
| .gz | Gzip compressed file |
| .tar.gz | Archived and compressed |
| .tgz | Short form of .tar.gz |
| .zip | ZIP archive |

---

## Real-World Use Cases

- Backup Linux servers
- Archive logs
- Package application releases
- Store configuration backups
- Transfer deployment artifacts

---

## Advantages

- Saves storage
- Faster transfers
- Easy backups
- Widely supported

---

## Limitations

- Compression requires CPU resources
- Corrupted archives may affect recovery
- Some formats (e.g., `.tar`) do not compress by themselves

---

## Common Interview Questions (Concept Only)

- Difference between Archiving and Compression?
- What is a `.tar.gz` file?
- Why is `tar` commonly used with `gzip`?
- When should `zip` be preferred?

---

## Common Mistakes

- Assuming `tar` compresses files by default
- Compressing files multiple times unnecessarily
- Deleting the original archive before verifying extraction

---

## Troubleshooting

| Problem | Solution |
|----------|----------|
| Cannot extract archive | Verify archive format and command |
| Archive corrupted | Verify checksum or recreate archive |
| Compression failed | Check disk space and file permissions |

---

## Summary

Linux archiving and compression tools are essential for backups, deployments, log management, and file transfers. Understanding the difference between archiving (`tar`) and compression (`gzip`, `zip`) is a common interview topic.

---

# tar

## Overview

`tar` (Tape Archive) combines multiple files and directories into a single archive file.

By default, `tar` **does not compress** data.

> **Interview Point**
>
> `tar` is primarily an **archiving utility**, not a compression utility.

---

## Why It Is Used

- Create backups
- Package applications
- Archive logs
- Preserve directory structure
- Prepare files for compression

---

## Architecture / Working

```mermaid
flowchart LR

Files --> tar --> Archive.tar
```

---

## Key Components

| Option | Purpose |
|---------|----------|
| -c | Create archive |
| -x | Extract archive |
| -t | List archive contents |
| -v | Verbose output |
| -f | Archive filename |
| -z | Use gzip compression |
| -C | Extract into specified directory |

---

## Types

### Archive Only

```bash
tar -cvf backup.tar project/
```

### Archive + Gzip

```bash
tar -czvf backup.tar.gz project/
```

### Extract

```bash
tar -xvf backup.tar
```

### Extract Gzip Archive

```bash
tar -xzvf backup.tar.gz
```

### List Contents

```bash
tar -tvf backup.tar
```

---

## Lifecycle / Workflow

```mermaid
flowchart LR

Files --> tar --> Archive --> Extract
```

---

## Configuration / Syntax

Create archive

```bash
tar -cvf archive.tar folder/
```

Create compressed archive

```bash
tar -czvf archive.tar.gz folder/
```

Extract archive

```bash
tar -xvf archive.tar
```

Extract compressed archive

```bash
tar -xzvf archive.tar.gz
```

---

## Important Commands

```bash
tar -cvf

tar -xvf

tar -czvf

tar -xzvf

tar -tvf

tar -C
```

---

## Important Files

| Extension | Purpose |
|-----------|----------|
| .tar | Archive |
| .tar.gz | Gzip compressed archive |
| .tgz | Compressed archive |

---

## Real-World Use Cases

- Backup servers
- Deploy applications
- Archive logs
- Package source code
- Transfer project files

---

## Advantages

- Preserves directory structure
- Supports multiple compression methods
- Widely supported

---

## Limitations

- No compression unless combined with a compression utility
- Large archives can take time to create or extract

---

## Common Interview Questions (Concept Only)

- What is `tar`?
- Does `tar` compress files?
- Difference between `tar` and `zip`?
- What does `tar -czvf` do?
- What does `tar -xvf` do?

---

## Common Mistakes

- Forgetting the `-f` option
- Confusing `-c` (create) with `-x` (extract)
- Assuming `.tar` files are compressed

---

## Troubleshooting

| Problem | Solution |
|----------|----------|
| Cannot extract | Verify archive type (`.tar` vs `.tar.gz`) |
| File not found | Check archive filename and path |
| Extraction location incorrect | Use the `-C` option to specify the destination directory |

---

## Summary

`tar` is the standard Linux archiving tool used to package files and directories. It is commonly combined with `gzip` to create compressed archives such as `.tar.gz`.

---

# gzip

## Overview

`gzip` compresses files to reduce their size.

Unlike `tar`, `gzip` compresses **individual files** rather than combining multiple files into a single archive.

By default, the original file is replaced with a `.gz` compressed file.

> **Interview Point**
>
> `gzip` compresses **one file at a time**. To compress multiple files together, first create a `tar` archive.

---

## Why It Is Used

- Reduce storage usage
- Speed up file transfers
- Compress log files
- Save bandwidth

---

## Architecture / Working

```mermaid
flowchart LR

File --> gzip --> File.gz
```

---

## Key Components

| Option | Purpose |
|---------|----------|
| -d | Decompress |
| -k | Keep original file |
| -l | List compressed file information |
| -r | Compress recursively |

---

## Lifecycle / Workflow

```mermaid
flowchart LR

File --> Compress --> File.gz
```

---

## Configuration / Syntax

Compress

```bash
gzip file.txt
```

Keep original file

```bash
gzip -k file.txt
```

---

## Important Commands

```bash
gzip

gzip -k

gzip -l

gzip -r
```

---

## Important Files

| Extension | Purpose |
|-----------|----------|
| .gz | Gzip compressed file |

---

## Real-World Use Cases

- Compress logs
- Archive reports
- Reduce backup size

---

## Advantages

- Fast compression
- Good compression ratio
- Standard on Linux

---

## Limitations

- Compresses one file at a time
- Replaces the original file unless instructed otherwise

---

## Common Interview Questions (Concept Only)

- What is `gzip`?
- Difference between `gzip` and `tar`?
- Why combine `tar` and `gzip`?

---

## Common Mistakes

- Compressing multiple files individually instead of using `tar`
- Forgetting that the original file is removed by default

---

## Troubleshooting

| Problem | Solution |
|----------|----------|
| Original file missing | Use the `-k` option to keep the original |
| Compression failed | Verify file permissions and available disk space |

---

## Summary

`gzip` efficiently compresses individual files and is commonly paired with `tar` to create compressed archives.

---

# gunzip

## Overview

`gunzip` decompresses `.gz` files created by `gzip`.

It restores the original file by removing the `.gz` extension.

> **Interview Point**
>
> `gunzip` is functionally equivalent to running `gzip -d`.

---

## Why It Is Used

- Restore compressed files
- Read archived logs
- Recover backups

---

## Architecture / Working

```mermaid
flowchart LR

File.gz --> gunzip --> File
```

---

## Lifecycle / Workflow

```mermaid
flowchart LR

CompressedFile --> Decompress --> OriginalFile
```

---

## Configuration / Syntax

```bash
gunzip file.gz
```

Equivalent command

```bash
gzip -d file.gz
```

---

## Important Commands

```bash
gunzip

gzip -d
```

---

## Real-World Use Cases

- Restore log files
- Extract backups
- Recover deployment packages

---

## Advantages

- Simple
- Fast

---

## Limitations

- Works only with gzip-compressed files

---

## Common Interview Questions (Concept Only)

- What is the purpose of `gunzip`?
- Difference between `gunzip` and `gzip -d`?

---

## Common Mistakes

- Attempting to extract `.tar.gz` using only `gunzip`
- Using `gunzip` on unsupported formats

---

## Troubleshooting

| Problem | Solution |
|----------|----------|
| Not in gzip format | Verify the file extension and format |
| File missing | Confirm the file path and name |

---

## Summary

`gunzip` restores files compressed with `gzip` and is commonly used to recover `.gz` archives.

---

# zip

## Overview

`zip` creates compressed ZIP archives.

Unlike `tar`, `zip` both **archives and compresses** files in a single step.

ZIP is widely supported across Linux, Windows, and macOS.

> **Interview Point**
>
> `zip` performs **archiving and compression together**, while `tar` requires an additional compression utility such as `gzip`.

---

## Why It Is Used

- Cross-platform compatibility
- Compress project files
- Email attachments
- Package documents

---

## Architecture / Working

```mermaid
flowchart LR

Files --> zip --> Archive.zip
```

---

## Key Components

| Option | Purpose |
|---------|----------|
| -r | Recursive archive |
| -9 | Maximum compression |
| -e | Encrypt archive (password-protected ZIP) |

---

## Lifecycle / Workflow

```mermaid
flowchart LR

Files --> Compress --> Archive.zip
```

---

## Configuration / Syntax

Create ZIP archive

```bash
zip archive.zip file.txt
```

Archive a directory

```bash
zip -r project.zip project/
```

---

## Important Commands

```bash
zip

zip -r

zip -9

zip -e
```

---

## Important Files

| Extension | Purpose |
|-----------|----------|
| .zip | ZIP archive |

---

## Real-World Use Cases

- Share projects
- Backup documents
- Cross-platform file exchange

---

## Advantages

- Built-in compression
- Widely supported
- Easy sharing

---

## Limitations

- Typically slower than `tar` for large Linux backups
- May not preserve all Linux file metadata as effectively as `tar`

---

## Common Interview Questions (Concept Only)

- Difference between `zip` and `tar`?
- Why is `zip` popular on Windows?

---

## Common Mistakes

- Forgetting the recursive (`-r`) option for directories
- Assuming ZIP preserves all Linux permissions identically across platforms

---

## Troubleshooting

| Problem | Solution |
|----------|----------|
| Directory not included | Use the `-r` option |
| Archive not created | Verify destination path and write permissions |

---

## Summary

`zip` combines archiving and compression into a single operation, making it ideal for cross-platform file sharing.

---

# unzip

## Overview

`unzip` extracts files from ZIP archives.

It restores the archived directory structure and files to the current or specified directory.

> **Interview Point**
>
> `unzip` is the standard utility for extracting ZIP archives on Linux.

---

## Why It Is Used

- Restore ZIP archives
- Extract application packages
- Access shared files

---

## Architecture / Working

```mermaid
flowchart LR

Archive.zip --> unzip --> Files
```

---

## Lifecycle / Workflow

```mermaid
flowchart LR

ZIPArchive --> Extract --> Files
```

---

## Configuration / Syntax

Extract to the current directory

```bash
unzip archive.zip
```

Extract to another directory

```bash
unzip archive.zip -d /home/user/project
```

List archive contents without extracting

```bash
unzip -l archive.zip
```

---

## Important Commands

```bash
unzip

unzip -d

unzip -l
```

---

## Important Files

| Extension | Purpose |
|-----------|----------|
| .zip | ZIP archive |

---

## Real-World Use Cases

- Restore project archives
- Extract deployment packages
- Install software distributed as ZIP files

---

## Advantages

- Simple extraction
- Cross-platform compatibility
- Preserves directory structure

---

## Limitations

- Requires the `unzip` package if it is not installed
- Extraction may overwrite existing files if not managed carefully

---

## Common Interview Questions (Concept Only)

- What does `unzip` do?
- How do you extract a ZIP file into a different directory?
- How do you list ZIP archive contents without extracting them?

---

## Common Mistakes

- Extracting into the wrong directory
- Overwriting existing files unintentionally

---

## Troubleshooting

| Problem | Solution |
|----------|----------|
| unzip: command not found | Install the `unzip` package |
| Archive corrupted | Verify archive integrity or download it again |
| Permission denied | Check write permissions on the destination directory |

---

## Summary

`unzip` extracts ZIP archives and is commonly used to restore compressed files, deployment packages, and cross-platform project archives.
