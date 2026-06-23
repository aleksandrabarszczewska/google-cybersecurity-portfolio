# Web Application Security Incident Investigation

## Overview

This project presents a simulated web application security incident investigation involving unauthorized administrative access obtained through a brute-force attack against default credentials.

The objective was to identify the root cause of the compromise, assess its impact, and recommend remediation measures to improve the organization's security posture.

## Scenario

A web application was compromised after an attacker successfully gained administrative access using default account credentials. Following the compromise, malicious code was injected into the website, resulting in unauthorized redirects to a malicious domain.

## Investigation Activities

The investigation included:

- DNS traffic analysis
- HTTP traffic analysis using tcpdump
- Review of website source code
- Analysis of malicious redirection activity
- Root cause determination
- Documentation of findings and remediation recommendations

## Key Findings

The investigation identified the following issues:

- Administrative account protected by default credentials
- Successful brute-force attack resulting in unauthorized access
- Malicious JavaScript embedded within website source code
- Users redirected to a malicious external domain
- Potential compromise of customer devices through downloaded malware

## Root Cause

The primary cause of the incident was the use of default administrative credentials combined with insufficient account protection controls.

## Recommended Controls

### Identity and Access Security

- Multi-Factor Authentication (MFA)
- Strong password policy enforcement
- Secure credential management
- Account lockout mechanisms

### Monitoring and Detection

- Continuous monitoring of administrative accounts
- Authentication event monitoring
- Security logging and alerting

### Application Security

- Source code integrity monitoring
- Change management controls
- Regular security reviews of web applications

## Skills Demonstrated

- Incident Investigation
- Root Cause Analysis
- Access Control Review
- Risk Assessment
- Network Traffic Analysis
- Web Security Analysis
- Security Documentation
- Remediation Planning

## Outcome

This project demonstrates the ability to investigate web application security incidents, identify attack vectors, determine root causes, evaluate business impact, and develop remediation recommendations to reduce future risk.
