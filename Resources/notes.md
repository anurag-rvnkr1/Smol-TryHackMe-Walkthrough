# 📝 Resources / notes.md

> **Quick Reference Notes — TryHackMe Smol Walkthrough**
>
> A concise field guide containing reconnaissance commands, exploitation workflow, post-exploitation notes, privilege escalation checklist, MITRE ATT&CK mapping, defensive recommendations, and learning resources from the **TryHackMe Smol** room.
>
> **Portfolio Edition** — Flags, passwords, hashes, SSH keys, and sensitive values have been intentionally **redacted**.

---

# 📚 Room Summary

| Item        | Details                                                              |
| ----------- | -------------------------------------------------------------------- |
| Platform    | TryHackMe                                                            |
| Room        | Smol                                                                 |
| Difficulty  | Intermediate                                                         |
| Category    | WordPress / Linux Privilege Escalation                               |
| Focus Areas | LFI, WordPress Enumeration, RCE, Credential Access, Lateral Movement |
| Environment | Controlled CTF Lab                                                   |

---

# 🎯 Learning Objectives

This room demonstrates:

* Network reconnaissance.
* WordPress enumeration.
* Plugin vulnerability discovery.
* Local File Inclusion (LFI).
* WordPress configuration disclosure.
* Remote Code Execution.
* Reverse shell stabilization.
* Credential harvesting.
* SSH lateral movement.
* Linux privilege escalation.

---

# ⚔️ Attack Path Overview

```text
Target Enumeration
      │
      ▼
WordPress Discovery
      │
      ▼
Plugin Enumeration
      │
      ▼
LFI → wp-config.php
      │
      ▼
Admin Access
      │
      ▼
Hello Dolly Backdoor
      │
      ▼
Remote Code Execution
      │
      ▼
www-data Shell
      │
 ┌────┴────┐
 ▼         ▼
Hashes    SSH Keys
 │         │
 ▼         ▼
diego    think
 │         │
 ▼         ▼
Backup Archive
      │
      ▼
Additional Credentials
      │
      ▼
Root via sudo
```

---

# Phase 1 — Reconnaissance

## Nmap Enumeration

```bash
nmap -sC -sV -Pn TARGET_IP
```

Useful additions:

```bash
nmap -A TARGET_IP
nmap -p- TARGET_IP
nmap --script vuln TARGET_IP
```

### Enumeration Goals

* Identify exposed TCP ports.
* Detect web technologies.
* Identify SSH service.
* Identify HTTP server.
* Fingerprint operating system.

---

# Phase 2 — Web Enumeration

## Gobuster

```bash
gobuster dir \
-u http://TARGET_IP \
-w /usr/share/wordlists/dirb/common.txt
```

Common discoveries include:

* `/wp-admin`
* `/wp-login.php`
* `/robots.txt`
* `/wp-content`
* `/wp-includes`
* Plugin directories.

---

# Phase 3 — WordPress Enumeration

## WPScan

```bash
wpscan --url http://TARGET_IP --enumerate u,p,t
```

### Enumerated Information

* WordPress version.
* Installed plugins.
* Themes.
* Users.
* XML-RPC.
* Vulnerable plugin versions.

### Useful WPScan Options

```bash
wpscan --url http://TARGET_IP --plugins-detection aggressive
```

---

# Phase 4 — Local File Inclusion

## Target Plugin

The walkthrough identifies a vulnerable WordPress plugin allowing Local File Inclusion.

### LFI Goal

Access internal application files such as:

```text
wp-config.php
```

### LFI Indicators

* Arbitrary file inclusion.
* Directory traversal.
* PHP configuration disclosure.
* WordPress database credentials.

> **Sensitive output intentionally removed.**

---

# Phase 5 — WordPress Configuration Review

Important file discovered:

```text
wp-config.php
```

Interesting information obtained:

* Database name.
* Database user.
* Database password.
* Authentication salts.
* WordPress installation path.

### Security Impact

Misconfigured LFI can expose application secrets and authentication material.

---

# Phase 6 — Remote Code Execution

## Hello Dolly Plugin Analysis

A modified plugin contains hidden PHP code enabling remote command execution.

### RCE Verification

Typical verification command:

```bash
whoami
```

### Additional Enumeration

```bash
id
hostname
pwd
uname -a
```

---

# Phase 7 — Reverse Shell

## Listener

```bash
nc -lvnp 4444
```

## Reverse Shell Payload

Example payload category:

```bash
bash reverse shell
```

> Exact payload omitted.

---

## Shell Stabilization

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

Then:

```bash
export TERM=xterm
stty rows 40 columns 120
```

Useful improvements:

```bash
Ctrl + Z
stty raw -echo
fg
reset
```

---

# Phase 8 — Post Exploitation Enumeration

Useful commands:

```bash
whoami
id
hostname
pwd
ls -la
env
history
```

### Filesystem Enumeration

```bash
find / -type f 2>/dev/null
```

### Search Configuration Files

```bash
find / -name "*.conf" 2>/dev/null
```

---

# Phase 9 — Credential Discovery

Potential sources explored:

* WordPress database.
* wp-config.php.
* Backup archives.
* Home directories.
* SSH folders.

### Interesting Files

```text
~/.ssh/
authorized_keys
id_rsa
backup.zip
wp_users
```

All sensitive values removed.

---

# Phase 10 — Password Hashes

