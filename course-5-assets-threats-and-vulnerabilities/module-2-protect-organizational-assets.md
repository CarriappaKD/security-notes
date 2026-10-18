# Module 2: Protect Organizational Assets

## Security Controls

**Security controls** are what keep sensitive data private and safe.

| Control Type | What it covers |
|---|---|
| **Technical** | Technology-based safeguards — encryption, authentication systems |
| **Operational** | Day-to-day security activities performed by people — awareness training, incident response |
| **Managerial** | Defines *how* technical and operational controls reduce risk — policies, standards, procedures |

## Data Ownership and Custodianship

| Role | Responsibility |
|---|---|
| **Data owner** | Decides who can access, edit, use, or destroy specific information |
| **Data custodian** | Responsible for the secure handling, transport, and storage of information |

## Principle of Least Privilege (PoLP)

A user is granted only the **minimum level of access** needed to do their job. Implementing it reduces risk by:
- Limiting access to sensitive information
- Reducing accidental data modification, tampering, or loss
- Supporting easier system monitoring and administration

Closely related: **separation of duties** — dividing tasks/responsibilities among different users so no single person has complete control over a critical business function.

### Determining Access and Authorization

Two questions to ask before granting access:
1. Who is the user?
2. How much access do they need to a specific resource?

A "user" can be a person (employee, customer, vendor) or a device/software connected to the network. Every user should ideally have their own account.

| Account Type | Who/what it's for |
|---|---|
| **Guest** | External users needing internal access — customers, clients, contractors, partners |
| **User** | Staff, based on job duties |
| **Service** | Applications/software interacting with other network software |
| **Privileged** | Elevated/administrative access |

Best practice: set a baseline access level per account type before applying least privilege — though appropriate access can shift over time.

### Auditing Account Privileges

| Audit Type | What it checks |
|---|---|
| **Usage audit** | Which resources an account accesses and what the user does with them — flags unused permissions that could be revoked |
| **Privilege audit** | Whether a user's role still matches their access — catches **privilege creep** (access accumulated after promotions/team changes that's never cleaned up) |
| **Account change audit** | Reviews logged changes to an account (e.g., repeated password-change attempts) to catch suspicious or unauthorized activity |

## The Data Lifecycle

A model mapping how data flows through an organization, and where security controls apply to maintain the CIA triad:

**Collect → Store → Use → Archive → Destroy**

## Data Governance

**Data governance** is the set of processes defining how an organization manages information — covering how data stays private, accurate, available, and secure across its lifecycle.

| Role | Responsibility |
|---|---|
| **Data owner** | Decides who can access, edit, use, or destroy their information |
| **Data custodian** | Responsible for safe handling, transport, storage |
| **Data steward** | Maintains and implements the governance policies set by the organization |

A **data governance policy** is the document defining procedures for keeping data safe and limiting who/what can access it. As a security professional acting as data custodian, you're responsible for ensuring data isn't damaged, stolen, or misused.

### Regulated Categories of Information

Since custodians/stewards don't always get explicit per-case instructions, regulators define categories that must be protected by default:

| Term | Meaning |
|---|---|
| **PII** (Personally Identifiable Information) | Any information that can be used to infer, contact, or locate an individual |
| **PHI** | Protected Health Information |
| **SPII** | *Sensitive* PII — stricter handling, need-to-know basis only (e.g., bank account number, login credentials) |

## Information Security vs. Information Privacy

| | Focus |
|---|---|
| **Information privacy** | Protection from unauthorized *access and distribution* of data — giving people control over their personal information |
| **Information security (InfoSec)** | Keeping data, in all states, away from unauthorized users — protecting that data from threats |

The more data an organization collects, stores, and uses, the more exposed it is to breaches. Both privacy and security are essential to maintaining customer trust and brand reputation.

## Notable Privacy Regulations

| Regulation | Full Name | Covers |
|---|---|---|
| **GDPR** | General Data Protection Regulation | EU rules putting data owners in control of their personal data (name, address, phone, financial/medical info). Applies to any business handling EU citizens'/residents' data, regardless of where the business operates |
| **PCI DSS** | Payment Card Industry Data Security Standard | Security standards from the financial industry to secure credit/debit card transactions against theft and fraud |
| **HIPAA** | Health Insurance Portability and Accountability Act | U.S. law protecting sensitive patient health information; prohibits disclosure without the patient's knowledge and consent |

## Security Assessments and Audits

