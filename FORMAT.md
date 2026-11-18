# Corpus format

Index format: 2. Snapshot: 2026-11-18-r1.

## Payload files

Every `datasets/**/*.pb` is exactly one raw protobuf message, without gRPC, HTTP/2, TCP, compression or length framing. The three original Google messages retain their upstream bytes and schemas. All other payloads are schema-specific `Batch` messages whose `records` field contains typed record messages, not arbitrary packet bytes.

`MANIFEST.json` is the complete lexicographically ordered payload index. Each file records its path, dataset, schema, fully qualified message type, byte count, SHA-256, Git blob SHA-1, record count and data license identifier. Converted files also have zero-based `first_row`; the range is `[first_row, first_row + records)`. Ranges are contiguous, non-overlapping and cover the selected source rows. Original Google files count as one source entry each. A source-entry count is not a message-file count.

`duplicate_of` identifies the lexicographically first identical payload. Identical wire bytes do not imply identical schema identity. Consumers should explicitly choose how to handle duplicates when splitting samples.

Dataset summary statistics use the midpoint median and nearest-rank 95th percentile. `unique_payload_count` counts distinct SHA-256 payloads. `total_payload_bytes` includes duplicate files. Git blob SHA-1 is SHA-1 of `blob <decimal size>`, NUL, and the exact file bytes. Schema hashes cover the exact `.proto` files.

## Uniform metadata

Every `metadata/*.json` has `format_version`, `id`, `kind`, `description`, `schema`, `message_type`, `source_snapshots`, `rights`, `conversion`, `record_count` and `files`. Every file entry uses `file` as its path key. This uniform layout applies to original Google messages as well as converted records.

`source_snapshots` gives exact request URLs, retrieval UTC timestamps, source-byte SHA-256 and size. `stored_path` points to the included gzip copy. `stored_sha256` and `stored_bytes` identify compressed bytes; after decompression, the source hash and size must match. Original source snapshots may contain columns outside a benchmark projection. Conversion metadata defines selection, column mappings, row order, batch size, numeric types and missing-value behavior.

Converted v2 schemas use optional fields: missing numeric values remain absent, while explicitly reported zero values remain present. Source suppression flags are retained in NNDSS. No unknown value is fabricated as zero. New messages use the official protobuf serializer with deterministic serialization. Weather and industry-unemployment retain their earlier corpus bytes, including explicit default-valued fields; every decoded field was compared to the pinned source records. Decoding and reserializing a protobuf can change its bytes, so preserve source payloads for byte-exact comparisons.

`rights` records the dataset-specific reuse basis, attribution, source evidence URL and local notice/license text. The repository MIT license does not replace third-party data terms. `licenses/rights-evidence.json` records the observed source declarations and their source-metadata hashes. Government-work identifiers describe the published U.S. status and do not grant unrelated trademark, privacy or foreign rights.

## Integrity and updates

`SHA256SUMS` covers every distributed regular file, including payloads, included source snapshots, schemas, metadata, licenses, documentation and MANIFEST.json. It excludes only itself. No symlinks or external paths are part of the release. The release archive's SHA-256 is distributed alongside the archive, outside this index.

Pin a snapshot archive or Git commit for immutable bytes. An addition, removal, byte change or schema change requires a new snapshot identifier, verified source and rights records, regenerated inventory and checksums, and a full decode/source-comparison pass. Do not silently substitute a live feed for a source snapshot. This repository ships no download scripts, benchmark framework or codec-specific results.
