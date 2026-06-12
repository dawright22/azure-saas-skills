---
name: tenant-lifecycle-automation
description: "Implements automated tenant onboarding, provisioning, upgrade, suspension, and offboarding workflows."
argument-hint: "Provisioning SLA, onboarding approvals, data retention policy, and lifecycle states"
user-invocable: true
last_updated: "2026-06-12"
---

# Tenant Lifecycle Automation

Defines lifecycle workflows that keep tenant operations consistent and auditable.

## Lifecycle coverage

1. Tenant signup and activation.
2. Plan/subscription assignment.
3. Resource provisioning and configuration.
4. Upgrade, downgrade, and pause/resume.
5. Offboarding, retention, and deletion.

## Deliverables

- Lifecycle state machine and event contracts.
- Automation responsibilities by service/component.
- Operational runbook for failed provisioning and retries.
