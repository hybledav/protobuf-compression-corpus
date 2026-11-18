# Snapshot 2026-11-18-r1

- Datasets: 15
- Message files: 803
- Distinct payloads: 802
- Payload bytes: 36,743,059
- Source entries: 474,131
- Included source snapshots: 17
- Schemas: 15

The snapshot replaces empty COVID/NNDSS records and malformed PLACES bytes with identified source conversions, replaces Silesia-derived SAO data with NASA HEASARC data, and removes unverified or incorrectly extracted material. Sources, column mappings, nullable values, source snapshots and per-dataset reuse terms are recorded in metadata. The corpus is standalone and codec-neutral.

Validation includes decoding every payload with its declared schema, checking every source-record projection, verifying row coverage and metadata hashes, independently reading the NASA VOTables, checking duplicates, and verifying complete inventory and checksum coverage. Exact validation results are supplied with the reviewed change; consumers can verify the immutable tree with SHA256SUMS.

See RELEASE.md before making development history public.
