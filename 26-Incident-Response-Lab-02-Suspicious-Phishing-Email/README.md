# Incident Response Lab 2 — Suspicious Benefits Email

> **Project type:** Self-directed educational simulation  
> **Focus:** Phishing triage, email-header review, URL analysis, IoC handling, incident severity, response recommendations  
> **Environment:** Fictional training data only; all domains and indicators are reserved or non-routable  
> **Experience note:** This case study does not represent production incident-response work or use of a production SIEM.

## 1. Executive summary

A staff member reported an unexpected email claiming that a benefits statement was ready. The message used urgency, an unfamiliar sender, a mismatched reply address, failed authentication results in the supplied header, and a link whose displayed text did not match its destination. The recipient clicked the link. A simulated browser security event records that navigation was blocked; the supplied evidence shows no form submission, credential entry, download, or execution.

**Initial assessment:** Confirmed phishing attempt; exposure from the click is limited by the reported block, but requires validation. No account or endpoint compromise is confirmed by the available evidence.

**Initial severity:** Medium, pending the organization’s severity matrix and validation of endpoint, identity, and mail telemetry. The click raises risk; the block and absence of observed submission or execution limit the currently evidenced impact.

## 2. Scenario and evidence packet

This scenario is fictional. The .example and .invalid domains are reserved for documentation and should not be visited. The IP addresses below are from documentation-only ranges. Do not click or resolve any indicator.

**Case ID:** IR-2026-021  
**Reported:** 2026-10-21 09:24 UTC  
**Recipient:** j.lee@northstar.example  
**Mailbox:** j.lee@northstar.example  
**Message subject:** Benefits statement available — action required today  
**Message ID:** <20261021.0921.44@mailer.benefits-alert.example>

### Sample message

~~~text
From: "Northstar Benefits" <notice@benefits-alert.example>
Reply-To: claims@northstar-benefits.invalid
To: j.lee@northstar.example
Date: Wed, 21 Oct 2026 09:21:44 +0000
Subject: Benefits statement available — action required today
Message-ID: <20261021.0921.44@mailer.benefits-alert.example>

Your updated benefits statement is ready. Review it today to avoid a
delay in your account.

View statement:
hxxps://northstar-benefits.invalid/statement

If you have questions, reply to this message.
~~~

The URL is defanged for safe reading. The link text in the original message was “View statement”; the destination shown in the evidence packet was https://northstar-benefits.invalid/statement. No live destination was opened for this exercise.

### Sanitized header excerpt (fictional)

~~~text
Return-Path: <bounce@mailer.benefits-alert.example>
Received: from relay-07.mailer.benefits-alert.example
 (192.0.2.44) by mx.northstar.example with ESMTPS;
 Wed, 21 Oct 2026 09:21:46 +0000
From: "Northstar Benefits" <notice@benefits-alert.example>
Reply-To: claims@northstar-benefits.invalid
Authentication-Results: mx.northstar.example;
 spf=fail smtp.mailfrom=mailer.benefits-alert.example;
 dkim=fail header.d=benefits-alert.example;
 dmarc=fail header.from=benefits-alert.example
Message-ID: <20261021.0921.44@mailer.benefits-alert.example>
~~~

This is a deliberately partial, synthetic header. The excerpt does not establish the full mail path, the actual sender, or whether a real mail system would evaluate authentication the same way.

### Related telemetry supplied for triage

| Timestamp (UTC) | Source | Event |
|---|---|---|
| 09:21:46 | Mail gateway | Message delivered to one recipient; no attachment recorded |
| 09:23:08 | User report | Recipient reported the message as suspicious |
| 09:23:31 | Endpoint/browser event | Click on the message link; browser security control blocked navigation |
| 09:24:02 | Identity log summary | No sign-in or MFA event correlated in the supplied 30-minute window |
| 09:24:10 | Endpoint log summary | No download or process launch correlated in the supplied 30-minute window |

These are scenario facts, not findings from a live environment. Missing events in this small evidence packet do not prove that no activity occurred.

## 3. Analyst objectives

