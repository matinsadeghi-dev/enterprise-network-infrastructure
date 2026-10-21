# Publish this project to GitHub

## 1. Create a repository

1. Sign in to GitHub and create a new repository named `enterprise-network-infrastructure`.
2. For the easiest first upload, create it without a README, license or `.gitignore`, because those files are already included here.
3. Download and extract this project folder on your computer.

## 2. Initialize Git and commit all project files

Open a terminal inside the extracted `enterprise-network-infrastructure` directory. First ensure Git knows your preferred commit identity:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Use the email you want associated with your Git commits. Then run:

```bash
git init
git branch -M main
git add -A
git status
git commit -m "chore: publish network lab project and documentation"
```

Review `git status` before committing so you can confirm exactly which files will be published. `git add -A` includes additions, modifications and deletions under the project folder, except files ignored by `.gitignore`.

## 3. Push to GitHub

Replace the URL below with the repository URL shown by GitHub:

```bash
git remote add origin https://github.com/YOUR-USERNAME/enterprise-network-infrastructure.git
git push -u origin main
```

If `origin` already exists, inspect it with `git remote -v` rather than adding it a second time.

## 4. Enable GitHub Pages

1. Open the repository on GitHub.
2. Go to **Settings → Pages**.
3. Under the build/deployment source, choose **Deploy from a branch**.
4. Select branch **main** and folder **/(root)**, then save.
5. Wait for GitHub Pages to finish deploying; the published URL will appear on the Pages settings screen.

`index.html` is at the repository root, so it is the page entry point. The project uses no external libraries or build command.

## 5. Verify the public repository

- Ensure `README.md`, `index.html`, `assets/`, `docs/` and `packet-tracer/matin-network-lab.pkt` are visible.
- Open the Pages URL and check navigation, tables and the topology section.
- Confirm the address plan documented in `docs/ADDRESSING-PLAN.md`.
- Open `packet-tracer/matin-network-lab.pkt` in Packet Tracer and test DNS/HTTP from clients on both LANs before presenting it as verified.
- Do not publish credentials, private keys or tokens. Make sure the lab itself contains no information you intend to keep private.

## Suggested follow-up commits

If you prefer a more descriptive history, make later changes as separate commits, for example:

```text
feat: document all devices in the two-LAN topology
docs: add addressing and subnetting reference
docs: explain DHCP DNS HTTP and routing
fix: stabilize Web Server IP and repair DNS/DHCP settings
```

A first public release can reasonably use the single initial commit shown above. Update this repository whenever the Packet Tracer configuration changes so the website and documentation do not drift from the simulation.
