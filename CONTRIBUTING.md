# 🤝 CONTRIBUTING.md

> **Contribution Guide for the Smol TryHackMe Walkthrough**
>
> Thank you for your interest in contributing to this repository. This project is maintained as a **professional cybersecurity portfolio** documenting the **TryHackMe Smol** Capture The Flag room through structured penetration testing methodology, technical reporting, and GitHub Pages documentation.

<div align="center">

### Smol • TryHackMe Walkthrough

**WordPress Security • LFI • RCE • Linux Privilege Escalation**

*Portfolio-quality cybersecurity documentation maintained with technical accuracy and responsible disclosure.*

</div>

---

# 📖 Table of Contents

* Project Philosophy
* Contribution Principles
* Repository Structure
* How to Contribute
* Documentation Standards
* Image & Asset Guidelines
* Markdown Style Guide
* Security & Responsible Disclosure
* Pull Request Guidelines
* Commit Convention
* Code of Conduct
* License & Attribution

---

# 🎯 Project Philosophy

This repository is **not** intended to be a simple answer dump for the Smol room.

Instead, it serves as a **professional penetration testing report** that demonstrates:

* Realistic reconnaissance methodology.
* WordPress security assessment techniques.
* Web exploitation workflow.
* Linux post-exploitation methodology.
* Professional reporting practices.
* GitHub Pages portfolio presentation.

The objective is educational documentation while protecting challenge integrity.

---

# 🛡️ Contribution Principles

All contributions should improve one or more of the following:

| Area                   | Examples                                                    |
| ---------------------- | ----------------------------------------------------------- |
| Documentation          | Grammar, clarity, technical explanation.                    |
| Cybersecurity Accuracy | Correct methodology, terminology, ATT&CK mapping.           |
| GitHub Pages UI        | Layout improvements, responsive fixes, accessibility.       |
| Visual Assets          | Better SVG illustrations, diagrams, timelines.              |
| Reporting              | Executive summaries, findings tables, remediation guidance. |

Contributions should maintain the project's professional tone and structure.

---

# 📂 Repository Structure

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
│       ├── css/
│       │   └── custom.scss
│       └── img/
│
└── .github/
    └── workflows/
        └── pages.yml
```

Please preserve this structure whenever possible.

---

# 🚀 How to Contribute

## 1. Fork the Repository

Fork this repository to your own GitHub account.

## 2. Clone Your Fork

```bash
git clone https://github.com/<your-username>/Smol-TryHackMe-Walkthrough.git
cd Smol-TryHackMe-Walkthrough
```

## 3. Create a Feature Branch

```bash
git checkout -b docs/improve-wordpress-analysis
```

Use descriptive branch names.

Examples:

```text
docs/update-readme
docs/improve-lfi-section
assets/new-svg-diagrams
style/github-pages-theme
fix/code-formatting
```

## 4. Make Your Changes

Examples include:

* Improve explanations.
* Add diagrams.
* Correct Markdown formatting.
* Improve accessibility.
* Refine ATT&CK mapping.

## 5. Commit Changes

```bash
git add .

git commit -m "docs: improve LFI explanation and attack timeline"
```

## 6. Push Your Branch

```bash
git push origin docs/improve-wordpress-analysis
```

## 7. Open a Pull Request

Describe:

* What changed.
* Why it changed.
* Screenshots if UI-related.
* Testing performed.

---

# 📝 Documentation Standards

Every documentation contribution should follow the repository reporting format.

## Required Section Order

1. Executive Summary
2. Target Overview
3. Reconnaissance
4. Enumeration
5. Exploitation
6. Initial Access
7. Post Exploitation
8. Lateral Movement
9. Privilege Escalation
10. MITRE ATT&CK Mapping
11. Lessons Learned

Avoid changing this flow unless necessary.

---

## Writing Style

Write documentation like a professional penetration testing report.

**Preferred**

> Enumerated the WordPress installation and identified a vulnerable plugin exposing a Local File Inclusion vector.

**Avoid**

> I hacked the website and got in.

Use:

* Passive or technical voice.
* Clear explanations.
* Professional cybersecurity terminology.
* Action-oriented reporting.

---

# 📚 Markdown Style Guide

## Headings

Use hierarchical headings.

```markdown
# Phase Title

## Technique

### Explanation