1. Separate observed evidence from interpretation.
2. Assess sender identity and authentication signals in the supplied headers.
3. Parse the displayed link and destination without opening it.
4. Record useful, safe-to-share indicators and their limitations.
5. Assign a provisional severity with rationale and confidence.
6. Recommend proportionate response, validation, and escalation steps.
7. Produce a concise incident report that does not overstate impact or attribution.

## 4. Triage findings

### Observed facts

- The message claims to be from “Northstar Benefits,” but the sender domain is benefits-alert.example, not the fictional organization’s northstar.example domain.
- Reply-To points to a different domain, northstar-benefits.invalid.
- The supplied Authentication-Results line records SPF, DKIM, and DMARC failures.
- The message uses urgency (“action required today”) and asks the recipient to review a benefits statement.
- The visible link text is generic, and its destination is on the unrelated northstar-benefits.invalid domain.
- One recipient received the message in the scenario.
- The recipient clicked the link; a browser control recorded blocked navigation.
- The supplied summaries show no correlated identity sign-in/MFA event, download, or process launch in a 30-minute window.

### Assessment

The combined sender mismatch, failed authentication results, unrelated reply and link domains, and urgency are consistent with a phishing attempt. These signals support classification of the email as malicious or highly suspicious, but they do not identify the operator or prove that the destination hosted a particular payload.

The click is a meaningful exposure event. The browser block and the supplied absence of follow-on events are reassuring but need corroboration from the relevant mail, web proxy/DNS, endpoint, and identity records. Based on this packet alone, credential theft, malware execution, and account compromise are **not confirmed**.

### Preliminary severity

**Provisional severity: Medium. Confidence: Moderate.**

Rationale: a user clicked the link, so the case warrants prompt validation and response. The scenario records a browser block, one recipient, and no observed submission, download, process launch, or correlated sign-in in the limited supplied window. Raise severity if validation finds credentials submitted, authentication anomalies, endpoint execution, additional recipients, or sensitive data access. Apply the organization’s severity matrix and escalation criteria before finalizing.

## 5. Header and URL analysis

| Evidence | What it may indicate | Limitation |
|---|---|---|
| Display name claims “Northstar Benefits”; sender domain is benefits-alert.example | Brand impersonation or an unfamiliar sender | A display-name/domain mismatch alone is not proof of maliciousness |
| Reply-To differs from the sender and uses .invalid | Replies may be directed elsewhere | The header is synthetic; verify actual message metadata in the mail platform |
| SPF, DKIM, and DMARC are marked fail | The message did not pass the checks as represented in this packet | Authentication failures can have benign causes; check alignment, forwarding, and raw headers |
| Link destination is northstar-benefits.invalid/statement | Destination does not match the claimed sender or expected organization domain | The URL is inert training data; no reputation or hosting claims can be made |
| Browser event says navigation was blocked | A protective control intervened after the click | Confirm whether the block happened before any redirect, content load, or data entry |

### Safe URL handling

- Preserve and inspect the message as an attachment or through the approved mail-analysis workflow.
- Do not open the link, paste it into a browser, or query the synthetic domain.
- Record both the displayed link text and the actual destination from the message source.
- Defang URLs in notes shared outside the controlled analysis environment.
- In a real case, use approved sandboxing and reputation tools, and follow the organization’s handling procedures.

## 6. Indicators of compromise (IoCs)

All indicators below are fictional training artifacts. They are not live threat intelligence and must not be used to block or investigate real infrastructure.

| Type | Indicator | Confidence | Notes |
|---|---|---:|---|
| Sender address | notice@benefits-alert.example | High for this message | From field in the sample; sender identity is not authenticated by this alone |
| Reply address | claims@northstar-benefits.invalid | High for this message | Mismatched Reply-To in sample |
| Sender domain | benefits-alert.example | High for this message | Synthetic reserved domain |
| Link domain | northstar-benefits.invalid | High for this message | Synthetic reserved domain; link was not visited |
| URL path | /statement | High for this message | Path alone is not a unique indicator |
| Source IP | 192.0.2.44 | High for the synthetic header | Documentation range; not a real attacker IP |
| Message-ID | <20261021.0921.44@mailer.benefits-alert.example> | High for this sample | Useful for locating this message in mail telemetry |

