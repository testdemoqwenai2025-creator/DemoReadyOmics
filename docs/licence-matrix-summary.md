---
layout: default
title: Licence Matrix Summary
description: Tessera Bio / ReadyOmics — Licence Matrix Summary documentation
---

# Licence Compatibility — Public Summary

Tessera Bio / ReadyOmics ingests data from a range of public biological data portals. Each portal has its own licence terms that govern whether the data can be redistributed, used commercially, or modified.

This page is a public summary of the licence review we have conducted. The full review — including per-source notes, risk levels, and concrete next-step actions — is maintained internally. The summary below is sufficient for prospective customers and partners to understand our licence posture.

## Sources we ingest

| Source | Licence | Commercial use | Notes |
|---|---|---|---|
| GEO (Gene Expression Omnibus) | Public domain (US Gov) | Yes | US government data; per-record submitter terms apply |
| ArrayExpress | CC0 / CC-BY 4.0 | Yes | Mixed per submission; audited per experiment |
| Expression Atlas | CC-BY 4.0 | Yes | Clean, well-versioned, attribution required |
| recount3 | CC0 (derived) | Yes | Re-derived from SRA under consistent pipeline |
| ARCHS4 | CC-BY 4.0 (derived) | Yes | Attribution required |
| GTEx Portal | GTEx Data Use Certification | Conditional | Controlled access; raw data not redistributable; derived summaries may be open |
| TCGA via GDC | Open + Controlled tiers | Conditional | Open tier is freely redistributable; controlled tier requires dbGaP |
| DepMap | CC-BY 4.0 | Yes | Some legacy partner datasets carry separate terms |
| ENA (European Nucleotide Archive) | Public domain / CC0 | Yes | Submitting projects may attach their own terms |
| NCBI SRA | Public domain (US Gov) | Yes | Some submissions controlled via dbGaP |
| Ensembl | Apache 2.0 (software) + CC0 (data) | Yes | Reference data is CC0 |
| UniProt | CC-BY 4.0 | Yes | Attribution required |
| Open Targets Platform | CC-BY 4.0 | Yes | Underlying evidence sources retain their own licences |
| GWAS Catalog | CC-BY 4.0 | Yes | Attribution required |
| cBioPortal | Mixed (AGPL software; data per-study) | Conditional | Per-study audit required |
| CellxGene | CC-BY 4.0 (curated) | Yes | Some submitted datasets carry their own terms |
| PRIDE / ProteomeXchange | CC-BY 4.0 (metadata); raw per-submitter | Conditional | Per-submitter audit required |
| MetaboLights | CC-BY 4.0 | Yes | Attribution required |
| Reactome | CC-BY 4.0 (data) + Apache 2.0 (tools) | Yes | Attribution required |
| ClinVar | Public domain (US Gov) | Yes | US government data |

## Licence types reference

| Licence | Commercial use | Attribution | Redistribution |
|---|---|---|---|
| Public domain (US Gov) | Yes | No | Yes |
| CC0 1.0 | Yes | No | Yes |
| CC-BY 4.0 | Yes | Yes | Yes |
| CC-BY-NC 4.0 | No | Yes | Yes (non-commercial only) |
| ODbC 1.0 | Yes | Yes | Yes (with share-alike on database) |
| Apache 2.0 | Yes | Yes (NOTICE file) | Yes |
| AGPL-3.0 | Conditional | Yes | Yes (with copyleft) |
| GTEx DUC | Conditional | Yes | Conditional |
| dbGaP controlled | No (without approval) | Yes | No (raw) |

## How this affects the product

Tessera Bio maintains a **tiered product architecture** based on the licence review:

1. **Open tier** (free, attribution required) — datasets sourced from public-domain, CC0, and CC-BY 4.0 sources. Suitable for both research and commercial use, with attribution.
2. **Controlled tier** (research use only, requires user to bring their own dbGaP access) — datasets sourced from GTEx, TCGA controlled tier, and other controlled-access sources. Tessera provides the harmonisation; the user holds the access.
3. **Commercial tier** — datasets Tessera curates, harmonises, and signs. Pricing varies by dataset and use case.

The open tier is the default. The controlled tier requires explicit opt-in. The commercial tier is the revenue source.

## How we keep this up to date

The internal licence matrix is reviewed quarterly. Any change to a source's licence terms triggers an immediate review of the affected datasets. If a dataset can no longer be distributed under its existing terms, it is deprecated and removed from circulation, with a notice period for existing users.

## Disclaimer

This public summary is provided for general information. It is not legal advice. The actual licence terms of any public dataset are governed by the source's published licence, not by this summary. If you have a specific question about licence compatibility for your use case, contact the Tessera Bio team directly.
