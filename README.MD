# Smart Home Automation Configuration

This repository contains the version-controlled configuration and automation files for our smart home ecosystem. It utilizes GitHub Actions for continuous integration (syntax validation) and automated deployment.

## Repository Architecture

* `.github/workflows/validate.yml` — Automated CI pipeline that validates yaml syntax before code merges.
* `configuration.yaml` — Main Home Assistant core configuration file.
* `automations.yaml` — Dedicated file containing active automation rules.
* `secrets.yaml` — **(Local Only)** Contains sensitive credentials. Automatically ignored by Git via `.gitignore`.

---

## Deployment Secrets (GitHub Settings)

To configure or update the deployment pipeline, the following encrypted secrets must be maintained under **Settings > Secrets and variables > Actions**:

* **DNS_NAME**: The base domain name only (e.g., `richardjanderson.uk`). Do not include `http://`, `https://`, or trailing slashes.
* **SECURE_TOKEN1**: The primary Long-Lived Access Token generated directly from the Home Assistant profile page to authorize API operations.
* **SECURE_TOKEN2**: The secondary or backup Long-Lived Access Token used for redundant failover automation pathways.
* **SECURITY_BYPASS**: A dedicated override token, header key, or configuration string used to bypass Cloudflare Access policies specifically for automated GitHub runner traffic.

---

## Local Development Workflow

To ensure local adjustments do not leak credentials or break live setups, always verify your tracking state locally before staging changes.

1. **Check Status:** Ensure `secrets.yaml` is never shown as a modified file ready for staging.
   ```bash
   git status