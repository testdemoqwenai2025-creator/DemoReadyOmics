# Tessera Bio / ReadyOmics

> The bioinformatics platform that ships **ML-ready, harmonised, version-controlled multi-omic datasets** — so your ML and drug discovery teams train on data they can trust, reproduce, and audit.

This repository is the **public demo and preview endpoint** for the Tessera Bio / ReadyOmics project. It exists so prospective customers, partners, and investors can evaluate the product without signing an NDA, and so that any public documentation or demo artefacts have a single canonical home.

The corresponding internal code repository is private. Anything that should be shared publicly is mirrored into this repository from the private one by an automated workflow — see [`docs/how-it-works.md`](docs/how-it-works.md) for the sync mechanism.

---

## What is ReadyOmics?

ReadyOmics is a bioinformatics platform that sits **on top of public biological data portals** (GEO, ArrayExpress, Expression Atlas, DepMap, Ensembl, UniProt, Open Targets, and others) and ships **ML-ready, harmonised, versioned training datasets with provenance**, rather than raw `BAM` and `VCF` files.

The pain it removes:

- ML teams in drug discovery spend 60–80% of their time producing clean, harmonised training datasets. ReadyOmics removes that step.
- When Ensembl or UniProt publish a new release, models trained on the previous release silently become un-reproducible. ReadyOmics ships an identifier-drift report with every dataset so teams know exactly which models need retraining.
- Train / val / test splits in computational biology commonly leak donors, families, or chromosomes. ReadyOmics ships biologically stratified splits with leakage controls, by default.

For more detail on the positioning, see [`docs/positioning.md`](docs/positioning.md).

---

## What is in this public repository?

This repository is intentionally **a strict subset** of the private internal repository. The sync workflow that maintains this invariant lives in the private repo and pushes only files that are explicitly placed in a `public/` directory.

The public repository contains:

- **Demo dataset cards** — sample machine-readable metadata files for representative ML-ready datasets, in YAML. These are illustrative; the real ones live behind the API.
- **Public documentation** — positioning, dataset-card schema, identifier-drift report format, licence-compatibility matrix summary.
- **Landing pages and GitHub Pages site** — the public marketing surface.
- **Tutorial notebooks** — read-only walkthroughs that consume the API (without revealing the API internals).

The public repository **does not contain**:

- Internal pipeline source code
- The harmonisation layer implementation
- The dataset-card generator implementation
- Private dataset files
- Customer data
- Customer-specific configurations or commercial terms

---

## Repository structure

```
DemoReadyOmics/
├── README.md                      # this file
├── docs/
│   ├── index.md                   # GitHub Pages landing page
│   ├── positioning.md             # one-page product positioning
│   ├── how-it-works.md            # how the sync mechanism works
│   ├── dataset-card-schema.md     # public schema spec for dataset cards
│   ├── identifier-drift-report.md # identifier-drift report format
│   ├── licence-matrix-summary.md  # public summary of the licence review
│   └── tutorial-notebook.ipynb    # example: training a classifier on a demo dataset card
└── demo-dataset-cards/
    ├── gtex-breast-v0.1.yaml
    ├── tcga-breast-open-v0.1.yaml
    └── depmap-breast-v0.1.yaml
```

---

## GitHub Pages

This repository publishes a static site at:

```
https://<owner>.github.io/DemoReadyOmics/
```

The site is generated from the `docs/` directory. No build step is required — GitHub Pages serves the Markdown files directly (Jekyll with the default theme).

To view the site:
1. Wait ~2 minutes after the bootstrap script runs for Pages to propagate.
2. Visit the URL printed by the bootstrap script.
3. If you see a 404, check `Settings -> Pages` on the repository to confirm the source is `main` branch, `/docs` folder.

---

## For investors and prospective customers

You do not need an NDA to view this repository or its GitHub Pages site. The contents here are sufficient for an initial evaluation of:

- **The product concept** — see [`docs/positioning.md`](docs/positioning.md)
- **The data schema** — see [`docs/dataset-card-schema.md`](docs/dataset-card-schema.md)
- **The licence posture** — see [`docs/licence-matrix-summary.md`](docs/licence-matrix-summary.md)
- **A worked example** — see [`docs/tutorial-notebook.ipynb`](docs/tutorial-notebook.ipynb)

For deeper technical evaluation, customer pilots, or source-code access, please contact the Tessera Bio team directly. Source-code access is granted via a separate evaluation agreement, not via this repository.

---

## Licence

The content in this repository is licensed under [CC-BY 4.0](https://creativecommons.org/licenses/by/4.0/) unless otherwise noted at the top of a file. You are free to share, adapt, and use this content for any purpose, including commercial, with attribution.

The Tessera Bio / ReadyOmics name, logo, and any proprietary dataset artefacts referenced in the documentation are not licensed for unrestricted use; please contact the team for terms.

---

## Contact

- **Project site:** this repository
- **Pages site:** see the URL above
- **Private repository:** access by arrangement

> _Maintained by the Tessera Bio / ReadyOmics team. This public mirror is updated automatically on every push to the private repository._
