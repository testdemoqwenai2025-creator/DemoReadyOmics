# Dataset Card Schema

Every ML-ready dataset shipped by Tessera Bio is accompanied by a machine-readable **dataset card**. The dataset card is the primary artefact that allows an ML team to trust, reproduce, and audit a model trained on the dataset.

This page documents the public schema. The implementation that produces these cards lives in the private repository.

## Format

Dataset cards are YAML files (for human readability) and JSON-LD files (for machine processing). The JSON-LD is generated from the YAML; the YAML is the canonical source.

## Fields

### Identity

| Field | Type | Required | Description |
|---|---|---|---|
| `dataset_id` | string | yes | Globally unique identifier, namespaced: `tessera.<assay>.<version>.<cohort>.<reference>` |
| `dataset_version` | semver | yes | Semantic version of this dataset |
| `release_date` | date | yes | ISO 8601 date |
| `producer` | string | yes | "Tessera Bio / ReadyOmics" |
| `licence` | string | yes | Licence under which this dataset is released |

### Cohort definition

| Field | Type | Required | Description |
|---|---|---|---|
| `cohort_definition.n_samples` | int | yes | Number of samples in the dataset |
| `cohort_definition.n_donors` | int | yes | Number of unique donors |
| `cohort_definition.species` | string | yes | Species (typically `Homo sapiens`) |
| `cohort_definition.tissue` | list[string] | yes | Tissue(s) represented |
| `cohort_definition.disease_focus` | string | yes | Disease focus or "healthy" |
| `cohort_definition.selection_criteria` | string | yes | Human-readable selection criteria |

### Reference versions (U2 — cross-release identifier stability)

| Field | Type | Required | Description |
|---|---|---|---|
| `reference_versions.ensembl_release` | int | yes | Pinned Ensembl release (e.g., 110) |
| `reference_versions.ensembl_assembly` | string | yes | Pinned genome assembly (e.g., `GRCh38`) |
| `reference_versions.uniprot_release` | string | yes | Pinned UniProt release (e.g., `2024_01`) |
| `reference_versions.gene_id_type` | string | yes | Identifier type used for genes |
| `reference_versions.transcript_id_type` | string | yes | Identifier type used for transcripts |

### Pipeline provenance

| Field | Type | Required | Description |
|---|---|---|---|
| `pipeline.pipeline_name` | string | yes | Name of the pipeline that produced this dataset |
| `pipeline.pipeline_version` | semver | yes | Version of the pipeline |
| `pipeline.pipeline_url` | string | yes | URL to the pipeline source (if public) |
| `pipeline.container_hash` | string | yes | SHA256 of the container image used |
| `pipeline.pipeline_commit` | string | yes | Git commit hash of the pipeline |
| `pipeline.workflow_lang` | string | yes | Workflow language and version (e.g., `Nextflow 23.10`) |
| `pipeline.tools` | map | yes | Map of tool name to version (e.g., `alignment: STAR 2.7.11b`) |

### Input sources

A list of source records. Each source carries its own licence for attribution pass-through.

| Field | Type | Required | Description |
|---|---|---|---|
| `inputs[].source_id` | string | yes | Identifier for the source (e.g., `GEO-GSE12345`) |
| `inputs[].source_url` | string | yes | URL to the source record |
| `inputs[].source_licence` | string | yes | Licence under which the source is released |
| `inputs[].n_samples_taken` | int | yes | Number of samples taken from this source |
| `inputs[].submitters_acknowledgement` | string | yes | Citation for the original submitter |

### Quality metrics

| Field | Type | Required | Description |
|---|---|---|---|
| `quality.median_reads_per_sample` | int | yes | Median read depth |
| `quality.median_mapping_rate` | float | yes | Median alignment rate |
| `quality.median_duplication` | float | yes | Median duplication rate |
| `quality.median_3_prime_bias` | float | yes | Median 3' bias |
| `quality.failed_qc_samples` | list[string] | yes | Sample IDs removed for failing QC |
| `quality.qc_threshold` | string | yes | QC threshold description |

### Batch effects

| Field | Type | Required | Description |
|---|---|---|---|
| `batch_effects.detected` | bool | yes | Whether batch effects were detected |
| `batch_effects.correction_method` | string | yes | Correction method applied |
| `batch_effects.before_correction_pca_explained_by_batch` | float | yes | Variance explained by batch before correction |
| `batch_effects.after_correction_pca_explained_by_batch` | float | yes | Variance explained by batch after correction |

### Train / val / test splits (U1 — leakage-controlled)

| Field | Type | Required | Description |
|---|---|---|---|
| `splits.split_strategy` | string | yes | Strategy used to define splits |
| `splits.train.n_samples` | int | yes | Number of training samples |
| `splits.train.cohort_ids` | list[string] | yes | Cohorts in the training split |
| `splits.validation.n_samples` | int | yes | Number of validation samples |
| `splits.validation.cohort_ids` | list[string] | yes | Cohorts in the validation split |
| `splits.test.n_samples` | int | yes | Number of test samples |
| `splits.test.cohort_ids` | list[string] | yes | Cohorts in the test split |
| `splits.leakage_controls.donor_overlap_check` | string | yes | Result of donor overlap check |
| `splits.leakage_controls.family_overlap_check` | string | yes | Result of family overlap check |

### Normalisation

| Field | Type | Required | Description |
|---|---|---|---|
| `normalisation.method` | string | yes | Normalisation method (e.g., `DESeq2 vst`) |
| `normalisation.reference_distribution` | string | yes | Reference distribution used for fitting |
| `normalisation.apply_to_test` | string | yes | How the test set is normalised |

### Known biases and limitations

| Field | Type | Required | Description |
|---|---|---|---|
| `known_biases` | list[string] | yes | List of known biases and limitations |

### Suggested and discouraged uses

| Field | Type | Required | Description |
|---|---|---|---|
| `suggested_uses` | list[string] | yes | Suggested downstream uses |
| `discouraged_uses` | list[string] | yes | Discouraged downstream uses |

### Identifier drift report (U2)

| Field | Type | Required | Description |
|---|---|---|---|
| `identifier_drift_report.compared_to_ensembl_release` | int | yes | Previous Ensembl release compared against |
| `identifier_drift_report.genes_added` | int | yes | Genes added in this release |
| `identifier_drift_report.genes_removed` | int | yes | Genes removed in this release |
| `identifier_drift_report.genes_merged` | int | yes | Genes merged in this release |
| `identifier_drift_report.genes_split` | int | yes | Genes split in this release |
| `identifier_drift_report.impact_on_dataset` | string | yes | Description of impact on this dataset |

### Provenance

| Field | Type | Required | Description |
|---|---|---|---|
| `provenance.output_matrix_sha256` | string | yes | SHA256 of the output matrix |
| `provenance.dataset_card_sha256` | string | yes | SHA256 of the dataset card |
| `provenance.signed_by` | string | yes | Signing key identifier |

## Example

A worked example is in the `demo-dataset-cards/` directory of this repository.
