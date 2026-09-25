# 🚀 PUBLISHING.md

> **Publication Guide for the Smol TryHackMe Walkthrough Repository**
>
> A complete deployment guide for publishing this project as a premium cybersecurity portfolio on **GitHub** and **GitHub Pages**. This document ensures the repository is presented professionally for recruiters, hiring managers, and the cybersecurity community.

---

## Overview

This repository is designed to function as both:

* A professional GitHub CTF repository.
* A fully deployed GitHub Pages cybersecurity portfolio.
* A long-form technical penetration testing report.
* A recruiter-friendly showcase project.

The publication workflow below preserves formatting, visuals, responsiveness, SEO, and GitHub Pages compatibility.

---

# Publication Checklist

Before making the repository public, verify the following:

| Item                                 | Status |
| ------------------------------------ | ------ |
| README completed                     | ✅      |
| Documentation completed              | ✅      |
| GitHub Pages (`docs/index.md`) ready | ✅      |
| CSS theme applied                    | ✅      |
| Images renamed professionally        | ✅      |
| Flags removed / redacted             | ✅      |
| Secrets removed                      | ✅      |
| LICENSE added (optional)             | ✅      |
| SECURITY.md added                    | ✅      |
| CONTRIBUTING.md added                | ✅      |
| Repository Topics configured         | ✅      |

---

# Repository Metadata

## Repository Name

```text
Smol-TryHackMe-Walkthrough
```

## Repository Description

> Professional TryHackMe Smol penetration testing walkthrough covering WordPress reconnaissance, Local File Inclusion, Remote Code Execution, credential harvesting, lateral movement, SSH key abuse, backup archive analysis, and Linux privilege escalation. Portfolio-ready documentation with GitHub Pages support.

## Suggested Topics

```text
tryhackme
ctf
cybersecurity
penetration-testing
wordpress-security
web-security
linux
lfi
rce
privilege-escalation
ethical-hacking
security-research
```

---

# Recommended Repository Visibility

| Stage                | Recommendation |
| -------------------- | -------------- |
| While Building       | Private        |
| Final Portfolio      | Public         |
| Interview Submission | Public         |
| Recruiter Sharing    | Public         |

---

# Branch Strategy

```text
main
│
├── Production documentation
├── GitHub Pages deployment
└── Portfolio content
```

Use `main` as the publishing branch.

---

# Folder Structure

```text
Smol-TryHackMe-Walkthrough/
│
├── README.md
├── SECURITY.md
├── CONTRIBUTING.md
├── PUBLISHING.md
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
│
└── .github/
    └── workflows/
        └── pages.yml
```

---

# GitHub Pages Deployment

## Step 1 — Open Repository Settings

Navigate to:

```text
Repository
    ↓
Settings
    ↓
Pages
```

---

## Step 2 — Configure Build Source

Select:

| Setting | Value          |
| ------- | -------------- |
| Source  | GitHub Actions |
| Branch  | main           |
| Folder  | docs/          |

Do **not** select Deploy from Branch.

---

## Step 3 — Workflow

Use the included workflow.

```yaml
.github/workflows/pages.yml
```

The workflow automatically:

* Builds Jekyll.
* Compiles SCSS.
* Uploads Pages artifacts.
* Deploys the site.

---

# GitHub Pages Configuration

`docs/_config.yml`

Recommended configuration:

```yaml
title: Smol — TryHackMe Walkthrough

description: Professional WordPress CTF Walkthrough Portfolio

theme: jekyll-theme-hacker

markdown: kramdown

highlighter: rouge

plugins:
  - jekyll-feed
  - jekyll-seo-tag
  - jekyll-sitemap
```

---

# Custom Styling

Location:

```text
docs/assets/css/custom.scss
```

Features included:

* Dark hacker UI.
* Neon cyber typography.
* Responsive cards.
* Timeline styling.
* Code block improvements.
* Table styling.
* Mobile optimization.
* Animated badges.

---

# Homepage Configuration

Primary landing page:

```text
docs/index.md
```

The landing page includes:

* Hero banner.
* Statistics dashboard.
* Attack chain.
* Visual timeline.
* MITRE ATT&CK mapping.
* Evidence gallery.
* Findings section.
* Learning outcomes.
* Footer portfolio section.

---

# Images to Publish

## Publication-safe Evidence

| Image                         | Purpose                |
| ----------------------------- | ---------------------- |
| 01-cover-hero.svg             | Repository hero        |
| 02-network-recon.svg          | Reconnaissance         |
| 03-web-enumeration.svg        | Gobuster results       |
| 04-plugin-enumeration.svg     | WPScan plugins         |
| 05-lfi-wp-config-redacted.svg | LFI disclosure         |
| 06-backdoor-source.svg        | Hello Dolly payload    |
| 07-rce-confirmation.svg       | Command execution      |
| 08-reverse-shell.svg          | Reverse shell          |
| 09-wp-user-db-redacted.svg    | Database enumeration   |
| 10-diego-crack-redacted.svg   | Password cracking      |
| 11-ssh-key-redacted.svg       | SSH pivot              |
| 12-backup-transfer.svg        | Backup archive         |
| 13-backup-crack-redacted.svg  | ZIP password recovery  |
| 14-xavi-config-redacted.svg   | Historical credentials |
| 15-privilege-escalation.svg   | Root access            |

---

# Image Naming Convention

