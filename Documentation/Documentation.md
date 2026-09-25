# 🛡️ Smol — TryHackMe Walkthrough

<div align="center">

![Cover](../docs/assets/img/01-cover-hero.svg)

# Professional Penetration Testing Walkthrough

### WordPress Exploitation • Local File Inclusion • Remote Code Execution • Linux Privilege Escalation

**Author:** Anurag Revankar

Cybersecurity Portfolio Project

TryHackMe — Smol

</div>

---

# Executive Summary

## Assessment Overview

This repository documents a complete penetration testing assessment of the **Smol** machine from the TryHackMe platform. The engagement follows a structured offensive security methodology that mirrors a real-world web application and Linux host compromise, beginning with external reconnaissance and ending with full administrative control of the target operating system.

Unlike traditional Capture The Flag writeups, this documentation has been rewritten as a **professional technical assessment report** suitable for cybersecurity portfolios, GitHub Pages, interview discussions, and learning purposes.

Throughout this report, sensitive challenge material—including flags, passwords, password hashes, SSH private keys, authentication salts, and secrets—has been intentionally removed or replaced with **`[REDACTED]`**.

The emphasis is placed on:

* Understanding attack methodology.
* Explaining vulnerability impact.
* Demonstrating offensive security workflow.
* Providing defensive recommendations.
* Producing enterprise-style documentation.

---

## Engagement Objectives

The primary objective of this assessment was to identify exploitable weaknesses within a WordPress-based target, obtain initial access through legitimate attack paths, perform post-exploitation enumeration, pivot across compromised users, and escalate privileges to obtain full administrative access.

### Security Objectives

| Objective                        | Result      |
| -------------------------------- | ----------- |
| Discover exposed services        | ✅ Completed |
| Identify web technologies        | ✅ Completed |
| Enumerate WordPress installation | ✅ Completed |
| Identify vulnerable plugin       | ✅ Completed |
| Exploit Local File Inclusion     | ✅ Completed |
| Obtain Remote Code Execution     | ✅ Completed |
| Establish reverse shell          | ✅ Completed |
| Harvest credentials              | ✅ Completed |
| Perform lateral movement         | ✅ Completed |
| Escalate privileges to root      | ✅ Completed |

---

# Assessment Scope

## Target Information

<table><table-row><table-cell width="220">**Target Platform**</table-cell><table-cell>TryHackMe</table-cell></table-row><table-row><table-cell>**Room Name**</table-cell><table-cell>Smol</table-cell></table-row><table-row><table-cell>**Assessment Type**</table-cell><table-cell>Black Box Web Application Assessment</table-cell></table-row><table-row><table-cell>**Operating System**</table-cell><table-cell>Linux</table-cell></table-row><table-row><table-cell>**Primary Technology**</table-cell><table-cell>WordPress CMS</table-cell></table-row><table-row><table-cell>**Attack Surface**</table-cell><table-cell>HTTP, SSH, WordPress Plugins</table-cell></table-row><table-row><table-cell>**Difficulty**</table-cell><table-cell>Intermediate</table-cell></table-row><table-row><table-cell>**Testing Environment**</table-cell><table-cell>Controlled CTF Laboratory</table-cell></table-row></table>

---

## Rules of Engagement

The assessment was conducted under controlled laboratory conditions within the TryHackMe environment.

Activities performed include:

* Passive reconnaissance.
* Active service enumeration.
* Web application enumeration.
* Vulnerability validation.
* Local File Inclusion exploitation.
* Authenticated WordPress analysis.
* Remote Code Execution.
* Linux post-exploitation.
* Privilege escalation.

No persistence mechanisms were installed beyond temporary shell access required for the exercise.

---

# Report Classification

<table><table-row><table-cell width="220">**Classification**</table-cell><table-cell>Educational / Portfolio</table-cell></table-row><table-row><table-cell>**Environment**</table-cell><table-cell>TryHackMe Controlled Lab</table-cell></table-row><table-row><table-cell>**Distribution**</table-cell><table-cell>Public GitHub Repository</table-cell></table-row><table-row><table-cell>**Sensitive Information**</table-cell><table-cell>Removed / Redacted</table-cell></table-row></table>

---

# Executive Attack Timeline

![Attack Timeline](../docs/assets/img/01-cover-hero.svg)

The compromise followed a multi-stage attack path beginning with reconnaissance of exposed services and ending with unrestricted root privileges.

```text
Internet Reconnaissance
        │
        ▼
HTTP Enumeration
        │
        ▼
WordPress Discovery
        │
        ▼
Plugin Enumeration
        │
        ▼
Local File Inclusion
        │
        ▼
wp-config.php Disclosure
        │
        ▼
Administrator Authentication
        │
        ▼
Hidden Plugin Backdoor
        │
        ▼
Remote Code Execution
        │
        ▼
Reverse Shell
        │
        ▼
Credential Harvesting
        │
        ▼
SSH Lateral Movement
        │
        ▼
Backup Archive Analysis
        │
        ▼
Privilege Escalation
        │
        ▼
ROOT ACCESS
```

---

# Attack Surface Overview

The initial reconnaissance revealed a relatively small external attack surface.

| Surface       | Security Observation                                            |
| ------------- | --------------------------------------------------------------- |
| HTTP Service  | WordPress application exposed publicly.                         |
| WordPress CMS | Administrative interfaces accessible.                           |
| Plugins       | Third-party plugin introduced exploitable attack surface.       |
| PHP           | Server-side execution exposed through vulnerable functionality. |
| SSH           | Service available after credential discovery.                   |

Although the exposed services appeared minimal, the combination of a vulnerable plugin and insecure credential management enabled complete host compromise.

---

# Risk Summary

<table><table-section header><table-row header><table-cell header>Finding</table-cell><table-cell header>Severity</table-cell></table-row></table-section><table-row><table-cell>Local File Inclusion in WordPress Plugin</table-cell><table-cell>🔴 High</table-cell></table-row><table-row><table-cell>Exposure of WordPress Configuration</table-cell><table-cell>🔴 High</table-cell></table-row><table-row><table-cell>Hidden PHP Backdoor</table-cell><table-cell>🔴 Critical</table-cell></table-row><table-row><table-cell>Remote Command Execution</table-cell><table-cell>🔴 Critical</table-cell></table-row><table-row><table-cell>Credential Harvesting from Database</table-cell><table-cell>🟠 High</table-cell></table-row><table-row><table-cell>SSH Key Exposure</table-cell><table-cell>🟠 High</table-cell></table-row><table-row><table-cell>Password-Protected Backup Containing Credentials</table-cell><table-cell>🟠 High</table-cell></table-row><table-row><table-cell>Unrestricted sudo Privileges</table-cell><table-cell>🔴 Critical</table-cell></table-row></table>

---

# MITRE ATT&CK Overview

The techniques demonstrated throughout this assessment align with several MITRE ATT&CK tactics.

| ATT&CK Tactic        | Technique Demonstrated               |
| -------------------- | ------------------------------------ |
| Reconnaissance       | Active Scanning                      |
| Initial Access       | Exploit Public-Facing Application    |
| Execution            | Command Shell                        |
| Persistence          | Server-Side Script Execution         |
| Credential Access    | Credentials from Configuration Files |
| Discovery            | Account Discovery                    |
| Lateral Movement     | SSH Authentication                   |
| Collection           | Archive Collection                   |
| Privilege Escalation | Abuse Elevation Control Mechanism    |

A complete ATT&CK mapping appears later in this document.

---

# Penetration Testing Methodology

This assessment follows a methodology similar to common industry penetration testing frameworks.

## Phase-Based Workflow

<table><table-section header><table-row header><table-cell header>Phase</table-cell><table-cell header>Description</table-cell></table-row></table-section><table-row><table-cell>Reconnaissance</table-cell><table-cell>Identify exposed services and technologies.</table-cell></table-row><table-row><table-cell>Enumeration</table-cell><table-cell>Gather information about WordPress, plugins, users, and directories.</table-cell></table-row><table-row><table-cell>Initial Exploitation</table-cell><table-cell>Exploit Local File Inclusion vulnerability.</table-cell></table-row><table-row><table-cell>Configuration Analysis</table-cell><table-cell>Extract WordPress configuration securely.</table-cell></table-row><table-row><table-cell>Code Execution</table-cell><table-cell>Validate server-side command execution.</table-cell></table-row><table-row><table-cell>Post Exploitation</table-cell><table-cell>Enumerate users, credentials, and filesystem.</table-cell></table-row><table-row><table-cell>Lateral Movement</table-cell><table-cell>Pivot using recovered credentials.</table-cell></table-row><table-row><table-cell>Privilege Escalation</table-cell><table-cell>Abuse insecure sudo configuration.</table-cell></table-row></table>

