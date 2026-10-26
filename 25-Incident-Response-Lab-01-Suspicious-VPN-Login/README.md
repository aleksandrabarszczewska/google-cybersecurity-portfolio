# Incident Response Lab 1 — Suspicious VPN Login Investigation

> **Project type:** Self-directed educational simulation  
> **Scope:** Authentication log triage, containment decision-making, MFA verification, VPN session investigation, incident documentation  
> **Environment:** Fictional data only; no production systems accessed

## 1. Executive summary

A simulated SIEM alert was raised after multiple failed authentication attempts against account `a.smith` were followed by a successful login and a VPN session from the same source IP address.

The sequence is suspicious and is consistent with a possible credential attack. However, the available evidence does **not** confirm that the account was compromised or identify who controlled the source IP.

The response should preserve evidence, follow the incident-response and escalation procedures, and investigate authentication, MFA, VPN and post-login activity. Containment should be proportionate to the risk and the applicable playbook.

## 2. Scenario and evidence

**Alert ID:** IR-2026-014  
**Target:** `VPN-Gateway-01`  
**Account:** `a.smith`  
**Source IP:** `185.220.101.45`  
**Initial alert priority:** High

### Authentication timeline (UTC)

| Timestamp | Source IP | Account | Event |
|---|---|---|---|
| 09:14:02 | 185.220.101.45 | a.smith | Login failed |
| 09:14:08 | 185.220.101.45 | a.smith | Login failed |
| 09:14:13 | 185.220.101.45 | a.smith | Login failed |
| 09:14:19 | 185.220.101.45 | a.smith | Login failed |
| 09:14:25 | 185.220.101.45 | a.smith | Login successful |
| 09:17:41 | 185.220.101.45 | a.smith | VPN session established |

### Additional triage information

- An MFA event was recorded as approved.
- It is not confirmed whether the legitimate user approved the request.
- Post-login activity is unknown.
- All data in this exercise is fictional and deliberately limited.

## 3. Initial assessment

### Observed facts

1. Five failed login attempts occurred within 23 seconds.
2. A successful login followed 6 seconds after the last failed attempt.
3. The failed and successful attempts came from the same source IP in the supplied records.
4. A VPN session was established shortly afterwards.
5. An MFA approval was recorded, but its context and legitimacy have not been verified.

### Working hypothesis

A credential attack, such as password guessing, may have preceded an unauthorized login. Other explanations remain possible, including a legitimate user repeatedly entering an incorrect password before successfully authenticating.

The alert is **suspicious and requires investigation**. Account compromise is not confirmed from the available evidence alone.

### Initial severity

The SIEM's initial priority is **High**. I would retain that priority pending review against the organization's severity matrix and escalation playbook. A final severity decision should consider evidence of unauthorized access, affected assets, post-login activity, business impact and confidence in the findings.

## 4. Triage and investigation plan

| Step | Action | Purpose |
|---|---|---|
| 1 | Preserve relevant authentication, MFA and VPN logs with timestamps and source details. | Maintain an evidence trail. |
| 2 | Review authentication events around the alert time and compare with the user's normal login patterns. | Establish whether the sequence is unusual. |
| 3 | Verify MFA event details, including timestamp, method and device/context where available, and ask whether the user recognizes the request. | Assess whether the approval matches legitimate activity. |
| 4 | Review VPN session metadata and post-login activity, including destinations, access to sensitive resources and subsequent alerts. | Determine whether suspicious actions followed login. |
| 5 | Check source-IP reputation and contextual intelligence. Treat geolocation and reputation as supporting context, not proof of identity. | Add context without over-relying on one indicator. |
| 6 | Follow the incident playbook for escalation and containment. Depending on risk and authorization, options may include revoking the active session, temporarily disabling the account or requiring a credential reset. | Reduce potential harm under approved procedures. |
| 7 | Record findings, actions, timestamps, decision rationale and unresolved questions. | Support handover and a defensible closure decision. |

## 5. Containment decision

My initial decision would be to **consider immediate containment** because multiple failed attempts were followed by a successful login and an established VPN session.

I would not treat account disablement as an automatic action in every case. I would follow the incident-response playbook and assess urgency, business impact, available evidence and my authorization. Where the risk warrants it, I would request or perform an approved action such as revoking active sessions or temporarily disabling the account.

Containment and investigation can proceed in parallel where the procedure allows. The goal is to reduce risk without destroying evidence or causing avoidable business disruption.

## 6. Zero Trust and user verification

The user reports that they were logging in and approved the MFA request. This statement is relevant, but it does not by itself resolve the alert.

Consistent with a Zero Trust mindset, I would verify the statement against independent evidence:

- Do the MFA timestamp and authentication sequence match the user's account?
- Does the VPN session context align with the user's expected activity?
- Is there anomalous access or activity after login?
- Are there corroborating logs or alerts?

Zero Trust does not mean assuming every user is malicious. It means not granting automatic trust based solely on a claim, identity or successful authentication; decisions should use context and evidence.

## 7. Preliminary MITRE ATT&CK mapping

The observed pattern may warrant considering **Brute Force (T1110)** as a candidate technique for investigation. This is a preliminary mapping, not a confirmed attribution. The supplied events do not establish which exact brute-force sub-technique occurred, whether an attacker was responsible, or whether credentials were compromised.

Further evidence is needed before finalizing a MITRE ATT&CK mapping.

## 8. Findings and limitations

### Current conclusion

**Status: Suspicious — investigation required.**

Repeated failed logins followed by successful authentication and a VPN session warrant further investigation and prompt handling under the incident-response playbook. The provided data is insufficient to confirm unauthorized access.

### Evidence gaps

- Whether the legitimate user approved the MFA request.
- Source-IP reputation and reliable contextual information.
- Whether the login pattern differs from the user's baseline.
- Which internal resources the VPN session accessed.
- Whether post-login actions, further alerts or signs of persistence were observed.
- The organization's severity criteria and containment authorization requirements.

### Closure criteria

Do not close the alert solely because the user says the login was legitimate. Closure should follow corroboration of the activity, review of relevant logs, assessment of potential impact, documentation and the applicable incident-response procedure. Escalate if suspicious activity remains unexplained or evidence of compromise emerges.

## 9. Sample incident note

**Summary:** Multiple failed authentication attempts for `a.smith` were followed by successful authentication and VPN session establishment from the same source IP.

**Assessment:** Potential credential attack or legitimate login failure; compromise not confirmed.

**Actions recommended:** Preserve and review authentication, MFA and VPN logs; validate the MFA approval with the user; investigate post-login activity; check contextual IP intelligence; follow the approved containment and escalation playbook.

**Current disposition:** Keep under investigation pending corroborating evidence.

## 10. Interview-ready explanation

> I would treat the alert as suspicious because several failed login attempts were followed by a successful login and an established VPN session from the same IP address. This may indicate a credential attack, but it does not prove account compromise. I would review the authentication, MFA and VPN logs, verify the activity with the user, and investigate what happened after login. In line with the incident-response playbook, I would consider proportionate containment, document my findings and escalate if the activity remains unexplained or evidence of compromise is found.

## 11. Learning outcomes

- Separate observable facts from hypotheses.
- Explain why a successful login following repeated failures warrants investigation.
- Verify MFA claims against independent log evidence.
- Assess containment choices without assuming one action fits every scenario.
- Document uncertainty, evidence gaps and escalation rationale.
- Use MITRE ATT&CK as an investigative framework without overstating attribution.

---

**Disclaimer:** This is a self-directed educational simulation using fictional log data. It is not evidence of professional incident-response work or hands-on experience with a production SIEM.
