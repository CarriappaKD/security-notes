# Module 2: Escalate Incidents

## Incident Escalation

**Security incident escalation** is the process of identifying a potential security incident and passing it to a more experienced team or team member. As an analyst, you're expected to recognize potential issues — for example, an employee repeatedly entering the wrong credentials on their account — and report them to the right person.

### Breach Notification Laws

Many countries have **breach notification laws** requiring companies and government entities to notify individuals when a security breach involves their **PII** (e.g., Social Security or driver's license numbers, medical records, addresses, and other sensitive customer information). Analysts should know the laws that apply where their company operates, and keep up with them, since they're updated regularly.

### Low-Level Security Issues

**Low-level issues** are security risks that don't result in PII exposure. Examples:

- An employee having a single failed login attempt
- An employee downloading unapproved software onto a work laptop

They aren't significant on their own, but they still need to be investigated in case they should be escalated:

| Situation | Likely Concern | Possible Explanation |
|---|---|---|
| Password typed wrong 2–3 times | Low | Typo or forgotten password |
| Password typed wrong 15 times in 30 minutes | Escalate | A malicious actor attempting to compromise the account |
| Unapproved game or software downloaded | Investigate | May be infected with malware — which can cause financial loss and reputational damage |

### The Escalation Process

Every company has its own protocols, including its own **escalation policy**. A policy typically specifies:

- Who should be notified when a security alert comes in
- Who to contact if the first responder is unavailable
- *How* to escalate — through the IT desk, an incident management tool, or direct communication between team members

### Essential Skills and Organizational Roles

| Skill | Why It Matters |
|---|---|
| **Attention to detail** | Lets you quickly spot anomalies or suspicious activity across networks and systems |
| **Following escalation guidelines** | Ensures the issue reaches the correct person or team through established procedures |

Larger security operations involve coordination across departments — including the **CISO**, engineering, legal, and public relations. Entry-level analysts are the first step in incident response, making sure the broader team is alerted so assets and data stay protected.

## Incident Classification Types

| Type | What It Is | Why Escalate |
|---|---|---|
| **Malware infection** | Malicious software infiltrates systems or networks — from simpler phishing attacks to complex ransomware that locks access to critical data | Can cause network slowdowns or sensitive data exposure; timely escalation protects the organization |
| **Unauthorized access** | Someone gains physical or digital access to an application or system without permission, often via methods like brute force attacks | Escalate **every** occurrence; urgency depends on how critical the affected system is to the business |
| **Improper usage** | An employee violates acceptable use policies — e.g., using software licenses for personal reasons or viewing coworkers' data | Hard to tell intentional from accidental, so always escalate to a supervisor |

## Who Gets Notified: Roles in Escalation

| Role | Responsibility | Escalate to them when… |
|---|---|---|
| **Data owner** | Decides who can access, edit, use, or destroy their information; has administrative control over specific information, hardware, or software; accountable for classification, protection, access, and use of company data | An employee gains unauthorized access to software they don't need for work — escalate to that software's data owner |
| **Data controller** | Determines the procedure and purpose for processing data, mostly personal information collected from customers; ensures data is used, stored, and processed in line with security/privacy regulations | Sensitive customer information is at risk |
| **Data processor** | Reports to the data controller and processes data on its behalf; typically a vendor, often tasked with installing security measures | There's a data-processing issue — escalated to whoever oversees the third-party organization doing the processing |
| **Data custodian** | Grants and removes access to software/hardware; implements security controls, creates policies for how data is stored and transmitted, advises on threats, and monitors the data | Security controls need strengthening or have been compromised |
| **Data protection officer (DPO)** | Monitors internal compliance with data protection procedures; advises the security team on obligations under data protection standards; assesses whether security measures actually protect the data | Set standards or protocols have been violated |

## Consequences of Unescalated Incidents

Small anomalies — like suspicious log activity in a banned application — can grow into severe data breaches and operational shutdowns if ignored. Halting critical operations (e.g., manufacturing) means significant financial losses and wasted operational time.

When the full scope of damage is unclear, an incident can initially be escalated with **medium criticality**, then adjusted up or down by an experienced incident handler once they've evaluated the findings.

### Determining Urgency Based on Assets

- Urgency tracks the **value and sensitivity of the affected asset** — e.g., databases containing PII or core manufacturing systems
- Repeated failed logins from a forgotten password are generally low urgency; unauthorized access to critical infrastructure needs immediate, high-priority escalation

> Example: unauthorized access to a manufacturing application takes priority over malware on a legacy system that doesn't affect business operations.

### Escalation Policies Vary by Organization

- Each organization sets its own policy on who to notify and how to manage alerts — there is **no universal industry standard**
- Unexpected situations come up (e.g., a supervisor is out of office), so alternative reporting paths matter
- You don't need to memorize the entire policy, but you should **bookmark or save it** on your work device for quick access
- Policies can be long, and small details can decide whether an incident reaches the right people — so attention to detail matters

## Your Decisions Matter

Analysts make daily decisions about which events to escalate **before** they become major incidents.

- **Trust your instincts and ask questions.** The team relies on your confidence; learn the escalation policy so you can decide with confidence, and ask when unsure — it shows commitment to doing the job right
- **Not all events are equal.** Learn which assets and data matter most to your organization through onboarding materials, your supervisor, and the company's security policies. Identifying the incident type (malware, unauthorized access, improper usage) helps you prioritize and escalate quickly. Incidents affecting assets essential to business operations take priority over those that don't

### Quick Escalation Tips

1. Familiarize yourself with your organization's escalation policy
2. Follow the policy at all times
3. Ask questions

## Questions / Things to Revisit

-

---
*Notes based on Google Cybersecurity Professional Certificate, Course 8 — Put It to Work: Prepare for Cybersecurity Jobs*