---

# Tools Used During Assessment

<table><table-section header><table-row header><table-cell header>Tool</table-cell><table-cell header>Purpose</table-cell></table-row></table-section><table-row><table-cell>Nmap</table-cell><table-cell>TCP service discovery and fingerprinting.</table-cell></table-row><table-row><table-cell>Gobuster</table-cell><table-cell>Directory and content enumeration.</table-cell></table-row><table-row><table-cell>WPScan</table-cell><table-cell>WordPress enumeration and vulnerability identification.</table-cell></table-row><table-row><table-cell>Netcat</table-cell><table-cell>Reverse shell listener.</table-cell></table-row><table-row><table-cell>Python</table-cell><table-cell>TTY shell stabilization.</table-cell></table-row><table-row><table-cell>John the Ripper / Hashcat</table-cell><table-cell>Offline password recovery methodology.</table-cell></table-row><table-row><table-cell>SSH</table-cell><table-cell>Lateral movement between compromised accounts.</table-cell></table-row><table-row><table-cell>zipinfo / unzip</table-cell><table-cell>Backup archive inspection.</table-cell></table-row></table>

---

# Reporting Standards

This report intentionally follows a penetration testing report format instead of a challenge walkthrough.

Each phase contains:

* Objective.
* Methodology.
* Commands executed.
* Technical explanation.
* Security impact.
* Defensive recommendations.
* Supporting visual evidence.

Every screenshot is referenced using numbered assets stored inside:

```text
docs/assets/img/
```

---

# Visual Evidence Index

The following figures are referenced throughout this documentation.

| Figure    | Description                     |
| --------- | ------------------------------- |
| Figure 1  | Attack Timeline / Cover         |
| Figure 2  | Network Enumeration             |
| Figure 3  | Gobuster Enumeration            |
| Figure 4  | WPScan Plugin Enumeration       |
| Figure 5  | LFI Exploitation                |
| Figure 6  | PHP Backdoor Analysis           |
| Figure 7  | RCE Validation                  |
| Figure 8  | Reverse Shell                   |
| Figure 9  | Database Credential Enumeration |
| Figure 10 | Password Recovery Workflow      |
| Figure 11 | SSH Pivot                       |
| Figure 12 | Backup Archive Discovery        |
| Figure 13 | Archive Password Recovery       |
| Figure 14 | Additional Credentials          |
| Figure 15 | Root Privilege Escalation       |

---

# Phase I — External Reconnaissance

---

## Objective

The first phase focused on identifying the publicly exposed attack surface without making assumptions about the target operating system or installed technologies.

The goals were to:

* Discover open ports.
* Identify network services.
* Fingerprint versions.
* Detect web technologies.
* Establish the initial attack vector.

---

## Network Enumeration

![Figure 2 — Network Enumeration](../docs/assets/img/02-network-recon.svg)

**Figure 2** illustrates the initial reconnaissance workflow performed against the target.

A TCP scan was executed to enumerate accessible services and identify listening applications.

### Commands Used

```bash
nmap -sC -sV -Pn TARGET_IP
```

Additional enumeration techniques included:

```bash
nmap -A TARGET_IP
nmap -p- TARGET_IP
```

### Why This Matters

Nmap combines version detection, default scripts, and service fingerprinting to quickly identify exposed services while minimizing assumptions about the environment.

During this phase the assessment identified:

* HTTP service exposed publicly.
* SSH service available.
* Linux-based host fingerprint.
* Apache/PHP technology stack indicators.
* WordPress application exposed over HTTP.

These findings established the foundation for the web application assessment performed in the next phase.

---

## Reconnaissance Findings

| Observation              | Impact                                                     |
| ------------------------ | ---------------------------------------------------------- |
| HTTP available           | Primary attack surface identified.                         |
| SSH accessible           | Potential lateral movement path after credential recovery. |
| Linux server fingerprint | Guides privilege escalation methodology.                   |
| Apache/PHP indicators    | Suggest WordPress or PHP-based application stack.          |
| WordPress discovered     | Enables CMS-specific enumeration tools.                    |

---

## Security Observation

The attack surface was intentionally small, but web applications often expose significantly larger logical attack surfaces than network scans reveal. Enumeration therefore shifted from infrastructure reconnaissance toward application-layer discovery in the next phase.

---

---

# 🌐 Phase II — Web Enumeration

> **Objective:** Enumerate the web application, identify publicly accessible resources, fingerprint the CMS, and locate potential attack vectors within the exposed WordPress installation.

---

## Phase Overview

After identifying an HTTP service during reconnaissance, the assessment shifted toward **application-layer enumeration**. The goal was to understand the structure of the website before attempting exploitation.

This phase focused on:

* Directory discovery.
* WordPress fingerprinting.
* Login surface identification.
* Plugin discovery.
* Administrative endpoints.
* Public information leakage.

Unlike vulnerability scanning, enumeration is designed to collect information that informs later exploitation while minimizing assumptions about the application's configuration.

---

## Figure 3 — Web Content Discovery

![Figure 3 — Gobuster Enumeration](../docs/assets/img/03-web-enumeration.svg)

**Figure 3** illustrates the initial directory enumeration performed against the target web application.

The directory scan identified publicly accessible endpoints that exposed the underlying WordPress installation and administrative functionality.

---

## Directory Enumeration Methodology

The assessment used a directory brute-force approach against the HTTP server.

### Command Used

```bash
gobuster dir \
-u http://TARGET_IP \
-w /usr/share/wordlists/dirb/common.txt \
-x php,txt,html
```

### Why Gobuster?

Gobuster helps identify:

* Hidden directories.
* Administrative portals.
* Backup files.
* Development resources.
* Plugin locations.
* Static assets.

This provides visibility into the application's structure without authenticated access.

---

## Enumeration Results

Several directories immediately indicated a WordPress deployment.

<table><table-section header><table-row header><table-cell header>Directory</table-cell><table-cell header>Purpose</table-cell><table-cell header>Security Observation</table-cell></table-row></table-section><table-row><table-cell>`/wp-admin/`</table-cell><table-cell>Administration Interface</table-cell><table-cell>Primary authentication portal.</table-cell></table-row><table-row><table-cell>`/wp-login.php`</table-cell><table-cell>WordPress Login</table-cell><table-cell>Credential attack surface.</table-cell></table-row><table-row><table-cell>`/wp-content/`</table-cell><table-cell>Plugins / Uploads</table-cell><table-cell>Plugin discovery target.</table-cell></table-row><table-row><table-cell>`/wp-includes/`</table-cell><table-cell>Core WordPress Libraries</table-cell><table-cell>Technology confirmation.</table-cell></table-row><table-row><table-cell>`/robots.txt`</table-cell><table-cell>Indexing Rules</table-cell><table-cell>Potential information disclosure.</table-cell></table-row></table>

---

## robots.txt Analysis

The `robots.txt` file often leaks administrative or development paths.

### Why Review robots.txt?

It may disclose:

* Administrative directories.
* Backup paths.
* Hidden application routes.
* Staging resources.
* Sitemap locations.

### Security Observation

Although `robots.txt` is not a vulnerability by itself, it frequently reveals resources attackers would otherwise need to enumerate.

**Risk:** Low

**Information Value:** Medium

---

## WordPress Fingerprinting

Several indicators confirmed the CMS.

### Indicators Identified

* WordPress login page.
* Standard directory layout.
* Plugin directory structure.
* Theme directory.
* WordPress asset paths.
* WordPress response headers.

### Security Importance

CMS identification enables targeted enumeration tools such as WPScan and vulnerability intelligence for installed plugins.

---

## Authentication Surface

The application exposed the standard WordPress authentication interface.

### Entry Points

