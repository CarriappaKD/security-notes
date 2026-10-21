# Module 3: Vulnerabilities in Systems

## Vulnerabilities and Exploits

| Term | Definition |
|---|---|
| **Vulnerability** | A weakness that can be exploited by a threat |
| **Exploit** | The method used to take advantage of a vulnerability |

### Vulnerability Management Process (4-Step Cycle)

1. Identify vulnerabilities
2. Consider potential exploits
3. Prepare defenses
4. Evaluate those defenses

This is a continuous cycle, since new vulnerabilities constantly emerge.

### Zero-Day Exploits

A **zero-day** is a previously unknown exploit happening in real time — there's no advance warning and no time to patch before it's used. It represents an unplanned-for threat that leaves assets especially vulnerable.

## Vulnerabilities in CI/CD Pipelines

**CI/CD** (Continuous Integration, Continuous Delivery/Deployment) automates the software release process end-to-end — from code creation to deployment — enabling fast, agile development. Like any automated system, an unsecured pipeline becomes a major entry point for vulnerabilities.

| Stage | What it does |
|---|---|
| **Continuous Integration (CI)** | Frequently merges code from different developers into a central repo, automatically building and testing it on every merge — catches integration problems early |
| **Continuous Delivery (CD)** | Code that passes automated tests is auto-deployed to a staging environment or prepped for release; a manual approval step still gates production |
| **Continuous Deployment (CD)** | Fully automated — code that passes all checks deploys straight to production, no manual approval |

### Security Benefits of CI/CD

Built-in automated security checks can include:
- **DAST** (Dynamic Application Security Testing) — finds vulnerabilities in running applications in staging
- **Security compliance checks** — confirm software meets the org's security policies
- **Infrastructure security validations** — confirm the hosting systems themselves are secure

A well-secured pipeline also means: fewer human errors from manual work, faster delivery of security patches, better cross-team collaboration (dev/security/ops), and smaller/more frequent releases that limit the blast radius of any single flaw.

### Common CI/CD Vulnerabilities

| Vulnerability | Risk | Mitigation |
|---|---|---|
| **Insecure dependencies** | Third-party libraries with known CVEs get pulled into builds automatically | Regularly scan and update dependencies |
| **Misconfigured permissions** | Weak access controls let attackers modify code/pipeline configs | Enforce RBAC; limit who can touch critical pipeline elements |
| **Lack of automated security testing** | No SAST/DAST means vulnerabilities ship undetected | Integrate SAST and DAST into the pipeline |
| **Exposed secrets** | Hardcoded API keys/passwords/tokens in code or configs | Never hardcode secrets — use a secrets vault (e.g., HashiCorp Vault, AWS Secrets Manager) |
| **Unsecured build environments** | A compromised pipeline server lets attackers alter builds or steal data | Harden build environments; use secure containers/VMs |

### Building a Secure CI/CD Pipeline

- **DevSecOps mindset** — build security into every development stage, not bolted on at the end
- **Strong access controls** — least privilege, MFA, RBAC
- **Automate security testing everywhere** — SAST, SCA (Software Composition Analysis), DAST
- **Keep dependencies updated** — maintain an inventory; use tools like Dependabot/Snyk
- **Secure secrets management** — dedicated vaults, never hardcoded

## Defense in Depth

A security model using **multiple layers of defense**, so that if one layer fails, another is still in place to stop an attack. Reduces risk by applying controls at every level.

### The Five Layers

| Layer | Focus | Example Technology |
|---|---|---|
| **Perimeter** | Authentication — filtering external access | Usernames/passwords |
| **Network** | Authorization — controlling access within the network | Network firewalls |
| **Endpoint** | Protecting devices accessing the network | Antivirus software |
| **Application** | Security built into applications | Multi-factor authentication |
| **Data** | Protecting critical data itself | Asset classification |

## Vulnerabilities vs. Exposures

| Term | Meaning |
|---|---|
| **Vulnerability** | A weakness in a system |
| **Exposure** | A mistake that can be exploited by a threat |

Example: a document is *vulnerable* to being misplaced; leaving it near an open window *exposes* it to being blown away.

### CVE List and NVD

- The **CVE** (Common Vulnerabilities and Exposures) list is an openly accessible dictionary of known vulnerabilities and exposures, maintained by **MITRE Corporation**. Reports come from independent researchers, vendors, and ethical hackers.
- The **NIST National Vulnerability Database (NVD)** scores vulnerability severity using **CVSS** (Common Vulnerability Scoring System) on a **0–10** scale — below 4.0 is low risk, above 9.0 is critical. Security teams use these scores to prioritize fixes.

## The OWASP Top 10

**OWASP** (Open Web Application Security Project, now Open Worldwide Application Security Project®) is a nonprofit that works to improve software security. The **OWASP Top 10** lists the most common vulnerabilities in new/custom software and is widely referenced during application development.

