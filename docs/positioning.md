---
layout: default
title: Positioning
description: Tessera Bio / ReadyOmics — Positioning documentation
---

# Positioning

## One-line

> Tessera Bio sits on top of public biological data portals and ships **ML-ready, harmonised, version-controlled multi-omic datasets** — so ML and drug discovery teams train on data they can trust, reproduce, and audit.

## The pain

Computational biology and ML-for-drug-discovery teams routinely spend 60–80% of their time turning public raw data (`FASTQ`, `BAM`, raw counts) into clean training datasets. The remaining 20–40% is the actual ML.

The handoff from pipelines to ML is where most teams lose time, reproducibility, and trust. Almost no existing platform ships datasets that are *ready to train on* — they ship processed files and expect the ML team to do the rest.

## The reframe

Existing free portals (Open Targets, GEO, ArrayExpress, DepMap, GTEx, UniProt, Ensembl, Reactome, cBioPortal, etc.) are **upstream suppliers**, not competitors. They are well-funded by NIH, EMBL-EBI, Wellcome, and CZI — we cannot and should not compete with them.

What is missing is the layer that **turns their outputs into ML-ready datasets**: harmonised across releases, leakage-controlled in train/val/test splits, with full provenance and dataset cards.

That is what Tessera Bio builds.

## The three differentiators (the wedge)

1. **ML-ready outputs (U1).** Every pipeline emits not just `BAM`/`VCF` but a model-ready tensor or matrix plus a dataset card. Train/val/test splits are stratified by biological leakage (held-out donors, families, chromosomes, drugs) — not random.
2. **Cross-release identifier stability (U2).** When Ensembl, UniProt, or Open Targets publish a new release, Tessera ships an identifier-drift report so teams know exactly which downstream models need retraining and why.
3. **Multi-omic harmonisation, native (U3).** Genes, transcripts, proteins, metabolites, and pathways are first-class, joined, versioned citizens — not bolted on after the fact.

## Who buys

| Segment | Why they buy |
|---|---|
| AI-first drug discovery startups | Clean training data is the bottleneck, not pipeline runtime |
| Mid-stage biotech with CompBio but no platform team | Have bioinformaticians, no platform engineers; every dataset rebuild costs weeks |
| Pharma R&D computational platforms groups | Already have home-grown platforms; recognise the harmonisation gap |
| CROs / contract research | Reproducible, provenance-rich delivery is a selling point for their clients |
| Diagnostic / clinical AI companies | Versioned identifiers for longitudinal reproducibility |

## What we do not compete on

- Workflow engine performance — Nextflow, Snakemake, Cromwell are good enough
- Cloud cost optimisation — cloud providers win this
- Pipeline library breadth — nf-core wins community, Bioconda wins tooling

## Open-core boundary

| Component | Licence |
|---|---|
| Pipeline code (Nextflow workflows) | Apache 2.0 (open-source) |
| Container images | Apache 2.0 base |
| Harmonisation layer | Source-available, dual-licence |
| Dataset-card schema + generator | Source-available, dual-licence |
| ML-ready datasets (parquet files) | Per-dataset licence (most: CC-BY 4.0) |
| CLI / SDK | Apache 2.0 |

The pipeline layer is open because pipeline execution is commodity. The harmonisation layer and dataset-card layer are source-available because that is where the defensible value sits.

## Status

v0.1 in development. Private beta with 3–5 ML teams planned within 90 days.

For evaluation access, contact the Tessera Bio team directly.
