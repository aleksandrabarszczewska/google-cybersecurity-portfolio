# SQL Security Log Investigation and Filtering

## Overview

This project demonstrates the use of SQL queries to investigate potential security incidents and retrieve relevant information from organizational databases.

Using filtering techniques such as `AND`, `OR`, `NOT`, and `LIKE`, the project analyzed login activity and employee records to identify suspicious events, support security investigations, and assist security-related decision-making.

## Project Objectives

The project focused on:

- Security log investigation
- Login activity analysis
- Employee record filtering
- Detection of suspicious activity
- Security monitoring support
- Database-driven investigations

---

## Investigation Activities

### Identifying After-Hours Failed Login Attempts

SQL queries were used to identify failed authentication attempts occurring outside normal business hours.

Example:

```sql
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00'
AND success = FALSE;
```

This activity helped identify potential unauthorized access attempts requiring further investigation.

### Investigating Login Activity on Specific Dates

Security events were reviewed by filtering records associated with specific dates.

Example:

```sql
SELECT *
FROM log_in_attempts
WHERE login_date = '2022-05-09'
OR login_date = '2022-05-08';
```

This allowed focused investigation around suspicious events and security incidents.

### Identifying Login Attempts from External Locations

Geographic filtering was used to identify login activity originating outside expected regions.

Example:

```sql
SELECT *
FROM log_in_attempts
WHERE NOT country LIKE 'MEX%';
```

This supported detection of unusual authentication activity and potential account compromise indicators.

### Filtering Employee Records for Security Operations

Employee records were filtered to support department-specific security activities.

Example:

```sql
SELECT *
FROM employees
WHERE department = 'Marketing'
AND office LIKE 'EAST%';
```

Additional filtering techniques included:

```sql
SELECT *
FROM employees
WHERE department = 'Finance'
OR department = 'Sales';
```

and

```sql
SELECT *
FROM employees
WHERE NOT department = 'Information Technology';
```

These queries supported asset management, security updates, and organizational security planning.

---

## SQL Techniques Demonstrated

### Logical Operators

- AND
- OR
- NOT

### Pattern Matching

- LIKE

### Data Filtering

- Time-based filtering
- Date-based filtering
- Geographic filtering
- Department-based filtering

### Database Investigation

- Security log analysis
- User activity review
- Employee record analysis
- Event correlation

---

## Security Concepts Demonstrated

- Security Monitoring
- Security Log Analysis
- Incident Investigation
- Authentication Monitoring
- Suspicious Activity Detection
- Data Analysis
- Operational Security Support
- Security Reporting

---

## Skills Demonstrated

- SQL Querying
- Data Filtering
- Security Log Analysis
- Incident Investigation
- Security Monitoring
- Database Querying
- Pattern Matching with LIKE
- Logical Operators (AND, OR, NOT)
- Security Analytics
- Cybersecurity Reporting

---

## Outcome

Successfully used SQL queries to support cybersecurity investigations and operational security tasks.

The project involved analyzing login activity and employee records, applying filtering techniques to identify suspicious events, investigate potential incidents, and retrieve information needed for security-related decision-making.

This project reinforced practical skills in security monitoring, log analysis, database investigations, and data-driven cybersecurity analysis.
