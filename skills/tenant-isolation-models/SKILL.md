---
name: tenant-isolation-models
description: "Designs and validates tenancy models (shared, pooled, siloed, hybrid) with security, cost, and scale trade-offs."
argument-hint: "Tenant count, data isolation requirements, noisy-neighbor tolerance, and regulatory constraints"
user-invocable: true
last_updated: "2026-06-12"
---

# Tenant Isolation Models

Selects the right multitenancy pattern for the product and compliance profile.

## Model options

- Shared infrastructure / shared data
- Shared infrastructure / isolated data
- Pooled resources per segment
- Silo model per tenant
- Hybrid progression model

## Deliverables

- Chosen tenancy model with rationale.
- Isolation control map (identity, network, data, compute).
- Migration path as tenant scale and compliance requirements grow.