<table><table-section header><table-row header><table-cell header>Endpoint</table-cell><table-cell header>Purpose</table-cell></table-row></table-section><table-row><table-cell>`/wp-login.php`</table-cell><table-cell>User authentication.</table-cell></table-row><table-row><table-cell>`/wp-admin/`</table-cell><table-cell>Administrative dashboard.</table-cell></table-row><table-row><table-cell>`/xmlrpc.php`</table-cell><table-cell>Remote WordPress functionality.</table-cell></table-row></table>

### Security Observation

The existence of multiple authentication mechanisms increases the application's exposed attack surface.

---

## Technology Stack Assessment

<table><table-section header><table-row header><table-cell header>Technology</table-cell><table-cell header>Purpose</table-cell></table-row></table-section><table-row><table-cell>Apache HTTP Server</table-cell><table-cell>Web server.</table-cell></table-row><table-row><table-cell>PHP</table-cell><table-cell>Server-side application runtime.</table-cell></table-row><table-row><table-cell>WordPress CMS</table-cell><table-cell>Content Management System.</table-cell></table-row><table-row><table-cell>MySQL / MariaDB</table-cell><table-cell>Backend database platform.</table-cell></table-row></table>

This stack informed subsequent enumeration decisions.

---

## Enumeration Findings Summary

<table><table-section header><table-row header><table-cell header>Finding</table-cell><table-cell header>Security Impact</table-cell></table-row></table-section><table-row><table-cell>WordPress CMS identified.</table-cell><table-cell>Target-specific tooling available.</table-cell></table-row><table-row><table-cell>Administrative login page exposed.</table-cell><table-cell>Authentication attack surface discovered.</table-cell></table-row><table-row><table-cell>Plugin directories publicly accessible.</table-cell><table-cell>Plugin enumeration possible.</table-cell></table-row><table-row><table-cell>robots.txt available.</table-cell><table-cell>Minor information disclosure.</table-cell></table-row></table>

---

## Security Assessment

The web application exposed a **typical WordPress attack surface**. While nothing immediately indicated compromise, plugin enumeration became the next logical objective because third-party plugins historically represent one of WordPress' highest-risk components.

---

# 🔎 Phase III — WordPress Enumeration

> **Objective:** Enumerate WordPress users, plugins, themes, XML-RPC functionality, and identify vulnerable components suitable for exploitation.

---

## Phase Overview

The assessment transitioned from generic web enumeration toward **CMS-specific reconnaissance** using WordPress-focused tooling.

Primary goals:

* Identify installed plugins.
* Detect plugin versions.
* Enumerate users.
* Detect XML-RPC availability.
* Identify vulnerable software versions.

---

## Figure 4 — WPScan Enumeration

![Figure 4 — Plugin Enumeration](../docs/assets/img/04-plugin-enumeration.svg)

**Figure 4** shows the WordPress enumeration workflow and vulnerable plugin discovery process.

---

## WPScan Methodology

### Enumeration Command

```bash
wpscan --url http://TARGET_IP --enumerate u,p,t
```

### Enumeration Categories

<table><table-section header><table-row header><table-cell header>Option</table-cell><table-cell header>Purpose</table-cell></table-row></table-section><table-row><table-cell>`u`</table-cell><table-cell>User enumeration.</table-cell></table-row><table-row><table-cell>`p`</table-cell><table-cell>Plugin enumeration.</table-cell></table-row><table-row><table-cell>`t`</table-cell><table-cell>Theme enumeration.</table-cell></table-row></table>

---

## Why WPScan?

WPScan specializes in WordPress reconnaissance.

Capabilities include:

* Plugin fingerprinting.
* Theme fingerprinting.
* User enumeration.
* Version detection.
* Vulnerability intelligence.

---

## Plugin Discovery

Enumeration identified several installed plugins.

### Security Importance

Plugins significantly expand the application's attack surface because:

* They introduce third-party PHP code.
* They may lag behind security updates.
* They often expose file inclusion or upload vulnerabilities.

One particular plugin became the focus of exploitation.

---

## Vulnerable Plugin Identification

The assessment identified the **jsmol2wp** plugin as an exploitable component.

### Security Observation

The detected version contained functionality vulnerable to **Local File Inclusion (LFI)**.

### Vulnerability Class

<table><table-section header><table-row header><table-cell header>Category</table-cell><table-cell header>Value</table-cell></table-row></table-section><table-row><table-cell>Component</table-cell><table-cell>WordPress Plugin</table-cell></table-row><table-row><table-cell>Vulnerability Type</table-cell><table-cell>Local File Inclusion</table-cell></table-row><table-row><table-cell>Attack Vector</table-cell><table-cell>HTTP Request Parameter</table-cell></table-row><table-row><table-cell>Authentication Required</table-cell><table-cell>No</table-cell></table-row><table-row><table-cell>Impact</table-cell><table-cell>Sensitive File Disclosure</table-cell></table-row></table>

---

## Why LFI Matters

A Local File Inclusion vulnerability allows an attacker to read files from the server's filesystem when input validation is insufficient.

Potential consequences include:

* Configuration disclosure.
* Credential disclosure.
* PHP source disclosure.
* Database information leakage.
* Authentication secret exposure.

---

## User Enumeration

WPScan successfully enumerated publicly discoverable WordPress users.

### Why Enumerate Users?

WordPress usernames can be used for:

* Credential attacks.
* Password reuse.
* Authentication targeting.
* Privilege analysis.

### Security Observation

Public usernames increase exposure if weak passwords or vulnerable plugins exist.

---

## XML-RPC Enumeration

The assessment reviewed XML-RPC availability.

### Why XML-RPC Matters

XML-RPC may enable:

* Remote publishing.
* Pingbacks.
* Authentication requests.
* Brute-force amplification.
* API functionality.

### Security Observation

Even when not directly exploited during this assessment, XML-RPC represents additional attack surface that defenders should evaluate.

---

## Theme Enumeration

The installed WordPress theme was fingerprinted.

### Why Themes Matter

Themes may contain:

* Vulnerable PHP templates.
* Exposed backups.
* Development artifacts.
* Upload functionality.

No direct exploitation path originated from the theme during this assessment.

---

## WordPress Version Analysis

Version fingerprinting helps determine:

* Known vulnerabilities.
* Plugin compatibility.
* Exploit availability.
* Security patch status.

### Assessment Finding

The application version aligned with the vulnerable plugin deployment identified earlier.

---

## Information Leakage Review

<table><table-section header><table-row header><table-cell header>Information</table-cell><table-cell header>Risk</table-cell></table-row></table-section><table-row><table-cell>WordPress Version</table-cell><table-cell>Medium</table-cell></table-row><table-row><table-cell>Plugin Versions</table-cell><table-cell>High</table-cell></table-row><table-row><table-cell>Usernames</table-cell><table-cell>Medium</table-cell></table-row><table-row><table-cell>XML-RPC Endpoint</table-cell><table-cell>Medium</table-cell></table-row><table-row><table-cell>Theme Information</table-cell><table-cell>Low</table-cell></table-row></table>

---

## Enumeration Findings Summary

<table><table-section header><table-row header><table-cell header>Finding</table-cell><table-cell header>Security Impact</table-cell></table-row></table-section><table-row><table-cell>WordPress installation fingerprinted.</table-cell><table-cell>CMS-specific attack surface identified.</table-cell></table-row><table-row><table-cell>Users successfully enumerated.</table-cell><table-cell>Authentication intelligence gathered.</table-cell></table-row><table-row><table-cell>Plugins identified.</table-cell><table-cell>Third-party attack surface expanded.</table-cell></table-row><table-row><table-cell>jsmol2wp plugin identified.</table-cell><table-cell>Primary exploitation vector discovered.</table-cell></table-row><table-row><table-cell>Plugin version vulnerable to LFI.</table-cell><table-cell>Initial access path confirmed.</table-cell></table-row></table>

---

## Security Analysis

This phase demonstrates a common real-world WordPress attack path:

1. Identify the CMS.
2. Enumerate plugins.
3. Match plugin versions against known vulnerabilities.
4. Validate exposure without authenticated access.
5. Select the lowest-complexity exploitation path.

Rather than attacking authentication directly, the assessment leveraged a vulnerable plugin to obtain sensitive configuration information, ultimately leading toward authenticated compromise.

---

# Blue Team Notes

### Detection Opportunities

