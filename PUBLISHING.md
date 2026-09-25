# Publishing Guide

## 1. Copy the package into the repository

Use the included `Smol_publish_to_github.sh` or `Smol_publish_to_github.ps1` helper from one directory above the repository checkout.

## 2. Enable GitHub Pages

Set **Settings → Pages → Source** to **GitHub Actions**. The included workflow also requests Pages enablement during the deployment setup.

## 3. Push the documentation

```bash
git add .
git commit -m "docs: publish portfolio-grade Smol CTF documentation"
git push origin main
```

## 4. Apply repository metadata

Copy the description and topics from `Documentation/Repository_Metadata.md` into the repository's **About** section.

## 5. Validate publication safety

Before publishing, confirm that flags, recovered passwords, hashes and private SSH key material remain redacted.
