---
name: strict-drift-detection
description: "Deep, property-level configuration drift detection for Azure resources. Use as a companion to Git-Ape's azure-drift-detector when the built-in check (a hardcoded subset of properties per resource type) is not catching nested, array, or resource-type-specific drift."
argument-hint: "Resource group, deployment ID, or resource IDs to baseline/compare; severity threshold to report at"
user-invocable: true
last_updated: "2026-11-05"
---

# Strict Drift Detection

Extends Git-Ape's `azure-drift-detector` with a generic, recursive, baseline-snapshot
diff that compares the **full resolved Azure resource state**, not just a hardcoded
subset of properties (`httpsOnly`, `minimumTlsVersion`, `tags`) checked against
`requirements.json` intent.

Reference implementation: https://github.com/dawright22/strict-drift-detection

## Table of Contents

- [Why the built-in drift detector misses things](#why-the-built-in-drift-detector-misses-things)
- [Core Concepts](#core-concepts)
- [CLI Reference](#cli-reference)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)

## Why the built-in drift detector misses things

Git-Ape's `azure-drift-detector` skill diffs a small, per-resource-type `case`
statement against `requirements.json` (deployment *intent*), which means it:

- Only recognizes a couple of hardcoded resource types and properties.
- Compares against intent, not the actual resolved ARM/Azure state.
- Cannot see nested objects, array reordering, or arbitrary properties.
- Produces false negatives for anything outside its hardcoded property list.

`strict-drift-detection` fixes this by taking a full `az resource show --output json`
**baseline snapshot** of every managed resource the first time it runs, then doing a
generic recursive diff against that baseline on every subsequent run — no per-resource-type
code required.

## Core Concepts

### Baseline snapshot, not template parsing

ARM template expressions (`reference()`, `resourceId()`, computed names) are unreliable
to resolve statically. Instead, this approach captures the real resolved resource JSON
(`az resource show`) once, stores it under `drift-analysis/strict-baseline/<resource>.json`,
and treats that as ground truth for future comparisons.

### Generic recursive diff (`deep-diff.jq`)

A single `jq` script walks every leaf path in both the baseline and current snapshot and
reports additions, removals, and value changes — no resource-type-specific logic.

### Array-aware diffing

Arrays of objects (e.g. `appSettings`, `ipRules`) are re-keyed by `name` / `id` / `key`
(in that priority order, configurable via `array-keys.json`) before diffing, so
reordering an array does not produce false-positive drift.

### Ignore list and severity rules

- `ignore-properties.json` filters out volatile, platform-managed properties
  (e.g. `etag`, `provisioningState`, timestamps) that change on every read.
- `drift-rules.json` classifies every remaining diff by severity using first-match-wins
  regex rules against the dotted property path, with a mandatory `.*` catch-all so
  nothing is silently dropped.

## CLI Reference

```bash
# Baseline every resource in a resource group (first run)
./strict-detect-drift.sh --resource-group rg-myapp-prod --baseline

# Compare current state against the stored baseline
./strict-detect-drift.sh --resource-group rg-myapp-prod

# Compare a single resource by ID
./strict-detect-drift.sh --resource-id /subscriptions/.../resourceGroups/rg-myapp-prod/providers/Microsoft.Web/sites/app-myapp

# Only report findings at or above a severity
./strict-detect-drift.sh --resource-group rg-myapp-prod --min-severity high
```

## Best Practices

- Run `--baseline` immediately after a known-good deployment, not before.
- Re-baseline deliberately after any approved manual change, so future comparisons
  only surface *unapproved* drift.
- Use `--min-severity` in CI/scheduled checks to avoid alert fatigue on `info`-level
  cosmetic diffs (e.g. tag ordering).
- Pair with Git-Ape's `/azure-drift-detector` for a quick intent-level check, then
  escalate to `strict-drift-detection` when a deeper, property-level audit is needed.

## Troubleshooting

| Symptom | Cause | Fix |
|---|---|---|
| Every property on every resource reports drift | No baseline captured yet | Run with `--baseline` first |
| Drift reported for a property that didn't change | Volatile property not in ignore list | Add its path pattern to `ignore-properties.json` |
| Array reorder reported as drift | Array has no `name`/`id`/`key` field to re-key by | Add the field name to `array-keys.json` |
| Findings missing expected severity | No matching rule in `drift-rules.json` | Add a pattern before the `.*` catch-all |
