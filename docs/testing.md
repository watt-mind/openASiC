# Testing and fixture policy

## Scaffold checks

Run `./scripts/check.sh` from the repository root. CI adds Linux, macOS,
Windows, MSRV 1.88, dependency policy, security checks, and a 90% workspace line
coverage threshold. Run `cargo build --release --locked` for the release build.
Tests exercise the capabilities JSON, human output, help/version, and rejection
of unimplemented commands. They do not assert ASiC processing exists.

## Planned interoperability tests

Use independent synthetic containers from DSS and libdigidocpp, recording tool
versions, profiles, generators, trust material, and expected coverage. Check
both directions: read their outputs and have them verify this tool's outputs.
A profile-policy disagreement is not automatically a cryptographic failure.
Run external counterparts locally or in isolated CI; do not upload private data.

Future regression tests must cover resource exhaustion, duplicate ZIP names,
path traversal, symlink escape, XML entities, reference ambiguity, wrapping,
unsigned entries, tampering, missing trust, revoked certificates, and missing or
invalid required evidence. Test observable boundaries instead of mirroring code.

## Fixtures and private inputs

Public fixtures belong in `tests/fixtures/` under its CC0 policy. None are
included yet. Record provenance, generation, profile, and expected outcome for
each. Never adapt a private document into a public fixture. Generate any needed
private keys at runtime and never commit keys or their complete PEM armour.

Private testing is not implemented. If added, require explicit opt-in and keep
it out of CI. Report aggregate counts and stable error-code buckets only; never
print private paths, names, metadata, payloads, hashes, certificates, or signer
information. Reproduce failures synthetically before adding public regressions.
