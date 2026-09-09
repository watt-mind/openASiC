# References and evidence policy

This scaffold does not claim ASiC conformance. These are discovery entry points,
not a completed profile specification or a licence to redistribute standards.

## Standards

- [ETSI electronic signatures standards activity][etsi]: locate EN 319 162
  (ASiC), EN 319 132 (XAdES), and EN 319 122 (CAdES).
- [European Commission eSignature FAQ][faq]: format and signature-level context.

[etsi]: https://portal.etsi.org/TB-SiteMap/esi/esi-activities
[faq]: https://ec.europa.eu/digital-building-blocks/sites/display/DIGITAL/eSignature%2BFAQ

## Interoperability counterparts

- [DSS](https://github.com/esig/dss): signature creation and validation library.
- [libdigidocpp](https://github.com/open-eid/libdigidocpp): native library and CLI.
- [DigiDoc4j](https://github.com/open-eid/digidoc4j): ASiC/XAdES tooling and profiles.

These repositories carry their own licences. Refer to their documentation and
use separate tools for interoperability; do not copy LGPL code into MIT files.
Record exact tested versions and policy configuration before citing results.

## Related independent projects

- [openSzigno](https://github.com/watt-mind/openSzigno): ES3 dossier tooling.
- [openKRX](https://github.com/watt-mind/openKRX): KRX package tooling.
- [openPapir](https://github.com/watt-mind/openPapir): correspondence workflows.

No sibling is currently a dependency. Shared interfaces require separate design.

## Evidence records

For every adopted rule, record issuer, title, edition/date, URL, relevant clause,
retrieval date, redistribution terms, and the supported claim. Distinguish
normative requirements, producer behaviour, validator policy, and inference.
Public availability does not establish redistribution rights. Use original
implementation and synthetic fixtures; keep unknowns explicit in the roadmap.
