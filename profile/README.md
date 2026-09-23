# 🧪 planday-labs

**Planday's experimental GitHub organisation** — for prototypes, proofs of concept, internal automation, and vibe-coded experiments.

Repositories here are separate from the production [`planday-corp`](https://github.com/planday-corp) organisation and are **not** subject to the same engineering or operational standards. That freedom comes with a responsibility: you're still accountable for the data your project touches.

---

## Getting started

1. **Link your GitHub account** to planday-labs via [Xero SSO](https://github.com/orgs/planday-labs/sso) (one-time setup — use `github.com/signup` first if you don't already have a personal account).
2. **Create a repository** through the [Self-Service Admin](https://github.com/planday-corp) wizard, which forks it from [`_labs-base`](https://github.com/planday-labs/_labs-base) and wires up CI/CD, Azure hosting, and DNS automatically.
3. **Ship it** — push to `main` and your app deploys to staging on every PR, and production on merge.

## What you get out of the box

Every app forked from `_labs-base` comes with:

- A **Container App** in both `labs-rg-staging` and `labs-rg-production`, reachable at `<app>.development.labs.planday.io` / `<app>.labs.planday.io` (VPN-only)
- **GitHub Actions** workflows that build, push to ACR, and deploy on every push — no manual steps
- **OIDC federated auth** to Azure, no stored secrets
- Its own **subnet, managed identity, and Application Insights** instance

The underlying infrastructure lives in [`azure-terraform-labs-infrastructure`](https://github.com/planday-corp/azure-terraform-labs-infrastructure).

## Data handling — the part that still matters

planday-labs isn't subject to production engineering standards, but it **is** still subject to Xero's Data Classification Standard. Before you build:

| Classification | Examples |
|---|---|
| 🔴 **Confidential** | Credentials, encryption keys, payment data |
| 🟠 **Sensitive** | Most customer or employee personal data |
| 🔵 **Internal** | Non-identifying internal information |
| 🟢 **External** | Safe to publish |

**Rule of thumb:** if your project touches customer or employee data, assume it's at least *Sensitive* until proven otherwise. Prefer synthetic, redacted, or de-identified data over the real thing wherever possible.

**Never**, regardless of classification:
- Commit secrets, tokens, or private keys to code, issues, PRs, or Action logs
- Copy production datasets into a repo or local files
- Send project data to third-party tools, AI tools, or SaaS products not approved for that data's classification

If you're unsure how to classify something, ask in **#hello-responsible-data-use** before proceeding — not after.

## Repositories

Browse the [repository list](https://github.com/orgs/planday-labs/repositories) — most are forks of `_labs-base` and follow the same structure and conventions.
