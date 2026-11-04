# Module 3: Incident Investigation and Response

## Detection and Analysis Phase (Revisited)

| Phase | Focus |
|---|---|
| **Detection** | Promptly discovering security events. Not all events are incidents, but all incidents are events |
| **Analysis** | Investigating and validating alerts — examining indicators of compromise (IoCs) to determine whether an incident actually occurred |

### Challenges

- It's impossible to detect everything — even advanced tools have limitations and may not be fully deployed across an organization
- High alert volume is common, often from misconfigurations generating false positives — though some of that volume is genuinely malicious activity

## Cybersecurity Incident Detection Methods

Detection tools only catch what they're configured to monitor. Teams need additional detection methods for broader coverage.

### Threat Hunting

The **proactive** search for threats on a network — combining human judgment with technology to catch what automated tools miss, do deeper analysis on existing detections, and ideally catch threats before damage occurs. **Threat hunters** research emerging attacks, assess an organization's vulnerability to them, and search using a mix of threat intelligence, IoCs, indicators of attack (IoAs), and machine learning.

### Threat Intelligence

Evidence-based information providing context about existing/emerging threats, drawn from:
- **Industry reports** — detail attacker tactics, techniques, procedures (TTPs)
- **Government advisories** — same, from government sources
- **Threat data feeds** — streams of indicators (IPs, domains, file hashes), useful against sophisticated actors like APTs

A **threat intelligence platform (TIP)** centralizes and analyzes this intelligence from multiple sources, helping prioritize relevant threats.

### Cyber Deception

Deliberately deceiving attackers to improve detection and defense. **Honeypots** are a key example — decoy systems/resources designed to look vulnerable and attractive (e.g., a fake file named "Client Credit Card Information - 2022"). When an attacker takes the bait, security teams are alerted.

## Ongoing Monitoring of CI/CD Pipelines

A compromised CI/CD pipeline lets attackers inject code, steal data, or break software — so continuous, automated anomaly detection is essential to catch IoCs before serious damage.

### Common CI/CD IoCs

| Category | Examples |
|---|---|
| **Unauthorized code changes** | Changes from the wrong people, at odd hours, from unexpected locations, or with suspicious content (large deletions, confusing code) |
| **Suspicious deployment patterns** | Deployments to unapproved systems, at unusual times/frequency, or triggered by unexpected accounts |
| **Compromised dependencies** | Known CVEs found in dependencies; unexpected new dependencies; downloads from untrusted sources |
| **Unusual pipeline execution** | Normally stable steps suddenly failing; runs taking much longer; step order changing without approval |
| **Secrets exposure attempts** | Logs showing attempts to reach secrets from unapproved locations; hardcoded secrets found in commits |

### Why Monitor for These

- **Faster incident response** — catching IoCs early stops attackers before they reach their goal
- **Limits damage** — shorter attacker dwell time in the pipeline
- **Improves future defenses** — each incident teaches the team more about how attackers target the pipeline

### Tools and Techniques

| Method | What it Covers |
|---|---|
| **Logging and auditing** | Pipeline execution logs (automated baselining flags deviations in duration/step order/error rates), code commit logs, access logs, deployment logs |
| **SIEM integration** | Feeding CI/CD logs into a SIEM for ML-driven anomaly detection and rule-based alerts (e.g., known malicious file hashes in builds, C2 server connections, unauthorized secret access attempts) |
| **Real-time alerting** | Notifications for unusual build failures, anomalous code changes, secrets-exposure attempts, suspicious outbound network traffic |
| **Performance monitoring** | Slowdowns or resource exhaustion (**indicators of attack**, or IoAs) can prompt deeper investigation that uncovers IoCs |
| **Continuous vulnerability scanning** | Regularly checking CI/CD tools/plugins/containers for CVEs — unpatched weaknesses are themselves potential IoCs |

## Indicators of Compromise (IoCs) vs. Indicators of Attack (IoAs)

