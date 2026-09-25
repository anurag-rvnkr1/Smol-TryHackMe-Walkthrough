# 🧩 Smol — TryHackMe Walkthrough

<div align="center">

<img src="docs/assets/img/01-cover-hero.svg" width="100%" alt="Smol TryHackMe Cover Banner"/>

### WordPress Exploitation • Local File Inclusion • Remote Code Execution • Linux Privilege Escalation

**A complete professional penetration testing walkthrough of the TryHackMe *Smol* Capture The Flag room.**

[![TryHackMe](https://img.shields.io/badge/TryHackMe-Smol-red?style=for-the-badge\&logo=tryhackme)](https://tryhackme.com/)
[![Writeup](https://img.shields.io/badge/Portfolio-CTF%20Writeup-blueviolet?style=for-the-badge)](#)
[![Linux](https://img.shields.io/badge/Linux-Ubuntu-E95420?style=for-the-badge\&logo=ubuntu)](#)
[![WordPress](https://img.shields.io/badge/WordPress-Security-21759B?style=for-the-badge\&logo=wordpress)](#)

</div>

---

## 📌 Overview

**Smol** is a realistic WordPress-focused Capture The Flag room that demonstrates how seemingly small web application weaknesses can evolve into complete system compromise.

The assessment follows an attacker's methodology from external reconnaissance through WordPress enumeration, plugin exploitation, remote command execution, credential harvesting, lateral movement, archive analysis, and finally unrestricted privilege escalation on a Linux host.

Unlike traditional writeups, this repository focuses on **methodology and technical understanding** rather than exposing challenge flags or sensitive credentials.

> **Flags, hashes, passwords, SSH keys, and other secrets have been intentionally redacted** to preserve academic integrity and prevent plagiarism.

---

# 🎯 Objectives

This walkthrough demonstrates practical offensive security techniques including:

* Network reconnaissance and service discovery.
* WordPress attack surface enumeration.
* Plugin fingerprinting and vulnerability analysis.
* Local File Inclusion (LFI).
* Extracting sensitive WordPress configuration securely.
* Identifying hidden malicious PHP backdoors.
* Remote Code Execution through authenticated WordPress access.
* Reverse shell deployment and stabilization.
* Password hash extraction and offline cracking methodology.
* SSH credential reuse.
* Backup archive analysis.
* Linux privilege escalation through misconfigured sudo permissions.
* Documentation and reporting practices.

---

# 🧠 Skills Demonstrated

| Domain               | Techniques                                   |
| -------------------- | -------------------------------------------- |
| Reconnaissance       | Nmap, Gobuster, HTTP Enumeration             |
| WordPress Security   | WPScan, Plugin Enumeration, User Enumeration |
| Web Exploitation     | Local File Inclusion, PHP Backdoor Analysis  |
| Post Exploitation    | Reverse Shell, Shell Stabilization           |
| Credential Access    | Hash Extraction, Offline Cracking            |
| Linux Enumeration    | User Enumeration, SSH Keys, Archives         |
| Privilege Escalation | Misconfigured sudo, Root Access              |
| Reporting            | Professional Penetration Test Documentation  |

---

# ⚔️ Attack Chain

```text
Internet Facing Web Server
            │
            ▼
      Service Enumeration
            │
            ▼
     WordPress Enumeration
            │
            ▼
 Vulnerable jsmol2wp Plugin
            │
            ▼
 Local File Inclusion
            │
            ▼
   wp-config.php Disclosure
            │
            ▼
 WordPress Administrator Access
            │
            ▼
 Hidden Hello Dolly Backdoor
            │
            ▼
 Remote Command Execution
            │
            ▼
        www-data Shell
            │
 ┌──────────┼──────────┐
 ▼          ▼          ▼
Database   SSH Key   Backup Archive
Hashes     Discovery   Discovery
 │            │            │
 ▼            ▼            ▼
diego       think       gege / xavi
            │
            ▼
 Privilege Escalation
            │
            ▼
           ROOT
```

---

# 🗂️ Repository Structure

```text
Smol-TryHackMe-Walkthrough/
│
├── README.md
├── SECURITY.md
├── CONTRIBUTING.md
│
├── Documentation/
│   ├── Documentation.md
│   ├── Smol_CTF_Documentation.docx
│   ├── Smol_CTF_Documentation.doc
│   ├── Repository_Metadata.md
│   └── Visual_Evidence_Index.md
│
├── Resources/
│   └── notes.md
│
├── docs/
│   ├── index.md
│   ├── _config.yml
│   └── assets/
│       ├── css/custom.scss
│       └── img/
│           ├── 01-cover-hero.svg
│           ├── 02-network-recon.svg
│           ├── ...
│           └── 15-privilege-escalation.svg
│
└── .github/workflows/pages.yml
```

---

# 🖼️ Visual Walkthrough

Every illustration has been redesigned into a **portfolio-safe SVG graphic** suitable for GitHub Pages.

| Stage                     | Asset                           |
| ------------------------- | ------------------------------- |
| Cover                     | `01-cover-hero.svg`             |
| Network Enumeration       | `02-network-recon.svg`          |
| Web Enumeration           | `03-web-enumeration.svg`        |
| Plugin Enumeration        | `04-plugin-enumeration.svg`     |
| LFI Discovery             | `05-lfi-wp-config-redacted.svg` |
| Backdoor Discovery        | `06-backdoor-source.svg`        |
| RCE Validation            | `07-rce-confirmation.svg`       |
| Reverse Shell             | `08-reverse-shell.svg`          |
| Database Enumeration      | `09-wp-user-db-redacted.svg`    |
| Password Cracking         | `10-diego-crack-redacted.svg`   |
| SSH Credential Access     | `11-ssh-key-redacted.svg`       |
| Backup Archive Analysis   | `12-backup-transfer.svg`        |
| Backup Password Recovery  | `13-backup-crack-redacted.svg`  |
| Additional Credentials    | `14-xavi-config-redacted.svg`   |
| Root Privilege Escalation | `15-privilege-escalation.svg`   |

---

# 🔍 Assessment Methodology

## Phase 1 — Reconnaissance

The target host was identified through TCP service enumeration.

Topics covered include:

* Port discovery.
* Service fingerprinting.
* HTTP identification.
* Operating system fingerprinting.

---

## Phase 2 — WordPress Enumeration

The WordPress installation was enumerated to identify:

* Installed plugins.
* WordPress version.
* Registered users.
* XML-RPC endpoint.
* Administrative paths.

---

## Phase 3 — Vulnerability Discovery

A vulnerable plugin exposed a Local File Inclusion vulnerability allowing access to internal application files.

The walkthrough explains:

* LFI mechanics.
* Secure validation methodology.
* Configuration disclosure impact.

---

## Phase 4 — WordPress Configuration Analysis

Sensitive configuration data was analyzed to understand authentication architecture without exposing credentials publicly.

Topics include:

* Database configuration.
* Authentication salts.
* WordPress filesystem layout.
* Database privilege implications.

---

## Phase 5 — Remote Code Execution

Administrative access led to analysis of a modified plugin containing an intentionally hidden PHP payload.

The documentation covers:

* Source code inspection.
* Payload decoding methodology.
* Command execution workflow.
* HTTP parameter abuse.

---

## Phase 6 — Initial Access

A reverse shell was deployed and stabilized.

Covered techniques:

* Shell generation.
* Listener setup.
* TTY stabilization.
* User context verification.

---

## Phase 7 — Credential Harvesting

Post-exploitation activities identified multiple credential sources including:

* WordPress database hashes.
* Local user accounts.
* SSH private keys.
* Backup archives.

No recovered passwords or hashes are published.

---

## Phase 8 — Lateral Movement

The walkthrough demonstrates secure methodology for moving between compromised accounts using legitimately recovered credentials during the lab.

Examples include:

* SSH authentication.
* Key reuse.
* User pivoting.
* Environment enumeration.

---

## Phase 9 — Backup Archive Analysis

A password-protected backup archive exposed historical WordPress content.

Topics include:

* Archive identification.
* Password recovery methodology.
* Configuration comparison.
* Historical credential discovery.

---

## Phase 10 — Privilege Escalation

The final phase documents Linux privilege escalation through sudo misconfiguration.

Topics include:

* sudo enumeration.
* Privileged binaries.
* Root shell acquisition.
* Verification procedures.

---

# 📚 Documentation Included

| File                          | Description                                            |
| ----------------------------- | ------------------------------------------------------ |
| `Documentation.md`            | Complete technical walkthrough with explanations.      |
| `Smol_CTF_Documentation.docx` | Professional report suitable for portfolio submission. |
| `Smol_CTF_Documentation.doc`  | Microsoft Word compatible version.                     |
| `notes.md`                    | Quick command reference and learning notes.            |
| `docs/index.md`               | Premium GitHub Pages cyber portfolio page.             |
| `Visual_Evidence_Index.md`    | Screenshot reference catalogue.                        |

---

# 🌐 GitHub Pages Preview

The repository includes a fully customized GitHub Pages portfolio featuring:

* Hacker-themed landing page.
* Attack timeline.
* Interactive navigation.
* SVG evidence gallery.
* Animated statistics.
* MITRE ATT&CK mapping.
* Findings dashboard.
* Responsive dark UI.

---

# 🧾 MITRE ATT&CK Mapping

| Tactic               | Technique                            |
| -------------------- | ------------------------------------ |
| Reconnaissance       | Active Scanning                      |
| Initial Access       | Exploit Public-Facing Application    |
| Execution            | Command Shell                        |
| Persistence          | Server-side Script                   |
| Credential Access    | Credentials from Configuration Files |
| Discovery            | Account Discovery                    |
| Lateral Movement     | SSH                                  |
| Collection           | Archive Collected Data               |
| Privilege Escalation | Abuse Elevation Control Mechanism    |

---

# 🛡️ Security Notice

This repository is intended for:

* Educational purposes.
* Blue Team learning.
* Penetration testing practice.
* CTF methodology.
* Portfolio demonstration.

It **does not publish** challenge flags, live credentials, SSH keys, hashes, or secrets.

---

# 🚀 Learning Outcomes

After completing this room, readers should understand:

* WordPress penetration testing methodology.
* LFI exploitation workflow.
* PHP payload analysis.
* Web shell identification.
* Reverse shell stabilization.
* Credential harvesting techniques.
* Linux privilege escalation fundamentals.
* Professional penetration test reporting.

---

# 📈 Portfolio Highlights

* ✅ End-to-end penetration testing workflow.
* ✅ Enterprise-style documentation.
* ✅ Recruiter-friendly formatting.
* ✅ GitHub Pages ready.
* ✅ SVG evidence illustrations.
* ✅ Plagiarism-safe publication.
* ✅ Modern cybersecurity portfolio presentation.

---

# 👨‍💻 Author

<div align="center">

## **Anurag Revankar**

Cybersecurity Researcher • Penetration Tester • Security Automation Enthusiast

Building practical cybersecurity projects focused on offensive security, defensive engineering, automation, Active Directory, cloud security, and AI-assisted SOC workflows.

**GitHub Portfolio:** `anurag-rvnkr1`

</div>

---

<div align="center">

### ⭐ If this project helped you learn something, consider giving the repository a star.

**Designed as a premium cybersecurity portfolio project.**

</div>
