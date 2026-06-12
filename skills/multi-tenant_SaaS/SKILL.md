---
name: multi-tenant_SaaS
description: "Primary orchestration skill for building a multi-tenant Azure SaaS platform, integrating ISV landing zone guidance, SaaS Accelerator patterns, and marketplace publication workflows."
argument-hint: "SaaS product type, target tenants, regions, compliance needs, and preferred offer model"
user-invocable: true
last_updated: "2026-06-12"
---

# Multi-Tenant SaaS Orchestrator

Use this skill as the top-level entrypoint: `/git-ape:multi-tenant_SaaS`.

## What this skill does

1. Collects platform requirements (tenant model, scale profile, compliance, regions).
2. Maps requirements to ISV landing zone and SaaS Accelerator implementation tracks.
3. Produces a staged execution plan:
   - Foundation and landing zone
   - SaaS platform build-out
   - Marketplace onboarding and publication
4. Routes work to specialized skills in this plugin.

## Required outputs

- Target architecture with tenancy boundaries.
- Offer strategy (SaaS vs Azure app/VM/container alternatives).
- Marketplace readiness checklist with go-live gates.
- Day-2 operations and SRE control plan.