* Monitor requests targeting plugin directories.
* Alert on abnormal access to PHP files inside plugins.
* Detect excessive WordPress enumeration requests.
* Log repeated requests to XML-RPC endpoints.

### Hardening Recommendations

* Disable unused plugins.
* Remove deprecated plugins immediately.
* Restrict directory listing.
* Hide version information where possible.
* Monitor plugin integrity using file integrity monitoring.

---

## Phase Conclusion

The reconnaissance and enumeration phases established a complete understanding of the application's attack surface. The vulnerable **jsmol2wp** plugin provided a direct path toward **Local File Inclusion**, making it the first confirmed exploitation vector of the assessment.

The next phase moves from information gathering into **active exploitation** by abusing the LFI vulnerability to retrieve the WordPress configuration file and expose sensitive application credentials.

---
---

# 🎯 Phase IV — Local File Inclusion (Initial Exploitation)

> **Objective:** Validate the Local File Inclusion vulnerability exposed by the vulnerable WordPress plugin and leverage it to access sensitive application configuration files without authentication.

---

## Phase Overview

The previous enumeration phase identified the **jsmol2wp** WordPress plugin as the primary attack surface. Version fingerprinting indicated that the plugin exposed functionality vulnerable to **Local File Inclusion (LFI)**.

LFI vulnerabilities occur when user-controlled input is incorporated into filesystem operations without proper validation or sanitization, allowing arbitrary local files to be read by the application.

This vulnerability became the **initial access vector** of the assessment.

---

## Figure 5 — Local File Inclusion Workflow

![Figure 5 — LFI Exploitation](../docs/assets/img/05-lfi-wp-config-redacted.svg)

**Figure 5** illustrates the exploitation path used to access the WordPress configuration file through the vulnerable plugin endpoint.

---

## Vulnerability Description

### Vulnerability Type

<table><table-row><table-cell width="220">**Category**</table-cell><table-cell>Local File Inclusion</table-cell></table-row><table-row><table-cell>**Affected Component**</table-cell><table-cell>jsmol2wp WordPress Plugin</table-cell></table-row><table-row><table-cell>**Authentication Required**</table-cell><table-cell>No</table-cell></table-row><table-row><table-cell>**Primary Impact**</table-cell><table-cell>Arbitrary Local File Disclosure</table-cell></table-row><table-row><table-cell>**Attack Vector**</table-cell><table-cell>HTTP Request Parameter</table-cell></table-row></table>

---

## Why LFI Is Dangerous

A Local File Inclusion vulnerability allows an attacker to read files that should never be exposed through the web application.

Potential targets include:

* Application configuration files.
* Password databases.
* Environment files.
* SSH configuration.
* PHP source code.
* Backup files.
* Log files.

For WordPress applications, one of the highest-value targets is:

```text id="iwjtja"
wp-config.php
```

---

## Exploitation Methodology

The vulnerable plugin accepted user-controlled file paths through an HTTP parameter.

Instead of serving intended plugin resources, insufficient validation allowed traversal into the WordPress filesystem.

### Security Objective

Read the application's configuration file without authentication.

### Validation Strategy

Rather than attempting code execution immediately, the assessment first confirmed:

1. File inclusion worked.
2. Arbitrary local paths were accessible.
3. PHP configuration files were readable.

This minimized unnecessary interaction while confirming exploitability.

---

## Configuration File Disclosure

Successful exploitation returned the contents of the WordPress configuration file.

### High-Value Information Retrieved

<table><table-section header><table-row header><table-cell header>Information Category</table-cell><table-cell header>Security Value</table-cell></table-row></table-section><table-row><table-cell>Database Host</table-cell><table-cell>High</table-cell></table-row><table-row><table-cell>Database Username</table-cell><table-cell>High</table-cell></table-row><table-row><table-cell>Database Password</table-cell><table-cell>Critical</table-cell></table-row><table-row><table-cell>Database Name</table-cell><table-cell>High</table-cell></table-row><table-row><table-cell>Authentication Salts</table-cell><table-cell>High</table-cell></table-row><table-row><table-cell>WordPress Table Prefix</table-cell><table-cell>Medium</table-cell></table-row><table-row><table-cell>Filesystem Configuration</table-cell><table-cell>Medium</table-cell></table-row></table>

---

## Security Impact Assessment

Exposing `wp-config.php` effectively compromises the trust boundary between the web application and its database.

An attacker gains knowledge of:

* Backend database credentials.
* Authentication mechanisms.
* Installation paths.
* Internal architecture.

This dramatically expands post-exploitation possibilities.

---

## Evidence Review

> **Figure 5** demonstrates configuration disclosure with all sensitive values replaced by **`[REDACTED]`**.

No passwords or salts are published in this repository.

---

## Security Observation

Configuration disclosure frequently leads to:

* Database compromise.
* Credential reuse attacks.
* Administrative account recovery.
* Session forgery in poorly configured deployments.

In this lab, configuration disclosure became the bridge toward authenticated WordPress compromise.

---

## Blue Team Recommendations

### Preventing LFI

* Validate user-controlled paths.
* Restrict file inclusion to approved directories.
* Remove directory traversal sequences.
* Disable unnecessary PHP include functionality.
* Keep plugins updated.

### Detection Opportunities

Monitor HTTP requests containing:

* `../`
* Encoded traversal sequences.
* Plugin file inclusion parameters.
* Requests for configuration files.

---

# 🧩 Phase V — WordPress Configuration Analysis

> **Objective:** Analyze exposed WordPress configuration data to understand authentication architecture and identify opportunities for post-exploitation.

---

## Understanding `wp-config.php`

The WordPress configuration file contains the application's most sensitive runtime configuration.

### Security Components

<table><table-section header><table-row header><table-cell header>Configuration Area</table-cell><table-cell header>Purpose</table-cell></table-row></table-section><table-row><table-cell>Database Configuration</table-cell><table-cell>Backend authentication.</table-cell></table-row><table-row><table-cell>Authentication Keys</table-cell><table-cell>Cookie integrity.</table-cell></table-row><table-row><table-cell>Table Prefix</table-cell><table-cell>Database schema mapping.</table-cell></table-row><table-row><table-cell>Debug Configuration</table-cell><table-cell>Error handling.</table-cell></table-row><table-row><table-cell>Filesystem Paths</table-cell><table-cell>Application layout.</table-cell></table-row></table>

---

## Database Architecture

The disclosed configuration confirmed:

* Backend relational database.
* WordPress authentication stored in database tables.
* User credentials managed through WordPress user tables.

This informed later credential harvesting methodology.

---

## Authentication Architecture

Rather than exposing passwords directly, WordPress stores password hashes inside its database.

### Relevant Concepts

* User authentication.
* Password hashing.
* Session cookies.
* Authentication salts.
* Cookie signing.

These concepts become important during credential harvesting.

---

## Security Assessment

Configuration disclosure alone is often enough to transition from:

**Information Disclosure**

to

**Credential Access**

This represents a significant privilege boundary crossing.

---

# 💀 Phase VI — Hidden Hello Dolly Backdoor Analysis

> **Objective:** Identify malicious functionality inside an installed WordPress plugin and understand how authenticated users could execute arbitrary operating system commands.

---

## Phase Overview

Following authenticated WordPress access, installed plugins were inspected manually.

One plugin contained additional PHP functionality beyond its expected purpose.

---

## Figure 6 — Hidden PHP Backdoor

![Figure 6 — Hello Dolly Backdoor Analysis](../docs/assets/img/06-backdoor-source.svg)

**Figure 6** shows the malicious functionality embedded inside the plugin source code.

Sensitive payload values have been removed.

---

## Why Plugin Review Matters

WordPress plugins execute server-side PHP.

Compromised plugins may provide:

* Web shells.
* Command execution.
* Persistence.
* Credential theft.
* Backdoors.

Manual inspection revealed unexpected PHP behavior inconsistent with the plugin's legitimate functionality.

---

## Code Review Methodology

The assessment reviewed:

* Plugin entry files.
* Included PHP modules.
* Request parameters.
* Conditional execution logic.

### Security Indicators

Unexpected behaviors included:

* Request parameter processing.
* Dynamic command handling.
* Shell invocation logic.
* Hidden execution path.

---

## Backdoor Behavior

The malicious functionality accepted externally supplied input and executed operating system commands.

### Security Characteristics