| | Frequency | Performed by | Purpose |
|---|---|---|---|
| **Security audit** | ~Once a year | Internal and/or external third parties | Reviews security controls, policies, and procedures against expectations |
| **Security assessment** | Every 3–6 months | Usually internal employees | Checks how resilient current security implementations are against threats — often prepares for an audit |

## Fundamentals of Cryptography

**Cryptography** transforms information into an unreadable format to protect it from unintended readers, through two steps:
- **Encryption** — scrambles plaintext into ciphertext
- **Decryption** — converts ciphertext back into readable plaintext

### Public Key Infrastructure (PKI)

A framework securing online information exchange using encryption plus digital certificates.

- **Asymmetric encryption**: a public/private key pair — the public key encrypts, the private key decrypts. More secure, but slower.
- **Symmetric encryption**: one secret key used for both encryption and decryption. Faster, but less secure since the key is shared.
- PKI addresses the risk of sharing keys by establishing trust through **digital certificates**, issued by trusted **certificate authorities (CAs)**, who verify an entity's identity and sign the certificate with their own private key. These certificates act like digital ID badges.

### Key Length

Ciphers are vulnerable to **brute force attacks** (trial-and-error guessing). Longer keys mean more possible combinations to try — more secure, but slower to process.

### Approved Algorithms

**Symmetric:**
| Algorithm | Notes |
|---|---|
| **Triple DES (3DES)** | A block cipher built on the older DES algorithm; applies DES three times with three different 56-bit keys (effective length: 168 bits). Being phased out due to data-volume limitations |
| **AES** (Advanced Encryption Standard) | One of the most secure symmetric algorithms today; generates 128/192/256-bit keys, considered safe from brute force |

**Asymmetric:**
| Algorithm | Notes |
|---|---|
| **RSA** (Rivest Shamir Adleman) | One of the first asymmetric algorithms; key sizes of 1,024 / 2,048 / 4,096 bits; used for highly sensitive data |
| **DSA** (Digital Signature Algorithm) | NIST-introduced standard; 2,048-bit keys; commonly used alongside RSA in PKI |

**Generating keys:** tools like **OpenSSL** (an open-source command-line tool) generate public/private key pairs and are commonly used to verify digital certificates.

### Obscurity Is Not Security

Per **Kerckhoff's principle**, a cryptographic system's security should not depend on keeping its algorithm secret — only the private key needs to stay secret. A system that requires secrecy about *how it works* to stay secure isn't actually secure.

## Non-Repudiation and Hashing

| | Encryption | Hashing |
|---|---|---|
| Reversible? | Yes (with the key) | No — one-way |
| Purpose | Confidentiality | Integrity verification |
| Output | Ciphertext (variable) | Fixed-length hash value/digest |

A **hash function** produces a unique, fixed-length digest. Even a tiny change to the input produces a completely different hash — making tampering detectable.

**Practical uses:**
- Comparing file hashes against databases of known malicious files (e.g., VirusTotal)
- Verifying data integrity via command line, e.g.: `sha256sum ./filename`

Hashing underpins **non-repudiation** — the concept that the authenticity of information can't be denied, since any change produces a verifiably different hash.

### Origins of Hashing: MD5

**MD5** (Message Digest 5) was one of the earliest hash functions, converting data into a 128-bit value (shown as a 32-character string). It was later found vulnerable due to its limited output size.

### Hash Collisions

Since hash functions map infinite possible inputs onto a *finite* set of outputs, two different inputs can theoretically produce the same hash — a **hash collision**. Because hashes are used for authentication, a collision is effectively like forging someone's identity; attackers can exploit this to impersonate authentic data. MD5's limited 32-character output made it especially vulnerable.

### Next-Generation Hashing: SHA Family

The **Secure Hashing Algorithms (SHA)** were developed to resist collisions. The number after "SHA" indicates the digest size in bits.

| Function | Notes |
|---|---|
| SHA-1 | 160-bit digest — no longer considered collision-resistant |
| SHA-224 | — |
| SHA-256 | — |
| SHA-384 | — |
| SHA-512 | — |

All except SHA-1 are considered collision-resistant, though no algorithm is invulnerable to every exploit.

### Rainbow Tables and Salting

A **rainbow table** is a precomputed file of hash values and their matching plaintext — essentially a dictionary of known weak passwords. An attacker with access to a password database can compare it against a rainbow table to crack passwords quickly.

