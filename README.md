# Tessera Bio / ReadyOmics — Public Demo (v0.1)

> **No NDA required. Available 24/7/365.**

## For investors, startup groups, and seeding-funding evaluators

This is the **public demo site** for Tessera Bio / ReadyOmics — the
bioinformatics platform that ships **ML-ready, harmonised, version-controlled
multi-omic datasets** for drug discovery and computational biology teams.

### View the live demo

> **🔗 https://testdemoqwenai2025-creator.github.io/DemoReadyOmics/**

The link above is the live, interactive demo. No login required. No NDA
required. Available 24 hours a day, 365 days a year.

### What you'll see

The demo is a full Next.js application with 8 pages:

| Page | What it shows |
|---|---|
| **[/](https://testdemoqwenai2025-creator.github.io/DemoReadyOmics/)** | Landing page — hero, differentiators (U1+U2+U3), customer stories, live dataset card viewer, identifier drift report, pipeline architecture, MVP code, comparison vs incumbents (Terra/Seqera/DNAnexus/Galaxy), ROI calculator, licence matrix, pricing |
| **[/about](https://testdemoqwenai2025-creator.github.io/DemoReadyOmics/about/)** | Founder story, the wedge, 3/6/12-month roadmap, team, advisors |
| **[/datasets](https://testdemoqwenai2025-creator.github.io/DemoReadyOmics/datasets/)** | Catalogue of ML-ready datasets (3 demo datasets, filterable by tissue + licence) |
| **[/datasets/[id]](https://testdemoqwenai2025-creator.github.io/DemoReadyOmics/datasets/tessera.rnaseq.v0.1.2026-09.gtex-breast.ensembl-v110/)** | Full-page dataset card view — cohort, inputs, quality, leakage-controlled splits, biases, identifier drift report, pipeline provenance, cryptographic signing, BibTeX citation, CLI usage, version history |
| **[/docs](https://testdemoqwenai2025-creator.github.io/DemoReadyOmics/docs/)** | Documentation hub — 9 interactive doc sections + additional resources |
| **[/privacy](https://testdemoqwenai2025-creator.github.io/DemoReadyOmics/privacy/)** | GDPR, HIPAA, CCPA, 21 CFR Part 11 compliance (honest, 800 words, no legalese) |
| **[/terms](https://testdemoqwenai2025-creator.github.io/DemoReadyOmics/terms/)** | Terms of service |
| **[/contact](https://testdemoqwenai2025-creator.github.io/DemoReadyOmics/contact/)** | Structured contact form (private beta, commercial, press, partnership, bug, other) |

### What this is (and isn't)

**This is:** a working demo of the Tessera Bio product, built on actual
running code (Python pipeline + Nextflow workflow + Next.js multi-page
app). The dataset cards, the identifier-drift report, the comparison table,
and the ROI calculator are all real, interactive components — not mockups.

**This isn't:** the production pipeline running on real data. The 3 demo
datasets use illustrative data; the real datasets will be added as the
private beta progresses. For source-code access or a live pipeline
demonstration, contact us directly.

### The wedge

Tessera Bio sits on top of public biological data portals (GEO, ArrayExpress,
DepMap, Ensembl, UniProt, Open Targets) and ships **ML-ready, harmonised,
versioned training datasets** — not raw BAM/VCF files. The three
differentiators:

1. **U1 — ML-ready outputs**: every pipeline emits a model-ready matrix plus
   a dataset card. Train/val/test splits are stratified by biological leakage
   (held-out donors, families, chromosomes), not random.
2. **U2 — Cross-release identifier stability**: every dataset is pinned to a
   specific Ensembl/UniProt release. A built-in identifier-drift report flags
   what breaks when those releases change, and which models need retraining.
3. **U3 — Multi-omic harmonisation**: genes, transcripts, proteins,
   metabolites, pathways are first-class, joined, versioned citizens.

### What we do not compete on

- Workflow engine performance (Nextflow, Snakemake, Cromwell are good enough)
- Cloud cost optimisation (cloud providers will always win this)
- Pipeline library breadth (nf-core wins community; Bioconda wins tooling)

### Compliance

Compliant with **GDPR**, **HIPAA**, **CCPA**, and designed for **21 CFR
Part 11** readiness. See the [privacy page](https://testdemoqwenai2025-creator.github.io/DemoReadyOmics/privacy/)
for the full, honest compliance documentation.

### Contact

- **General**: hello@tessera.bio
- **Privacy / DPO**: privacy@tessera.bio
- **Private beta access**: use the [contact form](https://testdemoqwenai2025-creator.github.io/DemoReadyOmics/contact/)
- **Source code**: this public repo contains the demo site source. The
  private internal repo (pipeline + harmonisation layer + dataset-card
  generator) is accessible on request.

### Licence

Public site content is licensed under **CC-BY 4.0** unless otherwise noted.
The Tessera Bio name, logo, and the Tessera mark are trademarks of Tessera Bio.

---

*This is the v0.1 public demo. The v0.2 evolving codebase lives at
[ReadyOmics2-Advance](https://github.com/testdemoqwenai2025-creator/ReadyOmics2-Advance)
(private) with its public preview at
[Demo2ReadyOmics](https://github.com/testdemoqwenai2025-creator/Demo2ReadyOmics)
(public). This v0.1 site remains live as a stable reference for investors
and evaluators.*
