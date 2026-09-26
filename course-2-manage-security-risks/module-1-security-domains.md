# Module 1: Security Domains

## The Eight CISSP Security Domains

Using these eight domains, security teams organize tasks, identify gaps, and establish an organization's security posture. (Examples below use a healthcare organization to show how each domain applies in practice.)

### Domain 1: Security and Risk Management
- **Defining security goals and objectives** — setting clear targets for what to protect and why
- **Risk mitigation** — procedures and rules to quickly reduce the impact of a security incident
- **Compliance** — following internal security policies, regulatory requirements, and independent standards
- **Business continuity** — disaster recovery plans so the organization can keep operating through an incident
- **Legal regulations** — following laws and ethical guidelines to prevent negligence, abuse, or fraud

> **Example:** Complying with patient privacy laws like HIPAA, defining data protection policies, and training hospital staff on safely handling patient files.

### Domain 2: Asset Security
Securing both digital and physical assets — knowing exactly what data an organization has and who has access to it.
- **Storage** — ensuring data is stored securely
- **Maintenance** — keeping assets in good, up-to-date condition to prevent vulnerabilities
- **Retention** — policies for how long data should be kept
- **Destruction** — properly disposing of data/physical assets once no longer needed

> **Example:** Labeling patient medical records "confidential" and securely shredding old paper charts or wiping hard drives from retired hospital computers.

### Domain 3: Security Architecture and Engineering
Optimizing data security by ensuring effective tools, systems, and processes protect the organization's assets and data.
- **Optimizing data security** — continuously improving how data is protected
- **Effective tools/systems/processes** — selecting the right security tech, designing secure systems, establishing clear procedures (e.g., encryption for sensitive data, MFA for system access)
- **Promoting shared responsibility** — security awareness training, clear policies, encouraging reporting of suspicious activity

> **Example:** Encrypting patient databases so stolen data stays unreadable, and placing physical servers in a locked, badge-only room.

### Domain 4: Communication and Network Security
Protecting an organization's data and communication by managing and securing physical networks and wireless communications.
- **Securing physical networks** — protecting infrastructure (servers, routers, cables) from unauthorized access/tampering
- **Securing wireless communications** — guarding against risks from insecure connections (public Wi-Fi, unknown devices)
- **Implementing access controls** — restricting access to insecure channels, blocking risky public Wi-Fi, limiting personal device use on company networks
- **Secure protocols and encryption** — protecting data in transit from eavesdropping/unauthorized access
- **Regular monitoring and auditing** — watching network traffic for suspicious activity and auditing configurations proactively

> **Example:** Using secure VPNs so doctors can view patient charts from home without data interception.

### Domain 5: Identity and Access Management (IAM)
Controlling access and authorization to keep data secure. Four main components:
- **Identification** — verifying who a user is (username, access card, biometrics)
- **Authentication** — verifying identity (password, PIN)
- **Authorization** — granting access appropriate to the user's role, once identity is confirmed
- **Accountability** — monitoring/recording user actions (e.g., login attempts)

> **Example:** Giving a nurse access to patient room monitors, but blocking access to hospital financial records.

### Domain 6: Security Assessment and Testing
Testing security controls, collecting/analyzing data, and performing audits to identify risks, threats, and vulnerabilities — then improving or implementing controls.
- Identifying new/better ways to mitigate threats via regular testing
- Ensuring security efforts align with business goals and objectives
- Improving or implementing controls (e.g., requiring MFA)

> **Example:** Hiring ethical hackers to run a simulated cyberattack on the hospital's online appointment system to find and fix bugs.

### Domain 7: Security Operations
Mitigating active attacks, conducting forensic investigations into how breaches occurred, and implementing preventive measures.
- **Conducting investigations** — after an incident is neutralized, forensic investigation determines when/how/why the breach occurred
- **Implementing preventative measures** — using investigation findings to improve defenses against future attacks

> **Example:** A 24/7 security center spots a ransomware alert locking hospital files and shuts down infected computers immediately, then implements new measures afterward.

### Domain 8: Software Development Security
Using secure coding practices throughout the Software Development Lifecycle (SDLC).
- Integrating security fully into the software product
- Secure design reviews during the design phase
- Secure code reviews during development/testing phases
- Penetration testing during deployment/implementation

> **Example:** Ensuring a hospital's patient check-in mobile app uses secure login code and safe data entry fields to prevent malicious injections.

## Threats, Risks, and Vulnerabilities

- **Threat** — any event or circumstance that can negatively impact assets (e.g., a phishing attack aiming to acquire sensitive data). Think of it as *something that could happen*. Common threats often stem from misconfigurations, unnecessary access, and outdated systems:
  - **Insider threats** — staff or vendors abusing authorized access to obtain data that harms the organization
  - **Advanced Persistent Threats (APTs)** — a threat actor maintaining unauthorized system access over an extended period

- **Risk** — anything that can impact the confidentiality, integrity, or availability of an asset; it's about the *probability of harm*. Risks are categorized as:
  - **Low** — public information; little harm if compromised
  - **Medium** — non-public data; could cause some financial/reputational damage
  - **High** — protected by regulations; compromise severely impacts the organization

  Factors affecting organizational risk: external risk (threat actors), internal risk (current/former employees, vendors, partners), unmaintained legacy systems, multiparty risk (third-party vendor access), and software compliance (unpatched/outdated software).

- **Vulnerability** — a weakness that can be exploited by a threat; a flaw or gap that allows a threat to cause damage (e.g., outdated software, weak passwords, risky human behavior).

> **Relationship:** a vulnerability is a weakness → a threat is something that can exploit that weakness → a risk is the potential for harm when a threat exploits a vulnerability.

Common impacts of threats/risks/vulnerabilities: **financial loss, identity theft, and reputational damage.**

### Key Terminology
| Term | Definition |
|---|---|
| **Asset** | An item perceived as having value to an organization |
| **Ransomware** | A malicious attack where threat actors encrypt an organization's data and demand payment to restore access |

## NIST Risk Management Framework (RMF)

The RMF provides a structured approach for managing risks, threats, and vulnerabilities. Seven steps (examples below use a banking/financial sector scenario):

1. **Prepare** — activities to manage security/privacy risk *before* a breach occurs.
   > Bank's board sets risk tolerance for fraud, assigns the CISO as authorizing official, maps controls to GLBA/PCI-DSS regulations.
2. **Categorize** — assessing how confidentiality, integrity, and availability could be impacted by risk.
   > Categorizing the mobile banking system as *High Impact* — breach could mean stolen funds, leaked account numbers, or transaction downtime.
3. **Select** — choosing, customizing, and documenting protective controls.
   > Selecting baseline controls from NIST SP 800-53: cryptographic protections, MFA, session time-outs.
4. **Implement** — putting security/privacy plans into action.
   > Implementing biometric logins, AES-256 encryption at rest, a fraud-detection API flagging unusual login locations.
5. **Assess** — determining whether controls are implemented correctly and identifying weaknesses.
   > An independent red-team firm pen-tests the app to try bypassing authentication or intercepting transactions.
6. **Authorize** — being accountable for remaining security/privacy risk in the organization.
   > CISO reviews the assessment, accepts minor remaining risk, signs the Authorization to Operate (ATO) so the app can launch.
7. **Monitor** — staying aware of how systems operate; maintaining technical operations over time.
   > The bank's SOC uses real-time monitoring to spot brute-force login attempts; developers push regular patches for new vulnerabilities.

## Questions / Things to Revisit

- 

---
*Notes based on Google Cybersecurity Professional Certificate, Course 2 — Play It Safe: Manage Security Risks*
