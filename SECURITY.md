# 🛡️ SECURITY.md

> **Security Policy — Smol TryHackMe Walkthrough**
>
> This repository documents the **TryHackMe Smol** Capture The Flag room through a professional penetration testing methodology. It is maintained as an educational cybersecurity portfolio project and follows responsible disclosure practices.

<div align="center">

# Smol — TryHackMe Walkthrough

### WordPress Security • Local File Inclusion • Remote Code Execution • Linux Privilege Escalation

**Professional Cybersecurity Portfolio Documentation**

![Security Policy](https://img.shields.io/badge/Security-Policy-success?style=for-the-badge\&logo=shield)
![Responsible Disclosure](https://img.shields.io/badge/Responsible-Disclosure-blue?style=for-the-badge)
![Portfolio](https://img.shields.io/badge/Cybersecurity-Portfolio-purple?style=for-the-badge)

</div>

---

# 📖 Table of Contents

* Security Overview
* Supported Repository Versions
* Responsible Disclosure
* Reporting Security Issues
* Scope
* Out of Scope
* Sensitive Information Policy
* Educational Use Policy
* Security Best Practices
* Dependency & Supply Chain Security
* GitHub Pages Security
* AI & Generated Asset Policy
* Legal Disclaimer
* Maintainer Information

---

# 🔐 Security Overview

This repository demonstrates offensive security techniques inside a **controlled TryHackMe laboratory environment**.

Its purpose is to teach:

* Penetration testing methodology.
* WordPress security assessment.
* Linux privilege escalation.
* Security reporting.
* GitHub portfolio presentation.

The repository **does not** contain usable exploits against public systems, live credentials, or challenge solutions intended for misuse.

---

# ✅ Supported Repository Versions

| Version                              | Supported           |
| ------------------------------------ | ------------------- |
| Latest `main` branch                 | ✅ Supported         |
| GitHub Pages documentation (`docs/`) | ✅ Supported         |
| Previous commits                     | ⚠️ Best effort only |
| Forks maintained by third parties    | ❌ Not supported     |

Always use the latest version of the repository for documentation and GitHub Pages.

---

# 🎯 Responsible Disclosure Policy

If you discover a security issue within this repository (documentation leak, exposed credential, secret, token, or accidental disclosure), please report it responsibly.

### Please report privately if the issue includes:

* API keys.
* Authentication tokens.
* SSH private keys.
* Passwords.
* Password hashes.
* Personally identifiable information.
* Cloud credentials.
* Secrets committed accidentally.

Do **not** publish sensitive information in GitHub Issues.

---

# 📬 Reporting Security Issues

When reporting an issue, include:

### Security Report Template

```text
Repository:
Smol-TryHackMe-Walkthrough

Issue Summary:

Affected File(s):

Risk Level:

Steps to Reproduce (if applicable):

Suggested Remediation:
```

Please provide enough information to reproduce the issue without exposing confidential information publicly.

---

# 📌 Scope

This security policy applies to:

| Included                       | Description             |
| ------------------------------ | ----------------------- |
| README.md                      | Repository landing page |
| Documentation/Documentation.md | Technical walkthrough   |
| Resources/notes.md             | Learning notes          |
| docs/index.md                  | GitHub Pages portfolio  |
| docs/assets/css/custom.scss    | Styling                 |
| SVG visual assets              | Portfolio illustrations |
| GitHub Actions workflow        | Pages deployment        |

---

# ❌ Out of Scope

The following are **not** supported vulnerability reports:

* TryHackMe room flags.
* Intended challenge solutions.
* Password guesses.
* Brute-force wordlists.
* Offensive payload modifications.
* Third-party WordPress vulnerabilities unrelated to this repository.
* Issues affecting TryHackMe infrastructure.

Please report platform vulnerabilities directly to the appropriate platform owner.

---

# 🔒 Sensitive Information Policy

This repository intentionally removes or redacts all sensitive material.

## Redacted Information

| Data Type              | Status     |
| ---------------------- | ---------- |
| Flags                  | ✅ Redacted |
| Passwords              | ✅ Redacted |
| Password Hashes        | ✅ Redacted |
| SSH Private Keys       | ✅ Redacted |
| Database Credentials   | ✅ Redacted |
| Authentication Cookies | ✅ Redacted |
| API Tokens             | ✅ Redacted |
| Secrets / Salts        | ✅ Redacted |

Public documentation replaces sensitive values with:

```text
[REDACTED]
```

---

# 🚫 What Will Never Be Published

The repository will never intentionally contain:

* Root flag values.
* User flag values.
* Real passwords.
* SSH private keys.
* Database passwords.
* Authentication secrets.
* Browser cookies.
* JWT tokens.
* Environment secrets.
* `.env` credentials.
* GitHub Personal Access Tokens.

If discovered accidentally, they will be removed immediately.

---

# 🎓 Educational Use Policy

The techniques documented in this repository are intended solely for:

* Cybersecurity education.
* Ethical hacking practice.
* Capture The Flag learning.
* Blue Team understanding.
* Security research.
* Portfolio demonstration.

Readers are responsible for ensuring all testing occurs only on systems they own or have explicit authorization to assess.

---

# ⚖️ Acceptable Use

You may:

* Study the documentation.
* Reproduce techniques inside legal lab environments.
* Use methodology for educational purposes.
* Reference reporting structure in your own portfolio.

You may **not** use this repository to:

* Attack public infrastructure.
* Target systems without authorization.
* Distribute malicious payloads.
* Bypass access controls on real systems.

---

# 🧠 Security Best Practices Demonstrated

The walkthrough encourages responsible offensive security practices.

### Web Security

* Service fingerprinting.
* Plugin enumeration.
* Version analysis.
* Local File Inclusion validation.

### Linux Security

* Principle of least privilege.
* Sudo auditing.
* Credential hygiene.
* SSH key management.

### WordPress Security

* Plugin inventory.
* Configuration review.
* Secure deployment awareness.
* Credential exposure prevention.

---

# 🛠️ Defensive Recommendations

The documentation also discusses defensive improvements.

## WordPress

* Keep plugins updated.
* Remove unused plugins.
* Disable unnecessary file editing.
* Restrict XML-RPC if unused.
* Monitor plugin integrity.

## Linux

* Review sudo permissions regularly.
* Rotate exposed credentials.
* Protect SSH keys with proper permissions.
* Remove historical backups containing secrets.

---

# 🧱 Dependency & Supply Chain Security

This repository contains primarily documentation and static assets.

## Included Technologies

| Component    | Purpose                      |
| ------------ | ---------------------------- |
| GitHub Pages | Static documentation hosting |
| Jekyll Theme | Site rendering               |
| SCSS         | Styling                      |
| Markdown     | Documentation                |
| SVG          | Visual illustrations         |

No runtime backend application is deployed.

---

## Third-Party Dependencies

Only trusted GitHub Pages components should be used.

Avoid adding:

* Remote JavaScript libraries without review.
* Tracking scripts.
* Obfuscated code.
* Cryptocurrency miners.
* Analytics requiring user data collection.

---

# 🌐 GitHub Pages Security

The portfolio site is intentionally static.

## Security Goals

* No authentication.
* No server-side processing.
* No databases.
* No user uploads.
* No cookies.
* No client-side secrets.

The Pages deployment should remain a read-only documentation site.

---

## GitHub Actions Security

The included workflow should only:

* Build documentation.
* Compile SCSS.
* Deploy Pages artifacts.

It should **never**:

* Store secrets in repository files.
* Echo tokens into logs.
* Publish sensitive artifacts.

---

# 🖼️ Visual Asset Security

All SVG illustrations included in `docs/assets/img/` are portfolio-safe.

Requirements:

* No embedded credentials.
* No hidden metadata containing secrets.
* No malicious JavaScript.
* No external resource loading.

SVG assets should remain static.

---

# 🤖 AI & Generated Content Policy

Some diagrams and illustrations may be AI-assisted.

Policy:

* AI-generated visuals must not contain copyrighted logos unless permitted.
* Technical explanations are reviewed for correctness.
* Sensitive information is manually redacted before publication.

AI-generated assets are used only for visualization and documentation.

---

# 🔍 Security Review Checklist

Before publishing a new version, verify:

* [x] No flags remain visible.
* [x] Passwords removed.
* [x] SSH keys removed.
* [x] Database credentials removed.
* [x] Markdown links verified.
* [x] Images reviewed for hidden secrets.
* [x] GitHub Pages builds successfully.
* [x] Workflow contains no exposed secrets.

---

# 🚨 Incident Response

If sensitive information is accidentally committed:

### Immediate Actions

1. Remove the sensitive content.
2. Rotate affected credentials.
3. Rewrite Git history if necessary.
4. Invalidate exposed secrets.
5. Publish a sanitized commit.

Never rely solely on deleting a file if secrets were committed previously.

---

# 📚 Security References

The techniques discussed relate to common security concepts including:

* OWASP Top 10
* MITRE ATT&CK
* WordPress Security Hardening
* Linux Privilege Escalation
* Responsible Disclosure Practices

Readers should consult official documentation for defensive implementation guidance.

---

# ⚠️ Legal Disclaimer

This repository is provided **for educational and research purposes only**.

The author does not authorize or encourage using these techniques against systems without explicit permission.

Users are solely responsible for complying with applicable laws, regulations, organizational policies, and platform rules.

---

# 👨‍💻 Maintainer

<div align="center">

## **Anurag Revankar**

Cybersecurity Researcher • Penetration Tester • Security Automation Enthusiast

Maintaining professional cybersecurity portfolio projects focused on offensive security, Active Directory, cloud security, AI-assisted SOC engineering, and penetration testing documentation.

</div>

---

# ⭐ Security Commitment

This repository is maintained with a focus on:

* Responsible disclosure.
* Technical accuracy.
* Secure documentation practices.
* Educational integrity.
* Recruiter-quality portfolio presentation.

If you discover a security concern within this repository, please report it responsibly so it can be addressed promptly.

---

<div align="center">

### 🛡️ Secure Documentation. Responsible Research. Ethical Hacking.

**Smol — TryHackMe Walkthrough**

*Professional Cybersecurity Portfolio Project by Anurag Revankar*

</div>
