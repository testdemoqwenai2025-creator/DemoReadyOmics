# Identifier Drift Report

One of the three core differentiators of Tessera Bio / ReadyOmics is **cross-release identifier stability** (U2). When a public database such as Ensembl or UniProt publishes a new release, identifiers change: genes are added, removed, merged, or split. Models trained on the previous release silently become un-reproducible.

Tessera ships an **identifier drift report** alongside every dataset to make this explicit. This page documents the public format of the report.

## Purpose

The report answers two questions:

1. **What changed between release A and release B?** Specifically, what genes/transcripts/proteins were added, removed, merged, or split.
2. **What is the impact on this dataset and the models trained on it?** Which models need retraining, and why.

## Format

Identifier drift reports are YAML files. They are produced by the harmonisation layer in the private repository and consumed by ML teams to schedule model retraining.

## Fields

### Identity

| Field | Type | Required | Description |
|---|---|---|---|
| `report_id` | string | yes | Globally unique identifier for the report |
| `report_version` | semver | yes | Schema version of the report |
| `produced_at` | datetime | yes | When the report was produced |
| `produced_by` | string | yes | "Tessera Bio / ReadyOmics" |

### Comparison

| Field | Type | Required | Description |
|---|---|---|---|
| `comparison.source_database` | string | yes | Database being compared (e.g., `Ensembl`) |
| `comparison.from_release` | int | yes | Previous release |
| `comparison.to_release` | int | yes | New release |
| `comparison.from_release_date` | date | yes | Release date of the previous release |
| `comparison.to_release_date` | date | yes | Release date of the new release |

### Changes

| Field | Type | Required | Description |
|---|---|---|---|
| `changes.genes.added` | list[string] | yes | New gene IDs in the new release |
| `changes.genes.removed` | list[string] | yes | Gene IDs present in old release but not new |
| `changes.genes.merged` | list[map] | yes | Gene IDs that were merged; each map has `from`, `to`, `reason` |
| `changes.genes.split` | list[map] | yes | Gene IDs that were split; each map has `from`, `to`, `reason` |
| `changes.genes.renamed` | list[map] | yes | Gene IDs that were renamed; each map has `from`, `to` |

Equivalent fields exist for transcripts and proteins.

### Impact

| Field | Type | Required | Description |
|---|---|---|---|
| `impact.datasets_affected` | list[string] | yes | List of Tessera dataset IDs affected by this drift |
| `impact.models_likely_affected` | list[string] | yes | Tessera dataset IDs whose downstream models likely need retraining |
| `impact.recommended_action` | string | yes | Human-readable recommendation |
| `impact.severity` | enum | yes | One of `low`, `medium`, `high` |

Severity is assigned as follows:

- **low** — fewer than 10 genes changed and none of them appear in the dataset's training features
- **medium** — between 10 and 100 genes changed, or fewer than 10 changes affect features used in the dataset
- **high** — more than 100 genes changed, or any structural change (merge/split) affects features used in the dataset

## Example

A worked example of an identifier drift report is included in the `demo-dataset-cards/` directory of this repository.

## Why this matters

Most computational biology teams handle identifier drift reactively: a model produces different results this quarter than last quarter, and the team debugs backwards to discover that Ensembl released a new version in between. This costs weeks of investigation per occurrence.

Tessera ships the drift report proactively, on every dataset, with every release. The investigation step is removed.
