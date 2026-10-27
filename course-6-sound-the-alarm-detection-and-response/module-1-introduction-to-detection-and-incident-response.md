# Module 1: Introduction to Detection and Incident Response

## Security Incidents

An **incident** is an occurrence that jeopardizes the confidentiality, integrity, or availability of information/systems, or violates security policy. All incidents are **events** (observable occurrences), but not all events rise to the level of an incident.

When investigating, analysts look for the **five W's**: who triggered it, what happened, when, where, and why.

## The NIST Incident Response Lifecycle

A four-phase, **cyclical** framework — steps can overlap as new information emerges.

Example scenario used throughout: a **vishing** attack.

| Phase | Purpose | Example Actions |
|---|---|---|
| **1. Preparation** | Planning and training | Set up uniform email conventions; build a culture where employees feel comfortable asking questions; provide quarterly security training |
| **2. Detection and Analysis** | Detect and assess | Identify signs of an incident; filter external emails flagging suspicious attachments (e.g., voicemail files); keep an incident response plan on hand |
| **3. Containment, Eradication, and Recovery** | Minimize and mitigate | Confirm the sender's origin for a suspicious message; give employees an easy way to report/contain suspicious messages |
| **4. Post-Incident Activity** | Learn | Update the playbook with new red flags; review and adjust permission oversight |

## Computer Security Incident Response Teams (CSIRTs)

**CSIRTs** are specialized groups trained in incident management and response. Goals: manage incidents effectively, provide response/recovery resources, and prevent future incidents. They collaborate with legal and PR teams for regulatory compliance and public disclosure.

Effective response depends on clear:
- **Command** — leadership and direction overseeing the response
- **Control** — managing technical aspects (coordinating resources, assigning tasks)
- **Communication** — keeping stakeholders informed

### Roles in a CSIRT

| Role | Responsibility |
|---|---|
| **Security analyst** | Continuously monitors the environment — triages alerts, performs root-cause investigations, escalates or resolves. Escalates critical threats to the technical lead |
| **Technical lead** | Owns the technical response — determines root cause, builds/implements containment/eradication/recovery strategies, aligns priorities with the business (e.g., minimizing customer disruption) |
| **Incident coordinator** | Coordinates with non-security departments during an incident, keeping communication open across personnel. Also called incident commander/manager; can exist in other teams too (e.g., SOC) |

## Security Operations Center (SOC)

A **SOC** ("sock") is an organizational unit dedicated to monitoring networks, systems, and devices for threats — often its own unit, or embedded within a CSIRT. SOC work is a form of **blue team** activity (defending against threats, as opposed to red team attack-simulation work).

### SOC Analyst Tiers

| Tier | Role | Responsibilities |
|---|---|---|
| **Tier 1 (L1)** | Least experienced | Monitor/review/prioritize alerts by severity; create and close tickets; escalate to Tier 2/3 |
| **Tier 2 (L2)** | More experienced | Receives escalated tickets; conducts deeper investigations; configures/refines security tools; reports to SOC lead |
| **Tier 3 (L3) / SOC lead** | Highly experienced | Manages team operations; performs advanced detection (malware/forensics analysis); reports to SOC manager |
| **SOC manager** | Top of the pyramid | Hires/trains/evaluates the team; sets performance metrics; builds incident/compliance/audit reports; communicates with executives |

**Other specialized SOC roles:**
- **Forensic investigators** (usually L2/L3) — collect, preserve, and analyze digital evidence from incidents
- **Threat hunters** (usually L3) — proactively detect, analyze, and defend against new/advanced threats using threat intelligence

## Incident Response Plans

Organizations need a formal, fast-response plan — regulations often require reporting incidents within specific timeframes.

### Key Elements

| Element | Includes |
|---|---|
| **Incident response procedures** | Step-by-step instructions for various incident types |
| **System information** | Network/data flow diagrams, logging details, asset inventory |
| **Supporting documents** | Contact lists, forms, templates |

Plans must be **regularly reviewed and tested** through exercises like tabletop simulations — this catches gaps, builds team familiarity, and ensures regulatory compliance.

## Incident Response Tools

Analysts rely on a diverse toolkit for detection, management, documentation, and investigation — and continuous learning to keep up with evolving threats.

### Documentation Tools

**Documentation** is any recorded content (audio, digital, handwritten, video) used for a specific purpose. There's no single industry standard — organizations build their own practices. Good documentation reduces confusion during high-tension incidents.

| Type | Examples |
|---|---|
| Common documents | Playbooks, incident handler's journal, policies, plans, final reports |
| Tools | Word processors (Google Docs, OneNote, Evernote, Notepad++), ticketing systems (Jira), spreadsheets, audio recorders, cameras, handwritten notes |

### Detection Tools

Detection tools continuously monitor networks/systems for suspicious activity and trigger alerts for investigation.

| Tool | What it Does | Examples |
|---|---|---|
| **IDS** (Intrusion Detection System) | Monitors and **alerts** on possible intrusions — does *not* stop the activity itself; a human investigates and acts | Zeek, Suricata, Snort®, Sagan |
| **IPS** (Intrusion Prevention System) | Monitors *and* actively **takes action** to stop intrusions | Suricata, Snort, Sagan (many tools serve as both IDS and IPS) |
| **EDR** (Endpoint Detection and Response) | Installed on endpoints (any networked device); monitors/records/analyzes endpoint activity using **behavioral analysis** (ML/AI-driven) to spot threat patterns, and can automate a response | Open EDR®, Bitdefender™ EDR, FortiEDR™ |

### Detection Categories (for evaluating IDS alerts)

| Category | Meaning |
|---|---|
| **True positive** | Alert correctly detects a real attack |
| **True negative** | No malicious activity exists, and no alert is triggered |
| **False positive** | Alert incorrectly flags something as malicious — wastes investigation time |
| **False negative** | A real attack occurs but goes undetected — the most dangerous outcome, since the team remains unaware |

### Management Tools: SIEM

A **SIEM** (Security Information and Event Management) tool collects and analyzes log data to monitor critical activity across an organization, supporting **log analysis** (examining logs for events of interest).

**Advantages:**
- **Access to event data** — ingests data from potentially hundreds of connected systems/devices, including real-time activity
- **Monitoring, detecting, alerting** — applies detection rules continuously; matches trigger alerts
- **Log storage** — acts as a retention system for historical data, kept/deleted per organizational policy

### The SIEM Process (3 Steps)

1. **Collect and aggregate data** — pulls logs (event details: timestamps, IPs, etc.) from sources like firewalls, servers, routers, and consolidates them into one central location, removing the need to check each source manually.
   - **Parsing** often happens here — mapping raw log data into labeled fields/values for readability.
     - Raw: `April 3 11:01:21 server sshd[1088]: Failed password for user nuhara from 218.124.14.105 port 5023`
     - Parsed: `host=server`, `process=sshd`, `source_user=nuhara`, `source_ip=218.124.14.105`, `source_port=5023`
2. **Normalize data** — converts differently-formatted logs (e.g., firewall vs. server logs) into one standard, structured, easily searchable format.
3. **Analyze data** — applies detection logic (rules/conditions) to the normalized data; matches trigger alerts.
   - **Correlation** — comparing multiple log events together to spot patterns that indicate a potential threat.

### Common SIEM Tools

AlienVault® OSSIM™, Chronicle, Elastic, Exabeam, IBM QRadar® Security Intelligence Platform, LogRhythm, Splunk

## Questions / Things to Revisit

- 

---
*Notes based on Google Cybersecurity Professional Certificate, Course 6 — Sound the Alarm: Detection and Response*
