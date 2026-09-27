# Module 2: Security Frameworks and Controls

## Security Frameworks

Security frameworks are guidelines that help organizations build plans to mitigate risks and threats to data and privacy, supporting compliance with laws and regulations.

| Framework | Description |
|---|---|
| **Cyber Threat Framework (CTF)** | Developed by the U.S. government to provide a common language for describing and communicating cyber threat activity |
| **ISO/IEC 27001** | An internationally recognized framework enabling organizations of any sector/size to manage the security of assets — financial info, intellectual property, employee data, and third-party-entrusted information |

## Security Controls

Security controls are safeguards designed to reduce specific security risks, helping organizations avoid significant financial and reputational damage.

### Types of Security Controls

1. **Encryption** — converts data from readable (plaintext) to encoded, unreadable (ciphertext) format to ensure confidentiality
2. **Authentication** — verifies the identity of a user/system, from basic username/password to MFA (security codes, biometrics)
3. **Authorization** — grants access to specific resources, ensuring only permitted individuals can access particular data/functionality

### Controls by Category

| Category | Examples |
|---|---|
| **Physical** | Gates, fences, locks; security guards; CCTV/surveillance/motion detectors; access cards/badges |
| **Technical** | Firewalls; MFA; antivirus software |
| **Administrative** | Separation of duties; authorization; asset classification |

### Control Types (by Function)

- **Preventative** — designed to stop an incident before it happens
- **Corrective** — restores an asset after an incident
- **Detective** — determines whether an incident has occurred or is in progress
- **Deterrent** — discourages attacks from being attempted

## CIA Triad (Recap)

A fundamental security model helping organizations manage risk and protect sensitive information:
- **Confidentiality** — only authorized users can access specific assets/data
- **Integrity** — data is verifiably correct, authentic, and reliable
- **Availability** — data is accessible to those authorized to use it

> Maintaining an *acceptable level of risk* while designing systems/policies to establish a strong security posture is a core part of the job — understanding what counts as "acceptable" is critical in cybersecurity.

## NIST Cybersecurity Framework (NIST CSF)

Helps organizations manage cybersecurity risk and implement risk management strategies. Six core functions (examples below use a mid-sized online store hit by ransomware):

| Function | Focus | Example |
|---|---|---|
| **1. Govern** | Establishing/maintaining structures and processes for effective risk management — objectives, leadership commitment, risk strategy, continuous improvement | Leadership defines a formal security policy; board approves a risk strategy requiring documented system owners, continuous monitoring, tested backups |
| **2. Identify** | Managing cybersecurity risk and its impact on people/assets | IT runs automated discovery, maintains an inventory of databases/servers/plugins, classifies the customer database as high-risk |
| **3. Protect** | Safeguarding via policies, procedures, training, and tools | Enforcing MFA for all logins, encrypting the customer database, installing endpoint protection on laptops |
| **4. Detect** | Identifying potential incidents; enhancing monitoring for faster detection | Monitoring tool alerts the team at 2 AM over an unknown account rapidly downloading files |
| **5. Respond** | Containing, neutralizing, and analyzing incidents; implementing improvements | Team isolates the compromised server, revokes credentials, notifies legal/executive leadership |
| **6. Recover** | Restoring affected systems to normal operation | IT restores from a clean offline backup, validates system integrity, updates customers on restoration |

## OWASP Security Principles

Core principles (OWASP = Open Web Application Security Project):

- **Minimize attack surface area** — reduce potential vulnerabilities threat actors could exploit
- **Principle of least privilege** — users get only the minimum access necessary for their tasks
- **Defense in depth** — layer multiple controls (MFA, firewalls, etc.) rather than relying on one
- **Separation of duties** — prevents any individual from holding too many privileges
- **Keep security simple** — avoid overly complex solutions that become unmanageable
- **Fix security issues correctly** — identify root cause, correct the vulnerability, and test the fix

**Additional principles:**
- **Establish secure defaults** — the most secure configuration should be the automatic/default setting
- **Fail securely** — if a control fails, it should default to its most secure state (e.g., a failed firewall shouldn't just let all traffic through)
- **Don't trust services blindly** — don't assume partner systems are secure; verify, then trust
- **Avoid security by obscurity** — security shouldn't depend on keeping a system's inner workings secret

## Planning a Security Audit

A security audit helps identify organizational risks, assess existing controls, and correct compliance issues — typically conducted internally to improve security posture and ensure regulatory compliance.

### Common Elements of an Internal Audit

1. **Establish scope and goals**
   - *Scope* — the specific areas, systems, people, and processes included in the audit
   - *Goals* — the specific objectives you want to accomplish to improve security posture
2. **Conduct a risk assessment** — identify potential threats/risks/vulnerabilities, determine needed security measures, prioritize security efforts
3. **Complete a controls assessment** — review existing assets and evaluate risks to those assets to confirm controls/processes are effective
4. **Assess compliance** — determine whether the organization adheres to required regulations
5. **Communicate results** — share findings/recommendations with stakeholders: audit scope/goals, existing risks and urgency, compliance status, and suggested improvements

### Audit Checklist Structure

1. **Identify the scope of the audit** — list assets to be assessed, note how the audit supports organizational goals, indicate audit frequency, evaluate whether existing policies/protocols are actually being followed
2. **Complete a risk assessment** — evaluate risks tied to budget, controls, internal processes, and external regulations
3. **Conduct the audit** — assess the security of the assets defined in the scope
4. **Create a mitigation plan** — a strategy to lower risk level and reduce potential costs/penalties
5. **Communicate results to stakeholders** — a detailed report of findings, suggested improvements, and applicable compliance regulations/standards

## Applied Project

This module's guided activity — conducting a full security audit for a scenario company, including a comparison against the exemplar solution — is documented separately as applied project work rather than notes:
📁 [`security-projects/01-security-audit`](https://github.com/CarriappaKD/security-projects/tree/main/01-security-audit)

## Questions / Things to Revisit

- 

---
*Notes based on Google Cybersecurity Professional Certificate, Course 2 — Play It Safe: Manage Security Risks*
