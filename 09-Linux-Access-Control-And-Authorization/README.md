# Linux Access Control and Authorization

## Overview

This project demonstrates the implementation of access control and authorization principles in a Linux environment through the review and modification of file and directory permissions.

The objective was to ensure that access to system resources was granted only to authorized users while enforcing the principle of least privilege and reducing unnecessary permissions.

## Project Objectives

The project focused on:

- Reviewing existing access permissions
- Identifying excessive privileges
- Restricting unauthorized access
- Securing hidden files
- Applying least privilege principles
- Strengthening file system security

## Activities Performed

### Reviewing File and Directory Permissions

Existing permissions were reviewed using:

```bash
ls -la
```

This allowed visibility into:

- File ownership
- Group assignments
- Hidden files
- Current permission settings

### Understanding Linux Permission Structures

The project included analysis of Linux permission strings such as:

```text
-rw-rw-r--
```

Permission reviews covered:

- Owner permissions
- Group permissions
- Other user permissions
- File type identification

### File Permission Modification

Permissions were adjusted to remove unnecessary write access.

Example:

```bash
chmod o-w project_k.txt
```

This reduced the risk of unauthorized modification by users outside the intended access group.

### Hidden File Protection

Additional controls were applied to sensitive hidden files.

Examples:

```bash
chmod u-w .project_x.txt
chmod g+r .project_x.txt
chmod g-w .project_x.txt
```

The resulting configuration ensured:

- Read access for authorized users
- Removal of unnecessary write permissions
- Improved protection of sensitive data

## Access Control Concepts Demonstrated

- Access Control
- Authorization Management
- Least Privilege Enforcement
- Linux Permission Management
- User and Group Security
- File System Hardening
- Security Administration
- Principle of Need-to-Know

## Security Benefits

The implemented controls helped:

- Reduce unauthorized access risks
- Restrict unnecessary privileges
- Protect sensitive files
- Improve security governance
- Strengthen access management practices

## Skills Demonstrated

- Linux Administration
- Linux Access Control
- Authorization Management
- Permission Analysis
- Principle of Least Privilege
- Security Hardening
- File System Security
- Command-Line Operations
- Security Verification

## Outcome

Successfully reviewed and modified Linux file permissions to align with organizational security requirements, improve authorization controls, and reduce the risk of unauthorized access or modification of sensitive resources.
