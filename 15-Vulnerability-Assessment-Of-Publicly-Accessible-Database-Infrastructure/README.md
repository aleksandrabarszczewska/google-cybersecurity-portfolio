# Access Control Investigation and Unauthorized Account Review

## Overview

This project involved investigating a suspicious payroll modification incident caused by unauthorized access to sensitive payroll resources.

The assessment focused on reviewing authentication records, access logs, user authorization practices, and account lifecycle management controls to determine how an inactive contractor account retained privileged access and contributed to the incident.

## Scenario

A growing organization detected suspicious modifications within its payroll system. Investigation revealed that an unauthorized bank account had been added to payroll records.

The incident prompted a detailed review of:

- Access logs
- User authorizations
- Privileged account management
- Identity and Access Management (IAM) processes
- Account deprovisioning procedures

---

## Objective

The objective was to:

- Identify weaknesses in access control processes
- Determine how an inactive contractor account retained access
- Analyze authorization and authentication records
- Assess risks associated with privileged accounts
- Recommend security improvements to prevent future incidents

---

## Investigation Activities

The investigation included:

- Reviewing authentication and authorization records
- Analyzing payroll system access logs
- Identifying privileged account activity
- Examining user lifecycle management processes
- Evaluating role assignments and authorization levels
- Assessing risks associated with inactive privileged accounts
- Developing remediation recommendations based on access control best practices

---

## Key Findings

### Inactive Contractor Account

The investigation identified a privileged contractor account that remained active after the contractor's engagement had ended.

### Excessive Privileges

The account retained administrator-level permissions despite no longer being required for business operations.

### Failed Deprovisioning Process

The organization lacked effective account deactivation procedures, allowing the account to remain active for several years after contract termination.

### Unauthorized Access

The inactive privileged account was used to access payroll resources and contributed to unauthorized modifications.

### Insider Threat Risk

Excessive permissions combined with poor account lifecycle management created a significant insider threat risk.

---

## Recommendations

### Account Lifecycle Management

- Automatically disable contractor accounts after contract expiration
- Implement formal offboarding procedures
- Review inactive accounts regularly

### Access Reviews

- Conduct periodic access reviews
- Validate privileged accounts quarterly
- Remove unnecessary permissions promptly

### Least Privilege

- Apply least privilege principles to administrative accounts
- Limit payroll access based on business requirements
- Reduce unnecessary privileged access

### Multi-Factor Authentication (MFA)

Implement MFA for all privileged and payroll-related accounts to reduce unauthorized access risks.

### Identity and Access Management (IAM)

Strengthen IAM processes through:

- Automated provisioning and deprovisioning
- Role-based access control (RBAC)
- Continuous account monitoring
- Privileged account governance

---

## Security Frameworks and Concepts

This project applied the following cybersecurity concepts:

- Access Control
- Authentication
- Authorization
- Identity and Access Management (IAM)
- Least Privilege
- Account Lifecycle Management
- Multi-Factor Authentication (MFA)
- Privileged Access Management

---

## Skills Demonstrated

- Log Analysis
- User Access Review
- Incident Investigation
- Authorization Assessment
- Risk Identification
- Security Recommendations
- Identity and Access Management
- Access Governance
- Privileged Account Review
- Security Documentation

---

## Outcome

Successfully identified weaknesses in account lifecycle management and privileged access governance that allowed an inactive contractor account to remain active after contract termination.

The project demonstrated how effective Identity and Access Management (IAM), least privilege enforcement, periodic access reviews, and automated deprovisioning processes help reduce insider threat risks and protect sensitive business systems.
