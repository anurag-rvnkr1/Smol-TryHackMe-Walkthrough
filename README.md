# Smol — TryHackMe Walkthrough

<p align="center">
  <strong>WordPress LFI → Plugin Backdoor → RCE → Lateral Movement → Root</strong><br>
  A portfolio-ready security assessment of the <a href="https://tryhackme.com/room/smol">TryHackMe Smol</a> room.
</p>

> A structured, original write-up built from the supplied lab evidence. Flags and recovered secrets are intentionally hidden for plagiarism-resistant portfolio publication.

## Repository description

**Professional TryHackMe Smol CTF write-up covering WordPress reconnaissance, jsmol2wp LFI, hidden PHP backdoor discovery, RCE, reverse-shell execution, credential-based lateral movement, SSH key reuse, encrypted backup analysis, and unrestricted sudo-based privilege escalation.**

## Suggested GitHub topics

`tryhackme` · `ctf` · `cybersecurity` · `penetration-testing` · `web-security` · `wordpress-security` · `lfi` · `rce` · `linux-privilege-escalation` · `red-team` · `ethical-hacking` · `security-research`

## Contents

| Path | Purpose |
|---|---|
| `Documentation/Documentation.md` | Full end-to-end technical report |
| `Documentation/Smol_CTF_Documentation.docx` | Professionally formatted Word document |
| `Documentation/Smol_CTF_Documentation.doc` | Legacy Word-compatible document |
| `Resources/notes.md` | Compact command and methodology reference |
| `docs/index.md` | Portfolio-facing GitHub Pages presentation |
| `docs/assets/img/` | Numbered, publication-safe visual evidence |
| `docs/assets/css/custom.scss` | Premium dark cybersecurity presentation layer |
| `docs/_config.yml` | Jekyll configuration for the `docs/` source |
| `.github/workflows/pages.yml` | GitHub Pages deployment workflow |
| `SECURITY.md` | Scope and responsible disclosure guidance |
| `CONTRIBUTING.md` | Documentation contribution guide |

## Attack chain at a glance

```text
Internet-facing HTTP service
        │
        ▼
WordPress discovery
        │
        ▼
jsmol2wp 1.07
        │
        ▼
LFI → wp-config.php
        │
        ▼
WordPress administration
        │
        ▼
Hello Dolly backdoor
        │
        ▼
RCE → www-data
        │
        ├──► DB hashes → diego
        │
        ├──► readable SSH key → think
        │
        ├──► backup ZIP → gege → xavi
        │
        └──► sudo ALL → root
```

## Methodology

The documentation follows the same evidence-driven sequence used in the lab: reconnaissance, service enumeration, web content discovery, plugin fingerprinting, initial exploitation, shell stabilization, credential discovery, lateral movement, archive analysis, and privilege escalation.

## Flag policy

Flag strings are deliberately replaced with `[REDACTED]` in the text and screenshots. This keeps the repository useful for interview discussion and portfolio review without turning it into an answer dump.

## Author

**Anurag Revankar**  
Cybersecurity | Penetration Testing | Security Automation
