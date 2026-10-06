# Module 2: The Linux Operating System

## Introduction to Linux

Linux was created in the early 1990s by **Linus Torvalds**, who developed the **Linux kernel** to improve on the existing UNIX operating system and make it open source. Around the same time, **Richard Stallman** worked on **GNU**, another UNIX-based OS, sharing Torvalds' vision of free and open software.

Linux is **open-source** — its source code is freely accessible, and anyone can use, share, and modify it under the **GNU Public License**. This philosophy fostered a large developer community that has produced over **600 different Linux distributions**.

As a security analyst, Linux is used to examine logs for system issues, verify access/authorization in identity management systems, and work with specialized distributions built for digital forensics or penetration testing.

## Linux Architecture

A task's request flows through this path: **User → Applications → Shell → Filesystem Hierarchy Standard (FHS) → Kernel → Hardware**.

| Component | Role |
|---|---|
| **User** | The person interacting with the computer, initiating/managing tasks. Linux is **multi-user** — multiple users can access the same resources simultaneously |
| **Applications** | Programs performing specific tasks. Typically installed via a **package manager** — a tool to install/manage/remove packages. A **package** is a piece of software that can combine with others to form an application |
| **Shell** | The command-line interpreter — translates text-based commands into instructions the kernel can execute, and relays the kernel's responses back |
| **Filesystem Hierarchy Standard (FHS)** | Organizes where data is stored in the OS. A **directory** is a file that organizes where other files live; the FHS defines how directories/contents are structured so the OS always knows where to find data |
| **Kernel** | Manages processes and memory, and routes commands between applications and hardware. Unique to Linux and critical for resource allocation |
| **Hardware** | The physical components — split into peripheral and internal |

### Hardware Categories

| Type | Description | Examples |
|---|---|---|
| **Peripheral** | Attached/controlled by the system but not core to running it; can be freely added/removed | Monitor, printer, keyboard, mouse |
| **Internal** | Required to run the computer; lives on or connects to the **motherboard** | CPU, RAM, hard drive |

| Internal Component | Function |
|---|---|
| **CPU (Central Processing Unit)** | The main processor; executes program instructions, enabling programs to run |
| **RAM (Random Access Memory)** | Short-term memory; stores data temporarily during active tasks. Cleared when the computer powers off. The CPU pulls data from RAM to run programs |
| **Hard drive** | Long-term memory; stores programs/files persistently, accessible even after a restart |

## Linux Distributions

Linux is highly customizable — its many versions are called **distributions**, **distros**, or **flavors**. The kernel is the shared core; its open-source nature lets anyone modify it to create new distros, each often built for a specific purpose. All distros trace back to a parent — e.g., **Red Hat** is the parent of **CentOS**, and **Debian** is the parent of **Ubuntu**, **Kali Linux**, and **Parrot**.

| Distribution | Based On | Purpose / Notes |
|---|---|---|
| **Kali Linux** | Debian | Built for **penetration testing** and **digital forensics**; comes pre-loaded with relevant tools. Recommended to run inside a VM to avoid system damage and allow reverting to prior states |
| **Ubuntu** | Debian | User-friendly, widely used in security and other industries; has both CLI and GUI; also popular for cloud computing |
| **Parrot** | Debian | Similar to Kali — pre-installed pen-testing/forensics tools; considered user-friendly thanks to an accessible GUI alongside its CLI |
| **Red Hat Enterprise Linux (RHEL)** | — | **Subscription-based**, built for enterprise use; not free, but includes dedicated customer support |
| **AlmaLinux** | Red Hat lineage | Community-driven; created as a **stable replacement for CentOS** after CentOS 8 (final stable release, Dec 2021) ended. Designed as a drop-in replacement so CentOS-compatible apps/configs keep working |

### Kali Linux Tooling

| Use Case | Tools |
|---|---|
| **Penetration testing** (simulating attacks to find vulnerabilities) | **Metasploit** (exploiting vulnerabilities), **Burp Suite** (web app weakness testing), **John the Ripper** (password guessing) |
| **Digital forensics** (collecting/analyzing data to understand what happened after an incident) | **tcpdump** (capturing network traffic), **Wireshark** (analyzing traffic via GUI), **Autopsy** (analyzing hard drives/smartphones) |

## Package Managers

A **package** is software that can combine with others to form a full application; packages include **dependencies** — supplemental files required for the app to run. A **package manager** installs, manages, and removes packages.

> Always use the most recent version of a package when possible — it carries the latest bug fixes and security patches.

### Package Managers by Distro Family

| Family | Package Manager | File Extension |
|---|---|---|
| **Red Hat-derived** (e.g., CentOS) | RPM (Red Hat Package Manager) | `.rpm` |
| **Debian-derived** (e.g., Kali, Ubuntu, Parrot) | dpkg | `.deb` |

### Package Management Tools (CLI-based, easier to use)

| Tool | Full Form | Works With |
|---|---|---|
| **APT** | Advanced Package Tool | Debian-derived distributions |
| **YUM** | Yellowdog Updater Modified | Red Hat-derived distributions (works with `.rpm` files) |

## Introduction to the Shell

The shell is the **command-line interpreter** — it's how you talk to the OS through the CLI. When you enter a command, the shell relays it to the **kernel** to execute, then returns the response. Think of it as a translator between you and your computer, since you don't speak binary directly.

### Common Linux Shells

| Shell | Full Form |
|---|---|
| **bash** | Bourne-Again Shell |
| **csh** | C Shell |
| **ksh** | Korn Shell |
| **tcsh** | Enhanced C Shell |
| **zsh** | Z Shell |

> **bash** is the default shell on most Linux distributions — user-friendly, usable for both basic commands and large projects, and the most popular shell in the cybersecurity profession.

### Shell Communication Flow

| Term | Meaning |
|---|---|
| **Standard input** | Information the OS receives via the command line — typically your keyboard input |
| **Standard output** | The OS's response, returned through the shell |
| **Standard error** | Error messages returned when the OS can't fulfill a command — due to typos, unknown commands, or insufficient permissions |

## Questions / Things to Revisit

- 

---
*Notes based on Google Cybersecurity Professional Certificate, Course 4 — Tools of the Trade: Linux and SQL*
