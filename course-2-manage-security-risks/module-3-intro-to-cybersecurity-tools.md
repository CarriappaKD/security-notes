# Module 3: Introduction to Cybersecurity Tools

## Logs

**Logs** are records of events within an organization's systems and networks. Security analysts rely on log data and SIEM tools to identify and manage security threats.

| Log Type | What It Records |
|---|---|
| **Firewall logs** | Incoming and outgoing internet traffic |
| **Network logs** | Which devices are connecting and what they're communicating with |
| **Server logs** | Service-related events, such as logins |

## Security Information and Event Management (SIEM)

A **SIEM tool** collects and analyzes log data to monitor critical activity across an organization. It offers real-time monitoring/tracking of security event logs, provides visibility, event monitoring, analysis, and automated alerts — storing all log data in a centralized location. SIEM tools still require **human interaction** to analyze the security events they surface.

### Types of SIEM Tools

| Type | Description | Example |
|---|---|---|
| **Self-hosted** | Installed, operated, and maintained on the organization's own infrastructure — good for retaining physical control over confidential data | Splunk Enterprise |
| **Cloud-hosted** | Managed by a SIEM provider, accessed via the internet — good for orgs that don't want to invest in their own infrastructure | Splunk Cloud |
| **Cloud-native** | Built to fully leverage cloud computing (availability, flexibility, scalability) | Google Chronicle |
| **Hybrid** | Combines self-hosted and cloud-hosted approaches — cloud flexibility while keeping physical control over sensitive data | — |

### Automation and SOAR

Automation helps security teams respond faster to incidents by performing many actions without waiting for a human response.

> **SOAR** (Security Orchestration, Automation, and Response) — a collection of applications, tools, and workflows that uses automation to respond to security events.

### SIEM Dashboards by Audience

SIEM dashboards present information in an easy-to-digest format, customized to what each stakeholder actually needs:

| Audience | Needs | Dashboard Includes |
|---|---|---|
| **Security Analyst** | Detailed, real-time operational data to detect/investigate/respond to threats | Real-time alerts, traffic anomalies, failed login attempts, vulnerability status, geographic source of attacks |
| **IT Manager** | Overview of system health, compliance status, and resource utilization | System uptime/availability, patch compliance, resource utilization, compliance reports |
| **Executive (e.g., CISO)** | High-level strategic overview of security posture, risk exposure, and ROI on security investments | Overall risk score, number of critical incidents, cost of incidents, security budget vs. actual spend, KPIs |

## Open-Source vs. Proprietary Tools

### Open-Source Tools
Often free to use, user-friendly, and highly customizable — leading to many different services being built from the same underlying software. (Common misconception: open-source tools are less effective or less safe than proprietary ones — not necessarily true.)

| Tool | Description |
|---|---|
| **Linux** | Widely used open-source OS; can be tailored to specific needs via the command line |
| **Suricata** | Open-source network analysis and threat detection software — inspects network traffic for suspicious behavior, generates logs, and detects activity across users/computers/IP addresses to uncover potential threats |

### Proprietary Tools
Developed and owned by a company; users typically pay for usage and training.

**Splunk** — offers Splunk Enterprise and Splunk Cloud, both reviewable via dashboards:
- Security posture dashboard
- Executive summary dashboard
- Incident review dashboard
- Risk analysis dashboard

**Chronicle (Google)** — a cloud-native SIEM tool that retains, analyzes, and searches log data to identify threats/risks/vulnerabilities. Allows collecting/analyzing log data by asset, domain name, user, or IP address. Dashboards include:
- Enterprise insights dashboard
- Data ingestion and health dashboard
- IOC (Indicators of Compromise) matches dashboard
- Main dashboard
- Rule detections dashboard
- User sign-in overview dashboard

## Questions / Things to Revisit

- 

---
*Notes based on Google Cybersecurity Professional Certificate, Course 2 — Play It Safe: Manage Security Risks*