| Vulnerability | What it means |
|---|---|
| **Broken access control** | Failures in restricting what users can do lead to unauthorized disclosure, modification, or destruction of data |
| **Cryptographic failures** | Sensitive data (e.g., PII) isn't properly encrypted, or a weak algorithm (like MD5) is used |
| **Injection** | Malicious code inserted into a vulnerable app (e.g., via a login form) lets attackers steal or modify data |
| **Insecure design** | Missing or poorly implemented security controls baked into the app from the start |
| **Security misconfiguration** | Security settings not properly set/maintained — e.g., leaving default settings on a deployed server |
| **Vulnerable and outdated components** | Using unmaintained open-source libraries increases exploit risk |
| **Identification and authentication failures** | App fails to correctly verify who should have access |
| **Software and data integrity failures** | Updates/patches aren't properly reviewed before deployment — can enable supply chain attacks |
| **Security logging and monitoring failures** | Inadequate logging/monitoring makes it hard to detect and respond to incidents |
| **Server-side request forgery (SSRF)** | Attacker manipulates a server into fetching or updating unauthorized resources |

## Open Source Intelligence (OSINT)

**OSINT** is the collection and analysis of information from publicly available sources to generate usable intelligence.

- **Information** = raw data/facts
- **Intelligence** = the analyzed, interpreted, integrated output of that information, usable for decisions

OSINT supports InfoSec by helping:
- Provide insight into cyberattacks
- Detect potential data exposures
- Evaluate existing defenses
- Identify unknown vulnerabilities

**Common OSINT tools:**
| Tool | Purpose |
|---|---|
| **VirusTotal** | Analyzes suspicious files, domains, URLs, IPs for malicious content |
| **MITRE ATT&CK®** | Knowledge base of real-world adversary tactics/techniques |
| **OSINT Framework** | Web interface linking OSINT tools by source/platform |
| **Have I Been Pwned** | Searches for breached email accounts |

## Vulnerability Assessments

An internal review of an organization's security systems — identifies weak points, prevents attacks, and ensures controls meet regulatory standards.

### Four-Step Process

1. **Identification** — scanning tools + manual testing to find vulnerabilities
2. **Vulnerability analysis** — investigate the root cause of each finding
3. **Risk assessment** — score each vulnerability by impact severity and likelihood of exploitation, to prioritize
4. **Remediation** — fix critical vulnerabilities (new procedures, patches, OS updates) via joint security/IT effort

A **vulnerability scanner** automatically compares known vulnerabilities/exposures against what's running on the network, flagging misconfigurations or programming flaws.

### The Five Attack Surfaces Scanned

1. Perimeter layer (authentication systems)
2. Network layer (firewalls, etc.)
3. Endpoint layer (laptops, desktops, servers)
4. Application layer (user-facing software)
5. Data layer (data at rest, in transit, in use)

### Types of Scans

| Dimension | Option A | Option B |
|---|---|---|
| **External vs. Internal** | External — tests the perimeter from outside (websites, firewalls) | Internal — examines internal systems (e.g., how an app handles user input) |
| **Authenticated vs. Unauthenticated** | Authenticated — logs in as a real/admin user to check for broken access controls | Unauthenticated — simulates an outsider with no access; a vulnerability exists if restricted content is still reachable |
| **Limited vs. Comprehensive** | Limited — targets specific devices (e.g., one firewall) | Comprehensive — scans everything connected to the network |

> Scanners are meant to be non-intrusive (unlike a real attack), though a scan can occasionally still cause instability. **Discovery scanning** (mapping devices/open ports on the network) should happen before limited or comprehensive scans.

## Patches, Updates, and EOL Software

A **patch** is a software/OS update addressing security vulnerabilities — usually containing bug fixes. Ideally patches ship before malicious hackers find the flaw, but sometimes they're a reaction to a zero-day.

| Strategy | Advantage | Disadvantage |
|---|---|---|
| **Manual updates** | More control — useful if updates aren't well-tested yet | Critical updates can be forgotten/ignored |
| **Automatic updates** | Simpler; keeps systems current with critical patches (CISA recommends this when available) | Poorly tested patches can cause instability |

**End-of-life (EOL) software** no longer receives updates once a newer version replaces it, even though it may still be in use — a growing risk as more connected devices enter the market.

> Note: patches/updates ≠ upgrades. An upgrade is a purchased, entirely new version of hardware/software.

## Penetration Testing

A **pen test** is an authorized, simulated attack that uses the same tools/techniques as real attackers to find and exploit vulnerabilities — a form of ethical hacking. Unlike a vulnerability assessment (which just finds weaknesses), a pen test actively exploits them to show real-world consequences.

| Team Type | Focus |
|---|---|
| **Red team** | Simulates attacks to find vulnerabilities |
| **Blue team** | Defense and incident response — validates existing security systems |
| **Purple team** | Collaborative — combines red + blue to improve overall posture |

