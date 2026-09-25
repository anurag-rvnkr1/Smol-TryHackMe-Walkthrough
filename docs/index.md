---
layout: default
title: "Smol — TryHackMe CTF Documentation"
description: "Portfolio-grade technical documentation for the TryHackMe Smol room."
---

<link rel="stylesheet" href="{{ '/assets/css/custom.css' | relative_url }}">

<div class="hero">
  <div class="hero-kicker">TRYHACKME / CTF / WEB + LINUX</div>
  <h1>SMOL</h1>
  <p class="hero-lead">WordPress LFI → hidden PHP backdoor → RCE → lateral movement → root.</p>
  <p class="hero-meta"><strong>Portfolio edition:</strong> evidence-driven, heavily documented, flags and secrets redacted.</p>
  <div class="hero-actions">
    <a class="btn" href="https://tryhackme.com/room/smol">Open Room</a>
    <a class="btn secondary" href="https://github.com/anurag-rvnkr1/Smol-TryHackMe-Walkthrough">Repository</a>
  </div>
</div>

<div class="callout warning"><strong>Publication-safe build.</strong> Flag strings, passwords, hashes and private-key material are intentionally hidden. Screenshots have been regenerated into numbered, redacted portfolio figures.</div>

## Attack chain

<div class="chain">
  <span>01 Recon</span><b>→</b><span>02 WordPress</span><b>→</b><span>03 LFI</span><b>→</b><span>04 Backdoor</span><b>→</b><span>05 RCE</span><b>→</b><span>06 Lateral Movement</span><b>→</b><span>07 Root</span>
</div>

## Executive summary

Smol is a compact multi-stage lab in which an exposed WordPress service becomes the first stepping stone into the operating system. The documented path combines a vulnerable plugin, configuration disclosure, a hidden PHP command-execution backdoor, reverse-shell handling, weak credential hygiene, an exposed SSH key, a legacy encrypted backup, and an unrestricted sudo rule.

The strength of the exercise is the transition between layers: web application discovery leads to application secrets; application secrets enable host access; host enumeration reveals further credentials; and local privilege configuration provides the final boundary crossing.

## Evidence-driven walkthrough

### 1. Reconnaissance

`nmap` reveals SSH on 22/tcp and HTTP on 80/tcp. The web service is associated with `www.smol.thm`.

![Network reconnaissance](assets/img/02-network-recon.svg)

### 2. WordPress discovery

Content discovery confirms the WordPress layout through `wp-admin`, `wp-content`, `wp-includes`, and `xmlrpc.php`.

![Web enumeration](assets/img/03-web-enumeration.svg)

### 3. Vulnerable plugin

WPScan identifies `jsmol2wp` version 1.07 under `wp-content/plugins/`.

![Plugin enumeration](assets/img/04-plugin-enumeration.svg)

### 4. LFI → `wp-config.php`

The `jsmol.php` handler is abused through the `query` parameter to reach the WordPress configuration file and establish the database context.

![LFI configuration disclosure](assets/img/05-lfi-wp-config-redacted.svg)

### 5. Hidden backdoor → RCE

The same file-read primitive exposes the Hello Dolly source. Encoded PHP logic reveals command execution through a `cmd` parameter.

![Backdoor source](assets/img/06-backdoor-source.svg)

![RCE confirmation](assets/img/07-rce-confirmation.svg)

### 6. Shell

The command primitive is converted into a reverse shell and stabilized for interactive work.

![Reverse shell](assets/img/08-reverse-shell.svg)

### 7. Lateral movement

The local database yields user hashes, a usable credential is recovered for `diego`, and the account chain continues through a readable SSH key and a historical WordPress backup.

![WordPress user database](assets/img/09-wp-user-db-redacted.svg)

![Diego password cracking](assets/img/10-diego-crack-redacted.svg)

![SSH key pivot](assets/img/11-ssh-key-redacted.svg)

![Backup transfer](assets/img/12-backup-transfer.svg)

![Backup password recovery](assets/img/13-backup-crack-redacted.svg)

![Xavi credentials](assets/img/14-xavi-config-redacted.svg)

### 8. Root

The final local check shows an unrestricted `(ALL : ALL) ALL` sudo rule for `xavi`. That rule provides arbitrary command execution as root.

![Privilege escalation](assets/img/15-privilege-escalation.svg)

## Findings matrix

| Area | Observation | Defensive priority |
|---|---|---|
| WordPress | Outdated vulnerable plugin | Patch/remove vulnerable components |
| Plugin integrity | Hidden PHP execution logic | Monitor and verify plugin integrity |
| Credentials | Reused credentials across trust boundaries | Enforce unique credentials |
| SSH | Readable private key | Restrict key permissions and ownership |
| Backups | Legacy archive contains active secrets | Encrypt and lifecycle-manage backups |
| Sudo | Full command delegation | Enforce least privilege |

## Technical toolkit

`nmap` · `ffuf` · `WPScan` · `mysql` · `John the Ripper` · `zip2john` · `Netcat` · `Python HTTP server` · standard Linux enumeration utilities

## Portfolio notes

This edition is deliberately answer-resistant: the methodology, decision points, command structure, and defensive interpretation remain visible while the exact values that solve the room are not.

**Full report:** [`Documentation/Documentation.md`](../Documentation/Documentation.md)  
**Quick reference:** [`Resources/notes.md`](../Resources/notes.md)
