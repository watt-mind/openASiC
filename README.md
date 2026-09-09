# openASiC

A proposed local-first, agent-first Rust library and CLI for inspecting,
listing, structurally validating, extracting, creating, signing, and verifying
ETSI Associated Signature Containers (ASiC).

**Status: scaffold.** Only help, version, and `capabilities [--json]` are
implemented. No container parsing, extraction, creation, signing, timestamping,
or signature verification exists yet. There is no published release.

ASiC is the umbrella standard; ASiC-S and ASiC-E are container variants. The
first planned implementation targets **ASiC-E with XAdES**. ASiC-S and CAdES
support are separate roadmap items, not implied capabilities. This project is
independent and is not endorsed by ETSI or the European Commission.

## Try the scaffold

Build from this checkout with Rust 1.88 or newer:

```sh
cargo run --locked -p openasic-cli -- --help
cargo run --locked -p openasic-cli -- --version
cargo run --locked -p openasic-cli -- capabilities --json
```

The capabilities command reports the current implementation:

```json
{
  "schema_version": 1,
  "ok": true,
  "command": "capabilities",
  "data": {
    "project": "openASiC",
    "stage": "scaffold",
    "operations": []
  },
  "verified": false
}
```

An empty operation list means no document operations are available.
`verified: false` means no cryptographic verification was performed.

## Intended responsibilities

- Bounded ASiC container inspection and safe extraction.
- Explicit structural validation, separate from cryptographic verification.
- Container creation and signing with precise document coverage.
- Verification against caller-supplied trust and revocation evidence.
- Human-readable output and stable, documented JSON contracts.

The planned tool owns ASiC packaging, manifests, and signature-scope rules.
[openSzigno](https://github.com/watt-mind/openSzigno) owns ES3 dossiers,
[openKRX](https://github.com/watt-mind/openKRX) owns KRX packages, and
[openPapir](https://github.com/watt-mind/openPapir) owns correspondence workflows.
None is a build dependency. Reusable signature machinery may later be extracted
behind reviewed interfaces; no sibling parser or crypto stack is copied here.

A container format alone establishes no qualified signature or legal effect.
Creating or signing a container must never claim that it was verified.

## Development

The workspace contains `openasic-core` and `openasic-cli`. Both crates are
unpublished, use Rust edition 2024, and are licensed under [MIT](LICENSE).
The repository name is `openASiC`; the executable is lowercase `openasic`.

```sh
./scripts/check.sh
cargo build --release --locked
```

Pull requests target `develop`; `master` is reserved for stable releases.
See [contributing](CONTRIBUTING.md), [security](SECURITY.md), and the
[documentation index](docs/index.md). The [roadmap](docs/roadmap.md) separates
profile discovery, implementation, and independent interoperability testing.