| | Focus | Answers |
|---|---|---|
| **IoC** | Observable evidence tied to an attack (e.g., a malware-associated filename) | The *who/what* — after the fact |
| **IoA** | A series of observed events indicating a real-time incident, focused on attacker behavior/intent | The *why/how* — during an ongoing/unknown attack |

> Example: a process making a network connection is an IoA; the process's filename and the IP it contacted are the related IoCs.

> Note: an IoC isn't automatic confirmation of an incident — it can also result from human error or system malfunction.

### The Pyramid of Pain

Maps IoC types to how much difficulty ("pain") blocking that indicator causes an attacker — the higher up the pyramid, the harder it is for the attacker to adapt.

| Level (low → high pain) | Indicator Type | Example |
|---|---|---|
| 1 | **Hash values** | A hash uniquely identifying a known malicious file |
| 2 | **IP addresses** | e.g., 192.168.1.1 |
| 3 | **Domain names** | e.g., www.google.com |
| 4 | **Network artifacts** | Evidence in network protocols, e.g., a User-Agent string |
| 5 | **Host artifacts** | Evidence on a host, e.g., a file created by malware |
| 6 | **Tools** | Software the attacker used, e.g., John the Ripper for password cracking |
| 7 | **Tactics, techniques, and procedures (TTPs)** | The attacker's actual behavior — hardest to detect and to change, since it's tied to how they operate, not a disposable artifact |

## Adding Context to Investigations

**Threat intelligence** helps analysts expand a single IoC into a fuller picture — e.g., linking a suspicious IP to related artifacts like unusual processes or other network communications — enabling faster detection and a more informed response.

### Crowdsourcing

**Crowdsourcing** pools threat intelligence from the global cybersecurity community (vendors, government agencies, cloud providers, researchers), so defenders aren't each rediscovering the same attack independently.

- **ISACs** (Information Sharing and Analysis Centers) — share sector-specific threat intelligence (energy, healthcare, etc.)
- **OSINT** — collecting/analyzing publicly available information to generate intelligence about threat actors, threats, and vulnerabilities

### Investigative Tools for IoCs

| Tool | Purpose |
|---|---|
| **VirusTotal** | Analyzes files/domains/URLs/IPs for malicious content; reports include Detection (vendor verdicts), Details (static analysis), Relations (connected IoCs), Behavior (sandboxed execution activity), Community (analyst comments), and a vendors'-ratio + community score |
| **Jotti's malware scan** | Free multi-antivirus file scanning (limited submissions) |
| **Urlscan.io** | Scans and reports on URLs |
| **MalwareBazaar** | Free repository of malware samples for research/threat intelligence |

## Documentation

Documentation supports investigations, task completion, and communicating findings. Three key benefits:

| Benefit | What it Provides |
|---|---|
| **Transparency** | Supports compliance, insurance requirements, legal proceedings. **Chain of custody** (tracking evidence possession/control) is a prime example of documentation creating an audit trail |
| **Standardization** | Repeatable processes aid continuous improvement, knowledge transfer, and onboarding — e.g., an incident response plan standardizes how every incident is handled |
| **Clarity** | Helps the audience act quickly — e.g., documenting *why* an alert was escalated or closed |

**Guidelines:**
- **Know your audience** — a SOC manager and a CEO need very different levels of technical detail
- **Be concise** — establish the purpose immediately (e.g., an executive summary up front)
- **Update regularly** — review/update documentation as the threat landscape evolves, especially after resolving an incident

## Chain of Custody

Tracking and documenting evidence possession/control to preserve its integrity and legal admissibility throughout an incident.

- Chain of custody forms start the moment evidence is collected — recording who handled it, when, where, and why it was transferred
- Securing digital evidence involves **write-protecting** the media and calculating a **cryptographic hash** to detect future tampering
- **Log form components:** evidence description (storage location, hostname, MAC/IP address) + custody log (who transferred/received it, purpose, timestamps)
- A **broken chain of custody** (inconsistencies, missing entries) undermines evidence reliability; an unbroken chain is what makes evidence usable in legal proceedings

## Incident Response Playbooks

Structured, step-by-step guidance for handling specific incident types quickly and consistently.

