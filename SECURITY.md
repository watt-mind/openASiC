# Security policy

## Reporting

Do not report vulnerabilities in public issues or attach real documents.
Use [GitHub private reporting][advisory], which is enabled for this repository.
If it is unavailable, request a private reporting channel from the maintainer
without disclosing vulnerability details publicly.
Describe the affected commit and a synthetic reproducer. Never include personal
information, credentials, private keys, or real signing material.

[advisory]: https://github.com/watt-mind/openASiC/security/advisories/new

## Current scope

There are no releases. Only help, version, and capabilities are implemented.
The scaffold does not read containers, extract files, sign, verify, or access
the network. Security fixes target `develop`.

## Requirements for future features

Treat ZIP entries, XML, manifests, certificates, signatures, and timestamp
responses as hostile input. Bound sizes, entry counts, compression ratios,
XML depth, and reference processing before allocation or expansion. Refuse
external XML entities and unapproved external references. Reject ambiguous
archive names. Extraction must prevent traversal, symlink escape, and clobber.
Preserve original payload bytes; never silently rewrite a signed container.

Keep structural validation and signing separate from verification. Report
coverage and caller-supplied trust context. Unperformed required checks cap
verification at indeterminate. A successful API call or signature primitive
cannot establish complete container validity, qualification, or legal effect.

No silent uploads, telemetry, or network lookups. Provider, timestamp,
revocation, and trust-list operations need explicit contracts and opt-in.
Remote signing transmits only the data its documented protocol requires;
private provider keys stay with the provider. Secret inputs must use protected
files or an explicitly documented secure input mechanism, never argv or logs.

Public fixtures must be wholly synthetic. Never enumerate or expose private
paths, filenames, contents, metadata, hashes, certificates, signer information,
or signature values. Private test reports contain aggregate counts and stable
error-code buckets only. Never derive fixtures from real documents.

Never commit secrets, `.env` files, private keys, or complete private-key PEM
armour lines. Generate test keys at runtime; never bypass secret-scanner rules.