#### Notes
```

---

## Tables

Use Markdown tables for findings.

| Item          | Description               |
| ------------- | ------------------------- |
| Vulnerability | Local File Inclusion      |
| Severity      | High                      |
| Impact        | Sensitive File Disclosure |

---

## Code Blocks

Always specify language.

````markdown
```bash
nmap -sV -Pn TARGET
```

```php
<?php
echo "Example";
?>
```

```sql
SELECT * FROM wp_users;
```
````

Supported languages include:

* bash
* php
* python
* yaml
* json
* sql
* text

---

# 🎨 Image & Asset Guidelines

## Asset Location

```text
docs/assets/img/
```

---

## Naming Convention

Use numbered descriptive filenames.

| Asset        | Example                       |
| ------------ | ----------------------------- |
| Cover        | `01-cover-hero.svg`           |
| Recon        | `02-network-recon.svg`        |
| Enumeration  | `03-web-enumeration.svg`      |
| Exploitation | `07-rce-confirmation.svg`     |
| Root         | `15-privilege-escalation.svg` |

Rules:

* Lowercase.
* Hyphen-separated.
* Sequential numbering.
* SVG preferred over PNG.

---

## Screenshot Policy

Only include screenshots that explain methodology.

### Never Publish

* TryHackMe flags.
* Passwords.
* Password hashes.
* SSH private keys.
* API tokens.
* Session cookies.
* Database credentials.
* Secrets.

Replace sensitive information with:

```text
[REDACTED]
```

---

## SVG Illustration Guidelines

Preferred style:

* Dark cyber theme.
* Neon accent colors.
* Transparent background.
* Responsive vector graphics.
* GitHub Pages compatible.

---

# 🧪 Technical Contribution Guidelines

Improvements should preserve technical correctness.

### Examples of Good Contributions

* Better explanation of Local File Inclusion.
* Additional WordPress security references.
* Improved Linux privilege escalation notes.
* ATT&CK technique references.
* Defensive remediation recommendations.

### Avoid

* Publishing room flags.
* Publishing recovered passwords.
* Publishing SSH keys.
* Publishing complete exploit payloads without explanation.
* Publishing copyrighted material.

---

# 🕵️ Responsible Disclosure Policy

This repository documents a **controlled educational lab**.

Do **not** submit pull requests containing:

* Real credentials.
* Personally identifiable information.
* Malware.
* Unauthorized exploits targeting real systems.
* Active command-and-control payloads.

If sensitive content is discovered, open a private issue instead.

---

# 🛡️ Security Documentation Contributions

Security improvements are welcome for:

* Defensive explanations.
* Detection recommendations.
* Hardening guidance.
* WordPress remediation.
* Linux mitigation strategies.

Security policy details are available in **SECURITY.md**.

---

# 🌐 GitHub Pages Contributions

UI contributions are encouraged for:

* Responsive layouts.
* Timeline improvements.
* Cards.
* Hero section.
* Navigation.
* Accessibility.
* Performance.

Files commonly modified:

```text
docs/index.md
docs/assets/css/custom.scss
docs/_config.yml
```

---

# 📊 Visual Evidence Contributions

Every new illustration should include:

| Requirement                     | Status |
| ------------------------------- | ------ |
| SVG format preferred            | ✅      |
| Descriptive filename            | ✅      |
| Referenced inside documentation | ✅      |
| Dark theme compatible           | ✅      |
| Mobile responsive               | ✅      |

---

# 📖 Notes & Resources

`Resources/notes.md` should remain concise.

Use it for:

* Commands.
* Enumeration checklist.
* Tools used.
* Useful references.
* Learning notes.

Avoid duplicating the full walkthrough.

---

# 📌 Pull Request Checklist

Before submitting a PR, verify:

* [ ] Documentation builds correctly.
* [ ] Markdown renders without formatting issues.
* [ ] Internal links work.
* [ ] Images load correctly.
* [ ] GitHub Pages preview works.
* [ ] Sensitive information has been redacted.
* [ ] File names follow project conventions.

---

# 💬 Commit Message Convention

Use Conventional Commit style.

### Documentation

```text
docs: improve privilege escalation explanation
```

### Assets

```text
assets: add SVG attack chain illustration
```

### Styling

```text
style: improve GitHub Pages hero layout
```

### Fixes

```text
fix: correct WPScan plugin table formatting
```

### GitHub Pages

```text
pages: update Jekyll navigation styling
```

---

# 📋 Recommended Commit Examples

```text
docs: publish complete Smol walkthrough

docs: add MITRE ATT&CK mapping

assets: add reverse shell SVG illustration

style: redesign GitHub Pages timeline

fix: correct markdown formatting

security: expand remediation section
```

---

# 📚 Documentation Quality Requirements

Contributions should be:

* Technically accurate.
* Reproducible.
* Easy to follow.
* Professionally written.
* Portfolio appropriate.
* Grammar checked.
* Consistent with repository formatting.

---

# ⚖️ Code of Conduct

By contributing, you agree to:

* Be respectful.
* Provide constructive feedback.
* Keep discussions technical.
* Respect responsible disclosure.
* Avoid plagiarism.
* Credit original work when appropriate.

Harassment, spam, or malicious contributions will not be accepted.

---

# 📜 Attribution

If your contribution significantly improves this project, appropriate GitHub attribution will appear automatically through commits and pull requests.

Please preserve existing project credits and repository branding.

---

# 🎓 Intended Audience

This project is designed for:

* Cybersecurity students.
* Penetration testers.
* Red Team practitioners.
* Blue Team defenders.
* SOC analysts.
* Recruiters reviewing offensive security portfolios.
* GitHub portfolio visitors.

---

# ⭐ Thank You

Thank you for helping improve this cybersecurity documentation project.

Every meaningful contribution helps make this repository a stronger educational and portfolio resource for the security community.

---

<div align="center">

## Smol • TryHackMe Walkthrough

**Maintained by Anurag Revankar**

Cybersecurity • Penetration Testing • Security Research • Offensive Security Portfolio

*Professional documentation. Responsible disclosure. Continuous improvement.*

⭐ **If you found this repository useful, consider starring it on GitHub.**

</div>
