# Module 1: Introduction to Asset Security

## Why Planning Matters in Security

Planning is central to security work — it's how organizations get ahead of uncertainty instead of just reacting to problems. Security teams analyze **risk** so they can plan proactively, and their core focus is protecting the **CIA triad**: the confidentiality, integrity, and availability of an organization's assets.

## Assets, Threats, and Vulnerabilities

| Term | Definition |
|---|---|
| **Asset** | Anything of value to an organization — buildings, equipment, data, people — that needs protection based on its value and risk exposure |
| **Threat** | A circumstance or event that could negatively impact an asset — from a malicious actor to an accident or natural event |
| **Vulnerability** | A weakness in an asset that a threat could exploit (e.g., a weak lock, outdated software) |
| **Risk** | Anything that can impact an asset's confidentiality, integrity, or availability |

## Security Risk

How an organization defines risk varies, but one common way to express it:

```
Likelihood × Impact = Risk
```

Calculating risk helps organizations:
- Prevent costly, disruptive events
- Identify where systems/processes need improvement
- Decide which risks are tolerable
- Prioritize which critical assets need the most attention

A **risk register** is a central record of an organization's potential risks to its assets, systems, and data — commonly used during a risk assessment.

## Risk Factors: Threats and Vulnerabilities

Whether an asset actually gets harmed depends on whether a **threat** successfully exploits a **vulnerability**.

**Threat categories:**
| Type | Example |
|---|---|
| **Intentional** | A hacker exploiting a misconfigured application |
| **Unintentional** | An employee holding the door open for someone unknown, unintentionally granting access |

**Vulnerability categories:**
| Type | Example |
|---|---|
| **Technical** | Misconfigured software exposing data to unauthorized access |
| **Human** | An employee losing their access card |

## Asset Management

**Asset management** is the ongoing process of tracking an organization's assets and the risks affecting them — it's the foundation every security plan is built on. An **asset inventory** (a full catalog of assets) keeps an organization from losing track of what it owns and helps it allocate protection resources effectively.

Common categories of assets:
- **Digital** — customer data, financial records
- **Information systems** — networks, software
- **Physical** — facilities, equipment, supplies
- **Intangible** — brand reputation, intellectual property

### Asset Classification

**Asset classification** labels assets by sensitivity and importance — similar to how a person might prioritize which of their own belongings matter most. It requires knowing:
- What you have
- Where it is
- Who owns it
- How important it is

Classification helps prioritize security resources, control IT costs, and stay compliant with regulations.

**Common classification levels (highest to lowest):**

| Level | Meaning |
|---|---|
| **Restricted** | Highest sensitivity — need-to-know information only |
| **Confidential** | Disclosure could significantly harm the organization |
| **Internal-only** | Available to employees and business partners |
| **Public** | Lowest level — no negative impact if released |

**Challenges of classifying information:**
1. Identifying ownership is straightforward for a physical asset, like a building — but much trickier for assets like information.
2. Information can also hold multiple classification values at the same time.

Asset management is a **continuous process** — it's how organizations catch unexpected security gaps and maintain a strong security posture over time, not a one-time task.

## Assets in a Digital World

**Data** is digital information translated, processed, or stored by a computer. Weak information security around data can lead to identity theft, financial loss, and reputational damage.

### The Three States of Data

| State | Meaning | Example |
|---|---|---|
| **Data in use** | Actively being accessed | Checking email on a laptop |
| **Data in transit** | Moving from one point to another | Sending an email |
| **Data at rest** | Not currently being accessed, stored on a device | Data on a closed laptop |

**Information security (InfoSec)** is the practice of protecting data in all three states from unauthorized access. Understanding these states helps security teams assess risk and build asset management plans — especially as storage shifts toward technologies like the cloud.

## Cloud Security

Cloud technology has reshaped how businesses operate — but it also introduces new cybersecurity challenges.

### Cloud Service Models

| Model | What it provides | Examples |
|---|---|---|
| **SaaS** (Software as a Service) | Front-end applications accessed via browser; provider manages all back-end systems | Gmail, Slack, Zoom |
| **PaaS** (Platform as a Service) | Back-end development tools clients use to build/manage/deploy their own apps; provider hosts the underlying hardware/software | Google App Engine, Heroku, VMware Cloud Foundry |
| **IaaS** (Infrastructure as a Service) | Remote access to back-end infrastructure — servers, storage, networking | — |

### The Shared Responsibility Model

In a traditional on-premises setup, an organization controls its entire IT infrastructure. In the cloud, responsibility is split between provider and client. The client is typically responsible for what's directly in their control:
- Identity and access management
- Resource configuration
- Data handling

### Cloud Security Challenges

- **Misconfiguration** — a major risk, since customers are responsible for configuring their own security environment and often leave out-of-the-box settings unchanged
- **Cloud-native breaches** — more likely when services are misconfigured
- **Monitoring access** — can be difficult depending on the client's level of service
- **Regulatory compliance** — especially tricky in regulated industries bound by standards like HIPAA, PCI DSS, and GDPR

## Elements of a Security Plan

Security is a joint effort of **people, processes, and technology**, built on a shared culture of values across an organization — all aimed at protecting assets.

Risks are categorized (e.g., damage, disclosure, loss of information) and can stem from physical damage, attacks, or human error.

| Element | Role |
|---|---|
| **Policies** | Rules defining *what* is protected and *why* — the strategic scope, objectives, and limitations of the plan |
| **Standards** | Tactical guidance that informs how policies are implemented (e.g., minimum password length) |
| **Procedures** | Step-by-step instructions for specific security tasks — supports accountability, consistency, and efficiency |

## Compliance

**Compliance** is adherence to internal standards and external regulations — essential for maintaining trust, reputation, safety, and data integrity.

**Non-compliance** can result in significant fines, lawsuits, and lasting reputational damage — especially in heavily regulated industries like healthcare and finance.

## The NIST Cybersecurity Framework (CSF)

The CSF is a **voluntary** framework of standards, guidelines, and best practices for managing cybersecurity risk.

### Three Components

| Component | Purpose |
|---|---|
| **Core** | A set of desired cybersecurity outcomes, organized into six functions: **Identify, Protect, Detect, Respond, Recover, Govern**. Used as a reference to identify key assets, apply safeguards, detect attacks, and plan response/recovery |
| **Tiers** | Measures how sophisticated an organization's cybersecurity program is, on a scale of **1 (limited controls) to 4 (exemplary)** — used to assess posture and find improvement areas |
| **Profiles** | Pre-built CSF templates tailored to a specific organization or industry's risks, used as a baseline or to benchmark against industry standards |

### CISA's (Cybersecurity and Infrastructure Security Agency) Recommended Steps for Implementing CSF

1. Create a current profile of security operations and the business's specific needs
2. Perform a risk assessment to see which current operations meet business and regulatory standards
3. Analyze and prioritize gaps that put assets at risk
4. Implement a plan of action to reach the organization's goals

## Questions / Things to Revisit

- 

---
*Notes based on Google Cybersecurity Professional Certificate, Course 5 — Assets, Threats, and Vulnerabilities*
