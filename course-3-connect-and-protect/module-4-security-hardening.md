# Module 4: Security Hardening

## What Is Security Hardening?

**Security hardening** — strengthening a system to reduce its vulnerabilities and shrink its **attack surface** (every potential weakness a threat actor could exploit). Applies across devices, networks, applications, and cloud infrastructure — commonly split into **OS hardening**, **network hardening**, and **cloud hardening**.

**General hardening practices:**
- Regular maintenance, patching, and config changes (stronger passwords, updated encryption)
- Removing unused apps, disabling unused ports, reducing access permissions — shrinks the attack surface and makes monitoring easier
- Regular **penetration testing** — a simulated attack used to find vulnerabilities in systems/networks/apps/processes, with findings used to strengthen posture

## OS Hardening

An insecure OS on even one system can compromise the entire network.

| Task | Type | Purpose |
|---|---|---|
| **Patch installation** | Regular | Keep OS updated with the latest security patches as vendors release them |
| **Hardware/software disposal** | Regular | Properly wipe/dispose of old hardware, delete unused software — avoids unnecessary vulnerabilities |
| **Baseline configuration** | One-time setup | A documented reference spec to compare current config against, to catch unauthorized changes |
| **Strong password policy** | One-time setup | Password rules + often MFA, to harden against unauthorized access |

> OS hardening helps specifically defend against **brute force attacks**.

### Brute Force Attacks

A trial-and-error method of guessing private information (usually passwords).

| Type | Description |
|---|---|
| **Simple brute force** | Trying many username/password combinations until one works |
| **Dictionary attack** | Using a list of common passwords or previously breached credentials |

Brute forcing is slow manually, so attackers typically automate it with software tools.

### Testing Tools: VMs and Sandboxes

| Tool | Use |
|---|---|
| **Virtual Machine (VM)** | Software version of a physical computer; runs code in isolation so malicious code can't affect the host. Useful for investigating infected machines or running malware safely. (Small risk: malware can sometimes "escape" virtualization.) |
| **Sandbox** | A testing environment separate from the main network — used to test patches, find bugs, evaluate suspicious files, or simulate attack scenarios |

### Brute Force Prevention Measures

| Measure | How It Works |
|---|---|
| **Hashing + Salting** | Hashing converts data into a unique, irreversible value (one-way function) to verify integrity. Salting adds random characters before hashing, increasing complexity/security |
| **MFA / 2FA** | MFA requires 2+ verification methods (password, biometrics, OTP, etc.); 2FA is the same idea but limited to exactly two |
| **CAPTCHA / reCAPTCHA** | A test proving the user is human, blocking automated brute-force attempts. reCAPTCHA is Google's free version |
| **Password policies** | Standardized rules: complexity requirements, update frequency, reuse restrictions, login attempt limits before lockout |

## Network Hardening

| Task | Type | Purpose |
|---|---|---|
| **Firewall rule maintenance + log analysis** | Regular | Keep rules current; use SIEM tools to analyze/prioritize security events |
| **Patch updates + server backups** | Regular | Maintain a secure environment, protect against known vulnerabilities |
| **Port filtering + wireless protocol updates** | One-time | Block/allow specific ports on firewalls; disable outdated wireless protocols in favor of current ones |
| **Network segmentation + encryption** | One-time | Isolate subnets by department/zone to contain issues; encrypt all communications, with stronger encryption for sensitive data |

### Defense in Depth

Layering multiple security tools so each adds an incremental layer of protection — starting from the minimum (just a firewall) up to the strongest combination (firewall + IDS/IPS + security event monitoring).

| Layer | Role |
|---|---|
| **Firewall** | Sits between the trusted private network and an untrusted external network (e.g., the internet, via router/modem); allows/blocks traffic by inspecting packet headers against a rule set |
| **IDS (Intrusion Detection System)** | Monitors activity and *alerts* on possible intrusions by matching known attack signatures/anomalies. Sits behind the firewall (reduces false-positive noise from already-filtered traffic). Limitation: only catches known attacks/obvious anomalies, and doesn't block anything itself — a human must act on the alert |
| **IPS (Intrusion Prevention System)** | Like an IDS, but actively *stops* the intrusive activity instead of just alerting. Also sits behind the firewall. Limitation: being inline means if it fails, the connection between the private network and internet breaks; also prone to false positives dropping legitimate traffic |
| **SIEM** | Collects and analyzes log data in real time from IDS, IPS, firewalls, VPNs, proxies, and DNS logs, surfacing it on a centralized dashboard — a **"single pane of glass"** for analysts |