Database enumeration identifies WordPress password hashes.

### Offline Cracking Workflow

Typical tools:

```bash
john hashes.txt
hashcat hashes.txt wordlist.txt
```

Repository intentionally excludes:

* Hash values.
* Cracked passwords.
* Wordlists.

---

# Phase 11 — SSH Lateral Movement

SSH authentication performed using recovered credentials.

Useful commands:

```bash
ssh USER@TARGET_IP
```

Check permissions:

```bash
chmod 600 id_rsa
```

### SSH Enumeration

```bash
ls ~/.ssh
cat authorized_keys
```

Private keys are redacted.

---

# Phase 12 — Backup Archive Analysis

Useful tools:

```bash
zipinfo backup.zip
unzip backup.zip
```

Password recovery methodology documented separately.

Repository omits recovered password.

---

# Phase 13 — Linux Enumeration Checklist

## Users

```bash
cat /etc/passwd
```

## Groups

```bash
id
groups
```

## Sudo

```bash
sudo -l
```

## SUID

```bash
find / -perm -4000 -type f 2>/dev/null
```

## Writable Files

```bash
find / -writable -type f 2>/dev/null
```

## Capabilities

```bash
getcap -r / 2>/dev/null
```

---

# Phase 14 — Privilege Escalation

Primary enumeration command:

```bash
sudo -l
```

Technique documented:

* Misconfigured unrestricted sudo permissions.
* Privileged binary execution.
* Root shell acquisition.

### Verification

```bash
whoami
id
hostnamectl
```

Expected verification:

```text
root
```

---

# Useful Linux Enumeration Commands

## Operating System

```bash
cat /etc/os-release
uname -a
lsb_release -a
```

## Processes

```bash
ps aux
top
```

## Network

```bash
ss -tulpn
netstat -tulpn
ip a
ip route
```

## Scheduled Tasks

```bash
crontab -l
cat /etc/crontab
systemctl list-timers
```

---

# WordPress Enumeration Checklist

* [x] Version identified.
* [x] Users enumerated.
* [x] Plugins identified.
* [x] Themes identified.
* [x] XML-RPC reviewed.
* [x] Vulnerable plugin analyzed.
* [x] wp-config.php accessed via LFI.
* [x] Administrator access obtained.
* [x] Plugin backdoor analyzed.

---

# Post-Exploitation Checklist

* [x] Shell stabilized.
* [x] User enumeration completed.
* [x] Credentials harvested.
* [x] SSH pivot completed.
* [x] Backup archive investigated.
* [x] Additional users discovered.
* [x] Privilege escalation completed.

---

# MITRE ATT&CK Mapping

| ATT&CK Tactic        | Technique                            |
| -------------------- | ------------------------------------ |
| Reconnaissance       | Active Scanning                      |
| Initial Access       | Exploit Public-Facing Application    |
| Execution            | Command Shell                        |
| Persistence          | Server-Side Script                   |
| Credential Access    | Credentials from Configuration Files |
| Discovery            | File and Directory Discovery         |
| Lateral Movement     | SSH                                  |
| Collection           | Archive Collected Data               |
| Privilege Escalation | Abuse Elevation Control Mechanism    |

---

# Defensive Recommendations

## WordPress

* Update vulnerable plugins.
* Remove unused plugins.
* Restrict file inclusion.
* Protect wp-config.php.
* Monitor plugin integrity.

## Linux

* Review sudo privileges.
* Rotate exposed credentials.
* Protect SSH private keys.
* Remove historical backup files.
* Limit archive access permissions.

---

# Tools Used

| Tool            | Purpose                   |
| --------------- | ------------------------- |
| Nmap            | Service Enumeration       |
| Gobuster        | Directory Enumeration     |
| WPScan          | WordPress Enumeration     |
| Netcat          | Reverse Shell Listener    |
| Python          | TTY Stabilization         |
| John / Hashcat  | Offline Password Recovery |
| SSH             | Lateral Movement          |
| unzip / zipinfo | Backup Archive Analysis   |

---

# Learning Outcomes

After completing **Smol**, you should understand:

* WordPress penetration testing methodology.
* Local File Inclusion exploitation workflow.
* PHP backdoor discovery and analysis.
* Remote command execution validation.
* Reverse shell stabilization techniques.
* Credential harvesting methodology.
* SSH pivoting concepts.
* Linux privilege escalation enumeration.
* Professional penetration testing reporting practices.

---

# References

## Official Resources

* TryHackMe — Smol Room
* WordPress Security Documentation
* MITRE ATT&CK Framework
* GTFOBins
* OWASP Web Security Testing Guide

---

# Portfolio Notes

This repository is intentionally maintained as a **portfolio-quality cybersecurity project**.

### Redacted Items

* Flags.
* Passwords.
* Password hashes.
* SSH private keys.
* Database credentials.
* Authentication tokens.
* Sensitive archive contents.

### Repository Purpose

* Cybersecurity Portfolio.
* Ethical Hacking Learning.
* Penetration Testing Documentation.
* GitHub Pages Showcase.
* Recruiter-Friendly Project.

---

<div align="center">

## Smol — TryHackMe Walkthrough

**Quick Reference Notes**

Maintained by **Anurag Revankar**

Cybersecurity • Penetration Testing • Security Research

*Professional notes for study, review, and portfolio documentation.*

</div>
