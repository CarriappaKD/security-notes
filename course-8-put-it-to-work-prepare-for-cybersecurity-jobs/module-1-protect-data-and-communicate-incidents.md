# Module 1: Protect Data and Communicate Incidents

## Security as a Mindset

Security isn't only a set of tools — it's a way of thinking that shapes how an analyst approaches every task:

- Evaluating risks, spotting potential or actual breaches, and knowing both **what assets you're defending** and **who you're defending against**
- A proactive level of scrutiny, where even a routine action like a mouse click is treated as a potential security risk
- Staying current on emerging threats, vulnerabilities, and social engineering tactics (like phishing), which in turn inspires new protection strategies
- Protecting everything from low-level assets (e.g., guest Wi-Fi) to critical ones (PII, financial records, intellectual property)

## Classifying Data for Safety

Classifying data types helps security professionals protect an organization from attacks that would hurt business operations.

| Classification | Description | Risk if Exposed | Examples |
|---|---|---|---|
| **Public** | Already accessible to the public; still needs basic protection | Minimal | Press releases, job descriptions, marketing materials |
| **Private** | Information that should be kept from the public; higher security level | Serious | Company email addresses, employee ID numbers, research data |
| **Sensitive** | Must be protected from everyone without authorized access; includes **PII**, **SPII**, and **PHI** | Significant damage to finances and reputation | Bank account numbers, usernames/passwords, Social Security numbers, passport numbers, medical information |
| **Confidential** | Important to ongoing business operations; access is often limited, sometimes requiring a signed **NDA** (non-disclosure agreement — a legal contract binding parties to protect information) | Severe | Trade secrets, financial records, sensitive government data |

## Asset Classification

**Asset classification** means labeling assets by their sensitivity and importance to the organization, ranging from low-level to high-level:

| Level | Asset Type | Why |
|---|---|---|
| **Low** | Public data | Readily available; little impact if compromised |
| **High** | Sensitive and confidential data | A leak can cost the company its competitive edge, reputation, and customer trust |

> Example: a company's website address is a low-level asset; an internal email discussing trade secrets is a high-level asset.

## Detect and Protect Without Neglect

Compromised assets can lead to severe financial losses, regulatory fines, and lost customer credibility — so protecting sensitive information like PII and credentials is essential. Security also depends on collaboration across stakeholders, since the assets being defended affect employees, third-party vendors, and customer trust.

### Events vs. Incidents

- A security **event** that results in a data breach is an **incident**; an event that's safely resolved without a breach is not
- Knowing the difference supports a proactive mindset built on continuous care and attention to detail when handling sensitive data

### Reporting and Escalation

- Report both **minor concerns** (e.g., an unapproved app installation) and **major threats** (e.g., malicious code execution showing up in logs)
- Because impact is hard to predict, err on the side of caution — no issue is too small or too large to escalate to a supervisor

## Identify and Protect: The Four-Part Process

Most security teams follow a four-part process, with continuity and recovery planning as the last step:

| Step | Action |
|---|---|
| **1. Identify** | Determine which assets in the organization need protecting |
| **2. Assess threats** | Determine what threats could negatively affect those assets |
| **3. Detect** | Implement tools and processes to detect potential threats to the assets |
| **4. Plan for recovery** | IT or the appropriate business function creates the **business continuity plan** and **disaster recovery plan**, developed together to reduce the impact of an incident |

## Business Continuity Plan (BCP)

Successful attacks can mean lost profits and lost customers. A **business continuity plan** is a document outlining the procedures to **sustain business operations during and after a significant disruption**. It's created alongside a disaster recovery plan.

### Four Essential Steps

1. **Conduct a business impact analysis** — assess the possible effects a disruption of business functions could have on the organization
2. **Identify, document, and implement recovery steps** for critical business functions and processes — giving the team actionable steps for responding to a security event
3. **Organize a business continuity team** — people from across the organization (typically cybersecurity, IT, HR, communications, and operations) who execute the plan when needed
4. **Train the business continuity team** — walk through different risk scenarios so they're prepared for security threats

## Disaster Recovery Plan (DRP)

A **disaster recovery plan** outlines the steps the security team takes to **minimize the impact of a security incident and resolve the threat** — for example, a ransomware attack that stops the manufacturing team from retrieving certain data. It's typically created alongside the BCP.

Steps should include:

- Implementing recovery strategies to **restore software**
- Implementing recovery strategies to **restore hardware functionality**
- **Identifying applications and data** that might be affected after an incident

### BCP vs. DRP at a Glance

| | Business Continuity Plan | Disaster Recovery Plan |
|---|---|---|
| **Focus** | Keeping business operations running during and after a disruption | Restoring systems, software, hardware, and data after an incident |
| **Typical team** | Cybersecurity, IT, HR, communications, operations | Security/IT team |

## Questions / Things to Revisit

-

---
*Notes based on Google Cybersecurity Professional Certificate, Course 8 — Put It to Work: Prepare for Cybersecurity Jobs*
