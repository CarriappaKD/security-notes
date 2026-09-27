# Module 4: Use Playbooks to Respond to Incidents

## What Is a Playbook?

A **playbook** is a detailed manual outlining operational actions and specifying tools for responding to security incidents. Playbooks ensure **urgency, efficiency, and accuracy** when mitigating threats and reducing risk.

> Playbooks are **living documents** — security teams update them frequently to keep pace with industry changes and new threats.

## The Six Phases of an Incident Response Playbook

Example scenario used throughout: a company's website suddenly becomes inaccessible.

| Phase | Purpose | Example |
|---|---|---|
| **1. Preparation** | Documenting procedures, establishing staffing plans, and educating users to reduce the likelihood/risk/impact of an incident | The plan outlines who's on the security team, their roles (investigator, communicator, etc.), and which tools they'll use |
| **2. Detection and Analysis** | Identifying and analyzing events using defined processes/technology to determine if a breach occurred and its scale | A SIEM alert flags unusual traffic patterns; analysis confirms the site is under a **DDoS attack** |
| **3. Containment** | Preventing further damage and reducing the incident's immediate impact | Team reroutes traffic through a scrubbing service or blocks known malicious IPs to stop further damage |
| **4. Eradication and Recovery** | Fully removing incident artifacts and restoring the affected environment to a secure state | Team works with the ISP to block the attack at a higher level, then verifies the site is fully functional and secure |
| **5. Post-Incident Activity** | Documenting the incident, informing leadership, and applying lessons learned | Team documents what happened, how they responded, and what they learned; informs leadership and discusses improvements (e.g., stronger DDoS protection) |
| **6. Coordination** | Reporting the incident and sharing information throughout the response, per organizational standards | Team coordinates with internal departments (e.g., customer support) and external partners (e.g., ISP) to keep the response unified |

> Playbook tools, methodologies, protocols, and procedures differ by organization — and the individuals involved at each step can vary depending on the organization and country.

## Incident and Vulnerability Response Playbooks

The most common type of playbook used by entry-level cybersecurity professionals. They're built around the goals defined in an organization's **business continuity plan**, and they help:
- Minimize errors during response
- Ensure critical actions happen within a defined timeframe
- Prevent mishandling of data that could compromise forensic evidence (making it unusable later)

**Common steps included:**
- Preparation
- Detection
- Analysis
- Containment
- Eradication
- Recovery

## Playbooks + SIEM / SOAR

Playbooks are used alongside both SIEM and SOAR tools, but in different ways:

- **Playbooks + SIEM** — if a SIEM tool flags unusual user behavior, the playbook tells the analyst exactly how to respond to it.
- **Playbooks + SOAR** — SOAR tools can act automatically (e.g., locking an account after too many failed login attempts), and the playbook then guides the analyst's follow-up steps to resolve the underlying issue.

## Questions / Things to Revisit

- 

---
*Notes based on Google Cybersecurity Professional Certificate, Course 2 — Play It Safe: Manage Security Risks*