Purpose: reduces guesswork/uncertainty during high-stress incidents; outlines specific procedures per threat type (ransomware, data breach, malware, DDoS, etc.).

| Type | Description |
|---|---|
| **Non-automated** | Analysts manually follow each step (e.g., a flowchart to identify IoCs, collect logs, analyze evidence) |
| **Automated / semi-automated** | Uses SIEM/SOAR tooling to handle repetitive tasks, boosting productivity and cutting resolution time |

Playbooks must be regularly reviewed/updated — the post-incident activity phase is the natural point to apply lessons learned back into them.

## The Triage Process

**Triage** prioritizes incidents by importance/urgency, so critical issues get resources first.

### Three Steps

1. **Receive and assess** — review the alert for validity:
   - Is it a false positive?
   - Has it occurred before, and how was it resolved?
   - Is it tied to a known vulnerability?
   - What's its severity?
2. **Assign priority** — based on:
   - **Functional impact** — effect on the affected system's business functionality
   - **Information impact** — effect on confidentiality/integrity/availability of data, including third-party data
   - **Recoverability** — whether (and how worthwhile) recovery actually is, given the size/scope and available resources
3. **Collect and analyze** — gather evidence, research externally, document the process; escalate to Tier 2/management if severity warrants

### Benefits of Triage

- **Resource management** — focuses effort on urgent threats, reduces time on low-priority tasks
- **Standardized approach** — playbooks/documentation ensure alerts move through a consistent, validated process

## Containment, Eradication, and Recovery (Revisited)

| Phase | Focus | Example Actions |
|---|---|---|
| **Containment** | Limit/prevent further damage | Isolate affected devices, e.g., disconnecting a malware-infected machine from the network |
| **Eradication** | Fully remove all traces of the incident | Run vulnerability tests, patch identified weaknesses |
| **Recovery** | Safely restore systems/operations to normal | Reimage systems, reset passwords, update firewall configurations |

## Business Continuity Planning

Minimizes the operational impact of an incident — prolonged disruption can cause serious legal, financial, and reputational damage.

A **business continuity plan (BCP)** outlines how to sustain operations during/after a major disruption, so critical functions can resume or be quickly restored.

> Note: a BCP ≠ a **disaster recovery plan**. Disaster recovery plans specifically address recovering information systems after a major disaster (hardware failure, natural disaster, etc.).

### Site Resilience (a Recovery Strategy)

**Resilience** is the ability to prepare for, respond to, and recover from disruptions. **Site resilience** ensures continued availability of networks/data centers/infrastructure during a disruption, via three types of recovery sites:

| Site Type | Readiness |
|---|---|
| **Hot site** | A fully operational duplicate environment — can activate immediately |
| **Warm site** | Fully updated/configured but not immediately live — can be made operational quickly |
| **Cold site** | Has some necessary infrastructure, but needs additional work before it's usable |

## Post-Incident Activity

The final NIST lifecycle phase — reviewing the incident to find areas for improvement.

### Lessons Learned Meeting (Post-Mortem)

Held with all involved parties, **no later than two weeks** after remediation. Purpose: evaluate the response, identify improvements — *not* to assign blame.

**Typical questions covered:**
- What happened? When? Who discovered it?
- How was it contained? What recovery actions were taken?
- What could have been done differently?

### Recommendations

The meeting should produce a prioritized list of actionable improvements — e.g., updating playbook steps or adopting new security tools — so the same incident doesn't recur.

### Final Report

A comprehensive, non-standardized document (format varies by organization), commonly including:

| Section | Content |
|---|---|
| **Executive summary** | High-level key findings and facts |
| **Timeline** | Chronological, timestamped sequence of events |
| **Investigation** | Actions taken during detection/analysis (e.g., findings from a packet capture) |
| **Recommendations** | Suggested actions for future prevention |

> Write with the audience in mind — final reports are often read by business executives without deep technical background, so clarity matters more than technical completeness.

## Questions / Things to Revisit

- 

---
*Notes based on Google Cybersecurity Professional Certificate, Course 6 — Sound the Alarm: Detection and Response*
