# How the public / private repository split works

## Architecture

```
┌──────────────────────────────────┐            ┌─────────────────────────────────┐
│  ReadyOmics1-Advance  (PRIVATE)  │            │  DemoReadyOmics     (PUBLIC)    │
│                                  │            │                                 │
│  - All source code               │  one-way   │  - README.md (public landing)  │
│  - Harmonisation layer           │  sync of   │  - docs/ (GitHub Pages site)   │
│  - Dataset-card generator        │  public/   │  - demo-dataset-cards/         │
│  - Pipeline workflows            │  ────────▶ │  - tutorial notebooks          │
│  - Internal configs              │            │                                 │
│  - .github/workflows/sync-...    │            │  GitHub Pages:                  │
│                                  │            │  <owner>.github.io/DemoReadyOmics │
└──────────────────────────────────┘            └─────────────────────────────────┘
```

## Invariants

1. **One-way only.** The public repo is always a strict subset of the private one. Nothing ever flows back from public to private.
2. **Explicit allowlist.** Only files placed in the `public/` directory of the private repo are mirrored. Everything else is private by default.
3. **Single workflow.** The sync workflow lives in the private repo at `.github/workflows/sync-to-public.yml` and runs on every push that touches `public/`.
4. **Two tokens.** The bootstrap token (used once to create the repos) is revoked immediately. The sync token (`DEMO_REPO_PAT`) lives as an encrypted secret on the private repo and is used by the workflow to push to the public repo.
5. **Audit trail.** Every commit on the public repo has a message that references the source commit hash on the private repo, so the trail is never lost.

## How to publish something publicly

1. Work in the private repository as normal.
2. When you want to publish a file, place it under `public/` in the private repo (e.g., `public/docs/new-page.md`).
3. Commit and push.
4. The sync workflow runs automatically (within ~1 minute) when the push touches `public/**`.
5. The public repository is updated. GitHub Pages updates within ~2 minutes.

## What if I want to publish something that lives outside `public/`?

You don't. Make a copy in `public/`. The default-deny posture is intentional — it prevents accidental leaks.

If a file is large or frequently updated, consider a build step that copies it from its source location to `public/` as part of the workflow. The public-facing copy is always the canonical public one.

## What about binary artefacts (PDFs, Excel files, images)?

Place them under `public/` as well. The sync workflow copies everything in `public/` recursively. Binary files are committed to the public repo like any other file.

If you need Git LFS for large binaries, enable it on both repos. The sync workflow handles LFS files transparently.

## What if the sync workflow fails?

Most failures fall into one of three categories:

| Symptom | Cause | Fix |
|---|---|---|
| "secret DEMO_REPO_PAT is not set" | The secret has not been added to the private repo | Add it under Settings → Secrets and variables → Actions |
| "Authentication failed" on the push step | The token has expired or been revoked | Generate a fresh token and update `DEMO_REPO_PAT` |
| "No changes to sync" (this is not a failure) | `public/` has not changed since the last sync | This is normal; nothing to fix |

Workflow run logs are at `https://github.com/<owner>/ReadyOmics1-Advance/actions`.

## Can the public repo ever push back to the private repo?

No. The architecture is intentionally one-way. If you want to receive community contributions on the public repo, they must be proposed as pull requests on the public repo and then **manually re-applied** to the private repo by a maintainer. There is no automated reverse-sync.

## Why not use a single public repo with private sub-modules?

Three reasons:

1. **Reviewer experience.** Anyone evaluating the product should be able to clone the public repo and explore it without encountering private sub-modules they cannot access.
2. **Accident surface.** Sub-modules can be misconfigured such that private code becomes accidentally visible. The default-deny posture of a separate public repo is harder to misconfigure.
3. **GitHub Pages simplicity.** Pages works out of the box with a single public repo; mixing public and private content in one repo complicates the Pages setup.

## Further reading

- [Positioning](positioning.md) — what ReadyOmics is, who buys it, what it does not compete on
- [Dataset Card Schema](dataset-card-schema.md) — the metadata format that ships with every ML-ready dataset
- [Identifier Drift Report](identifier-drift-report.md) — the format for cross-release identifier stability
- [Licence Matrix Summary](licence-matrix-summary.md) — public summary of the licence review
