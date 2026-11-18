# Protobuf Compression Corpus

A standalone, codec-neutral collection of serialized protobuf messages. Download the files under `datasets/` and read each file as one message. No build, generator, package or corpus-specific API is required.

Snapshot **2026-11-18-r1** contains **15 datasets, 803 message files, 474,131 source entries and 36,743,059 payload bytes**. There are 802 distinct payloads. The two small Google messages have identical bytes and different schemas; the duplicate is explicitly indexed.

| Dataset | Files | Source entries | Data terms |
|---|---:|---:|---|
| [cdc-covid-case-detailed](metadata/cdc-covid-case-detailed.json) | 64 | 16,384 | LicenseRef-US-Government-Public-Domain |
| [cdc-nndss-disease](metadata/cdc-nndss-disease.json) | 64 | 16,384 | ODbL-1.0 |
| [cdc-places-health](metadata/cdc-places-health.json) | 64 | 16,384 | LicenseRef-US-Government-Public-Domain |
| [google-message1-proto2](metadata/google-message1-proto2.json) | 1 | 1 | BSD-3-Clause |
| [google-message1-proto3](metadata/google-message1-proto3.json) | 1 | 1 | BSD-3-Clause |
| [google-message2](metadata/google-message2.json) | 1 | 1 | BSD-3-Clause |
| [industry-unemployment](metadata/industry-unemployment.json) | 10 | 1,708 | LicenseRef-US-Government-Public-Domain |
| [sao](metadata/sao.json) | 253 | 258,944 | LicenseRef-US-Government-Public-Domain |
| [us-county-stats](metadata/us-county-stats.json) | 45 | 22,541 | CC0-1.0 |
| [us-federal-agencies](metadata/us-federal-agencies.json) | 4 | 111 | CC0-1.0 |
| [us-hospitals](metadata/us-hospitals.json) | 22 | 5,419 | CC0-1.0 |
| [us-public-schools](metadata/us-public-schools.json) | 200 | 102,268 | CC0-1.0 |
| [us-school-districts](metadata/us-school-districts.json) | 39 | 19,714 | CC0-1.0 |
| [usgs-earthquakes](metadata/usgs-earthquakes.json) | 23 | 11,349 | LicenseRef-US-Government-Public-Domain |
| [weather](metadata/weather.json) | 12 | 2,922 | LicenseRef-US-Government-Public-Domain |

Converted public records use a schema-specific `Batch` with repeated record messages. The three Google benchmark files are original raw messages, without a batch wrapper. Every file's schema and fully qualified type are listed in [MANIFEST.json](MANIFEST.json).

## Verify and inspect

```sh
sha256sum -c SHA256SUMS
protoc -I schemas --decode=pbcorpus.cdc_places.v2.Batch \
  schemas/public-records/cdc-places-health.proto \
  < datasets/public-records/cdc-places-health/0000.pb
```

`SHA256SUMS` covers every release file except itself. [FORMAT.md](FORMAT.md) defines the index and metadata. Source snapshots are included as gzip files under `provenance/source-snapshots/`, with both compressed and uncompressed checksums in metadata; they are provenance material, not benchmark payloads.

## Source and reuse

Data are published records converted into protobuf, except the original Google benchmark payloads. This is not a capture of production RPC traffic. Read [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) and each dataset's metadata before redistributing. Original corpus contributions use [MIT](LICENSE); third-party data retain their stated terms. In particular, the NNDSS derivative database is **ODbL-1.0**, not public domain or MIT.

Source: CDC for the three named CDC datasets. The original CDC materials are available without charge at the linked source sites. Use of this corpus and its links does not imply endorsement by CDC, ATSDR, HHS or the United States Government. These are selected historical benchmark records, not official current statistics. No other source agency or contributor endorsement is implied.

[EXCLUDED.json](EXCLUDED.json) identifies development datasets omitted because their source or redistribution basis was not established, and records the replacements for broken datasets. [RELEASE.md](RELEASE.md) describes distribution of this snapshot without private development history.
