# Security Policy

## Purpose

This repository documents a controlled TryHackMe lab. The techniques described here are intended for authorized training environments only.

## Scope

The repository covers:

- WordPress reconnaissance and enumeration
- Local File Inclusion testing in the vulnerable `jsmol2wp` plugin
- Analysis of a PHP backdoor discovered within the lab WordPress installation
- Command execution and reverse-shell handling
- Credential and key discovery in a deliberately vulnerable environment
- Offline archive password recovery
- Linux privilege escalation through an overly permissive sudo rule

## Reporting

Because the target is a training room, findings are educational rather than production incident reports. Do not reuse the commands against systems without explicit authorization.

## Publication hygiene

Flags, recovered passwords, password hashes, and private SSH key material are intentionally redacted from this portfolio repository. Screenshots were regenerated into numbered publication-safe figures.

## Defensive interpretation

The write-up includes remediation-oriented observations so the same weaknesses can be recognized and prevented in real environments.
