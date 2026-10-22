# Module 4: Threats to Asset Security

A **threat** is any circumstance or event that can negatively impact an asset. This module covers three major categories: social engineering, malware, and web-based exploits.

## Social Engineering

**Social engineering** is a manipulation technique that exploits *human error* — not sophisticated programming — to gain unauthorized access, information, or valuables. It bypasses security procedures by preying on natural human tendencies like curiosity, generosity, and excitement, which is exactly what makes it so effective and hard to fully prevent.

### Stages of a Social Engineering Attack

1. **Preparation** — the attacker researches the target to determine the best approach
2. **Establishing trust (pretexting)** — using gathered info and a disguise to build false trust
3. **Persuasion** — manipulating the target into revealing information, often using insider-sounding language
4. **Disconnection** — breaking contact once the information is obtained, to cover tracks

### Common Types of Social Engineering

| Type | Description |
|---|---|
| **Baiting** | Tempts someone into compromising security — e.g., USB baiting (plugging in a found infected drive) |
| **Phishing** | Digital communication (usually email) tricking someone into revealing data or installing malware |
| **Quid pro quo** | Promises a reward in exchange for access/info/money — e.g., a fake bank offer asking for account details |
| **Tailgating (piggybacking)** | An unauthorized person follows an authorized person into a restricted area |
| **Watering hole** | Compromising a website frequently visited by a specific target group (e.g., the 2020 Holy Water attack on religious/charity sites) |

### Prevention

- **Managerial controls** — policies, standards, procedures (e.g., patch management)
- **User awareness training**, focused on three habits:
  - Stay alert to suspicious communications/unknown senders (check spelling, sender address)
  - Be cautious sharing information, especially on social media
  - Control curiosity around "too good to be true" offers, attachments, or links
- **Technical layers** — firewalls, MFA, block lists, email filtering
- Security training should extend beyond employees to customers too