```text
01-cover-hero.svg
02-network-recon.svg
03-web-enumeration.svg
04-plugin-enumeration.svg
05-lfi-wp-config-redacted.svg
06-backdoor-source.svg
07-rce-confirmation.svg
08-reverse-shell.svg
09-wp-user-db-redacted.svg
10-diego-crack-redacted.svg
11-ssh-key-redacted.svg
12-backup-transfer.svg
13-backup-crack-redacted.svg
14-xavi-config-redacted.svg
15-privilege-escalation.svg
```

Keep names lowercase with hyphens.

---

# Screenshot Publication Policy

This repository intentionally **does not expose**:

* Challenge flags.
* Passwords.
* Password hashes.
* SSH private keys.
* API tokens.
* Database credentials.
* Cookies.
* Session identifiers.

Instead, screenshots use:

```text
[REDACTED]
```

This keeps the project plagiarism-resistant while preserving methodology.

---

# Markdown Best Practices

Use consistent heading hierarchy.

```markdown
# Main Title

## Phase

### Technique

#### Notes
```

Avoid skipping heading levels.

---

# Code Block Formatting

Always specify language.

````markdown
```bash
nmap -sV -Pn TARGET
```

```php
<?php
// sample code
?>
```
````

Supported languages:

* bash
* php
* sql
* yaml
* json
* python
* text

---

# SVG Graphics Policy

Portfolio graphics are preferred over raw screenshots.

Advantages:

* Responsive.
* Lightweight.
* Dark-mode compatible.
* Search-engine indexable.
* Professional appearance.

---

# GitHub README Optimization

The README should include:

* Hero banner.
* Badges.
* Overview.
* Skills table.
* Attack chain.
* Repository tree.
* Documentation links.
* MITRE ATT&CK mapping.
* Author section.

---

# SEO Optimization

Recommended keywords throughout documentation:

* TryHackMe Smol Walkthrough
* WordPress Security
* Local File Inclusion
* Remote Code Execution
* Linux Privilege Escalation
* Penetration Testing
* Cybersecurity Portfolio
* Ethical Hacking
* Capture The Flag
* Red Team Documentation

---

# Recruiter Portfolio Optimization

Highlight practical skills instead of challenge completion.

Example bullets:

* Conducted WordPress reconnaissance using industry-standard tooling.
* Identified vulnerable plugin enabling Local File Inclusion.
* Performed authenticated code execution through malicious plugin analysis.
* Executed Linux post-exploitation and privilege escalation workflow.
* Produced enterprise-style penetration testing documentation.

---

# Recommended Commit History

```text
docs: add professional README

docs: add penetration testing documentation

docs: add recruiter portfolio landing page

style: add custom cyber theme

docs: add visual evidence gallery

docs: redact flags and sensitive data

pages: configure GitHub Pages deployment
```

Clean commits improve repository presentation.

---

# Git Commands for Publishing

## Clone

```bash
git clone https://github.com/anurag-rvnkr1/Smol-TryHackMe-Walkthrough.git

cd Smol-TryHackMe-Walkthrough
```

## Add Documentation

```bash
git add .
```

## Commit

```bash
git commit -m "docs: publish premium Smol walkthrough portfolio"
```

## Push

```bash
git push origin main
```

---

# Verify GitHub Pages

Wait for the workflow to complete.

Expected URL:

```text
https://anurag-rvnkr1.github.io/Smol-TryHackMe-Walkthrough/
```

Verify:

* Hero banner loads.
* CSS loads.
* Images render.
* Navigation works.
* Mobile layout is responsive.

---

# Expected GitHub Pages Features

* Responsive landing page.
* Hacker-inspired interface.
* Smooth scrolling navigation.
* Syntax highlighted code.
* Interactive timeline.
* Evidence gallery.
* MITRE ATT&CK section.
* Findings dashboard.
* Footer portfolio section.

---

# Documentation Standards

This repository follows professional penetration testing reporting practices.

Sections included:

1. Executive Summary
2. Scope
3. Target Information
4. Reconnaissance
5. Enumeration
6. Exploitation
7. Initial Access
8. Post Exploitation
9. Lateral Movement
10. Privilege Escalation
11. Findings
12. MITRE ATT&CK Mapping
13. Lessons Learned

---

# Quality Assurance Checklist

## Technical Review

* All commands validated.
* Output formatted consistently.
* Timeline matches exploitation order.
* Secrets removed.
* Markdown linted.

## Visual Review

* SVG assets render correctly.
* Image numbering matches references.
* Responsive layout verified.

## Portfolio Review

* Recruiter-friendly language.
* Professional formatting.
* Clean repository structure.
* Original explanations.

---

# Responsible Disclosure Notice

This repository documents a **controlled TryHackMe laboratory environment**.

The techniques demonstrated are intended solely for:

* Security education.
* Capture The Flag practice.
* Ethical hacking training.
* Defensive security learning.

Do not use these techniques against systems without explicit authorization.

---

# Final Publication Checklist

* [x] README.md completed.
* [x] Documentation.md completed.
* [x] Word (.docx/.doc) documentation generated.
* [x] GitHub Pages configured.
* [x] CSS theme applied.
* [x] SVG evidence added.
* [x] Flags redacted.
* [x] Passwords removed.
* [x] SSH keys hidden.
* [x] Repository metadata configured.
* [x] SECURITY.md included.
* [x] CONTRIBUTING.md included.
* [x] PUBLISHING.md included.

---

<div align="center">

## ⭐ Repository Ready for Publication

**Smol TryHackMe Walkthrough** is now structured as a premium cybersecurity portfolio project suitable for GitHub, GitHub Pages, resumes, and recruiter submissions.

**Author:** **Anurag Revankar**

Cybersecurity • Penetration Testing • Security Research • Offensive Security Portfolio

</div>