<table><table-row><table-cell width="220">**Execution Type**</table-cell><table-cell>Server-side PHP</table-cell></table-row><table-row><table-cell>**Authentication**</table-cell><table-cell>Authenticated WordPress Context</table-cell></table-row><table-row><table-cell>**Execution Context**</table-cell><table-cell>Web Server User</table-cell></table-row><table-row><table-cell>**Primary Impact**</table-cell><table-cell>Remote Command Execution</table-cell></table-row></table>

---

## Why This Is Critical

Remote Code Execution allows attackers to:

* Execute shell commands.
* Enumerate the operating system.
* Read files.
* Download payloads.
* Spawn reverse shells.
* Establish persistence.

This is considered a **Critical Severity** finding.

---

## Defensive Observations

The plugin appears to have been modified from its expected functionality.

Possible defensive indicators include:

* Unexpected PHP functions.
* Obfuscated code.
* Command execution functions.
* Suspicious HTTP parameters.

---

## Blue Team Detection

File Integrity Monitoring should alert on:

* Modified plugin files.
* Unexpected PHP changes.
* Plugin checksum mismatches.
* Unauthorized administrative plugin edits.

---

# ⚡ Phase VII — Remote Code Execution

> **Objective:** Validate command execution capability and establish operating system access through the vulnerable plugin.

---

## Figure 7 — Command Execution Validation

![Figure 7 — Remote Command Execution](../docs/assets/img/07-rce-confirmation.svg)

**Figure 7** demonstrates successful execution of operating system commands through the vulnerable PHP functionality.

---

## Validation Methodology

Rather than immediately launching a reverse shell, safe validation commands were executed.

### Initial Enumeration Commands

```bash id="b3a0ib"
whoami
id
hostname
pwd
uname -a
```

These commands establish:

* Execution context.
* Operating system.
* Current privileges.
* Working directory.

---

## Execution Context

The executed commands confirmed the process ran under the web server account.

### Why This Matters

The web server account usually has limited privileges.

Typical capabilities include:

* Reading web application files.
* Accessing plugin directories.
* Reading configuration files.
* Accessing uploads.

Privilege escalation generally requires additional weaknesses.

---

## Operating System Enumeration

Initial commands collected environmental information.

### Information Collected

<table><table-section header><table-row header><table-cell header>Enumeration Area</table-cell><table-cell header>Purpose</table-cell></table-row></table-section><table-row><table-cell>User Context</table-cell><table-cell>Privilege level.</table-cell></table-row><table-row><table-cell>Hostname</table-cell><table-cell>Target identification.</table-cell></table-row><table-row><table-cell>Kernel Version</table-cell><table-cell>Privilege escalation planning.</table-cell></table-row><table-row><table-cell>Filesystem Location</table-cell><table-cell>Application layout.</table-cell></table-row><table-row><table-cell>Operating System</table-cell><table-cell>Linux distribution fingerprint.</table-cell></table-row></table>

---

## Security Impact

Remote Code Execution transforms a web application vulnerability into operating system access.

This expands attacker capabilities beyond HTTP requests.

---

## Risk Rating

| Finding                  | Severity    |
| ------------------------ | ----------- |
| Remote Command Execution | 🔴 Critical |

---

# 🐚 Phase VIII — Initial Access (Reverse Shell)

> **Objective:** Upgrade command execution into an interactive shell suitable for post-exploitation and privilege escalation.

---

## Figure 8 — Reverse Shell Session

![Figure 8 — Reverse Shell](../docs/assets/img/08-reverse-shell.svg)

**Figure 8** illustrates the transition from one-off command execution into an interactive Linux shell.

---

## Why Reverse Shells Matter

Remote command execution executes isolated commands.

A reverse shell provides:

* Interactive terminal.
* Environment variables.
* Directory navigation.
* Process management.
* Long-running commands.

---

## Listener Setup

A listener was prepared before initiating shell execution.

```bash id="h32h6y"
nc -lvnp 4444
```

This waits for the target host to initiate a connection.

---

## Shell Stabilization

Once connected, the shell was upgraded into a fully interactive TTY.

### PTY Upgrade