## Network Security in the Cloud

Cloud networks host company data/applications in remote data centers, accessible via the internet. Cloud servers still need regular hardening — CSPs(Cloud Service Provider) can't prevent every intrusion, so organizations must add their own measures.

**Key distinction from traditional hardening:** cloud environments use a **server baseline image** across all instances, enabling easy comparison to detect unverified/unauthorized changes.

**Separating applications by service category** improves cloud security by:
- **Limiting blast radius** — a compromise in one category stays contained, rather than spreading to more critical applications
- **Enabling tailored controls** — different categories can have different security policies instead of one-size-fits-all
- **Easing monitoring/auditing** — simpler to watch traffic/logs per application group

*(Example: keeping older apps separate from newer ones, and internal/backend systems separate from front-end user-facing apps.)*

### Cloud Security Considerations

| Area | Key Point |
|---|---|
| **IAM** | Manages digital identities and authorizes cloud resource usage. Loosely configured user roles are a common risk — misconfigured roles can expose critical operations to unauthorized users |
| **Configuration** | Every cloud service needs precise setup for security/compliance. Misconfiguration (especially during migrations) is a frequent breach cause |
| **Attack surface** | Every service/app adds its own risks, increasing the overall attack surface. More services = more entry points for malware, though CSPs are often more scrutinized/secure than traditional on-prem setups |
| **Zero-day attacks** | Previously unknown exploits. CSPs often detect zero-days before traditional IT teams do, and can patch hypervisors/migrate workloads so customers aren't impacted |
| **Visibility and tracking** | On-prem admins can inspect every packet directly; in the cloud, similar visibility comes via flow logs and tools like packet mirroring — but CSPs don't let customers monitor traffic directly on CSP servers. CSPs undergo third-party audits to verify security |
| **Pace of change** | CSPs update frequently, which can force organizations to adjust configurations/processes to stay aligned — a shift from being fully in control of every change themselves |

### Shared Responsibility Model

A core cloud security principle: **the CSP secures the cloud infrastructure** (physical data centers, hypervisors, host OS) — **the organization secures what it puts in the cloud** (its assets, processes, and configurations).

> Common pitfall: assuming the CSP is handling something it isn't. Example — the CSP secures the underlying cloud, but it's the **organization's** job to configure its own applications/services correctly.

## Cloud Security Hardening Techniques

| Technique | What It Does |
|---|---|
| **IAM** | Same as above — manages identities and authorizes resource access |
| **Hypervisors** | Abstracts host hardware from the software environment. **Type 1** runs directly on hardware (e.g., VMware ESXi) — commonly used by CSPs. **Type 2** runs on top of a host OS (e.g., VirtualBox). CSPs manage/patch hypervisors; misconfigurations can cause a **VM escape** (attacker breaks out of a VM to access the hypervisor/host/other VMs) |
| **Baselining** | A fixed reference point for how the cloud environment should be configured, used to detect drift/unauthorized changes. Examples: restricting admin portal access, enabling password management, file encryption, threat detection for databases |
| **Cryptography** | Encryption scrambles data into unreadable ciphertext, protected by an encryption key rather than a secret algorithm — core to protecting cloud data confidentiality/integrity |
| **Cryptographic erasure (crypto-shredding)** | Destroying the encryption key(s) for encrypted data instead of traditional data wiping — once all key copies are destroyed, the data becomes permanently undecipherable |

### Key Management

| Tool | Purpose |
|---|---|
| **TPM (Trusted Platform Module)** | A chip that securely stores passwords, certificates, and encryption keys |
| **CloudHSM (Cloud Hardware Security Module)** | A dedicated device for secure key storage and cryptographic operations (encryption/decryption) |

> Customers generally don't have direct access to a CSP's own infrastructure, but can request audits/security reports. Most CSPs allow customers to supply their *own* encryption keys — but then the customer is fully responsible for keeping those keys safe; the CSP has limited ability to help if a customer's own keys are lost or compromised. (For U.S. federal contractors, **FedRAMP** maintains a list of verified/compliant CSPs.)

## Questions / Things to Revisit

- 

---
*Notes based on Google Cybersecurity Professional Certificate, Course 3 — Connect and Protect: Networks and Network Security*
