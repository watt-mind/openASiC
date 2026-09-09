# Roadmap

Only the scaffold is implemented: Rust workspace, help/version/capabilities,
and quality and documentation foundations. The following milestones are plans.

## 1. Specify one ASiC-E profile

Read the authoritative ETSI ASiC and XAdES standards. Record exact editions,
clauses, supported baseline levels, algorithms, container layout, mimetype and
manifest rules, signature coverage, and unsupported features. Distinguish
normative rules from observed producer behaviour and validator policy.

Deliver an evidence matrix, synthetic fixture plan, supported subset, resource
limits, and bounded implementation issues. Study DSS and libdigidocpp as
interoperability counterparts without copying their licensed implementation.
No parser, signing service, or qualification claim belongs in this discovery.

## 2. Bounded reader and safe extraction

Implement inspect/list/structural validation for the selected subset, then safe
extraction. Specify JSON schemas and exit/error codes before freezing them.
Test duplicate entries, path traversal, symlinks, compression bombs, malformed
XML, ambiguous references, and unsupported signature/container types.
Report signatures by presence only; reader success verifies nothing.

## 3. Verification and unsigned creation

Specify a verification policy and the boundary for any reusable openSzigno
components. Implement reference coverage, XAdES checks, trust, revocation, and
required timestamp validation without weakening missing-evidence outcomes.

Separately implement deterministic unsigned container creation with atomic,
no-clobber output. Preserve original payload bytes. Creation verifies nothing.
Unsupported profiles remain explicit, even if another application accepts them.

## 4. XAdES signing and interoperability

Add one signing backend with runtime-generated test keys, followed by opt-in
remote signing and RFC 3161 timestamp integration as separately specified work.
Do not assume a provider is usable until its authorization flow is supported.

Cross-test synthetic containers with DSS and libdigidocpp: create in each tool,
verify in the others, and document exact versions, profiles, trust inputs, and
policy differences. Compare coverage and reports, not only final verdicts.
Do not transfer existing ES3 signatures by repackaging extracted payloads.

## 5. ASiC-S and later profiles

Specify and implement ASiC-S independently, reusing safe archive primitives.
CAdES, additional baseline levels, and long-term evidence renewal need separate
acceptance matrices and tests. Do not advertise complete ASiC support before
its supported variants and profiles are demonstrably implemented.

## Work orchestration

Create one bounded issue per change with provenance, non-goals, owned paths,
acceptance criteria, tests, verification commands, and dependencies. Keep live
queue state in the configured private tracker, not this roadmap. This scaffold
creates no tickets, claims, provider accounts, or automatic dispatcher.