For a real incident, preserve the original message and record the source and collection time for each indicator. Avoid treating a sender address, domain, or IP as conclusive attribution.

## 7. Preliminary MITRE ATT&CK mapping

| Candidate technique | Rationale | Confidence / caveat |
|---|---|---|
| **T1566.002 — Phishing: Spearphishing Link** | The email contains a link and the recipient clicked it. | Candidate mapping based on the scenario. The fictional evidence does not establish the actor or the link’s actual payload. |
| **T1204.001 — User Execution: Malicious Link** | The recipient interacted with the link. | Preliminary only. The browser block is recorded; the evidence does not show that malicious content executed or credentials were submitted. |

This mapping describes candidate behaviors for investigation. It is not attribution, proof of compromise, or a claim that a technique succeeded.

## 8. Response recommendations

### Immediate actions

1. Preserve the original email, full headers, gateway verdict, and browser security event with timestamps and case references.
2. Search the mail environment for the Message-ID, sender, subject, and link indicators to identify other recipients or copies.
3. Remove or quarantine matching messages using approved mail-security procedures, if additional copies exist.
4. Confirm with the recipient whether they entered credentials, approved an MFA prompt, downloaded a file, or saw a page before the block. Avoid asking them to revisit the link.
5. Validate the browser block and check web proxy/DNS, endpoint, and identity telemetry around the event, including redirects and sign-ins outside the initial 30-minute summary.
6. If credentials may have been entered, follow the identity incident playbook to revoke sessions, reset credentials, and review MFA and sign-in activity. Do not reset accounts solely because a link was clicked if policy and evidence do not support it.
7. Escalate if evidence suggests credential submission, successful navigation to harmful content, endpoint execution, wider targeting, or access to sensitive resources.
8. Document each action, owner, timestamp, evidence source, and decision rationale.

### Closure criteria

Close or downgrade only after the message scope is understood, the click and browser block are validated, relevant endpoint and identity telemetry are reviewed, any exposed credentials or other impact are addressed, and the disposition is documented under the organization’s process. Keep the case open or escalate if material evidence remains unavailable or suspicious activity is found.

## 9. Concise incident report

**Incident:** IR-2026-021 — Suspicious benefits email  
**Status:** Phishing attempt; impact validation in progress  
**Severity:** Medium, provisional; Moderate confidence  
**Summary:** One fictional recipient received an unexpected benefits email with mismatched sender and reply domains, failed authentication results in the supplied header, urgency language, and an unrelated link. The recipient clicked the link; the scenario’s browser control blocked navigation.  
**Impact known:** No credential submission, download, process execution, or correlated sign-in is shown in the limited supplied evidence. These absences require validation and do not prove there was no impact.  
**Assessment:** The email is consistent with phishing. No account or endpoint compromise is confirmed.  
**Recommended actions:** Preserve the message and telemetry; search for additional recipients; validate the block and check mail, web, endpoint, and identity records; ask the recipient about any data entry or prompts; contain matching email and take identity actions only if supported by evidence and policy.  
**Next update:** After scope and post-click activity are validated.

## 10. Lessons demonstrated

- Analyze the actual sender, reply address, authentication results, and link destination together.
- Treat header fields as evidence to validate, not as standalone proof.
- Do not open suspicious links during triage; preserve and inspect them through approved methods.
- A click is exposure, not proof that credentials were stolen or code executed.
- Use safe indicators and clearly state the limits of synthetic data.
- Assign severity based on evidence, impact, confidence, and the organization’s own criteria.
- Map ATT&CK techniques provisionally and distinguish attempted behavior from confirmed outcomes.
- Write incident notes that separate facts, hypotheses, gaps, and next actions.

---

**Disclaimer:** This is a self-directed educational simulation using fictional, inert training data. It does not represent professional incident-response experience, investigation of a real phishing email, or hands-on work in a production environment.
