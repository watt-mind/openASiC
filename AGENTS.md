# openASiC

A local-first Rust ASiC toolkit scaffold. Read [README.md](README.md),
[architecture](docs/architecture.md), [roadmap](docs/roadmap.md),
[contributing](CONTRIBUTING.md), and [security](SECURITY.md) before changes.

## Boundaries

- Only help, version, and `capabilities [--json]` exist today. Never advertise
  planned parsing, extraction, creation, signing, or verification as implemented.
- ASiC-S and ASiC-E are distinct variants. Initial implementation is planned for
  ASiC-E with XAdES. Declare supported profiles and reject unsupported variants;
  never infer general ASiC or CAdES support from that subset.
- Keep ES3 in openSzigno, KRX in openKRX, and correspondence in openPapir.
  No unpublished sibling dependencies or copied parsers. Extract shared crypto
  only after demonstrating reuse and reviewing the versioned interface.
- Inspection, structural validation, creation, and signing verify nothing.
  Only a dedicated verification path may report cryptographic results. A valid
  verdict requires every required check; an unperformed required check caps it
  at indeterminate. Retain scope and supplied trust context. Never infer QES,
  authenticity of unrelated entries, or legal effect from a file extension,
  provider name, successful signing request, or valid cryptographic primitive.
- Signature coverage is format-specific. Check ASiC references and manifests;
  do not transplant ES3 scope rules. Preserve original bytes and distinguish
  signed content from unsigned extras. Never silently repack a signed archive.
- Real documents are private. Never enumerate, print, hash, log, commit, or
  disclose private filenames, paths, metadata, payloads, hashes, certificates,
  signer data, or signature values. Private-corpus reporting is aggregate counts
  and stable error-code buckets only. Never derive public fixtures from it.
- Synthetic fixtures only, with provenance and a redistributable licence.
  Never commit keys, complete private-key PEM armour lines, secrets, or `.env`
  files. Generate test keys at runtime. Never allowlist a secret-scanner rule.
  Future key/PIN/token/passphrase handling must keep secrets out of argv and
  diagnostics; remote signing keys remain with their provider.
- Bound ZIP expansion, entry count, compression ratio, XML depth, and input size.
  Refuse ambiguous duplicate names and unsafe references. Extraction must prevent
  traversal, symlink escape, and overwrites. Never relax limits for acceptance.
- No implicit network access. Provider, TSA, revocation, and trusted-list
  integration each need documented opt-in and trust-bootstrap semantics.

## Work ownership

Use one specified issue per `codex/` branch, with pull requests to `develop`.
`master` is the stable branch. Give concurrent contributors explicit ownership,
preserve others' changes, and keep follow-ups in separate issues. Public issues,
commits and PRs must contain no private tracker content, local maintainer paths,
or real documents. Vulnerabilities follow [SECURITY.md](SECURITY.md).

## Checks

```sh
./scripts/check.sh
cargo build --release --locked
cargo run --locked -p openasic-cli -- capabilities --json
```

CI adds platform/MSRV checks, coverage, dependency policy, and security scans.
Use meaningful behaviour and boundary tests. Keep files within the file-length
check and use Conventional Commits. Read [testing](docs/testing.md) before
adding fixtures. Do not copy LGPL implementation code into MIT sources.

## Factory orchestration

For an explicitly requested orchestration run, read
[the orchestrator instructions](docs/orchestrator.md) and
[runner setup](docs/factory.md). Resolve private host routing and live ticket
readiness before claims; the roadmap is not a dispatch queue. Manual
orchestration is opt-in. Scaffolding is not permission to launch workers or
unattended dispatch.
