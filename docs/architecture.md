# Architecture and CLI contract

## Current implementation

Rust edition 2024, MSRV 1.88, two unpublished crates:

| Crate | Current responsibility |
| --- | --- |
| `openasic-core` | Describe implemented capabilities without I/O. |
| `openasic-cli` | Expose help, version, and capabilities output. |

Supported invocations:

```sh
openasic --help
openasic --version
openasic capabilities
openasic capabilities --json
```

The capabilities JSON is one object on stdout with `schema_version: 1`,
`ok: true`, `command: "capabilities"`, and `verified: false`. Its `data` contains
`project: "openASiC"`, `stage: "scaffold"`, and `operations: []`.
It is not a promised response schema for future document commands.
Help/version/capabilities exit 0; missing commands, unknown commands, and invalid
arguments exit 2 with diagnostics on stderr and no document output on stdout.

## Planned format boundary

ASiC packages data and associated signature or timestamp evidence in a
constrained ZIP container. The first profile is ASiC-E with XAdES; exact ETSI
editions, baseline levels, algorithms, and accepted ZIP/XML features must be
recorded before implementation. ASiC-S, CAdES, and archival extension follow
separately. A ZIP reader or XML signature verifier alone is not ASiC validation.

Structural validation checks container layout and supported profile rules.
Cryptographic verification additionally checks references, signed coverage,
digests, signature values, signed certificate binding, paths, timestamps, and
revocation as required by the selected policy. Missing evidence is explicit;
unsupported checks must never produce a valid verdict.

List signed and unsigned entries distinctly. An individual signature need not
cover every payload. Validate manifest/reference resolution without filesystem
or network dereferencing. Bound decompression before allocation and XML before
traversal; reject duplicate or ambiguously normalised entry names. Extraction
requires an independent safe output boundary, no-clobber writes, and limits.

## Planned code ownership

The core will own bounded container parsing, models, and structural rules.
Authoring and verification should gain separate modules or crates when needed.
The CLI owns filesystem and opt-in network I/O, error rendering, and policy
configuration. No document modules are implemented in this scaffold.

openSzigno retains ES3 rules, openKRX retains KRX processing, and openPapir
retains correspondence workflows. There are no sibling dependencies today.
Candidate shared components include XAdES primitives, certificate validation,
timestamps, revocation, and remote-signing clients. Extract them only after a
concrete ASiC use case demonstrates reuse; keep container-specific scope checks
with each format. No cross-repository refactor is part of scaffolding.

## Verification and qualification

Only verification reports checks actually performed against explicit trust
material and policy. Structural success, successful signing, and cryptographic
validity are separate results. Neither a filename nor a provider assertion
establishes a qualified signature, and no verdict asserts legal effect.
Timestamp and long-term evidence requirements belong to an explicit profile
and policy; do not inherit another application's verdict policy accidentally.
