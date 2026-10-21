# Commit plan

This repository is ready to be committed under your own Git identity. No GitHub account is connected in this workspace, so it has not been pushed to a remote repository and no commit is falsely attributed to your account.

## Initial commit

Run from the project root after configuring your Git name and email:

```bash
git init
git branch -M main
git add -A
git status
git commit -m "chore: publish network lab project and documentation"
```

## Optional follow-up commits

For a clearer history after your first commit, use focused messages such as:

```text
feat: document complete two-LAN topology

docs: add subnetting and addressing reference

docs: document DHCP DNS HTTP and static routing
fix: update confirmed device addresses
```

Before every commit, review `git diff` and `git status`. Do not commit credentials or unverified files that might contain secrets.
