---
name: deployment-blueprints
description: "Provides implementation blueprints and deployment sequencing for Azure SaaS reference topologies."
argument-hint: "Preferred IaC tool, target topology, deployment environments, and release cadence"
user-invocable: true
last_updated: "2026-06-12"
---

# Deployment Blueprints

Turns architecture decisions into executable deployment tracks.

## Blueprint tracks

- Single-region starter SaaS topology.
- Multi-region production topology.
- Shared services + per-tenant workload topology.
- Reference CI/CD promotion model.

## Deliverables

- Deployment sequence and dependency graph.
- Environment-specific parameter model.
- Release and rollback strategy guidance.
