# Release policy

There are no published releases. Both crates use `publish = false`.
Development targets `develop`; `master` is reserved for reviewed stable releases.
Scaffolding does not provision GitHub, branch protection, registry publishing,
release credentials, or distribution workflows.

Before a first release, define supported ASiC profiles, stable CLI/JSON and exit
contracts, platform support, dependency licences, reproducible release checks,
and installation instructions. Document unsupported features prominently.
Require interoperability evidence and security review for implemented document
operations. Add packaging and release automation through a separate reviewed
change. Never advertise a release as a certification or legal-effect guarantee.