**Salting** defends against this: a random string (the salt) is added to data before hashing, producing a more unique hash and making rainbow-table attacks far less effective. The longer and more unique the salt, the harder it is to crack.

## The AAA Framework

**Authentication, Authorization, and Accounting** — the core model for controlling, monitoring, and tracking user/device access to networks and resources.

### Authentication Factors

| Factor | Example |
|---|---|
| **Knowledge** | Something you know — password, security question |
| **Ownership** | Something you have — a one-time passcode (OTP) sent to a device |
| **Characteristic** | Something you are — biometrics (fingerprint, facial scan) |

### Single Sign-On (SSO)

Combines multiple logins into one. Benefits:
1. Better user experience — fewer usernames/passwords to remember
2. Lower cost from managing fewer connected-service logins
3. Improved security — fewer access points for attackers to target

SSO combats **password fatigue** (reusing passwords across services). It works by exchanging encrypted access tokens between an identity provider and a service provider, using protocols like:
- **LDAP** (Lightweight Directory Access Protocol) — mostly used on-premises
- **SAML** (Security Assertion Markup Language) — mostly used off-premises/cloud

**Limitation of SSO:** it's still a single point of failure — a lost/stolen password can expose access across every connected service.

### Multi-Factor Authentication (MFA)

Requires verifying identity in **two or more** ways (2FA/3FA), combining:
- Something a user knows (username/password)
- Something a user has (OTP via SMS, etc.)
- Something a user is (fingerprint, facial scan)

Reduces the risk of unauthorized access by requiring proofs that are difficult to imitate or brute-force.

### Authorization Mechanisms

Authorization works with authentication to determine what an authenticated user is *allowed* to do, built on least privilege and separation of duties.

| Example | Notes |
|---|---|
| **HTTP Basic Auth** | Sends an identifier with every web communication — vulnerable since credentials are transmitted openly |
| **OAuth** | Secure, open-standard protocol that uses API tokens to grant access between applications without sharing credentials directly |

### Accounting: Why We Audit User Activity

**Accounting** monitors system access logs — who accessed what, when, and what they did. Security analysts rely on these logs to spot failed login trends, uncover attackers, and detect breaches.

- A **session** begins when a user accesses a system and covers the full sequence of requests/responses until they leave.
- A **session ID** is a unique token identifying a user/device for the duration of a session.
- **Session cookies** are exchanged between server and device to validate and time-bound a session without repeatedly sharing sensitive credentials.
- **Session hijacking**: an attacker steals a legitimate session ID to impersonate the user and gain unauthorized access. Monitoring session logs (accounting) is key to catching this kind of activity.

## Least Privilege and Separation of Duties, Revisited

Security isn't just combining processes and technologies — it's making sure they actually create a secure environment that supports a defense strategy. Two foundational principles drive this:

- **Least privilege** — limits the access *an individual* receives
- **Separation of duties** — divides responsibilities *among multiple people*, so no one person has too much control

> Note: "Separation of duties" is sometimes called "segregation of duties."

## Identity and Access Management (IAM)

**IAM** is the collection of processes and technologies that manage digital identities within an organization. Like AAA, IAM authenticates users, determines access privileges, and tracks activity — ensuring the right user gets the right resource at the right time, for the right reason. A "user" can be a person, device, or software.

- Authentication relies mainly on login credentials, often backed by **SSO** and **MFA**.
- **User provisioning**: creating and maintaining a user's digital identity.
- **Deprovisioning**: removing a user's access rights once they no longer need them — an equally important IAM responsibility.

### Authorization Frameworks

| Framework | How access is granted |
|---|---|
| **MAC** (Mandatory Access Control) | Strictest — access granted manually by a central authority on a strict need-to-know basis. Also called non-discretionary control. Common in military/government/law enforcement |
| **DAC** (Discretionary Access Control) | The data owner decides access levels — e.g., sharing a Google Drive folder as editor/viewer/commenter |
| **RBAC** (Role-Based Access Control) | Access is tied to a user's organizational role — e.g., marketing staff can see analytics but not network admin tools |

### Access Control Technologies

Authentication and authorization usually feel seamless to users because the underlying access control technologies are configured to work together. A typical IAM/AAA system includes: a user directory, tools to manage that directory's data, an authorization system, and an auditing system. The real security value comes not just from having these tools, but from configuring them correctly to maintain a secure environment.

## Questions / Things to Revisit

- 

---
*Notes based on Google Cybersecurity Professional Certificate, Course 5 — Assets, Threats, and Vulnerabilities*
