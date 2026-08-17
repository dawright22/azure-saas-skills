# git-ape

[![Git-Ape](https://github.com/Azure/git-ape/raw/main/APE.png)](https://github.com/Azure/git-ape/raw/main/APE.png)


📖 Documentation: azure.github.io/git-ape  •  🛒 VS Code Marketplace: Git-ApeTeam.git-ape

Git-Ape is a platform engineering framework built on GitHub Copilot. It is a multi-agent system that plans, validates, and deploys any Azure workload — with security gates, cost analysis, and CI/CD pipeline integration built in.

Nothing is deployed without your explicit confirmation.

What Git-Ape Does
Git-Ape walks every deployment through the same four steps:

Gather requirements through a guided interview.
Generate an ARM template, architecture diagram, cost estimate, and security report.
Confirm with you (interactive) or via PR review (headless) before anything is created.
Deploy to Azure and run post-deployment validation.

## azure-saas-skills

Azure SaaS platform skills plugin for Git-Ape, based on:

- Azure ISV Landing Zone guidance:  
  https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/isv-landing-zone
- [Architect multitenant solutions on Azure](https://learn.microsoft.com/en-us/azure/architecture/guide/multitenant/overview)
- Mastering the Marketplace SaaS hands-on labs:  
  https://microsoft.github.io/Mastering-the-Marketplace/saas/dev/#hands-on-labs
- Commercial Marketplace SaaS Accelerator:  
  https://github.com/Azure/Commercial-Marketplace-SaaS-Accelerator

The skills are designed so an SDC can stand up a multi-tenant SaaS platform, add product code, and onboard/publish through Azure Marketplace with scale and operational best practices.

## Multitenancy Architecture Principles

The skills apply the Azure Architecture Center's multitenancy guidance across the complete SaaS lifecycle:

- Define the tenant model and map business entities to explicit tenancy boundaries.
- Select shared, pooled, siloed, or hybrid isolation independently across compute, data, identity, messaging, and networking.
- Establish, validate, authorize, propagate, and audit tenant context in synchronous and asynchronous workloads.
- Use deployment stamps where appropriate, with tenant placement, capacity, scaling, migration, and blast-radius controls.
- Prevent noisy-neighbor effects through quotas, throttling, resource governance, and tenant-aware observability.
- Automate tenant onboarding, configuration, entitlement, movement, reconciliation, and offboarding.
- Test cross-tenant isolation and horizontal privilege-escalation controls throughout APIs, data stores, caches, messages, logs, and administrative tools.

These principles are implemented in `multi-tenant_SaaS`, `tenant-isolation-models`, `deployment-blueprints`, `tenant-lifecycle-automation`, `scale-and-sre`, and `security-and-compliance`.

## Install

### Copilot Plugin Marketplace (Recommended)

**From Bash:**

```bash
copilot plugin marketplace add dawright22/azure-saas-skills
copilot plugin install git-ape@azure-saas-skills
copilot plugin list   # Should show: git-ape@azure-saas-skills
```

**From within Copilot CLI:**

```bash
# Add the azure-saas-skills plugin from the marketplace
/plugin marketplace add dawright22/azure-saas-skills

# Install it into your workspace
/plugin install git-ape-azure-saas-skills@git-ape-azure-saas-skills

# Verify installation
/plugin list

# Update azure-saas-skills to the latest version
/plugin update dawright22/azure-saas-skills

# Remove azure-saas-skills if no longer needed
/plugin uninstall dawright22/azure-saas-skills
```

## Included Skills

| Skill | Purpose |
|---|---|
| `multi-tenant_SaaS` | End-to-end SaaS platform orchestration workflow |
| `isv-landing-zone-foundation` | Build Azure ISV landing zone baseline |
| `saas-accelerator-bootstrap` | Integrate/extend SaaS Accelerator foundations |
| `tenant-isolation-models` | Select and implement tenancy/isolation models |
| `tenant-lifecycle-automation` | Provisioning, upgrades, offboarding lifecycle |
| `fulfillment-and-metering` | Marketplace fulfillment APIs and metering events |
| `marketplace-offer-types` | Offer-type decision matrix and architecture mapping |
| `marketplace-onboarding` | Publisher setup, technical config, go-live checklist |
| `onboard-to-marketplace` | Execution-focused Marketplace onboarding workflow |
| `scale-and-sre` | Scale, resilience, observability, and operations patterns |
| `security-and-compliance` | Identity, secrets, data protection, compliance controls |
| `deployment-blueprints` | IaC deployment paths for reference SaaS topologies |

## Example Usage

```text
@git-ape /multi-tenant_SaaS build a transactable SaaS offer on Azure
@git-ape /marketplace-offer-types compare SaaS vs Managed Application for my B2B product
@git-ape /marketplace-onboarding generate my marketplace readiness checklist
@git-ape /onboard-to-marketplace run my publication onboarding flow
```

## Structure

```text
git-ape-azure-saas-skills/
├── README.md
├── plugin.json
├── marketplace.json
└── skills/
    ├── multi-tenant_SaaS/
    │   └── SKILL.md
    └── ... (12 skills total)
```
