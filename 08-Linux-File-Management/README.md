# Linux File Permissions Management

## Overview

This project demonstrates the review and modification of file and directory permissions in a Linux environment to align with organizational security requirements and the principle of least privilege.

The objective was to identify excessive permissions, reduce unauthorized access risks, and strengthen file system security through proper permission management.

## Objective

Review and modify file and directory permissions to ensure access is granted only to authorized users while maintaining operational functionality.

## Tasks Performed

### Permission Review

Existing permissions were reviewed using Linux command-line tools, including:

```bash
ls -la
```

The review included:

- Files and directories
- Hidden files
- Ownership settings
- Existing permission assignments

### File Permission Hardening

Removed unnecessary write permissions from other users using:

```bash
chmod o-w project_k.txt
```

Permissions were then verified to confirm successful implementation.

### Hidden File Security

Modified permissions on hidden files to reduce unnecessary access while preserving required functionality.

Example:

```bash
chmod u-w,g-w,g+r .project_x.txt
```

### Directory Access Control

Restricted directory permissions to enforce least privilege principles.

Example:

```bash
chmod g-x drafts
```

This ensured that only authorized users retained appropriate access to directory contents.

## Security Concepts Demonstrated

- Linux File Permissions
- User, Group, and Other Access Controls
- Principle of Least Privilege
- File System Hardening
- Access Management
- Security Verification
- Linux Command-Line Administration

## Security Benefits

The implemented changes helped:

- Reduce unauthorized modification risks
- Limit unnecessary access permissions
- Improve file system security
- Strengthen access governance
- Support least privilege enforcement

## Skills Demonstrated

- Linux Administration
- Linux Security
- File Permission Management
- Access Control
- Principle of Least Privilege
- File System Hardening
- Security Verification
- Command-Line Operations

## Outcome

Successfully reviewed and modified file and directory permissions to align with organizational security requirements, reduce unauthorized access risks, and improve overall Linux system security.
