# Infra Automation

Practicing infrastructure automation using Terraform, Ansible, Nginx, and GitHub Actions on DigitalOcean.

---

## Architecture

```
git push
    │
    ▼
GitHub Actions          ← triggers on every push
    ├──▶ Terraform       → provisions Droplet on DigitalOcean (blr1)
    └──▶ Ansible         → SSHes in, installs & configures Nginx
              │
              ▼
    DigitalOcean Droplet
    Ubuntu · Nginx · live
```

---

## Stack

| Tool | Role |
|---|---|
| **Terraform** | Create/destroy the server with code |
| **Ansible** | Configure the server — install packages, start services |
| **Nginx** | Web server — serves content on the Droplet |
| **GitHub Actions** | Runs Terraform + Ansible automatically on push |
| **DigitalOcean** | Cloud provider — region `blr1`, 1 vCPU / 512MB |

---

## What happens on `git push`

1. GitHub Actions picks up the push
2. Terraform runs `apply` → Droplet created, IP output
3. Ansible SSHes into the IP → installs Nginx, copies config, starts service
4. Site is live — no manual steps

---

## Key concepts I'm learning

- **IaC** — describe infrastructure in code, not clicks
- **Idempotency** — run Ansible playbook 10 times, same result
- **CI/CD** — automate the entire deploy, remove human steps
- **State** — Terraform tracks what exists in `terraform.tfstate`