### Testing Strategies (by access level)

| Strategy | Access Level | Also Known As |
|---|---|---|
| **Open-box** | Same privileged access as an internal developer | Internal / full-knowledge / white-box / clear-box |
| **Closed-box** | Little to no internal access, like a malicious hacker | External / black-box / zero-knowledge |
| **Partial knowledge** | Limited access, like a customer service rep | Gray-box |

Organizations often run **bug bounty programs**, paying freelance pen testers to find and report vulnerabilities (e.g., via platforms like HackerOne) — a good entry point for newer security professionals.

## Attack Surfaces

An **attack surface** covers every potential vulnerability a threat actor could exploit — analyzing it is how security teams prioritize where to allocate resources.

| Type | Covers |
|---|---|
| **Physical attack surface** | People and their devices, inside and outside the org — reduced via security hardening (policies, access controls) |
| **Digital attack surface** | Everything beyond the firewall, connected online — expanded significantly by cloud computing, harder to harden |

## Approaching Security with an Attacker Mindset

Security teams simulate attacks to proactively learn from vulnerability findings, applying an attacker's perspective in a controlled environment.

| Simulation Type | Role | Also Known As |
|---|---|---|
| **Proactive** | Plays the attacker — exploits vulnerabilities to test defenses and security awareness | Red team exercise |
| **Reactive** | Plays the defender — gathers info on protected assets, often using vulnerability scanning tools | Blue team exercise |

## Threat Actors

A **threat actor** is any person or group posing a security risk — intentional or accidental, inside or outside the organization.

### Threat Actor Categories (by motivation)

| Category | Description |
|---|---|
| **Competitors** | Rival companies who could benefit from leaked information |
| **State actors** | Government intelligence agencies |
| **Criminal syndicates** | Organized groups profiting from criminal activity |
| **Insider threats** | Anyone with current/past authorized access — accidental or intentional |
| **Shadow IT** | Individuals using ungoverned technology (e.g., personal email for work communications) |

### Hacker Types (by intent)

| Type | Intent |
|---|---|
| **Unauthorized (malicious)** | Commits crimes using programming skills. Lower-skilled attackers using others' pre-written malicious code are called **script kiddies** |
| **Authorized (ethical)** | Improves an org's security — internal security teams, external vendors, bug bounty hunters |
| **Semi-authorized** | May violate ethical norms but isn't malicious — e.g., a **hacktivist** exposing a vulnerability for a political cause before a malicious actor finds it |

### Advanced Persistent Threats (APT)

A threat actor that maintains **unauthorized access for an extended period**, focused on surveillance and intelligence gathering — often targeting government, defense, financial, or telecom sectors.

### Access Points (Attack Vector Categories)

- Direct physical access
- Removable media (USB drives, etc.)
- Social media platforms
- Email (personal and business)
- On-premises wireless networks
- Cloud services (third-party)
- Supply chains (third-party vendors as a backdoor)

## Attack Vectors

The pathways attackers use to breach defenses (e.g., social media, removable media) — can be exploited maliciously or triggered unintentionally by employees.

**Thinking like an attacker** means: identifying a target → determining how it can be accessed → evaluating exploitable vectors → finding tools/methods of attack.

**Defending against attack vectors:**
- Educate users on emerging threats (e.g., new phishing tactics)
- Apply least privilege
- Use appropriate security controls/tools (e.g., antivirus) to reduce human error
- Build a diverse security team — broader perspectives help anticipate more attacker approaches

## Brute Force Attacks

A trial-and-error process for discovering private information/credentials.

| Technique | Method |
|---|---|
| **Simple brute force** | Try every possible username/password combination |
| **Dictionary attack** | Try a list of commonly used credentials |
| **Reverse brute force** | Start with one known credential, try it against many systems |
| **Credential stuffing** | Reuse stolen credentials from one breach against other organizations. A specialized variant, **pass the hash**, reuses stolen unsalted hashed credentials to forge an authenticated session |

> **Exhaustive key search** is the equivalent brute-force technique applied to encrypted data rather than login credentials.

**Common brute-forcing tools** (used by security pros to test their own systems): Aircrack-ng, Hashcat, John the Ripper, Ophcrack, THC Hydra.

### Prevention Measures

| Control | How it helps |
|---|---|
| **Hashing + salting** | Converts credentials to unique values; salting strengthens resistance to precomputed attacks |
| **MFA** | Requires two or more proofs of identity |
| **CAPTCHA** (Completely Automated Public Turing test to tell Computers and Humans Apart) | Challenge-response test proving the user is human, not automated software |
| **Password policies** | Managerial controls — minimum length/complexity requirements, lockout after failed attempts, periodic password changes |

## Questions / Things to Revisit

- 

---
*Notes based on Google Cybersecurity Professional Certificate, Course 5 — Assets, Threats, and Vulnerabilities*
