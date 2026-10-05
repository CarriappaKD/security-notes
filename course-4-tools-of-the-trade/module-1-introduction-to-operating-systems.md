# Module 1: Introduction to Operating Systems

## What Is an Operating System?

An **operating system (OS)** is the software that manages a computer's hardware and software resources, making the computer run efficiently and stay user-friendly. It bridges the gap between humans and computers by translating user commands into binary code (0s and 1s) the hardware understands.

For a security analyst, understanding operating systems is essential for tasks like configuring system security, managing firewalls, setting security policies, and performing audits.

## Common Operating Systems

| OS | Openness | Notes |
|---|---|---|
| **Windows** | Closed-source | Common on personal and enterprise computers |
| **macOS** | Partially open-source | Common on personal and enterprise computers |
| **Linux** | Fully open-source | Especially important in security; some distributions are built specifically for security work |
| **ChromeOS** | Partially open-source | Derived from the fully open-source Chromium OS; common in education |
| **Android** | Open-source | Mobile OS |
| **iOS** | Partially open-source | Mobile OS |

## Operating Systems and Vulnerabilities

Security issues are inevitable across all operating systems — keeping the system and its components updated is a key part of protection.

> **Legacy operating system** — an outdated OS still in active use. Some organizations keep legacy systems running because the software they depend on isn't compatible with newer OS versions — common in industries relying on equipment with **embedded software** (software built into hardware components). Legacy systems are especially risky since they're no longer supported/patched, leaving them exposed to new threats.

Even fully updated operating systems can still become vulnerable to attack — staying current reduces risk but doesn't eliminate it.

## The OS's Core Role

The OS's primary job is to let other programs run efficiently by managing hardware — connecting applications to hardware so users can actually get things done.

### The Boot-Up Process

| Stage | What Happens |
|---|---|
| **1. Initial activation** | Pressing the power button activates either a **BIOS** or **UEFI** microchip |
| **2. Booting instructions** | The chip runs loading instructions — e.g., verifying hardware health — and finally activates the bootloader |
| **3. Starting the OS** | The **bootloader** (a software program) takes over and starts the operating system itself |

| Chip | Full Form | Notes |
|---|---|---|
| **BIOS** | Basic Input/Output System | Older systems; contains loading instructions |
| **UEFI** | Unified Extensible Firmware Interface | Modern replacement for BIOS; offers enhanced security features |

> **Why this matters for security:** BIOS is often **not scanned by antivirus software**, making it a soft target for malware. Understanding the boot process helps analysts:
> - **Identify vulnerable stages** — where malicious code could be injected
> - **Trace security events** — follow the flow from boot-up to application use to find where an incident originated
> - **Implement preventative measures** — e.g., ensuring firmware integrity, using secure boot technologies

### The Four-Part Task Completion Process

Once booted, completing any task on a computer follows this flow:

1. **User** — initiates something they want to accomplish
2. **Application** — the software the user interacts with to do it
3. **Operating system** — receives the request from the application, interprets it, and routes it to the right hardware components
4. **Hardware** — actually performs the processing

The output then flows back: **Hardware → OS → Application → User.** The OS's work isn't visible to the user, but it's critical to completing every task.

### Resource and Memory Management

The OS manages a computer's resources — allocating memory/CPU where needed among competing programs, and ensuring resources are properly allocated and de-allocated (mostly invisibly to the user). Tools like **Task Manager** let you view running tasks, memory, and CPU usage — useful for troubleshooting and **incident response**.

## Virtual Machines and Virtualization

**Virtualization** — using software to create virtual representations of physical machines. A **virtual machine (VM)** is a virtual version of a physical computer — it has its own virtual CPU, storage, and hardware, all software-defined rather than dedicated physical hardware. Multiple VMs can run on a single physical computer's hardware, with that hardware's resources shared across them.

### Benefits of VMs

| Benefit | Explanation |
|---|---|
| **Security** | VMs run as isolated "guests" on the host, separate from the host and from each other — a **sandbox** environment. This limits exposure if one VM is compromised. (Risk: malware can occasionally "escape" virtualization and reach the host — never fully trust a virtualized system.) |
| **Efficiency** | Multiple VMs can run simultaneously, making it easy to switch between environments — useful for streamlining tasks like testing and exploring different applications |

### Managing VMs

A **hypervisor** is the software used to manage multiple VMs — it connects virtual and physical hardware and allocates the host's shared resources across VMs.

**Other virtualization forms** (not OS-based): multiple virtual servers created from one physical server, or virtual networks built to more efficiently use physical network hardware.

## User Interfaces: GUI vs. CLI

A **user interface** is the program that lets a user control the OS's functions.

| Interface | Description |
|---|---|
| **GUI (Graphical User Interface)** | Icon- and visual-based — start menu, taskbar, desktop icons. Used on most personal computers and phones |
| **CLI (Command-Line Interface)** | Text-based — users type commands; no icons/graphics |

### Why CLI Matters for Security Analysts

- **Flexibility and power** — CLIs allow more customization and the ability to run multiple tasks at once, compared to GUIs
- **Relevance to the role** — security analysts commonly use the CLI for tasks like analyzing logs and authenticating users

**Advantages of CLI in cybersecurity:**
- **Efficiency** — once you know it, CLI handles multiple simultaneous requests faster than clicking through a GUI
- **History file** — the CLI keeps a record of every command run. This lets you verify past actions were correct, and — critically — trace an attacker's actions if you suspect a system has been compromised

## Questions / Things to Revisit

- 

---
*Notes based on Google Cybersecurity Professional Certificate, Course 4 — Tools of the Trade: Linux and SQL*
