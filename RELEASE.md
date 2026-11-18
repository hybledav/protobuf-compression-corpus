# Releasing this snapshot

Distribute the checked 2026-11-18-r1 tree or its prepared archive, including all schemas, source snapshots, metadata, licenses, notices and SHA256SUMS. Check the archive SHA-256 supplied alongside it, extract it, then run `sha256sum -c SHA256SUMS` inside the extracted directory. Benchmark only files under `datasets/`.

The existing repository is private. Its development history contains data and notices excluded from this snapshot. Removing them from the current tree does not remove them from earlier Git objects. Publish this snapshot from a new history initialized from the checked export, or distribute its clean archive while keeping the development repository private. Making the existing repository public requires separate history clearance or cleanup, including relevant refs and pull-request history. This update does not change repository visibility, publish a release, or clear historical material.

The source rights evidence and required notices for every included dataset are recorded in metadata and THIRD_PARTY_NOTICES.md. An exclusion means that this review did not establish a sufficiently traceable source/permission chain, not an assertion that the source is unlawful. No permission requests were sent to third parties. A later addition requires its own source, conversion and redistribution review.