```bash id="d2bypk"
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

### Environment Improvements

```bash id="agpz6u"
export TERM=xterm
stty rows 40 columns 120
```

---

## Benefits of Stabilization

| Improvement      | Reason                                       |
| ---------------- | -------------------------------------------- |
| Interactive Bash | Better usability.                            |
| Arrow Keys       | Command history.                             |
| Terminal Size    | Full-screen tools.                           |
| Signal Handling  | Improved shell behavior.                     |
| Text Editors     | Interactive applications function correctly. |

---

## Initial Post-Exploitation Checks

Immediately after stabilization, environmental validation was performed.

### Commands

```bash id="p4l87n"
whoami
id
pwd
hostname
env
```

### Objectives

* Verify current user.
* Verify group membership.
* Identify home directory.
* Inspect environment variables.

---

## Security Observation

Initial shell access was intentionally treated as **unprivileged** until privilege escalation was verified.

This reflects real-world engagement methodology where assumptions about privilege levels should never be made without validation.

---

## Blue Team Recommendations

### Detecting Reverse Shell Activity

Indicators include:

* Outbound connections from web server processes.
* Netcat execution.
* Bash spawning child processes.
* Python spawning `/bin/bash`.
* Unexpected TCP sessions originating from Apache or PHP.

### Mitigations

* Restrict outbound network connectivity.
* Disable unnecessary interpreters.
* Monitor process ancestry.
* Use EDR process monitoring.
* Audit PHP execution behavior.

---

# Phase Summary

This phase successfully transitioned the assessment from **web application exploitation** into **operating system compromise**.

The exploitation chain now includes:

<table><table-section header><table-row header><table-cell header>Stage</table-cell><table-cell header>Status</table-cell></table-row></table-section><table-row><table-cell>Local File Inclusion</table-cell><table-cell>✅ Successful</table-cell></table-row><table-row><table-cell>Configuration Disclosure</table-cell><table-cell>✅ Successful</table-cell></table-row><table-row><table-cell>Backdoor Discovery</table-cell><table-cell>✅ Successful</table-cell></table-row><table-row><table-cell>Remote Code Execution</table-cell><table-cell>✅ Successful</table-cell></table-row><table-row><table-cell>Reverse Shell</table-cell><table-cell>✅ Interactive Access Established</table-cell></table-row></table>

The assessment now proceeds into **post-exploitation enumeration**, where credentials, user accounts, SSH keys, and backup archives become the focus of the engagement.

---

---

# 🔐 Phase IX — Credential Harvesting

> **Objective:** Identify authentication material available after gaining initial access through the web server account and determine opportunities for lateral movement.

---

## Phase Overview

Once an interactive shell was established, the assessment transitioned into **post-exploitation reconnaissance**. The objective was to identify sensitive files, configuration artifacts, database credentials, SSH material, user accounts, and historical backups that could facilitate privilege escalation.

Credential harvesting is a critical phase because attackers frequently gain additional access not by exploiting new vulnerabilities, but by leveraging insecure credential storage practices.

---

## Figure 9 — WordPress Database Credential Enumeration

![Figure 9 — WordPress User Database](../docs/assets/img/09-wp-user-db-redacted.svg)

**Figure 9** illustrates the extraction and review of WordPress authentication records from the backend database. Usernames remain visible for educational context, while hashes and credentials have been removed.

---

## Enumeration Strategy

The assessment focused on identifying high-value credential sources.

### Primary Targets

<table><table-section header><table-row header><table-cell header>Location</table-cell><table-cell header>Purpose</table-cell></table-row></table-section><table-row><table-cell>WordPress Database</table-cell><table-cell>User password hashes.</table-cell></table-row><table-row><table-cell>`wp-config.php`</table-cell><table-cell>Database credentials.</table-cell></table-row><table-row><table-cell>User Home Directories</table-cell><table-cell>SSH keys and notes.</table-cell></table-row><table-row><table-cell>Backup Archives</table-cell><table-cell>Historical credentials.</table-cell></table-row><table-row><table-cell>Configuration Files</table-cell><table-cell>Application secrets.</table-cell></table-row></table>

---

## Filesystem Enumeration

The web server account was used to identify readable configuration files across the filesystem.

### Useful Enumeration Commands

```bash
find / -type f 2>/dev/null
find / -name "*.conf" 2>/dev/null
find / -name "*.php" 2>/dev/null
```

### Enumeration Goals

* Identify backup files.
* Locate WordPress configuration.
* Discover hidden application resources.
* Locate user home directories.

---

## WordPress User Table Analysis

The WordPress database stores user authentication data in dedicated tables.

### Information Retrieved

<table><table-section header><table-row header><table-cell header>Data</table-cell><table-cell header>Security Value</table-cell></table-row></table-section><table-row><table-cell>Username</table-cell><table-cell>High</table-cell></table-row><table-row><table-cell>Password Hash</table-cell><table-cell>Critical</table-cell></table-row><table-row><table-cell>Email Address</table-cell><table-cell>Medium</table-cell></table-row><table-row><table-cell>User Role</table-cell><table-cell>High</table-cell></table-row><table-row><table-cell>Registration Metadata</table-cell><table-cell>Low</table-cell></table-row></table>

---

## Security Impact

Even without plaintext passwords, password hashes enable:

* Offline password recovery.
* Password reuse attacks.
* Administrative account compromise.
* Lateral movement opportunities.

This finding significantly increased the attacker's authentication capability.

---

## Credential Sources Identified

<table><table-section header><table-row header><table-cell header>Source</table-cell><table-cell header>Purpose</table-cell></table-row></table-section><table-row><table-cell>Database Hashes</table-cell><table-cell>Offline cracking.</table-cell></table-row><table-row><table-cell>SSH Key Material</table-cell><table-cell>User authentication.</table-cell></table-row><table-row><table-cell>Backup Archive</table-cell><table-cell>Historical secrets.</table-cell></table-row><table-row><table-cell>Configuration Files</table-cell><table-cell>Database authentication.</table-cell></table-row></table>

---

## Security Observation

Many production compromises occur because sensitive credentials remain readable by low-privileged service accounts. Principle of Least Privilege would significantly reduce the impact of this vulnerability chain.

---

# 🔓 Phase X — Password Recovery Methodology

> **Objective:** Demonstrate responsible offline password recovery methodology without publishing recovered credentials.

---

## Phase Overview

Password hashes extracted from the WordPress database were analyzed offline. The goal was to recover reusable credentials while preserving challenge integrity.

---

## Figure 10 — Offline Password Recovery Workflow

![Figure 10 — Password Recovery Methodology](../docs/assets/img/10-diego-crack-redacted.svg)

**Figure 10** illustrates the password recovery workflow while removing the actual recovered password and hash values.

---

## Why Offline Cracking?

Offline recovery offers several advantages:

* No interaction with the target.
* No authentication attempts.
* Faster analysis.
* Wordlist testing.
* Rule-based password mutations.

---

## Methodology

### Hash Extraction

Hashes were exported from the WordPress user table into a local analysis file.

### Recovery Tools

Examples include:

```bash
john hashes.txt
```

or

```bash
hashcat hashes.txt wordlist.txt
```

### Security Principle

The assessment documents **methodology only**.

The following are intentionally omitted:

* Hash values.
* Password values.
* Wordlists used.
* Cracking duration.

---

## Account Recovery

A privileged WordPress-related account became available after password recovery.

### Security Importance

Recovered credentials enabled:

* Authenticated WordPress access.
* User pivoting.
* SSH authentication attempts.
* Lateral movement planning.

---

## Credential Reuse Observation

This lab demonstrates an important security lesson:

> Credentials reused across services dramatically increase attacker success after a single compromise.

---

## Blue Team Recommendations

### Password Security

* Enforce unique passwords.
* Require strong password policies.
* Use MFA for administrators.
* Monitor credential stuffing attempts.
* Rotate exposed credentials immediately.

---

## Detection Opportunities

* Multiple hash extraction attempts.
* Database export activity.
* Unauthorized database reads.
* Password file creation.

---

# 🔑 Phase XI — SSH Lateral Movement

> **Objective:** Pivot from the web server account into additional Linux user accounts using legitimately recovered authentication material.

---

## Phase Overview

After credential discovery, the assessment explored user home directories and SSH authentication material.

---

## Figure 11 — SSH Key Discovery

![Figure 11 — SSH Key Enumeration](../docs/assets/img/11-ssh-key-redacted.svg)

**Figure 11** demonstrates SSH key discovery and permission handling. The private key contents have been fully removed.

---

## SSH Enumeration Strategy

Target directories included:

```text
/home/*
~/.ssh/
```

### Interesting Files

<table><table-section header><table-row header><table-cell header>File</table-cell><table-cell header>Purpose</table-cell></table-row></table-section><table-row><table-cell>`id_rsa`</table-cell><table-cell>Private authentication key.</table-cell></table-row><table-row><table-cell>`authorized_keys`</table-cell><table-cell>Allowed public keys.</table-cell></table-row><table-row><table-cell>`known_hosts`</table-cell><table-cell>Previously contacted hosts.</table-cell></table-row><table-row><table-cell>`config`</table-cell><table-cell>SSH configuration.</table-cell></table-row></table>

---

## Permission Handling

Private keys require secure permissions before SSH authentication.

### Typical Permission Adjustment

```bash
chmod 600 id_rsa
```

---

## Authentication Workflow

Recovered credentials were used to authenticate to the SSH service.

### Benefits of SSH Access

* Stable shell.
* Full terminal.
* Persistent session.
* User-specific environment.
* Improved filesystem access.

---

## User Pivot

The assessment successfully pivoted into another Linux account using recovered authentication material.

### Security Significance

This demonstrates **Lateral Movement**.

No additional vulnerability was required.

Instead:

1. Credentials were harvested.
2. Credentials were reused.
3. Authentication succeeded.

---

## User Enumeration

After pivoting, additional reconnaissance included:

```bash
whoami
id
hostname
pwd
ls -la
```

### Objectives

* Verify new privilege level.
* Identify accessible files.
* Enumerate additional users.
* Search for escalation paths.

---

## Blue Team Recommendations

* Protect SSH private keys.
* Restrict file permissions.
* Rotate exposed keys.
* Disable unused keys.
* Enable SSH logging.

---

## Detection Opportunities

* New SSH sessions.
* Authentication using unusual keys.
* Login from unexpected users.
* SSH authentication from web server IP.

---

# 📦 Phase XII — Backup Archive Analysis

> **Objective:** Investigate historical backups for additional credentials, configuration data, and lateral movement opportunities.

---

## Phase Overview

Backup archives often contain historical application states and forgotten credentials.

The assessment identified a compressed archive containing WordPress-related information.

---

## Figure 12 — Backup Archive Discovery

![Figure 12 — Backup Archive Enumeration](../docs/assets/img/12-backup-transfer.svg)

**Figure 12** shows the discovery of a password-protected backup archive during filesystem enumeration.

---

## Why Backup Files Matter

Backup archives frequently contain:

* Database exports.
* Configuration files.
* User credentials.
* Source code.
* Historical secrets.

Improper backup storage is a common security weakness.

---

## Archive Enumeration

Useful inspection commands include:

```bash
zipinfo backup.zip
```

### Extraction

```bash
unzip backup.zip
```

The archive required authentication before extraction.

---

## Security Assessment

Password-protected archives improve security only if:

* Passwords are unique.
* Passwords are stored securely.
* Archive permissions are restricted.

Otherwise, archived credentials remain accessible after compromise.

---

# 🔓 Phase XIII — Archive Password Recovery

> **Objective:** Recover archive contents using offline methodology while preserving challenge integrity.

---

## Figure 13 — Archive Password Recovery Workflow

![Figure 13 — Archive Password Recovery](../docs/assets/img/13-backup-crack-redacted.svg)

**Figure 13** documents the recovery workflow while removing the recovered archive password.

---

## Methodology

Password recovery followed responsible offline analysis.

The documentation intentionally excludes:

* Password value.
* Recovery command output.
* Wordlists.

---

## Information Recovered

After extraction, the archive exposed historical WordPress resources.

### Interesting Findings

<table><table-section header><table-row header><table-cell header>Artifact</table-cell><table-cell header>Security Value</table-cell></table-row></table-section><table-row><table-cell>Historical Configuration</table-cell><table-cell>High</table-cell></table-row><table-row><table-cell>Credential References</table-cell><table-cell>High</table-cell></table-row><table-row><table-cell>Backup User Information</table-cell><table-cell>Medium</table-cell></table-row><table-row><table-cell>Application Files</table-cell><table-cell>Medium</table-cell></table-row></table>

---

## Security Observation

Historical backups frequently preserve credentials that administrators believe have been removed from production systems.

This significantly expands post-exploitation opportunities.

---

# 👥 Phase XIV — Additional User Discovery

> **Objective:** Identify additional user accounts and authentication opportunities discovered inside recovered application artifacts.

---

## Figure 14 — Historical Credential Discovery

![Figure 14 — Additional Credential Discovery](../docs/assets/img/14-xavi-config-redacted.svg)

**Figure 14** shows configuration analysis revealing additional authentication information while removing all sensitive values.

---

## Enumeration Strategy

The recovered backup was searched for:

* Usernames.
* Password references.
* SSH paths.
* Configuration files.
* Environment variables.

---

## Additional Accounts

Historical application configuration referenced another Linux user.

### Security Importance

Additional accounts may provide:

* Different filesystem permissions.
* Additional SSH keys.
* Sudo privileges.
* Configuration ownership.

---

## Lateral Movement Opportunities

The assessment reviewed:

* Home directories.
* SSH configuration.
* Backup ownership.
* Group memberships.

This expanded visibility across the Linux environment before privilege escalation.

---

## Security Assessment

Credential reuse between:

* WordPress,
* Backup archives,
* Linux users,

created multiple authentication paths after the initial compromise.

---

## Blue Team Recommendations

### Backup Security

* Encrypt backups.
* Store backups outside web-accessible directories.
* Rotate archive passwords.
* Remove outdated backups.
* Monitor backup file access.

### Credential Hygiene

* Never reuse passwords across services.
* Restrict configuration readability.
* Separate service accounts.
* Audit archived secrets regularly.

---

# Phase Summary

At this stage, the assessment achieved substantial post-exploitation success.

<table><table-section header><table-row header><table-cell header>Post-Exploitation Objective</table-cell><table-cell header>Status</table-cell></table-row></table-section><table-row><table-cell>WordPress database enumeration</table-cell><table-cell>✅ Completed</table-cell></table-row><table-row><table-cell>Password hashes recovered</table-cell><table-cell>✅ Completed</table-cell></table-row><table-row><table-cell>Offline password recovery methodology</table-cell><table-cell>✅ Completed</table-cell></table-row><table-row><table-cell>SSH key discovery</table-cell><table-cell>✅ Completed</table-cell></table-row><table-row><table-cell>User pivot via SSH</table-cell><table-cell>✅ Completed</table-cell></table-row><table-row><table-cell>Backup archive discovery</table-cell><table-cell>✅ Completed</table-cell></table-row><table-row><table-cell>Archive password recovery</table-cell><table-cell>✅ Completed</table-cell></table-row><table-row><table-cell>Additional credential discovery</table-cell><table-cell>✅ Completed</table-cell></table-row></table>

The engagement now possesses sufficient user-level access to begin **Linux privilege escalation** through misconfigured permissions and elevated execution paths.

---

---

# 👑 Phase XV — Linux Privilege Escalation

> **Objective:** Escalate from a compromised user account to full administrative (root) privileges through insecure privilege management.

---

## Phase Overview

After successfully pivoting across multiple user accounts and completing filesystem enumeration, the assessment shifted toward identifying privilege escalation opportunities available to the compromised Linux users.

Rather than exploiting a kernel vulnerability, this machine demonstrates a far more common real-world issue:

> **Improper privilege delegation through sudo configuration.**

Privilege escalation was achieved using functionality already available to an authenticated local user.

---

## Figure 15 — Privilege Escalation Workflow

![Figure 15 — Root Privilege Escalation](../docs/assets/img/15-privilege-escalation.svg)

**Figure 15** illustrates the final privilege escalation path from a low-privileged Linux account to unrestricted root access.

---

## Enumeration Strategy

Privilege escalation always begins with local enumeration.

### Primary Enumeration Commands

```bash
whoami
id
hostname
pwd
sudo -l
```

Additional checks included:

```bash
groups
find / -perm -4000 -type f 2>/dev/null
getcap -r / 2>/dev/null
```

### Enumeration Objectives

* Identify sudo permissions.
* Enumerate SUID binaries.
* Discover Linux capabilities.
* Review group memberships.
* Identify writable privileged paths.

---

## Sudo Enumeration

The most valuable discovery came from reviewing sudo permissions.

### Command

```bash
sudo -l
```

### Why `sudo -l` Matters

This command reveals:

* Commands executable as root.
* Password requirements.
* Run-as permissions.
* Environment restrictions.
* Misconfigured privilege delegation.

---

## Finding — Excessive sudo Permissions

The compromised user possessed permissions that exceeded the principle of least privilege.

### Security Classification

| Finding                   | Severity    |
| ------------------------- | ----------- |
| Excessive sudo delegation | 🔴 Critical |

### Impact

An authenticated user could execute privileged functionality that ultimately resulted in root command execution.

---

## GTFOBins Methodology

The assessment referenced documented privilege escalation techniques applicable to permitted binaries.

### Why GTFOBins?

GTFOBins documents legitimate Linux binaries that can be abused when executed with elevated privileges.

The methodology focused on:

* Existing sudo permissions.
* Expected binary behavior.
* Privileged shell spawning.

The exact binary used in the lab is intentionally not emphasized in this portfolio version.

---

## Privilege Escalation Validation

Successful execution resulted in a privileged shell.

### Verification Commands

```bash
whoami
id
hostnamectl
```

Expected verification output:

```text
root
uid=0(root)
```

---

## Root Context Verification

Additional verification confirmed unrestricted administrative access.

### Validation Areas

| Validation        | Purpose                           |
| ----------------- | --------------------------------- |
| `whoami`          | Current user context.             |
| `id`              | UID/GID verification.             |
| Filesystem Access | Root-only directories accessible. |
| Sudo Context      | Full administrative permissions.  |

---

## Security Impact Assessment

This represents a complete host compromise.

### Attacker Capabilities After Escalation

* Read any file.
* Modify system configuration.
* Create privileged users.
* Access SSH configuration.
* Persist across reboots.
* Disable security tooling.
* Extract sensitive application data.

---

## Risk Assessment

<table><table-section header><table-row header><table-cell header>Finding</table-cell><table-cell header>Severity</table-cell></table-row></table-section><table-row><table-cell>Privilege Escalation via sudo Misconfiguration</table-cell><table-cell>🔴 Critical</table-cell></table-row><table-row><table-cell>Complete Administrative Access</table-cell><table-cell>🔴 Critical</table-cell></table-row></table>

---

## Defensive Recommendations

### Sudo Hardening

* Grant only required commands.
* Remove unrestricted sudo access.
* Require authentication.
* Audit sudoers regularly.
* Monitor privileged command execution.

---

### Detection Opportunities

Monitor:

* `sudo -l`
* Privileged shell spawning.
* Unexpected root sessions.
* Sudo log entries.
* Privileged binary execution.

---

# 🏁 Root Access Summary

The assessment successfully completed the entire attack chain.

| Objective              | Status |
| ---------------------- | ------ |
| Initial Access         | ✅      |
| Remote Shell           | ✅      |
| Credential Harvesting  | ✅      |
| SSH Pivot              | ✅      |
| Backup Analysis        | ✅      |
| Additional User Access | ✅      |
| Root Access            | ✅      |

---

# 📊 Findings Summary Dashboard

## Executive Findings

| ID   | Finding                                             | Severity    |
| ---- | --------------------------------------------------- | ----------- |
| F-01 | WordPress Plugin Vulnerable to Local File Inclusion | 🔴 High     |
| F-02 | Exposure of `wp-config.php`                         | 🔴 High     |
| F-03 | Database Credential Disclosure                      | 🔴 High     |
| F-04 | Hidden PHP Backdoor Inside Plugin                   | 🔴 Critical |
| F-05 | Remote Code Execution                               | 🔴 Critical |
| F-06 | Password Hash Exposure                              | 🟠 High     |
| F-07 | SSH Private Key Exposure                            | 🟠 High     |
| F-08 | Password-Protected Backup with Credentials          | 🟠 High     |
| F-09 | Credential Reuse Across Services                    | 🟠 High     |
| F-10 | Excessive sudo Privileges                           | 🔴 Critical |

---

## Vulnerability Severity Matrix

| Severity         | Count |
| ---------------- | ----: |
| 🔴 Critical      |     3 |
| 🔴 High          |     4 |
| 🟠 Medium / High |     3 |
| 🟢 Low           |     0 |

---

## Attack Progression Summary

| Phase                 | Outcome                             |
| --------------------- | ----------------------------------- |
| Reconnaissance        | Target fingerprinted.               |
| Web Enumeration       | WordPress identified.               |
| WPScan                | Vulnerable plugin discovered.       |
| LFI                   | Configuration disclosure.           |
| Plugin Review         | Backdoor identified.                |
| RCE                   | Operating system commands executed. |
| Reverse Shell         | Interactive shell established.      |
| Credential Harvesting | Password hashes recovered.          |
| SSH Pivot             | Additional user compromised.        |
| Backup Analysis       | Historical credentials recovered.   |
| Privilege Escalation  | Root obtained.                      |

---

# 🎯 MITRE ATT&CK Mapping

## ATT&CK Coverage

| ATT&CK Tactic        | Technique Demonstrated               |
| -------------------- | ------------------------------------ |
| Reconnaissance       | Active Scanning                      |
| Resource Development | Credential Collection                |
| Initial Access       | Exploit Public-Facing Application    |
| Execution            | Command and Scripting Interpreter    |
| Persistence          | Server-Side Script                   |
| Privilege Escalation | Abuse Elevation Control Mechanism    |
| Defense Evasion      | Abuse Trusted Utilities              |
| Credential Access    | Credentials from Configuration Files |
| Discovery            | File and Directory Discovery         |
| Lateral Movement     | SSH                                  |
| Collection           | Archive Collected Data               |
| Impact               | Full System Compromise               |

---

## ATT&CK Timeline

```text
Reconnaissance
      │
      ▼
Initial Access
      │
      ▼
Execution
      │
      ▼
Credential Access
      │
      ▼
Discovery
      │
      ▼
Lateral Movement
      │
      ▼
Privilege Escalation
      │
      ▼
Full Host Compromise
```

---

# 🔵 Blue Team Defensive Recommendations

## WordPress Hardening

### Plugin Management

* Remove unused plugins.
* Keep plugins updated.
* Install only trusted plugins.
* Enable integrity monitoring.
* Disable plugin editing in production.

---

### Configuration Protection

Protect:

* `wp-config.php`
* Backup files.
* Environment variables.
* Upload directories.

Restrict filesystem permissions.

---

### Authentication Hardening

* Multi-factor authentication.
* Strong administrator passwords.
* Disable password reuse.
* Limit login attempts.
* Review administrator accounts regularly.

---

## Linux Hardening

### Least Privilege

* Remove unnecessary sudo rights.
* Separate service accounts.
* Restrict filesystem permissions.
* Protect SSH keys.

---

### SSH Security

* Disable unused accounts.
* Rotate exposed keys.
* Restrict root login.
* Monitor authentication logs.

---

### Backup Security

* Encrypt archives.
* Store backups outside the web root.
* Rotate archive passwords.
* Remove outdated backups.
* Restrict backup ownership.

---

## Monitoring Recommendations

### File Integrity Monitoring

Watch:

* WordPress plugins.
* Theme files.
* PHP files.
* `wp-config.php`.
* SSH configuration.

---

### Network Monitoring

Detect:

* Reverse shell connections.
* Unexpected outbound TCP traffic.
* Netcat execution.
* Bash child processes from Apache/PHP.

---

### Log Monitoring

Alert on:

* Repeated plugin access.
* Directory traversal attempts.
* XML-RPC abuse.
* sudo privilege enumeration.
* SSH authentication anomalies.

---

# 🧠 Lessons Learned

## Offensive Security Lessons

### Reconnaissance Matters

A small attack surface does not imply a secure application.

Application-layer enumeration exposed the vulnerable plugin responsible for the initial compromise.

---

### Third-Party Plugins Increase Risk

WordPress plugins dramatically expand attack surface.

Security depends on:

* Updates.
* Vendor trust.
* Code review.
* Plugin lifecycle management.

---

### Configuration Files Are High-Value Targets

Exposing `wp-config.php` compromises:

* Database credentials.
* Authentication secrets.
* Internal architecture.

Configuration disclosure should always be treated as a severe vulnerability.

---

### Credential Reuse Multiplies Impact

Recovered credentials enabled authentication across multiple services.

This demonstrates why password reuse is a major organizational risk.

---

### Least Privilege Prevents Escalation

The final compromise occurred because a user possessed unnecessary administrative capabilities.

Proper sudo design would have broken the attack chain.

---

# 🛡️ Defensive Security Lessons

## Web Application Security

* Validate file paths.
* Patch vulnerable plugins.
* Remove deprecated extensions.
* Monitor plugin integrity.

---

## Identity Security

* Rotate credentials.
* Enforce MFA.
* Separate administrator accounts.
* Audit authentication regularly.

---

## Infrastructure Security

* Restrict outbound traffic.
* Monitor shells spawned by web services.
* Audit sudo usage.
* Protect backups.

---

# 📈 Skills Demonstrated

## Technical Skills

| Domain               | Demonstrated Skill             |
| -------------------- | ------------------------------ |
| Reconnaissance       | Nmap, Gobuster                 |
| WordPress Security   | WPScan, Plugin Enumeration     |
| Web Exploitation     | Local File Inclusion           |
| PHP Security         | Backdoor Analysis              |
| Linux                | Shell Stabilization            |
| Credential Access    | Database Enumeration           |
| Authentication       | SSH Key Management             |
| Post Exploitation    | User Enumeration               |
| Privilege Escalation | sudo Abuse                     |
| Reporting            | Penetration Test Documentation |

---

## Security Concepts Reinforced

* OWASP Web Security.
* WordPress Hardening.
* Linux Privilege Escalation.
* Credential Hygiene.
* MITRE ATT&CK.
* Defense-in-Depth.
* Principle of Least Privilege.

---

# 🧾 Executive Conclusion

## Assessment Outcome

The **Smol** assessment demonstrates how a seemingly ordinary WordPress deployment can be completely compromised through a chain of independently understandable security weaknesses.

Beginning with external reconnaissance, the engagement identified a vulnerable third-party plugin that exposed a Local File Inclusion vulnerability. Configuration disclosure enabled authenticated access to sensitive application components, where a hidden PHP backdoor provided remote operating system command execution.

Post-exploitation activities recovered reusable authentication material from multiple sources, enabling lateral movement across Linux user accounts. Historical backups exposed additional configuration information, and the engagement concluded with full administrative compromise through excessive sudo permissions.

The attack chain highlights several recurring security themes frequently observed in real environments:

* Third-party component risk.
* Configuration exposure.
* Credential reuse.
* Insecure backup storage.
* Privilege misconfiguration.

Although performed within a controlled laboratory environment, the methodology mirrors realistic penetration testing workflows used during web application and Linux host assessments.

---

# 📚 Key Takeaways

* Complete end-to-end WordPress penetration testing workflow.
* Practical Local File Inclusion exploitation methodology.
* PHP backdoor identification and analysis.
* Remote Code Execution validation.
* Linux post-exploitation enumeration.
* Credential harvesting and lateral movement.
* Privilege escalation through sudo misconfiguration.
* Enterprise-style penetration testing reporting.

---

# 🎓 Portfolio Statement

This documentation was created as a **professional cybersecurity portfolio project**.

It emphasizes:

* Technical methodology.
* Responsible disclosure.
* Recruiter-friendly reporting.
* GitHub Pages compatibility.
* Original explanations and diagrams.
* Plagiarism-resistant publication.

All sensitive challenge artifacts—including flags, passwords, hashes, SSH keys, and secrets—have been intentionally removed or replaced with **`[REDACTED]`**.

---

<div align="center">

## Smol — TryHackMe Walkthrough

**Professional Penetration Testing Documentation**

**Author:** **Anurag Revankar**

Cybersecurity • Penetration Testing • Security Research • Offensive Security Portfolio

*Designed for GitHub, GitHub Pages, interview portfolios, and cybersecurity learning.*

</div>

* Figure 3 (`03-web-enumeration.svg`)
* Phase III — WPScan Enumeration Begins