**Resources:** *OUCH!* (SANS Institute's free monthly newsletter) and *Scamwatch* (scam recognition/reporting resource).

## Phishing (In Depth)

Since phishing is the most common form of social engineering, it gets dedicated attention. A single compromised employee can give an attacker access to an entire organization's systems and data.

**Phishing kits** are pre-built toolsets that let low-skill attackers launch campaigns — bundling malicious attachments, fake data-collection forms, and fraudulent links disguised as trusted brands.

### Five Common Types of Phishing

| Type | Method |
|---|---|
| **Email phishing** | Messages impersonating a trusted person/entity, sent via email |
| **Smishing** | Phishing via SMS/text messaging platforms (iMessage, WhatsApp, etc.) |
| **Vishing** | Phishing via voice calls/voice messages |
| **Spear phishing** | Email phishing targeted at specific people (e.g., a company's accountants) |
| **Whaling** | Spear phishing aimed specifically at high-ranking executives |

**Recent trends:**
- **Targeted phishing** — highly customized attacks aimed at creating strong familiarity
- **Angler phishing** — impersonating customer service reps on social media

### Prevention

Anti-phishing policies, employee training, email filters (blocklists/allowlists), and intrusion prevention systems to monitor email traffic. There's no perfect fix — ongoing awareness is the best defense.

**Resources:** Google's phishing quiz, KnowBe4 (phishing trend reports), APWG — the Anti-Phishing Working Group (quarterly trend reports).

## Malware

**Malware** (malicious software) is designed to harm devices or networks — often spread via infected USB drives or online connections.

| Type | How it Works |
|---|---|
| **Virus** | Must be installed by the user before it spreads and causes damage — often via phishing links/attachments |
| **Worm** | Self-replicates and spreads across systems on its own once installed; often targets shared-access devices/files on a network |
| **Trojan** | Disguised as a legitimate file/program; tricks users into installing it, enabling spying, remote access, etc. |
| **Adware** | Legitimate ad-display software, but a malicious variant falls under **PUA** (potentially unwanted application) — bundled with legitimate programs, can slow devices or install other software |
| **Spyware** | Gathers/sells data without consent; also a PUA, commonly hidden in bundleware |
| **Scareware** | A PUA that frightens users into self-infecting via fake warnings, often via email/pop-ups |
| **Fileless malware** | Doesn't need installation — hijacks legitimate already-installed programs and lives in memory rather than on disk, making it harder to detect (requires memory analysis) |
| **Rootkit** | Grants remote administrative access; typically opens a backdoor for installing further malware. Often spread via a **dropper** (delivers/installs the malicious payload) or **loader** (downloads malicious code from an external source) |
| **Botnet** | A network of infected devices ("bots") controlled by a single attacker (the "bot-herder"), usually built via viruses/worms/trojans |
| **Ransomware** | Encrypts an organization's data and demands payment to restore access |

### Cryptojacking

A newer malware type that illegally mines cryptocurrency using a compromised device's resources, running in the background without consent.

- **Signs:** system slowdowns, high CPU usage, crashes, fast battery drain, unusually high electricity costs
- **Detection:** hard to spot directly, but intrusion detection systems (IDS) can flag abnormal activity
- **Prevention:** browser extensions/ad blockers, disabling JavaScript, staying current on trends

## Web-Based Exploits and Injection Attacks

These exploit coding flaws in web applications, often by inserting malicious code that runs silently in the background.

### Cross-Site Scripting (XSS)

Injects malicious code into a vulnerable website/application, often via HTML/JavaScript — can expose session cookies, geolocation, webcam/microphone access.

| XSS Type | How it Works |
|---|---|
| **Reflected** | Malicious script sent to the server and triggered in its response, often via a malicious link |
| **Stored** | Script injected directly onto the server — triggers the moment any user visits the infected page |
| **DOM-based** | Script lives in the loaded web page itself, often hidden in URL parameters |

### SQL Injection

Attackers manipulate database queries through **unsanitized user input** in fields like login forms, search bars, or comment boxes, to modify, delete, or steal data (or take control of an application).

| Category | How it Works |
|---|---|
| **In-band** | The same channel is used to launch the attack *and* retrieve results — e.g., a vulnerable search box returning stolen data directly in its results |
| **Out-of-band** | A different channel is used to retrieve results — e.g., routing stolen data to an attacker-controlled external server. Uncommon, since it depends on specific server features being enabled |
| **Inferential** | The attacker can't see results directly, but infers them from the system's *behavior* (e.g., analyzing error messages to deduce database structure) |

**Prevention — "escaping" user input:**
- **Prepared statements** — execute SQL statements before passing user input into them
- **Input sanitization** — strips out input that could be interpreted as code
- **Input validation** — ensures input matches what the system expects

## Threat Modeling

The process of identifying assets, their vulnerabilities, and how each is exposed to threats — used proactively to reduce risk to a system or business process. Typically performed by a **DevSecOps** team (development, security, operations).

### The Threat Modeling Cycle

1. **Defining the scope** — inventory and classify the assets to protect
2. **Identifying threats** — both internal (e.g., malicious employees) and external (e.g., hackers)
3. **Characterizing the environment** — adopt an attacker's mindset to understand how users/partners interact with the system
4. **Analyzing threats** — review existing protections, identify gaps, rank threats by risk score
5. **Mitigating risk** — decide to avoid, transfer, reduce, or accept each risk
6. **Evaluating findings** — document results, apply fixes, record lessons learned for future cycles

Threat modeling should be built into every stage of the **SDLC** (software development lifecycle).

### Common Threat Modeling Frameworks

| Framework | Focus |
|---|---|
| **STRIDE** (Microsoft) | Identifies 6 attack vectors: **S**poofing, **T**ampering, **R**epudiation, **I**nformation disclosure, **D**enial of service, **E**levation of privilege |
| **PASTA** (Process of Attack Simulation and Threat Analysis) | A risk-centric, 7-stage process focused on finding evidence of viable threats |
| **Trike** | Open-source, security-centric — focuses on permissions, use cases, and privilege models |
| **VAST** (Visual, Agile, and Simple Threat) | Part of the automated ThreatModeler® platform — used to streamline/automate assessments |

### PASTA's Seven Stages (Example: a fitness app protecting customer data)

1. **Define business and security objectives** — e.g., protecting customer PII
2. **Define technical scope** — identify components to evaluate (data at rest/in use, network protocols, controls)
3. **Decompose the application** — build a data flow diagram with developers, note existing controls
4. **Perform threat analysis** — research current attack types relevant to the app, think like an attacker
5. **Perform vulnerability analysis** — investigate root causes of potential weaknesses
6. **Conduct attack modeling** — simulate attacks (attack trees) against real risks, e.g., SQL injection on a customer database
7. **Analyze risk and impact** — compile findings into risk management recommendations for stakeholders

## Questions / Things to Revisit

- 

---
*Notes based on Google Cybersecurity Professional Certificate, Course 5 — Assets, Threats, and Vulnerabilities*
